---
title: Demander des autorisations d’appareil pour votre application Microsoft Teams
keywords: Les fonctionnalités d’applications Teams autorisent la vidéo audio de l’image de code-barres qr d’analyse native de l’appareil
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès à des fonctionnalités natives qui nécessitent généralement le consentement de l’utilisateur, telles que l’analyse qr, le code-barres, l’image, l’audio, les fonctionnalités vidéo
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 5269aed130714bc9afbe97b170d955d79d79abc8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103305"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Demander des autorisations d’appareil pour votre application Microsoft Teams

Vous pouvez enrichir votre application Teams avec des fonctionnalités d’appareil natives, telles que la caméra, le microphone et l’emplacement. Ce document vous guide sur la façon de demander le consentement de l’utilisateur et d’accéder aux autorisations d’appareil natif.

> [!NOTE]
>
> * Pour intégrer des fonctionnalités multimédias dans votre application mobile Microsoft Teams, consultez [Intégrer les fonctionnalités multimédias](mobile-camera-image-permissions.md).
> * Pour intégrer la fonctionnalité de QR ou de scanneur de codes-barres dans votre application mobile Microsoft Teams, consultez [Intégrer la QR ou la fonctionnalité de scanneur de codes-barres dans Teams](qr-barcode-scanner-capability.md).
> * Pour intégrer des fonctionnalités d’emplacement dans votre application mobile Microsoft Teams, consultez [Intégrer les fonctionnalités d’emplacement](location-capability.md).

## <a name="native-device-permissions"></a>Autorisations d’appareil natives

Vous devez demander les autorisations d’appareil pour accéder aux fonctionnalités natives de l’appareil. Les autorisations d’appareil fonctionnent de la même façon pour toutes les constructions d’application, telles que les onglets, les modules de tâches ou les extensions de message. L’utilisateur doit accéder à la page des autorisations dans Teams paramètres pour gérer les autorisations de l’appareil.
En accédant aux fonctionnalités de l’appareil, vous pouvez créer des expériences plus riches sur la plateforme Teams, par exemple :

* Capturez et affichez des images.
* Analysez QR ou code-barres.
* Enregistrez et partagez de courtes vidéos.
* Enregistrez les mémos audio et enregistrez-les pour une utilisation ultérieure.
* Utilisez les informations d’emplacement de l’utilisateur pour afficher les informations pertinentes.

> [!NOTE]
> * Actuellement, Teams ne prend pas en charge les autorisations d’appareil pour les applications multi-fenêtres, les onglets et le panneau côté réunion.
> * Les autorisations d’appareil sont différentes dans le navigateur. Pour plus d’informations, consultez [les autorisations d’appareil du navigateur](browser-device-permissions.md).

## <a name="access-device-permissions"></a>Accéder aux autorisations d’appareil

