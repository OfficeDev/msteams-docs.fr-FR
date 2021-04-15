---
title: Authentification pour les bots à l'aide d'Azure Active Directory
description: Décrit l'authentification Azure AD dans Teams et comment l'utiliser dans vos bots
keywords: Bots d'authentification Teams AAD
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: f772ef84282c3b8e1ee3e6aa96b47bf12caaa4dd
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696681"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="72fc4-104">Authentifier un utilisateur dans un bot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="72fc4-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="72fc4-105">Il existe de nombreux services que vous souhaitez peut-être consommer dans votre application Teams, et la plupart de ces services nécessitent une authentification et une autorisation pour accéder au service.</span><span class="sxs-lookup"><span data-stu-id="72fc4-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="72fc4-106">Les services incluent Facebook, Twitter et bien entendu Teams.</span><span class="sxs-lookup"><span data-stu-id="72fc4-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="72fc4-107">Les utilisateurs de Teams ont des informations de profil utilisateur stockées dans Azure Active Directory (Azure AD) à l'aide de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="72fc4-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="72fc4-108">Cet article se concentre sur l'authentification à l'aide d'Azure AD pour accéder à ces informations.</span><span class="sxs-lookup"><span data-stu-id="72fc4-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="72fc4-109">OAuth 2.0 est une norme ouverte pour l'authentification utilisée par Azure AD et de nombreux autres fournisseurs de services.</span><span class="sxs-lookup"><span data-stu-id="72fc4-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="72fc4-110">La compréhension d'OAuth 2.0 est une condition préalable à l'authentification dans Teams et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72fc4-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="72fc4-111">Les exemples ci-dessous utilisent le flux d'octroi implicite OAuth 2.0 pour finir par lire les informations de profil de l'utilisateur à partir d'Azure AD et de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="72fc4-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="72fc4-112">Le flux d'authentification décrit dans cet article est très similaire à celui des onglets, sauf que les onglets peuvent utiliser un flux d'authentification web et que les bots nécessitent l'authentification basée sur le code.</span><span class="sxs-lookup"><span data-stu-id="72fc4-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="72fc4-113">Les concepts de cet article seront également utiles lors de l'implémentation de l'authentification à partir de la plateforme mobile.</span><span class="sxs-lookup"><span data-stu-id="72fc4-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="72fc4-114">Pour une vue d'ensemble du flux d'authentification pour les bots, consultez la rubrique [Flux d'authentification dans les bots.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="72fc4-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="72fc4-115">Configuration des fournisseurs d'identité</span><span class="sxs-lookup"><span data-stu-id="72fc4-115">Configuring identity providers</span></span>

<span data-ttu-id="72fc4-116">Consultez la rubrique [Configurer](~/concepts/authentication/configure-identity-provider.md) les fournisseurs d'identité pour obtenir la procédure détaillée de configuration des URL de redirection de rappel OAuth 2.0 lors de l'utilisation d'Azure Active Directory en tant que fournisseur d'identité.</span><span class="sxs-lookup"><span data-stu-id="72fc4-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="72fc4-117">Démarrer le flux d'authentification</span><span class="sxs-lookup"><span data-stu-id="72fc4-117">Initiate authentication flow</span></span>

<span data-ttu-id="72fc4-118">Le flux d'authentification doit être déclenché par une action de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="72fc4-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="72fc4-119">Vous ne devez pas ouvrir automatiquement la fenêtre d'authentification, car cela est susceptible de déclencher le bloqueur de fenêtres d'authentification du navigateur et de dérouter l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="72fc4-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="72fc4-120">Ajouter une interface utilisateur pour démarrer l'authentification</span><span class="sxs-lookup"><span data-stu-id="72fc4-120">Add UI to start authentication</span></span>

<span data-ttu-id="72fc4-121">Ajoutez une interface utilisateur au bot pour permettre à l'utilisateur de se connecter en cas de besoin.</span><span class="sxs-lookup"><span data-stu-id="72fc4-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="72fc4-122">Ici, elle est effectuée à partir d'une carte miniature, dans TypeScript :</span><span class="sxs-lookup"><span data-stu-id="72fc4-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

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

<span data-ttu-id="72fc4-123">Trois boutons ont été ajoutés à la carte Hero : se connectez, affichez le profil et se connectez.</span><span class="sxs-lookup"><span data-stu-id="72fc4-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="72fc4-124">Connectez l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="72fc4-124">Sign the user in</span></span>

<span data-ttu-id="72fc4-125">En raison de la validation qui doit être effectuée pour des raisons de sécurité et de la prise en charge des versions mobiles de Teams, le code n'est pas affiché ici, mais voici un exemple de code qui lance le processus lorsque [l'utilisateur](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)appuie sur le bouton Se connecter. .</span><span class="sxs-lookup"><span data-stu-id="72fc4-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="72fc4-126">La validation et la prise en charge mobile sont expliquées dans la rubrique [Flux d'authentification dans les bots.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="72fc4-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="72fc4-127">N'oubliez pas d'ajouter le domaine de votre URL de redirection d'authentification à [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) la section du manifeste.</span><span class="sxs-lookup"><span data-stu-id="72fc4-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="72fc4-128">Si ce n'est pas le cas, la fenêtre de connexion ne s'affiche pas.</span><span class="sxs-lookup"><span data-stu-id="72fc4-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="72fc4-129">Affichage des informations de profil utilisateur</span><span class="sxs-lookup"><span data-stu-id="72fc4-129">Showing user profile information</span></span>

<span data-ttu-id="72fc4-130">Bien que l'obtention d'un jeton d'accès soit difficile en raison de toutes les transitions entre différents sites web et des problèmes de sécurité qui doivent être résolus, une fois que vous avez un jeton, l'obtention d'informations auprès d'Azure Active Directory est simple.</span><span class="sxs-lookup"><span data-stu-id="72fc4-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="72fc4-131">Le bot effectue un appel au point de terminaison `me` Graph avec le jeton d'accès.</span><span class="sxs-lookup"><span data-stu-id="72fc4-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="72fc4-132">Graph répond avec les informations utilisateur de la personne qui s'est connectée.</span><span class="sxs-lookup"><span data-stu-id="72fc4-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="72fc4-133">Les informations de la réponse sont utilisées pour construire une carte bot et envoyées.</span><span class="sxs-lookup"><span data-stu-id="72fc4-133">Information from the response is used to construct a bot card and sent.</span></span>

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

<span data-ttu-id="72fc4-134">Si l'utilisateur n'est pas inscrit, il est invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="72fc4-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="72fc4-135">Déconnexion de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="72fc4-135">Sign the user out</span></span>

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

## <a name="other-samples"></a><span data-ttu-id="72fc4-136">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="72fc4-136">Other samples</span></span>

<span data-ttu-id="72fc4-137">Pour obtenir un exemple de code montrant le processus d'authentification du bot, voir :</span><span class="sxs-lookup"><span data-stu-id="72fc4-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="72fc4-138">Exemple d'authentification de bot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="72fc4-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
