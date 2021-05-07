---
title: 'Fonctionnalités de l’appareil : vue d’ensemble'
author: Rajeshwari-v
description: Vue d’ensemble des fonctionnalités natives de l’appareil.
ms.author: surbhigupta
keywords: Image de l’image de l’appareil photo microphone microphone qr code code code-barres code-barres analyse scanneur emplacement des fonctionnalités natives d’autorisations de périphérique
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: d67b343e3e07d7aea79282ce02ef8247fcf77159
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230896"
---
# <a name="device-capabilities"></a><span data-ttu-id="dcf88-104">Fonctionnalités de l’appareil</span><span class="sxs-lookup"><span data-stu-id="dcf88-104">Device capabilities</span></span>

<span data-ttu-id="dcf88-105">Microsoft Teams plateforme de développement améliore en permanence les fonctionnalités des développeurs en s’alignant sur les expériences intégrées de la première partie.</span><span class="sxs-lookup"><span data-stu-id="dcf88-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="dcf88-106">La plateforme Teams améliorée permet aux partenaires d’intégrer des fonctionnalités d’appareil, telles que l’appareil photo, le scanneur de QR ou de code-barres, la galerie de photos, le microphone et l’emplacement à leurs applications web.</span><span class="sxs-lookup"><span data-stu-id="dcf88-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="dcf88-107">Cette intégration réduit les obstacles au développement d’applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d’utilisation pour la communauté des développeurs.</span><span class="sxs-lookup"><span data-stu-id="dcf88-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="dcf88-108">Fonctionnalités natives de l’appareil</span><span class="sxs-lookup"><span data-stu-id="dcf88-108">Native device capabilities</span></span>

<span data-ttu-id="dcf88-109">Un appareil mobile ou de bureau dispose d’appareils intégrés, tels qu’un appareil photo et un microphone, appelés fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="dcf88-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="dcf88-110">Vous pouvez accéder aux fonctionnalités d’appareil suivantes sur mobile ou bureau via des API dédiées disponibles [dans Microsoft Teams SDK client JavaScript :](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="dcf88-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="dcf88-111">Fonctionnalités multimédias, telles que</span><span class="sxs-lookup"><span data-stu-id="dcf88-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="dcf88-112">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="dcf88-112">Camera</span></span>
    * <span data-ttu-id="dcf88-113">Microphone</span><span class="sxs-lookup"><span data-stu-id="dcf88-113">Microphone</span></span>
    * <span data-ttu-id="dcf88-114">Galerie</span><span class="sxs-lookup"><span data-stu-id="dcf88-114">Gallery</span></span>
    * <span data-ttu-id="dcf88-115">QR ou scanneur de code-barres</span><span class="sxs-lookup"><span data-stu-id="dcf88-115">QR or barcode scanner</span></span>
* <span data-ttu-id="dcf88-116">Emplacement</span><span class="sxs-lookup"><span data-stu-id="dcf88-116">Location</span></span>

<span data-ttu-id="dcf88-117">Après avoir accédé aux fonctionnalités de l’appareil, vous pouvez les intégrer à Teams plateforme pour améliorer l’expérience de collaboration.</span><span class="sxs-lookup"><span data-stu-id="dcf88-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="dcf88-118">Demande des autorisations d’appareil</span><span class="sxs-lookup"><span data-stu-id="dcf88-118">Request device permissions</span></span>

<span data-ttu-id="dcf88-119">Utilisez les outils présents [dans Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) pour demander les autorisations requises pour accéder aux [fonctionnalités natives](native-device-permissions.md) de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="dcf88-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="dcf88-120">Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="dcf88-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="dcf88-121">Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur Teams clients mobiles ou de bureau.</span><span class="sxs-lookup"><span data-stu-id="dcf88-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="dcf88-122">Intégrer les fonctionnalités de l’appareil</span><span class="sxs-lookup"><span data-stu-id="dcf88-122">Integrate device capabilities</span></span>

<span data-ttu-id="dcf88-123">Après avoir accédé aux fonctionnalités de l’appareil, [](mobile-camera-image-permissions.md) utilisez Teams API de fonctionnalité multimédia pour intégrer des fonctionnalités multimédias à Teams plateforme afin d’améliorer l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dcf88-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="dcf88-124">Ces fonctionnalités intégrées permettent à votre application de :</span><span class="sxs-lookup"><span data-stu-id="dcf88-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="dcf88-125">Capturer et partager des images</span><span class="sxs-lookup"><span data-stu-id="dcf88-125">Capture and share images</span></span>
* <span data-ttu-id="dcf88-126">Analyser la QR ou le code-barres à l’aide du [contrôle scanneur](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="dcf88-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md)</span></span>
* <span data-ttu-id="dcf88-127">Enregistrer l’audio via le microphone</span><span class="sxs-lookup"><span data-stu-id="dcf88-127">Record audio through microphone</span></span>
* <span data-ttu-id="dcf88-128">Partager l’emplacement à [l’aide du s picker d’emplacement.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="dcf88-128">Share location using [location picker](location-capability.md).</span></span>
