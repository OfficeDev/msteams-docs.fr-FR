---
title: Authentification pour les robots à l’aide d’Azure Active Directory
description: Décrit l’authentification Azure AD dans teams et son utilisation dans vos robots
keywords: les robots d’authentification des équipes AAD
ms.date: 03/01/2018
ms.openlocfilehash: 268af02c51b21b65214bce4673b54ac564a125ae
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673844"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Authentifier un utilisateur dans un bot Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Il est possible que vous souhaitiez consommer de nombreux services au sein de votre application teams et que la plupart de ces services requièrent une authentification et une autorisation pour accéder au service. Les services incluent Facebook, Twitter et des équipes de cours. Les utilisateurs de teams disposent d’informations de profil utilisateur stockées dans Azure Active Directory (Azure AD) à l’aide de Microsoft Graph. Cet article se concentre sur l’authentification à l’aide d’Azure AD pour accéder à ces informations.

OAuth 2,0 est une norme ouverte pour l’authentification utilisée par Azure AD et de nombreux autres fournisseurs de services. La présentation de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans teams et Azure AD. Les exemples ci-dessous utilisent le flux d’octroi implicite OAuth 2,0 avec l’objectif de lire les informations de profil de l’utilisateur à partir d’Azure AD et de Microsoft Graph.

Le flux d’authentification décrit dans cet article est très similaire à celui des onglets, mais les onglets peuvent utiliser un flux d’authentification basé sur le Web, et les robots nécessitent une authentification à partir du code. Les concepts décrits dans cet article seront également utiles lors de l’implémentation de l’authentification à partir de la plateforme mobile.

Pour obtenir une vue d’ensemble du flux d’authentification des robots, consultez la rubrique [flux d’authentification dans les robots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

## <a name="configuring-identity-providers"></a>Configuration des fournisseurs d’identité

Consultez la rubrique [configure Identity Providers](~/concepts/authentication/configure-identity-provider.md) pour obtenir des instructions détaillées sur la configuration des URL de redirection de rappel OAuth 2,0 lors de l’utilisation d’Azure Active Directory en tant que fournisseur d’identité.

## <a name="initiate-authentication-flow"></a>Activer le flux d’authentification

Le flux d’authentification doit être déclenché par une action de l’utilisateur. Vous ne devez pas ouvrir automatiquement la fenêtre contextuelle d’authentification, car cela déclenchera probablement le blocage des fenêtres publicitaires intempestives du navigateur, ainsi que la confusion de l’utilisateur.

## <a name="add-ui-to-start-authentication"></a>Ajouter une interface utilisateur pour démarrer l’authentification

Ajoutez l’interface utilisateur au bot pour permettre à l’utilisateur de se connecter lorsque cela est nécessaire. Cette opération est exécutée à partir d’une carte miniature, dans la machine à écrire :

```typescript
// Show prompt of options
protected async promptForAction(session: builder.Session): Promise<void> {
    let msg = new builder.Message(session)
        .addAttachment(new builder.ThumbnailCard(session)
            .title(this.providerDisplayName)
            .buttons([
                 builder.CardAction.messageBack(session, "{}", "Sign in")
                     .text("SignIn")
                     .displayText("Sign in"),
                  builder.CardAction.messageBack(session, "{}", "Show profile")
                     .text("ShowProfile")
                     .displayText("Show profile"),
                  builder.CardAction.messageBack(session, "{}", "Sign out")
                     .text("SignOut")
                     .displayText("Sign out"),
            ]));
    session.send(msg);
}
```

Trois boutons ont été ajoutés à la carte héros : se connecter, afficher le profil et se déconnecter.

## <a name="sign-the-user-in"></a>Signature de l’utilisateur

En raison de la validation qui doit être effectuée pour des raisons de sécurité et de la prise en charge des versions mobiles de teams, le code n’est pas affiché ici, mais [Voici un exemple du code qui lance le processus lorsque l’utilisateur appuie sur le bouton de connexion.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).

La validation et la prise en charge mobile sont expliquées dans la rubrique [flux d’authentification dans les robots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

N’oubliez pas d’ajouter le domaine de votre URL de redirection de [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) l’authentification à la section du manifeste. Si ce n’est pas le cas, le menu contextuel de connexion n’apparaît pas.

## <a name="showing-user-profile-information"></a>Affichage des informations de profil utilisateur

Même si l’obtention d’un jeton d’accès est difficile en raison de toutes les transitions entre différents sites Web et des problèmes de sécurité à résoudre, une fois que vous avez un jeton, obtenir des informations à partir d’Azure Active Directory est simple. Le bot appelle le point de terminaison `me` Graph avec le jeton d’accès. Graph répond avec les informations utilisateur de la personne qui a ouvert une session. Les informations de la réponse permettent de construire une carte bot et de l’envoyer.

```typescript
// Show user profile
protected async showUserProfile(session: builder.Session): Promise<void> {
    let azureADApi = this.authProvider as AzureADv1Provider;
    let userToken = this.getUserToken(session);

    if (userToken) {
        let profile = await azureADApi.getProfileAsync(userToken.accessToken);
        let profileCard = new builder.ThumbnailCard()
            .title(profile.displayName)
            .subtitle(profile.mail)
            .text(`${profile.jobTitle}<br/> ${profile.officeLocation}`);
        session.send(new builder.Message().addAttachment(profileCard));
    } else {
        session.send("Please sign in to AzureAD so I can access your profile.");
    }

    await this.promptForAction(session);
}

// Helper function to make the Graph API call
public async getProfileAsync(accessToken: string): Promise<any> {
    let options = {
        url: "https://graph.microsoft.com/v1.0/me",
        json: true,
        headers: {
            "Authorization": `Bearer ${accessToken}`,
        },
    };
    return await request.get(options);
}
```

Si l’utilisateur n’est pas connecté, il est invité à le faire.

## <a name="sign-the-user-out"></a>Déconnexion de l’utilisateur

```typescript
// Handle user logout request
private async handleLogout(session: builder.Session): Promise<void> {
    if (!utils.getUserToken(session, this.providerName)) {
        session.send(`You're already signed out of ${this.providerDisplayName}.`);
    } else {
        utils.setUserToken(session, this.providerName, null);
        session.send(`You're now signed out of ${this.providerDisplayName}.`);
    }

    await this.promptForAction(session);
}
```

## <a name="other-samples"></a>Autres exemples

Pour obtenir un exemple de code illustrant le processus d’authentification du bot, voir :

* [Exemple d’authentification Microsoft teams bot](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
