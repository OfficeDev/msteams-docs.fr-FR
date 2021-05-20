---
title: Capacités de l’appareil - Vue d’ensemble
author: Rajeshwari-v
description: Vue d’ensemble des capacités des appareils natifs.
ms.author: surbhigupta
keywords: caméra image media microphone micro qr code qrcode code à barres scanner capacités de localisation des autorisations de périphérique natif
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 8df8341e8996e4bf380575ac59e05325da16bd0d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566193"
---
# <a name="device-capabilities"></a><span data-ttu-id="3d9ef-104">Fonctionnalités de l’appareil</span><span class="sxs-lookup"><span data-stu-id="3d9ef-104">Device capabilities</span></span>

<span data-ttu-id="3d9ef-105">Microsoft Teams plate-forme améliore continuellement les capacités des développeurs en s’alignant sur les expériences intégrées de première partie.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="3d9ef-106">La plate-forme Teams permet aux partenaires d’intégrer des fonctionnalités d’appareil, telles que l’appareil photo, QR ou scanner de codes à barres, galerie de photos, microphone, et l’emplacement avec leurs applications Web.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="3d9ef-107">Cette intégration réduit l’obstacle au développement d’applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d’utilisation pour la communauté des développeurs.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="3d9ef-108">Capacités des appareils indigènes</span><span class="sxs-lookup"><span data-stu-id="3d9ef-108">Native device capabilities</span></span>

<span data-ttu-id="3d9ef-109">Un appareil mobile ou de bureau est constitué d’appareils intégrés, tels qu’une caméra et un microphone, appelés capacités.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="3d9ef-110">Vous pouvez accéder aux fonctionnalités de l’appareil suivant sur mobile ou bureau via des API dédiées [disponibles dans Microsoft Teams client JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span><span class="sxs-lookup"><span data-stu-id="3d9ef-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="3d9ef-111">Les capacités des médias, telles que</span><span class="sxs-lookup"><span data-stu-id="3d9ef-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="3d9ef-112">caméra</span><span class="sxs-lookup"><span data-stu-id="3d9ef-112">Camera</span></span>
    * <span data-ttu-id="3d9ef-113">microphone</span><span class="sxs-lookup"><span data-stu-id="3d9ef-113">Microphone</span></span>
    * <span data-ttu-id="3d9ef-114">Galerie</span><span class="sxs-lookup"><span data-stu-id="3d9ef-114">Gallery</span></span>
    * <span data-ttu-id="3d9ef-115">QR ou scanner de codes à barres</span><span class="sxs-lookup"><span data-stu-id="3d9ef-115">QR or barcode scanner</span></span>
* <span data-ttu-id="3d9ef-116">Emplacement</span><span class="sxs-lookup"><span data-stu-id="3d9ef-116">Location</span></span>

<span data-ttu-id="3d9ef-117">Après avoir eu accès aux fonctionnalités de l’appareil, vous pouvez les intégrer à Teams plate-forme pour améliorer l’expérience collaborative.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="3d9ef-118">Demande des autorisations d’appareil</span><span class="sxs-lookup"><span data-stu-id="3d9ef-118">Request device permissions</span></span>

<span data-ttu-id="3d9ef-119">Utilisez les outils présents dans [Microsoft Teams client JavaScript SDK pour](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) demander les autorisations requises pour accéder aux [fonctionnalités](native-device-permissions.md) de l’appareil natif.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="3d9ef-120">Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs Web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="3d9ef-121">Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute Teams clients mobiles ou de bureau.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="3d9ef-122">Intégrer les capacités de l’appareil</span><span class="sxs-lookup"><span data-stu-id="3d9ef-122">Integrate device capabilities</span></span>

<span data-ttu-id="3d9ef-123">Après avoir eu accès aux fonctionnalités de l’appareil, utilisez Teams apis de capacité multimédia pour intégrer [les capacités](mobile-camera-image-permissions.md) multimédias à une plate Teams pour améliorer l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="3d9ef-124">Ces fonctionnalités intégrées permettent à votre application de :</span><span class="sxs-lookup"><span data-stu-id="3d9ef-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="3d9ef-125">Capturez et partagez des images.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-125">Capture and share images.</span></span>
* <span data-ttu-id="3d9ef-126">Scannez QR ou code à barres à l’aide du [contrôle du scanner](qr-barcode-scanner-capability.md).</span><span class="sxs-lookup"><span data-stu-id="3d9ef-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md).</span></span>
* <span data-ttu-id="3d9ef-127">Enregistrez l’audio à travers le microphone.</span><span class="sxs-lookup"><span data-stu-id="3d9ef-127">Record audio through microphone.</span></span>
* <span data-ttu-id="3d9ef-128">Partagez l’emplacement à [l’aide du cueilleur de localisation](location-capability.md).</span><span class="sxs-lookup"><span data-stu-id="3d9ef-128">Share location using [location picker](location-capability.md).</span></span>
