---
title: Demander des autorisations d’appareil pour votre application Microsoft Teams client
keywords: autorisations des fonctionnalités des applications Teams
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui nécessitent généralement le consentement de l’utilisateur
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 920ab47a60340fd9a14e4f5dfb2e39a8ad8f3a89
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994349"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Demander des autorisations d’appareil pour votre application Microsoft Teams client

Vous pouvez enrichir votre application Teams avec des fonctionnalités natives d’appareil, telles que la caméra, le microphone et l’emplacement. Ce document vous guide sur la façon de demander le consentement de l’utilisateur et d’accéder aux autorisations natives de l’appareil.

> [!NOTE]
> * Pour intégrer des fonctionnalités multimédias dans Microsoft Teams application mobile, voir [Intégrer les fonctionnalités multimédias.](mobile-camera-image-permissions.md)
> * Pour intégrer la fonctionnalité de QR ou de scanneur de code-barres dans votre application mobile Microsoft Teams, voir Intégrer la [QR](qr-barcode-scanner-capability.md)ou la fonctionnalité de scanneur de code-barres dans Teams .
> * Pour intégrer des fonctionnalités d’emplacement dans Microsoft Teams application mobile, voir [Intégrer les fonctionnalités d’emplacement.](location-capability.md)

## <a name="native-device-permissions"></a>Autorisations d’appareil natives

Vous devez demander les autorisations d’appareil pour accéder aux fonctionnalités natives de l’appareil. Les autorisations d’appareil fonctionnent de la même manière pour toutes les constructions d’application, telles que les onglets, les modules de tâche ou les extensions de messagerie. L’utilisateur doit se rendre sur la page d’autorisations Teams paramètres pour gérer les autorisations d’appareil.
En accédant aux fonctionnalités de l’appareil, vous pouvez créer des expériences plus riches sur la plateforme Teams, telles que :
* Capturer et afficher des images.
* Analysez la QR ou le code-barres.
* Enregistrez et partagez de courtes vidéos.
* Enregistrez les mémos audio et enregistrez-les pour une utilisation ultérieure.
* Utilisez les informations d’emplacement de l’utilisateur pour afficher les informations pertinentes.

> [!NOTE]
> Actuellement, Teams ne prend pas en charge les autorisations d’appareil pour les applications à fenêtres multiples, les onglets et le bureau secondaire de la réunion. 

## <a name="access-device-permissions"></a>Autorisations d’accès aux appareils

Le [Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) fournit les outils nécessaires à votre application mobile Teams pour accéder aux [autorisations](#manage-permissions) d’appareil de l’utilisateur et créer une expérience plus riche.

Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour votre manifeste d’application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur Teams client de bureau.

> [!NOTE] 
> Actuellement, Microsoft Teams prise en charge des fonctionnalités multimédias et de scanneur de code-barres QR est disponible uniquement pour les clients mobiles.

## <a name="manage-permissions"></a>Gérer les autorisations

Un utilisateur peut gérer les autorisations d’appareil  Teams  paramètres en sélectionnant Autoriser ou refuser des autorisations pour des applications spécifiques.
 
# <a name="desktop"></a>[Bureau](#tab/desktop)

1. Ouvrez votre Teams application.
1. Sélectionnez votre icône de profil dans le coin supérieur droit de la fenêtre.
1. Sélectionnez **Paramètres**  >  **autorisations** dans le menu déroulant.
1. Sélectionnez les paramètres souhaités.

   ![Écran des paramètres de bureau des autorisations d’appareil](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

1. Ouvrez Teams.
1. Go to **Paramètres**  >  **App Permissions**.
1. Sélectionnez l’application pour laquelle vous devez choisir les paramètres.
1. Sélectionnez les paramètres souhaités.

    ![Écran des paramètres mobiles des autorisations d’appareil](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>Spécifier des autorisations

Mettez à jour les propriétés de votre application en ajoutant et en spécifiant les cinq propriétés que vous `manifest.json` utilisez dans votre application `devicePermissions` :

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement :

| Propriété      | Description   |
| --- | --- |
| media         | Autorisation d’utiliser la caméra, le microphone, les haut-parleurs et d’accéder à la galerie multimédia. |
| géolocalisation   | Autorisation de renvoyer l’emplacement de l’utilisateur.      |
| notifications | Autorisation d’envoyer des notifications à l’utilisateur.      |
| midi          | Autorisation d’envoyer et de recevoir des informations MIDI (Music Instrument Digital Interface) à partir d’un instrument de musique numérique.   |
| openExternal  | Autorisation d’ouvrir des liens dans des applications externes.  |

## <a name="check-permissions-from-your-app"></a>Vérifier les autorisations de votre application

Après l’ajout au manifeste de votre application, vérifiez les autorisations à l’aide de `devicePermissions` **l’API d’autorisations HTML5** sans provoquer d’invite :

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

## <a name="use-teams-apis-to-get-device-permissions"></a>Utiliser Teams API pour obtenir des autorisations d’appareil

Tirez parti de l’API HTML5 ou Teams appropriée pour afficher une invite pour obtenir l’autorisation d’accès aux autorisations d’appareil.

> [!IMPORTANT]
> * Prise en `camera` charge de , et est activée par le biais de `gallery` `microphone` [**l’API selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Utilisez [**l’API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) pour une capture d’image unique.
> * La prise `location` en charge est activée via [**l’API getLocation.**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) Vous devez l’utiliser pour l’emplacement, car l’API de géolocalisation HTML5 n’est actuellement pas entièrement prise `getLocation API` en charge Teams client de bureau.

Par exemple :
 * Pour demander à l’utilisateur d’accéder à son emplacement, vous devez appeler `getCurrentPosition()` :

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * Pour demander à l’utilisateur d’accéder à son appareil photo sur un ordinateur de bureau ou sur le web, vous devez appeler `getUserMedia()` :

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * Pour capturer l’image sur un appareil mobile, Teams mobile demande l’autorisation lorsque vous appelez `captureImage()` :

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * Les notifications inviteront l’utilisateur à appeler `requestPermission()` :

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* Pour utiliser l’appareil photo ou accéder à la galerie de photos, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()` :

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* Pour utiliser le microphone, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()` :

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* Pour demander à l’utilisateur de partager un emplacement sur l’interface de carte, Teams mobile demande l’autorisation lorsque vous appelez `getLocation()` :

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[Bureau](#tab/desktop)

   ![Invite d’autorisations d’appareil de bureau Onglets](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

   ![Invite d’autorisations d’appareil mobile Onglets](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>Comportement des autorisations entre les sessions de connexion

Les autorisations d’appareil sont stockées pour chaque session de connexion. Cela signifie que si vous vous connectez à une autre instance de Teams, par exemple, sur un autre ordinateur, les autorisations de votre appareil à partir de vos sessions précédentes ne sont pas disponibles. Par conséquent, vous devez consentir à nouveau aux autorisations d’appareil pour la nouvelle session. Cela signifie également que, si vous vous dé connectez à Teams ou que vous changez de client dans Teams, les autorisations de votre appareil sont supprimées de la session de connexion précédente.  

> [!NOTE]
> Lorsque vous consentez aux autorisations natives de l’appareil, elle n’est valide que pour votre session _de_ connexion actuelle.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Intégrer des fonctionnalités multimédias dans Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Intégrer des fonctionnalités d’emplacement dans Teams](location-capability.md)
