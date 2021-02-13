---
title: Vue d’ensemble des fonctionnalités de l’appareil
description: Vue d’ensemble des fonctionnalités natives de l’appareil.
keywords: Autorisations natives du microphone du média de l’image d’appareil photo
ms.topic: overview
ms.openlocfilehash: 8b2f92cb4586d646bde02742883122bb009847ea
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2021
ms.locfileid: "50232846"
---
# <a name="device-capabilities"></a><span data-ttu-id="5ea1a-104">Fonctionnalités de l’appareil</span><span class="sxs-lookup"><span data-stu-id="5ea1a-104">Device capabilities</span></span> 

<span data-ttu-id="5ea1a-105">La plateforme Microsoft Teams améliore en permanence les fonctionnalités de développement en s’alignant sur les expériences intégrées de la première partie.</span><span class="sxs-lookup"><span data-stu-id="5ea1a-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="5ea1a-106">La plateforme Teams améliorée permet aux partenaires d’intégrer des fonctionnalités d’appareil, telles que l’appareil photo, la galerie de photos, le microphone et l’emplacement, à leurs applications web.</span><span class="sxs-lookup"><span data-stu-id="5ea1a-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, photo gallery, microphone, and location, with their web apps.</span></span> <span data-ttu-id="5ea1a-107">Cette intégration réduit les obstacles au développement d’applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d’utilisation pour la communauté des développeurs.</span><span class="sxs-lookup"><span data-stu-id="5ea1a-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="5ea1a-108">Fonctionnalités natives de l’appareil</span><span class="sxs-lookup"><span data-stu-id="5ea1a-108">Native device capabilities</span></span>

<span data-ttu-id="5ea1a-109">Un appareil mobile ou de bureau dispose d’appareils intégrés, tels qu’un appareil photo et un microphone, appelés fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="5ea1a-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="5ea1a-110">Vous pouvez accéder aux fonctionnalités d’appareil suivantes sur mobile ou bureau via des API dédiées disponibles dans le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span><span class="sxs-lookup"><span data-stu-id="5ea1a-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="5ea1a-111">Fonctionnalités multimédias, telles que</span><span class="sxs-lookup"><span data-stu-id="5ea1a-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="5ea1a-112">Caméra</span><span class="sxs-lookup"><span data-stu-id="5ea1a-112">Camera</span></span>
    * <span data-ttu-id="5ea1a-113">Microphone</span><span class="sxs-lookup"><span data-stu-id="5ea1a-113">Microphone</span></span>
    * <span data-ttu-id="5ea1a-114">Galerie</span><span class="sxs-lookup"><span data-stu-id="5ea1a-114">Gallery</span></span>
* <span data-ttu-id="5ea1a-115">Lieu</span><span class="sxs-lookup"><span data-stu-id="5ea1a-115">Location</span></span>

<span data-ttu-id="5ea1a-116">Après avoir accédé aux fonctionnalités de l’appareil, vous pouvez les intégrer à la plateforme Teams pour améliorer l’expérience de collaboration.</span><span class="sxs-lookup"><span data-stu-id="5ea1a-116">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="5ea1a-117">Demande des autorisations d’appareil</span><span class="sxs-lookup"><span data-stu-id="5ea1a-117">Request device permissions</span></span>

<span data-ttu-id="5ea1a-118">Utilisez les outils présents dans le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) pour demander les  [autorisations requises](native-device-permissions.md) pour accéder aux fonctionnalités natives de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="5ea1a-118">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to  request the required  [permissions](native-device-permissions.md) for  accessing the native device capabilities.</span></span> <span data-ttu-id="5ea1a-119">Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams des fonctionnalités que vous utilisez en mettant à jour votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="5ea1a-119">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="5ea1a-120">Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur les clients mobiles ou de bureau Teams.</span><span class="sxs-lookup"><span data-stu-id="5ea1a-120">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="5ea1a-121">Intégrer des fonctionnalités d’appareil</span><span class="sxs-lookup"><span data-stu-id="5ea1a-121">Integrate device capabilities</span></span>

<span data-ttu-id="5ea1a-122">Après avoir accédé aux fonctionnalités d’appareil, utilisez les API de fonctionnalité multimédia **Teams** pour intégrer les fonctionnalités à la plateforme Teams afin d’améliorer l’expérience utilisateur. [](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="5ea1a-122">After getting access to device capabilities,use **Teams media capability APIs** to [integrate the capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="5ea1a-123">Ces fonctionnalités intégrées permettent à votre application de :</span><span class="sxs-lookup"><span data-stu-id="5ea1a-123">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="5ea1a-124">Capturer et partager des images</span><span class="sxs-lookup"><span data-stu-id="5ea1a-124">Capture and share images</span></span>
* <span data-ttu-id="5ea1a-125">Enregistrer l’audio via le microphone</span><span class="sxs-lookup"><span data-stu-id="5ea1a-125">Record audio through microphone</span></span>
* <span data-ttu-id="5ea1a-126">Partager les informations d’emplacement</span><span class="sxs-lookup"><span data-stu-id="5ea1a-126">Share the location information</span></span>


