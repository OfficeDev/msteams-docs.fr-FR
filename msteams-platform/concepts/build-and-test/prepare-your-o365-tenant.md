---
title: Préparer votre client Microsoft Office 365
description: Comment commencer à travailler avec Teams dans Microsoft 365
ms.topic: how-to
keywords: Configurer le téléchargement de Microsoft 365 tenant Teams
ms.openlocfilehash: 50765271b93edd380d1c23672289b618baf1d346
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093942"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="53ac7-104">Préparer votre client Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="53ac7-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="53ac7-105">Si vous êtes abonné à Microsoft 365, vous pouvez développer des applications pour Microsoft Teams avec l’un des [plans suivants](https://products.office.com/business/compare-more-office-365-for-business-plans):</span><span class="sxs-lookup"><span data-stu-id="53ac7-105">If you are a Microsoft 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="53ac7-106">Basic</span><span class="sxs-lookup"><span data-stu-id="53ac7-106">Basic</span></span>
* <span data-ttu-id="53ac7-107">Standard</span><span class="sxs-lookup"><span data-stu-id="53ac7-107">Standard</span></span>
* <span data-ttu-id="53ac7-108">Entreprise E1, E3 et E5</span><span class="sxs-lookup"><span data-stu-id="53ac7-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="53ac7-109">Developer</span><span class="sxs-lookup"><span data-stu-id="53ac7-109">Developer</span></span>
* <span data-ttu-id="53ac7-110">Éducation, Éducation Plus et Éducation E5</span><span class="sxs-lookup"><span data-stu-id="53ac7-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="53ac7-111">Microsoft Teams sera également disponible pour les clients qui ont souscrit à L’E4 avant son [retrait.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)</span><span class="sxs-lookup"><span data-stu-id="53ac7-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="53ac7-112">Vous avez simplement besoin d’un environnement de développement ?</span><span class="sxs-lookup"><span data-stu-id="53ac7-112">Just need a development environment?</span></span>

<span data-ttu-id="53ac7-113">Si vous n’avez pas encore de compte Microsoft 365, vous pouvez vous inscrire à un abonnement au programme pour les développeurs [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="53ac7-113">If you don't currently have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="53ac7-114">Il est *gratuit pendant* 90 jours et est continuellement renouvelé tant que vous l’utilisez pour l’activité de développement.</span><span class="sxs-lookup"><span data-stu-id="53ac7-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="53ac7-115">Si vous avez un abonnement  Visual Studio *Entreprise* ou Professionnel, les deux programmes incluent un abonnement microsoft 365 [](https://aka.ms/MyVisualStudioBenefits)développeur gratuit, actif pendant toute la durée de vie de Visual Studio abonnement.</span><span class="sxs-lookup"><span data-stu-id="53ac7-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="53ac7-116">*Voir* [Configurer un abonnement Microsoft 365 Développeur.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="53ac7-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="53ac7-117">Activer Microsoft Teams pour votre organisation</span><span class="sxs-lookup"><span data-stu-id="53ac7-117">Enable Microsoft Teams for your organization</span></span> 

<span data-ttu-id="53ac7-118">Si Microsoft Teams n’a pas été activé pour votre organisation, vous devez d’abord le faire.</span><span class="sxs-lookup"><span data-stu-id="53ac7-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="53ac7-119">Jetez un œil à nos conseils détaillés pour [l’activation de Teams pour votre organisation.](/microsoftteams/enable-features-office-365)</span><span class="sxs-lookup"><span data-stu-id="53ac7-119">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="53ac7-120">Activer les applications Teams personnalisées et activer le chargement d’applications personnalisées</span><span class="sxs-lookup"><span data-stu-id="53ac7-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="53ac7-121">Activer le chargement indépendant d’une application personnalisée pour votre client développeur comme suit :</span><span class="sxs-lookup"><span data-stu-id="53ac7-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="53ac7-122">Connectez-vous au Centre d’administration [Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="53ac7-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="53ac7-123">Sélectionnez **Afficher toutes les**  -->  **équipes.**</span><span class="sxs-lookup"><span data-stu-id="53ac7-123">Select **Show All** --> **Teams**.</span></span> 

![image du menu centre d’administration](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> <span data-ttu-id="53ac7-125">L’apparition de l’option « Teams » peut prendre jusqu’à 24 heures.</span><span class="sxs-lookup"><span data-stu-id="53ac7-125">It can take up to 24 hours for the "Teams" option to appear.</span></span> <span data-ttu-id="53ac7-126">Pendant l’intervalle, vous pouvez [charger votre application personnalisée dans un](/microsoftteams/upload-custom-apps#validate) environnement Teams à des fins de test et de validation.</span><span class="sxs-lookup"><span data-stu-id="53ac7-126">During interim, you can [Upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation.</span></span>

3. <span data-ttu-id="53ac7-127">Accéder aux **stratégies d’installation** des applications Teams à  -->  **l’échelle**  -->  **globale (par défaut à l’échelle de l’organisation)**</span><span class="sxs-lookup"><span data-stu-id="53ac7-127">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![activer l’affichage sideload](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="53ac7-129">Basculez le **chargement d’applications personnalisées** à **la** position sur.</span><span class="sxs-lookup"><span data-stu-id="53ac7-129">Toggle **upload custom apps** to the **on** position.</span></span>

5. <span data-ttu-id="53ac7-130">Sélectionnez **Enregistrer** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="53ac7-130">Select **Save** to save the changes.</span></span>

<span data-ttu-id="53ac7-131">Voilà !</span><span class="sxs-lookup"><span data-stu-id="53ac7-131">That's it!</span></span> <span data-ttu-id="53ac7-132">Votre client test autorise désormais le chargement de version test de l’application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="53ac7-132">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="53ac7-133">Le chargement de version latéral peut prendre jusqu’à 24 heures.</span><span class="sxs-lookup"><span data-stu-id="53ac7-133">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="53ac7-134">Pendant l’intervalle, vous pouvez utiliser **le chargement pour \<your tenant>** tester votre application.</span><span class="sxs-lookup"><span data-stu-id="53ac7-134">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![affichage updload de l’application](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="53ac7-136">Pour plus d’informations sur l’interaction de ces paramètres, voir , Gérer les stratégies et paramètres d’application [personnalisés](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) dans Microsoft Teams et Gérer les stratégies de configuration d’application [dans Microsoft Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)</span><span class="sxs-lookup"><span data-stu-id="53ac7-136">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
