---
title: Demander des autorisations d’appareil pour votre application Microsoft Teams client
keywords: teams apps capabilities permissions device native scan qr barcode image audio video
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès à des fonctionnalités natives qui nécessitent généralement le consentement de l’utilisateur, telles que l’analyse qr, le code-barres, l’image, l’audio et les fonctionnalités vidéo
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 3cb15e82101be7df9f90c94928fa91ae570c14d5
ms.sourcegitcommit: a36760750ff4f510c374a4c956be57f7c1b4a0db
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/20/2022
ms.locfileid: "63674963"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Demander des autorisations d’appareil pour votre application Microsoft Teams client

Vous pouvez enrichir votre application Teams avec des fonctionnalités natives d’appareil, telles que la caméra, le microphone et l’emplacement. Ce document vous guide sur la façon de demander le consentement de l’utilisateur et d’accéder aux autorisations d’appareil natives.

> [!NOTE]
>
> * Pour intégrer des fonctionnalités multimédias dans Microsoft Teams application mobile, voir [Intégrer les fonctionnalités multimédias](mobile-camera-image-permissions.md).
> * Pour intégrer la fonctionnalité de QR ou de scanneur de code-barres dans votre application mobile Microsoft Teams, voir Intégrer la QR ou la fonctionnalité de scanneur de code-barres [dans Teams](qr-barcode-scanner-capability.md).
> * Pour intégrer des fonctionnalités d’emplacement dans Microsoft Teams application mobile, voir [Intégrer les fonctionnalités d’emplacement](location-capability.md).

## <a name="native-device-permissions"></a>Autorisations d’appareil natives

Vous devez demander les autorisations d’appareil pour accéder aux fonctionnalités natives de l’appareil. Les autorisations d’appareil fonctionnent de la même manière pour toutes les constructions d’application, telles que les onglets, les modules de tâche ou les extensions de messagerie. L’utilisateur doit se rendre sur la page d’autorisations Teams paramètres pour gérer les autorisations d’appareil.
En accédant aux fonctionnalités de l’appareil, vous pouvez créer des expériences plus riches sur la plateforme Teams, telles que :

* Capturer et afficher des images.
* Analysez la QR ou le code-barres.
* Enregistrez et partagez de courtes vidéos.
* Enregistrez les mémos audio et enregistrez-les pour une utilisation ultérieure.
* Utilisez les informations d’emplacement de l’utilisateur pour afficher les informations pertinentes.

> [!NOTE]
> * Actuellement, Teams ne prend pas en charge les autorisations d’appareil pour les applications multi-fenêtres, les onglets et le panneau latéral de la réunion.
> * Les autorisations d’appareil sont différentes dans le navigateur. Pour plus d’informations, voir [autorisations d’appareil de navigateur](browser-device-permissions.md).

## <a name="access-device-permissions"></a>Autorisations d’accès aux appareils

