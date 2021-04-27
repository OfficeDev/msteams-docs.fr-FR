---
title: "Fonctionnalités de l'appareil : vue d'ensemble"
author: Rajeshwari-v
description: Vue d'ensemble des fonctionnalités natives de l'appareil.
ms.author: surbhigupta
keywords: Image de l'image de l'appareil photo microphone microphone qr code code-barres analyser les fonctionnalités natives d'autorisations de l'appareil
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 7d214e5011abdc83d2f6b5b49c2261359259035e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020750"
---
# <a name="device-capabilities---overview"></a>Fonctionnalités de l'appareil : vue d'ensemble

La plateforme Microsoft Teams améliore en permanence les capacités des développeurs en s'alignant sur les expériences intégrées de la première partie. La plateforme Teams améliorée permet aux partenaires d'intégrer des fonctionnalités d'appareil, telles que l'appareil photo, le scanneur de QR ou de code-barres, la galerie de photos, le microphone et l'emplacement à leurs applications web. Cette intégration réduit les obstacles au développement d'applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d'utilisation pour la communauté des développeurs.

## <a name="native-device-capabilities"></a>Fonctionnalités natives de l'appareil

Un appareil mobile ou de bureau dispose d'appareils intégrés, tels qu'un appareil photo et un microphone, appelés fonctionnalités. Vous pouvez accéder aux fonctionnalités d'appareil suivantes sur mobile ou bureau via des API dédiées disponibles dans le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):
* Fonctionnalités multimédias, telles que
    * Appareil photo
    * Microphone
    * Galerie
    * QR ou scanneur de code-barres
* Emplacement

Après avoir accédé aux fonctionnalités de l'appareil, vous pouvez les intégrer à la plateforme Teams pour améliorer l'expérience de collaboration. 

## <a name="request-device-permissions"></a>Demande des autorisations d’appareil

Utilisez les outils présents dans le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) pour demander les  [autorisations requises](native-device-permissions.md) pour accéder aux fonctionnalités natives de l'appareil. Bien que l'accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams des fonctionnalités que vous utilisez en mettant à jour votre manifeste d'application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s'exécute sur les clients mobiles ou de bureau Teams.
 
 ## <a name="integrate-device-capabilities"></a>Intégrer les fonctionnalités de l'appareil

Après avoir accédé aux fonctionnalités de l'appareil, utilisez les API de fonctionnalité multimédia Teams pour intégrer des fonctionnalités multimédias à la plateforme Teams afin d'améliorer l'expérience utilisateur. [](mobile-camera-image-permissions.md) Ces fonctionnalités intégrées permettent à votre application de :

* Capturer et partager des images
* Analyser la QR ou le code-barres à l'aide du [contrôle scanneur](qr-barcode-scanner-capability.md)
* Enregistrer l'audio via le microphone
* Partager l'emplacement à [l'aide du s picker d'emplacement.](location-capability.md)
