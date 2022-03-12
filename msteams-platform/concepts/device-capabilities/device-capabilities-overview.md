---
title: 'Fonctionnalités de l’appareil : vue d’ensemble'
author: Rajeshwari-v
description: Vue d’ensemble des fonctionnalités natives de l’appareil, telles que l’appareil photo, l’image, le média, le microphone, le micro, le code qr, etc.
ms.author: surbhigupta
keywords: Image de l’image de l’appareil photo microphone microphone qr code code-barres analyser les fonctionnalités natives d’autorisations de l’appareil
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 4febce3868df9fbba90cb4a94e67f6d0856606c9
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452689"
---
# <a name="device-capabilities"></a>Fonctionnalités de l’appareil

Microsoft Teams plateforme améliore en permanence les capacités des développeurs en s’alignant sur les expériences intégrées de la première partie. La plateforme Teams améliorée permet aux partenaires d’intégrer des fonctionnalités d’appareil, telles que l’appareil photo, le scanneur de QR ou de code-barres, la galerie de photos, le microphone et l’emplacement à leurs applications web. Cette intégration réduit le obstacle au développement d’applications, accélère le cycle de développement et crée de nouveaux scénarios ou cas d’utilisation pour la communauté des développeurs.

Les autorisations d’appareil sont différentes dans le navigateur. Auparavant, le navigateur  géré comment accorder des autorisations d’accès et maintenant ces autorisations sont gérées dans Microsoft Teams. Pour plus d’informations, voir [autorisations d’appareil de navigateur](browser-device-permissions.md).

## <a name="native-device-capabilities"></a>Fonctionnalités natives de l’appareil

Un appareil mobile ou de bureau dispose d’appareils intégrés, tels que l’appareil photo et le microphone, appelés fonctionnalités. Vous pouvez accéder aux fonctionnalités d’appareil suivantes sur mobile ou bureau via des API dédiées disponibles [dans Microsoft Teams SDK client JavaScript :](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)

* Fonctionnalités multimédias, telles que
  * Appareil photo
  * Microphone
  * Galerie
  * QR ou scanneur de code-barres
* Emplacement

Après avoir accédé aux fonctionnalités de l’appareil, vous pouvez les intégrer à la plateforme Teams pour améliorer l’expérience de collaboration.

## <a name="request-device-permissions"></a>Demande des autorisations d’appareil

Utilisez les outils présents [dans Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) pour demander les [autorisations requises pour accéder aux fonctionnalités natives](native-device-permissions.md) de l’appareil. Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour votre manifeste d’application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur Teams clients mobiles ou de bureau.

## <a name="integrate-device-capabilities"></a>Intégrer les fonctionnalités de l’appareil

Après avoir accédé aux fonctionnalités de l’appareil, utilisez Teams API de fonctionnalité multimédia [](mobile-camera-image-permissions.md) pour intégrer des fonctionnalités multimédias à la plateforme Teams pour améliorer l’expérience utilisateur. Ces fonctionnalités intégrées permettent à votre application de :

* Capturer et partager des images.
* Analysez la QR ou le code-barres à l’aide [du contrôle scanneur](qr-barcode-scanner-capability.md).
* Enregistrez l’audio via le microphone.
* Partager l’emplacement à [l’aide du s sélectionneur d’emplacement](location-capability.md).

En outre, vous pouvez intégrer le contrôle Teams sélecateur de personnes natives qui permet aux utilisateurs de rechercher et de sélectionner des personnes dans l’expérience d’application web.[](people-picker-capability.md)
