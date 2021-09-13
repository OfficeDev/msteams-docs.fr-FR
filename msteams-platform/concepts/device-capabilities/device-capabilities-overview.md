---
title: 'Fonctionnalités de l’appareil : vue d’ensemble'
author: Rajeshwari-v
description: Vue d’ensemble des fonctionnalités natives de l’appareil.
ms.author: surbhigupta
keywords: Image de l’image de l’appareil photo microphone microphone qr code code code-barres code-barres analyse scanneur emplacement des fonctionnalités natives d’autorisations de périphérique
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 6b1fcb436dc77c1859c81010c1d1eb5adcc3773a
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156928"
---
# <a name="device-capabilities"></a>Fonctionnalités de l’appareil

Microsoft Teams plateforme de développement améliore en permanence les fonctionnalités des développeurs en s’alignant sur les expériences intégrées de la première partie. La plateforme Teams améliorée permet aux partenaires d’intégrer des fonctionnalités d’appareil, telles que l’appareil photo, le scanneur de QR ou de code-barres, la galerie de photos, le microphone et l’emplacement à leurs applications web. Cette intégration réduit les obstacles au développement d’applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d’utilisation pour la communauté des développeurs.

## <a name="native-device-capabilities"></a>Fonctionnalités natives de l’appareil

Un appareil mobile ou de bureau dispose d’appareils intégrés, tels qu’un appareil photo et un microphone, appelés fonctionnalités. Vous pouvez accéder aux fonctionnalités d’appareil suivantes sur mobile ou bureau via des API dédiées disponibles [dans Microsoft Teams SDK client JavaScript :](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* Fonctionnalités multimédias, telles que
    * Appareil photo
    * Microphone
    * Galerie
    * QR ou scanneur de code-barres
* Emplacement

Après avoir accédé aux fonctionnalités de l’appareil, vous pouvez les intégrer à Teams plateforme pour améliorer l’expérience de collaboration. 

## <a name="request-device-permissions"></a>Demande des autorisations d’appareil

Utilisez les outils présents [dans Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) pour demander les autorisations requises pour accéder aux [fonctionnalités natives](native-device-permissions.md) de l’appareil. Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour votre manifeste d’application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur Teams clients mobiles ou de bureau.
 
 ## <a name="integrate-device-capabilities"></a>Intégrer les fonctionnalités de l’appareil

Après avoir accédé aux fonctionnalités de l’appareil, [](mobile-camera-image-permissions.md) utilisez Teams API de fonctionnalité multimédia pour intégrer des fonctionnalités multimédias à Teams plateforme afin d’améliorer l’expérience utilisateur. Ces fonctionnalités intégrées permettent à votre application de :

* Capturer et partager des images.
* Analysez la QR ou le code-barres à l’aide [du contrôle scanneur.](qr-barcode-scanner-capability.md)
* Enregistrez l’audio via le microphone.
* Partager l’emplacement à [l’aide du s picker d’emplacement.](location-capability.md)

En outre, vous pouvez intégrer [](people-picker-capability.md) le Teams sélecateur de personnes natives qui permet aux utilisateurs de rechercher et de sélectionner des personnes dans l’expérience d’application web.


