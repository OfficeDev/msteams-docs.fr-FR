---
title: Ajouter l’authentification à votre robot teams
author: clearab
description: Comment ajouter l’authentification OAuth à un bot dans Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 63d06100f69a5dc3777bdfb20b3231a85dce1f04
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673698"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="8a968-103">Ajouter l’authentification à votre robot teams</span><span class="sxs-lookup"><span data-stu-id="8a968-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="8a968-104">Dans certains cas, vous devrez peut-être créer des robots dans Microsoft teams qui peuvent accéder aux ressources au nom de l’utilisateur, tel qu’un service de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8a968-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="8a968-105">Cet article explique comment utiliser l’authentification du kit de développement logiciel (SDK) de l’outil Azure bot Service v4, basée sur OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="8a968-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="8a968-106">Ainsi, il est plus facile de développer un bot qui peut utiliser des jetons d’authentification en fonction des informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8a968-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="8a968-107">Key dans tout ceci est l’utilisation de **fournisseurs d’identité**, comme nous le verrons plus tard.</span><span class="sxs-lookup"><span data-stu-id="8a968-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="8a968-108">OAuth 2,0 est une norme ouverte pour l’authentification et l’autorisation utilisées par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="8a968-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="8a968-109">Une compréhension de base de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans Teams.</span><span class="sxs-lookup"><span data-stu-id="8a968-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="8a968-110">Voir [OAuth 2 simplifiée](https://aka.ms/oauth2-simplified) pour une compréhension de base et [OAuth 2,0](https://oauth.net/2/) pour la spécification complète.</span><span class="sxs-lookup"><span data-stu-id="8a968-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="8a968-111">Pour plus d’informations sur la façon dont le service Azure bot gère l’authentification, consultez [la rubrique authentification des utilisateurs au sein d’une conversation](https://aka.ms/azure-bot-authentication).</span><span class="sxs-lookup"><span data-stu-id="8a968-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="8a968-112">Voici les titres des sections de cet article :</span><span class="sxs-lookup"><span data-stu-id="8a968-112">In this article you'll learn:</span></span>

- <span data-ttu-id="8a968-113">**Comment créer un bot compatible avec l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="8a968-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="8a968-114">Vous utiliserez [CS-Auth-Sample][teams-auth-bot] pour gérer les informations d’identification de connexion de l’utilisateur et la génération du jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8a968-114">You'll use [cs-auth-sample][teams-auth-bot] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="8a968-115">**Comment déployer le bot sur Azure et l’associer à un fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="8a968-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="8a968-116">Le fournisseur émet un jeton basé sur les informations d’identification de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8a968-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="8a968-117">Le bot peut utiliser le jeton pour accéder aux ressources, telles qu’un service de messagerie, qui requiert l’authentification.</span><span class="sxs-lookup"><span data-stu-id="8a968-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="8a968-118">Pour plus d’informations, consultez la rubrique [flux d’authentification de Microsoft teams pour les robots](auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="8a968-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="8a968-119">**Comment intégrer le robot dans Microsoft teams**.</span><span class="sxs-lookup"><span data-stu-id="8a968-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="8a968-120">Une fois le robot intégré, vous pouvez vous connecter et échanger des messages avec celui-ci dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="8a968-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a968-121">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="8a968-121">Prerequisites</span></span>

- <span data-ttu-id="8a968-122">Connaissance des [notions de base des robots][concept-basics], de la gestion de l' [État][concept-state], de la bibliothèque de [boîtes de dialogue][concept-dialogs]et de la mise en œuvre d’un [flux de conversation séquentiel][simple-dialog].</span><span class="sxs-lookup"><span data-stu-id="8a968-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="8a968-123">Connaissance des développements Azure et OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="8a968-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="8a968-124">Visual Studio 2017 ou version ultérieure et git.</span><span class="sxs-lookup"><span data-stu-id="8a968-124">Visual Studio 2017 or later and Git.</span></span>
- <span data-ttu-id="8a968-125">Compte Azure.</span><span class="sxs-lookup"><span data-stu-id="8a968-125">Azure account.</span></span> <span data-ttu-id="8a968-126">Si nécessaire, vous pouvez créer un [compte Azure gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="8a968-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="8a968-127">L’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="8a968-127">The following sample.</span></span>

    | <span data-ttu-id="8a968-128">Exemple</span><span class="sxs-lookup"><span data-stu-id="8a968-128">Sample</span></span> | <span data-ttu-id="8a968-129">Version d’BotBuilder</span><span class="sxs-lookup"><span data-stu-id="8a968-129">BotBuilder version</span></span> | <span data-ttu-id="8a968-130">Montre</span><span class="sxs-lookup"><span data-stu-id="8a968-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="8a968-131">**Authentification bot** dans [CS-Auth-Sample][teams-auth-bot]</span><span class="sxs-lookup"><span data-stu-id="8a968-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot]</span></span> | <span data-ttu-id="8a968-132">v4</span><span class="sxs-lookup"><span data-stu-id="8a968-132">v4</span></span> | <span data-ttu-id="8a968-133">Prise en charge OAuthCard</span><span class="sxs-lookup"><span data-stu-id="8a968-133">OAuthCard support</span></span> |
    | <span data-ttu-id="8a968-134">**Authentification de robot** dans [python-auth-Sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="8a968-134">**Bot authentication** in [python-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="8a968-135">v4</span><span class="sxs-lookup"><span data-stu-id="8a968-135">v4</span></span> | <span data-ttu-id="8a968-136">Prise en charge OAuthCard</span><span class="sxs-lookup"><span data-stu-id="8a968-136">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="8a968-137">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8a968-137">Create the resource group</span></span>

<span data-ttu-id="8a968-138">Le groupe de ressources et le plan de service ne sont pas strictement nécessaires, mais ils vous permettent de libérer facilement les ressources que vous créez.</span><span class="sxs-lookup"><span data-stu-id="8a968-138">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="8a968-139">Cette pratique est intéressante pour maintenir l’organisation et la gestion de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="8a968-139">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="8a968-140">Vous utilisez un groupe de ressources pour créer des ressources individuelles pour l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-140">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="8a968-141">Pour des performances optimales, vérifiez que ces ressources se trouvent dans la même région Azure.</span><span class="sxs-lookup"><span data-stu-id="8a968-141">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="8a968-142">Dans votre navigateur, connectez-vous au [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="8a968-142">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="8a968-143">Dans le volet de navigation de gauche, sélectionnez **groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="8a968-143">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="8a968-144">Dans le coin supérieur gauche de la fenêtre affichée, sélectionnez **Ajouter** un onglet pour créer un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8a968-144">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="8a968-145">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a968-145">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="8a968-146">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8a968-146">**Subscription**.</span></span> <span data-ttu-id="8a968-147">Utilisez votre abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="8a968-147">Use your existing subscription.</span></span>
    1. <span data-ttu-id="8a968-148">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="8a968-148">**Resource group**.</span></span> <span data-ttu-id="8a968-149">Entrez le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8a968-149">Enter the name for the resource group.</span></span> <span data-ttu-id="8a968-150">Un exemple peut être *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8a968-150">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="8a968-151">N’oubliez pas que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="8a968-151">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="8a968-152">Dans le menu déroulant **région** , sélectionnez *anglais (États-Unis*) ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="8a968-152">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="8a968-153">Sélectionnez le bouton **vérifier et créer** .</span><span class="sxs-lookup"><span data-stu-id="8a968-153">Select the **Review and create** button.</span></span> <span data-ttu-id="8a968-154">Vous devriez voir une bannière indiquant que la *validation a réussi*.</span><span class="sxs-lookup"><span data-stu-id="8a968-154">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="8a968-155">Sélectionnez le bouton **créer** .</span><span class="sxs-lookup"><span data-stu-id="8a968-155">Select the **Create** button.</span></span> <span data-ttu-id="8a968-156">La création du groupe de ressources peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8a968-156">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="8a968-157">Comme pour les ressources que vous allez créer plus loin dans ce didacticiel, nous vous recommandons de épingler ce groupe de ressources à votre tableau de bord pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="8a968-157">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="8a968-158">Si vous souhaitez le faire, sélectionnez l’icône de code confidentiel & # 128204 ; dans le coin supérieur droit du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="8a968-158">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="8a968-159">Créer le plan de service</span><span class="sxs-lookup"><span data-stu-id="8a968-159">Create the service plan</span></span>

1. <span data-ttu-id="8a968-160">Dans le [**portail Azure**][azure-portal], dans le volet de navigation de gauche, sélectionnez **créer une ressource**.</span><span class="sxs-lookup"><span data-stu-id="8a968-160">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="8a968-161">Dans la zone de recherche, tapez *plan de service d’application*.</span><span class="sxs-lookup"><span data-stu-id="8a968-161">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="8a968-162">Sélectionnez la carte **app service plan** dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="8a968-162">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="8a968-163">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8a968-163">Select **Create**.</span></span>
1. <span data-ttu-id="8a968-164">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a968-164">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="8a968-165">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8a968-165">**Subscription**.</span></span> <span data-ttu-id="8a968-166">Vous pouvez utiliser un abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="8a968-166">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="8a968-167">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="8a968-167">**Resource Group**.</span></span> <span data-ttu-id="8a968-168">Sélectionnez le groupe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8a968-168">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="8a968-169">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="8a968-169">**Name**.</span></span> <span data-ttu-id="8a968-170">Entrez le nom du plan de service.</span><span class="sxs-lookup"><span data-stu-id="8a968-170">Enter the name for the service plan.</span></span> <span data-ttu-id="8a968-171">Un exemple peut être *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="8a968-171">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="8a968-172">N’oubliez pas que le nom doit être unique au sein du groupe.</span><span class="sxs-lookup"><span data-stu-id="8a968-172">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="8a968-173">**Système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="8a968-173">**Operating System**.</span></span> <span data-ttu-id="8a968-174">Sélectionnez *Windows* ou votre système d’exploitation applicable.</span><span class="sxs-lookup"><span data-stu-id="8a968-174">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="8a968-175">**Région**.</span><span class="sxs-lookup"><span data-stu-id="8a968-175">**Region**.</span></span> <span data-ttu-id="8a968-176">Sélectionnez *West US* ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="8a968-176">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="8a968-177">**Niveau de tarification**.</span><span class="sxs-lookup"><span data-stu-id="8a968-177">**Pricing Tier**.</span></span> <span data-ttu-id="8a968-178">Assurez-vous que l’option *standard S1* est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="8a968-178">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="8a968-179">Il doit s’agir de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="8a968-179">This should be the default value.</span></span>
    1. <span data-ttu-id="8a968-180">Sélectionnez le bouton **vérifier et créer** .</span><span class="sxs-lookup"><span data-stu-id="8a968-180">Select the **Review and create** button.</span></span> <span data-ttu-id="8a968-181">Vous devriez voir une bannière indiquant que la *validation a réussi*.</span><span class="sxs-lookup"><span data-stu-id="8a968-181">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="8a968-182">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8a968-182">Select **Create**.</span></span> <span data-ttu-id="8a968-183">La création du plan de service d’application peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8a968-183">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="8a968-184">Le plan est affiché dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8a968-184">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="8a968-185">Création de l’enregistrement des canaux de robots</span><span class="sxs-lookup"><span data-stu-id="8a968-185">Create the bot channels registration</span></span>

<span data-ttu-id="8a968-186">L’inscription des canaux de robots enregistre votre service Web en tant que bot avec l’infrastructure de robot, à condition que vous disposiez d’un ID d’application Microsoft et d’un mot de passe d’application (clé secrète client).</span><span class="sxs-lookup"><span data-stu-id="8a968-186">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a968-187">Il vous suffit d’enregistrer votre robot s’il n’est pas hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8a968-187">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="8a968-188">Si vous avez [créé un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) via le portail Azure, il est déjà enregistré auprès du service.</span><span class="sxs-lookup"><span data-stu-id="8a968-188">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="8a968-189">Si vous avez créé votre bot via l' [infrastructure bot](https://dev.botframework.com/bots/new) ou [AppStudio](~/concepts/build-and-test/app-studio-overview.md) , votre bot n’est pas enregistré dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8a968-189">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="8a968-190">Une fois que Azure a créé la ressource d’inscription, elle est incluse dans la liste des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="8a968-190">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![Groupe d’enregistrement des canaux de l’application bot](../../../assets/images/authentication/auth-bot-channels-registration-group.PNG)

> [!NOTE]
> <span data-ttu-id="8a968-192">La ressource d’inscription des canaux de robots affiche la région **globale** , même si vous avez sélectionné West US.</span><span class="sxs-lookup"><span data-stu-id="8a968-192">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="8a968-193">Cela est attendu.</span><span class="sxs-lookup"><span data-stu-id="8a968-193">This is expected.</span></span>

<span data-ttu-id="8a968-194">Pour plus d’informations, consultez [la rubrique Create a bot for teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="8a968-194">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="8a968-195">Créer le fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="8a968-195">Create the identity provider</span></span>

<span data-ttu-id="8a968-196">Vous avez besoin d’un fournisseur d’identité qui peut être utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="8a968-196">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="8a968-197">Dans cette procédure, vous allez utiliser un fournisseur Azure AD ; d’autres fournisseurs d’identité pris en charge par Azure AD peuvent également être utilisés.</span><span class="sxs-lookup"><span data-stu-id="8a968-197">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="8a968-198">Dans le [**portail Azure**][azure-portal], dans le volet de navigation de gauche, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a968-198">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="8a968-199">Vous devrez créer et enregistrer cette ressource Azure AD dans un client dans lequel vous pouvez consentir à déléguer les autorisations demandées par une application.</span><span class="sxs-lookup"><span data-stu-id="8a968-199">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="8a968-200">Pour obtenir des instructions sur la création d’un client, consultez [la rubrique accéder au portail et créer un client](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span><span class="sxs-lookup"><span data-stu-id="8a968-200">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="8a968-201">Dans le volet gauche, sélectionnez **inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="8a968-201">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="8a968-202">Dans le volet droit, sélectionnez l’onglet **nouvel enregistrement** , dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="8a968-202">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="8a968-203">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a968-203">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="8a968-204">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="8a968-204">**Name**.</span></span> <span data-ttu-id="8a968-205">Entrez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="8a968-205">Enter the name for the application.</span></span> <span data-ttu-id="8a968-206">Un exemple peut être *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="8a968-206">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="8a968-207">N’oubliez pas que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="8a968-207">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="8a968-208">Sélectionnez les **types de comptes pris en charge** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="8a968-208">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="8a968-209">Sélectionnez des *comptes dans n’importe quel annuaire d’organisation (n’importe quel compte Azure ad Directory-multiclient) et des comptes Microsoft personnels (par exemple, Skype, Xbox)*.</span><span class="sxs-lookup"><span data-stu-id="8a968-209">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="8a968-210">Pour l' **URI de redirection**:</span><span class="sxs-lookup"><span data-stu-id="8a968-210">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="8a968-211">&#x2713;sélectionnez **Web**.</span><span class="sxs-lookup"><span data-stu-id="8a968-211">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="8a968-212">&#x2713; définissez l’URL sur `https://token.botframework.com/.auth/web/redirect`.</span><span class="sxs-lookup"><span data-stu-id="8a968-212">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="8a968-213">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8a968-213">Select **Register**.</span></span>

1. <span data-ttu-id="8a968-214">Une fois créé, Azure affiche la page de **vue d’ensemble** de l’application.</span><span class="sxs-lookup"><span data-stu-id="8a968-214">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="8a968-215">Copiez et enregistrez les informations suivantes dans un fichier :</span><span class="sxs-lookup"><span data-stu-id="8a968-215">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="8a968-216">Valeur de l’ID de l' **application (client)** .</span><span class="sxs-lookup"><span data-stu-id="8a968-216">The **Application (client) ID** value.</span></span> <span data-ttu-id="8a968-217">Vous utiliserez cette valeur ultérieurement comme *ID client* lorsque vous enregistrerez cette application d’identité Azure avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-217">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="8a968-218">Valeur de l' **ID d’annuaire (locataire)** .</span><span class="sxs-lookup"><span data-stu-id="8a968-218">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="8a968-219">Vous utiliserez également cette valeur ultérieurement comme *ID de client* pour enregistrer cette application d’identité Azure avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-219">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="8a968-220">Dans le volet gauche, sélectionnez **certificats & secrets** pour créer une clé secrète client pour votre application.</span><span class="sxs-lookup"><span data-stu-id="8a968-220">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="8a968-221">Sous **secrets client**, sélectionnez &#x2795; **nouvelle clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="8a968-221">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="8a968-222">Ajoutez une description pour identifier cette clé secrète auprès d’autres personnes que vous devrez peut-être créer pour cette application, telle que *l’application d’identité bot dans teams*.</span><span class="sxs-lookup"><span data-stu-id="8a968-222">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="8a968-223">Définit **expire** à votre sélection.</span><span class="sxs-lookup"><span data-stu-id="8a968-223">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="8a968-224">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8a968-224">Select **Add**.</span></span>
   1. <span data-ttu-id="8a968-225">Avant de quitter cette page, **Enregistrez la clé secrète**.</span><span class="sxs-lookup"><span data-stu-id="8a968-225">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="8a968-226">Vous utiliserez cette valeur ultérieurement comme _clé secrète client_ lorsque vous enregistrerez votre application Azure ad avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="8a968-226">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="8a968-227">Configurer la connexion du fournisseur d’identité et l’inscrire auprès du robot</span><span class="sxs-lookup"><span data-stu-id="8a968-227">Configure the identity provider connection and register it with the bot</span></span>

1. <span data-ttu-id="8a968-228">Dans le [**portail Azure**][azure-portal], sélectionnez votre groupe de ressources dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="8a968-228">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="8a968-229">Sélectionnez le lien d’inscription de votre robot.</span><span class="sxs-lookup"><span data-stu-id="8a968-229">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="8a968-230">Sur la page des ressources, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8a968-230">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="8a968-231">Sous **paramètres de connexion OAuth** , dans la partie inférieure de la page, sélectionnez **Ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="8a968-231">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="8a968-232">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a968-232">Complete the form as follows:</span></span>

    1. <span data-ttu-id="8a968-233">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="8a968-233">**Name**.</span></span> <span data-ttu-id="8a968-234">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="8a968-234">Enter a name for the connection.</span></span> <span data-ttu-id="8a968-235">Vous utiliserez ce nom dans votre robot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="8a968-235">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="8a968-236">Par exemple *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="8a968-236">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="8a968-237">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="8a968-237">**Service Provider**.</span></span> <span data-ttu-id="8a968-238">Sélectionner **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a968-238">Select **Azure Active Directory**.</span></span> <span data-ttu-id="8a968-239">Une fois que vous avez sélectionné cette option, les champs spécifiques à Azure AD sont affichés.</span><span class="sxs-lookup"><span data-stu-id="8a968-239">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="8a968-240">**ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8a968-240">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="8a968-241">**Clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="8a968-241">**Client secret**.</span></span> <span data-ttu-id="8a968-242">Entrez le secret que vous avez enregistré pour votre application Azure Identity Provider dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8a968-242">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="8a968-243">**Type d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="8a968-243">**Grant Type**.</span></span> <span data-ttu-id="8a968-244">Entrée `authorization_code`.</span><span class="sxs-lookup"><span data-stu-id="8a968-244">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="8a968-245">**URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="8a968-245">**Login URL**.</span></span> <span data-ttu-id="8a968-246">Entrée `https://login.microsoftonline.com`.</span><span class="sxs-lookup"><span data-stu-id="8a968-246">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="8a968-247">**ID de client**, entrez l' **ID de répertoire (locataire)** que vous avez enregistré précédemment pour votre application d’identité Azure ou **courant** en fonction du type de compte pris en charge sélectionné lors de la création de l’application du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="8a968-247">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="8a968-248">Pour déterminer la valeur à affecter, suivez ces critères :</span><span class="sxs-lookup"><span data-stu-id="8a968-248">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="8a968-249">Si vous avez sélectionné l’un des *comptes de cet annuaire d’organisation uniquement (Microsoft uniquement-client unique)* ou *des comptes dans n’importe quel annuaire d’organisation (Microsoft AAD Directory-multi-client),* entrez l' **ID de client** que vous avez enregistré précédemment pour l’application AAD.</span><span class="sxs-lookup"><span data-stu-id="8a968-249">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="8a968-250">Il s’agira du client associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="8a968-250">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="8a968-251">Si vous avez sélectionné *comptes dans n’importe quel annuaire d’organisation (tous les comptes Microsoft AAD Directory-clients multiples et personnels, par exemple Skype, Xbox, Outlook)* , entrez le mot **commun** au lieu d’un ID de client.</span><span class="sxs-lookup"><span data-stu-id="8a968-251">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="8a968-252">Dans le cas contraire, l’application AAD vérifie via le client dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="8a968-252">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="8a968-253">h.</span><span class="sxs-lookup"><span data-stu-id="8a968-253">h.</span></span> <span data-ttu-id="8a968-254">Pour **URL de ressource**, `https://graph.microsoft.com/`entrez.</span><span class="sxs-lookup"><span data-stu-id="8a968-254">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="8a968-255">Cela n’est pas utilisé dans l’exemple de code actuel.</span><span class="sxs-lookup"><span data-stu-id="8a968-255">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="8a968-256">Je.</span><span class="sxs-lookup"><span data-stu-id="8a968-256">i.</span></span> <span data-ttu-id="8a968-257">Laissez les **étendues** vides.</span><span class="sxs-lookup"><span data-stu-id="8a968-257">Leave **Scopes** blank.</span></span> <span data-ttu-id="8a968-258">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8a968-258">The following image is an example:</span></span>

    ![chaîne de connexion d’authentification de l’application bots de teams ADV1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="8a968-260">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8a968-260">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="8a968-261">Tester la connexion</span><span class="sxs-lookup"><span data-stu-id="8a968-261">Test the connection</span></span>

1. <span data-ttu-id="8a968-262">Sélectionnez l’entrée de connexion pour ouvrir la connexion que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="8a968-262">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="8a968-263">Sélectionnez **tester la connexion** en haut du panneau **paramètres de connexion du fournisseur de services** .</span><span class="sxs-lookup"><span data-stu-id="8a968-263">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="8a968-264">La première fois que vous effectuez cette opération, une nouvelle fenêtre de navigateur s’ouvre et vous invite à sélectionner un compte.</span><span class="sxs-lookup"><span data-stu-id="8a968-264">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="8a968-265">Sélectionnez celle que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="8a968-265">Select the one you want to use.</span></span>
1. <span data-ttu-id="8a968-266">Ensuite, vous serez invité à autoriser le fournisseur d’identité à utiliser vos données (informations d’identification).</span><span class="sxs-lookup"><span data-stu-id="8a968-266">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="8a968-267">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8a968-267">The following image is an example:</span></span>

    ![chaîne de connexion d’authentification de l’application bots de teams ADV1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="8a968-269">Sélectionnez **accepter**.</span><span class="sxs-lookup"><span data-stu-id="8a968-269">Select **Accept**.</span></span>
1. <span data-ttu-id="8a968-270">Cela doit ensuite vous rediriger vers une **connexion test à \<votre page-connection-Name> Succeeded** .</span><span class="sxs-lookup"><span data-stu-id="8a968-270">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="8a968-271">Actualisez la page si vous obtenez une erreur.</span><span class="sxs-lookup"><span data-stu-id="8a968-271">Refresh the page if you get an error.</span></span> <span data-ttu-id="8a968-272">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8a968-272">The following image is an example:</span></span>

  ![chaîne de connexion d’authentification de l’application bots de teams ADV1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="8a968-274">Le nom de connexion est utilisé par le code de robot pour récupérer des jetons d’authentification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8a968-274">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="8a968-275">Préparation de l’exemple de code bot</span><span class="sxs-lookup"><span data-stu-id="8a968-275">Prepare the bot sample code</span></span>

<span data-ttu-id="8a968-276">Une fois les paramètres préliminaires effectués, nous allons nous concentrer sur la création du bot à utiliser dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8a968-276">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="8a968-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8a968-277">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="8a968-278">Clone [CS-Auth-Sample][teams-auth-bot].</span><span class="sxs-lookup"><span data-stu-id="8a968-278">Clone [cs-auth-sample][teams-auth-bot].</span></span>
1. <span data-ttu-id="8a968-279">Lancez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a968-279">Launch Visual Studio.</span></span>
1. <span data-ttu-id="8a968-280">Dans la barre d’outils, sélectionnez **fichier-> ouvrir-> projet/solution** et ouvrir le projet bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-280">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="8a968-281">Dans la mise à jour C# **appSettings. JSON** , comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a968-281">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="8a968-282">Définissez `ConnectionName` le nom de la connexion du fournisseur d’identité que vous avez ajoutée à l’enregistrement du canal du robot.</span><span class="sxs-lookup"><span data-stu-id="8a968-282">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="8a968-283">Le nom que nous avons utilisé dans cet exemple est *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="8a968-283">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="8a968-284">Définissez `MicrosoftAppId` l’ID de l' **application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-284">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="8a968-285">Définissez `MicrosoftAppPassword` la **clé secrète client** que vous avez enregistrée au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-285">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="8a968-286">Définissez le `ConnectionName` sur le nom de la connexion du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="8a968-286">Set the `ConnectionName` to the name of the identity provider connection.</span></span> 

    <span data-ttu-id="8a968-287">En fonction des caractères de votre clé secrète, il se peut que vous deviez utiliser le mot de passe XML.</span><span class="sxs-lookup"><span data-stu-id="8a968-287">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="8a968-288">Par exemple, tous les esperluettes (&) doivent être codés en tant que `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="8a968-288">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="8a968-289">Dans l’Explorateur de solutions, accédez au `TeamsAppManifest` dossier, ouvrez `manifest.json` et définissez `id` `botId` l’ID d' **application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-289">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="pythontabpython"></a>[<span data-ttu-id="8a968-290">Python</span><span class="sxs-lookup"><span data-stu-id="8a968-290">Python</span></span>](#tab/python)

1. <span data-ttu-id="8a968-291">Clonez l’authentification de l’exemple de [moteur teams de teams][teams-auth-bot-py] à partir du référentiel github.</span><span class="sxs-lookup"><span data-stu-id="8a968-291">Clone the sample [Teams bot authentication][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="8a968-292">Mettre à jour **config.py**:</span><span class="sxs-lookup"><span data-stu-id="8a968-292">Update **config.py**:</span></span>

    - <span data-ttu-id="8a968-293">Définissez `ConnectionName` le nom du paramètre de connexion OAuth que vous avez ajouté à votre bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-293">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="8a968-294">Défini `MicrosoftAppId` et `MicrosoftAppPassword` à l’ID de l’application et à la clé secrète de l’application de votre bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-294">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="8a968-295">En fonction des caractères de votre clé secrète, il se peut que vous deviez utiliser le mot de passe XML.</span><span class="sxs-lookup"><span data-stu-id="8a968-295">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="8a968-296">Par exemple, tous les esperluettes (&) doivent être codés en tant que `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="8a968-296">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="8a968-297">Déployer le bot sur Azure</span><span class="sxs-lookup"><span data-stu-id="8a968-297">Deploy the bot to Azure</span></span>

<span data-ttu-id="8a968-298">Pour déployer le robot, suivez les étapes décrites dans la procédure de [déploiement de votre robot sur Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="8a968-298">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="8a968-299">Par ailleurs, dans Visual Studio, vous pouvez suivre les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a968-299">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="8a968-300">Dans l' *Explorateur de solutions* Visual Studio, sélectionnez le nom du projet (ou cliquez avec le bouton droit).</span><span class="sxs-lookup"><span data-stu-id="8a968-300">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="8a968-301">Dans le menu déroulant, sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="8a968-301">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="8a968-302">Dans la fenêtre affichée, sélectionnez le **nouveau** lien.</span><span class="sxs-lookup"><span data-stu-id="8a968-302">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="8a968-303">Dans la fenêtre de boîte de dialogue, sélectionnez **app service** sur la gauche et **créer un nouveau** à droite.</span><span class="sxs-lookup"><span data-stu-id="8a968-303">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="8a968-304">Sélectionnez le bouton **publier** .</span><span class="sxs-lookup"><span data-stu-id="8a968-304">Select the **Publish** button.</span></span>
1. <span data-ttu-id="8a968-305">Dans la fenêtre de boîte de dialogue suivante, entrez les informations requises.</span><span class="sxs-lookup"><span data-stu-id="8a968-305">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="8a968-306">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="8a968-306">The following is an example:</span></span>

   ![AUTH-App-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="8a968-308">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8a968-308">Select **Create**.</span></span>
1. <span data-ttu-id="8a968-309">Si le déploiement réussit, vous devriez le voir apparaître dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a968-309">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="8a968-310">De plus, une page s’affiche dans votre navigateur par défaut pour dire que *votre robot est prêt !*.</span><span class="sxs-lookup"><span data-stu-id="8a968-310">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="8a968-311">L’URL sera semblable à ceci : `https://botteamsauth.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="8a968-311">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="8a968-312">Enregistrez-le dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="8a968-312">Save it to a file.</span></span>
1. <span data-ttu-id="8a968-313">Dans votre navigateur, accédez au [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="8a968-313">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="8a968-314">Vérifiez votre groupe de ressources, le bot doit être affiché avec les autres ressources.</span><span class="sxs-lookup"><span data-stu-id="8a968-314">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="8a968-315">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8a968-315">The following image is an example:</span></span>

    ![teams-bot-auth-App-service-Group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="8a968-317">Dans le groupe ressource, sélectionnez le nom de l’enregistrement du canal bot (lien).</span><span class="sxs-lookup"><span data-stu-id="8a968-317">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="8a968-318">Dans le volet de gauche, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8a968-318">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="8a968-319">Dans la zone **point de terminaison de messagerie** , entrez l’URL obtenue `api/messages`ci-dessus suivie de.</span><span class="sxs-lookup"><span data-stu-id="8a968-319">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="8a968-320">Voici un exemple : `https://botteamsauth.azurewebsites.net/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="8a968-320">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="8a968-321">Sélectionnez le bouton **Enregistrer** dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="8a968-321">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="8a968-322">Tester le bot à l’aide de l’émulateur</span><span class="sxs-lookup"><span data-stu-id="8a968-322">Test the bot using the Emulator</span></span>

<span data-ttu-id="8a968-323">Si vous ne l’avez pas encore fait, installez l' [émulateur de Microsoft bot Framework](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="8a968-323">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="8a968-324">Voir aussi [Déboguer avec l’émulateur](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="8a968-324">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="8a968-325">Pour que l’exemple de robot de connexion fonctionne, vous devez configurer l’émulateur comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8a968-325">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="8a968-326">Configurer l’émulateur pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="8a968-326">Configure the Emulator for authentication</span></span>

<span data-ttu-id="8a968-327">Si un bot requiert une authentification, vous devez configurer l’émulateur comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8a968-327">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="8a968-328">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="8a968-328">Start the Emulator.</span></span>
1. <span data-ttu-id="8a968-329">Dans l’émulateur, sélectionnez l’icône représentant un engrenage &#9881; en bas à gauche ou l’onglet Paramètres de l' **émulateur** dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="8a968-329">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="8a968-330">Activez la case à cocher **utiliser les jetons d’authentification version 1,0**.</span><span class="sxs-lookup"><span data-stu-id="8a968-330">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="8a968-331">Entrez le chemin d’accès local à l’outil **ngrok** .</span><span class="sxs-lookup"><span data-stu-id="8a968-331">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="8a968-332">*Voir* le [wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))de l’émulateur de robot/ngrok tunneling Integration.</span><span class="sxs-lookup"><span data-stu-id="8a968-332">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="8a968-333">Pour plus d’informations sur l’outil, voir [ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="8a968-333">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="8a968-334">Activez la case à cocher **exécuter ngrok au démarrage de l’émulateur**.</span><span class="sxs-lookup"><span data-stu-id="8a968-334">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="8a968-335">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8a968-335">Select the **Save** button.</span></span>

<span data-ttu-id="8a968-336">Lorsque le bot affiche une carte de connexion et que l’utilisateur sélectionne le bouton de connexion, l’émulateur ouvre une page que l’utilisateur peut utiliser pour se connecter avec le fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8a968-336">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="8a968-337">Une fois que l’utilisateur effectue cette opération, le fournisseur génère un jeton utilisateur et l’envoie au bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-337">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="8a968-338">Après cela, le bot peut agir au nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8a968-338">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="8a968-339">Tester le bot localement</span><span class="sxs-lookup"><span data-stu-id="8a968-339">Test the bot locally</span></span>

<span data-ttu-id="8a968-340">Une fois que vous avez configuré le mécanisme d’authentification, vous pouvez effectuer les tests de votre propre robot.</span><span class="sxs-lookup"><span data-stu-id="8a968-340">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="8a968-341">Exécutez l’exemple de bot localement sur votre ordinateur, via Visual Studio par exemple.</span><span class="sxs-lookup"><span data-stu-id="8a968-341">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="8a968-342">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="8a968-342">Start the Emulator.</span></span>
1. <span data-ttu-id="8a968-343">Sélectionnez le bouton **ouvrir un bot** .</span><span class="sxs-lookup"><span data-stu-id="8a968-343">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="8a968-344">Dans l' **URL du robot**, entrez l’URL locale du robot.</span><span class="sxs-lookup"><span data-stu-id="8a968-344">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="8a968-345">En règle `http://localhost:3978/api/messages`générale,.</span><span class="sxs-lookup"><span data-stu-id="8a968-345">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="8a968-346">Dans l' **ID de l’application Microsoft** , entrez l’ID d' `appsettings.json`application du bot à partir de.</span><span class="sxs-lookup"><span data-stu-id="8a968-346">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="8a968-347">Dans le **mot de passe de l’application Microsoft** , entrez le mot `appsettings.json`de passe d’application du bot dans le.</span><span class="sxs-lookup"><span data-stu-id="8a968-347">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="8a968-348">Sélectionnez **se connecter**.</span><span class="sxs-lookup"><span data-stu-id="8a968-348">Select **Connect**.</span></span>
1. <span data-ttu-id="8a968-349">Une fois le robot opérationnel, entrez le texte pour afficher la carte de connexion.</span><span class="sxs-lookup"><span data-stu-id="8a968-349">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="8a968-350">Sélectionnez le bouton **se connecter** .</span><span class="sxs-lookup"><span data-stu-id="8a968-350">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="8a968-351">Une boîte de dialogue contextuelle s’affiche pour **confirmer l’ouverture**de l’URL.</span><span class="sxs-lookup"><span data-stu-id="8a968-351">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="8a968-352">Cela permet d’authentifier l’utilisateur du robot (vous).</span><span class="sxs-lookup"><span data-stu-id="8a968-352">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="8a968-353">Sélectionnez **confirmer**.</span><span class="sxs-lookup"><span data-stu-id="8a968-353">Select **Confirm**.</span></span>
1. <span data-ttu-id="8a968-354">Si vous y êtes invité, sélectionnez le compte de l’utilisateur concerné.</span><span class="sxs-lookup"><span data-stu-id="8a968-354">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="8a968-355">En fonction de la configuration que vous avez utilisée pour l’émulateur, vous obtenez l’un des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8a968-355">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="8a968-356">**Utilisation du code de vérification de connexion**</span><span class="sxs-lookup"><span data-stu-id="8a968-356">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="8a968-357">&#x2713; une fenêtre s’ouvre et affiche le code de validation.</span><span class="sxs-lookup"><span data-stu-id="8a968-357">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="8a968-358">&#x2713; copiez et entrez le code de validation dans la zone de conversation pour terminer la connexion.</span><span class="sxs-lookup"><span data-stu-id="8a968-358">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="8a968-359">**À l’aide de jetons d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="8a968-359">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="8a968-360">&#x2713; vous êtes connecté en fonction de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="8a968-360">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="8a968-361">L’image suivante est un exemple de l’interface utilisateur du bot une fois que vous avez ouvert une session :</span><span class="sxs-lookup"><span data-stu-id="8a968-361">The following image is an example of the bot UI after you've logged in:</span></span>

    ![émulateur de connexion du bot auth](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="8a968-363">Si vous sélectionnez **Oui** lorsque le bot vous demande si *vous souhaitez afficher votre jeton ?*, vous obtiendrez une réponse semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="8a968-363">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![jeton de l’émulateur de connexion auth bot](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="8a968-365">Entrez **déconnexion** dans la zone de conversation d’entrée pour vous déconnecter. Cela libère le jeton d’utilisateur et le bot ne pourra pas agir en votre nom tant que vous n’aurez pas reconnecté.</span><span class="sxs-lookup"><span data-stu-id="8a968-365">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="8a968-366">L’authentification du robot nécessite l’utilisation du **service de connecteur bot**.</span><span class="sxs-lookup"><span data-stu-id="8a968-366">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="8a968-367">Le service accède aux informations d’inscription des canaux des robots pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-367">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="8a968-368">Tester le robot déployé</span><span class="sxs-lookup"><span data-stu-id="8a968-368">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="8a968-369">Dans votre navigateur, accédez au [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="8a968-369">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="8a968-370">Recherchez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8a968-370">Find your resource group.</span></span>
1. <span data-ttu-id="8a968-371">Sélectionnez le lien ressource.</span><span class="sxs-lookup"><span data-stu-id="8a968-371">Select the resource link.</span></span> <span data-ttu-id="8a968-372">La page de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8a968-372">The resource page is displayed.</span></span>
1. <span data-ttu-id="8a968-373">Dans la page des ressources, sélectionnez **tester dans la conversation Web**.</span><span class="sxs-lookup"><span data-stu-id="8a968-373">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="8a968-374">Le bot démarre et affiche les messages d’accueil prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="8a968-374">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="8a968-375">Tapez n’importe quel élément dans la zone conversation.</span><span class="sxs-lookup"><span data-stu-id="8a968-375">Type anything in the chat box.</span></span>
1. <span data-ttu-id="8a968-376">Sélectionnez la zone **se connecter** .</span><span class="sxs-lookup"><span data-stu-id="8a968-376">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="8a968-377">Une boîte de dialogue contextuelle s’affiche pour **confirmer l’ouverture**de l’URL.</span><span class="sxs-lookup"><span data-stu-id="8a968-377">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="8a968-378">Cela permet d’authentifier l’utilisateur du robot (vous).</span><span class="sxs-lookup"><span data-stu-id="8a968-378">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="8a968-379">Sélectionnez **confirmer**.</span><span class="sxs-lookup"><span data-stu-id="8a968-379">Select **Confirm**.</span></span>
1. <span data-ttu-id="8a968-380">Si vous y êtes invité, sélectionnez le compte de l’utilisateur concerné.</span><span class="sxs-lookup"><span data-stu-id="8a968-380">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="8a968-381">L’image suivante est un exemple de l’interface utilisateur du bot une fois que vous avez ouvert une session :</span><span class="sxs-lookup"><span data-stu-id="8a968-381">The following image is an example of the bot UI after you have logged in:</span></span>

    ![connexion à un bot auth déployée](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="8a968-383">.</span><span class="sxs-lookup"><span data-stu-id="8a968-383">.</span></span>

1. <span data-ttu-id="8a968-384">Sélectionnez le bouton **Oui** pour afficher votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8a968-384">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="8a968-385">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8a968-385">The following image is an example:</span></span>

    ![jeton déployé de connexion à un bot d’authentification](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="8a968-387">.</span><span class="sxs-lookup"><span data-stu-id="8a968-387">.</span></span>

1. <span data-ttu-id="8a968-388">Entrez déconnexion pour vous déconnecter.</span><span class="sxs-lookup"><span data-stu-id="8a968-388">Enter logout to sign out.</span></span>

    ![la déconnexion du robot d’authentification a été déployée](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="8a968-390">Si vous rencontrez des problèmes lors de la connexion, essayez de tester à nouveau la connexion, comme décrit dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="8a968-390">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="8a968-391">Cela peut recréer le jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8a968-391">This could recreate the authentication token.</span></span>
> <span data-ttu-id="8a968-392">Avec le client de conversation Web de robot dans Azure, il se peut que vous deviez vous connecter à plusieurs reprises avant l’établissement correct de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="8a968-392">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="8a968-393">Installer et tester le bot dans teams</span><span class="sxs-lookup"><span data-stu-id="8a968-393">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="8a968-394">Dans votre projet de robot, vérifiez que `TeamsAppManifest` le dossier contient `manifest.json` avec un `outline.png` et `color.png` des fichiers.</span><span class="sxs-lookup"><span data-stu-id="8a968-394">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="8a968-395">Dans l' `TeamsAppManifest` Explorateur de solutions, accédez au dossier.</span><span class="sxs-lookup"><span data-stu-id="8a968-395">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="8a968-396">Modifiez `manifest.json` en assignant les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a968-396">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="8a968-397">Assurez-vous que l' **ID d’application bot** que vous avez reçu au moment de l’enregistrement `id` du `botId`canal bot est affecté à et.</span><span class="sxs-lookup"><span data-stu-id="8a968-397">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="8a968-398">Affectez cette valeur `validDomains: [ "token.botframework.com" ]`:.</span><span class="sxs-lookup"><span data-stu-id="8a968-398">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="8a968-399">Sélectionnez et **compressez** les `manifest.json`fichiers, `outline.png`et `color.png` .</span><span class="sxs-lookup"><span data-stu-id="8a968-399">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="8a968-400">Ouvrez **Microsoft teams**.</span><span class="sxs-lookup"><span data-stu-id="8a968-400">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="8a968-401">Dans le volet gauche, dans la partie inférieure, sélectionnez l' **icône applications**.</span><span class="sxs-lookup"><span data-stu-id="8a968-401">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="8a968-402">Dans le volet droit, dans la partie inférieure, sélectionnez **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="8a968-402">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="8a968-403">Naviguez jusqu' `TeamsAppManifest` au dossier et téléchargez le manifeste zippé.</span><span class="sxs-lookup"><span data-stu-id="8a968-403">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="8a968-404">L’Assistant suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="8a968-404">The following wizard is displayed:</span></span>

    ![chargement des équipes du bot auth](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="8a968-406">Sélectionnez le bouton **Ajouter à une équipe** .</span><span class="sxs-lookup"><span data-stu-id="8a968-406">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="8a968-407">Dans la fenêtre suivante, sélectionnez l’équipe dans laquelle vous souhaitez utiliser le bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-407">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="8a968-408">Sélectionnez le bouton **configurer un robot** .</span><span class="sxs-lookup"><span data-stu-id="8a968-408">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="8a968-409">Sélectionnez les trois points (&#x25cf;&#x25cf;&#x25cf;) dans le volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="8a968-409">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="8a968-410">Ensuite, sélectionnez l’icône **app Studio** .</span><span class="sxs-lookup"><span data-stu-id="8a968-410">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="8a968-411">Sélectionnez l’onglet **éditeur de manifeste** . L’icône du bot que vous avez téléchargé doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="8a968-411">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="8a968-412">De plus, vous devriez voir le robot répertorié en tant que contact dans la liste des conversations que vous pouvez utiliser pour échanger des messages avec le bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-412">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="8a968-413">Test du bot localement dans teams</span><span class="sxs-lookup"><span data-stu-id="8a968-413">Testing the bot locally in Teams</span></span>

<span data-ttu-id="8a968-414">Microsoft teams est un produit entièrement basé sur le Cloud, il faut que tous les services auxquels il accède soient disponibles dans le nuage à l’aide de points de terminaison HTTPs.</span><span class="sxs-lookup"><span data-stu-id="8a968-414">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="8a968-415">Par conséquent, pour permettre au bot (notre exemple) de fonctionner dans Teams, vous devez soit publier le code dans le nuage de votre choix, soit rendre une instance en cours d’exécution accessible en externe via un outil de **tunneling** .</span><span class="sxs-lookup"><span data-stu-id="8a968-415">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="8a968-416">Nous vous recommandons d’utiliser [ngrok](https://ngrok.com/download), qui crée une URL adressable en externe pour un port que vous ouvrez localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8a968-416">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="8a968-417">Pour configurer ngrok en vue de l’exécution locale de votre application Microsoft Teams, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a968-417">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="8a968-418">Dans une fenêtre de terminal, accédez au répertoire dans lequel `ngrok.exe` vous avez installé.</span><span class="sxs-lookup"><span data-stu-id="8a968-418">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="8a968-419">Nous vous suggérons de définir le chemin d’accès de la *variable d’environnement* de sorte qu’il pointe vers lui.</span><span class="sxs-lookup"><span data-stu-id="8a968-419">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="8a968-420">Exécuter, par exemple, `ngrok http 3978 --host-header=localhost:3978`.</span><span class="sxs-lookup"><span data-stu-id="8a968-420">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="8a968-421">Remplacez le numéro de port selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="8a968-421">Replace the port number as needed.</span></span>
<span data-ttu-id="8a968-422">Cela lance ngrok pour écouter sur le port que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="8a968-422">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="8a968-423">En retour, elle vous fournit une URL adressable de manière externe, valide pendant le temps que ngrok est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8a968-423">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="8a968-424">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8a968-424">The following image is an example:</span></span>

    ![chaîne de connexion d’authentification de l’application bots de teams ADV1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="8a968-426">.</span><span class="sxs-lookup"><span data-stu-id="8a968-426">.</span></span>

1. <span data-ttu-id="8a968-427">Copiez l’adresse HTTPs de transfert.</span><span class="sxs-lookup"><span data-stu-id="8a968-427">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="8a968-428">Il doit ressembler à ce qui `https://dea822bf.ngrok.io/`suit :.</span><span class="sxs-lookup"><span data-stu-id="8a968-428">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="8a968-429">Ajouter `/api/messages` pour obtenir `https://dea822bf.ngrok.io/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="8a968-429">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="8a968-430">Il s’agit du **point de terminaison de messages** pour le robot s’exécutant localement sur votre ordinateur et accessible via le Web dans une conversation dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8a968-430">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="8a968-431">Une dernière étape consiste à mettre à jour le point de terminaison des messages du bot déployé.</span><span class="sxs-lookup"><span data-stu-id="8a968-431">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="8a968-432">Dans l’exemple, nous avons déployé le bot dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8a968-432">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="8a968-433">So \* \* nous allons effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a968-433">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="8a968-434">Dans votre navigateur, accédez au [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="8a968-434">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="8a968-435">Sélectionnez l' **enregistrement**de votre canal de robot.</span><span class="sxs-lookup"><span data-stu-id="8a968-435">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="8a968-436">Dans le volet de gauche, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8a968-436">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="8a968-437">Dans le volet droit, dans la zone **point de terminaison de messagerie** , entrez l’URL ngrok, dans `https://dea822bf.ngrok.io/api/messages`notre exemple,.</span><span class="sxs-lookup"><span data-stu-id="8a968-437">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="8a968-438">Démarrez votre robot localement, par exemple en mode de débogage Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a968-438">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="8a968-439">Testez le robot tout en s’exécutant localement à l’aide de la **conversation Web test**du portail de l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="8a968-439">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="8a968-440">À l’instar de l’émulateur, ce test ne vous permet pas d’accéder aux fonctionnalités spécifiques des équipes.</span><span class="sxs-lookup"><span data-stu-id="8a968-440">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="8a968-441">Dans la fenêtre de terminal `ngrok` où est exécuté, vous pouvez voir le trafic http entre le bot et le client de conversation Web.</span><span class="sxs-lookup"><span data-stu-id="8a968-441">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="8a968-442">Si vous souhaitez une vue plus détaillée, dans une fenêtre de navigateur `http://127.0.0.1:4040` , entrez que vous avez obtenu à partir de la fenêtre de terminal précédente.</span><span class="sxs-lookup"><span data-stu-id="8a968-442">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="8a968-443">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="8a968-443">The following image is an example:</span></span>

    ![tests ngrok des équipes de robots d’authentification](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="8a968-445">.</span><span class="sxs-lookup"><span data-stu-id="8a968-445">.</span></span>

> [!NOTE]
> <span data-ttu-id="8a968-446">Si vous arrêtez et redémarrez ngrok, l’URL change.</span><span class="sxs-lookup"><span data-stu-id="8a968-446">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="8a968-447">Pour utiliser ngrok dans votre projet et selon les fonctionnalités que vous utilisez, vous devez mettre à jour toutes les références d’URL.</span><span class="sxs-lookup"><span data-stu-id="8a968-447">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>

## <a name="additional-information"></a><span data-ttu-id="8a968-448">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8a968-448">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="8a968-449">TeamsAppManifest/manifest. JSON</span><span class="sxs-lookup"><span data-stu-id="8a968-449">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="8a968-450">Ce manifeste contient les informations nécessaires à Microsoft teams pour se connecter au robot.</span><span class="sxs-lookup"><span data-stu-id="8a968-450">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

<span data-ttu-id="8a968-451">Avec l’authentification, teams se comporte légèrement différemment des autres canaux, comme expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8a968-451">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="8a968-452">Gestion de l’activité d’appel</span><span class="sxs-lookup"><span data-stu-id="8a968-452">Handling Invoke Activity</span></span>

<span data-ttu-id="8a968-453">Une **activité d’appel** est envoyée au bot au lieu de l’activité d’événement utilisée par d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="8a968-453">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="8a968-454">Cette opération est réalisée par la sous-classe du **ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="8a968-454">This is done by sub-classing the **ActivityHandler**.</span></span>

<span data-ttu-id="8a968-455">**Robots/DialogBot. cs**</span><span class="sxs-lookup"><span data-stu-id="8a968-455">**Bots/DialogBot.cs**</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="8a968-456">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8a968-456">C#/.NET</span></span>](#tab/dotnet)

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="8a968-457">**Robots/TeamsBot. cs**</span><span class="sxs-lookup"><span data-stu-id="8a968-457">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="8a968-458">L' *activité d’appel* doit être transférée à la boîte de dialogue si **OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8a968-458">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="8a968-459">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="8a968-459">TeamsActivityHandler.cs</span></span>

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

# <a name="pythontabpython"></a>[<span data-ttu-id="8a968-460">Python</span><span class="sxs-lookup"><span data-stu-id="8a968-460">Python</span></span>](#tab/python)

<span data-ttu-id="8a968-461">**bots/dialog_bot. py**</span><span class="sxs-lookup"><span data-stu-id="8a968-461">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="8a968-462">**bots/teams_bot. py**</span><span class="sxs-lookup"><span data-stu-id="8a968-462">**bots/teams_bot.py**</span></span>

<span data-ttu-id="8a968-463">L' *activité d’appel* doit être transférée à la boîte de dialogue si **OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8a968-463">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)] 

<span data-ttu-id="8a968-464">**Dialogs/main_dialog. py**</span><span class="sxs-lookup"><span data-stu-id="8a968-464">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="8a968-465">Dans une étape de dialogue, `begin_dialog` utilisez pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="8a968-465">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="8a968-466">Si l’utilisateur est déjà connecté, cela génère un événement de réponse au jeton, sans demander de confirmation à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8a968-466">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="8a968-467">Dans le cas contraire, l’utilisateur est invité à se connecter.</span><span class="sxs-lookup"><span data-stu-id="8a968-467">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="8a968-468">Le service de robots Azure envoie l’événement de réponse de jeton une fois que l’utilisateur tente de se connecter.</span><span class="sxs-lookup"><span data-stu-id="8a968-468">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="8a968-469">Dans l’étape suivante de la boîte de dialogue, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="8a968-469">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="8a968-470">Si ce n’est pas le cas, l’utilisateur s’est connecté.</span><span class="sxs-lookup"><span data-stu-id="8a968-470">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=54-65)]

<span data-ttu-id="8a968-471">**Dialogs/logout_dialog. py**</span><span class="sxs-lookup"><span data-stu-id="8a968-471">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="further-reading"></a><span data-ttu-id="8a968-472">Autres lectures</span><span class="sxs-lookup"><span data-stu-id="8a968-472">Further reading</span></span>

- [<span data-ttu-id="8a968-473">Ajouter l’authentification à votre robot via le service de robots Azure</span><span class="sxs-lookup"><span data-stu-id="8a968-473">Add authentication to your bot via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
