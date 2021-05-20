---
title: Ajouter l’authentification à votre bot Teams’argent
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
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="7deb7-103">Ajouter l’authentification à votre bot Teams’argent</span><span class="sxs-lookup"><span data-stu-id="7deb7-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="7deb7-104">Il ya des moments où vous devrez peut-être créer des bots dans Microsoft Teams qui peuvent accéder à des ressources pour le compte de l’utilisateur, comme un service de messagerie.</span><span class="sxs-lookup"><span data-stu-id="7deb7-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="7deb7-105">Cet article montre comment utiliser Azure Bot Service v4 SDK authentification, basée sur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="7deb7-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="7deb7-106">Il est ainsi plus facile de développer un bot qui peut utiliser des jetons d’authentification basés sur les informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="7deb7-107">La clé dans tout cela est l’utilisation de **fournisseurs d’identité**, comme nous le verrons plus loin.</span><span class="sxs-lookup"><span data-stu-id="7deb7-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="7deb7-108">OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="7deb7-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="7deb7-109">Une compréhension de base d’OAuth 2.0 est une condition préalable pour travailler avec l’authentification Teams.</span><span class="sxs-lookup"><span data-stu-id="7deb7-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="7deb7-110">Voir [OAuth 2 Simplifié](https://aka.ms/oauth2-simplified) pour une compréhension de base, [et OAuth 2.0](https://oauth.net/2/) pour la spécification complète.</span><span class="sxs-lookup"><span data-stu-id="7deb7-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="7deb7-111">Pour plus d’informations sur la façon dont le Service Azure Bot gère l’authentification, consultez [l’authentification utilisateur dans une conversation](https://aka.ms/azure-bot-authentication).</span><span class="sxs-lookup"><span data-stu-id="7deb7-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="7deb7-112">Voici les titres des sections de cet article :</span><span class="sxs-lookup"><span data-stu-id="7deb7-112">In this article you'll learn:</span></span>

- <span data-ttu-id="7deb7-113">**Comment créer un bot activé par l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="7deb7-114">Vous utiliserez [l’échantillon cs-auth pour gérer][teams-auth-bot-cs] les informations d’identification de connexion de l’utilisateur et la génération du jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="7deb7-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="7deb7-115">**Comment déployer le bot sur Azure et l’associer à un fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="7deb7-116">Le fournisseur émet un jeton basé sur les informations d’identification de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="7deb7-117">Le bot peut utiliser le jeton pour accéder aux ressources, telles qu’un service postal, qui nécessitent une authentification.</span><span class="sxs-lookup"><span data-stu-id="7deb7-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="7deb7-118">Pour plus d’informations, [Microsoft Teams flux d’authentification pour les bots](auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="7deb7-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="7deb7-119">**Comment intégrer le bot dans Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="7deb7-120">Une fois que le bot a été intégré, vous pouvez vous connecter et échanger des messages avec lui dans un chat.</span><span class="sxs-lookup"><span data-stu-id="7deb7-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7deb7-121">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7deb7-121">Prerequisites</span></span>

- <span data-ttu-id="7deb7-122">Connaissance des bases [bot , état][concept-basics]de gestion , [la][concept-state]bibliothèque de [dialogues][concept-dialogs], et comment implémenter [le flux de conversation séquentielle][simple-dialog].</span><span class="sxs-lookup"><span data-stu-id="7deb7-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="7deb7-123">Connaissance du développement Azure et OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="7deb7-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="7deb7-124">Les versions actuelles de Visual Studio et Git.</span><span class="sxs-lookup"><span data-stu-id="7deb7-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="7deb7-125">Compte Azure.</span><span class="sxs-lookup"><span data-stu-id="7deb7-125">Azure account.</span></span> <span data-ttu-id="7deb7-126">Si nécessaire, vous pouvez créer un [compte azure gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7deb7-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="7deb7-127">L’échantillon suivant :</span><span class="sxs-lookup"><span data-stu-id="7deb7-127">The following sample:</span></span>

    | <span data-ttu-id="7deb7-128">Échantillon</span><span class="sxs-lookup"><span data-stu-id="7deb7-128">Sample</span></span> | <span data-ttu-id="7deb7-129">Version BotBuilder</span><span class="sxs-lookup"><span data-stu-id="7deb7-129">BotBuilder version</span></span> | <span data-ttu-id="7deb7-130">Démontre</span><span class="sxs-lookup"><span data-stu-id="7deb7-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="7deb7-131">**Authentification** bot [en échantillon cs-auth][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="7deb7-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="7deb7-132">v4 (en)</span><span class="sxs-lookup"><span data-stu-id="7deb7-132">v4</span></span> | <span data-ttu-id="7deb7-133">Support OAuthCard</span><span class="sxs-lookup"><span data-stu-id="7deb7-133">OAuthCard support</span></span> |
    | <span data-ttu-id="7deb7-134">**Authentification** bot [en js-auth-sample][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="7deb7-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="7deb7-135">v4 (en)</span><span class="sxs-lookup"><span data-stu-id="7deb7-135">v4</span></span>| <span data-ttu-id="7deb7-136">Support OAuthCard</span><span class="sxs-lookup"><span data-stu-id="7deb7-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="7deb7-137">**Authentification** bot [en py-auth-sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="7deb7-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="7deb7-138">v4 (en)</span><span class="sxs-lookup"><span data-stu-id="7deb7-138">v4</span></span> | <span data-ttu-id="7deb7-139">Support OAuthCard</span><span class="sxs-lookup"><span data-stu-id="7deb7-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="7deb7-140">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7deb7-140">Create the resource group</span></span>

<span data-ttu-id="7deb7-141">Le groupe de ressources et le plan de service ne sont pas strictement nécessaires, mais ils vous permettent de libérer facilement les ressources que vous créez.</span><span class="sxs-lookup"><span data-stu-id="7deb7-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="7deb7-142">C’est une bonne pratique pour garder vos ressources organisées et gérables.</span><span class="sxs-lookup"><span data-stu-id="7deb7-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="7deb7-143">Vous utilisez un groupe de ressources pour créer des ressources individuelles pour le Cadre Bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="7deb7-144">Pour des performances, assurez-vous que ces ressources sont situées dans la même région Azure.</span><span class="sxs-lookup"><span data-stu-id="7deb7-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="7deb7-145">Dans votre navigateur, connectez-vous [**au portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7deb7-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="7deb7-146">Dans le panneau de navigation gauche, sélectionnez **Groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="7deb7-147">En haut à gauche de la fenêtre affichée, sélectionnez **Ajouter l’onglet** pour créer un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7deb7-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="7deb7-148">Vous serez invité à fournir les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7deb7-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="7deb7-149">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-149">**Subscription**.</span></span> <span data-ttu-id="7deb7-150">Utilisez votre abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="7deb7-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="7deb7-151">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-151">**Resource group**.</span></span> <span data-ttu-id="7deb7-152">Entrez le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7deb7-152">Enter the name for the resource group.</span></span> <span data-ttu-id="7deb7-153">Un exemple pourrait être  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="7deb7-154">Rappelez-vous que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="7deb7-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="7deb7-155">Dans le menu **de** drop-down de la Région, *sélectionnez West US* ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="7deb7-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="7deb7-156">Sélectionnez **l’examen et créez** le bouton.</span><span class="sxs-lookup"><span data-stu-id="7deb7-156">Select the **Review and create** button.</span></span> <span data-ttu-id="7deb7-157">Vous devriez voir une bannière qui se lit *validation passé*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="7deb7-158">Sélectionnez **le bouton** Créer.</span><span class="sxs-lookup"><span data-stu-id="7deb7-158">Select the **Create** button.</span></span> <span data-ttu-id="7deb7-159">La création du groupe de ressources peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7deb7-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="7deb7-160">Comme avec les ressources que vous allez créer plus tard dans ce tutoriel, c’est une bonne idée d’épingler ce groupe de ressources à votre tableau de bord pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="7deb7-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="7deb7-161">Si vous souhaitez le faire, sélectionnez l’icône de goupille &#128204; en haut à droite du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="7deb7-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="7deb7-162">Créer le plan de service</span><span class="sxs-lookup"><span data-stu-id="7deb7-162">Create the service plan</span></span>

1. <span data-ttu-id="7deb7-163">Dans le [**portail Azure**][azure-portal], sur le panneau de navigation gauche, **sélectionnez Créer une ressource**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="7deb7-164">Dans la boîte de recherche, tapez *App Service Plan*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="7deb7-165">Sélectionnez la **carte App Service Plan** à partir des résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="7deb7-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="7deb7-166">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-166">Select **Create**.</span></span>
1. <span data-ttu-id="7deb7-167">Il vous sera demandé de fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7deb7-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="7deb7-168">**Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-168">**Subscription**.</span></span> <span data-ttu-id="7deb7-169">Vous pouvez utiliser un abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="7deb7-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="7deb7-170">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-170">**Resource Group**.</span></span> <span data-ttu-id="7deb7-171">Sélectionnez le groupe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="7deb7-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="7deb7-172">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-172">**Name**.</span></span> <span data-ttu-id="7deb7-173">Entrez le nom du plan de service.</span><span class="sxs-lookup"><span data-stu-id="7deb7-173">Enter the name for the service plan.</span></span> <span data-ttu-id="7deb7-174">Un exemple pourrait être  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="7deb7-175">Rappelez-vous que le nom doit être unique, au sein du groupe.</span><span class="sxs-lookup"><span data-stu-id="7deb7-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="7deb7-176">**Système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-176">**Operating System**.</span></span> <span data-ttu-id="7deb7-177">Sélectionnez *Windows* ou votre système d’exploitation applicable.</span><span class="sxs-lookup"><span data-stu-id="7deb7-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="7deb7-178">**Région**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-178">**Region**.</span></span> <span data-ttu-id="7deb7-179">Sélectionnez *West US* ou une région proche de vos applications.</span><span class="sxs-lookup"><span data-stu-id="7deb7-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="7deb7-180">**Niveau de tarification**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-180">**Pricing Tier**.</span></span> <span data-ttu-id="7deb7-181">Assurez-vous *que standard S1* est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="7deb7-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="7deb7-182">Il devrait s’agir de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="7deb7-182">This should be the default value.</span></span>
    1. <span data-ttu-id="7deb7-183">Sélectionnez **l’examen et créez** le bouton.</span><span class="sxs-lookup"><span data-stu-id="7deb7-183">Select the **Review and create** button.</span></span> <span data-ttu-id="7deb7-184">Vous devriez voir une bannière qui se lit *validation passé*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="7deb7-185">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-185">Select **Create**.</span></span> <span data-ttu-id="7deb7-186">La création du plan de service de l’application peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7deb7-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="7deb7-187">Le plan sera inscrit dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7deb7-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="7deb7-188">Créer l’enregistrement des canaux bot</span><span class="sxs-lookup"><span data-stu-id="7deb7-188">Create the bot channels registration</span></span>

<span data-ttu-id="7deb7-189">L’enregistrement des canaux bot enregistre votre service Web en tant que bot avec le Cadre Bot, à condition d’avoir un identifiant d’application Microsoft et un mot de passe app (secret client).</span><span class="sxs-lookup"><span data-stu-id="7deb7-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7deb7-190">Vous n’avez besoin d’enregistrer votre bot que s’il n’est pas hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7deb7-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="7deb7-191">Si vous [avez créé un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) via le portail Azure, il est déjà enregistré auprès du service.</span><span class="sxs-lookup"><span data-stu-id="7deb7-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="7deb7-192">Si vous avez créé votre bot via le [Bot Framework](https://dev.botframework.com/bots/new) ou [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) votre bot n’est pas enregistré sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7deb7-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="7deb7-193">La ressource d’enregistrement bot channels affichera la région **mondiale même** si vous avez sélectionné West US.</span><span class="sxs-lookup"><span data-stu-id="7deb7-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="7deb7-194">Ceci est normal.</span><span class="sxs-lookup"><span data-stu-id="7deb7-194">This is expected.</span></span>

<span data-ttu-id="7deb7-195">Pour plus d’informations, [voir Créer un bot pour Teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="7deb7-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="7deb7-196">Créer le fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="7deb7-196">Create the identity provider</span></span>

<span data-ttu-id="7deb7-197">Vous avez besoin d’un fournisseur d’identité qui peut être utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7deb7-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="7deb7-198">Dans cette procédure, vous utiliserez un fournisseur d’ANNONCE Azure ; d’autres fournisseurs d’identité pris en charge par Azure AD peuvent également être utilisés.</span><span class="sxs-lookup"><span data-stu-id="7deb7-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="7deb7-199">Dans le [**portail Azure**][azure-portal], sur le panneau de navigation gauche, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="7deb7-200">Vous devrez créer et enregistrer cette ressource Azure AD dans un locataire dans lequel vous pouvez consentir à déléguer les autorisations demandées par une application.</span><span class="sxs-lookup"><span data-stu-id="7deb7-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="7deb7-201">Pour obtenir des instructions sur la création d’un locataire, [consultez Accéder au portail et créer un locataire.](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)</span><span class="sxs-lookup"><span data-stu-id="7deb7-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="7deb7-202">Dans le panneau gauche, sélectionnez **les enregistrements app**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="7deb7-203">Dans le panneau de droite, sélectionnez le **nouvel onglet** d’enregistrement, en haut à gauche.</span><span class="sxs-lookup"><span data-stu-id="7deb7-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="7deb7-204">Il vous sera demandé de fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7deb7-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="7deb7-205">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-205">**Name**.</span></span> <span data-ttu-id="7deb7-206">Entrez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="7deb7-206">Enter the name for the application.</span></span> <span data-ttu-id="7deb7-207">Un exemple pourrait être  *BotTeamsIdentity*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="7deb7-208">Rappelez-vous que le nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="7deb7-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="7deb7-209">Sélectionnez les **types de compte pris en** charge pour votre application.</span><span class="sxs-lookup"><span data-stu-id="7deb7-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="7deb7-210">Sélectionnez *les comptes dans n’importe quel répertoire organisationnel (Tout répertoire Azure AD - Multitenant) et les comptes Microsoft personnels (par exemple Skype, Xbox).*</span><span class="sxs-lookup"><span data-stu-id="7deb7-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="7deb7-211">Pour **l’URI Redirect**:</span><span class="sxs-lookup"><span data-stu-id="7deb7-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="7deb7-212">&#x2713;Select **Web**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="7deb7-213">&#x2713; définir l’URL à `https://token.botframework.com/.auth/web/redirect` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="7deb7-214">Sélectionnez **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-214">Select **Register**.</span></span>

1. <span data-ttu-id="7deb7-215">Une fois qu’il est créé, Azure affiche la page **Vue d’ensemble** de l’application.</span><span class="sxs-lookup"><span data-stu-id="7deb7-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="7deb7-216">Copiez et enregistrez les informations suivantes dans un fichier :</span><span class="sxs-lookup"><span data-stu-id="7deb7-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="7deb7-217">La valeur **d’identification de l’application (client).**</span><span class="sxs-lookup"><span data-stu-id="7deb7-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="7deb7-218">Vous utiliserez cette valeur plus tard comme identifiant *client lorsque vous* enregistrerez cette application d’identité Azure avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="7deb7-219">La **valeur d’identification de l’annuaire (locataire).**</span><span class="sxs-lookup"><span data-stu-id="7deb7-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="7deb7-220">Vous utiliserez également cette valeur plus tard en tant *qu’identifiant locataire* pour enregistrer cette application d’identité Azure avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="7deb7-221">Dans le panneau gauche, sélectionnez **certificats & secrets** pour créer un secret client pour votre application.</span><span class="sxs-lookup"><span data-stu-id="7deb7-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="7deb7-222">Sous **secrets clients**, sélectionnez &#x2795; nouveau secret **client**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="7deb7-223">Ajoutez une description pour identifier ce secret à partir d’autres que vous devrez peut-être créer pour cette application, comme *l’application d’identité Bot dans Teams*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="7deb7-224">**L’ensemble expire** à votre sélection.</span><span class="sxs-lookup"><span data-stu-id="7deb7-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="7deb7-225">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-225">Select **Add**.</span></span>
   1. <span data-ttu-id="7deb7-226">Avant de quitter cette page, **enregistrez le secret**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="7deb7-227">Vous utiliserez cette valeur plus tard comme _secret client lorsque_ vous enregistrerez votre application Azure AD avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="7deb7-228">Configurez la connexion du fournisseur d’identité et enregistrez-la avec le bot</span><span class="sxs-lookup"><span data-stu-id="7deb7-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="7deb7-229">Notez qu’il existe deux options pour les fournisseurs de services ici-Azure AD V1 et Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="7deb7-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="7deb7-230">Les différences entre les deux fournisseurs sont résumées ici, [mais](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)en général, V2 offre plus de flexibilité en ce qui concerne la modification des autorisations de bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-230">The differences between the two providers are summarized [here](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="7deb7-231">Graph Les autorisations api sont répertoriées dans le champ de portée, et au fur et à mesure que de nouvelles autorisations sont ajoutées, les bots permettront aux utilisateurs de consentir aux nouvelles autorisations lors de la prochaine inscription.</span><span class="sxs-lookup"><span data-stu-id="7deb7-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="7deb7-232">Pour V1, le consentement du bot doit être supprimé par l’utilisateur pour que de nouvelles autorisations soient incitées dans le dialogue OAuth.</span><span class="sxs-lookup"><span data-stu-id="7deb7-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="7deb7-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="7deb7-233">Azure AD V1</span></span>

1. <span data-ttu-id="7deb7-234">Dans le portail [**Azure,**][azure-portal]sélectionnez votre groupe de ressources à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="7deb7-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="7deb7-235">Sélectionnez votre lien d’enregistrement de canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="7deb7-236">Ouvrez la page de ressources et **sélectionnez Configuration** **sous Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-236">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="7deb7-237">Sélectionnez **Ajouter OAuth Connection Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-237">Select **Add OAuth Connection Settings**.</span></span>    
<span data-ttu-id="7deb7-238">L’image suivante affiche la sélection correspondante dans la page de ressources :</span><span class="sxs-lookup"><span data-stu-id="7deb7-238">The following image displays the corresponding selection in the resource page:</span></span>  
<span data-ttu-id="7deb7-239">![Configuration SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="7deb7-239">![SampleAppDemoBot configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span>
1. <span data-ttu-id="7deb7-240">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="7deb7-240">Complete the form as follows:</span></span>

    1. <span data-ttu-id="7deb7-241">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-241">**Name**.</span></span> <span data-ttu-id="7deb7-242">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="7deb7-242">Enter a name for the connection.</span></span> <span data-ttu-id="7deb7-243">Vous utiliserez ce nom dans votre bot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="7deb7-243">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="7deb7-244">Par exemple *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-244">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="7deb7-245">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-245">**Service Provider**.</span></span> <span data-ttu-id="7deb7-246">Sélectionner **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-246">Select **Azure Active Directory**.</span></span> <span data-ttu-id="7deb7-247">Une fois que vous sélectionnez ceci, les champs azuréens spécifiques à la MA s’affichent.</span><span class="sxs-lookup"><span data-stu-id="7deb7-247">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="7deb7-248">**Id client**. Entrez l’iD d’application (client) que vous avez enregistré pour votre application fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7deb7-248">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="7deb7-249">**Secret client**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-249">**Client secret**.</span></span> <span data-ttu-id="7deb7-250">Entrez le secret que vous avez enregistré pour votre application fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7deb7-250">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="7deb7-251">**Type de subvention**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-251">**Grant Type**.</span></span> <span data-ttu-id="7deb7-252">Entrez `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-252">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="7deb7-253">**URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-253">**Login URL**.</span></span> <span data-ttu-id="7deb7-254">Entrez `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-254">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="7deb7-255">**Identifiant locataire**, entrez **l’IDENTIFIANT d’annuaire (locataire) que vous** avez enregistré précédemment pour votre application d’identité Azure ou commun **en** fonction du type de compte pris en charge sélectionné lors de la création de l’application fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="7deb7-255">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="7deb7-256">Pour décider quelle valeur attribuer, suivez les critères suivants :</span><span class="sxs-lookup"><span data-stu-id="7deb7-256">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="7deb7-257">Si vous avez sélectionné soit les comptes de cet *annuaire organisationnel uniquement (Microsoft uniquement - locataire unique)* ou *les comptes dans n’importe quel répertoire organisationnel (répertoire Microsoft AAD - Multi locataire) entrez l’identifiant* de locataire que **vous** avez enregistré précédemment pour l’application AAD.</span><span class="sxs-lookup"><span data-stu-id="7deb7-257">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="7deb7-258">Ce sera le locataire associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="7deb7-258">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="7deb7-259">Si vous avez sélectionné *des comptes dans n’importe quel répertoire organisationnel (tout répertoire AAD - Compte Microsoft multi locataire et personnel par exemple Skype, Xbox, Outlook) entrez* le mot **commun au lieu d’un** identifiant de locataire.</span><span class="sxs-lookup"><span data-stu-id="7deb7-259">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="7deb7-260">Dans le cas contraire, l’application AAD vérifiera par l’intermédiaire du locataire dont l’iD a été sélectionné et exclura les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="7deb7-260">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="7deb7-261">h.</span><span class="sxs-lookup"><span data-stu-id="7deb7-261">h.</span></span> <span data-ttu-id="7deb7-262">Pour **l’URL de** ressource, entrez `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-262">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="7deb7-263">Ceci n’est pas utilisé dans l’échantillon de code actuel.</span><span class="sxs-lookup"><span data-stu-id="7deb7-263">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="7deb7-264">i.</span><span class="sxs-lookup"><span data-stu-id="7deb7-264">i.</span></span> <span data-ttu-id="7deb7-265">Laissez **les portées** vides.</span><span class="sxs-lookup"><span data-stu-id="7deb7-265">Leave **Scopes** blank.</span></span> <span data-ttu-id="7deb7-266">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="7deb7-266">The following image is an example:</span></span>

    ![équipes bots app auth connection string adv1 view](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="7deb7-268">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-268">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="7deb7-269">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="7deb7-269">Azure AD V2</span></span>

1. <span data-ttu-id="7deb7-270">Dans le portail [**Azure,**][azure-portal]sélectionnez votre groupe de ressources à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="7deb7-270">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="7deb7-271">Sélectionnez votre lien d’enregistrement de canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-271">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="7deb7-272">Ouvrez la page de ressources et **sélectionnez Configuration** **sous Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-272">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="7deb7-273">Sélectionnez **Ajouter OAuth Connection Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-273">Select **Add OAuth Connection Settings**.</span></span>  
<span data-ttu-id="7deb7-274">L’image suivante affiche la sélection correspondante dans la page de ressources :</span><span class="sxs-lookup"><span data-stu-id="7deb7-274">The following image displays the corresponding selection in the resource page:</span></span>        
<span data-ttu-id="7deb7-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="7deb7-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span> 

1. <span data-ttu-id="7deb7-276">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="7deb7-276">Complete the form as follows:</span></span>

    1. <span data-ttu-id="7deb7-277">**Nom**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-277">**Name**.</span></span> <span data-ttu-id="7deb7-278">Entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="7deb7-278">Enter a name for the connection.</span></span> <span data-ttu-id="7deb7-279">Vous utiliserez ce nom dans votre bot dans le `appsettings.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="7deb7-279">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="7deb7-280">Par exemple *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-280">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="7deb7-281">**Fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-281">**Service Provider**.</span></span> <span data-ttu-id="7deb7-282">Sélectionnez **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-282">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="7deb7-283">Une fois que vous sélectionnez ceci, les champs azuréens spécifiques à la MA s’affichent.</span><span class="sxs-lookup"><span data-stu-id="7deb7-283">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="7deb7-284">**Id client**. Entrez l’iD d’application (client) que vous avez enregistré pour votre application fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7deb7-284">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="7deb7-285">**Secret client**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-285">**Client secret**.</span></span> <span data-ttu-id="7deb7-286">Entrez le secret que vous avez enregistré pour votre application fournisseur d’identité Azure dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7deb7-286">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="7deb7-287">**URL de Exchange jetons**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-287">**Token Exchange URL**.</span></span> <span data-ttu-id="7deb7-288">Laisse ce vide.</span><span class="sxs-lookup"><span data-stu-id="7deb7-288">Leave this blank.</span></span>
    1. <span data-ttu-id="7deb7-289">**Identifiant locataire**, entrez **l’IDENTIFIANT d’annuaire (locataire) que vous** avez enregistré précédemment pour votre application d’identité Azure ou commun **en** fonction du type de compte pris en charge sélectionné lors de la création de l’application fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="7deb7-289">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="7deb7-290">Pour décider quelle valeur attribuer, suivez les critères suivants :</span><span class="sxs-lookup"><span data-stu-id="7deb7-290">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="7deb7-291">Si vous avez sélectionné soit les comptes de cet *annuaire organisationnel uniquement (Microsoft uniquement - locataire unique)* ou *les comptes dans n’importe quel répertoire organisationnel (répertoire Microsoft AAD - Multi locataire) entrez l’identifiant* de locataire que **vous** avez enregistré précédemment pour l’application AAD.</span><span class="sxs-lookup"><span data-stu-id="7deb7-291">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="7deb7-292">Ce sera le locataire associé aux utilisateurs qui peuvent être authentifiés.</span><span class="sxs-lookup"><span data-stu-id="7deb7-292">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="7deb7-293">Si vous avez sélectionné *des comptes dans n’importe quel répertoire organisationnel (tout répertoire AAD - Compte Microsoft multi locataire et personnel par exemple Skype, Xbox, Outlook) entrez* le mot **commun au lieu d’un** identifiant de locataire.</span><span class="sxs-lookup"><span data-stu-id="7deb7-293">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="7deb7-294">Dans le cas contraire, l’application AAD vérifiera par l’intermédiaire du locataire dont l’iD a été sélectionné et exclura les comptes Microsoft personnels.</span><span class="sxs-lookup"><span data-stu-id="7deb7-294">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="7deb7-295">Pour **scopes**, entrez une liste délimitée dans l’espace des autorisations graphiques de cette application nécessite par exemple: User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="7deb7-295">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="7deb7-296">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-296">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="7deb7-297">Testez la connexion</span><span class="sxs-lookup"><span data-stu-id="7deb7-297">Test the connection</span></span>

1. <span data-ttu-id="7deb7-298">Sélectionnez l’entrée de connexion pour ouvrir la connexion que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="7deb7-298">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="7deb7-299">Sélectionnez **Connexion de** test en haut du panneau de **réglage de connexion fournisseur de** services.</span><span class="sxs-lookup"><span data-stu-id="7deb7-299">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="7deb7-300">La première fois que vous faites cela ouvrira une nouvelle fenêtre de navigateur vous demandant de sélectionner un compte.</span><span class="sxs-lookup"><span data-stu-id="7deb7-300">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="7deb7-301">Sélectionnez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="7deb7-301">Select the one you want to use.</span></span>
1. <span data-ttu-id="7deb7-302">Ensuite, il vous sera demandé de permettre au fournisseur d’identité d’utiliser vos données (informations d’identification).</span><span class="sxs-lookup"><span data-stu-id="7deb7-302">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="7deb7-303">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="7deb7-303">The following image is an example:</span></span>

    ![équipes bot auth connection string adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="7deb7-305">Sélectionnez **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-305">Select **Accept**.</span></span>
1. <span data-ttu-id="7deb7-306">Cela devrait ensuite vous rediriger vers une connexion de test à la page **\<your-connection-name> Succeeded.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-306">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="7deb7-307">Actualisez la page si vous obtenez une erreur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-307">Refresh the page if you get an error.</span></span> <span data-ttu-id="7deb7-308">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="7deb7-308">The following image is an example:</span></span>

    ![équipes bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="7deb7-310">Le nom de connexion est utilisé par le code bot pour récupérer les jetons d’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-310">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="7deb7-311">Préparer le code d’échantillon bot</span><span class="sxs-lookup"><span data-stu-id="7deb7-311">Prepare the bot sample code</span></span>

<span data-ttu-id="7deb7-312">Avec les paramètres préliminaires faits, nous allons nous concentrer sur la création du bot à utiliser dans cet article.</span><span class="sxs-lookup"><span data-stu-id="7deb7-312">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7deb7-313">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7deb7-313">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="7deb7-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="7deb7-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="7deb7-315">Lancez-Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7deb7-315">Launch Visual Studio.</span></span>
1. <span data-ttu-id="7deb7-316">À partir de la barre **d’outils sélectionnez Fichier -> Open -> Project/Solution** et ouvrez le projet bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-316">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="7deb7-317">Dans C# Update **appsettings.jssur** comme suit:</span><span class="sxs-lookup"><span data-stu-id="7deb7-317">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="7deb7-318">Définissez `ConnectionName` le nom de la connexion fournisseur d’identité que vous avez ajoutée à l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-318">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="7deb7-319">Le nom que nous avons utilisé dans cet exemple *est BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-319">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="7deb7-320">Définissez `MicrosoftAppId` sur **l’id d’application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-320">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="7deb7-321">Définissez `MicrosoftAppPassword` le secret client **que** vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-321">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="7deb7-322">Selon les caractères de votre secret bot, vous devrez peut-être XML échapper au mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7deb7-322">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="7deb7-323">Par exemple, tous les ampersands (&) devront être codés comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-323">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="7deb7-324">Dans le Solution Explorer, accédez au `TeamsAppManifest` dossier, ouvrez `manifest.json` et définissez `id` et vers `botId` **l’ID d’application bot que** vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-324">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="7deb7-325">JavaScript</span><span class="sxs-lookup"><span data-stu-id="7deb7-325">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="7deb7-326">Clone [nœud-auth-échantillon][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="7deb7-326">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="7deb7-327">Dans une console, accédez au projet :</span><span class="sxs-lookup"><span data-stu-id="7deb7-327">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="7deb7-328">Installer des modules</span><span class="sxs-lookup"><span data-stu-id="7deb7-328">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="7deb7-329">Mettez à jour la configuration **.env** comme suit :</span><span class="sxs-lookup"><span data-stu-id="7deb7-329">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="7deb7-330">Définissez `MicrosoftAppId` sur **l’id d’application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-330">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="7deb7-331">Définissez `MicrosoftAppPassword` le secret client **que** vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-331">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="7deb7-332">Définissez le `connectionName` nom de la connexion du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="7deb7-332">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="7deb7-333">Selon les caractères de votre secret bot, vous devrez peut-être XML échapper au mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7deb7-333">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="7deb7-334">Par exemple, tous les ampersands (&) devront être codés comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-334">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="7deb7-335">Dans le `teamsAppManifest` dossier, ouvrez `manifest.json` et définissez `id`  votre identifiant **d’application Microsoft et** `botId` **l’identifiant d’application bot que** vous avez enregistré au moment de l’enregistrement du canal bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-335">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="7deb7-336">Python</span><span class="sxs-lookup"><span data-stu-id="7deb7-336">Python</span></span>](#tab/python)

1. <span data-ttu-id="7deb7-337">Clone [py-auth-sample][teams-auth-bot-py] du dépôt github.</span><span class="sxs-lookup"><span data-stu-id="7deb7-337">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="7deb7-338">Mise à **config.py**:</span><span class="sxs-lookup"><span data-stu-id="7deb7-338">Update **config.py**:</span></span>

    - <span data-ttu-id="7deb7-339">Définissez `ConnectionName` le nom du paramètre de connexion OAuth que vous avez ajouté à votre bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-339">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="7deb7-340">Définissez `MicrosoftAppId` et `MicrosoftAppPassword` vers l’iD de l’application de votre bot et le secret de l’application.</span><span class="sxs-lookup"><span data-stu-id="7deb7-340">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="7deb7-341">Selon les caractères de votre secret bot, vous devrez peut-être XML échapper au mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7deb7-341">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="7deb7-342">Par exemple, tous les ampersands (&) devront être codés comme `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-342">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="7deb7-343">Déployer le bot sur Azure</span><span class="sxs-lookup"><span data-stu-id="7deb7-343">Deploy the bot to Azure</span></span>

<span data-ttu-id="7deb7-344">Pour déployer le bot, suivez les étapes dans la façon de [déployer votre bot sur Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="7deb7-344">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="7deb7-345">Alternativement, pendant Visual Studio, vous pouvez suivre ces étapes :</span><span class="sxs-lookup"><span data-stu-id="7deb7-345">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="7deb7-346">Dans Visual Studio *Solution Explorer sélectionnez* et maintenez (ou cliquez à droite) le nom du projet.</span><span class="sxs-lookup"><span data-stu-id="7deb7-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="7deb7-347">Dans le menu drop-down, sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-347">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="7deb7-348">Dans la fenêtre affichée, sélectionnez le **nouveau** lien.</span><span class="sxs-lookup"><span data-stu-id="7deb7-348">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="7deb7-349">Dans la fenêtre de dialogue, **sélectionnez App Service** à gauche et **Créez nouveau** à droite.</span><span class="sxs-lookup"><span data-stu-id="7deb7-349">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="7deb7-350">Sélectionnez **le bouton** Publier.</span><span class="sxs-lookup"><span data-stu-id="7deb7-350">Select the **Publish** button.</span></span>
1. <span data-ttu-id="7deb7-351">Dans la fenêtre de dialogue suivante, entrez les informations requises.</span><span class="sxs-lookup"><span data-stu-id="7deb7-351">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="7deb7-352">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="7deb7-352">The following is an example:</span></span>

    ![service auth-app](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="7deb7-354">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-354">Select **Create**.</span></span>
1. <span data-ttu-id="7deb7-355">Si le déploiement se termine avec succès, vous devez le voir reflété dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7deb7-355">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="7deb7-356">En outre, une page est affichée dans votre navigateur par défaut en disant *que votre bot est prêt!*.</span><span class="sxs-lookup"><span data-stu-id="7deb7-356">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="7deb7-357">L’URL sera similaire à ceci: `https://botteamsauth.azurewebsites.net/` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-357">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="7deb7-358">Enregistrez-le dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="7deb7-358">Save it to a file.</span></span>
1. <span data-ttu-id="7deb7-359">Dans votre navigateur, accédez [**au portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7deb7-359">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="7deb7-360">Vérifiez votre groupe de ressources, le bot doit être répertorié avec les autres ressources.</span><span class="sxs-lookup"><span data-stu-id="7deb7-360">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="7deb7-361">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="7deb7-361">The following image is an example:</span></span>

    ![équipes-bot-auth-app-service-groupe](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="7deb7-363">Dans le groupe de ressources, sélectionnez le nom d’enregistrement du canal bot (lien).</span><span class="sxs-lookup"><span data-stu-id="7deb7-363">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="7deb7-364">Dans le panneau gauche, sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-364">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="7deb7-365">Dans la boîte **de point de terminaison** messagerie, entrez l’URL obtenue ci-dessus suivie de `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-365">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="7deb7-366">C’est un exemple: `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-366">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="7deb7-367">Sélectionnez le bouton **Enregistrer** en haut à gauche.</span><span class="sxs-lookup"><span data-stu-id="7deb7-367">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="7deb7-368">Testez le bot à l’aide de l’émulateur</span><span class="sxs-lookup"><span data-stu-id="7deb7-368">Test the bot using the Emulator</span></span>

<span data-ttu-id="7deb7-369">Si vous ne l’avez pas déjà fait, installez [le Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="7deb7-369">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="7deb7-370">Voir aussi [Debug avec l’Émulateur](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="7deb7-370">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="7deb7-371">Pour que l’échantillon de bot fonctionne, vous devez configurer l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-371">In order for the bot sample login to work you must configure the Emulator.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="7deb7-372">Configurer l’émulateur pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="7deb7-372">Configure the Emulator for authentication</span></span>

<span data-ttu-id="7deb7-373">Si un bot nécessite une authentification, vous devez configurer l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-373">If a bot requires authentication, you must configure the Emulator.</span></span> <span data-ttu-id="7deb7-374">Pour configurer :</span><span class="sxs-lookup"><span data-stu-id="7deb7-374">To configure:</span></span>

1. <span data-ttu-id="7deb7-375">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-375">Start the Emulator.</span></span>
1. <span data-ttu-id="7deb7-376">Dans l’émulateur, sélectionnez l’icône de vitesse &#9881; en bas à gauche, **ou l’émulateur Paramètres** onglet en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="7deb7-376">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="7deb7-377">Cochez la case **par utilisez les jetons d’authentification de la version 1.0**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-377">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="7deb7-378">Entrez le chemin local vers **l’outil ngrok.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-378">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="7deb7-379">*Voir* le Bot Framework Emulator / ngrok tunneling intégration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span><span class="sxs-lookup"><span data-stu-id="7deb7-379">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="7deb7-380">Pour plus d’informations sur les outils, [voir ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="7deb7-380">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="7deb7-381">Cochez la **case par Run ngrok lorsque l’émulateur démarre.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-381">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="7deb7-382">Sélectionnez **le bouton Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-382">Select the **Save** button.</span></span>

<span data-ttu-id="7deb7-383">Lorsque le bot affiche une carte de connectement et que l’utilisateur sélectionne le bouton de dédonnement, l’émulateur ouvre une page que l’utilisateur peut utiliser pour se connecter avec le fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="7deb7-383">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="7deb7-384">Une fois que l’utilisateur le fait, le fournisseur génère un jeton utilisateur et l’envoie au bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-384">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="7deb7-385">Après cela, le bot peut agir au nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-385">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="7deb7-386">Testez le bot localement</span><span class="sxs-lookup"><span data-stu-id="7deb7-386">Test the bot locally</span></span>

<span data-ttu-id="7deb7-387">Une fois que vous avez configuré le mécanisme d’authentification, vous pouvez effectuer les tests de bot réels.</span><span class="sxs-lookup"><span data-stu-id="7deb7-387">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="7deb7-388">Exécutez l’échantillon de bot localement sur votre machine, via Visual Studio par exemple.</span><span class="sxs-lookup"><span data-stu-id="7deb7-388">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="7deb7-389">Démarrez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-389">Start the Emulator.</span></span>
1. <span data-ttu-id="7deb7-390">Sélectionnez **le bouton Open bot.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-390">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="7deb7-391">Dans **l’URL Bot**, entrez l’URL locale du bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-391">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="7deb7-392">Habituellement, `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-392">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="7deb7-393">Dans **l’iD de l’application Microsoft,** entrez l’iD de l’application du bot à partir `appsettings.json` de .</span><span class="sxs-lookup"><span data-stu-id="7deb7-393">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="7deb7-394">Dans le mot **de passe microsoft app** entrez le mot de passe de l’application du bot à partir de la `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-394">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="7deb7-395">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-395">Select **Connect**.</span></span>
1. <span data-ttu-id="7deb7-396">Une fois le bot opérationnel, entrez n’importe quel texte pour afficher la carte de dédage.</span><span class="sxs-lookup"><span data-stu-id="7deb7-396">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="7deb7-397">Sélectionnez le bouton **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-397">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="7deb7-398">Un dialogue contexturé s’affiche pour confirmer **l’URL ouverte**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-398">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="7deb7-399">Il s’agit de permettre à l’utilisateur du bot (vous) d’être authentifié.</span><span class="sxs-lookup"><span data-stu-id="7deb7-399">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="7deb7-400">Sélectionner **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-400">Select **Confirm**.</span></span>
1. <span data-ttu-id="7deb7-401">Si on vous le demande, sélectionnez le compte de l’utilisateur applicable.</span><span class="sxs-lookup"><span data-stu-id="7deb7-401">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="7deb7-402">Selon la configuration que vous avez utilisée pour l’émulateur, vous obtenez l’une des configurations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7deb7-402">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="7deb7-403">**Utilisation du code de vérification de la dédontologie**</span><span class="sxs-lookup"><span data-stu-id="7deb7-403">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="7deb7-404">&#x2713; une fenêtre est ouverte affichant le code de validation.</span><span class="sxs-lookup"><span data-stu-id="7deb7-404">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="7deb7-405">&#x2713; copiez et entrez le code de validation dans la boîte de chat pour compléter l’inscription.</span><span class="sxs-lookup"><span data-stu-id="7deb7-405">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="7deb7-406">**Utilisation de jetons d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-406">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="7deb7-407">&#x2713; Vous êtes connecté en fonction de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7deb7-407">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="7deb7-408">L’image suivante est un exemple de l’interface utilisateur bot après que vous vous êtes connecté:</span><span class="sxs-lookup"><span data-stu-id="7deb7-408">The following image is an example of the bot UI after you've logged in:</span></span>

    ![émulateur de connexion auth bot](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="7deb7-410">Si vous **sélectionnez** Oui lorsque le bot *demande Souhaitez-vous afficher votre jeton?*, vous obtiendrez une réponse similaire à ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="7deb7-410">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![jetons émulateur de connexion bot auth](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="7deb7-412">Entrez **le logout** dans la boîte de chat d’entrée pour vous déduter. Cela libère le jeton utilisateur, et le bot ne sera pas en mesure d’agir en votre nom jusqu’à ce que vous vous connectez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="7deb7-412">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="7deb7-413">L’authentification bot nécessite **l’utilisation du service de connecteur Bot**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-413">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="7deb7-414">Le service accède aux informations d’enregistrement des canaux bot pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-414">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="7deb7-415">Testez le bot déployé</span><span class="sxs-lookup"><span data-stu-id="7deb7-415">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="7deb7-416">Dans votre navigateur, accédez [**au portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7deb7-416">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="7deb7-417">Trouvez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7deb7-417">Find your resource group.</span></span>
1. <span data-ttu-id="7deb7-418">Sélectionnez le lien de ressources.</span><span class="sxs-lookup"><span data-stu-id="7deb7-418">Select the resource link.</span></span> <span data-ttu-id="7deb7-419">La page de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7deb7-419">The resource page is displayed.</span></span>
1. <span data-ttu-id="7deb7-420">Dans la page de ressources, **sélectionnez Test in Web Chat**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-420">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="7deb7-421">Le bot démarre et affiche les salutations prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="7deb7-421">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="7deb7-422">Tapez n’importe quoi dans la boîte de chat.</span><span class="sxs-lookup"><span data-stu-id="7deb7-422">Type anything in the chat box.</span></span>
1. <span data-ttu-id="7deb7-423">Sélectionnez **le panneau dans la** boîte.</span><span class="sxs-lookup"><span data-stu-id="7deb7-423">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="7deb7-424">Un dialogue contexturé s’affiche pour confirmer **l’URL ouverte**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-424">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="7deb7-425">Il s’agit de permettre à l’utilisateur du bot (vous) d’être authentifié.</span><span class="sxs-lookup"><span data-stu-id="7deb7-425">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="7deb7-426">Sélectionner **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-426">Select **Confirm**.</span></span>
1. <span data-ttu-id="7deb7-427">Si on vous le demande, sélectionnez le compte de l’utilisateur applicable.</span><span class="sxs-lookup"><span data-stu-id="7deb7-427">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="7deb7-428">L’image suivante est un exemple de l’interface utilisateur bot après que vous vous êtes connecté:</span><span class="sxs-lookup"><span data-stu-id="7deb7-428">The following image is an example of the bot UI after you have logged in:</span></span>

    ![connexion bot auth déployé](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="7deb7-430">.</span><span class="sxs-lookup"><span data-stu-id="7deb7-430">.</span></span>

1. <span data-ttu-id="7deb7-431">Sélectionnez le **bouton Oui** pour afficher votre jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="7deb7-431">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="7deb7-432">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="7deb7-432">The following image is an example:</span></span>

    ![connexion bot auth déployé jeton](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="7deb7-434">.</span><span class="sxs-lookup"><span data-stu-id="7deb7-434">.</span></span>

1. <span data-ttu-id="7deb7-435">Entrez logout pour vous déduter.</span><span class="sxs-lookup"><span data-stu-id="7deb7-435">Enter logout to sign out.</span></span>

    ![auth bot déployé logout](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="7deb7-437">Si vous avez des problèmes de connexion, essayez de tester la connexion à nouveau comme décrit dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="7deb7-437">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="7deb7-438">Cela pourrait recréer le jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="7deb7-438">This could recreate the authentication token.</span></span>
> <span data-ttu-id="7deb7-439">Avec le client Bot Framework Web Chat dans Azure, vous devrez peut-être vous connecter plusieurs fois avant que l’authentification ne soit correctement établie.</span><span class="sxs-lookup"><span data-stu-id="7deb7-439">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="7deb7-440">Installez et testez le bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="7deb7-440">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="7deb7-441">Dans votre projet de bot, assurez-vous que `TeamsAppManifest` le dossier contient le long avec un et des `manifest.json` `outline.png` `color.png` fichiers.</span><span class="sxs-lookup"><span data-stu-id="7deb7-441">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="7deb7-442">Dans Solution Explorer, accédez au `TeamsAppManifest` dossier.</span><span class="sxs-lookup"><span data-stu-id="7deb7-442">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="7deb7-443">Modifier `manifest.json` en attribuant les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="7deb7-443">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="7deb7-444">Assurez-vous que **l’ID d’application bot** que vous avez reçu au moment de l’enregistrement du canal bot est attribué `id` à et `botId` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-444">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="7deb7-445">Attribuez cette valeur : `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-445">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="7deb7-446">Sélectionnez et **zip** le `manifest.json` , et les `outline.png` `color.png` fichiers.</span><span class="sxs-lookup"><span data-stu-id="7deb7-446">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="7deb7-447">Ouvrez **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-447">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="7deb7-448">Dans le panneau gauche, en bas, sélectionnez **l’icône Apps**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-448">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="7deb7-449">Dans le panneau droit, en bas, sélectionnez **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-449">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="7deb7-450">Naviguez dans `TeamsAppManifest` le dossier et téléchargez le manifeste zippé.</span><span class="sxs-lookup"><span data-stu-id="7deb7-450">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="7deb7-451">L’assistant suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="7deb7-451">The following wizard is displayed:</span></span>

    ![auth bot équipes télécharger](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="7deb7-453">Sélectionnez le bouton **Ajouter à une équipe**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-453">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="7deb7-454">Dans la fenêtre suivante, sélectionnez l’équipe où vous souhaitez utiliser le bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-454">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="7deb7-455">Sélectionnez **le bouton Configurer un bot.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-455">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="7deb7-456">Sélectionnez les trois points (&#x25cf;&#x25cf;&#x25cf;) dans le panneau gauche.</span><span class="sxs-lookup"><span data-stu-id="7deb7-456">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="7deb7-457">Sélectionnez ensuite **l’icône App Studio.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-457">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="7deb7-458">Sélectionnez **l’onglet Éditeur** Manifeste. Vous devriez voir l’icône pour le bot que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7deb7-458">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="7deb7-459">En outre, vous devriez être en mesure de voir le bot répertorié comme un contact dans la liste de chat que vous pouvez utiliser pour échanger des messages avec le bot.</span><span class="sxs-lookup"><span data-stu-id="7deb7-459">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="7deb7-460">Tester le bot localement dans Teams</span><span class="sxs-lookup"><span data-stu-id="7deb7-460">Testing the bot locally in Teams</span></span>

<span data-ttu-id="7deb7-461">Microsoft Teams est un produit entièrement basé sur le cloud, il nécessite tous les services qu’il accède pour être disponible à partir du cloud en utilisant les points de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7deb7-461">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="7deb7-462">Par conséquent, pour permettre au bot (notre échantillon) de fonctionner en Teams, vous devez soit publier le code sur le nuage de votre choix, soit rendre une instance localement en cours d’exécution accessible à l’extérieur via **un outil de tunneling.**</span><span class="sxs-lookup"><span data-stu-id="7deb7-462">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="7deb7-463">Nous recommandons  [ngrok](https://ngrok.com/download), qui crée une URL adressable extérieurement pour un port que vous ouvrez localement sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="7deb7-463">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="7deb7-464">Pour configurer ngrok en vue de l’exécution de votre application Microsoft Teams’application locale, suivez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7deb7-464">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="7deb7-465">Dans une fenêtre terminale, allez à l’annuaire où vous avez `ngrok.exe` installé.</span><span class="sxs-lookup"><span data-stu-id="7deb7-465">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="7deb7-466">Nous suggérons de définir *le chemin variable de* l’environnement pour le pointer vers elle.</span><span class="sxs-lookup"><span data-stu-id="7deb7-466">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="7deb7-467">Exécuter, par exemple, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-467">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="7deb7-468">Remplacez le numéro de port au besoin.</span><span class="sxs-lookup"><span data-stu-id="7deb7-468">Replace the port number as needed.</span></span>
<span data-ttu-id="7deb7-469">Cela lance ngrok pour écouter sur le port que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="7deb7-469">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="7deb7-470">En retour, il vous donne une URL adressable extérieurement, valide aussi longtemps que ngrok est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7deb7-470">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="7deb7-471">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="7deb7-471">The following image is an example:</span></span>

    ![équipes bot app auth connection string adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="7deb7-473">.</span><span class="sxs-lookup"><span data-stu-id="7deb7-473">.</span></span>

1. <span data-ttu-id="7deb7-474">Copiez l’adresse HTTPS de forwarding.</span><span class="sxs-lookup"><span data-stu-id="7deb7-474">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="7deb7-475">Il devrait être similaire à ce qui suit: `https://dea822bf.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-475">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="7deb7-476">Annexe à `/api/messages` obtenir `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-476">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="7deb7-477">Il s’agit **du point de terminaison** des messages pour le bot fonctionnant localement sur votre machine et accessible sur le Web dans un chat Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7deb7-477">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="7deb7-478">Une dernière étape à effectuer est de mettre à jour le point de terminaison des messages du bot déployé.</span><span class="sxs-lookup"><span data-stu-id="7deb7-478">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="7deb7-479">Dans l’exemple, nous avons déployé le bot dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7deb7-479">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="7deb7-480">Donc \*\*effectuons ces étapes :</span><span class="sxs-lookup"><span data-stu-id="7deb7-480">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="7deb7-481">Dans votre navigateur naviguer vers le [**portail Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7deb7-481">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="7deb7-482">Sélectionnez votre **inscription bot channel**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-482">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="7deb7-483">Dans le panneau gauche, sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-483">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="7deb7-484">Dans le panneau droit, dans la boîte **de point de terminaison** messagerie, entrez l’URL ngrok, dans notre exemple, `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="7deb7-484">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="7deb7-485">Démarrez votre bot localement, par exemple en mode Visual Studio débog.</span><span class="sxs-lookup"><span data-stu-id="7deb7-485">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="7deb7-486">Testez le bot tout en exécutant localement en utilisant le chat Web de test **du portail Bot** Framework .</span><span class="sxs-lookup"><span data-stu-id="7deb7-486">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="7deb7-487">Comme l’émulateur, ce test ne vous permet pas d’accéder Teams fonctionnalités spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7deb7-487">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="7deb7-488">Dans la fenêtre terminale `ngrok` où s’exécution, vous pouvez voir le trafic HTTP entre le bot et le client de chat web.</span><span class="sxs-lookup"><span data-stu-id="7deb7-488">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="7deb7-489">Si vous voulez une vue plus détaillée, dans une fenêtre de navigateur, entrez-vous `http://127.0.0.1:4040` obtenu à partir de la fenêtre terminale précédente.</span><span class="sxs-lookup"><span data-stu-id="7deb7-489">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="7deb7-490">L’image suivante est un exemple :</span><span class="sxs-lookup"><span data-stu-id="7deb7-490">The following image is an example:</span></span>

    ![auth bot équipes ngrok test](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="7deb7-492">.</span><span class="sxs-lookup"><span data-stu-id="7deb7-492">.</span></span>

> [!NOTE]
> <span data-ttu-id="7deb7-493">Si vous arrêtez et redémarrez ngrok, l’URL change.</span><span class="sxs-lookup"><span data-stu-id="7deb7-493">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="7deb7-494">Pour utiliser ngrok dans votre projet, et en fonction des fonctionnalités que vous utilisez, vous devez mettre à jour toutes les références URL.</span><span class="sxs-lookup"><span data-stu-id="7deb7-494">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="7deb7-495">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7deb7-495">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="7deb7-496">TeamsAppManifest/manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="7deb7-496">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="7deb7-497">Ce manifeste contient les informations dont Microsoft Teams pour se connecter avec le bot :</span><span class="sxs-lookup"><span data-stu-id="7deb7-497">This manifest contains information needed by Microsoft Teams to connect with the bot:</span></span>  

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

<span data-ttu-id="7deb7-498">Avec l’authentification, Teams se comporte légèrement différemment des autres canaux, comme expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7deb7-498">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="7deb7-499">Manipulation Invoquer l’activité</span><span class="sxs-lookup"><span data-stu-id="7deb7-499">Handling Invoke Activity</span></span>

<span data-ttu-id="7deb7-500">Une **activité Invocant** est envoyée au bot plutôt qu’à l’activité événementale utilisée par d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="7deb7-500">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="7deb7-501">Ceci est fait en sous-classant le **ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="7deb7-501">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7deb7-502">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7deb7-502">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="7deb7-503">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="7deb7-503">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="7deb7-504">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="7deb7-504">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="7deb7-505">*L’activité Invocation* doit être transmise au dialogue si **l’OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="7deb7-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="7deb7-506">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="7deb7-506">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="7deb7-507">JavaScript</span><span class="sxs-lookup"><span data-stu-id="7deb7-507">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="7deb7-508">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="7deb7-508">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="7deb7-509">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="7deb7-509">**bots/teamsBot.js**</span></span>

<span data-ttu-id="7deb7-510">*L’activité Invocation* doit être transmise au dialogue si **l’OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="7deb7-510">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="7deb7-511">**dialogues/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="7deb7-511">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="7deb7-512">Dans une étape de dialogue, utilisez `beginDialog` pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="7deb7-512">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="7deb7-513">Si l’utilisateur est déjà connecté, cela générera un événement de réponse symbolique, sans inciter l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-513">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="7deb7-514">Dans le cas contraire, cela incitera l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="7deb7-514">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="7deb7-515">Le service Azure Bot envoie l’événement de réponse symbolique après que l’utilisateur tente de se connecter.</span><span class="sxs-lookup"><span data-stu-id="7deb7-515">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="7deb7-516">Dans l’étape de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="7deb7-516">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="7deb7-517">Si ce n’est pas nul, l’utilisateur s’est connecté avec succès.</span><span class="sxs-lookup"><span data-stu-id="7deb7-517">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="7deb7-518">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="7deb7-518">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="7deb7-519">Python</span><span class="sxs-lookup"><span data-stu-id="7deb7-519">Python</span></span>](#tab/python-sample)

<span data-ttu-id="7deb7-520">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="7deb7-520">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="7deb7-521">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="7deb7-521">**bots/teams_bot.py**</span></span>

<span data-ttu-id="7deb7-522">*L’activité Invocation* doit être transmise au dialogue si **l’OAuthPrompt** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="7deb7-522">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="7deb7-523">**dialogues/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="7deb7-523">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="7deb7-524">Dans une étape de dialogue, utilisez `begin_dialog` pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="7deb7-524">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="7deb7-525">Si l’utilisateur est déjà connecté, cela générera un événement de réponse symbolique, sans inciter l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7deb7-525">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="7deb7-526">Dans le cas contraire, cela incitera l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="7deb7-526">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="7deb7-527">Le service Azure Bot envoie l’événement de réponse symbolique après que l’utilisateur tente de se connecter.</span><span class="sxs-lookup"><span data-stu-id="7deb7-527">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="7deb7-528">Dans l’étape de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="7deb7-528">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="7deb7-529">Si ce n’est pas nul, l’utilisateur s’est connecté avec succès.</span><span class="sxs-lookup"><span data-stu-id="7deb7-529">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="7deb7-530">**dialogues/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="7deb7-530">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a><span data-ttu-id="7deb7-531">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7deb7-531">See also</span></span>

[<span data-ttu-id="7deb7-532">Ajouter l’authentification via Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="7deb7-532">Add authentication through Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

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
