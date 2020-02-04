---
title: Préparer votre client Office 365
description: Prise en main de teams dans Office 365
keywords: Configurer le chargement des équipes client Office 365
ms.openlocfilehash: 62cd640196631f50c72762253ff1bd75a143337d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673902"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="6bb00-104">Préparer votre client Office 365</span><span class="sxs-lookup"><span data-stu-id="6bb00-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="6bb00-105">Pour développer des applications pour Microsoft Teams, vous devez être un [client Office 365 avec l’un des plans suivants](https://products.office.com/business/compare-more-office-365-for-business-plans).</span><span class="sxs-lookup"><span data-stu-id="6bb00-105">To develop apps for Microsoft Teams, you need to be an [Office 365 customer with one of the following plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>

* <span data-ttu-id="6bb00-106">Business Essentials</span><span class="sxs-lookup"><span data-stu-id="6bb00-106">Business Essentials</span></span>
* <span data-ttu-id="6bb00-107">Business Premium</span><span class="sxs-lookup"><span data-stu-id="6bb00-107">Business Premium</span></span>
* <span data-ttu-id="6bb00-108">Entreprise E1, E3 et E5</span><span class="sxs-lookup"><span data-stu-id="6bb00-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="6bb00-109">Développeur</span><span class="sxs-lookup"><span data-stu-id="6bb00-109">Developer</span></span>
* <span data-ttu-id="6bb00-110">Éducation, éducation plus et éducation E5</span><span class="sxs-lookup"><span data-stu-id="6bb00-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="6bb00-111">Microsoft teams est également disponible pour les clients qui ont acheté E4 avant sa retraite.</span><span class="sxs-lookup"><span data-stu-id="6bb00-111">Microsoft Teams will also be available to customers who purchased E4 prior to its retirement.</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="6bb00-112">Vous avez besoin d’un environnement de développement ?</span><span class="sxs-lookup"><span data-stu-id="6bb00-112">Just need a development environment?</span></span>

<span data-ttu-id="6bb00-113">Si vous ne disposez pas d’un compte Office 365, vous pouvez vous inscrire au [programme pour les développeurs office 365](https://dev.office.com/devprogram) pour obtenir un service *gratuit* 90 jours (vous pouvez le renouveler aussi longtemps que vous l’utilisez pour une activité de développement) client Office 365 développeur.</span><span class="sxs-lookup"><span data-stu-id="6bb00-113">If you don't currently have an Office 365 account, you can sign up for the [Office 365 Developer program](https://dev.office.com/devprogram) to get a *free* 90 days (can be renewed for as long as you're using it for development activity) Office 365 Developer Tenant.</span></span> <span data-ttu-id="6bb00-114">Ce compte peut uniquement être utilisé à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="6bb00-114">This account can only be used for testing purposes.</span></span> <span data-ttu-id="6bb00-115">Pour plus d’informations sur [la configuration de vos comptes de test](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="6bb00-115">See more information on [setting up your test accounts](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="6bb00-116">Activer Microsoft teams pour votre organisation</span><span class="sxs-lookup"><span data-stu-id="6bb00-116">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="6bb00-117">Si Microsoft teams n’est pas encore activé pour votre organisation, vous devez tout d’abord le faire.</span><span class="sxs-lookup"><span data-stu-id="6bb00-117">If Microsoft Teams is not yet enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="6bb00-118">Consultez nos conseils détaillés pour [l’activation de teams pour votre organisation](/microsoftteams/how-to-roll-out-teams).</span><span class="sxs-lookup"><span data-stu-id="6bb00-118">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/how-to-roll-out-teams).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="6bb00-119">Activer les applications de teams personnalisées et activer le téléchargement de l’application personnalisée</span><span class="sxs-lookup"><span data-stu-id="6bb00-119">Enable custom Teams apps and turn on custom app uploading</span></span>

> <span data-ttu-id="6bb00-120">Remarque : Si vous utilisez une organisation de développement O365 pour créer votre application, ces paramètres doivent déjà être configurés pour vous permettre de créer, de charger et de tester votre application.</span><span class="sxs-lookup"><span data-stu-id="6bb00-120">Note: If you're using an O365 Developer Organization to build your app, these settings should already be configured to allow you to build, upload and test your app.</span></span>

<span data-ttu-id="6bb00-121">Il y a trois paramètres impliqués dans l’activation des applications personnalisées et le téléchargement d’applications personnalisées :</span><span class="sxs-lookup"><span data-stu-id="6bb00-121">There are three settings involved in enabling custom apps and custom app uploading:</span></span>

* <span data-ttu-id="6bb00-122">**Paramètre de l’application personnalisée** à l’échelle de l’Organisation : ce paramètre active ou désactive les applications personnalisées pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="6bb00-122">**Org-wide custom app setting** - This setting either enables or disables custom apps for your organization.</span></span> <span data-ttu-id="6bb00-123">Il doit être activé.</span><span class="sxs-lookup"><span data-stu-id="6bb00-123">It needs to be on.</span></span> 
* <span data-ttu-id="6bb00-124">**Paramètre de l’application personnalisée d’équipe** : ce paramètre est pour chaque équipe individuelle dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6bb00-124">**Team custom app setting** - This setting is for each individual team inside Microsoft Teams.</span></span> <span data-ttu-id="6bb00-125">Si vous souhaitez installer votre application pour une équipe spécifique, celle-ci doit être activée pour cette équipe.</span><span class="sxs-lookup"><span data-stu-id="6bb00-125">If you want to install your app for a specific team, this will need to be on for that team.</span></span>
* <span data-ttu-id="6bb00-126">**Stratégie d’application personnalisée** par l’utilisateur : cet ensemble de paramètres contrôle les autorisations d’un utilisateur individuel.</span><span class="sxs-lookup"><span data-stu-id="6bb00-126">**User custom app policy** - This set of settings controls the permissions for an individual user.</span></span> <span data-ttu-id="6bb00-127">Vous devez activer cette activation pour les utilisateurs qui souhaitent télécharger des applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="6bb00-127">You'll need to enable this for individuals you want to upload custom apps.</span></span>

<span data-ttu-id="6bb00-128">Pour plus d’informations sur le mode d’interaction de ces paramètres, consultez la rubrique [Manage Custom App Policies and Settings in Microsoft teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).</span><span class="sxs-lookup"><span data-stu-id="6bb00-128">For complete information on how these settings interact see [Manage custom app policies and settings in Microsoft Teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).</span></span>
