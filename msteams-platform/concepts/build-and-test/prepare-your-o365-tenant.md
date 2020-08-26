---
title: Préparer votre client Office 365
description: Prise en main de teams dans Office 365
keywords: Configurer le chargement des équipes client Office 365
ms.openlocfilehash: a246b13ae3a12a486a06ff9d98d37d4d147e4ed4
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874862"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="afd18-104">Préparer votre client Office 365</span><span class="sxs-lookup"><span data-stu-id="afd18-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="afd18-105">Si vous êtes un abonné Office 365, vous pouvez développer des applications pour Microsoft teams à l’aide de l’un des [plans](https://products.office.com/business/compare-more-office-365-for-business-plans)suivants :</span><span class="sxs-lookup"><span data-stu-id="afd18-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="afd18-106">Business Essentials</span><span class="sxs-lookup"><span data-stu-id="afd18-106">Business Essentials</span></span>
* <span data-ttu-id="afd18-107">Business Premium</span><span class="sxs-lookup"><span data-stu-id="afd18-107">Business Premium</span></span>
* <span data-ttu-id="afd18-108">Entreprise E1, E3 et E5</span><span class="sxs-lookup"><span data-stu-id="afd18-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="afd18-109">Developer</span><span class="sxs-lookup"><span data-stu-id="afd18-109">Developer</span></span>
* <span data-ttu-id="afd18-110">Éducation, éducation plus et éducation E5</span><span class="sxs-lookup"><span data-stu-id="afd18-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="afd18-111">Microsoft teams sera également disponible pour les clients abonnés à E4 avant sa [retraite](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span><span class="sxs-lookup"><span data-stu-id="afd18-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="afd18-112">Vous avez besoin d’un environnement de développement ?</span><span class="sxs-lookup"><span data-stu-id="afd18-112">Just need a development environment?</span></span>

<span data-ttu-id="afd18-113">Si vous ne disposez pas d’un compte Office 365, vous pouvez vous inscrire pour obtenir un abonnement au [programme de développement Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) .</span><span class="sxs-lookup"><span data-stu-id="afd18-113">If you don't currently have an Office 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="afd18-114">Elle est *gratuite* pendant 90 jours et se renouvelle en permanence tant que vous l’utiliserez pour l’activité de développement.</span><span class="sxs-lookup"><span data-stu-id="afd18-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="afd18-115">Si vous disposez d’un abonnement Visual Studio *entreprise* ou *professionnel* , les deux programmes incluent un [abonnement de développeur](https://aka.ms/MyVisualStudioBenefits)gratuit Microsoft 365, actif pendant la durée de vie de votre abonnement Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="afd18-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="afd18-116">*Consultez la rubrique* [configurer un abonnement développeur Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="afd18-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="afd18-117">Activer Microsoft teams pour votre organisation</span><span class="sxs-lookup"><span data-stu-id="afd18-117">Enable Microsoft Teams for your organization</span></span> 

<span data-ttu-id="afd18-118">Si Microsoft teams n’a pas été activé pour votre organisation, vous devez tout d’abord le faire.</span><span class="sxs-lookup"><span data-stu-id="afd18-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="afd18-119">Consultez nos conseils détaillés pour [l’activation de teams pour votre organisation](/microsoftteams/enable-features-office-365).</span><span class="sxs-lookup"><span data-stu-id="afd18-119">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="afd18-120">Activer les applications de teams personnalisées et activer le téléchargement de l’application personnalisée</span><span class="sxs-lookup"><span data-stu-id="afd18-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="afd18-121">Activez l’application personnalisée chargement pour votre client développeur comme suit :</span><span class="sxs-lookup"><span data-stu-id="afd18-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="afd18-122">Connectez-vous au [Centre d’administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="afd18-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="afd18-123">Sélectionnez **afficher toutes les**  -->  **équipes**.</span><span class="sxs-lookup"><span data-stu-id="afd18-123">Select **Show All** --> **Teams**.</span></span> 

![image du menu du centre d’administration](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> <span data-ttu-id="afd18-125">L’option « teams » peut prendre jusqu’à 24 heures.</span><span class="sxs-lookup"><span data-stu-id="afd18-125">It can take up to 24 hours for the "Teams" option to appear.</span></span> <span data-ttu-id="afd18-126">Pendant le temps, vous pouvez [charger votre application personnalisée dans un environnement de teams](/microsoftteams/upload-custom-apps#validate) à des fins de test et de validation.</span><span class="sxs-lookup"><span data-stu-id="afd18-126">During interim, you can [Upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation.</span></span>

3. <span data-ttu-id="afd18-127">Accéder aux stratégies d’installation des **applications teams**  -->  **Setup Policies**  -->  **global (par défaut** à l’échelle de l’organisation)</span><span class="sxs-lookup"><span data-stu-id="afd18-127">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![activer l’affichage chargement](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="afd18-129">Basculez **charger les applications personnalisées** vers la position **en** place.</span><span class="sxs-lookup"><span data-stu-id="afd18-129">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="afd18-130">Voilà !</span><span class="sxs-lookup"><span data-stu-id="afd18-130">That's it!</span></span> <span data-ttu-id="afd18-131">Votre client de test autorisera maintenant l’application personnalisée chargement.</span><span class="sxs-lookup"><span data-stu-id="afd18-131">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="afd18-132">L’activation de la chargement peut prendre jusqu’à 24 heures.</span><span class="sxs-lookup"><span data-stu-id="afd18-132">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="afd18-133">Pendant un intervalle de temps, vous pouvez utiliser le \*\*chargement pour \<your tenant> \*\* tester votre application.</span><span class="sxs-lookup"><span data-stu-id="afd18-133">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![affichage de l’application updload](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="afd18-135">Pour plus d’informations sur la façon dont ces paramètres interagissent, *voir* [gérer les stratégies et les paramètres d’application personnalisés dans Microsoft teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) et [gérer les stratégies de configuration d’application dans Microsoft teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span><span class="sxs-lookup"><span data-stu-id="afd18-135">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
