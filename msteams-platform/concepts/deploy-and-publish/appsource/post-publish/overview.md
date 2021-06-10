---
title: Maintenir et prendre en charge votre application publiée
description: Ce à quoi il faut penser une fois que votre magasin est répertorié dans Teams store et AppSource.
ms.topic: conceptual
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 8e4656ea7ca9f373123026a50ecb837d1a64e3fa
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230916"
---
# <a name="maintain-your-published-microsoft-teams-app"></a><span data-ttu-id="a8cd2-103">Gérer votre application Microsoft Teams publiée</span><span class="sxs-lookup"><span data-stu-id="a8cd2-103">Maintain your published Microsoft Teams app</span></span>

<span data-ttu-id="a8cd2-104">Une fois votre application répertoriée dans le Microsoft Teams, commencez à réfléchir à la façon dont vous allez gérer l’application à l’avenir et augmenter les téléchargements et l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-104">With your app listed on the Microsoft Teams store, start thinking about how you'll maintain the app going forward and increase downloads and usage.</span></span>

## <a name="publish-updates-to-your-app"></a><span data-ttu-id="a8cd2-105">Publier des mises à jour sur votre application</span><span class="sxs-lookup"><span data-stu-id="a8cd2-105">Publish updates to your app</span></span>

<span data-ttu-id="a8cd2-106">Vous pouvez soumettre des modifications à votre application (par exemple, de nouvelles fonctionnalités ou même des métadonnées) dans l’Partner Center.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-106">You can submit changes to your app (such as new features or even metadata) in Partner Center.</span></span> <span data-ttu-id="a8cd2-107">Ces modifications nécessitent un nouveau processus de révision.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-107">These changes requires a new review process.</span></span>

<span data-ttu-id="a8cd2-108">Veillez à ce qui suit lors de la publication des mises à jour :</span><span class="sxs-lookup"><span data-stu-id="a8cd2-108">Ensure the following when publishing updates:</span></span>

* <span data-ttu-id="a8cd2-109">Ne modifiez pas votre ID d’application.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-109">Don't change your app ID.</span></span>
* <span data-ttu-id="a8cd2-110">Incrémentez le numéro de version de votre application.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-110">Increment your app's version number.</span></span>
* <span data-ttu-id="a8cd2-111">Dans l’Partner Center, ne sélectionnez **pas Ajouter une nouvelle application** pour la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-111">In Partner Center, don't select **Add a new app** to do the update.</span></span> <span data-ttu-id="a8cd2-112">À la place, allez sur la page de votre application.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-112">Go to your app's page instead.</span></span>

### <a name="app-updates-requiring-user-consent"></a><span data-ttu-id="a8cd2-113">Mises à jour d’application nécessitant le consentement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a8cd2-113">App updates requiring user consent</span></span>

<span data-ttu-id="a8cd2-114">Lorsqu’un utilisateur installe votre application, il doit lui accorder l’autorisation d’accéder aux services et aux informations dont l’application a besoin pour fonctionner.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-114">When a user installs your app, they must give the app permission to access the services and information the app requires to function.</span></span> <span data-ttu-id="a8cd2-115">Dans la plupart des cas, les utilisateurs n’ont à le faire qu’une seule fois et les nouvelles versions de votre application s’installent automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-115">In most cases, users only have to do this once and new versions of your app install automatically.</span></span>

<span data-ttu-id="a8cd2-116">Toutefois, si vous a apporté l’une des modifications suivantes à votre application, vos utilisateurs existants doivent accepter une autre demande d’autorisation pour installer la mise à jour :</span><span class="sxs-lookup"><span data-stu-id="a8cd2-116">If you make any of the following changes to your app, however, your existing users must accept another permission request to install the update:</span></span>