Le [Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) fournit les outils nécessaires à votre application mobile Teams pour accéder aux [autorisations](#manage-permissions) d’appareil de l’utilisateur et créer une expérience plus riche.

Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour le manifeste de votre application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur Teams client de bureau.

> [!NOTE]
> Actuellement, Microsoft Teams prise en charge des fonctionnalités multimédias et de scanneur de code-barres QR est disponible uniquement pour les clients mobiles.

## <a name="manage-permissions"></a>Gérer les autorisations

Un utilisateur peut gérer les autorisations d’appareil dans Teams paramètres en sélectionnant  Autoriser ou  refuser des autorisations pour des applications spécifiques.

# <a name="mobile"></a>[Mobile](#tab/mobile)

1. Ouvrez Teams.
1. Go to **Paramètres** >  **App Permissions**.
1. Sélectionnez l’application pour laquelle vous devez choisir les paramètres.
1. Sélectionnez les paramètres souhaités.

    ![Écran des paramètres mobiles des autorisations d’appareil](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

1. Ouvrez votre Teams application.
1. Sélectionnez votre icône de profil dans le coin supérieur droit de la fenêtre.
1. **Sélectionnez Paramètres** >  **Permissions** dans le menu déroulant.
1. Sélectionnez les paramètres souhaités.

   ![Écran des paramètres de bureau des autorisations d’appareil](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>Spécifier des autorisations

Mettez à jour les propriétés de votre `devicePermissions` application `manifest.json` en ajoutant et en spécifiant les cinq propriétés suivantes que vous utilisez dans votre application :

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

Après l’ajout `devicePermissions` au manifeste de votre application, vérifiez les autorisations à l’aide de **l’API d’autorisations HTML5** sans provoquer d’invite :

``` JavaScript
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

Tirez parti de l’API HTML5 ou Teams pour afficher une invite pour obtenir l’autorisation d’accès aux autorisations d’appareil.

> [!IMPORTANT]
>
> * Prise en charge `camera`de , `gallery`et `microphone` est activée par le biais [**de l’API selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Utilisez [**l’API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) pour une capture d’image unique.
> * La prise en charge `location` est activée via [**l’API getLocation**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Vous devez l’utiliser pour `getLocation API` l’emplacement, car l’API de géolocalisation HTML5 n’est actuellement pas entièrement prise en charge Teams client de bureau.

Par exemple :

* Pour demander à l’utilisateur d’accéder à son emplacement, vous devez appeler `getCurrentPosition()`:

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* Pour demander à l’utilisateur d’accéder à son appareil photo sur un ordinateur de bureau ou sur le web, vous devez appeler `getUserMedia()`:

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* Pour capturer l’image sur un appareil mobile, Teams mobile demande l’autorisation lorsque vous appelez `captureImage()`:

    ```JavaScript
            function captureImage() {
            microsoftTeams.media.captureImage((error, files) => {
                // If there's any error, an alert shows the error message/code
                if (error) {
                    if (error.message) {
                        alert(" ErrorCode: " + error.errorCode + error.message);
                    } else {
                        alert(" ErrorCode: " + error.errorCode);
                    }
                } else if (files) {
                    image = files[0].content;
                    // Adding this image string in src attr of image tag will display the image on web page.
                    let imageString = "data:" + item.mimeType + ";base64," + image;
                }
            });
        } 
    ```

* Les notifications inviteront l’utilisateur à appeler `requestPermission()`:

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* Pour utiliser l’appareil photo ou accéder à la galerie de photos, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()`:

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia(mediaInput, (error, attachments) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         } else if (attachments) {
             // creating image array which contains image string for all attached images. 
             const imageArray = attachments.map((item, index) => {
                 return ("data:" + item.mimeType + ";base64," + item.preview)
             })
         }
     });
    } 
  ```

* Pour utiliser le microphone, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()`:

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         }

         if (attachments) {
             // taking the first attachment  
             let audioResult = attachments[0];

             // setting audio string which can be used in Video tag
             let audioData = "data:" + audioResult.mimeType + ";base64," + audioResult.preview
         }
     });
     }
    ```

* Pour demander à l’utilisateur de partager un emplacement sur l’interface de carte, Teams mobile demande l’autorisation lorsque vous appelez `getLocation()`:

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[Mobile](#tab/mobile)

   ![Invite d’autorisations d’appareil mobile Onglets](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

   ![Invite d’autorisations d’appareil de bureau Onglets](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>Comportement des autorisations entre les sessions de connexion

Les autorisations d’appareil sont stockées pour chaque session de connexion. Cela signifie que si vous vous connectez à une autre instance de Teams, par exemple, sur un autre ordinateur, les autorisations de votre appareil à partir de vos sessions précédentes ne sont pas disponibles. Par conséquent, vous devez consentir à nouveau aux autorisations d’appareil pour la nouvelle session. Cela signifie également que, si vous vous dé connectez à Teams ou que vous changez de client dans Teams, les autorisations de votre appareil sont supprimées de la session de connexion précédente.  

> [!NOTE]
> Lorsque vous consentez aux autorisations natives de l’appareil, elle n’est valide que pour votre session _de_ connexion actuelle.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Node.js** |
|---------------|--------------|--------|
|Autorisations de l’appareil | Utiliser un exemple Microsoft Teams’onglet pour démontrer les autorisations de l’appareil |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Autorisations de périphérique pour le navigateur](browser-device-permissions.md)
* [Intégrer des fonctionnalités multimédias dans Teams](mobile-camera-image-permissions.md)
* [Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams](qr-barcode-scanner-capability.md)
* [Intégrer des fonctionnalités d’emplacement dans Teams](location-capability.md)
