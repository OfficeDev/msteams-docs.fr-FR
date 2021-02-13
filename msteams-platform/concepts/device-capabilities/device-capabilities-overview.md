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
# <a name="device-capabilities"></a>Fonctionnalités de l’appareil 

La plateforme Microsoft Teams améliore en permanence les fonctionnalités de développement en s’alignant sur les expériences intégrées de la première partie. La plateforme Teams améliorée permet aux partenaires d’intégrer des fonctionnalités d’appareil, telles que l’appareil photo, la galerie de photos, le microphone et l’emplacement, à leurs applications web. Cette intégration réduit les obstacles au développement d’applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d’utilisation pour la communauté des développeurs.

## <a name="native-device-capabilities"></a>Fonctionnalités natives de l’appareil

Un appareil mobile ou de bureau dispose d’appareils intégrés, tels qu’un appareil photo et un microphone, appelés fonctionnalités. Vous pouvez accéder aux fonctionnalités d’appareil suivantes sur mobile ou bureau via des API dédiées disponibles dans le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):
* Fonctionnalités multimédias, telles que
    * Caméra
    * Microphone
    * Galerie
* Lieu

Après avoir accédé aux fonctionnalités de l’appareil, vous pouvez les intégrer à la plateforme Teams pour améliorer l’expérience de collaboration. 

## <a name="request-device-permissions"></a>Demande des autorisations d’appareil

Utilisez les outils présents dans le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) pour demander les  [autorisations requises](native-device-permissions.md) pour accéder aux fonctionnalités natives de l’appareil. Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams des fonctionnalités que vous utilisez en mettant à jour votre manifeste d’application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur les clients mobiles ou de bureau Teams.
 
 ## <a name="integrate-device-capabilities"></a>Intégrer des fonctionnalités d’appareil

Après avoir accédé aux fonctionnalités d’appareil, utilisez les API de fonctionnalité multimédia **Teams** pour intégrer les fonctionnalités à la plateforme Teams afin d’améliorer l’expérience utilisateur. [](mobile-camera-image-permissions.md) Ces fonctionnalités intégrées permettent à votre application de :

* Capturer et partager des images
* Enregistrer l’audio via le microphone
* Partager les informations d’emplacement


