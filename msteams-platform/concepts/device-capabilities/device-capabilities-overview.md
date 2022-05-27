---
title: Fonctionnalités de l’appareil – Vue d’ensemble
author: Rajeshwari-v
description: Découvrez comment intégrer des fonctionnalités d’appareil natif, telles que la caméra, l’image, le média, le microphone, le code QR, etc. avec Microsoft Teams application.
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 8d5c288e35ef18ada9ff93390ff745798ba3b01c
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757030"
---
# <a name="device-capabilities"></a>Fonctionnalités de l’appareil

La plateforme Microsoft Teams améliore en permanence les fonctionnalités de développement en s’alignant sur les expériences internes intégrées. La plateforme Teams améliorée permet aux partenaires d’intégrer des fonctionnalités d’appareil, telles que l’appareil photo, la QR ou le scanneur de codes-barres, la galerie de photos, le microphone et l’emplacement avec leurs applications web. Cette intégration réduit la barrière au développement d’applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d’usage pour la communauté des développeurs.

Les autorisations d’appareil sont différentes dans le navigateur. Auparavant, le navigateur gérait la façon d’accorder des autorisations d’accès et ces autorisations sont désormais gérées dans Microsoft Teams. Pour plus d'informations, consultez la section [Autorisations du périphérique de navigation](browser-device-permissions.md).

## <a name="native-device-capabilities"></a>Fonctionnalités natives de l’appareil

Un appareil mobile ou un bureau dispose d’appareils intégrés, tels que la caméra et le microphone, appelés fonctionnalités. Vous pouvez accéder aux fonctionnalités d’appareil suivantes sur les appareils mobiles ou de bureau via des API dédiées disponibles dans le [Kit de développement logiciel (SDK) client JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) : 

* Fonctionnalités multimédias, telles que
  * Appareil photo
  * Microphone
  * Galerie
  * QR ou scanneur de codes-barres
* Emplacement

Une fois que vous avez accès aux fonctionnalités de l’appareil, vous pouvez les intégrer à la plateforme Teams pour améliorer l’expérience collaborative.

## <a name="request-device-permissions"></a>Demande des autorisations d’appareil

Utilisez les outils présents dans le [Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) pour demander les [autorisations](native-device-permissions.md) requises pour accéder aux fonctionnalités d’appareil natif. Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams des fonctionnalités que vous utilisez en mettant à jour le manifeste de votre application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur des clients mobiles ou de bureau Teams.

## <a name="integrate-device-capabilities"></a>Intégrer les fonctionnalités de l’appareil

Une fois que vous avez accès aux fonctionnalités de l’appareil, utilisez les API de fonctionnalité multimédia Teams pour [intégrer des fonctionnalités multimédias](mobile-camera-image-permissions.md) à la plateforme Teams pour améliorer l’expérience utilisateur. Ces fonctionnalités intégrées permettent à votre application de :

* Capturer des photos et des images.
* Analysez le QR ou le code-barres à l’aide de [contrôle scanneur](qr-barcode-scanner-capability.md).
* Enregistrez l’audio via le microphone.
* Partagez l’emplacement à l’aide du [sélecteur d’emplacement](location-capability.md).

En outre, vous pouvez intégrer le [contrôle de sélecteur de personnes](people-picker-capability.md) natif Teams qui permet aux utilisateurs de rechercher et de sélectionner des personnes dans l’expérience d’application web.
