---
title: Ajouter l’authentification à Teams bot
author: clearab
description: Comment ajouter l’authentification OAuth à un bot dans Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 36cb6f3de6f97af1d01512175923b79f69f630ad
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565969"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="d5003-103">Ajouter l’authentification à Teams bot</span><span class="sxs-lookup"><span data-stu-id="d5003-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="d5003-104">Il arrive parfois que vous devrez créer des bots dans Microsoft Teams qui peuvent accéder aux ressources pour le compte de l’utilisateur, telles qu’un service de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d5003-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="d5003-105">Cet article montre comment utiliser l’authentification SDK Azure Bot Service v4, basée sur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5003-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="d5003-106">Cela facilite le développement d’un bot qui peut utiliser des jetons d’authentification basés sur les informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="d5003-107">L’élément clé de tout cela est l’utilisation de fournisseurs **d’identité,** comme nous le constaterons plus tard.</span><span class="sxs-lookup"><span data-stu-id="d5003-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="d5003-108">OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="d5003-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="d5003-109">Une compréhension de base d’OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d5003-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="d5003-110">Voir [OAuth 2 Simplifié pour](https://aka.ms/oauth2-simplified) une compréhension de base et [OAuth 2.0](https://oauth.net/2/) pour la spécification complète.</span><span class="sxs-lookup"><span data-stu-id="d5003-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="d5003-111">Pour plus d’informations sur la façon dont Azure Bot Service gère l’authentification, consultez [l’authentification utilisateur dans une conversation.](https://aka.ms/azure-bot-authentication)</span><span class="sxs-lookup"><span data-stu-id="d5003-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="d5003-112">Voici les titres des sections de cet article :</span><span class="sxs-lookup"><span data-stu-id="d5003-112">In this article you'll learn:</span></span>

- <span data-ttu-id="d5003-113">**Comment créer un bot activé pour l’authentification.**</span><span class="sxs-lookup"><span data-stu-id="d5003-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="d5003-114">Vous utiliserez [cs-auth-sample][teams-auth-bot-cs] pour gérer les informations d’identification de connexion de l’utilisateur et la génération du jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d5003-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="d5003-115">**Comment déployer le bot sur Azure et l’associer à un fournisseur d’identité.**</span><span class="sxs-lookup"><span data-stu-id="d5003-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="d5003-116">Le fournisseur émettra un jeton basé sur les informations d’identification de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="d5003-117">Le bot peut utiliser le jeton pour accéder à des ressources, telles qu’un service de messagerie, qui nécessitent une authentification.</span><span class="sxs-lookup"><span data-stu-id="d5003-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="d5003-118">Pour plus d’informations, [Microsoft Teams flux d’authentification pour les bots.](auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="d5003-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="d5003-119">**Comment intégrer le bot dans Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="d5003-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="d5003-120">Une fois le bot intégré, vous pouvez vous y inscrire et échanger des messages avec lui dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="d5003-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5003-121">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="d5003-121">Prerequisites</span></span>

- <span data-ttu-id="d5003-122">Connaissance des principes [de base du bot,][concept-basics] [de la gestion de l’état,][concept-state]de la bibliothèque [de][concept-dialogs]boîtes de dialogue et de la façon d’implémenter un flux de [conversation séquentiel.][simple-dialog]</span><span class="sxs-lookup"><span data-stu-id="d5003-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="d5003-123">Connaissance du développement Azure et OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5003-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="d5003-124">Les versions actuelles de Visual Studio git.</span><span class="sxs-lookup"><span data-stu-id="d5003-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="d5003-125">Compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d5003-125">Azure account.</span></span> <span data-ttu-id="d5003-126">Si nécessaire, vous pouvez créer un [compte gratuit Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="d5003-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="d5003-127">L’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d5003-127">The following sample:</span></span>

    | <span data-ttu-id="d5003-128">Échantillon</span><span class="sxs-lookup"><span data-stu-id="d5003-128">Sample</span></span> | <span data-ttu-id="d5003-129">Version de BotBuilder</span><span class="sxs-lookup"><span data-stu-id="d5003-129">BotBuilder version</span></span> | <span data-ttu-id="d5003-130">Demonstrates</span><span class="sxs-lookup"><span data-stu-id="d5003-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="d5003-131">**Authentification de bot** [dans cs-auth-sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="d5003-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="d5003-132">v4</span><span class="sxs-lookup"><span data-stu-id="d5003-132">v4</span></span> | <span data-ttu-id="d5003-133">Prise en charge d’OAuthCard</span><span class="sxs-lookup"><span data-stu-id="d5003-133">OAuthCard support</span></span> |
    | <span data-ttu-id="d5003-134">**Authentification de bot** [dans js-auth-sample][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="d5003-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="d5003-135">v4</span><span class="sxs-lookup"><span data-stu-id="d5003-135">v4</span></span>| <span data-ttu-id="d5003-136">Prise en charge d’OAuthCard</span><span class="sxs-lookup"><span data-stu-id="d5003-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="d5003-137">**Authentification de bot** [dans py-auth-sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="d5003-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="d5003-138">v4</span><span class="sxs-lookup"><span data-stu-id="d5003-138">v4</span></span> | <span data-ttu-id="d5003-139">Prise en charge d’OAuthCard</span><span class="sxs-lookup"><span data-stu-id="d5003-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="d5003-140">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="d5003-140">Create the resource group</span></span>

<span data-ttu-id="d5003-141">Le groupe de ressources et le plan de service ne sont pas strictement nécessaires, mais ils vous permettent de libérer facilement les ressources que vous créez.</span><span class="sxs-lookup"><span data-stu-id="d5003-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="d5003-142">Il s’agit d’une bonne pratique pour maintenir l’organisation et la gestion de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="d5003-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="d5003-143">Vous utilisez un groupe de ressources pour créer des ressources individuelles pour Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d5003-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="d5003-144">Pour obtenir des performances, assurez-vous que ces ressources se trouvent dans la même région Azure.</span><span class="sxs-lookup"><span data-stu-id="d5003-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="d5003-145">Dans votre navigateur, connectez-vous au [**portail Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="d5003-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="d5003-146">Dans le panneau de navigation de gauche, sélectionnez **Groupes de ressources.**</span><span class="sxs-lookup"><span data-stu-id="d5003-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="d5003-147">Dans le coin supérieur gauche de la fenêtre affichée, **sélectionnez** Ajouter un onglet pour créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d5003-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="d5003-148">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5003-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="d5003-149">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="d5003-149">**Subscription**.</span></span> <span data-ttu-id="d5003-150">Utilisez votre abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="d5003-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="d5003-151">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="d5003-151">**Resource group**.</span></span> <span data-ttu-id="d5003-152">Entrez le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d5003-152">Enter the name for the resource group.</span></span> <span data-ttu-id="d5003-153">Par exemple,  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="d5003-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="d5003-154">N’oubliez pas que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="d5003-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="d5003-155">Dans le menu **déroulant Région,** sélectionnez *Ouest des* États-Unis ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="d5003-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="d5003-156">Sélectionnez le **bouton Révision et** créer.</span><span class="sxs-lookup"><span data-stu-id="d5003-156">Select the **Review and create** button.</span></span> <span data-ttu-id="d5003-157">Vous devriez voir une bannière qui lit *Validation transmise*.</span><span class="sxs-lookup"><span data-stu-id="d5003-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="d5003-158">Sélectionnez **le bouton** Créer.</span><span class="sxs-lookup"><span data-stu-id="d5003-158">Select the **Create** button.</span></span> <span data-ttu-id="d5003-159">La création du groupe de ressources peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d5003-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="d5003-160">Comme pour les ressources que vous créerez plus loin dans ce didacticiel, il est bon d’épingler ce groupe de ressources à votre tableau de bord pour en faciliter l’accès.</span><span class="sxs-lookup"><span data-stu-id="d5003-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="d5003-161">Si vous le souhaitez, sélectionnez l’icône d'&#128204 ; dans le coin supérieur droit du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d5003-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="d5003-162">Créer le plan de service</span><span class="sxs-lookup"><span data-stu-id="d5003-162">Create the service plan</span></span>

1. <span data-ttu-id="d5003-163">Dans le [**portail Azure,**][azure-portal]dans le panneau de navigation de gauche, **sélectionnez Créer une ressource.**</span><span class="sxs-lookup"><span data-stu-id="d5003-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="d5003-164">Dans la zone de recherche, tapez *App Service Plan*.</span><span class="sxs-lookup"><span data-stu-id="d5003-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="d5003-165">Sélectionnez la carte **Plan du service d’application** dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="d5003-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="d5003-166">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d5003-166">Select **Create**.</span></span>
1. <span data-ttu-id="d5003-167">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5003-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="d5003-168">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="d5003-168">**Subscription**.</span></span> <span data-ttu-id="d5003-169">Vous pouvez utiliser un abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="d5003-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="d5003-170">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="d5003-170">**Resource Group**.</span></span> <span data-ttu-id="d5003-171">Sélectionnez le groupe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d5003-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="d5003-172">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="d5003-172">**Name**.</span></span> <span data-ttu-id="d5003-173">Entrez le nom du plan de service.</span><span class="sxs-lookup"><span data-stu-id="d5003-173">Enter the name for the service plan.</span></span> <span data-ttu-id="d5003-174">Par exemple,  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="d5003-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="d5003-175">N’oubliez pas que le nom doit être unique au sein du groupe.</span><span class="sxs-lookup"><span data-stu-id="d5003-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="d5003-176">**Système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="d5003-176">**Operating System**.</span></span> <span data-ttu-id="d5003-177">Sélectionnez *Windows* ou votre système d’exploitation applicable.</span><span class="sxs-lookup"><span data-stu-id="d5003-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="d5003-178">**Région**.</span><span class="sxs-lookup"><span data-stu-id="d5003-178">**Region**.</span></span> <span data-ttu-id="d5003-179">Sélectionnez *Ouest des États-Unis* ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="d5003-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="d5003-180">**Niveau de tarification**.</span><span class="sxs-lookup"><span data-stu-id="d5003-180">**Pricing Tier**.</span></span> <span data-ttu-id="d5003-181">Assurez-vous *que Standard S1* est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d5003-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="d5003-182">Cette valeur doit être la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="d5003-182">This should be the default value.</span></span>
    1. <span data-ttu-id="d5003-183">Sélectionnez le **bouton Révision et** créer.</span><span class="sxs-lookup"><span data-stu-id="d5003-183">Select the **Review and create** button.</span></span> <span data-ttu-id="d5003-184">Vous devriez voir une bannière qui lit *Validation transmise*.</span><span class="sxs-lookup"><span data-stu-id="d5003-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="d5003-185">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d5003-185">Select **Create**.</span></span> <span data-ttu-id="d5003-186">La création du plan de service d’application peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d5003-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="d5003-187">Le plan sera répertorié dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d5003-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="d5003-188">Créer l’inscription des canaux de bot</span><span class="sxs-lookup"><span data-stu-id="d5003-188">Create the bot channels registration</span></span>

<span data-ttu-id="d5003-189">L’inscription des canaux du bot inscrit votre service web en tant que bot auprès de Bot Framework, à condition que vous avez un ID d’application Microsoft et un mot de passe d’application (secret client).</span><span class="sxs-lookup"><span data-stu-id="d5003-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5003-190">Vous ne devez inscrire votre bot que s’il n’est pas hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d5003-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="d5003-191">Si vous [avez créé un bot via](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) le portail Azure, il est déjà inscrit auprès du service.</span><span class="sxs-lookup"><span data-stu-id="d5003-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="d5003-192">Si vous avez créé votre bot via [Bot Framework](https://dev.botframework.com/bots/new) ou [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) votre bot n’est pas inscrit dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d5003-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="d5003-193">La ressource d’inscription des canaux bots affiche la **région** globale même si vous avez sélectionné Ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="d5003-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="d5003-194">Ceci est normal.</span><span class="sxs-lookup"><span data-stu-id="d5003-194">This is expected.</span></span>

<span data-ttu-id="d5003-195">Pour plus d’informations, [voir Créer un bot pour Teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="d5003-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="d5003-196">Créer le fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="d5003-196">Create the identity provider</span></span>

<span data-ttu-id="d5003-197">Vous avez besoin d’un fournisseur d’identité qui peut être utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="d5003-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="d5003-198">Dans cette procédure, vous allez utiliser un fournisseur Azure AD ; d’autres fournisseurs d’identité pris en charge par Azure AD peuvent également être utilisés.</span><span class="sxs-lookup"><span data-stu-id="d5003-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="d5003-199">Dans le [**portail Azure,**][azure-portal]dans le panneau de navigation de gauche, **sélectionnez Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5003-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="d5003-200">Vous devez créer et inscrire cette ressource Azure AD dans un client dans lequel vous pouvez consentir à déléguer les autorisations demandées par une application.</span><span class="sxs-lookup"><span data-stu-id="d5003-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="d5003-201">Pour obtenir des instructions sur la création d’un client, voir [Accéder au portail et créer un client.](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)</span><span class="sxs-lookup"><span data-stu-id="d5003-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="d5003-202">Dans le panneau gauche, sélectionnez **Inscriptions d’applications.**</span><span class="sxs-lookup"><span data-stu-id="d5003-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="d5003-203">Dans le panneau droit, sélectionnez **l’onglet** Nouvelle inscription, dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="d5003-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="d5003-204">Vous serez invité à fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5003-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="d5003-205">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="d5003-205">**Name**.</span></span> <span data-ttu-id="d5003-206">Entrez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="d5003-206">Enter the name for the application.</span></span> <span data-ttu-id="d5003-207">Par exemple,  *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="d5003-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="d5003-208">N’oubliez pas que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="d5003-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="d5003-209">Sélectionnez les **types de comptes pris en** charge pour votre application.</span><span class="sxs-lookup"><span data-stu-id="d5003-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="d5003-210">Sélectionnez les comptes dans n’importe quel annuaire d’organisation (n’importe quel annuaire *Azure AD - Multi-client)* et les comptes Microsoft personnels (par exemple, Skype, Xbox).</span><span class="sxs-lookup"><span data-stu-id="d5003-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="d5003-211">Pour **l’URI de redirection**:</span><span class="sxs-lookup"><span data-stu-id="d5003-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="d5003-212">&#x2713;Sélectionnez **Web**.</span><span class="sxs-lookup"><span data-stu-id="d5003-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="d5003-213">&#x2713; définir l’URL sur `https://token.botframework.com/.auth/web/redirect` .</span><span class="sxs-lookup"><span data-stu-id="d5003-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="d5003-214">Sélectionnez **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="d5003-214">Select **Register**.</span></span>

1. <span data-ttu-id="d5003-215">Une fois créé, Azure affiche la page **Vue d’ensemble** de l’application.</span><span class="sxs-lookup"><span data-stu-id="d5003-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="d5003-216">Copiez et enregistrez les informations suivantes dans un fichier :</span><span class="sxs-lookup"><span data-stu-id="d5003-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="d5003-217">Valeur **de l’ID de l’application (client).**</span><span class="sxs-lookup"><span data-stu-id="d5003-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="d5003-218">Vous utiliserez cette valeur ultérieurement comme *ID client* lorsque vous enregistrerez cette application d’identité Azure auprès de votre bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="d5003-219">Valeur **de l’ID** du répertoire (client).</span><span class="sxs-lookup"><span data-stu-id="d5003-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="d5003-220">Vous utiliserez également cette valeur ultérieurement comme *ID* de client pour inscrire cette application d’identité Azure auprès de votre bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="d5003-221">Dans le panneau gauche, **sélectionnez Certificats & secrets** pour créer une secret client pour votre application.</span><span class="sxs-lookup"><span data-stu-id="d5003-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="d5003-222">Sous **Les secrets client,** sélectionnez &#x2795; **Nouvelle secret client.**</span><span class="sxs-lookup"><span data-stu-id="d5003-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="d5003-223">Ajoutez une description pour identifier ce secret auprès d’autres personnes que vous devrez peut-être créer pour cette application, telles que l’application d’identité bot *dans Teams*.</span><span class="sxs-lookup"><span data-stu-id="d5003-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="d5003-224">La **sélection expire.**</span><span class="sxs-lookup"><span data-stu-id="d5003-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="d5003-225">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d5003-225">Select **Add**.</span></span>
   1. <span data-ttu-id="d5003-226">Avant de quitter cette page, **enregistrez le secret.**</span><span class="sxs-lookup"><span data-stu-id="d5003-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="d5003-227">Vous utiliserez cette valeur comme secret _client_ ultérieurement lorsque vous enregistrerez votre application Azure AD auprès de votre bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="d5003-228">Configurer la connexion du fournisseur d’identité et l’inscrire auprès du bot</span><span class="sxs-lookup"><span data-stu-id="d5003-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="d5003-229">Remarque : il existe deux options pour les fournisseurs de services ici : Azure AD V1 et Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="d5003-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="d5003-230">Les différences entre les deux fournisseurs sont résumées [ici,](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)mais en général, V2 offre plus de flexibilité en ce qui concerne la modification des autorisations de bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-230">The differences between the two providers are summarized [here](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="d5003-231">Graph Les autorisations d’API sont répertoriées dans le champ d’étendues et, à mesure que de nouvelles autorisations sont ajoutées, les bots permettent aux utilisateurs d’autoriser les nouvelles autorisations à la prochaine connexion.</span><span class="sxs-lookup"><span data-stu-id="d5003-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="d5003-232">Pour V1, le consentement du bot doit être supprimé par l’utilisateur pour que de nouvelles autorisations soient invités dans la boîte de dialogue OAuth.</span><span class="sxs-lookup"><span data-stu-id="d5003-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="d5003-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="d5003-233">Azure AD V1</span></span>

1. <span data-ttu-id="d5003-234">Dans le [**portail Azure,**][azure-portal]sélectionnez votre groupe de ressources dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d5003-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="d5003-235">Sélectionnez le lien d’inscription de votre canal bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="d5003-236">Ouvrez la page de ressources et **sélectionnez Configuration** **sous Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d5003-236">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="d5003-237">Sélectionnez **Ajouter une connexion OAuth Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d5003-237">Select **Add OAuth Connection Settings**.</span></span>    
<span data-ttu-id="d5003-238">L’image suivante affiche la sélection correspondante dans la page de ressources :</span><span class="sxs-lookup"><span data-stu-id="d5003-238">The following image displays the corresponding selection in the resource page:</span></span>  
<span data-ttu-id="d5003-239">![Configuration de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="d5003-239">![SampleAppDemoBot configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span>
1. <span data-ttu-id="d5003-240">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5003-240">Complete the form as follows:</span></span>

    1. <span data-ttu-id="d5003-241">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="d5003-241">**Name**.</span></span> <span data-ttu-id="d5003-242">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="d5003-242">Enter a name for the connection.</span></span> <span data-ttu-id="d5003-243">Vous utiliserez ce nom dans votre bot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="d5003-243">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="d5003-244">Par exemple *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="d5003-244">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="d5003-245">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="d5003-245">**Service Provider**.</span></span> <span data-ttu-id="d5003-246">Sélectionner **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5003-246">Select **Azure Active Directory**.</span></span> <span data-ttu-id="d5003-247">Une fois cette sélection sélectionnée, les champs spécifiques à Azure AD s’affichent.</span><span class="sxs-lookup"><span data-stu-id="d5003-247">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="d5003-248">**ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d5003-248">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="d5003-249">**Secret client**.</span><span class="sxs-lookup"><span data-stu-id="d5003-249">**Client secret**.</span></span> <span data-ttu-id="d5003-250">Entrez le secret que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d5003-250">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="d5003-251">**Type d’octroi**.</span><span class="sxs-lookup"><span data-stu-id="d5003-251">**Grant Type**.</span></span> <span data-ttu-id="d5003-252">Entrez `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="d5003-252">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="d5003-253">**URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="d5003-253">**Login URL**.</span></span> <span data-ttu-id="d5003-254">Entrez `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="d5003-254">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="d5003-255">**ID de client**, entrez l’ID d’annuaire **(client)**  que vous avez enregistré précédemment pour votre application d’identité Azure ou commun en fonction du type de compte pris en charge sélectionné lors de la création de l’application fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="d5003-255">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="d5003-256">Pour déterminer la valeur à attribuer, suivez ces critères :</span><span class="sxs-lookup"><span data-stu-id="d5003-256">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="d5003-257">Si vous avez sélectionné des comptes dans cet annuaire d’organisation uniquement (Microsoft uniquement - Client *unique)* ou des comptes dans un annuaire d’organisation *(annuaire Microsoft AAD - Multi-locataire),* entrez l’ID de locataire que vous avez enregistré précédemment pour l’application AAD. </span><span class="sxs-lookup"><span data-stu-id="d5003-257">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="d5003-258">Il s’agit du client associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="d5003-258">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="d5003-259">Si vous avez sélectionné des comptes dans un répertoire d’organisation (n’importe quel répertoire AAD - comptes Microsoft multi-clients  et personnels, par *exemple, Skype, Xbox, Outlook),* entrez le mot commun au lieu d’un ID de client.</span><span class="sxs-lookup"><span data-stu-id="d5003-259">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="d5003-260">Dans le cas contraire, l’application AAD vérifie via le client dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="d5003-260">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="d5003-261">h.</span><span class="sxs-lookup"><span data-stu-id="d5003-261">h.</span></span> <span data-ttu-id="d5003-262">Pour **l’URL de** la ressource, entrez `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="d5003-262">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="d5003-263">Cela n’est pas utilisé dans l’exemple de code actuel.</span><span class="sxs-lookup"><span data-stu-id="d5003-263">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="d5003-264">i.</span><span class="sxs-lookup"><span data-stu-id="d5003-264">i.</span></span> <span data-ttu-id="d5003-265">Laissez **les étendues** vides.</span><span class="sxs-lookup"><span data-stu-id="d5003-265">Leave **Scopes** blank.</span></span> <span data-ttu-id="d5003-266">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="d5003-266">The following image is an example:</span></span>

    ![Affichage adv1 de chaîne de connexion d’th de l’application teams bots](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="d5003-268">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d5003-268">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="d5003-269">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="d5003-269">Azure AD V2</span></span>

1. <span data-ttu-id="d5003-270">Dans le [**portail Azure,**][azure-portal]sélectionnez votre groupe de ressources dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d5003-270">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="d5003-271">Sélectionnez le lien d’inscription de votre canal bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-271">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="d5003-272">Ouvrez la page de ressources et **sélectionnez Configuration** **sous Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d5003-272">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="d5003-273">Sélectionnez **Ajouter une connexion OAuth Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d5003-273">Select **Add OAuth Connection Settings**.</span></span>  
<span data-ttu-id="d5003-274">L’image suivante affiche la sélection correspondante dans la page de ressources :</span><span class="sxs-lookup"><span data-stu-id="d5003-274">The following image displays the corresponding selection in the resource page:</span></span>        
<span data-ttu-id="d5003-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="d5003-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span> 

1. <span data-ttu-id="d5003-276">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5003-276">Complete the form as follows:</span></span>

    1. <span data-ttu-id="d5003-277">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="d5003-277">**Name**.</span></span> <span data-ttu-id="d5003-278">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="d5003-278">Enter a name for the connection.</span></span> <span data-ttu-id="d5003-279">Vous utiliserez ce nom dans votre bot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="d5003-279">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="d5003-280">Par exemple *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="d5003-280">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="d5003-281">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="d5003-281">**Service Provider**.</span></span> <span data-ttu-id="d5003-282">Sélectionnez **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="d5003-282">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="d5003-283">Une fois cette sélection sélectionnée, les champs spécifiques à Azure AD s’affichent.</span><span class="sxs-lookup"><span data-stu-id="d5003-283">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="d5003-284">**ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d5003-284">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="d5003-285">**Secret client**.</span><span class="sxs-lookup"><span data-stu-id="d5003-285">**Client secret**.</span></span> <span data-ttu-id="d5003-286">Entrez le secret que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d5003-286">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="d5003-287">**URL de Exchange jeton**.</span><span class="sxs-lookup"><span data-stu-id="d5003-287">**Token Exchange URL**.</span></span> <span data-ttu-id="d5003-288">Laissez ce vide.</span><span class="sxs-lookup"><span data-stu-id="d5003-288">Leave this blank.</span></span>
    1. <span data-ttu-id="d5003-289">**ID de client**, entrez l’ID d’annuaire **(client)**  que vous avez enregistré précédemment pour votre application d’identité Azure ou commun en fonction du type de compte pris en charge sélectionné lors de la création de l’application fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="d5003-289">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="d5003-290">Pour déterminer la valeur à attribuer, suivez ces critères :</span><span class="sxs-lookup"><span data-stu-id="d5003-290">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="d5003-291">Si vous avez sélectionné des comptes dans cet annuaire d’organisation uniquement (Microsoft uniquement - Client *unique)* ou des comptes dans un annuaire d’organisation *(annuaire Microsoft AAD - Multi-locataire),* entrez l’ID de locataire que vous avez enregistré précédemment pour l’application AAD. </span><span class="sxs-lookup"><span data-stu-id="d5003-291">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="d5003-292">Il s’agit du client associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="d5003-292">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="d5003-293">Si vous avez sélectionné des comptes dans un répertoire d’organisation (n’importe quel répertoire AAD - comptes Microsoft multi-clients  et personnels, par *exemple, Skype, Xbox, Outlook),* entrez le mot commun au lieu d’un ID de client.</span><span class="sxs-lookup"><span data-stu-id="d5003-293">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="d5003-294">Dans le cas contraire, l’application AAD vérifie via le client dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="d5003-294">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="d5003-295">Pour **les étendues,** entrez une liste délimitée par des espaces d’autorisations graphiques que cette application requiert par exemple : User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="d5003-295">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="d5003-296">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d5003-296">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="d5003-297">Tester la connexion</span><span class="sxs-lookup"><span data-stu-id="d5003-297">Test the connection</span></span>

1. <span data-ttu-id="d5003-298">Sélectionnez l’entrée de connexion pour ouvrir la connexion que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="d5003-298">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="d5003-299">Sélectionnez **Tester la connexion** en haut du panneau **Paramètres de connexion** du fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="d5003-299">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="d5003-300">La première fois que vous le faites, une nouvelle fenêtre de navigateur s’ouvre et vous demande de sélectionner un compte.</span><span class="sxs-lookup"><span data-stu-id="d5003-300">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="d5003-301">Sélectionnez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d5003-301">Select the one you want to use.</span></span>
1. <span data-ttu-id="d5003-302">Ensuite, vous serez invité à autoriser le fournisseur d’identité à utiliser vos données (informations d’identification).</span><span class="sxs-lookup"><span data-stu-id="d5003-302">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="d5003-303">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="d5003-303">The following image is an example:</span></span>

    ![teams bot auth connection string adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="d5003-305">Sélectionnez **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="d5003-305">Select **Accept**.</span></span>
1. <span data-ttu-id="d5003-306">Cela doit ensuite vous rediriger vers une page **De connexion de test à \<your-connection-name> réussite.**</span><span class="sxs-lookup"><span data-stu-id="d5003-306">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="d5003-307">Actualisez la page si vous obtenez une erreur.</span><span class="sxs-lookup"><span data-stu-id="d5003-307">Refresh the page if you get an error.</span></span> <span data-ttu-id="d5003-308">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="d5003-308">The following image is an example:</span></span>

    ![teams bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="d5003-310">Le nom de connexion est utilisé par le code du bot pour récupérer les jetons d’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-310">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="d5003-311">Préparer l’exemple de code du bot</span><span class="sxs-lookup"><span data-stu-id="d5003-311">Prepare the bot sample code</span></span>

<span data-ttu-id="d5003-312">Une fois les paramètres préliminaires terminés, nous allons nous concentrer sur la création du bot à utiliser dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d5003-312">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="d5003-313">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d5003-313">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="d5003-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="d5003-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="d5003-315">Lancez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5003-315">Launch Visual Studio.</span></span>
1. <span data-ttu-id="d5003-316">Dans la barre d’outils, **sélectionnez Fichier -> Ouvrir -> Project/Solution** et ouvrez le projet bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-316">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="d5003-317">Dans C# mise **à jourappsettings.jsles informations suivantes** :</span><span class="sxs-lookup"><span data-stu-id="d5003-317">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="d5003-318">Définissez `ConnectionName` ce nom sur le nom de la connexion de fournisseur d’identité que vous avez ajoutée à l’inscription du canal du bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-318">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="d5003-319">Le nom que nous avons utilisé dans cet exemple *est BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="d5003-319">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="d5003-320">Définissez `MicrosoftAppId` ce dernier sur **l’ID d’application** du bot que vous avez enregistré au moment de l’inscription du canal du bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-320">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="d5003-321">Définissez `MicrosoftAppPassword` la secret client **que** vous avez enregistrée au moment de l’inscription au canal du bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-321">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="d5003-322">En fonction des caractères dans votre secret de bot, vous devrez peut-être éviter le mot de passe au code XML.</span><span class="sxs-lookup"><span data-stu-id="d5003-322">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="d5003-323">Par exemple, toutes les andersands (&) doivent être codées comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="d5003-323">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="d5003-324">Dans l’Explorateur de solutions, accédez au dossier, ouvrez et définissez l’ID d’application du bot que vous avez enregistré au moment de l’inscription du `TeamsAppManifest` `manifest.json` canal du `id` `botId` bot. </span><span class="sxs-lookup"><span data-stu-id="d5003-324">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="d5003-325">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d5003-325">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="d5003-326">Clone [node-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="d5003-326">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="d5003-327">Dans une console, accédez au projet :</span><span class="sxs-lookup"><span data-stu-id="d5003-327">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="d5003-328">Installer des modules</span><span class="sxs-lookup"><span data-stu-id="d5003-328">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="d5003-329">Mettez à jour la configuration **.env** comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5003-329">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="d5003-330">Définissez `MicrosoftAppId` ce dernier sur **l’ID d’application** du bot que vous avez enregistré au moment de l’inscription du canal du bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-330">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="d5003-331">Définissez `MicrosoftAppPassword` la secret client **que** vous avez enregistrée au moment de l’inscription au canal du bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-331">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="d5003-332">Définissez `connectionName` le nom de la connexion du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="d5003-332">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="d5003-333">En fonction des caractères dans votre secret de bot, vous devrez peut-être éviter le mot de passe au code XML.</span><span class="sxs-lookup"><span data-stu-id="d5003-333">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="d5003-334">Par exemple, toutes les andersands (&) doivent être codées comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="d5003-334">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="d5003-335">Dans le dossier, ouvrez et définissez votre ID d’application Microsoft et `teamsAppManifest` `manifest.json` `id` l’ID d’application du  `botId` **bot** que vous avez enregistré au moment de l’inscription du canal du bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-335">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="d5003-336">Python</span><span class="sxs-lookup"><span data-stu-id="d5003-336">Python</span></span>](#tab/python)

1. <span data-ttu-id="d5003-337">Clonez [py-auth-sample][teams-auth-bot-py] à partir du référentiel github.</span><span class="sxs-lookup"><span data-stu-id="d5003-337">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="d5003-338">Mettre **à jour config.py**:</span><span class="sxs-lookup"><span data-stu-id="d5003-338">Update **config.py**:</span></span>

    - <span data-ttu-id="d5003-339">Définissez `ConnectionName` ce paramètre sur le nom du paramètre de connexion OAuth que vous avez ajouté à votre bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-339">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="d5003-340">Définissez `MicrosoftAppId` et `MicrosoftAppPassword` définissez l’ID d’application et la secret de l’application de votre bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-340">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="d5003-341">En fonction des caractères dans votre secret de bot, vous devrez peut-être éviter le mot de passe au code XML.</span><span class="sxs-lookup"><span data-stu-id="d5003-341">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="d5003-342">Par exemple, toutes les andersands (&) doivent être codées comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="d5003-342">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="d5003-343">Déployer le bot sur Azure</span><span class="sxs-lookup"><span data-stu-id="d5003-343">Deploy the bot to Azure</span></span>

<span data-ttu-id="d5003-344">Pour déployer le bot, suivez les étapes de la procédure de déploiement de [votre bot sur Azure.](https://aka.ms/azure-bot-deployment-cli)</span><span class="sxs-lookup"><span data-stu-id="d5003-344">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="d5003-345">Sinon, dans Visual Studio, vous pouvez suivre les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5003-345">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="d5003-346">Dans *Visual Studio’Explorateur de* solutions, sélectionnez et maintenez (ou cliquez avec le bouton droit) le nom du projet.</span><span class="sxs-lookup"><span data-stu-id="d5003-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="d5003-347">Dans le menu déroulant, sélectionnez **Publier.**</span><span class="sxs-lookup"><span data-stu-id="d5003-347">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="d5003-348">Dans la fenêtre affichée, sélectionnez le **lien** Nouveau.</span><span class="sxs-lookup"><span data-stu-id="d5003-348">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="d5003-349">Dans la fenêtre de boîte de dialogue, **sélectionnez Service d’application** sur la gauche et **Créer** à droite.</span><span class="sxs-lookup"><span data-stu-id="d5003-349">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="d5003-350">Sélectionnez **le bouton** Publier.</span><span class="sxs-lookup"><span data-stu-id="d5003-350">Select the **Publish** button.</span></span>
1. <span data-ttu-id="d5003-351">Dans la fenêtre de boîte de dialogue suivante, entrez les informations requises.</span><span class="sxs-lookup"><span data-stu-id="d5003-351">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="d5003-352">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="d5003-352">The following is an example:</span></span>

    ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="d5003-354">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d5003-354">Select **Create**.</span></span>
1. <span data-ttu-id="d5003-355">Si le déploiement se termine correctement, vous devez le voir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5003-355">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="d5003-356">En outre, une page s’affiche dans votre navigateur par défaut pour dire *que votre bot est prêt !*.</span><span class="sxs-lookup"><span data-stu-id="d5003-356">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="d5003-357">L’URL sera similaire à celle-ci : `https://botteamsauth.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="d5003-357">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="d5003-358">Enregistrez-le dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="d5003-358">Save it to a file.</span></span>
1. <span data-ttu-id="d5003-359">Dans votre navigateur, accédez au [**portail Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="d5003-359">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="d5003-360">Vérifiez votre groupe de ressources, le bot doit être répertorié avec les autres ressources.</span><span class="sxs-lookup"><span data-stu-id="d5003-360">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="d5003-361">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="d5003-361">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="d5003-363">Dans le groupe de ressources, sélectionnez le nom d’inscription du canal bot (lien).</span><span class="sxs-lookup"><span data-stu-id="d5003-363">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="d5003-364">Dans le panneau gauche, **sélectionnez Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d5003-364">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="d5003-365">Dans la **zone Point de terminaison de messagerie,** entrez l’URL obtenue ci-dessus, suivie de `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="d5003-365">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="d5003-366">Voici un exemple : `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="d5003-366">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="d5003-367">Sélectionnez **le bouton** Enregistrer dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="d5003-367">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="d5003-368">Tester le bot à l’aide de l’émulateur</span><span class="sxs-lookup"><span data-stu-id="d5003-368">Test the bot using the Emulator</span></span>

<span data-ttu-id="d5003-369">Si vous ne l’avez pas déjà fait, installez [le Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="d5003-369">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="d5003-370">Voir aussi [Déboguer avec l’émulateur.](https://aka.ms/bot-framework-emulator-debug-with-emulator)</span><span class="sxs-lookup"><span data-stu-id="d5003-370">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="d5003-371">Pour que l’exemple de connexion du bot fonctionne, vous devez configurer l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-371">In order for the bot sample login to work you must configure the Emulator.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="d5003-372">Configurer l’émulateur pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="d5003-372">Configure the Emulator for authentication</span></span>

<span data-ttu-id="d5003-373">Si un bot nécessite une authentification, vous devez configurer l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-373">If a bot requires authentication, you must configure the Emulator.</span></span> <span data-ttu-id="d5003-374">Pour configurer :</span><span class="sxs-lookup"><span data-stu-id="d5003-374">To configure:</span></span>

1. <span data-ttu-id="d5003-375">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-375">Start the Emulator.</span></span>
1. <span data-ttu-id="d5003-376">Dans l’émulateur, sélectionnez l’icône d’engrenage &#9881;  en bas à gauche ou l’onglet Paramètres’émulateur dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="d5003-376">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="d5003-377">Cochez la case **en authentification version 1.0.**</span><span class="sxs-lookup"><span data-stu-id="d5003-377">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="d5003-378">Entrez le chemin d’accès local à **l’outil ngrok.**</span><span class="sxs-lookup"><span data-stu-id="d5003-378">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="d5003-379">*Consultez* le Wiki Bot Framework Emulator/ngrok [d’intégration](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))de tunneling.</span><span class="sxs-lookup"><span data-stu-id="d5003-379">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="d5003-380">Pour plus d’informations sur l’outil, [voir ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="d5003-380">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="d5003-381">Cochez la case par Exécuter ngrok au démarrage de **l’émulateur.**</span><span class="sxs-lookup"><span data-stu-id="d5003-381">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="d5003-382">Sélectionnez le **bouton** Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="d5003-382">Select the **Save** button.</span></span>

<span data-ttu-id="d5003-383">Lorsque le bot affiche une carte de visite et que l’utilisateur sélectionne le bouton de la signature, l’émulateur ouvre une page que l’utilisateur peut utiliser pour se connecter avec le fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d5003-383">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="d5003-384">Une fois que l’utilisateur a fait cela, le fournisseur génère un jeton utilisateur et l’envoie au bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-384">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="d5003-385">Après cela, le bot peut agir pour le compte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-385">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="d5003-386">Tester le bot localement</span><span class="sxs-lookup"><span data-stu-id="d5003-386">Test the bot locally</span></span>

<span data-ttu-id="d5003-387">Une fois que vous avez configuré le mécanisme d’authentification, vous pouvez effectuer le test réel du bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-387">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="d5003-388">Exécutez l’exemple de bot localement sur votre ordinateur, Visual Studio par exemple.</span><span class="sxs-lookup"><span data-stu-id="d5003-388">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="d5003-389">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-389">Start the Emulator.</span></span>
1. <span data-ttu-id="d5003-390">Sélectionnez **le bouton Ouvrir le bot.**</span><span class="sxs-lookup"><span data-stu-id="d5003-390">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="d5003-391">Dans **l’URL du bot,** entrez l’URL locale du bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-391">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="d5003-392">Généralement, `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="d5003-392">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="d5003-393">Dans **l’ID d’application Microsoft,** entrez l’ID d’application du bot à partir de `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="d5003-393">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="d5003-394">Dans le mot **de passe de l’application Microsoft,** entrez le mot de passe de l’application du bot à partir du `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="d5003-394">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="d5003-395">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="d5003-395">Select **Connect**.</span></span>
1. <span data-ttu-id="d5003-396">Une fois que le bot est en cours d’exécution, entrez du texte pour afficher la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="d5003-396">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="d5003-397">Sélectionnez le bouton **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="d5003-397">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="d5003-398">Une boîte de dialogue s’affiche pour confirmer **l’ouverture de l’URL.**</span><span class="sxs-lookup"><span data-stu-id="d5003-398">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="d5003-399">Cela permet à l’utilisateur du bot (vous) d’être authentifié.</span><span class="sxs-lookup"><span data-stu-id="d5003-399">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="d5003-400">Sélectionner **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="d5003-400">Select **Confirm**.</span></span>
1. <span data-ttu-id="d5003-401">Si vous y êtes invité, sélectionnez le compte de l’utilisateur applicable.</span><span class="sxs-lookup"><span data-stu-id="d5003-401">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="d5003-402">Selon la configuration que vous avez utilisée pour l’émulateur, vous obtenez l’une des configurations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5003-402">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="d5003-403">**Utilisation du code de vérification de la signature**</span><span class="sxs-lookup"><span data-stu-id="d5003-403">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="d5003-404">&#x2713; Fenêtre ouverte affichant le code de validation.</span><span class="sxs-lookup"><span data-stu-id="d5003-404">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="d5003-405">&#x2713; copiez et entrez le code de validation dans la zone de conversation pour terminer la signature.</span><span class="sxs-lookup"><span data-stu-id="d5003-405">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="d5003-406">**Utilisation de jetons d’authentification.**</span><span class="sxs-lookup"><span data-stu-id="d5003-406">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="d5003-407">&#x2713; vous êtes connecté en fonction de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d5003-407">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="d5003-408">L’image suivante est un exemple de l’interface utilisateur du bot après vous être connecté :</span><span class="sxs-lookup"><span data-stu-id="d5003-408">The following image is an example of the bot UI after you've logged in:</span></span>

    ![émulateur de connexion au bot d’authentification](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="d5003-410">Si vous sélectionnez **Oui** lorsque le bot vous demande *Voulez-vous* afficher votre jeton ? , vous recevrez une réponse semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="d5003-410">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![Jeton d’émulateur de connexion du bot d’authentification](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="d5003-412">Entrez **la connexion dans** la zone de conversation d’entrée pour vous déconnecter. Cela libère le jeton utilisateur et le bot ne peut pas agir en votre nom tant que vous ne vous connectez pas à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d5003-412">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="d5003-413">L’authentification du bot nécessite l’utilisation **du service Bot Connector.**</span><span class="sxs-lookup"><span data-stu-id="d5003-413">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="d5003-414">Le service accède aux informations d’inscription des canaux du bot pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-414">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="d5003-415">Tester le bot déployé</span><span class="sxs-lookup"><span data-stu-id="d5003-415">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="d5003-416">Dans votre navigateur, accédez au [**portail Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="d5003-416">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="d5003-417">Recherchez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d5003-417">Find your resource group.</span></span>
1. <span data-ttu-id="d5003-418">Sélectionnez le lien de la ressource.</span><span class="sxs-lookup"><span data-stu-id="d5003-418">Select the resource link.</span></span> <span data-ttu-id="d5003-419">La page de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d5003-419">The resource page is displayed.</span></span>
1. <span data-ttu-id="d5003-420">Dans la page de ressources, **sélectionnez Tester dans la conversation web.**</span><span class="sxs-lookup"><span data-stu-id="d5003-420">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="d5003-421">Le bot démarre et affiche les salutations prédéfinës.</span><span class="sxs-lookup"><span data-stu-id="d5003-421">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="d5003-422">Tapez quoi que ce soit dans la zone de conversation.</span><span class="sxs-lookup"><span data-stu-id="d5003-422">Type anything in the chat box.</span></span>
1. <span data-ttu-id="d5003-423">Sélectionnez la **zone Se** connectez.</span><span class="sxs-lookup"><span data-stu-id="d5003-423">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="d5003-424">Une boîte de dialogue s’affiche pour confirmer **l’ouverture de l’URL.**</span><span class="sxs-lookup"><span data-stu-id="d5003-424">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="d5003-425">Cela permet à l’utilisateur du bot (vous) d’être authentifié.</span><span class="sxs-lookup"><span data-stu-id="d5003-425">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="d5003-426">Sélectionner **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="d5003-426">Select **Confirm**.</span></span>
1. <span data-ttu-id="d5003-427">Si vous y êtes invité, sélectionnez le compte de l’utilisateur applicable.</span><span class="sxs-lookup"><span data-stu-id="d5003-427">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="d5003-428">L’image suivante est un exemple de l’interface utilisateur du bot après vous être connecté :</span><span class="sxs-lookup"><span data-stu-id="d5003-428">The following image is an example of the bot UI after you have logged in:</span></span>

    ![Connexion du bot d’authentification déployée](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="d5003-430">.</span><span class="sxs-lookup"><span data-stu-id="d5003-430">.</span></span>

1. <span data-ttu-id="d5003-431">Sélectionnez le **bouton Oui** pour afficher votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d5003-431">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="d5003-432">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="d5003-432">The following image is an example:</span></span>

    ![Jeton déployé de connexion au bot d’authentification](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="d5003-434">.</span><span class="sxs-lookup"><span data-stu-id="d5003-434">.</span></span>

1. <span data-ttu-id="d5003-435">Entrez la connexion pour vous déconnecter.</span><span class="sxs-lookup"><span data-stu-id="d5003-435">Enter logout to sign out.</span></span>

    ![Connexion déployée par le bot d’th](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="d5003-437">Si vous avez des problèmes de connexion, essayez de tester à nouveau la connexion comme décrit dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="d5003-437">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="d5003-438">Cela pourrait recréer le jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d5003-438">This could recreate the authentication token.</span></span>
> <span data-ttu-id="d5003-439">Avec le client De conversation web Bot Framework dans Azure, vous devrez peut-être vous y connecter plusieurs fois avant que l’authentification ne soit établie correctement.</span><span class="sxs-lookup"><span data-stu-id="d5003-439">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="d5003-440">Installer et tester le bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="d5003-440">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="d5003-441">Dans votre projet de bot, assurez-vous que le dossier contient `TeamsAppManifest` le contenu et les `manifest.json` `outline.png` `color.png` fichiers.</span><span class="sxs-lookup"><span data-stu-id="d5003-441">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="d5003-442">Dans l’Explorateur de solutions, accédez au `TeamsAppManifest` dossier.</span><span class="sxs-lookup"><span data-stu-id="d5003-442">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="d5003-443">Modifiez `manifest.json` en attribuant les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5003-443">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="d5003-444">Assurez-vous que **l’ID d’application** du bot que vous avez reçu au moment de l’inscription au canal du bot est affecté à `id` et `botId` .</span><span class="sxs-lookup"><span data-stu-id="d5003-444">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="d5003-445">Affectez cette valeur : `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="d5003-445">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="d5003-446">Sélectionnez **et compresser** `manifest.json` les fichiers et les `outline.png` `color.png` fichiers.</span><span class="sxs-lookup"><span data-stu-id="d5003-446">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="d5003-447">Ouvrez **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="d5003-447">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="d5003-448">Dans le panneau gauche, en bas, sélectionnez **l’icône Applications.**</span><span class="sxs-lookup"><span data-stu-id="d5003-448">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="d5003-449">Dans le panneau droit, en bas, sélectionnez **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="d5003-449">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="d5003-450">Accédez au `TeamsAppManifest` dossier et téléchargez le manifeste compressé.</span><span class="sxs-lookup"><span data-stu-id="d5003-450">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="d5003-451">L’Assistant suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="d5003-451">The following wizard is displayed:</span></span>

    ![Chargement des équipes de bot d’th](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="d5003-453">Sélectionnez le bouton **Ajouter à une équipe**.</span><span class="sxs-lookup"><span data-stu-id="d5003-453">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="d5003-454">Dans la fenêtre suivante, sélectionnez l’équipe dans laquelle vous souhaitez utiliser le bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-454">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="d5003-455">Sélectionnez **le bouton Configurer un bot.**</span><span class="sxs-lookup"><span data-stu-id="d5003-455">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="d5003-456">Sélectionnez les trois points (&#x25cf;&#x25cf;&#x25cf;) dans le panneau gauche.</span><span class="sxs-lookup"><span data-stu-id="d5003-456">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="d5003-457">Sélectionnez ensuite **l’icône App Studio.**</span><span class="sxs-lookup"><span data-stu-id="d5003-457">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="d5003-458">Sélectionnez **l’onglet Éditeur de** manifeste. Vous devriez voir l’icône du bot que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d5003-458">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="d5003-459">En outre, vous devriez être en mesure de voir le bot répertorié en tant que contact dans la liste de conversation que vous pouvez utiliser pour échanger des messages avec le bot.</span><span class="sxs-lookup"><span data-stu-id="d5003-459">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="d5003-460">Test du bot localement dans Teams</span><span class="sxs-lookup"><span data-stu-id="d5003-460">Testing the bot locally in Teams</span></span>

<span data-ttu-id="d5003-461">Microsoft Teams est un produit entièrement basé sur le cloud, tous les services accessibles doivent être disponibles à partir du cloud à l’aide de points de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d5003-461">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="d5003-462">Par conséquent, pour permettre au bot (notre exemple) de fonctionner dans Teams, vous devez publier le code dans le cloud de votre choix ou rendre une instance en cours d’exécution localement accessible en externe via un outil **de tunneling.**</span><span class="sxs-lookup"><span data-stu-id="d5003-462">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="d5003-463">Nous vous  [recommandons ngrok](https://ngrok.com/download), qui crée une URL adressan externe pour un port que vous ouvrez localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d5003-463">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="d5003-464">Pour configurer ngrok en vue de l’exécution locale de Microsoft Teams’application, suivez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5003-464">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="d5003-465">Dans une fenêtre terminal, allez dans le répertoire où vous `ngrok.exe` avez installé.</span><span class="sxs-lookup"><span data-stu-id="d5003-465">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="d5003-466">Nous vous suggérons de définir *le chemin d’accès de la variable* d’environnement pour qu’il pointe vers celui-ci.</span><span class="sxs-lookup"><span data-stu-id="d5003-466">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="d5003-467">Exécuter, par exemple, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="d5003-467">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="d5003-468">Remplacez le numéro de port selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="d5003-468">Replace the port number as needed.</span></span>
<span data-ttu-id="d5003-469">Cela lance ngrok pour écouter sur le port que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="d5003-469">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="d5003-470">En retour, il vous donne une URL adressan externe, valide tant que ngrok est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d5003-470">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="d5003-471">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="d5003-471">The following image is an example:</span></span>

    ![teams bot app auth connection string adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="d5003-473">.</span><span class="sxs-lookup"><span data-stu-id="d5003-473">.</span></span>

1. <span data-ttu-id="d5003-474">Copiez l’adresse HTTPS de forwarding.</span><span class="sxs-lookup"><span data-stu-id="d5003-474">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="d5003-475">Il doit être similaire à ce qui `https://dea822bf.ngrok.io/` suit :</span><span class="sxs-lookup"><span data-stu-id="d5003-475">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="d5003-476">Append `/api/messages` pour obtenir `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="d5003-476">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="d5003-477">Il s’agit du **point de terminaison** des messages pour le bot s’exécutant localement sur votre ordinateur et accessible sur le web dans une conversation Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d5003-477">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="d5003-478">Une dernière étape consiste à mettre à jour le point de terminaison des messages du bot déployé.</span><span class="sxs-lookup"><span data-stu-id="d5003-478">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="d5003-479">Dans l’exemple, nous avons déployé le bot dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d5003-479">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="d5003-480">Par donc, \*\*nous allons effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5003-480">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="d5003-481">Dans votre navigateur, accédez au [**portail Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="d5003-481">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="d5003-482">Sélectionnez votre **inscription au canal bot.**</span><span class="sxs-lookup"><span data-stu-id="d5003-482">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="d5003-483">Dans le panneau gauche, **sélectionnez Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d5003-483">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="d5003-484">Dans le panneau droit, dans la **zone** Point de terminaison de messagerie, entrez l’URL ngrok, dans notre `https://dea822bf.ngrok.io/api/messages` exemple.</span><span class="sxs-lookup"><span data-stu-id="d5003-484">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="d5003-485">Démarrez votre bot localement, par exemple en mode Visual Studio débogage.</span><span class="sxs-lookup"><span data-stu-id="d5003-485">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="d5003-486">Testez le bot lors de l’exécution locale à l’aide de la **conversation Web test** du portail Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d5003-486">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="d5003-487">Comme l’émulateur, ce test ne vous permet pas d’accéder Teams fonctionnalités spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d5003-487">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="d5003-488">Dans la fenêtre terminal où s’exécute le trafic HTTP entre le bot et `ngrok` le client de conversation web.</span><span class="sxs-lookup"><span data-stu-id="d5003-488">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="d5003-489">Si vous souhaitez une vue plus détaillée, dans une fenêtre de navigateur, entrez ce que vous avez obtenu à partir de `http://127.0.0.1:4040` la fenêtre terminal précédente.</span><span class="sxs-lookup"><span data-stu-id="d5003-489">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="d5003-490">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="d5003-490">The following image is an example:</span></span>

    ![Test ngrok des équipes de bot d’th](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="d5003-492">.</span><span class="sxs-lookup"><span data-stu-id="d5003-492">.</span></span>

> [!NOTE]
> <span data-ttu-id="d5003-493">Si vous arrêtez et redémarrez ngrok, l’URL change.</span><span class="sxs-lookup"><span data-stu-id="d5003-493">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="d5003-494">Pour utiliser ngrok dans votre projet et en fonction des fonctionnalités que vous utilisez, vous devez mettre à jour toutes les références d’URL.</span><span class="sxs-lookup"><span data-stu-id="d5003-494">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="d5003-495">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d5003-495">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="d5003-496">TeamsAppManifest/manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="d5003-496">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="d5003-497">Ce manifeste contient les informations requises par Microsoft Teams pour se connecter au bot :</span><span class="sxs-lookup"><span data-stu-id="d5003-497">This manifest contains information needed by Microsoft Teams to connect with the bot:</span></span>  

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

<span data-ttu-id="d5003-498">Avec l’authentification, Teams se comporte légèrement différemment des autres canaux, comme expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d5003-498">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="d5003-499">Gestion de l’activité d’appel</span><span class="sxs-lookup"><span data-stu-id="d5003-499">Handling Invoke Activity</span></span>

<span data-ttu-id="d5003-500">Une **activité d’appel** est envoyée au bot au lieu de l’activité d’événement utilisée par d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="d5003-500">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="d5003-501">Cette action est effectuée en sous-classant **l’ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="d5003-501">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="d5003-502">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d5003-502">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="d5003-503">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="d5003-503">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="d5003-504">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="d5003-504">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="d5003-505">*L’activité d’appel* doit être transmis à la boîte de dialogue si **le OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d5003-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="d5003-506">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="d5003-506">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="d5003-507">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d5003-507">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="d5003-508">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="d5003-508">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="d5003-509">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="d5003-509">**bots/teamsBot.js**</span></span>

<span data-ttu-id="d5003-510">*L’activité d’appel* doit être transmis à la boîte de dialogue si **le OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d5003-510">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="d5003-511">**dialogs/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="d5003-511">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="d5003-512">Dans une étape de boîte de dialogue, utilisez pour démarrer l’invite OAuth, qui demande à `beginDialog` l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="d5003-512">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="d5003-513">Si l’utilisateur est déjà signé, cela génère un événement de réponse de jeton, sans que l’utilisateur soit invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="d5003-513">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="d5003-514">Sinon, cela invite l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="d5003-514">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="d5003-515">Le service Azure Bot envoie l’événement de réponse du jeton après que l’utilisateur a tenté de se connecter.</span><span class="sxs-lookup"><span data-stu-id="d5003-515">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="d5003-516">Dans l’étape de boîte de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="d5003-516">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="d5003-517">S’il n’est pas null, l’utilisateur s’est correctement inscrit.</span><span class="sxs-lookup"><span data-stu-id="d5003-517">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="d5003-518">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="d5003-518">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="d5003-519">Python</span><span class="sxs-lookup"><span data-stu-id="d5003-519">Python</span></span>](#tab/python-sample)

<span data-ttu-id="d5003-520">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="d5003-520">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="d5003-521">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="d5003-521">**bots/teams_bot.py**</span></span>

<span data-ttu-id="d5003-522">*L’activité d’appel* doit être transmis à la boîte de dialogue si **le OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d5003-522">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="d5003-523">**dialogs/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="d5003-523">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="d5003-524">Dans une étape de boîte de dialogue, utilisez pour démarrer l’invite OAuth, qui demande à `begin_dialog` l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="d5003-524">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="d5003-525">Si l’utilisateur est déjà signé, cela génère un événement de réponse de jeton, sans que l’utilisateur soit invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="d5003-525">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="d5003-526">Sinon, cela invite l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="d5003-526">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="d5003-527">Le service Azure Bot envoie l’événement de réponse du jeton après que l’utilisateur a tenté de se connecter.</span><span class="sxs-lookup"><span data-stu-id="d5003-527">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="d5003-528">Dans l’étape de boîte de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="d5003-528">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="d5003-529">S’il n’est pas null, l’utilisateur s’est correctement inscrit.</span><span class="sxs-lookup"><span data-stu-id="d5003-529">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="d5003-530">**dialogs/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="d5003-530">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a><span data-ttu-id="d5003-531">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d5003-531">See also</span></span>

[<span data-ttu-id="d5003-532">Ajouter l’authentification via Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="d5003-532">Add authentication through Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
