---
title: Demandez des autorisations d’appareil pour votre application Microsoft Teams’utilisateur
keywords: équipes apps fonctionnalités autorisations
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui nécessitent généralement le consentement de l’utilisateur
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 34f84285dc883cc474cf1720c42b1699f76c6653
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566179"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Demandez des autorisations d’appareil pour votre application Microsoft Teams’utilisateur

Vous pouvez enrichir votre application Teams avec des fonctionnalités d’appareil natives, telles que la caméra, le microphone et l’emplacement. Ce document vous guide sur la façon de demander le consentement de l’utilisateur et d’accéder aux autorisations de l’appareil natif.

> [!NOTE]
> * Pour intégrer les capacités multimédias dans votre Microsoft Teams mobile, consultez [Intégrer les capacités multimédias](mobile-camera-image-permissions.md).
> * Pour intégrer la capacité de scanner QR ou code à barres dans votre application mobile Microsoft Teams, consultez [la capacité de scanner QR ou code à barres dans Teams](qr-barcode-scanner-capability.md).
> * Pour intégrer les fonctionnalités de localisation dans votre Microsoft Teams mobile, consultez les [fonctionnalités de localisation Intégrer](location-capability.md).

## <a name="native-device-permissions"></a>Autorisations d’appareils indigènes

Vous devez demander aux périphériques l’autorisation d’accéder aux fonctionnalités de l’appareil natif. Les autorisations d’appareil fonctionnent de la même manière pour toutes les constructions d’applications, telles que les onglets, les modules de tâches ou les extensions de messagerie. L’utilisateur doit se rendre à la page d’autorisations dans Teams pour gérer les autorisations de périphérique.
En accédant aux fonctionnalités de l’appareil, vous pouvez créer des expériences plus riches sur la Teams de base, telles que :
* Capturez et visualisez des images.
* Scannez QR ou code à barres.
* Enregistrez et partagez de courtes vidéos.
* Enregistrez les notes audio et enregistrez-les pour une utilisation ultérieure.
* Utilisez les informations de localisation de l’utilisateur pour afficher les informations pertinentes.

## <a name="access-device-permissions"></a>Autorisations d’accès à l’appareil

Le [client JavaScript Microsoft Teams SDK fournit les](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) outils nécessaires à votre application mobile Teams pour accéder aux autorisations de l’appareil de [l’utilisateur et](#manage-permissions) construire une expérience plus riche.

Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs Web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour le manifeste de votre application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur Teams client de bureau.

> [!NOTE] 
> Actuellement, le Microsoft Teams des capacités multimédias et de la capacité de scanner de codes à barres QR n’est disponible que pour les clients mobiles.

## <a name="manage-permissions"></a>Gérer les autorisations

Un utilisateur peut gérer les autorisations d’Teams paramètres en sélectionnant **autoriser** ou **refuser des** autorisations à des applications spécifiques.
 
# <a name="desktop"></a>[Desktop](#tab/desktop)

1. Ouvrez votre application Teams’argent.
1. Sélectionnez votre icône de profil dans le coin supérieur droit de la fenêtre.
1. Sélectionnez **Paramètres**  >  **autorisations** de base dans le menu drop-down.
1. Sélectionnez les paramètres souhaités.

   ![L’appareil autorise l’écran des paramètres de bureau](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

1. Ouvrez Teams.
1. Allez à **Paramètres**  >  **App Permissions**.
1. Sélectionnez l’application pour laquelle vous devez choisir les paramètres.
1. Sélectionnez les paramètres souhaités.

    ![L’appareil autorise l’écran des paramètres mobiles](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Spécifier les autorisations

Mettez à jour vos applications `manifest.json` en ajoutant et en `devicePermissions` spécifier les cinq propriétés que vous utilisez dans votre application :

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Chaque propriété vous permet d’inciter l’utilisateur à demander son consentement :

| Propriété      | Description   |
| --- | --- |
| media         | Autorisation d’utiliser la caméra, le microphone, les haut-parleurs et la galerie multimédia d’accès. |
| géolocalisation   | Autorisation de retourner l’emplacement de l’utilisateur.      |
| Notifications | Autorisation d’envoyer les notifications de l’utilisateur.      |
| Midi          | Autorisation d’envoyer et de recevoir des informations sur l’interface numérique des instruments de musique (MIDI) à partir d’un instrument de musique numérique.   |
| openExternal  | Autorisation d’ouvrir des liens dans des applications externes.  |

## <a name="check-permissions-from-your-app"></a>Vérifiez les autorisations de votre application

Après avoir ajouté `devicePermissions` à votre manifeste d’application, vérifiez les autorisations en **utilisant l’API des autorisations HTML5** sans provoquer d’invite :

``` Javascript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="use-teams-apis-to-get-device-permissions"></a>Utilisez Teams pour obtenir les autorisations de l’appareil

Tirez parti des données HTML5 ou Teams API appropriées pour afficher une invite à obtenir le consentement aux autorisations de l’appareil d’accès.

> [!IMPORTANT]
> * Prise en `camera` charge pour , et est activé par `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Utilisez [**l’API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) pour une seule capture d’image.
> * La prise en `location` charge est activée [**grâce à getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Vous devez l’utiliser `getLocation API` pour l’emplacement, car l’API de géolocalisation HTML5 n’est actuellement pas entièrement prise en charge Teams client de bureau.

Par exemple :
 * Pour inciter l’utilisateur à accéder à son emplacement, vous devez appeler `getCurrentPosition()` :

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Pour inciter l’utilisateur à accéder à son appareil photo sur le bureau ou le Web, vous devez appeler `getUserMedia()` :

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Pour capturer l’image sur mobile, Teams mobile vous demande la permission lorsque vous appelez `captureImage()` :

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * Les notifications inviteront l’utilisateur lorsque vous appelez `requestPermission()` :

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Pour utiliser l’appareil photo ou accéder à la galerie de photos, Teams mobile vous demande la permission lorsque vous appelez `selectMedia()` :

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Pour utiliser le microphone, Teams mobile vous demande la permission lorsque vous appelez `selectMedia()` :

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Pour inciter l’utilisateur à partager l’emplacement sur l’interface de la carte, Teams mobile demande la permission lorsque vous appelez `getLocation()` :

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Desktop](#tab/desktop)

   ![Les autorisations des périphériques de bureau tabs invitent](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

   ![Les autorisations des appareils mobiles tabs invitent](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Comportement d’autorisation à travers les sessions de connexion

Les autorisations d’appareil sont stockées pour chaque session de connexion. Cela signifie que si vous vous connectez à une autre instance de Teams, par exemple, sur un autre ordinateur, les autorisations de votre appareil de vos sessions précédentes ne sont pas disponibles. Par conséquent, vous devez consentir à nouveau aux autorisations de périphérique pour la nouvelle session. Cela signifie également que si vous vous déconnectez de Teams ou changez de locataire en Teams, les autorisations de votre appareil sont supprimées de la session de connexion précédente.  

> [!NOTE]
> Lorsque vous consentez aux autorisations de l’appareil natif, il n’est valable que pour _votre session_ de connexion actuelle.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Intégrer les capacités des médias dans Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Intégrer la capacité de scanner QR ou de code à barres dans Teams](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Intégrer les capacités de localisation dans Teams](location-capability.md)
