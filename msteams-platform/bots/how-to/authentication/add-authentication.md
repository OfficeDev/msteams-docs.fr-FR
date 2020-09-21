---
title: Ajouter l’authentification à votre robot teams
author: clearab
description: Comment ajouter l’authentification OAuth à un bot dans Microsoft Teams.
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 403072efeccdd09e46ac93e2e811ee2d10131668
ms.sourcegitcommit: aabfd65a67e1889ec16f09476bc757dd4a46ec5b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "48097885"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="bce7d-103">Ajouter l’authentification à votre robot teams</span><span class="sxs-lookup"><span data-stu-id="bce7d-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="bce7d-104">Dans certains cas, vous devrez peut-être créer des robots dans Microsoft teams qui peuvent accéder aux ressources au nom de l’utilisateur, tel qu’un service de messagerie.</span><span class="sxs-lookup"><span data-stu-id="bce7d-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="bce7d-105">Cet article explique comment utiliser l’authentification du kit de développement logiciel (SDK) de l’outil Azure bot Service v4, basée sur OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="bce7d-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="bce7d-106">Ainsi, il est plus facile de développer un bot qui peut utiliser des jetons d’authentification en fonction des informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="bce7d-107">Key dans tout ceci est l’utilisation de **fournisseurs d’identité**, comme nous le verrons plus tard.</span><span class="sxs-lookup"><span data-stu-id="bce7d-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="bce7d-108">OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="bce7d-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="bce7d-109">Une compréhension de base de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans Teams.</span><span class="sxs-lookup"><span data-stu-id="bce7d-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="bce7d-110">Voir [OAuth 2 simplifiée](https://aka.ms/oauth2-simplified) pour une compréhension de base et [OAuth 2,0](https://oauth.net/2/) pour la spécification complète.</span><span class="sxs-lookup"><span data-stu-id="bce7d-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="bce7d-111">Pour plus d’informations sur la façon dont le service Azure bot gère l’authentification, consultez [la rubrique authentification des utilisateurs au sein d’une conversation](https://aka.ms/azure-bot-authentication).</span><span class="sxs-lookup"><span data-stu-id="bce7d-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="bce7d-112">Voici les titres des sections de cet article :</span><span class="sxs-lookup"><span data-stu-id="bce7d-112">In this article you'll learn:</span></span>

- <span data-ttu-id="bce7d-113">**Comment créer un bot compatible avec l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="bce7d-114">Vous utiliserez [CS-Auth-Sample][teams-auth-bot-cs] pour gérer les informations d’identification de connexion de l’utilisateur et la génération du jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="bce7d-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="bce7d-115">**Comment déployer le bot sur Azure et l’associer à un fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="bce7d-116">Le fournisseur émet un jeton basé sur les informations d’identification de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="bce7d-117">Le bot peut utiliser le jeton pour accéder aux ressources, telles qu’un service de messagerie, qui requiert l’authentification.</span><span class="sxs-lookup"><span data-stu-id="bce7d-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="bce7d-118">Pour plus d’informations, consultez la rubrique  [flux d’authentification de Microsoft teams pour les robots](auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="bce7d-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="bce7d-119">**Comment intégrer le robot dans Microsoft teams**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="bce7d-120">Une fois le robot intégré, vous pouvez vous connecter et échanger des messages avec celui-ci dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="bce7d-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bce7d-121">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="bce7d-121">Prerequisites</span></span>

- <span data-ttu-id="bce7d-122">Connaissance des [notions de base des robots][concept-basics], de la gestion de l' [État][concept-state], de la bibliothèque de [boîtes de dialogue][concept-dialogs]et de la mise en œuvre d’un [flux de conversation séquentiel][simple-dialog].</span><span class="sxs-lookup"><span data-stu-id="bce7d-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="bce7d-123">Connaissance des développements Azure et OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="bce7d-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="bce7d-124">Les versions actuelles de Visual Studio et de git.</span><span class="sxs-lookup"><span data-stu-id="bce7d-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="bce7d-125">Compte Azure.</span><span class="sxs-lookup"><span data-stu-id="bce7d-125">Azure account.</span></span> <span data-ttu-id="bce7d-126">Si nécessaire, vous pouvez créer un [compte Azure gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="bce7d-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="bce7d-127">L’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="bce7d-127">The following sample.</span></span>

    | <span data-ttu-id="bce7d-128">Échantillon</span><span class="sxs-lookup"><span data-stu-id="bce7d-128">Sample</span></span> | <span data-ttu-id="bce7d-129">Version d’BotBuilder</span><span class="sxs-lookup"><span data-stu-id="bce7d-129">BotBuilder version</span></span> | <span data-ttu-id="bce7d-130">Montre</span><span class="sxs-lookup"><span data-stu-id="bce7d-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="bce7d-131">**Authentification bot** dans [CS-Auth-Sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="bce7d-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="bce7d-132">v4</span><span class="sxs-lookup"><span data-stu-id="bce7d-132">v4</span></span> | <span data-ttu-id="bce7d-133">Prise en charge OAuthCard</span><span class="sxs-lookup"><span data-stu-id="bce7d-133">OAuthCard support</span></span> |
    | <span data-ttu-id="bce7d-134">**Authentification bot** dans [js-auth-Sample][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="bce7d-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="bce7d-135">v4</span><span class="sxs-lookup"><span data-stu-id="bce7d-135">v4</span></span>| <span data-ttu-id="bce7d-136">Prise en charge OAuthCard</span><span class="sxs-lookup"><span data-stu-id="bce7d-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="bce7d-137">**Authentification de robot** dans la [py-auth-Sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="bce7d-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="bce7d-138">v4</span><span class="sxs-lookup"><span data-stu-id="bce7d-138">v4</span></span> | <span data-ttu-id="bce7d-139">Prise en charge OAuthCard</span><span class="sxs-lookup"><span data-stu-id="bce7d-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="bce7d-140">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="bce7d-140">Create the resource group</span></span>

<span data-ttu-id="bce7d-141">Le groupe de ressources et le plan de service ne sont pas strictement nécessaires, mais ils vous permettent de libérer facilement les ressources que vous créez.</span><span class="sxs-lookup"><span data-stu-id="bce7d-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="bce7d-142">Cette pratique est intéressante pour maintenir l’organisation et la gestion de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="bce7d-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="bce7d-143">Vous utilisez un groupe de ressources pour créer des ressources individuelles pour l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="bce7d-144">Pour des performances optimales, vérifiez que ces ressources se trouvent dans la même région Azure.</span><span class="sxs-lookup"><span data-stu-id="bce7d-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="bce7d-145">Dans votre navigateur, connectez-vous au [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="bce7d-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="bce7d-146">Dans le volet de navigation de gauche, sélectionnez **groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="bce7d-147">Dans le coin supérieur gauche de la fenêtre affichée, sélectionnez **Ajouter** un onglet pour créer un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bce7d-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="bce7d-148">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bce7d-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="bce7d-149">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-149">**Subscription**.</span></span> <span data-ttu-id="bce7d-150">Utilisez votre abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="bce7d-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="bce7d-151">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-151">**Resource group**.</span></span> <span data-ttu-id="bce7d-152">Entrez le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bce7d-152">Enter the name for the resource group.</span></span> <span data-ttu-id="bce7d-153">Un exemple peut être  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="bce7d-154">N’oubliez pas que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="bce7d-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="bce7d-155">Dans le menu déroulant **région** , sélectionnez *anglais (États-Unis*) ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="bce7d-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="bce7d-156">Sélectionnez le bouton **vérifier et créer** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-156">Select the **Review and create** button.</span></span> <span data-ttu-id="bce7d-157">Vous devriez voir une bannière indiquant que la *validation a réussi*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="bce7d-158">Sélectionnez le bouton **créer** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-158">Select the **Create** button.</span></span> <span data-ttu-id="bce7d-159">La création du groupe de ressources peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="bce7d-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="bce7d-160">Comme pour les ressources que vous allez créer plus loin dans ce didacticiel, nous vous recommandons de épingler ce groupe de ressources à votre tableau de bord pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="bce7d-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="bce7d-161">Si vous souhaitez le faire, sélectionnez l’icône de code confidentiel & # 128204 ; dans le coin supérieur droit du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="bce7d-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="bce7d-162">Créer le plan de service</span><span class="sxs-lookup"><span data-stu-id="bce7d-162">Create the service plan</span></span>

1. <span data-ttu-id="bce7d-163">Dans le [**portail Azure**][azure-portal], dans le volet de navigation de gauche, sélectionnez **créer une ressource**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="bce7d-164">Dans la zone de recherche, tapez *plan de service d’application*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="bce7d-165">Sélectionnez la carte **app service plan** dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="bce7d-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="bce7d-166">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-166">Select **Create**.</span></span>
1. <span data-ttu-id="bce7d-167">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bce7d-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="bce7d-168">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-168">**Subscription**.</span></span> <span data-ttu-id="bce7d-169">Vous pouvez utiliser un abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="bce7d-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="bce7d-170">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-170">**Resource Group**.</span></span> <span data-ttu-id="bce7d-171">Sélectionnez le groupe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="bce7d-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="bce7d-172">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-172">**Name**.</span></span> <span data-ttu-id="bce7d-173">Entrez le nom du plan de service.</span><span class="sxs-lookup"><span data-stu-id="bce7d-173">Enter the name for the service plan.</span></span> <span data-ttu-id="bce7d-174">Un exemple peut être  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="bce7d-175">N’oubliez pas que le nom doit être unique au sein du groupe.</span><span class="sxs-lookup"><span data-stu-id="bce7d-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="bce7d-176">**Système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-176">**Operating System**.</span></span> <span data-ttu-id="bce7d-177">Sélectionnez *Windows* ou votre système d’exploitation applicable.</span><span class="sxs-lookup"><span data-stu-id="bce7d-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="bce7d-178">**Région**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-178">**Region**.</span></span> <span data-ttu-id="bce7d-179">Sélectionnez *West US* ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="bce7d-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="bce7d-180">**Niveau de tarification**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-180">**Pricing Tier**.</span></span> <span data-ttu-id="bce7d-181">Assurez-vous que l’option *standard S1* est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="bce7d-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="bce7d-182">Il doit s’agir de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="bce7d-182">This should be the default value.</span></span>
    1. <span data-ttu-id="bce7d-183">Sélectionnez le bouton **vérifier et créer** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-183">Select the **Review and create** button.</span></span> <span data-ttu-id="bce7d-184">Vous devriez voir une bannière indiquant que la *validation a réussi*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="bce7d-185">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-185">Select **Create**.</span></span> <span data-ttu-id="bce7d-186">La création du plan de service d’application peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="bce7d-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="bce7d-187">Le plan est affiché dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bce7d-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="bce7d-188">Création de l’enregistrement des canaux de robots</span><span class="sxs-lookup"><span data-stu-id="bce7d-188">Create the bot channels registration</span></span>

<span data-ttu-id="bce7d-189">L’inscription des canaux de robots enregistre votre service Web en tant que bot avec l’infrastructure de robot, à condition que vous disposiez d’un ID d’application Microsoft et d’un mot de passe d’application (clé secrète client).</span><span class="sxs-lookup"><span data-stu-id="bce7d-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bce7d-190">Il vous suffit d’enregistrer votre robot s’il n’est pas hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bce7d-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="bce7d-191">Si vous avez [créé un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) via le portail Azure, il est déjà enregistré auprès du service.</span><span class="sxs-lookup"><span data-stu-id="bce7d-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="bce7d-192">Si vous avez créé votre bot via l' [infrastructure bot](https://dev.botframework.com/bots/new) ou [AppStudio](~/concepts/build-and-test/app-studio-overview.md) , votre bot n’est pas enregistré dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bce7d-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="bce7d-193">La ressource d’inscription des canaux de robots affiche la région **globale** , même si vous avez sélectionné West US.</span><span class="sxs-lookup"><span data-stu-id="bce7d-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="bce7d-194">Ceci est normal.</span><span class="sxs-lookup"><span data-stu-id="bce7d-194">This is expected.</span></span>

<span data-ttu-id="bce7d-195">Pour plus d’informations, consultez [la rubrique Create a bot for teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="bce7d-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="bce7d-196">Créer le fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="bce7d-196">Create the identity provider</span></span>

<span data-ttu-id="bce7d-197">Vous avez besoin d’un fournisseur d’identité qui peut être utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="bce7d-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="bce7d-198">Dans cette procédure, vous allez utiliser un fournisseur Azure AD ; d’autres fournisseurs d’identité pris en charge par Azure AD peuvent également être utilisés.</span><span class="sxs-lookup"><span data-stu-id="bce7d-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="bce7d-199">Dans le [**portail Azure**][azure-portal], dans le volet de navigation de gauche, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="bce7d-200">Vous devrez créer et enregistrer cette ressource Azure AD dans un client dans lequel vous pouvez consentir à déléguer les autorisations demandées par une application.</span><span class="sxs-lookup"><span data-stu-id="bce7d-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="bce7d-201">Pour obtenir des instructions sur la création d’un client, consultez [la rubrique accéder au portail et créer un client](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span><span class="sxs-lookup"><span data-stu-id="bce7d-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="bce7d-202">Dans le volet gauche, sélectionnez **inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="bce7d-203">Dans le volet droit, sélectionnez l’onglet **nouvel enregistrement** , dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="bce7d-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="bce7d-204">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bce7d-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="bce7d-205">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-205">**Name**.</span></span> <span data-ttu-id="bce7d-206">Entrez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="bce7d-206">Enter the name for the application.</span></span> <span data-ttu-id="bce7d-207">Un exemple peut être  *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="bce7d-208">N’oubliez pas que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="bce7d-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="bce7d-209">Sélectionnez les **types de comptes pris en charge** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="bce7d-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="bce7d-210">Sélectionnez des *comptes dans n’importe quel annuaire d’organisation (n’importe quel compte Azure ad Directory-multiclient) et des comptes Microsoft personnels (par exemple, Skype, Xbox)*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="bce7d-211">Pour l' **URI de redirection**:</span><span class="sxs-lookup"><span data-stu-id="bce7d-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="bce7d-212">&#x2713;sélectionnez **Web**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="bce7d-213">&#x2713; définissez l’URL sur `https://token.botframework.com/.auth/web/redirect` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="bce7d-214">Sélectionnez **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-214">Select **Register**.</span></span>

1. <span data-ttu-id="bce7d-215">Une fois créé, Azure affiche la page de **vue d’ensemble** de l’application.</span><span class="sxs-lookup"><span data-stu-id="bce7d-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="bce7d-216">Copiez et enregistrez les informations suivantes dans un fichier :</span><span class="sxs-lookup"><span data-stu-id="bce7d-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="bce7d-217">Valeur de l’ID de l' **application (client)** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="bce7d-218">Vous utiliserez cette valeur ultérieurement comme *ID client* lorsque vous enregistrerez cette application d’identité Azure avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="bce7d-219">Valeur de l' **ID d’annuaire (locataire)** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="bce7d-220">Vous utiliserez également cette valeur ultérieurement comme *ID de client* pour enregistrer cette application d’identité Azure avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="bce7d-221">Dans le volet gauche, sélectionnez **certificats & secrets** pour créer une clé secrète client pour votre application.</span><span class="sxs-lookup"><span data-stu-id="bce7d-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="bce7d-222">Sous **secrets client**, sélectionnez &#x2795; **nouvelle clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="bce7d-223">Ajoutez une description pour identifier cette clé secrète auprès d’autres personnes que vous devrez peut-être créer pour cette application, telle que *l’application d’identité bot dans teams*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="bce7d-224">Définit **expire** à votre sélection.</span><span class="sxs-lookup"><span data-stu-id="bce7d-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="bce7d-225">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-225">Select **Add**.</span></span>
   1. <span data-ttu-id="bce7d-226">Avant de quitter cette page, **Enregistrez la clé secrète**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="bce7d-227">Vous utiliserez cette valeur ultérieurement comme _clé secrète client_ lorsque vous enregistrerez votre application Azure ad avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="bce7d-228">Configurer la connexion du fournisseur d’identité et l’inscrire auprès du robot</span><span class="sxs-lookup"><span data-stu-id="bce7d-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="bce7d-229">Remarque : il existe deux options pour les fournisseurs de services ici-Azure AD v1 et Azure AD v2.</span><span class="sxs-lookup"><span data-stu-id="bce7d-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="bce7d-230">Les différences entre les deux fournisseurs sont résumées [ici](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), mais en général, la version 2 offre davantage de flexibilité en ce qui concerne la modification des autorisations du bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="bce7d-231">Les autorisations de l’API Graph sont répertoriées dans le champ étendues et, lorsque de nouvelles sont ajoutées, les robots permettent aux utilisateurs de consentir aux nouvelles autorisations lors de la connexion suivante.</span><span class="sxs-lookup"><span data-stu-id="bce7d-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="bce7d-232">Pour v1, le consentement du bot doit être supprimé par l’utilisateur pour que de nouvelles autorisations soient demandées dans la boîte de dialogue OAuth.</span><span class="sxs-lookup"><span data-stu-id="bce7d-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="bce7d-233">Azure AD v1</span><span class="sxs-lookup"><span data-stu-id="bce7d-233">Azure AD V1</span></span>

1. <span data-ttu-id="bce7d-234">Dans le [**portail Azure**][azure-portal], sélectionnez votre groupe de ressources dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="bce7d-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="bce7d-235">Sélectionnez le lien d’inscription de votre robot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="bce7d-236">Sur la page des ressources, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-236">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="bce7d-237">Sous **paramètres de connexion OAuth** , dans la partie inférieure de la page, sélectionnez **Ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-237">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="bce7d-238">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="bce7d-238">Complete the form as follows:</span></span>

    1. <span data-ttu-id="bce7d-239">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-239">**Name**.</span></span> <span data-ttu-id="bce7d-240">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="bce7d-240">Enter a name for the connection.</span></span> <span data-ttu-id="bce7d-241">Vous utiliserez ce nom dans votre robot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="bce7d-241">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="bce7d-242">Par exemple *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-242">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="bce7d-243">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-243">**Service Provider**.</span></span> <span data-ttu-id="bce7d-244">Sélectionner **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-244">Select **Azure Active Directory**.</span></span> <span data-ttu-id="bce7d-245">Une fois que vous avez sélectionné cette option, les champs spécifiques à Azure AD sont affichés.</span><span class="sxs-lookup"><span data-stu-id="bce7d-245">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="bce7d-246">**ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="bce7d-246">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="bce7d-247">**Clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-247">**Client secret**.</span></span> <span data-ttu-id="bce7d-248">Entrez le secret que vous avez enregistré pour votre application Azure Identity Provider dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="bce7d-248">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="bce7d-249">**Type d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-249">**Grant Type**.</span></span> <span data-ttu-id="bce7d-250">Entrée `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-250">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="bce7d-251">**URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-251">**Login URL**.</span></span> <span data-ttu-id="bce7d-252">Entrée `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-252">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="bce7d-253">**ID de client**, entrez l' **ID de répertoire (locataire)** que vous avez enregistré précédemment pour votre application d’identité Azure ou **courant** en fonction du type de compte pris en charge sélectionné lors de la création de l’application du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="bce7d-253">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="bce7d-254">Pour déterminer la valeur à affecter, suivez ces critères :</span><span class="sxs-lookup"><span data-stu-id="bce7d-254">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="bce7d-255">Si vous avez sélectionné l’un des *comptes de cet annuaire d’organisation uniquement (Microsoft uniquement-client unique)* ou *des comptes dans n’importe quel annuaire d’organisation (Microsoft AAD Directory-multi-client),* entrez l' **ID de client** que vous avez enregistré précédemment pour l’application AAD.</span><span class="sxs-lookup"><span data-stu-id="bce7d-255">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="bce7d-256">Il s’agira du client associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="bce7d-256">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="bce7d-257">Si vous avez sélectionné *comptes dans n’importe quel annuaire d’organisation (tous les comptes Microsoft AAD Directory-clients multiples et personnels, par exemple Skype, Xbox, Outlook)* , entrez le mot **commun** au lieu d’un ID de client.</span><span class="sxs-lookup"><span data-stu-id="bce7d-257">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="bce7d-258">Dans le cas contraire, l’application AAD vérifie via le client dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="bce7d-258">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="bce7d-259">h.</span><span class="sxs-lookup"><span data-stu-id="bce7d-259">h.</span></span> <span data-ttu-id="bce7d-260">Pour **URL de ressource**, entrez `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-260">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="bce7d-261">Cela n’est pas utilisé dans l’exemple de code actuel.</span><span class="sxs-lookup"><span data-stu-id="bce7d-261">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="bce7d-262">i.</span><span class="sxs-lookup"><span data-stu-id="bce7d-262">i.</span></span> <span data-ttu-id="bce7d-263">Laissez les **étendues** vides.</span><span class="sxs-lookup"><span data-stu-id="bce7d-263">Leave **Scopes** blank.</span></span> <span data-ttu-id="bce7d-264">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="bce7d-264">The following image is an example:</span></span>

    ![chaîne de connexion d’authentification de l’application robots teams ADV1 affichage](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="bce7d-266">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-266">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="bce7d-267">Azure AD v2</span><span class="sxs-lookup"><span data-stu-id="bce7d-267">Azure AD V2</span></span>

1. <span data-ttu-id="bce7d-268">Dans le [**portail Azure**][azure-portal], sélectionnez votre groupe de ressources dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="bce7d-268">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="bce7d-269">Sélectionnez le lien d’inscription de votre robot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-269">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="bce7d-270">Sur la page des ressources, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-270">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="bce7d-271">Sous **paramètres de connexion OAuth** , dans la partie inférieure de la page, sélectionnez **Ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-271">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="bce7d-272">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="bce7d-272">Complete the form as follows:</span></span>

    1. <span data-ttu-id="bce7d-273">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-273">**Name**.</span></span> <span data-ttu-id="bce7d-274">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="bce7d-274">Enter a name for the connection.</span></span> <span data-ttu-id="bce7d-275">Vous utiliserez ce nom dans votre robot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="bce7d-275">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="bce7d-276">Par exemple *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-276">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="bce7d-277">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-277">**Service Provider**.</span></span> <span data-ttu-id="bce7d-278">Sélectionnez **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-278">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="bce7d-279">Une fois que vous avez sélectionné cette option, les champs spécifiques à Azure AD sont affichés.</span><span class="sxs-lookup"><span data-stu-id="bce7d-279">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="bce7d-280">**ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="bce7d-280">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="bce7d-281">**Clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-281">**Client secret**.</span></span> <span data-ttu-id="bce7d-282">Entrez le secret que vous avez enregistré pour votre application Azure Identity Provider dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="bce7d-282">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="bce7d-283">**URL d’échange de jetons**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-283">**Token Exchange URL**.</span></span> <span data-ttu-id="bce7d-284">Laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="bce7d-284">Leave this blank.</span></span>
    1. <span data-ttu-id="bce7d-285">**ID de client**, entrez l' **ID de répertoire (locataire)** que vous avez enregistré précédemment pour votre application d’identité Azure ou **courant** en fonction du type de compte pris en charge sélectionné lors de la création de l’application du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="bce7d-285">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="bce7d-286">Pour déterminer la valeur à affecter, suivez ces critères :</span><span class="sxs-lookup"><span data-stu-id="bce7d-286">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="bce7d-287">Si vous avez sélectionné l’un des *comptes de cet annuaire d’organisation uniquement (Microsoft uniquement-client unique)* ou *des comptes dans n’importe quel annuaire d’organisation (Microsoft AAD Directory-multi-client),* entrez l' **ID de client** que vous avez enregistré précédemment pour l’application AAD.</span><span class="sxs-lookup"><span data-stu-id="bce7d-287">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="bce7d-288">Il s’agira du client associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="bce7d-288">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="bce7d-289">Si vous avez sélectionné *comptes dans n’importe quel annuaire d’organisation (tous les comptes Microsoft AAD Directory-clients multiples et personnels, par exemple Skype, Xbox, Outlook)* , entrez le mot **commun** au lieu d’un ID de client.</span><span class="sxs-lookup"><span data-stu-id="bce7d-289">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="bce7d-290">Dans le cas contraire, l’application AAD vérifie via le client dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="bce7d-290">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="bce7d-291">Pour les **étendues**, entrez une liste séparée par des espaces des autorisations de graphique dont cette application a besoin, par exemple : User. Read User. ReadBasic. All Mail. Read</span><span class="sxs-lookup"><span data-stu-id="bce7d-291">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="bce7d-292">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-292">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="bce7d-293">Tester la connexion</span><span class="sxs-lookup"><span data-stu-id="bce7d-293">Test the connection</span></span>

1. <span data-ttu-id="bce7d-294">Sélectionnez l’entrée de connexion pour ouvrir la connexion que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="bce7d-294">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="bce7d-295">Sélectionnez **tester la connexion** en haut du panneau **paramètres de connexion du fournisseur de services** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-295">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="bce7d-296">La première fois que vous effectuez cette opération, une nouvelle fenêtre de navigateur s’ouvre et vous invite à sélectionner un compte.</span><span class="sxs-lookup"><span data-stu-id="bce7d-296">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="bce7d-297">Sélectionnez celle que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="bce7d-297">Select the one you want to use.</span></span>
1. <span data-ttu-id="bce7d-298">Ensuite, vous serez invité à autoriser le fournisseur d’identité à utiliser vos données (informations d’identification).</span><span class="sxs-lookup"><span data-stu-id="bce7d-298">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="bce7d-299">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="bce7d-299">The following image is an example:</span></span>

    ![chaîne de connexion d’authentification de teams bot ADV1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="bce7d-301">Sélectionnez **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-301">Select **Accept**.</span></span>
1. <span data-ttu-id="bce7d-302">Cela doit ensuite vous rediriger vers une page de **test de connexion à la \<your-connection-name> réussite** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-302">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="bce7d-303">Actualisez la page si vous obtenez une erreur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-303">Refresh the page if you get an error.</span></span> <span data-ttu-id="bce7d-304">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="bce7d-304">The following image is an example:</span></span>

  ![chaîne de connexion d’authentification de l’application robots teams ADV1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="bce7d-306">Le nom de connexion est utilisé par le code de robot pour récupérer des jetons d’authentification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-306">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="bce7d-307">Préparation de l’exemple de code bot</span><span class="sxs-lookup"><span data-stu-id="bce7d-307">Prepare the bot sample code</span></span>

<span data-ttu-id="bce7d-308">Une fois les paramètres préliminaires effectués, nous allons nous concentrer sur la création du bot à utiliser dans cet article.</span><span class="sxs-lookup"><span data-stu-id="bce7d-308">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="bce7d-309">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="bce7d-309">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="bce7d-310">Clone [CS-Auth-Sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="bce7d-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="bce7d-311">Lancez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bce7d-311">Launch Visual Studio.</span></span>
1. <span data-ttu-id="bce7d-312">Dans la barre d’outils, sélectionnez **fichier-> ouvrir-> projet/solution** et ouvrir le projet bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-312">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="bce7d-313">Dans la mise à jour C# **appsettings.jsez** comme suit :</span><span class="sxs-lookup"><span data-stu-id="bce7d-313">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="bce7d-314">Définissez `ConnectionName` le nom de la connexion du fournisseur d’identité que vous avez ajoutée à l’enregistrement du canal du robot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-314">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="bce7d-315">Le nom que nous avons utilisé dans cet exemple est *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-315">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="bce7d-316">Définissez `MicrosoftAppId` l’ID de l' **application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-316">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="bce7d-317">Définissez `MicrosoftAppPassword` la **clé secrète client** que vous avez enregistrée au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-317">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="bce7d-318">Définissez le `ConnectionName` sur le nom de la connexion du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="bce7d-318">Set the `ConnectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="bce7d-319">En fonction des caractères de votre clé secrète, il se peut que vous deviez utiliser le mot de passe XML.</span><span class="sxs-lookup"><span data-stu-id="bce7d-319">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="bce7d-320">Par exemple, tous les esperluettes (&) doivent être codés en tant que `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-320">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="bce7d-321">Dans l’Explorateur de solutions, accédez au `TeamsAppManifest` dossier, ouvrez `manifest.json` et définissez `id` `botId` l’ID d' **application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-321">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="bce7d-322">JavaScript</span><span class="sxs-lookup"><span data-stu-id="bce7d-322">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="bce7d-323">Clone [node-auth-Sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="bce7d-323">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="bce7d-324">Dans une console, accédez au projet :</span><span class="sxs-lookup"><span data-stu-id="bce7d-324">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="bce7d-325">Modules d’installation</span><span class="sxs-lookup"><span data-stu-id="bce7d-325">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="bce7d-326">Mettez à jour la configuration **. env** comme suit :</span><span class="sxs-lookup"><span data-stu-id="bce7d-326">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="bce7d-327">Définissez `MicrosoftAppId` l’ID de l' **application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-327">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="bce7d-328">Définissez `MicrosoftAppPassword` la **clé secrète client** que vous avez enregistrée au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-328">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="bce7d-329">Définissez le `connectionName` sur le nom de la connexion du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="bce7d-329">Set the `connectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="bce7d-330">En fonction des caractères de votre clé secrète, il se peut que vous deviez utiliser le mot de passe XML.</span><span class="sxs-lookup"><span data-stu-id="bce7d-330">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="bce7d-331">Par exemple, tous les esperluettes (&) doivent être codés en tant que `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-331">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="bce7d-332">Dans le `teamsAppManifest` dossier, ouvrez `manifest.json` et définissez l' `id`  ID de votre **application Microsoft** et `botId` l' **ID de l’application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-332">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="bce7d-333">Python</span><span class="sxs-lookup"><span data-stu-id="bce7d-333">Python</span></span>](#tab/python)

1. <span data-ttu-id="bce7d-334">Clone [py-auth-Sample][teams-auth-bot-py] à partir du référentiel github.</span><span class="sxs-lookup"><span data-stu-id="bce7d-334">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="bce7d-335">Mettre à jour **config.py**:</span><span class="sxs-lookup"><span data-stu-id="bce7d-335">Update **config.py**:</span></span>

    - <span data-ttu-id="bce7d-336">Définissez `ConnectionName` le nom du paramètre de connexion OAuth que vous avez ajouté à votre bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-336">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="bce7d-337">Défini `MicrosoftAppId` et `MicrosoftAppPassword` à l’ID de l’application et à la clé secrète de l’application de votre bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-337">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="bce7d-338">En fonction des caractères de votre clé secrète, il se peut que vous deviez utiliser le mot de passe XML.</span><span class="sxs-lookup"><span data-stu-id="bce7d-338">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="bce7d-339">Par exemple, tous les esperluettes (&) doivent être codés en tant que `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-339">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="bce7d-340">Déployer le bot sur Azure</span><span class="sxs-lookup"><span data-stu-id="bce7d-340">Deploy the bot to Azure</span></span>

<span data-ttu-id="bce7d-341">Pour déployer le robot, suivez les étapes décrites dans la procédure de [déploiement de votre robot sur Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="bce7d-341">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="bce7d-342">Par ailleurs, dans Visual Studio, vous pouvez suivre les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="bce7d-342">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="bce7d-343">Dans l' *Explorateur de solutions* Visual Studio, sélectionnez le nom du projet (ou cliquez avec le bouton droit).</span><span class="sxs-lookup"><span data-stu-id="bce7d-343">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="bce7d-344">Dans le menu déroulant, sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-344">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="bce7d-345">Dans la fenêtre affichée, sélectionnez le **nouveau** lien.</span><span class="sxs-lookup"><span data-stu-id="bce7d-345">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="bce7d-346">Dans la fenêtre de boîte de dialogue, sélectionnez **app service** sur la gauche et **créer un nouveau** à droite.</span><span class="sxs-lookup"><span data-stu-id="bce7d-346">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="bce7d-347">Sélectionnez le bouton **publier** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-347">Select the **Publish** button.</span></span>
1. <span data-ttu-id="bce7d-348">Dans la fenêtre de boîte de dialogue suivante, entrez les informations requises.</span><span class="sxs-lookup"><span data-stu-id="bce7d-348">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="bce7d-349">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="bce7d-349">The following is an example:</span></span>

   ![AUTH-App-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="bce7d-351">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-351">Select **Create**.</span></span>
1. <span data-ttu-id="bce7d-352">Si le déploiement réussit, vous devriez le voir apparaître dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bce7d-352">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="bce7d-353">De plus, une page s’affiche dans votre navigateur par défaut pour dire que *votre robot est prêt !*.</span><span class="sxs-lookup"><span data-stu-id="bce7d-353">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="bce7d-354">L’URL sera semblable à ceci : `https://botteamsauth.azurewebsites.net/` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-354">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="bce7d-355">Enregistrez-le dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="bce7d-355">Save it to a file.</span></span>
1. <span data-ttu-id="bce7d-356">Dans votre navigateur, accédez au [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="bce7d-356">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="bce7d-357">Vérifiez votre groupe de ressources, le bot doit être affiché avec les autres ressources.</span><span class="sxs-lookup"><span data-stu-id="bce7d-357">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="bce7d-358">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="bce7d-358">The following image is an example:</span></span>

    ![teams-bot-auth-App-service-Group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="bce7d-360">Dans le groupe ressource, sélectionnez le nom de l’enregistrement du canal bot (lien).</span><span class="sxs-lookup"><span data-stu-id="bce7d-360">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="bce7d-361">Dans le volet de gauche, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-361">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="bce7d-362">Dans la zone **point de terminaison de messagerie** , entrez l’URL obtenue ci-dessus suivie de `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-362">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="bce7d-363">Voici un exemple : `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-363">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="bce7d-364">Sélectionnez le bouton **Enregistrer** dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="bce7d-364">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="bce7d-365">Tester le bot à l’aide de l’émulateur</span><span class="sxs-lookup"><span data-stu-id="bce7d-365">Test the bot using the Emulator</span></span>

<span data-ttu-id="bce7d-366">Si vous ne l’avez pas encore fait, installez l' [émulateur de Microsoft bot Framework](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="bce7d-366">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="bce7d-367">Voir aussi [Déboguer avec l’émulateur](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="bce7d-367">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="bce7d-368">Pour que l’exemple de robot de connexion fonctionne, vous devez configurer l’émulateur comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bce7d-368">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="bce7d-369">Configurer l’émulateur pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="bce7d-369">Configure the Emulator for authentication</span></span>

<span data-ttu-id="bce7d-370">Si un bot requiert une authentification, vous devez configurer l’émulateur comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bce7d-370">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="bce7d-371">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-371">Start the Emulator.</span></span>
1. <span data-ttu-id="bce7d-372">Dans l’émulateur, sélectionnez l’icône représentant un engrenage &#9881; en bas à gauche ou l’onglet Paramètres de l' **émulateur** dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="bce7d-372">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="bce7d-373">Activez la case à cocher **utiliser les jetons d’authentification version 1,0**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-373">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="bce7d-374">Entrez le chemin d’accès local à l’outil **ngrok** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-374">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="bce7d-375">*Voir* le [wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))de l’émulateur de robot/ngrok tunneling Integration.</span><span class="sxs-lookup"><span data-stu-id="bce7d-375">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="bce7d-376">Pour plus d’informations sur l’outil, voir [ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="bce7d-376">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="bce7d-377">Activez la case à cocher **exécuter ngrok au démarrage de l’émulateur**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-377">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="bce7d-378">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-378">Select the **Save** button.</span></span>

<span data-ttu-id="bce7d-379">Lorsque le bot affiche une carte de connexion et que l’utilisateur sélectionne le bouton de connexion, l’émulateur ouvre une page que l’utilisateur peut utiliser pour se connecter avec le fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="bce7d-379">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="bce7d-380">Une fois que l’utilisateur effectue cette opération, le fournisseur génère un jeton utilisateur et l’envoie au bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-380">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="bce7d-381">Après cela, le bot peut agir au nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-381">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="bce7d-382">Tester le bot localement</span><span class="sxs-lookup"><span data-stu-id="bce7d-382">Test the bot locally</span></span>

<span data-ttu-id="bce7d-383">Une fois que vous avez configuré le mécanisme d’authentification, vous pouvez effectuer les tests de votre propre robot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-383">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="bce7d-384">Exécutez l’exemple de bot localement sur votre ordinateur, via Visual Studio par exemple.</span><span class="sxs-lookup"><span data-stu-id="bce7d-384">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="bce7d-385">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-385">Start the Emulator.</span></span>
1. <span data-ttu-id="bce7d-386">Sélectionnez le bouton **ouvrir un bot** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-386">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="bce7d-387">Dans l' **URL du robot**, entrez l’URL locale du robot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-387">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="bce7d-388">En règle générale, `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-388">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="bce7d-389">Dans l' **ID de l’application Microsoft** , entrez l’ID d’application du bot à partir de `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-389">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="bce7d-390">Dans le **mot de passe de l’application Microsoft** , entrez le mot de passe d’application du bot dans le `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-390">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="bce7d-391">Sélectionnez **se connecter**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-391">Select **Connect**.</span></span>
1. <span data-ttu-id="bce7d-392">Une fois le robot opérationnel, entrez le texte pour afficher la carte de connexion.</span><span class="sxs-lookup"><span data-stu-id="bce7d-392">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="bce7d-393">Sélectionnez le bouton **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-393">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="bce7d-394">Une boîte de dialogue contextuelle s’affiche pour **confirmer l’ouverture**de l’URL.</span><span class="sxs-lookup"><span data-stu-id="bce7d-394">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="bce7d-395">Cela permet d’authentifier l’utilisateur du robot (vous).</span><span class="sxs-lookup"><span data-stu-id="bce7d-395">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="bce7d-396">Sélectionnez **confirmer**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-396">Select **Confirm**.</span></span>
1. <span data-ttu-id="bce7d-397">Si vous y êtes invité, sélectionnez le compte de l’utilisateur concerné.</span><span class="sxs-lookup"><span data-stu-id="bce7d-397">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="bce7d-398">En fonction de la configuration que vous avez utilisée pour l’émulateur, vous obtenez l’un des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bce7d-398">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="bce7d-399">**Utilisation du code de vérification de connexion**</span><span class="sxs-lookup"><span data-stu-id="bce7d-399">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="bce7d-400">&#x2713; une fenêtre s’ouvre et affiche le code de validation.</span><span class="sxs-lookup"><span data-stu-id="bce7d-400">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="bce7d-401">&#x2713; copiez et entrez le code de validation dans la zone de conversation pour terminer la connexion.</span><span class="sxs-lookup"><span data-stu-id="bce7d-401">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="bce7d-402">**À l’aide de jetons d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-402">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="bce7d-403">&#x2713; vous êtes connecté en fonction de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="bce7d-403">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="bce7d-404">L’image suivante est un exemple de l’interface utilisateur du bot une fois que vous avez ouvert une session :</span><span class="sxs-lookup"><span data-stu-id="bce7d-404">The following image is an example of the bot UI after you've logged in:</span></span>

    ![émulateur de connexion du bot auth](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="bce7d-406">Si vous sélectionnez **Oui** lorsque le bot vous demande si *vous souhaitez afficher votre jeton ?*, vous obtiendrez une réponse semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="bce7d-406">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![jeton de l’émulateur de connexion auth bot](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="bce7d-408">Entrez **déconnexion** dans la zone de conversation d’entrée pour vous déconnecter. Cela libère le jeton d’utilisateur et le bot ne pourra pas agir en votre nom tant que vous n’aurez pas reconnecté.</span><span class="sxs-lookup"><span data-stu-id="bce7d-408">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="bce7d-409">L’authentification du robot nécessite l’utilisation du **service de connecteur bot**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-409">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="bce7d-410">Le service accède aux informations d’inscription des canaux des robots pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-410">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="bce7d-411">Tester le robot déployé</span><span class="sxs-lookup"><span data-stu-id="bce7d-411">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="bce7d-412">Dans votre navigateur, accédez au [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="bce7d-412">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="bce7d-413">Recherchez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bce7d-413">Find your resource group.</span></span>
1. <span data-ttu-id="bce7d-414">Sélectionnez le lien ressource.</span><span class="sxs-lookup"><span data-stu-id="bce7d-414">Select the resource link.</span></span> <span data-ttu-id="bce7d-415">La page de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bce7d-415">The resource page is displayed.</span></span>
1. <span data-ttu-id="bce7d-416">Dans la page des ressources, sélectionnez **tester dans la conversation Web**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-416">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="bce7d-417">Le bot démarre et affiche les messages d’accueil prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="bce7d-417">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="bce7d-418">Tapez n’importe quel élément dans la zone conversation.</span><span class="sxs-lookup"><span data-stu-id="bce7d-418">Type anything in the chat box.</span></span>
1. <span data-ttu-id="bce7d-419">Sélectionnez la zone **se connecter** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-419">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="bce7d-420">Une boîte de dialogue contextuelle s’affiche pour **confirmer l’ouverture**de l’URL.</span><span class="sxs-lookup"><span data-stu-id="bce7d-420">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="bce7d-421">Cela permet d’authentifier l’utilisateur du robot (vous).</span><span class="sxs-lookup"><span data-stu-id="bce7d-421">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="bce7d-422">Sélectionnez **confirmer**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-422">Select **Confirm**.</span></span>
1. <span data-ttu-id="bce7d-423">Si vous y êtes invité, sélectionnez le compte de l’utilisateur concerné.</span><span class="sxs-lookup"><span data-stu-id="bce7d-423">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="bce7d-424">L’image suivante est un exemple de l’interface utilisateur du bot une fois que vous avez ouvert une session :</span><span class="sxs-lookup"><span data-stu-id="bce7d-424">The following image is an example of the bot UI after you have logged in:</span></span>

    ![connexion à un bot auth déployée](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="bce7d-426">.</span><span class="sxs-lookup"><span data-stu-id="bce7d-426">.</span></span>

1. <span data-ttu-id="bce7d-427">Sélectionnez le bouton **Oui** pour afficher votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="bce7d-427">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="bce7d-428">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="bce7d-428">The following image is an example:</span></span>

    ![jeton déployé de connexion à un bot d’authentification](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="bce7d-430">.</span><span class="sxs-lookup"><span data-stu-id="bce7d-430">.</span></span>

1. <span data-ttu-id="bce7d-431">Entrez déconnexion pour vous déconnecter.</span><span class="sxs-lookup"><span data-stu-id="bce7d-431">Enter logout to sign out.</span></span>

    ![la déconnexion du robot d’authentification a été déployée](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="bce7d-433">Si vous rencontrez des problèmes lors de la connexion, essayez de tester à nouveau la connexion, comme décrit dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="bce7d-433">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="bce7d-434">Cela peut recréer le jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="bce7d-434">This could recreate the authentication token.</span></span>
> <span data-ttu-id="bce7d-435">Avec le client de conversation Web de robot dans Azure, il se peut que vous deviez vous connecter à plusieurs reprises avant l’établissement correct de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="bce7d-435">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="bce7d-436">Installer et tester le bot dans teams</span><span class="sxs-lookup"><span data-stu-id="bce7d-436">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="bce7d-437">Dans votre projet de robot, vérifiez que le `TeamsAppManifest` dossier contient `manifest.json` avec un `outline.png` et des `color.png` fichiers.</span><span class="sxs-lookup"><span data-stu-id="bce7d-437">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="bce7d-438">Dans l’Explorateur de solutions, accédez au `TeamsAppManifest` dossier.</span><span class="sxs-lookup"><span data-stu-id="bce7d-438">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="bce7d-439">Modifiez `manifest.json` en assignant les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="bce7d-439">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="bce7d-440">Assurez-vous que l' **ID d’application bot** que vous avez reçu au moment de l’enregistrement du canal bot est affecté à `id` et `botId` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-440">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="bce7d-441">Affectez cette valeur : `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-441">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="bce7d-442">Sélectionnez et **compressez** les `manifest.json` `outline.png` fichiers, et `color.png` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-442">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="bce7d-443">Ouvrez **Microsoft teams**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-443">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="bce7d-444">Dans le volet gauche, dans la partie inférieure, sélectionnez l' **icône applications**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-444">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="bce7d-445">Dans le volet droit, dans la partie inférieure, sélectionnez **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-445">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="bce7d-446">Naviguez jusqu’au `TeamsAppManifest` dossier et téléchargez le manifeste zippé.</span><span class="sxs-lookup"><span data-stu-id="bce7d-446">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="bce7d-447">L’Assistant suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="bce7d-447">The following wizard is displayed:</span></span>

    ![chargement des équipes du bot auth](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="bce7d-449">Sélectionnez le bouton **Ajouter à une équipe**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-449">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="bce7d-450">Dans la fenêtre suivante, sélectionnez l’équipe dans laquelle vous souhaitez utiliser le bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-450">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="bce7d-451">Sélectionnez le bouton **configurer un robot** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-451">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="bce7d-452">Sélectionnez les trois points (&#x25cf;&#x25cf;&#x25cf;) dans le volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="bce7d-452">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="bce7d-453">Ensuite, sélectionnez l’icône **app Studio** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-453">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="bce7d-454">Sélectionnez l’onglet **éditeur de manifeste** . L’icône du bot que vous avez téléchargé doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="bce7d-454">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="bce7d-455">De plus, vous devriez voir le robot répertorié en tant que contact dans la liste des conversations que vous pouvez utiliser pour échanger des messages avec le bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-455">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="bce7d-456">Test du bot localement dans teams</span><span class="sxs-lookup"><span data-stu-id="bce7d-456">Testing the bot locally in Teams</span></span>

<span data-ttu-id="bce7d-457">Microsoft teams est un produit entièrement basé sur le Cloud, il faut que tous les services auxquels il accède soient disponibles dans le nuage à l’aide de points de terminaison HTTPs.</span><span class="sxs-lookup"><span data-stu-id="bce7d-457">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="bce7d-458">Par conséquent, pour permettre au bot (notre exemple) de fonctionner dans Teams, vous devez soit publier le code dans le nuage de votre choix, soit rendre une instance en cours d’exécution accessible en externe via un outil de **tunneling** .</span><span class="sxs-lookup"><span data-stu-id="bce7d-458">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="bce7d-459">Nous vous recommandons d’utiliser  [ngrok](https://ngrok.com/download), qui crée une URL adressable en externe pour un port que vous ouvrez localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-459">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="bce7d-460">Pour configurer ngrok en vue de l’exécution locale de votre application Microsoft Teams, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bce7d-460">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="bce7d-461">Dans une fenêtre de terminal, accédez au répertoire dans lequel vous avez `ngrok.exe` installé.</span><span class="sxs-lookup"><span data-stu-id="bce7d-461">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="bce7d-462">Nous vous suggérons de définir le chemin d’accès de la *variable d’environnement* de sorte qu’il pointe vers lui.</span><span class="sxs-lookup"><span data-stu-id="bce7d-462">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="bce7d-463">Exécuter, par exemple, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-463">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="bce7d-464">Remplacez le numéro de port selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="bce7d-464">Replace the port number as needed.</span></span>
<span data-ttu-id="bce7d-465">Cela lance ngrok pour écouter sur le port que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="bce7d-465">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="bce7d-466">En retour, elle vous fournit une URL adressable de manière externe, valide pendant le temps que ngrok est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bce7d-466">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="bce7d-467">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="bce7d-467">The following image is an example:</span></span>

    ![chaîne de connexion d’authentification de l’application Microsoft Team bot ADV1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="bce7d-469">.</span><span class="sxs-lookup"><span data-stu-id="bce7d-469">.</span></span>

1. <span data-ttu-id="bce7d-470">Copiez l’adresse HTTPs de transfert.</span><span class="sxs-lookup"><span data-stu-id="bce7d-470">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="bce7d-471">Il doit ressembler à ce qui suit : `https://dea822bf.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-471">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="bce7d-472">Ajouter `/api/messages` pour obtenir `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-472">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="bce7d-473">Il s’agit du **point de terminaison de messages** pour le robot s’exécutant localement sur votre ordinateur et accessible via le Web dans une conversation dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="bce7d-473">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="bce7d-474">Une dernière étape consiste à mettre à jour le point de terminaison des messages du bot déployé.</span><span class="sxs-lookup"><span data-stu-id="bce7d-474">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="bce7d-475">Dans l’exemple, nous avons déployé le bot dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bce7d-475">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="bce7d-476">So \* \* nous allons effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="bce7d-476">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="bce7d-477">Dans votre navigateur, accédez au [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="bce7d-477">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="bce7d-478">Sélectionnez l' **enregistrement**de votre canal de robot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-478">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="bce7d-479">Dans le volet de gauche, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-479">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="bce7d-480">Dans le volet droit, dans la zone **point de terminaison de messagerie** , entrez l’URL ngrok, dans notre exemple, `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="bce7d-480">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="bce7d-481">Démarrez votre robot localement, par exemple en mode de débogage Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bce7d-481">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="bce7d-482">Testez le robot tout en s’exécutant localement à l’aide de la **conversation Web test**du portail de l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-482">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="bce7d-483">À l’instar de l’émulateur, ce test ne vous permet pas d’accéder aux fonctionnalités spécifiques des équipes.</span><span class="sxs-lookup"><span data-stu-id="bce7d-483">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="bce7d-484">Dans la fenêtre de terminal où `ngrok` est exécuté, vous pouvez voir le trafic http entre le bot et le client de conversation Web.</span><span class="sxs-lookup"><span data-stu-id="bce7d-484">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="bce7d-485">Si vous souhaitez une vue plus détaillée, dans une fenêtre de navigateur, entrez `http://127.0.0.1:4040` que vous avez obtenu à partir de la fenêtre de terminal précédente.</span><span class="sxs-lookup"><span data-stu-id="bce7d-485">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="bce7d-486">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="bce7d-486">The following image is an example:</span></span>

    ![tests ngrok des équipes de robots d’authentification](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="bce7d-488">.</span><span class="sxs-lookup"><span data-stu-id="bce7d-488">.</span></span>

> [!NOTE]
> <span data-ttu-id="bce7d-489">Si vous arrêtez et redémarrez ngrok, l’URL change.</span><span class="sxs-lookup"><span data-stu-id="bce7d-489">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="bce7d-490">Pour utiliser ngrok dans votre projet et selon les fonctionnalités que vous utilisez, vous devez mettre à jour toutes les références d’URL.</span><span class="sxs-lookup"><span data-stu-id="bce7d-490">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="bce7d-491">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bce7d-491">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="bce7d-492">TeamsAppManifest/manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="bce7d-492">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="bce7d-493">Ce manifeste contient les informations nécessaires à Microsoft teams pour se connecter au robot.</span><span class="sxs-lookup"><span data-stu-id="bce7d-493">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

<span data-ttu-id="bce7d-494">Avec l’authentification, teams se comporte légèrement différemment des autres canaux, comme expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bce7d-494">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="bce7d-495">Gestion de l’activité d’appel</span><span class="sxs-lookup"><span data-stu-id="bce7d-495">Handling Invoke Activity</span></span>

<span data-ttu-id="bce7d-496">Une **activité d’appel** est envoyée au bot au lieu de l’activité d’événement utilisée par d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="bce7d-496">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="bce7d-497">Cette opération est réalisée par la sous-classe du **ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="bce7d-497">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="bce7d-498">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="bce7d-498">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="bce7d-499">**Robots/DialogBot. cs**</span><span class="sxs-lookup"><span data-stu-id="bce7d-499">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="bce7d-500">**Robots/TeamsBot. cs**</span><span class="sxs-lookup"><span data-stu-id="bce7d-500">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="bce7d-501">L' *activité d’appel* doit être transférée à la boîte de dialogue si **OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="bce7d-501">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="bce7d-502">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="bce7d-502">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="bce7d-503">JavaScript</span><span class="sxs-lookup"><span data-stu-id="bce7d-503">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="bce7d-504">**robots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="bce7d-504">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="bce7d-505">**robots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="bce7d-505">**bots/teamsBot.js**</span></span>

<span data-ttu-id="bce7d-506">L' *activité d’appel* doit être transférée à la boîte de dialogue si **OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="bce7d-506">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="bce7d-507">**boîtes de dialogue/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="bce7d-507">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="bce7d-508">Dans une étape de dialogue, utilisez `beginDialog` pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="bce7d-508">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="bce7d-509">Si l’utilisateur est déjà connecté, cela génère un événement de réponse au jeton, sans demander de confirmation à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-509">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="bce7d-510">Dans le cas contraire, l’utilisateur est invité à se connecter.</span><span class="sxs-lookup"><span data-stu-id="bce7d-510">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="bce7d-511">Le service de robots Azure envoie l’événement de réponse de jeton une fois que l’utilisateur tente de se connecter.</span><span class="sxs-lookup"><span data-stu-id="bce7d-511">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="bce7d-512">Dans l’étape suivante de la boîte de dialogue, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="bce7d-512">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="bce7d-513">Si ce n’est pas le cas, l’utilisateur s’est connecté.</span><span class="sxs-lookup"><span data-stu-id="bce7d-513">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="bce7d-514">**robots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="bce7d-514">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="bce7d-515">Python</span><span class="sxs-lookup"><span data-stu-id="bce7d-515">Python</span></span>](#tab/python-sample)

<span data-ttu-id="bce7d-516">**bots/dialog_bot. py**</span><span class="sxs-lookup"><span data-stu-id="bce7d-516">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="bce7d-517">**bots/teams_bot. py**</span><span class="sxs-lookup"><span data-stu-id="bce7d-517">**bots/teams_bot.py**</span></span>

<span data-ttu-id="bce7d-518">L' *activité d’appel* doit être transférée à la boîte de dialogue si **OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="bce7d-518">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="bce7d-519">**Dialogs/main_dialog. py**</span><span class="sxs-lookup"><span data-stu-id="bce7d-519">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="bce7d-520">Dans une étape de dialogue, utilisez `begin_dialog` pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="bce7d-520">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="bce7d-521">Si l’utilisateur est déjà connecté, cela génère un événement de réponse au jeton, sans demander de confirmation à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bce7d-521">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="bce7d-522">Dans le cas contraire, l’utilisateur est invité à se connecter.</span><span class="sxs-lookup"><span data-stu-id="bce7d-522">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="bce7d-523">Le service de robots Azure envoie l’événement de réponse de jeton une fois que l’utilisateur tente de se connecter.</span><span class="sxs-lookup"><span data-stu-id="bce7d-523">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="bce7d-524">Dans l’étape suivante de la boîte de dialogue, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="bce7d-524">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="bce7d-525">Si ce n’est pas le cas, l’utilisateur s’est connecté.</span><span class="sxs-lookup"><span data-stu-id="bce7d-525">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="bce7d-526">**Dialogs/logout_dialog. py**</span><span class="sxs-lookup"><span data-stu-id="bce7d-526">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="bce7d-527">En savoir plus sur l’ajout de l’authentification via le service de robots Azure</span><span class="sxs-lookup"><span data-stu-id="bce7d-527">Learn about adding adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
