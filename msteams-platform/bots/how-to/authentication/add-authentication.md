---
title: Ajouter l’authentification à votre bot Teams
author: clearab
description: Comment ajouter l’authentification OAuth à un bot dans Microsoft Teams.
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 71a24dad47b3686d207df3f4e3521bbe46508cb9
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585868"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="8b3df-103">Ajouter l’authentification à votre bot Teams</span><span class="sxs-lookup"><span data-stu-id="8b3df-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="8b3df-104">Parfois, vous devrez peut-être créer des bots dans Microsoft Teams qui peuvent accéder aux ressources pour le compte de l’utilisateur, telles qu’un service de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8b3df-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="8b3df-105">Cet article montre comment utiliser l’authentification SDK Azure Bot Service v4, basée sur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8b3df-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="8b3df-106">Cela facilite le développement d’un bot qui peut utiliser des jetons d’authentification basés sur les informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="8b3df-107">L’élément clé de tout cela est l’utilisation de fournisseurs **d’identité,** comme nous le constaterons plus tard.</span><span class="sxs-lookup"><span data-stu-id="8b3df-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="8b3df-108">OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="8b3df-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="8b3df-109">Une compréhension de base d’OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans Teams.</span><span class="sxs-lookup"><span data-stu-id="8b3df-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="8b3df-110">Voir [OAuth 2 Simplifié pour](https://aka.ms/oauth2-simplified) une compréhension de base et [OAuth 2.0](https://oauth.net/2/) pour la spécification complète.</span><span class="sxs-lookup"><span data-stu-id="8b3df-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="8b3df-111">Pour plus d’informations sur la façon dont Azure Bot Service gère l’authentification, consultez [l’authentification utilisateur dans une conversation.](https://aka.ms/azure-bot-authentication)</span><span class="sxs-lookup"><span data-stu-id="8b3df-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="8b3df-112">Voici les titres des sections de cet article :</span><span class="sxs-lookup"><span data-stu-id="8b3df-112">In this article you'll learn:</span></span>

- <span data-ttu-id="8b3df-113">**Comment créer un bot activé pour l’authentification.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="8b3df-114">Vous utiliserez [cs-auth-sample][teams-auth-bot-cs] pour gérer les informations d’identification de connexion de l’utilisateur et la génération du jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8b3df-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="8b3df-115">**Comment déployer le bot sur Azure et l’associer à un fournisseur d’identité.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="8b3df-116">Le fournisseur émettra un jeton basé sur les informations d’identification de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="8b3df-117">Le bot peut utiliser le jeton pour accéder à des ressources, telles qu’un service de messagerie, qui nécessitent une authentification.</span><span class="sxs-lookup"><span data-stu-id="8b3df-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="8b3df-118">Pour plus d’informations, [voir flux d’authentification Microsoft Teams pour les bots.](auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="8b3df-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="8b3df-119">**Comment intégrer le bot dans Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="8b3df-120">Une fois le bot intégré, vous pouvez vous inscrire et échanger des messages avec lui dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="8b3df-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b3df-121">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="8b3df-121">Prerequisites</span></span>

- <span data-ttu-id="8b3df-122">Connaissance des principes [de base du bot,][concept-basics] [de la gestion de l’état,][concept-state]de la bibliothèque [de][concept-dialogs]boîtes de dialogue et de la façon d’implémenter un flux de [conversation séquentiel.][simple-dialog]</span><span class="sxs-lookup"><span data-stu-id="8b3df-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="8b3df-123">Connaissance du développement Azure et OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8b3df-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="8b3df-124">Les versions actuelles de Visual Studio git.</span><span class="sxs-lookup"><span data-stu-id="8b3df-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="8b3df-125">Compte Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3df-125">Azure account.</span></span> <span data-ttu-id="8b3df-126">Si nécessaire, vous pouvez créer un [compte gratuit Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="8b3df-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="8b3df-127">Exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="8b3df-127">The following sample.</span></span>

    | <span data-ttu-id="8b3df-128">Échantillon</span><span class="sxs-lookup"><span data-stu-id="8b3df-128">Sample</span></span> | <span data-ttu-id="8b3df-129">Version de BotBuilder</span><span class="sxs-lookup"><span data-stu-id="8b3df-129">BotBuilder version</span></span> | <span data-ttu-id="8b3df-130">Demonstrates</span><span class="sxs-lookup"><span data-stu-id="8b3df-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="8b3df-131">**Authentification de bot** [dans cs-auth-sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="8b3df-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="8b3df-132">v4</span><span class="sxs-lookup"><span data-stu-id="8b3df-132">v4</span></span> | <span data-ttu-id="8b3df-133">Prise en charge d’OAuthCard</span><span class="sxs-lookup"><span data-stu-id="8b3df-133">OAuthCard support</span></span> |
    | <span data-ttu-id="8b3df-134">**Authentification de bot** [dans js-auth-sample][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="8b3df-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="8b3df-135">v4</span><span class="sxs-lookup"><span data-stu-id="8b3df-135">v4</span></span>| <span data-ttu-id="8b3df-136">Prise en charge d’OAuthCard</span><span class="sxs-lookup"><span data-stu-id="8b3df-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="8b3df-137">**Authentification de bot** [dans py-auth-sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="8b3df-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="8b3df-138">v4</span><span class="sxs-lookup"><span data-stu-id="8b3df-138">v4</span></span> | <span data-ttu-id="8b3df-139">Prise en charge d’OAuthCard</span><span class="sxs-lookup"><span data-stu-id="8b3df-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="8b3df-140">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8b3df-140">Create the resource group</span></span>

<span data-ttu-id="8b3df-141">Le groupe de ressources et le plan de service ne sont pas strictement nécessaires, mais ils vous permettent de libérer facilement les ressources que vous créez.</span><span class="sxs-lookup"><span data-stu-id="8b3df-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="8b3df-142">Il s’agit d’une bonne pratique pour maintenir l’organisation et la gestion de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="8b3df-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="8b3df-143">Vous utilisez un groupe de ressources pour créer des ressources individuelles pour Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8b3df-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="8b3df-144">Pour obtenir des performances, assurez-vous que ces ressources se trouvent dans la même région Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3df-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="8b3df-145">Dans votre navigateur, connectez-vous au [**portail Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="8b3df-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="8b3df-146">Dans le panneau de navigation de gauche, sélectionnez **Groupes de ressources.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="8b3df-147">Dans le coin supérieur gauche de la fenêtre affichée, **sélectionnez** Ajouter un onglet pour créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8b3df-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="8b3df-148">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b3df-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="8b3df-149">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-149">**Subscription**.</span></span> <span data-ttu-id="8b3df-150">Utilisez votre abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="8b3df-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="8b3df-151">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-151">**Resource group**.</span></span> <span data-ttu-id="8b3df-152">Entrez le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8b3df-152">Enter the name for the resource group.</span></span> <span data-ttu-id="8b3df-153">Par exemple,  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="8b3df-154">N’oubliez pas que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="8b3df-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="8b3df-155">Dans le menu **déroulant Région,** sélectionnez *Ouest des* États-Unis ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="8b3df-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="8b3df-156">Sélectionnez le **bouton Révision et** créer.</span><span class="sxs-lookup"><span data-stu-id="8b3df-156">Select the **Review and create** button.</span></span> <span data-ttu-id="8b3df-157">Vous devriez voir une bannière qui lit *Validation transmise*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="8b3df-158">Sélectionnez **le bouton** Créer.</span><span class="sxs-lookup"><span data-stu-id="8b3df-158">Select the **Create** button.</span></span> <span data-ttu-id="8b3df-159">La création du groupe de ressources peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8b3df-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="8b3df-160">Comme pour les ressources que vous créerez plus loin dans ce didacticiel, il est bon d’épingler ce groupe de ressources à votre tableau de bord pour en faciliter l’accès.</span><span class="sxs-lookup"><span data-stu-id="8b3df-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="8b3df-161">Si vous le souhaitez, sélectionnez l’icône d'&#128204 ; dans le coin supérieur droit du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="8b3df-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="8b3df-162">Créer le plan de service</span><span class="sxs-lookup"><span data-stu-id="8b3df-162">Create the service plan</span></span>

1. <span data-ttu-id="8b3df-163">Dans le [**portail Azure,**][azure-portal]dans le panneau de navigation de gauche, **sélectionnez Créer une ressource.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="8b3df-164">Dans la zone de recherche, tapez *App Service Plan*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="8b3df-165">Sélectionnez la carte **Plan du service d’application** dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="8b3df-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="8b3df-166">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-166">Select **Create**.</span></span>
1. <span data-ttu-id="8b3df-167">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b3df-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="8b3df-168">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-168">**Subscription**.</span></span> <span data-ttu-id="8b3df-169">Vous pouvez utiliser un abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="8b3df-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="8b3df-170">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-170">**Resource Group**.</span></span> <span data-ttu-id="8b3df-171">Sélectionnez le groupe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8b3df-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="8b3df-172">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-172">**Name**.</span></span> <span data-ttu-id="8b3df-173">Entrez le nom du plan de service.</span><span class="sxs-lookup"><span data-stu-id="8b3df-173">Enter the name for the service plan.</span></span> <span data-ttu-id="8b3df-174">Par exemple,  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="8b3df-175">N’oubliez pas que le nom doit être unique au sein du groupe.</span><span class="sxs-lookup"><span data-stu-id="8b3df-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="8b3df-176">**Système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-176">**Operating System**.</span></span> <span data-ttu-id="8b3df-177">Sélectionnez *Windows* ou votre système d’exploitation applicable.</span><span class="sxs-lookup"><span data-stu-id="8b3df-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="8b3df-178">**Région**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-178">**Region**.</span></span> <span data-ttu-id="8b3df-179">Sélectionnez *Ouest des États-Unis* ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="8b3df-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="8b3df-180">**Niveau de tarification**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-180">**Pricing Tier**.</span></span> <span data-ttu-id="8b3df-181">Assurez-vous *que Standard S1* est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="8b3df-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="8b3df-182">Cette valeur doit être la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="8b3df-182">This should be the default value.</span></span>
    1. <span data-ttu-id="8b3df-183">Sélectionnez le **bouton Révision et** créer.</span><span class="sxs-lookup"><span data-stu-id="8b3df-183">Select the **Review and create** button.</span></span> <span data-ttu-id="8b3df-184">Vous devriez voir une bannière qui lit *Validation transmise*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="8b3df-185">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-185">Select **Create**.</span></span> <span data-ttu-id="8b3df-186">La création du plan de service d’application peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8b3df-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="8b3df-187">Le plan sera répertorié dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8b3df-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="8b3df-188">Créer l’inscription des canaux de bot</span><span class="sxs-lookup"><span data-stu-id="8b3df-188">Create the bot channels registration</span></span>

<span data-ttu-id="8b3df-189">L’inscription des canaux du bot inscrit votre service web en tant que bot auprès de Bot Framework, à condition que vous avez un ID d’application Microsoft et un mot de passe d’application (secret client).</span><span class="sxs-lookup"><span data-stu-id="8b3df-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b3df-190">Vous ne devez inscrire votre bot que s’il n’est pas hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3df-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="8b3df-191">Si vous [avez créé un bot via](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) le portail Azure, il est déjà inscrit auprès du service.</span><span class="sxs-lookup"><span data-stu-id="8b3df-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="8b3df-192">Si vous avez créé votre bot via [Bot Framework](https://dev.botframework.com/bots/new) ou [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) votre bot n’est pas inscrit dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3df-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="8b3df-193">La ressource d’inscription des canaux bots affiche la **région** globale même si vous avez sélectionné Ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="8b3df-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="8b3df-194">Ceci est normal.</span><span class="sxs-lookup"><span data-stu-id="8b3df-194">This is expected.</span></span>

<span data-ttu-id="8b3df-195">Pour plus d’informations, [voir Créer un bot pour Teams.](../create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="8b3df-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="8b3df-196">Créer le fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="8b3df-196">Create the identity provider</span></span>

<span data-ttu-id="8b3df-197">Vous avez besoin d’un fournisseur d’identité qui peut être utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="8b3df-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="8b3df-198">Dans cette procédure, vous allez utiliser un fournisseur Azure AD ; d’autres fournisseurs d’identité pris en charge par Azure AD peuvent également être utilisés.</span><span class="sxs-lookup"><span data-stu-id="8b3df-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="8b3df-199">Dans le [**portail Azure,**][azure-portal]dans le panneau de navigation de gauche, **sélectionnez Azure Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="8b3df-200">Vous devez créer et inscrire cette ressource Azure AD dans un client dans lequel vous pouvez consentir à déléguer les autorisations demandées par une application.</span><span class="sxs-lookup"><span data-stu-id="8b3df-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="8b3df-201">Pour obtenir des instructions sur la création d’un client, voir [Accéder au portail et créer un client.](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)</span><span class="sxs-lookup"><span data-stu-id="8b3df-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="8b3df-202">Dans le panneau gauche, sélectionnez **Inscriptions d’applications.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="8b3df-203">Dans le panneau droit, sélectionnez **l’onglet** Nouvelle inscription, dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="8b3df-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="8b3df-204">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b3df-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="8b3df-205">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-205">**Name**.</span></span> <span data-ttu-id="8b3df-206">Entrez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="8b3df-206">Enter the name for the application.</span></span> <span data-ttu-id="8b3df-207">Par exemple,  *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="8b3df-208">N’oubliez pas que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="8b3df-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="8b3df-209">Sélectionnez les **types de comptes pris en** charge pour votre application.</span><span class="sxs-lookup"><span data-stu-id="8b3df-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="8b3df-210">Sélectionnez les comptes dans n’importe quel annuaire d’organisation (n’importe quel annuaire *Azure AD - Multi-client)* et les comptes Microsoft personnels (par exemple, Skype, Xbox).</span><span class="sxs-lookup"><span data-stu-id="8b3df-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="8b3df-211">Pour **l’URI de redirection**:</span><span class="sxs-lookup"><span data-stu-id="8b3df-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="8b3df-212">&#x2713;Sélectionnez **Web**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="8b3df-213">&#x2713; définir l’URL sur `https://token.botframework.com/.auth/web/redirect` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="8b3df-214">Sélectionnez **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-214">Select **Register**.</span></span>

1. <span data-ttu-id="8b3df-215">Une fois créé, Azure affiche la page **Vue d’ensemble** de l’application.</span><span class="sxs-lookup"><span data-stu-id="8b3df-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="8b3df-216">Copiez et enregistrez les informations suivantes dans un fichier :</span><span class="sxs-lookup"><span data-stu-id="8b3df-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="8b3df-217">Valeur **de l’ID de l’application (client).**</span><span class="sxs-lookup"><span data-stu-id="8b3df-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="8b3df-218">Vous utiliserez cette valeur ultérieurement comme *ID client* lorsque vous enregistrerez cette application d’identité Azure auprès de votre bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="8b3df-219">Valeur **de l’ID** du répertoire (client).</span><span class="sxs-lookup"><span data-stu-id="8b3df-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="8b3df-220">Vous utiliserez également cette valeur ultérieurement comme *ID* de client pour inscrire cette application d’identité Azure auprès de votre bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="8b3df-221">Dans le panneau gauche, **sélectionnez Certificats & secrets** pour créer une secret client pour votre application.</span><span class="sxs-lookup"><span data-stu-id="8b3df-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="8b3df-222">Sous **Les secrets client,** sélectionnez &#x2795; **Nouvelle secret client.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="8b3df-223">Ajoutez une description pour identifier ce secret auprès d’autres personnes que vous devrez peut-être créer pour cette application, telles que l’application d’identité *bot dans Teams.*</span><span class="sxs-lookup"><span data-stu-id="8b3df-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="8b3df-224">La **sélection expire.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="8b3df-225">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-225">Select **Add**.</span></span>
   1. <span data-ttu-id="8b3df-226">Avant de quitter cette page, **enregistrez le secret.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="8b3df-227">Vous utiliserez cette valeur comme secret _client_ ultérieurement lorsque vous enregistrerez votre application Azure AD auprès de votre bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="8b3df-228">Configurer la connexion du fournisseur d’identité et l’inscrire auprès du bot</span><span class="sxs-lookup"><span data-stu-id="8b3df-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="8b3df-229">Remarque : il existe deux options pour les fournisseurs de services ici : Azure AD V1 et Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="8b3df-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="8b3df-230">Les différences entre les deux fournisseurs sont résumées [ici,](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)mais en général, V2 offre plus de flexibilité en ce qui concerne la modification des autorisations de bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="8b3df-231">Les autorisations de l’API Graph sont répertoriées dans le champ d’étendues et, à mesure que de nouvelles autorisations sont ajoutées, les bots permettent aux utilisateurs d’autoriser les nouvelles autorisations à la prochaine connexion.</span><span class="sxs-lookup"><span data-stu-id="8b3df-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="8b3df-232">Pour V1, le consentement du bot doit être supprimé par l’utilisateur pour que de nouvelles autorisations soient invités dans la boîte de dialogue OAuth.</span><span class="sxs-lookup"><span data-stu-id="8b3df-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="8b3df-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="8b3df-233">Azure AD V1</span></span>

1. <span data-ttu-id="8b3df-234">Dans le [**portail Azure,**][azure-portal]sélectionnez votre groupe de ressources dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="8b3df-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="8b3df-235">Sélectionnez le lien d’inscription de votre canal bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="8b3df-236">Dans la page de ressources, sélectionnez **Paramètres.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-236">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="8b3df-237">Sous **Paramètres de connexion OAuth** en bas de la page, sélectionnez **Ajouter un paramètre.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-237">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="8b3df-238">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="8b3df-238">Complete the form as follows:</span></span>

    1. <span data-ttu-id="8b3df-239">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-239">**Name**.</span></span> <span data-ttu-id="8b3df-240">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="8b3df-240">Enter a name for the connection.</span></span> <span data-ttu-id="8b3df-241">Vous utiliserez ce nom dans votre bot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="8b3df-241">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="8b3df-242">Par exemple *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-242">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="8b3df-243">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-243">**Service Provider**.</span></span> <span data-ttu-id="8b3df-244">Sélectionner **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-244">Select **Azure Active Directory**.</span></span> <span data-ttu-id="8b3df-245">Une fois cette sélection sélectionnée, les champs spécifiques à Azure AD s’affichent.</span><span class="sxs-lookup"><span data-stu-id="8b3df-245">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="8b3df-246">**ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8b3df-246">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="8b3df-247">**Secret client**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-247">**Client secret**.</span></span> <span data-ttu-id="8b3df-248">Entrez le secret que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8b3df-248">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="8b3df-249">**Type d’octroi**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-249">**Grant Type**.</span></span> <span data-ttu-id="8b3df-250">Entrez `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-250">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="8b3df-251">**URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-251">**Login URL**.</span></span> <span data-ttu-id="8b3df-252">Entrez `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-252">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="8b3df-253">**ID de client**, entrez l’ID d’annuaire **(client)**  que vous avez enregistré précédemment pour votre application d’identité Azure ou commun en fonction du type de compte pris en charge sélectionné lors de la création de l’application fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="8b3df-253">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="8b3df-254">Pour déterminer la valeur à attribuer, suivez ces critères :</span><span class="sxs-lookup"><span data-stu-id="8b3df-254">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="8b3df-255">Si vous avez sélectionné des comptes dans cet annuaire d’organisation uniquement (Microsoft uniquement - Client *unique)* ou des comptes dans un annuaire d’organisation *(annuaire Microsoft AAD - Multi-locataire),* entrez l’ID de locataire que vous avez enregistré précédemment pour l’application AAD. </span><span class="sxs-lookup"><span data-stu-id="8b3df-255">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="8b3df-256">Il s’agit du client associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="8b3df-256">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="8b3df-257">Si vous avez sélectionné des comptes dans un annuaire d’organisation (n’importe quel annuaire AAD - comptes  Microsoft multi-clients et personnels par *exemple, Skype, Xbox, Outlook),* entrez le mot commun au lieu d’un ID de client.</span><span class="sxs-lookup"><span data-stu-id="8b3df-257">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="8b3df-258">Dans le cas contraire, l’application AAD vérifie via le client dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="8b3df-258">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="8b3df-259">h.</span><span class="sxs-lookup"><span data-stu-id="8b3df-259">h.</span></span> <span data-ttu-id="8b3df-260">Pour **l’URL de** la ressource, entrez `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-260">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="8b3df-261">Cela n’est pas utilisé dans l’exemple de code actuel.</span><span class="sxs-lookup"><span data-stu-id="8b3df-261">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="8b3df-262">i.</span><span class="sxs-lookup"><span data-stu-id="8b3df-262">i.</span></span> <span data-ttu-id="8b3df-263">Laissez **les étendues** vides.</span><span class="sxs-lookup"><span data-stu-id="8b3df-263">Leave **Scopes** blank.</span></span> <span data-ttu-id="8b3df-264">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b3df-264">The following image is an example:</span></span>

    ![Affichage adv1 de chaîne de connexion d’th de l’application teams bots](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="8b3df-266">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-266">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="8b3df-267">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="8b3df-267">Azure AD V2</span></span>

1. <span data-ttu-id="8b3df-268">Dans le [**portail Azure,**][azure-portal]sélectionnez votre groupe de ressources dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="8b3df-268">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="8b3df-269">Sélectionnez le lien d’inscription de votre canal bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-269">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="8b3df-270">Dans la page de ressources, sélectionnez **Paramètres.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-270">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="8b3df-271">Sous **Paramètres de connexion OAuth** en bas de la page, sélectionnez **Ajouter un paramètre.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-271">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="8b3df-272">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="8b3df-272">Complete the form as follows:</span></span>

    1. <span data-ttu-id="8b3df-273">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-273">**Name**.</span></span> <span data-ttu-id="8b3df-274">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="8b3df-274">Enter a name for the connection.</span></span> <span data-ttu-id="8b3df-275">Vous utiliserez ce nom dans votre bot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="8b3df-275">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="8b3df-276">Par exemple *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-276">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="8b3df-277">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-277">**Service Provider**.</span></span> <span data-ttu-id="8b3df-278">Sélectionnez **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-278">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="8b3df-279">Une fois cette sélection sélectionnée, les champs spécifiques à Azure AD s’affichent.</span><span class="sxs-lookup"><span data-stu-id="8b3df-279">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="8b3df-280">**ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8b3df-280">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="8b3df-281">**Secret client**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-281">**Client secret**.</span></span> <span data-ttu-id="8b3df-282">Entrez le secret que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8b3df-282">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="8b3df-283">**URL d’Exchange de jeton**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-283">**Token Exchange URL**.</span></span> <span data-ttu-id="8b3df-284">Laissez ce vide.</span><span class="sxs-lookup"><span data-stu-id="8b3df-284">Leave this blank.</span></span>
    1. <span data-ttu-id="8b3df-285">**ID de client**, entrez l’ID d’annuaire **(client)**  que vous avez enregistré précédemment pour votre application d’identité Azure ou commun en fonction du type de compte pris en charge sélectionné lors de la création de l’application fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="8b3df-285">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="8b3df-286">Pour déterminer la valeur à attribuer, suivez ces critères :</span><span class="sxs-lookup"><span data-stu-id="8b3df-286">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="8b3df-287">Si vous avez sélectionné des comptes dans cet annuaire d’organisation uniquement (Microsoft uniquement - Client *unique)* ou des comptes dans un annuaire d’organisation *(annuaire Microsoft AAD - Multi-locataire),* entrez l’ID de locataire que vous avez enregistré précédemment pour l’application AAD. </span><span class="sxs-lookup"><span data-stu-id="8b3df-287">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="8b3df-288">Il s’agit du client associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="8b3df-288">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="8b3df-289">Si vous avez sélectionné des comptes dans un annuaire d’organisation (n’importe quel annuaire AAD - comptes  Microsoft multi-clients et personnels par *exemple, Skype, Xbox, Outlook),* entrez le mot commun au lieu d’un ID de client.</span><span class="sxs-lookup"><span data-stu-id="8b3df-289">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="8b3df-290">Dans le cas contraire, l’application AAD vérifie via le client dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="8b3df-290">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="8b3df-291">Pour **les étendues,** entrez une liste délimitée par des espaces d’autorisations graphiques que cette application requiert par exemple : User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="8b3df-291">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="8b3df-292">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-292">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="8b3df-293">Tester la connexion</span><span class="sxs-lookup"><span data-stu-id="8b3df-293">Test the connection</span></span>

1. <span data-ttu-id="8b3df-294">Sélectionnez l’entrée de connexion pour ouvrir la connexion que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="8b3df-294">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="8b3df-295">Sélectionnez **Tester la connexion** en haut du panneau **Paramètres de connexion** du fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="8b3df-295">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="8b3df-296">La première fois que vous le faites, une nouvelle fenêtre de navigateur s’ouvre et vous demande de sélectionner un compte.</span><span class="sxs-lookup"><span data-stu-id="8b3df-296">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="8b3df-297">Sélectionnez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="8b3df-297">Select the one you want to use.</span></span>
1. <span data-ttu-id="8b3df-298">Ensuite, vous serez invité à autoriser le fournisseur d’identité à utiliser vos données (informations d’identification).</span><span class="sxs-lookup"><span data-stu-id="8b3df-298">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="8b3df-299">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b3df-299">The following image is an example:</span></span>

    ![teams bot auth connection string adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="8b3df-301">Sélectionnez **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-301">Select **Accept**.</span></span>
1. <span data-ttu-id="8b3df-302">Vous devez ensuite vous rediriger vers une page **De connexion test à \<your-connection-name> Réussite.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-302">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="8b3df-303">Actualisez la page si vous obtenez une erreur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-303">Refresh the page if you get an error.</span></span> <span data-ttu-id="8b3df-304">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b3df-304">The following image is an example:</span></span>

  ![teams bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="8b3df-306">Le nom de connexion est utilisé par le code du bot pour récupérer les jetons d’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-306">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="8b3df-307">Préparer l’exemple de code du bot</span><span class="sxs-lookup"><span data-stu-id="8b3df-307">Prepare the bot sample code</span></span>

<span data-ttu-id="8b3df-308">Une fois les paramètres préliminaires terminés, nous allons nous concentrer sur la création du bot à utiliser dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8b3df-308">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8b3df-309">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8b3df-309">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="8b3df-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="8b3df-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="8b3df-311">Lancez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b3df-311">Launch Visual Studio.</span></span>
1. <span data-ttu-id="8b3df-312">Dans la barre d’outils, **sélectionnez Fichier -> Ouvrir -> projet/solution** et ouvrez le projet bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-312">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="8b3df-313">Dans C# mise **à jourappsettings.jsles informations suivantes** :</span><span class="sxs-lookup"><span data-stu-id="8b3df-313">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="8b3df-314">Définissez `ConnectionName` ce nom sur le nom de la connexion de fournisseur d’identité que vous avez ajoutée à l’inscription du canal du bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-314">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="8b3df-315">Le nom que nous avons utilisé dans cet exemple *est BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-315">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="8b3df-316">Définissez `MicrosoftAppId` ce dernier sur **l’ID d’application** du bot que vous avez enregistré au moment de l’inscription du canal du bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-316">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="8b3df-317">Définissez `MicrosoftAppPassword` sur la secret client **que** vous avez enregistrée au moment de l’inscription au canal du bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-317">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="8b3df-318">En fonction des caractères dans votre secret de bot, vous devrez peut-être éviter le mot de passe au code XML.</span><span class="sxs-lookup"><span data-stu-id="8b3df-318">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="8b3df-319">Par exemple, toutes les andersands (&) doivent être codées comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-319">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="8b3df-320">Dans l’Explorateur de solutions, accédez au dossier, ouvrez et définissez l’ID d’application du bot que vous avez enregistré au moment de l’inscription du `TeamsAppManifest` `manifest.json` canal du `id` `botId` bot. </span><span class="sxs-lookup"><span data-stu-id="8b3df-320">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="8b3df-321">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8b3df-321">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="8b3df-322">Clone [node-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="8b3df-322">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="8b3df-323">Dans une console, accédez au projet :</span><span class="sxs-lookup"><span data-stu-id="8b3df-323">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="8b3df-324">Installer des modules</span><span class="sxs-lookup"><span data-stu-id="8b3df-324">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="8b3df-325">Mettez à jour la configuration **.env** comme suit :</span><span class="sxs-lookup"><span data-stu-id="8b3df-325">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="8b3df-326">Définissez `MicrosoftAppId` ce dernier sur **l’ID d’application** du bot que vous avez enregistré au moment de l’inscription du canal du bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-326">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="8b3df-327">Définissez `MicrosoftAppPassword` sur la secret client **que** vous avez enregistrée au moment de l’inscription au canal du bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-327">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="8b3df-328">Définissez `connectionName` le nom de la connexion du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="8b3df-328">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="8b3df-329">En fonction des caractères dans votre secret de bot, vous devrez peut-être éviter le mot de passe au code XML.</span><span class="sxs-lookup"><span data-stu-id="8b3df-329">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="8b3df-330">Par exemple, toutes les andersands (&) doivent être codées comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-330">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="8b3df-331">Dans le dossier, ouvrez et définissez votre ID d’application Microsoft et `teamsAppManifest` l’ID d’application du bot que vous avez enregistré au moment de l’inscription du `manifest.json` `id` canal du  `botId` bot. </span><span class="sxs-lookup"><span data-stu-id="8b3df-331">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="8b3df-332">Python</span><span class="sxs-lookup"><span data-stu-id="8b3df-332">Python</span></span>](#tab/python)

1. <span data-ttu-id="8b3df-333">Clonez [py-auth-sample][teams-auth-bot-py] à partir du référentiel github.</span><span class="sxs-lookup"><span data-stu-id="8b3df-333">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="8b3df-334">Mettre **à jour config.py**:</span><span class="sxs-lookup"><span data-stu-id="8b3df-334">Update **config.py**:</span></span>

    - <span data-ttu-id="8b3df-335">Définissez `ConnectionName` ce paramètre sur le nom du paramètre de connexion OAuth que vous avez ajouté à votre bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-335">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="8b3df-336">Définissez `MicrosoftAppId` et `MicrosoftAppPassword` définissez l’ID d’application et la secret de l’application de votre bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-336">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="8b3df-337">En fonction des caractères dans votre secret de bot, vous devrez peut-être éviter le mot de passe au code XML.</span><span class="sxs-lookup"><span data-stu-id="8b3df-337">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="8b3df-338">Par exemple, toutes les andersands (&) doivent être codées comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-338">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="8b3df-339">Déployer le bot sur Azure</span><span class="sxs-lookup"><span data-stu-id="8b3df-339">Deploy the bot to Azure</span></span>

<span data-ttu-id="8b3df-340">Pour déployer le bot, suivez les étapes de la procédure de déploiement [de votre bot sur Azure.](https://aka.ms/azure-bot-deployment-cli)</span><span class="sxs-lookup"><span data-stu-id="8b3df-340">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="8b3df-341">Vous pouvez également utiliser Visual Studio, vous pouvez suivre les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b3df-341">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="8b3df-342">Dans *Visual Studio’Explorateur de* solutions, sélectionnez et maintenez (ou cliquez avec le bouton droit) le nom du projet.</span><span class="sxs-lookup"><span data-stu-id="8b3df-342">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="8b3df-343">Dans le menu déroulant, sélectionnez **Publier.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-343">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="8b3df-344">Dans la fenêtre affichée, sélectionnez le **lien** Nouveau.</span><span class="sxs-lookup"><span data-stu-id="8b3df-344">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="8b3df-345">Dans la fenêtre de boîte de dialogue, **sélectionnez Service d’application** sur la gauche et **Créer** à droite.</span><span class="sxs-lookup"><span data-stu-id="8b3df-345">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="8b3df-346">Sélectionnez **le bouton** Publier.</span><span class="sxs-lookup"><span data-stu-id="8b3df-346">Select the **Publish** button.</span></span>
1. <span data-ttu-id="8b3df-347">Dans la fenêtre de boîte de dialogue suivante, entrez les informations requises.</span><span class="sxs-lookup"><span data-stu-id="8b3df-347">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="8b3df-348">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b3df-348">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="8b3df-350">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-350">Select **Create**.</span></span>
1. <span data-ttu-id="8b3df-351">Si le déploiement se termine correctement, vous devez le voir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b3df-351">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="8b3df-352">En outre, une page s’affiche dans votre navigateur par défaut pour dire *que votre bot est prêt !*.</span><span class="sxs-lookup"><span data-stu-id="8b3df-352">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="8b3df-353">L’URL sera similaire à celle-ci : `https://botteamsauth.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="8b3df-353">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="8b3df-354">Enregistrez-le dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="8b3df-354">Save it to a file.</span></span>
1. <span data-ttu-id="8b3df-355">Dans votre navigateur, accédez au [**portail Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="8b3df-355">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="8b3df-356">Vérifiez votre groupe de ressources, le bot doit être répertorié avec les autres ressources.</span><span class="sxs-lookup"><span data-stu-id="8b3df-356">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="8b3df-357">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b3df-357">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="8b3df-359">Dans le groupe de ressources, sélectionnez le nom d’inscription du canal bot (lien).</span><span class="sxs-lookup"><span data-stu-id="8b3df-359">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="8b3df-360">Dans le panneau gauche, sélectionnez **Paramètres.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-360">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="8b3df-361">Dans la **zone Point de terminaison de messagerie,** entrez l’URL obtenue ci-dessus, suivie de `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-361">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="8b3df-362">Voici un exemple : `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-362">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="8b3df-363">Sélectionnez **le bouton** Enregistrer dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="8b3df-363">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="8b3df-364">Tester le bot à l’aide de l’émulateur</span><span class="sxs-lookup"><span data-stu-id="8b3df-364">Test the bot using the Emulator</span></span>

<span data-ttu-id="8b3df-365">Si vous ne l’avez pas déjà fait, installez [l’émulateur Microsoft Bot Framework.](https://aka.ms/bot-framework-emulator-readme)</span><span class="sxs-lookup"><span data-stu-id="8b3df-365">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="8b3df-366">Voir aussi [Déboguer avec l’émulateur.](https://aka.ms/bot-framework-emulator-debug-with-emulator)</span><span class="sxs-lookup"><span data-stu-id="8b3df-366">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="8b3df-367">Pour que l’exemple de connexion du bot fonctionne, vous devez configurer l’émulateur comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b3df-367">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="8b3df-368">Configurer l’émulateur pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="8b3df-368">Configure the Emulator for authentication</span></span>

<span data-ttu-id="8b3df-369">Si un bot nécessite une authentification, vous devez configurer l’émulateur comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b3df-369">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="8b3df-370">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-370">Start the Emulator.</span></span>
1. <span data-ttu-id="8b3df-371">Dans l’émulateur, sélectionnez l’icône d’engrenage &#9881; en bas à gauche ou l’onglet **Paramètres** de l’émulateur dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="8b3df-371">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="8b3df-372">Cochez la case **en authentification version 1.0.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-372">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="8b3df-373">Entrez le chemin d’accès local à **l’outil ngrok.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-373">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="8b3df-374">*Consultez* le Wiki d’intégration de tunneling Bot Framework/ngrok. [](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))</span><span class="sxs-lookup"><span data-stu-id="8b3df-374">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="8b3df-375">Pour plus d’informations sur l’outil, [voir ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="8b3df-375">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="8b3df-376">Cochez la case par Exécuter ngrok au démarrage de **l’émulateur.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-376">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="8b3df-377">Sélectionnez le **bouton** Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="8b3df-377">Select the **Save** button.</span></span>

<span data-ttu-id="8b3df-378">Lorsque le bot affiche une carte de visite et que l’utilisateur sélectionne le bouton de la signature, l’émulateur ouvre une page que l’utilisateur peut utiliser pour se connecter avec le fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8b3df-378">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="8b3df-379">Une fois que l’utilisateur a fait cela, le fournisseur génère un jeton utilisateur et l’envoie au bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-379">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="8b3df-380">Après cela, le bot peut agir pour le compte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-380">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="8b3df-381">Tester le bot localement</span><span class="sxs-lookup"><span data-stu-id="8b3df-381">Test the bot locally</span></span>

<span data-ttu-id="8b3df-382">Une fois que vous avez configuré le mécanisme d’authentification, vous pouvez effectuer le test réel du bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-382">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="8b3df-383">Exécutez l’exemple de bot localement sur votre ordinateur, Visual Studio par exemple.</span><span class="sxs-lookup"><span data-stu-id="8b3df-383">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="8b3df-384">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-384">Start the Emulator.</span></span>
1. <span data-ttu-id="8b3df-385">Sélectionnez **le bouton Ouvrir le bot.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-385">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="8b3df-386">Dans **l’URL du bot,** entrez l’URL locale du bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-386">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="8b3df-387">Généralement, `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-387">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="8b3df-388">Dans **l’ID d’application Microsoft,** entrez l’ID d’application du bot à partir de `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-388">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="8b3df-389">Dans le mot **de passe de l’application Microsoft,** entrez le mot de passe de l’application du bot à partir du `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-389">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="8b3df-390">Sélectionnez **Se connecter.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-390">Select **Connect**.</span></span>
1. <span data-ttu-id="8b3df-391">Une fois que le bot est en cours d’exécution, entrez du texte pour afficher la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="8b3df-391">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="8b3df-392">Sélectionnez le bouton **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-392">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="8b3df-393">Une boîte de dialogue s’affiche pour confirmer **l’ouverture de l’URL.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-393">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="8b3df-394">Cela permet à l’utilisateur du bot (vous) d’être authentifié.</span><span class="sxs-lookup"><span data-stu-id="8b3df-394">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="8b3df-395">Sélectionner **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-395">Select **Confirm**.</span></span>
1. <span data-ttu-id="8b3df-396">Si vous y êtes invité, sélectionnez le compte de l’utilisateur applicable.</span><span class="sxs-lookup"><span data-stu-id="8b3df-396">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="8b3df-397">Selon la configuration que vous avez utilisée pour l’émulateur, vous obtenez l’une des configurations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b3df-397">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="8b3df-398">**Utilisation du code de vérification de la signature**</span><span class="sxs-lookup"><span data-stu-id="8b3df-398">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="8b3df-399">&#x2713; fenêtre ouverte affichant le code de validation.</span><span class="sxs-lookup"><span data-stu-id="8b3df-399">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="8b3df-400">&#x2713; copiez et entrez le code de validation dans la zone de conversation pour terminer la signature.</span><span class="sxs-lookup"><span data-stu-id="8b3df-400">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="8b3df-401">**Utilisation de jetons d’authentification.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-401">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="8b3df-402">&#x2713; vous êtes connecté en fonction de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="8b3df-402">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="8b3df-403">L’image suivante est un exemple de l’interface utilisateur du bot après vous être connecté :</span><span class="sxs-lookup"><span data-stu-id="8b3df-403">The following image is an example of the bot UI after you've logged in:</span></span>

    ![émulateur de connexion au bot d’authentification](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="8b3df-405">Si vous sélectionnez **Oui** lorsque le bot vous demande *Voulez-vous* afficher votre jeton ? , vous recevrez une réponse semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="8b3df-405">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![Jeton d’émulateur de connexion du bot d’authentification](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="8b3df-407">Entrez **la connexion dans** la zone de conversation d’entrée pour vous déconnecter. Cela libère le jeton utilisateur et le bot ne peut pas agir en votre nom tant que vous ne vous connectez pas à nouveau.</span><span class="sxs-lookup"><span data-stu-id="8b3df-407">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="8b3df-408">L’authentification du bot nécessite l’utilisation **du service Bot Connector.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-408">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="8b3df-409">Le service accède aux informations d’inscription des canaux du bot pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-409">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="8b3df-410">Tester le bot déployé</span><span class="sxs-lookup"><span data-stu-id="8b3df-410">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="8b3df-411">Dans votre navigateur, accédez au [**portail Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="8b3df-411">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="8b3df-412">Recherchez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8b3df-412">Find your resource group.</span></span>
1. <span data-ttu-id="8b3df-413">Sélectionnez le lien de la ressource.</span><span class="sxs-lookup"><span data-stu-id="8b3df-413">Select the resource link.</span></span> <span data-ttu-id="8b3df-414">La page de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8b3df-414">The resource page is displayed.</span></span>
1. <span data-ttu-id="8b3df-415">Dans la page de ressources, **sélectionnez Tester dans la conversation web.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-415">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="8b3df-416">Le bot démarre et affiche les salutations prédéfinës.</span><span class="sxs-lookup"><span data-stu-id="8b3df-416">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="8b3df-417">Tapez quoi que ce soit dans la zone de conversation.</span><span class="sxs-lookup"><span data-stu-id="8b3df-417">Type anything in the chat box.</span></span>
1. <span data-ttu-id="8b3df-418">Sélectionnez la **zone Se** connectez.</span><span class="sxs-lookup"><span data-stu-id="8b3df-418">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="8b3df-419">Une boîte de dialogue s’affiche pour confirmer **l’ouverture de l’URL.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-419">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="8b3df-420">Cela permet à l’utilisateur du bot (vous) d’être authentifié.</span><span class="sxs-lookup"><span data-stu-id="8b3df-420">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="8b3df-421">Sélectionner **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-421">Select **Confirm**.</span></span>
1. <span data-ttu-id="8b3df-422">Si vous y êtes invité, sélectionnez le compte de l’utilisateur applicable.</span><span class="sxs-lookup"><span data-stu-id="8b3df-422">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="8b3df-423">L’image suivante est un exemple de l’interface utilisateur du bot après vous être connecté :</span><span class="sxs-lookup"><span data-stu-id="8b3df-423">The following image is an example of the bot UI after you have logged in:</span></span>

    ![Connexion du bot d’authentification déployée](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="8b3df-425">.</span><span class="sxs-lookup"><span data-stu-id="8b3df-425">.</span></span>

1. <span data-ttu-id="8b3df-426">Sélectionnez le **bouton Oui** pour afficher votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8b3df-426">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="8b3df-427">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b3df-427">The following image is an example:</span></span>

    ![Jeton déployé de connexion au bot d’authentification](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="8b3df-429">.</span><span class="sxs-lookup"><span data-stu-id="8b3df-429">.</span></span>

1. <span data-ttu-id="8b3df-430">Entrez la connexion pour vous déconnecter.</span><span class="sxs-lookup"><span data-stu-id="8b3df-430">Enter logout to sign out.</span></span>

    ![Connexion déployée par le bot d’th](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="8b3df-432">Si vous avez des problèmes de connexion, essayez de tester à nouveau la connexion comme décrit dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="8b3df-432">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="8b3df-433">Cela pourrait recréer le jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8b3df-433">This could recreate the authentication token.</span></span>
> <span data-ttu-id="8b3df-434">Avec le client De conversation web Bot Framework dans Azure, vous devrez peut-être vous y connecter plusieurs fois avant que l’authentification ne soit établie correctement.</span><span class="sxs-lookup"><span data-stu-id="8b3df-434">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="8b3df-435">Installer et tester le bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="8b3df-435">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="8b3df-436">Dans votre projet de bot, assurez-vous que le dossier contient `TeamsAppManifest` le contenu et les `manifest.json` `outline.png` `color.png` fichiers.</span><span class="sxs-lookup"><span data-stu-id="8b3df-436">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="8b3df-437">Dans l’Explorateur de solutions, accédez au `TeamsAppManifest` dossier.</span><span class="sxs-lookup"><span data-stu-id="8b3df-437">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="8b3df-438">Modifiez `manifest.json` en attribuant les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b3df-438">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="8b3df-439">Assurez-vous que **l’ID d’application** du bot que vous avez reçu au moment de l’inscription au canal du bot est affecté à `id` et `botId` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-439">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="8b3df-440">Affectez cette valeur : `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-440">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="8b3df-441">Sélectionnez **et compresser** `manifest.json` les fichiers et les `outline.png` `color.png` fichiers.</span><span class="sxs-lookup"><span data-stu-id="8b3df-441">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="8b3df-442">Ouvrez **Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-442">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="8b3df-443">Dans le panneau gauche, en bas, sélectionnez **l’icône Applications.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-443">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="8b3df-444">Dans le panneau droit, en bas, sélectionnez **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-444">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="8b3df-445">Accédez au `TeamsAppManifest` dossier et téléchargez le manifeste compressé.</span><span class="sxs-lookup"><span data-stu-id="8b3df-445">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="8b3df-446">L’Assistant suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="8b3df-446">The following wizard is displayed:</span></span>

    ![Chargement des équipes de bot d’th](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="8b3df-448">Sélectionnez le bouton **Ajouter à une équipe**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-448">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="8b3df-449">Dans la fenêtre suivante, sélectionnez l’équipe dans laquelle vous souhaitez utiliser le bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-449">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="8b3df-450">Sélectionnez **le bouton Configurer un bot.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-450">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="8b3df-451">Sélectionnez les trois points (&#x25cf;&#x25cf;&#x25cf;) dans le panneau gauche.</span><span class="sxs-lookup"><span data-stu-id="8b3df-451">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="8b3df-452">Sélectionnez ensuite **l’icône App Studio.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-452">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="8b3df-453">Sélectionnez **l’onglet Éditeur de** manifeste. Vous devriez voir l’icône du bot que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="8b3df-453">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="8b3df-454">En outre, vous devriez être en mesure de voir le bot répertorié en tant que contact dans la liste de conversation que vous pouvez utiliser pour échanger des messages avec le bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-454">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="8b3df-455">Test du bot localement dans Teams</span><span class="sxs-lookup"><span data-stu-id="8b3df-455">Testing the bot locally in Teams</span></span>

<span data-ttu-id="8b3df-456">Microsoft Teams est un produit entièrement basé sur le cloud, il nécessite que tous les services accessibles soient disponibles à partir du cloud à l’aide de points de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8b3df-456">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="8b3df-457">Par conséquent, pour permettre au bot (notre exemple) de fonctionner dans Teams, vous devez publier le code dans le cloud de votre choix ou rendre une instance en cours d’exécution localement accessible en externe via un outil **de tunneling.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-457">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="8b3df-458">Nous vous  [recommandons ngrok,](https://ngrok.com/download)qui crée une URL adressan externe pour un port que vous ouvrez localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-458">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="8b3df-459">Pour configurer ngrok en vue de l’exécution locale de votre application Microsoft Teams, suivez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b3df-459">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="8b3df-460">Dans une fenêtre terminal, allez dans le répertoire où vous `ngrok.exe` avez installé.</span><span class="sxs-lookup"><span data-stu-id="8b3df-460">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="8b3df-461">Nous vous suggérons de définir *le chemin d’accès de la variable* d’environnement pour qu’il pointe vers celui-ci.</span><span class="sxs-lookup"><span data-stu-id="8b3df-461">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="8b3df-462">Exécutez, par exemple, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-462">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="8b3df-463">Remplacez le numéro de port selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="8b3df-463">Replace the port number as needed.</span></span>
<span data-ttu-id="8b3df-464">Cela lance ngrok pour écouter sur le port que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="8b3df-464">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="8b3df-465">En retour, il vous donne une URL adressan externe, valide tant que ngrok est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8b3df-465">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="8b3df-466">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b3df-466">The following image is an example:</span></span>

    ![teams bot app auth connection string adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="8b3df-468">.</span><span class="sxs-lookup"><span data-stu-id="8b3df-468">.</span></span>

1. <span data-ttu-id="8b3df-469">Copiez l’adresse HTTPS de forwarding.</span><span class="sxs-lookup"><span data-stu-id="8b3df-469">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="8b3df-470">Il doit être similaire à ce qui `https://dea822bf.ngrok.io/` suit :</span><span class="sxs-lookup"><span data-stu-id="8b3df-470">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="8b3df-471">Append `/api/messages` pour obtenir `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="8b3df-471">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="8b3df-472">Il s’agit du **point de terminaison** des messages pour le bot s’exécutant localement sur votre ordinateur et accessible sur le web dans une conversation dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8b3df-472">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="8b3df-473">Une dernière étape consiste à mettre à jour le point de terminaison des messages du bot déployé.</span><span class="sxs-lookup"><span data-stu-id="8b3df-473">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="8b3df-474">Dans l’exemple, nous avons déployé le bot dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3df-474">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="8b3df-475">Par donc, \*\*nous allons effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b3df-475">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="8b3df-476">Dans votre navigateur, accédez au [**portail Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="8b3df-476">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="8b3df-477">Sélectionnez votre **inscription au canal bot.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-477">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="8b3df-478">Dans le panneau gauche, sélectionnez **Paramètres.**</span><span class="sxs-lookup"><span data-stu-id="8b3df-478">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="8b3df-479">Dans le panneau droit, dans la **zone** Point de terminaison de messagerie, entrez l’URL ngrok, dans notre `https://dea822bf.ngrok.io/api/messages` exemple.</span><span class="sxs-lookup"><span data-stu-id="8b3df-479">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="8b3df-480">Démarrez votre bot localement, par exemple en mode Visual Studio débogage.</span><span class="sxs-lookup"><span data-stu-id="8b3df-480">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="8b3df-481">Testez le bot lors de l’exécution locale à l’aide de la **conversation Web test** du portail Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8b3df-481">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="8b3df-482">Comme l’émulateur, ce test ne vous permet pas d’accéder aux fonctionnalités propres à Teams.</span><span class="sxs-lookup"><span data-stu-id="8b3df-482">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="8b3df-483">Dans la fenêtre terminal où s’exécute le trafic HTTP entre le bot et `ngrok` le client de conversation web.</span><span class="sxs-lookup"><span data-stu-id="8b3df-483">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="8b3df-484">Si vous souhaitez une vue plus détaillée, dans une fenêtre de navigateur, entrez ce que vous avez obtenu à partir de `http://127.0.0.1:4040` la fenêtre terminal précédente.</span><span class="sxs-lookup"><span data-stu-id="8b3df-484">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="8b3df-485">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b3df-485">The following image is an example:</span></span>

    ![Test ngrok des équipes de bot d’th](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="8b3df-487">.</span><span class="sxs-lookup"><span data-stu-id="8b3df-487">.</span></span>

> [!NOTE]
> <span data-ttu-id="8b3df-488">Si vous arrêtez et redémarrez ngrok, l’URL change.</span><span class="sxs-lookup"><span data-stu-id="8b3df-488">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="8b3df-489">Pour utiliser ngrok dans votre projet et en fonction des fonctionnalités que vous utilisez, vous devez mettre à jour toutes les références d’URL.</span><span class="sxs-lookup"><span data-stu-id="8b3df-489">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="8b3df-490">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8b3df-490">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="8b3df-491">TeamsAppManifest/manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="8b3df-491">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="8b3df-492">Ce manifeste contient les informations requises par Microsoft Teams pour se connecter au bot.</span><span class="sxs-lookup"><span data-stu-id="8b3df-492">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

<span data-ttu-id="8b3df-493">Avec l’authentification, Teams se comporte légèrement différemment des autres canaux, comme expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b3df-493">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="8b3df-494">Gestion de l’activité d’appel</span><span class="sxs-lookup"><span data-stu-id="8b3df-494">Handling Invoke Activity</span></span>

<span data-ttu-id="8b3df-495">Une **activité d’appel** est envoyée au bot au lieu de l’activité d’événement utilisée par d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="8b3df-495">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="8b3df-496">Cette action est effectuée en sous-classant **l’ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="8b3df-496">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8b3df-497">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8b3df-497">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="8b3df-498">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="8b3df-498">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="8b3df-499">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="8b3df-499">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="8b3df-500">*L’activité d’appel* doit être transmis à la boîte de dialogue si **le OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8b3df-500">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="8b3df-501">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="8b3df-501">TeamsActivityHandler.cs</span></span>

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[<span data-ttu-id="8b3df-502">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8b3df-502">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="8b3df-503">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="8b3df-503">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="8b3df-504">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="8b3df-504">**bots/teamsBot.js**</span></span>

<span data-ttu-id="8b3df-505">*L’activité d’appel* doit être transmis à la boîte de dialogue si **le OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8b3df-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="8b3df-506">**dialogs/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="8b3df-506">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="8b3df-507">Dans une étape de boîte de dialogue, utilisez `beginDialog` pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="8b3df-507">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="8b3df-508">Si l’utilisateur est déjà inscrit, cela génère un événement de réponse de jeton, sans invite de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-508">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="8b3df-509">Sinon, cela invite l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="8b3df-509">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="8b3df-510">Le service Azure Bot envoie l’événement de réponse du jeton après que l’utilisateur a tenté de se connecter.</span><span class="sxs-lookup"><span data-stu-id="8b3df-510">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="8b3df-511">Dans l’étape de boîte de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="8b3df-511">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="8b3df-512">S’il n’est pas null, l’utilisateur s’est correctement inscrit.</span><span class="sxs-lookup"><span data-stu-id="8b3df-512">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="8b3df-513">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="8b3df-513">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="8b3df-514">Python</span><span class="sxs-lookup"><span data-stu-id="8b3df-514">Python</span></span>](#tab/python-sample)

<span data-ttu-id="8b3df-515">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="8b3df-515">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="8b3df-516">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="8b3df-516">**bots/teams_bot.py**</span></span>

<span data-ttu-id="8b3df-517">*L’activité d’appel* doit être transmis à la boîte de dialogue si **le OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8b3df-517">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="8b3df-518">**dialogs/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="8b3df-518">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="8b3df-519">Dans une étape de boîte de dialogue, utilisez `begin_dialog` pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="8b3df-519">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="8b3df-520">Si l’utilisateur est déjà inscrit, cela génère un événement de réponse de jeton, sans invite de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8b3df-520">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="8b3df-521">Sinon, cela invite l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="8b3df-521">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="8b3df-522">Le service Azure Bot envoie l’événement de réponse du jeton après que l’utilisateur a tenté de se connecter.</span><span class="sxs-lookup"><span data-stu-id="8b3df-522">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="8b3df-523">Dans l’étape de boîte de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="8b3df-523">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="8b3df-524">S’il n’est pas null, l’utilisateur s’est correctement inscrit.</span><span class="sxs-lookup"><span data-stu-id="8b3df-524">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="8b3df-525">**dialogs/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="8b3df-525">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="8b3df-526">En savoir plus sur l’ajout d’authentification via Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="8b3df-526">Learn about adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
