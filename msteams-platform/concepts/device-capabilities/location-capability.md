---
title: Intégrer les fonctionnalités d’emplacement
author: Rajeshwari-v
description: Apprenez à utiliser le SDK client JavaScript de Teams pour exploiter les fonctionnalités de localisation à l'aide d'extraits de code et d'échantillons.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 8290e78e9ea1baf87ce89642cd4f4f51b5f3c63d
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2022
ms.locfileid: "66842016"
---
# <a name="integrate-location-capabilities"></a>Intégrer les fonctionnalités d’emplacement

Vous pouvez intégrer les capacités de localisation de l'appareil natif à votre application Teams.  

Vous pouvez utiliser [Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), qui fournit les outils nécessaires à votre application pour accéder aux [fonctionnalités d’appareil natif](native-device-permissions.md) de l’utilisateur. Utilisez les API de localisation, telles que [getLocation](/javascript/api/@microsoft/teams-js/location.locationprops) et [showLocation](/javascript/api/@microsoft/teams-js/location.locationprops?), pour intégrer ces fonctionnalités dans votre application.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="advantages-of-integrating-location-capabilities"></a>Avantages de l'intégration des capacités de localisation

Le principal avantage de l'intégration des capacités de localisation dans vos applications Teams est qu'elle permet aux développeurs d'applications Web sur la plateforme Teams d'exploiter la fonctionnalité de localisation avec le SDK client JavaScript de Microsoft Teams.

Les exemples suivants montrent comment l'intégration des capacités de localisation est utilisée dans différents scénarios :

* Dans une usine, le superviseur peut suivre la présence des travailleurs en leur demandant de prendre un selfie à proximité de l'usine et de le partager via l'application spécifiée. Les données de localisation sont également capturées et envoyées avec l'image.
* Les capacités de localisation permettent au personnel de maintenance d'un fournisseur de services de partager des données authentiques sur l'état d’intégrité des tours cellulaires avec la direction. La direction peut comparer toute discordance entre les informations de localisation capturées et les données soumises par le personnel de maintenance.

Pour intégrer des fonctionnalités de localisation, vous devez mettre à jour le fichier manifeste de l'application et appeler les API. Pour une intégration efficace, vous devez avoir une bonne compréhension des [extraits de code](#code-snippets) pour appeler les API de localisation.
Il est important de vous familiariser avec les [Erreurs de réponse de l'API](#error-handling) pour gérer les erreurs dans votre application Teams.

> [!NOTE]
> Actuellement, la prise en charge des capacités de localisation de Microsoft Teams n'est disponible que pour les clients mobiles.

## <a name="update-manifest"></a>Mise à jour du manifeste

Mettez à jour le fichier [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) de votre application Teams en ajoutant la `devicePermissions`propriété et en spécifiant`geolocation`. Il permet à votre application de demander les autorisations nécessaires aux utilisateurs avant qu'ils ne commencent à utiliser les fonctions de localisation. La mise à jour du manifeste de l’application est la suivante :

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
>
> * L'invite **Demander des autorisations** s'affiche automatiquement lorsqu'une API Teams pertinente est lancée. Pour plus d'informations, reportez-vous à la section [Demander les autorisations de l'appareil](native-device-permissions.md).
> * Les autorisations de l'appareil sont différentes dans le navigateur. Pour plus d'informations, voir les [autorisations d'appareil de navigation](browser-device-permissions.md).

## <a name="location-apis"></a>API de localisation

Vous devez utiliser l'ensemble des API suivantes pour activer les capacités de localisation de votre appareil :

| API      | Description   |
| --- | --- |
|[getLocation()](/javascript/api/@microsoft/teams-js/location.locationprops) | Donne l'emplacement actuel de l'appareil de l'utilisateur ou ouvre le sélecteur d'emplacement natif et renvoie l'emplacement choisi par l'utilisateur. |
|[showLocation](/javascript/api/@microsoft/teams-js/location.locationprops?) | Affiche l’emplacement sur la carte. |

> [!NOTE]
> L'`getLocation()`API s'accompagne des configurations[ d'entrée suivantes](/javascript/api/@microsoft/teams-js/microsoftteams.location.locationprops), `allowChooseLocation`et`showMap`.<br/> Si la valeur de `allowChooseLocation`est *vraie*, alors les utilisateurs peuvent choisir l'emplacement de leur choix.<br/>  Si la valeur est *false*, les utilisateurs ne peuvent pas modifier leur emplacement actuel.<br/> Si la valeur est `showMap` *faux*, l’emplacement actuel est extrait sans afficher la carte. `showMap` est ignorée si `allowChooseLocation`elle est définie à *vrai*.

L'image suivante montre l'expérience de l'application web en matière de localisation :

![expérience des applications web pour les capacités de localisation](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a>Extraits de code

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

**Appel de `getLocation`l'API pour récupérer l'emplacement :**

```javascript
import {location} from "@microsoft/teams-js"

let locationProps = {"allowChooseLocation":true,"showMap":true};
if(location.isSupported()) {
    const locationPromise = location.getLocation(locationProps);
    locationPromise.
        then((result) => {output(JSON.stringify(result));}.
        catch((error) => {output(error);});
}
else {/*Handle case where capability isn't supported */}
```

**Appel `showLocation` API pour afficher l'emplacement :**

```javascript
import {location} from "@microsoft/teams-js"

let location = {"latitude":17,"longitude":17};
if(location.isSupported()) {
    const locationPromise = location.showLocation(location);
    locationPromise.
         then((result) => {/*Successful map display*/}).
         catch((error) => {/*Failed map display*/});
}
else {/*Handle case where capability isn't supported */}
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

**Appel de `getLocation`l'API pour récupérer l'emplacement :**

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

**Appel `showLocation` API pour afficher l'emplacement :**

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

---

## <a name="error-handling"></a>Gestion des erreurs

Vous devez vous assurer de traiter ces erreurs de manière appropriée dans votre application Teams. Le tableau suivant répertorie les codes d'erreur et les conditions dans lesquelles les erreurs sont générées :

|Code d’erreur |  Nom de l’erreur     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plateforme actuelle.|
| **500** | INTERNAL_ERROR | Une erreur interne a été rencontrée lors de l'exécution de l'opération requise.|
| **1 000** | PERMISSION_DENIED |L'utilisateur s'est vu refuser les droits d'accès à l'application Teams ou à l'application web.|
| **4000** | ARGUMENTS NON VALIDES | L’API est appelée avec des arguments obligatoires incorrects ou insuffisants.|
| **8000** | USER_ABORT |L’utilisateur a annulé l’opération.|
| **9000** | OLD_PLATFORM | L'utilisateur est sur une ancienne build de plateforme où l'implémentation de l'API n'est pas présente. La mise à jour de la compilation devrait résoudre le problème.|

### <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Localisation actuelle dans l'application | Les utilisateurs peuvent enregistrer l'emplacement actuel et visualiser tous les enregistrements précédents.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Intégrer les fonctionnalités médias](media-capabilities.md)
* [Intégrer le code QR ou la fonctionnalité de scanneur de code-barres dans Teams](qr-barcode-scanner-capability.md)
* [Intégrer le sélecteur de personnes dans Teams](people-picker-capability.md)
