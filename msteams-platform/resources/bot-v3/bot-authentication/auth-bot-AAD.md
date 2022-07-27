---
title: Authentification pour les bots à l’aide d’Azure Active Directory
description: Décrit l’authentification Azure AD dans Teams et comment l’utiliser dans vos bots
keywords: bots d’authentification Teams Azure AD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: 2b467f6a7b4678110dece3b54a67227df6beeaf7
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035162"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Authentifier un utilisateur dans un bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Il existe de nombreux services que vous souhaiterez peut-être utiliser dans votre application Teams, et la plupart de ces services nécessitent une authentification et une autorisation pour obtenir l’accès. Les services incluent Facebook, Twitter et Teams. Les utilisateurs de Teams disposent d’informations de profil utilisateur stockées dans Azure Active Directory à l’aide de Microsoft Graph. Cette rubrique se concentre sur l’authentification à l’aide d’Azure AD pour obtenir l’accès.
OAuth 2.0 est une norme ouverte pour l’authentification utilisée par Azure AD et de nombreux autres fournisseurs de services. La compréhension d’OAuth 2.0 est un prérequis pour l’utilisation de l’authentification dans Teams et Azure AD. Les exemples suivants utilisent le flux d’octroi implicite OAuth 2.0 pour finalement lire les informations de profil de l’utilisateur à partir d’Azure AD et de Microsoft Graph.

Le flux d’authentification décrit dans cette rubrique est similaire aux onglets, à ceci près que les onglets peuvent utiliser le flux d’authentification web et que les bots exigent que l’authentification soit pilotée à partir du code. Les concepts de cette rubrique seront également utiles lors de l’implémentation de l’authentification à partir de la plateforme mobile.

Pour obtenir une vue d’ensemble du flux d’authentification pour les bots, consultez la rubrique [Flux d’authentification dans les bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

## <a name="configuring-identity-providers"></a>Configuration des fournisseurs d’identité

Consultez la rubrique [Configurer les fournisseurs d’identité](~/concepts/authentication/configure-identity-provider.md) pour obtenir des instructions détaillées sur la configuration des URL de redirection de rappel OAuth 2.0 lors de l’utilisation d’Azure Active Directory en tant que fournisseur d’identité.

## <a name="initiate-authentication-flow"></a>Lancer le flux d’authentification

Le flux d’authentification doit être déclenché par une action de l’utilisateur. N’ouvrez pas la fenêtre contextuelle d’authentification automatiquement, car elle peut déclencher le bloqueur de fenêtres contextuelles du navigateur et confondre l’utilisateur.

## <a name="add-ui-to-start-authentication"></a>Ajouter une interface utilisateur pour démarrer l’authentification

Ajoutez l’interface utilisateur au bot pour permettre à l’utilisateur de se connecter si nécessaire. Ici, elle est effectuée à partir d’une carte miniature, en TypeScript :

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

Trois boutons ont été ajoutés à la carte Hero : Se connecter, afficher le profil et se déconnecter.

## <a name="sign-the-user-in"></a>Connecter l’utilisateur

En raison de la validation qui doit être effectuée pour des raisons de sécurité et de la prise en charge des versions mobiles de Teams, le code n’est pas affiché ici, mais [voici un exemple de code qui lance le processus lorsque l’utilisateur appuie sur le bouton Connexion.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)

La validation et la prise en charge mobile sont expliquées dans la rubrique [Flux d’authentification dans les bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).

Veillez à ajouter le domaine de votre URL de redirection d’authentification à la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section du manifeste. Si vous ne vous connectez pas, la fenêtre contextuelle n’apparaît pas.

## <a name="showing-user-profile-information"></a>Affichage des informations de profil utilisateur

Bien que l’obtention d’un jeton d’accès soit difficile en raison de toutes les transitions entre les différents sites web et des problèmes de sécurité qui doivent être résolus, une fois que vous disposez d’un jeton, l’obtention d’informations à partir d’Azure Active Directory est simple. Le bot effectue un appel au `me` point de terminaison Graph avec le jeton d’accès. Graph répond avec les informations utilisateur de la personne qui s’est connectée. Les informations de la réponse sont utilisées pour construire une carte de bot et être envoyées.

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

Pour obtenir un exemple de code montrant le processus d’authentification du bot, consultez :

* [Exemple d’authentification de bot Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
