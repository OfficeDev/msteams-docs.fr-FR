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
# <a name="device-capabilities"></a>Fonctionnalités de l’appareil

Microsoft Teams plate-forme améliore continuellement les capacités des développeurs en s’alignant sur les expériences intégrées de première partie. La plate-forme Teams permet aux partenaires d’intégrer des fonctionnalités d’appareil, telles que l’appareil photo, QR ou scanner de codes à barres, galerie de photos, microphone, et l’emplacement avec leurs applications Web. Cette intégration réduit l’obstacle au développement d’applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d’utilisation pour la communauté des développeurs.

## <a name="native-device-capabilities"></a>Capacités des appareils indigènes

Un appareil mobile ou de bureau est constitué d’appareils intégrés, tels qu’une caméra et un microphone, appelés capacités. Vous pouvez accéder aux fonctionnalités de l’appareil suivant sur mobile ou bureau via des API dédiées [disponibles dans Microsoft Teams client JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):
* Les capacités des médias, telles que
    * caméra
    * microphone
    * Galerie
    * QR ou scanner de codes à barres
* Emplacement

Après avoir eu accès aux fonctionnalités de l’appareil, vous pouvez les intégrer à Teams plate-forme pour améliorer l’expérience collaborative. 

## <a name="request-device-permissions"></a>Demande des autorisations d’appareil

Utilisez les outils présents dans [Microsoft Teams client JavaScript SDK pour](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) demander les autorisations requises pour accéder aux [fonctionnalités](native-device-permissions.md) de l’appareil natif. Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs Web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour le manifeste de votre application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute Teams clients mobiles ou de bureau.
 
 ## <a name="integrate-device-capabilities"></a>Intégrer les capacités de l’appareil

Après avoir eu accès aux fonctionnalités de l’appareil, utilisez Teams apis de capacité multimédia pour intégrer [les capacités](mobile-camera-image-permissions.md) multimédias à une plate Teams pour améliorer l’expérience utilisateur. Ces fonctionnalités intégrées permettent à votre application de :

* Capturez et partagez des images.
* Scannez QR ou code à barres à l’aide du [contrôle du scanner](qr-barcode-scanner-capability.md).
* Enregistrez l’audio à travers le microphone.
* Partagez l’emplacement à [l’aide du cueilleur de localisation](location-capability.md).