* <span data-ttu-id="a8cd2-117">Ajoutez ou supprimez un bot.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-117">Add or remove a bot.</span></span>
* <span data-ttu-id="a8cd2-118">Modifiez l’ID du bot.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-118">Change the bot ID.</span></span>
* <span data-ttu-id="a8cd2-119">Modifier la configuration de notification à sens seul d’un bot.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-119">Modify a bot's one-way notification configuration.</span></span>
* <span data-ttu-id="a8cd2-120">Modifier la prise en charge d’un bot pour le chargement et le téléchargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-120">Modify a bot's support for uploading and downloading files.</span></span>
* <span data-ttu-id="a8cd2-121">Ajouter ou supprimer une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-121">Add or remove a messaging extension.</span></span>
* <span data-ttu-id="a8cd2-122">Ajoutez un onglet personnel.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-122">Add a personal tab.</span></span>
* <span data-ttu-id="a8cd2-123">Ajoutez un canal et un onglet de groupe.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-123">Add a channel and group tab.</span></span>
* <span data-ttu-id="a8cd2-124">Ajoutez un connecteur.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-124">Add a connector.</span></span>
* <span data-ttu-id="a8cd2-125">Modifiez les configurations liées à l’inscription Azure Active Directory de votre application (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8cd2-125">Modify configurations related to your Azure Active Directory (Azure AD) app registration.</span></span> <span data-ttu-id="a8cd2-126">Pour plus d’informations, voir [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo) .</span><span class="sxs-lookup"><span data-stu-id="a8cd2-126">For more information, see [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).</span></span>

## <a name="fix-issues-with-your-published-app"></a><span data-ttu-id="a8cd2-127">Résoudre les problèmes avec votre application publiée</span><span class="sxs-lookup"><span data-stu-id="a8cd2-127">Fix issues with your published app</span></span>

<span data-ttu-id="a8cd2-128">Microsoft exécute des tests d’automatisation quotidiens sur les applications répertoriées dans Teams store.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-128">Microsoft runs daily automation tests on apps listed on the Teams store.</span></span> <span data-ttu-id="a8cd2-129">Si des problèmes avec votre application sont identifiés, nous vous contactons avec un rapport détaillé sur la façon de reproduire les problèmes et les recommandations pour les résoudre.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-129">If issues with your app are identified, we contact you with a detailed report on how to reproduce the issues and recommendations to resolve them.</span></span> <span data-ttu-id="a8cd2-130">Si vous ne pouvez pas résoudre les problèmes dans une chronologie, la liste de votre application peut être supprimée du Store.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-130">If you can't fix the problems within a stated timeline, your app listing may be removed from the store.</span></span>

## <a name="promote-your-app-on-another-site"></a><span data-ttu-id="a8cd2-131">Promouvoir votre application sur un autre site</span><span class="sxs-lookup"><span data-stu-id="a8cd2-131">Promote your app on another site</span></span>

<span data-ttu-id="a8cd2-132">Lorsque votre application est répertoriée dans le magasin Teams, vous pouvez créer un lien qui lance Teams et affiche une boîte de dialogue pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-132">When your app is listed in the Teams store, you can create a link that launches Teams and displays a dialog to install your app.</span></span> <span data-ttu-id="a8cd2-133">Vous pouvez inclure ce lien, par exemple, avec un bouton de téléchargement sur la page marketing de votre produit.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-133">You could include this link, for example, with a download button on your product's marketing page.</span></span>

<span data-ttu-id="a8cd2-134">Créez le lien à l’aide de l’URL suivante, à l’aide de votre ID d’application : `https://teams.microsoft.com/l/app/<your-app-id>`</span><span class="sxs-lookup"><span data-stu-id="a8cd2-134">Create the link using the following URL appended with your app ID: `https://teams.microsoft.com/l/app/<your-app-id>`.</span></span>

## <a name="complete-microsoft-365-certification"></a><span data-ttu-id="a8cd2-135">Certification Microsoft 365 complète</span><span class="sxs-lookup"><span data-stu-id="a8cd2-135">Complete Microsoft 365 Certification</span></span>

<span data-ttu-id="a8cd2-136">[Microsoft 365 certification](/microsoft-365-app-certification/docs/certification) garantit que les données et la confidentialité sont correctement sécurisées et protégées lorsqu’un application Office ou un add-in tiers est installé dans votre écosystème Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-136">[Microsoft 365 Certification](/microsoft-365-app-certification/docs/certification) offers assurances that data and privacy are adequately secured and protected when a third-party Office app or add-in is installed in your Microsoft 365 ecosystem.</span></span> <span data-ttu-id="a8cd2-137">La certification confirme que votre application est compatible avec les technologies Microsoft, conforme aux meilleures pratiques de sécurité des applications cloud et prise en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a8cd2-137">Certification confirms that your app is compatible with Microsoft technologies, compliant with cloud app security best practices, and supported by Microsoft.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8cd2-138">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a8cd2-138">See also</span></span>

[<span data-ttu-id="a8cd2-139">Monétisez votre application via Microsoft Commercial Marketplace</span><span class="sxs-lookup"><span data-stu-id="a8cd2-139">Monetize your app through Microsoft Commercial Marketplace</span></span>](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
