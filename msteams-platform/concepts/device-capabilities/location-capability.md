---
title: Intégrer les fonctionnalités d’emplacement
author: Rajeshwari-v
description: Utilisation du SDK Teams client JavaScript pour tirer parti des fonctionnalités d’emplacement
keywords: autorisations natives d’appareil pour les fonctionnalités de carte d’emplacement
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b85f19e74d0a8121dd290fc395c1018178437b3a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566186"
---
# <a name="integrate-location-capabilities"></a>Intégrer les fonctionnalités d’emplacement 

Ce document vous guide sur l’intégration des fonctionnalités d’emplacement de l’appareil natif à votre application Teams web.  

Vous pouvez utiliser [Microsoft Teams SDK client JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit les outils nécessaires à votre application pour accéder aux fonctionnalités natives de l’appareil de l’utilisateur. [](native-device-permissions.md) Utilisez les API d’emplacement, telles [que getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) et [showLocation,](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) pour intégrer les fonctionnalités dans votre application. 

## <a name="advantages-of-integrating-location-capabilities"></a>Avantages de l’intégration des fonctionnalités d’emplacement

Le principal avantage de l’intégration des fonctionnalités d’emplacement dans vos applications Teams est qu’elle permet aux développeurs d’applications web sur la plateforme Teams d’exploiter les fonctionnalités d’emplacement avec Microsoft Teams SDK client JavaScript. 

Les exemples suivants montrent comment l’intégration des fonctionnalités d’emplacement est utilisée dans différents scénarios :
* Dans une usine, le responsable peut suivre la présence des employés en leur demandant de prendre un selfie à proximité de l’usine et de le partager via l’application spécifiée. Les données d’emplacement sont également capturées et envoyées avec l’image.
* Les fonctionnalités d’emplacement permettent au personnel de maintenance d’un fournisseur de services de partager des données d’état d’état authentiques des pylônes cellulaires avec la direction. La direction peut comparer toute insérialisation entre les informations d’emplacement capturées et les données envoyées par le personnel de maintenance.

Pour intégrer des fonctionnalités d’emplacement, vous devez mettre à jour le fichier manifeste de l’application et appeler les API. Pour une intégration efficace, vous devez bien comprendre les [extraits](#code-snippets) de code pour appeler les API d’emplacement. Il est important de vous familiariser avec les erreurs de réponse [d’API](#error-handling) pour gérer les erreurs dans votre Teams application.

> [!NOTE] 
> Actuellement, Microsoft Teams prise en charge des fonctionnalités de localisation est disponible uniquement pour les clients mobiles.

## <a name="update-manifest"></a>Mettre à jour le manifeste

Mettez à jour [Teams’applicationmanifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la `devicePermissions` propriété et en spécifiant `geolocation` . Il permet à votre application de demander les autorisations requises aux utilisateurs avant de commencer à utiliser les fonctionnalités de localisation.

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> **L’invite Demander des autorisations** s’affiche automatiquement lorsqu’une API Teams est lancée. Pour plus d’informations, voir [demander des autorisations d’appareil.](native-device-permissions.md)

## <a name="location-apis"></a>API d’emplacement

Vous devez utiliser l’ensemble d’API suivant pour activer les fonctionnalités d’emplacement de votre appareil :

| API      | Description   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | Fournit l’emplacement actuel de l’appareil de l’utilisateur ou ouvre le s picker d’emplacement natif et renvoie l’emplacement choisi par l’utilisateur. |
|[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | Affiche l’emplacement sur la carte. |

> [!NOTE]

> `getLocation()`L’API est livré avec les [configurations d’entrée suivantes](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)et `allowChooseLocation` `showMap` . <br/> Si la valeur est `allowChooseLocation` *true,* les utilisateurs peuvent choisir n’importe quel emplacement de leur choix.<br/>  Si la valeur est *false,* les utilisateurs ne peuvent pas modifier leur emplacement actuel.<br/> Si la valeur est `showMap` *false,* l’emplacement actuel est récupéré sans afficher la carte. `showMap` est ignoré si `allowChooseLocation` est définie sur *true*.

**Expérience d’application web pour les fonctionnalités de localisation** 
 ![ expérience d’application web pour les fonctionnalités de localisation](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>Gestion des erreurs

Vous devez vous assurer de gérer ces erreurs de manière appropriée dans votre Teams application. Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées : 

|Code d’erreur |  Nom de l’erreur     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plateforme actuelle.|
| **500** | INTERNAL_ERROR | Une erreur interne est rencontrée lors de l’opération requise.|
| **1000** | PERMISSION_DENIED |Autorisations d’emplacement refusées par l’utilisateur Teams’application ou l’application web.|
| **4000** | INVALID_ARGUMENTS | L’API est invoquée avec des arguments obligatoires erronés ou insuffisants.|
| **8000** | USER_ABORT |L’utilisateur a annulé l’opération.|
| **9000** | OLD_PLATFORM | L’utilisateur se trouve sur une ancienne build de plateforme où l’implémentation de l’API n’est pas présente. La mise à niveau de la build doit résoudre le problème.|

## <a name="code-snippets"></a>Extraits de code

**Api `getLocation` d’appel pour récupérer l’emplacement :**

```javascript
let locationProps = {"allowChooseLocation":true,"showMap":true};
microsoftTeams.location.getLocation(locationProps, (err: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
          if (err) {
            output(err);
            return;
          }
          output(JSON.stringify(location));
});
```

**Api `showLocation` d’appel pour afficher l’emplacement :**

```javascript
let location = {"latitude":17,"longitude":17};
microsoftTeams.location.showLocation(location, (err: microsoftTeams.SdkError, result: boolean) => {
          if (err) {
            output(err);
            return;
          }
     output(result);
});
```

## <a name="see-also"></a>Voir aussi

* [Intégrer des fonctionnalités multimédias dans Teams](mobile-camera-image-permissions.md)
* [Intégrer le code QR ou la fonctionnalité de scanneur de code-barres dans Teams](qr-barcode-scanner-capability.md)
