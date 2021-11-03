---
title: Authentification pour les bots utilisant Azure Active Directory
description: Décrit Azure AD l’authentification Teams et comment l’utiliser dans vos bots
keywords: Bots d’authentification teams AAD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: 1f13e561e94029f007ff055627f335d00ee1c441
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720070"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Authentifier un utilisateur dans un bot Microsoft Teams client

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Il existe de nombreux services que vous souhaitez peut-être consommer dans votre application Teams, et la plupart de ces services nécessitent une authentification et une autorisation pour obtenir l’accès. Les services incluent Facebook, Twitter et Teams. Les utilisateurs Teams ont des informations de profil utilisateur stockées dans Azure Active Directory (Azure AD) à l’aide de Microsoft Graph. Cette rubrique se concentre sur l’authentification à l Azure AD pour obtenir l’accès.
OAuth 2.0 est une norme ouverte pour l’authentification utilisée par Azure AD et de nombreux autres fournisseurs de services. La compréhension d’OAuth 2.0 est une condition préalable pour travailler avec l’authentification dans Teams et Azure AD. Les exemples suivants utilisent le flux d’octroi implicite OAuth 2.0 pour finir par lire les informations de profil de l’utilisateur à partir de Azure AD et Microsoft Graph.

Le flux d’authentification décrit dans cette rubrique est similaire aux onglets, sauf que les onglets peuvent utiliser le flux d’authentification web et que les bots nécessitent que l’authentification soit pilotée à partir du code. Les concepts de cette rubrique seront également utiles lors de l’implémentation de l’authentification à partir de la plateforme mobile.

Pour une vue d’ensemble du flux d’authentification pour les bots, consultez la rubrique [Flux d’authentification dans les bots.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)

## <a name="configuring-identity-providers"></a>Configuration des fournisseurs d’identité

Consultez la rubrique [Configurer](~/concepts/authentication/configure-identity-provider.md) les fournisseurs d’identité pour obtenir la procédure détaillée de configuration des URL de redirection de rappel OAuth 2.0 lors de l’utilisation de Azure Active Directory comme fournisseur d’identité.

## <a name="initiate-authentication-flow"></a>Démarrer le flux d’authentification

Le flux d’authentification doit être déclenché par une action de l’utilisateur. N’ouvrez pas automatiquement la fenêtre d’authentification, car elle peut déclencher le bloqueur de fenêtres d’authentification du navigateur et dérouter l’utilisateur.

## <a name="add-ui-to-start-authentication"></a>Ajouter une interface utilisateur pour démarrer l’authentification

Ajoutez une interface utilisateur au bot pour permettre à l’utilisateur de se connecter si nécessaire. Ici, elle est effectuée à partir d’une carte miniature, dans TypeScript :

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

Trois boutons ont été ajoutés à la carte Hero : se connectez, affichez le profil et se connectez.

## <a name="sign-the-user-in"></a>Connectez l’utilisateur

En raison de la validation qui doit être effectuée pour des raisons de sécurité et de la prise en charge des versions mobiles de Teams, le code n’est pas affiché ici, mais voici un exemple de code qui lance le processus lorsque [l’utilisateur](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)appuie sur le bouton Se connecter. .

La validation et la prise en charge mobile sont expliquées dans la rubrique [Flux d’authentification dans les bots.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)

N’oubliez pas d’ajouter le domaine de votre URL de redirection d’authentification à [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) la section du manifeste. Si vous ne vous connectez pas, la fenêtre popup ne s’affiche pas.

## <a name="showing-user-profile-information"></a>Affichage des informations de profil utilisateur

Bien que l’obtention d’un jeton d’accès soit difficile en raison de toutes les transitions entre différents sites web et des problèmes de sécurité qui doivent être résolus, une fois que vous avez un jeton, l’obtention d’informations auprès de Azure Active Directory est simple. Le bot appelle le point de terminaison `me` Graph avec le jeton d’accès. Graph répond avec les informations utilisateur de la personne qui s’est connectée. Les informations de la réponse sont utilisées pour construire une carte de bot et envoyées.

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

Si l’utilisateur n’est pas inscrit, il est invité à le faire.

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

Pour obtenir un exemple de code montrant le processus d’authentification du bot, voir :

* [exemple Microsoft Teams’authentification de bot](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