Le [kit de développement logiciel (SDK) client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) fournit les outils nécessaires à votre application mobile Teams pour accéder aux [autorisations d’appareil](#manage-permissions) de l’utilisateur et créer une expérience plus riche.

Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour le manifeste de votre application. Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur le client de bureau Teams.

> [!NOTE]
> Actuellement, Microsoft Teams prise en charge des fonctionnalités multimédias et du scanneur de codes-barres QR est disponible uniquement pour les clients mobiles.

## <a name="manage-permissions"></a>Gérer les autorisations

Un utilisateur peut gérer les autorisations d’appareil dans Teams paramètres en sélectionnant **Autoriser** ou **refuser** des autorisations sur des applications spécifiques.

# <a name="mobile"></a>[Mobile](#tab/mobile)

1. Ouvrez Teams.
1. Accédez à **Paramètres** >  **App Permissions**.
1. Sélectionnez l’application pour laquelle vous devez choisir les paramètres.
1. Sélectionnez les paramètres souhaités.

    ![Écran des paramètres mobiles des autorisations d’appareil](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

1. Ouvrez votre application Teams.
1. Sélectionnez l’icône de votre profil dans le coin supérieur droit de la fenêtre.
1. Sélectionnez **Paramètres** >  **Permissions** dans le menu déroulant.
1. Sélectionnez les paramètres souhaités.

   ![Écran des paramètres de bureau des autorisations d’appareil](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>Spécifier des autorisations

Mettez à jour vos applications `manifest.json` en ajoutant `devicePermissions` et en spécifiant les cinq propriétés suivantes que vous utilisez dans votre application :

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
| Médias         | Autorisation d’utiliser la caméra, le microphone, les haut-parleurs et la galerie multimédia d’accès. |
| Géolocalisation   | Autorisation de retourner l’emplacement de l’utilisateur.      |
| Notifications | Autorisation d’envoyer les notifications utilisateur.      |
| Midi          | Autorisation d’envoyer et de recevoir des informations midi (Musical Instrument Digital Interface) à partir d’un instrument de musique numérique.   |
| openExternal  | Autorisation d’ouvrir des liens dans des applications externes.  |

## <a name="check-permissions-from-your-app"></a>Vérifier les autorisations de votre application

Après avoir ajouté `devicePermissions` le manifeste de votre application, vérifiez les autorisations à l’aide de **l’API d’autorisations HTML5** sans provoquer d’invite :

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

Tirez parti de l’API HTML5 ou Teams appropriée pour afficher une invite d’obtention du consentement pour accéder aux autorisations d’appareil.

> [!IMPORTANT]
>
> * Prise en charge de `camera`, `gallery`et `microphone` est activée via [**l’API selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true). Utilisez [**l’API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) pour une capture d’image unique.
> * La prise `location` en charge est activée via [**l’API getLocation**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Vous devez l’utiliser `getLocation API` pour l’emplacement, car l’API de géolocalisation HTML5 n’est actuellement pas entièrement prise en charge sur Teams client de bureau.

Par exemple :

* Pour inviter l’utilisateur à accéder à son emplacement, vous devez appeler `getCurrentPosition()`:

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* Pour inviter l’utilisateur à accéder à son appareil photo sur le bureau ou sur le web, vous devez appeler `getUserMedia()`:

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* Pour capturer l’image sur un appareil mobile, Teams mobile vous demande l’autorisation d’appeler `captureImage()`:

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

* Les notifications invitent l’utilisateur quand vous appelez `requestPermission()`:

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* Pour utiliser la caméra ou accéder à la galerie de photos, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()`:

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

* Pour inviter l’utilisateur à partager l’emplacement sur l’interface de carte, Teams mobile demande l’autorisation lorsque vous appelez `getLocation()`:

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[Mobile](#tab/mobile)

   ![Invite d’autorisations des appareils mobiles Tabs](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

   ![Invite d’autorisations de l’appareil de bureau Tabs](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>Comportement des autorisations entre les sessions de connexion

Les autorisations d’appareil sont stockées pour chaque session de connexion. Cela signifie que si vous vous connectez à une autre instance de Teams, par exemple, sur un autre ordinateur, les autorisations de votre appareil à partir de vos sessions précédentes ne sont pas disponibles. Par conséquent, vous devez donner à nouveau votre consentement aux autorisations d’appareil pour la nouvelle session. Cela signifie également que si vous vous déconnectez de Teams ou que vous changez de locataire dans Teams, les autorisations de votre appareil sont supprimées de la session de connexion précédente.  

> [!NOTE]
> Lorsque vous consentez aux autorisations d’appareil natif, elle est valide uniquement pour votre session _de connexion actuelle_ .

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Node.js** |
|---------------|--------------|--------|
|Autorisations de l’appareil | Utiliser Microsoft Teams’exemple d’application d’onglet pour illustrer les autorisations d’appareil |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Autorisations de périphérique pour le navigateur](browser-device-permissions.md)
* [Intégrer les fonctionnalités médias](mobile-camera-image-permissions.md)
* [Intégrer la fonctionnalité de QR ou de scanneur de codes-barres dans Teams](qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement sur Teams](location-capability.md)
