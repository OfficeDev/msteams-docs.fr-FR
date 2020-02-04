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
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="2a37d-104">Authentifier un utilisateur dans un bot Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="2a37d-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="2a37d-105">Il est possible que vous souhaitiez consommer de nombreux services au sein de votre application teams et que la plupart de ces services requièrent une authentification et une autorisation pour accéder au service.</span><span class="sxs-lookup"><span data-stu-id="2a37d-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="2a37d-106">Les services incluent Facebook, Twitter et des équipes de cours.</span><span class="sxs-lookup"><span data-stu-id="2a37d-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="2a37d-107">Les utilisateurs de teams disposent d’informations de profil utilisateur stockées dans Azure Active Directory (Azure AD) à l’aide de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2a37d-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="2a37d-108">Cet article se concentre sur l’authentification à l’aide d’Azure AD pour accéder à ces informations.</span><span class="sxs-lookup"><span data-stu-id="2a37d-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="2a37d-109">OAuth 2,0 est une norme ouverte pour l’authentification utilisée par Azure AD et de nombreux autres fournisseurs de services.</span><span class="sxs-lookup"><span data-stu-id="2a37d-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="2a37d-110">La présentation de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans teams et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a37d-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="2a37d-111">Les exemples ci-dessous utilisent le flux d’octroi implicite OAuth 2,0 avec l’objectif de lire les informations de profil de l’utilisateur à partir d’Azure AD et de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2a37d-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="2a37d-112">Le flux d’authentification décrit dans cet article est très similaire à celui des onglets, mais les onglets peuvent utiliser un flux d’authentification basé sur le Web, et les robots nécessitent une authentification à partir du code.</span><span class="sxs-lookup"><span data-stu-id="2a37d-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="2a37d-113">Les concepts décrits dans cet article seront également utiles lors de l’implémentation de l’authentification à partir de la plateforme mobile.</span><span class="sxs-lookup"><span data-stu-id="2a37d-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="2a37d-114">Pour obtenir une vue d’ensemble du flux d’authentification des robots, consultez la rubrique [flux d’authentification dans les robots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="2a37d-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="2a37d-115">Configuration des fournisseurs d’identité</span><span class="sxs-lookup"><span data-stu-id="2a37d-115">Configuring identity providers</span></span>

<span data-ttu-id="2a37d-116">Consultez la rubrique [configure Identity Providers](~/concepts/authentication/configure-identity-provider.md) pour obtenir des instructions détaillées sur la configuration des URL de redirection de rappel OAuth 2,0 lors de l’utilisation d’Azure Active Directory en tant que fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="2a37d-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="2a37d-117">Activer le flux d’authentification</span><span class="sxs-lookup"><span data-stu-id="2a37d-117">Initiate authentication flow</span></span>

<span data-ttu-id="2a37d-118">Le flux d’authentification doit être déclenché par une action de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2a37d-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="2a37d-119">Vous ne devez pas ouvrir automatiquement la fenêtre contextuelle d’authentification, car cela déclenchera probablement le blocage des fenêtres publicitaires intempestives du navigateur, ainsi que la confusion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2a37d-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="2a37d-120">Ajouter une interface utilisateur pour démarrer l’authentification</span><span class="sxs-lookup"><span data-stu-id="2a37d-120">Add UI to start authentication</span></span>

<span data-ttu-id="2a37d-121">Ajoutez l’interface utilisateur au bot pour permettre à l’utilisateur de se connecter lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2a37d-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="2a37d-122">Cette opération est exécutée à partir d’une carte miniature, dans la machine à écrire :</span><span class="sxs-lookup"><span data-stu-id="2a37d-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

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

<span data-ttu-id="2a37d-123">Trois boutons ont été ajoutés à la carte héros : se connecter, afficher le profil et se déconnecter.</span><span class="sxs-lookup"><span data-stu-id="2a37d-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="2a37d-124">Signature de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2a37d-124">Sign the user in</span></span>

<span data-ttu-id="2a37d-125">En raison de la validation qui doit être effectuée pour des raisons de sécurité et de la prise en charge des versions mobiles de teams, le code n’est pas affiché ici, mais [Voici un exemple du code qui lance le processus lorsque l’utilisateur appuie sur le bouton de connexion.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span><span class="sxs-lookup"><span data-stu-id="2a37d-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="2a37d-126">La validation et la prise en charge mobile sont expliquées dans la rubrique [flux d’authentification dans les robots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="2a37d-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="2a37d-127">N’oubliez pas d’ajouter le domaine de votre URL de redirection de [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) l’authentification à la section du manifeste.</span><span class="sxs-lookup"><span data-stu-id="2a37d-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="2a37d-128">Si ce n’est pas le cas, le menu contextuel de connexion n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="2a37d-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="2a37d-129">Affichage des informations de profil utilisateur</span><span class="sxs-lookup"><span data-stu-id="2a37d-129">Showing user profile information</span></span>

<span data-ttu-id="2a37d-130">Même si l’obtention d’un jeton d’accès est difficile en raison de toutes les transitions entre différents sites Web et des problèmes de sécurité à résoudre, une fois que vous avez un jeton, obtenir des informations à partir d’Azure Active Directory est simple.</span><span class="sxs-lookup"><span data-stu-id="2a37d-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="2a37d-131">Le bot appelle le point de terminaison `me` Graph avec le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="2a37d-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="2a37d-132">Graph répond avec les informations utilisateur de la personne qui a ouvert une session.</span><span class="sxs-lookup"><span data-stu-id="2a37d-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="2a37d-133">Les informations de la réponse permettent de construire une carte bot et de l’envoyer.</span><span class="sxs-lookup"><span data-stu-id="2a37d-133">Information from the response is used to construct a bot card and sent.</span></span>

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

<span data-ttu-id="2a37d-134">Si l’utilisateur n’est pas connecté, il est invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="2a37d-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="2a37d-135">Déconnexion de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2a37d-135">Sign the user out</span></span>

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

## <a name="other-samples"></a><span data-ttu-id="2a37d-136">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="2a37d-136">Other samples</span></span>

<span data-ttu-id="2a37d-137">Pour obtenir un exemple de code illustrant le processus d’authentification du bot, voir :</span><span class="sxs-lookup"><span data-stu-id="2a37d-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="2a37d-138">Exemple d’authentification Microsoft teams bot</span><span class="sxs-lookup"><span data-stu-id="2a37d-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
