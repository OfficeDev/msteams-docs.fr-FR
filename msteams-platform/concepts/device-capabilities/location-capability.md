---
title: Intégrer les fonctionnalités d’emplacement
author: Rajeshwari-v
description: Comment utiliser le client JavaScript SDK Teams tirer parti des capacités de localisation
keywords: fonctionnalités de carte de localisation autorisations d’appareil natif
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

Ce document vous guide sur la façon d’intégrer les capacités de localisation de l’appareil natif à votre Teams appe.  

Vous pouvez utiliser [Microsoft Teams client JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), qui fournit les outils nécessaires pour que votre application accède aux fonctionnalités de l’appareil [natif de l’utilisateur.](native-device-permissions.md) Utilisez les API de localisation, telles que [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) et [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) pour intégrer les fonctionnalités de votre application. 

## <a name="advantages-of-integrating-location-capabilities"></a>Avantages de l’intégration des capacités de localisation

Le principal avantage de l’intégration des fonctionnalités de localisation dans vos applications Teams est qu’il permet aux développeurs d’applications Web sur la plate-forme Teams de tirer parti des fonctionnalités de localisation avec Microsoft Teams client JavaScript SDK. 

Des exemples suivants montrent comment l’intégration des capacités de localisation est utilisée dans différents scénarios :
* Dans une usine, le superviseur peut suivre la présence des travailleurs en leur demandant de prendre un selfie à proximité de l’usine et de le partager via l’application spécifiée. Les données de localisation sont également capturées et envoyées avec l’image.
* Les capacités de localisation permettent au personnel d’entretien d’un fournisseur de services de partager les données de santé authentiques des tours cellulaires avec la direction. La direction peut comparer n’importe quel décalage entre les informations de localisation saisies et les données soumises par le personnel de maintenance.

Pour intégrer les fonctionnalités de localisation, vous devez mettre à jour le fichier manifeste de l’application et appeler les API. Pour une intégration efficace, vous devez avoir une bonne compréhension des [extraits de code pour appeler](#code-snippets) les API de localisation. Il est important de vous familiariser avec les erreurs [de réponse API](#error-handling) pour gérer les erreurs dans votre application Teams apprité.

> [!NOTE] 
> Actuellement, le Microsoft Teams pour les capacités de localisation n’est disponible que pour les clients mobiles.

## <a name="update-manifest"></a>Manifeste de mise à jour

Mettez à jour Teams application [manifest.jsdans le](../../resources/schema/manifest-schema.md#devicepermissions) fichier en ajoutant la propriété et en `devicePermissions` spécifier `geolocation` . Il permet à votre application de demander les autorisations requises aux utilisateurs avant qu’ils ne commencent à utiliser les fonctionnalités de localisation.

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> **L’invite autorisations** de demande s’affiche automatiquement lorsqu’une Teams api est lancée. Pour plus d’informations, consultez les [autorisations de l’appareil de demande](native-device-permissions.md).

## <a name="location-apis"></a>API de localisation

Vous devez utiliser l’ensemble d’API suivants pour activer les capacités de localisation de votre appareil :

| API      | Description   |
| --- | --- |
|[getLocation (en)](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | Donne l’emplacement actuel de l’appareil de l’utilisateur ou ouvre le cueilleur de localisation natif et renvoie l’emplacement choisi par l’utilisateur. |
|[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | Affiche l’emplacement sur la carte. |

> [!NOTE]

> `getLocation()`L’API est livré avec les [configurations d’entrée suivantes](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` et `showMap` . <br/> Si la valeur est `allowChooseLocation` *vraie, alors les* utilisateurs peuvent choisir n’importe quel endroit de leur choix.<br/>  Si la valeur est *fausse,* alors les utilisateurs ne peuvent pas modifier leur emplacement actuel.<br/> Si la valeur est `showMap` *fausse,* l’emplacement actuel est récupéré sans afficher la carte. `showMap` est ignoré si `allowChooseLocation` est mis à *vrai*.

**Expérience d’application Web pour les fonctionnalités de localisation** 
 ![ expérience d’application web pour les fonctionnalités de localisation](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>Gestion des erreurs

Vous devez vous assurer de gérer ces erreurs de manière appropriée dans Teams application. Le tableau suivant énumère les codes d’erreur et les conditions dans lesquelles les erreurs sont générées : 

|Code d’erreur |  Nom de l’erreur     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plate-forme actuelle.|
| **500** | INTERNAL_ERROR | L’erreur interne est rencontrée lors de l’exécution de l’opération requise.|
| **1000** | PERMISSION_DENIED |Utilisateur refusé les autorisations de localisation à l Teams appe ou l’application Web .|
| **4000** | INVALID_ARGUMENTS | L’API est invoquée avec des arguments obligatoires erronés ou insuffisants.|
| **8000** | USER_ABORT |L’utilisateur a annulé l’opération.|
| **9000** | OLD_PLATFORM | L’utilisateur est sur l’ancienne plate-forme de construction où la mise en œuvre de l’API n’est pas présente. La mise à niveau de la build devrait résoudre le problème.|

## <a name="code-snippets"></a>Extraits de code

**Appel `getLocation` api pour récupérer l’emplacement:**

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

**Appel `showLocation` api pour afficher l’emplacement :**

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

* [Intégrer les capacités des médias dans Teams](mobile-camera-image-permissions.md)
* [Intégrer la capacité de scanner de code QR ou de code à barres dans Teams](qr-barcode-scanner-capability.md)
