---
title: Demander des autorisations d’appareil pour votre onglet
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui nécessitent généralement le consentement de l’utilisateur
ms.topic: how-to
keywords: développement d’onglets teams
ms.openlocfilehash: a2893fb2905584eac4b398287d431f406c23b12b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014529"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Demander des autorisations d’appareil pour votre onglet Microsoft Teams

Vous souhaitez peut-être enrichir votre onglet avec des fonctionnalités qui nécessitent l’accès aux fonctionnalités natives de l’appareil, telles que :

> [!div class="checklist"]
>
> * Appareil photo
> * Microphone
> * Lieu
> * Notifications

> [!NOTE]
> Pour intégrer des fonctionnalités d’appareil photo et d’image dans votre application mobile Microsoft Teams, voir fonctionnalités d’appareil photo et [d’image dans Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!IMPORTANT]
>
> * Pour l’instant, le client mobile Teams prend uniquement en charge l’accès aux fonctionnalités d’appareils natifs, ainsi qu’aux fonctionnalités de l’appareil natif, et il est disponible sur toutes les constructions d’application, y compris `camera` `gallery` les `mic` `location` onglets. </br>
> * Prise en `camera` charge de , et est activée par le biais de `gallery` `mic` [**l’API selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Pour une capture d’image unique, vous pouvez utiliser [**l’API captureImage.**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)
> * La prise `location` en charge est activée via [**l’API getLocation.**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) Il est recommandé d’utiliser cette API comme API de [**géolocalisation**](../../resources/schema/manifest-schema.md#devicepermissions) n’est actuellement pas entièrement prise en charge sur tous les clients de bureau.

## <a name="device-permissions"></a>Autorisations de l’appareil

L’accès aux autorisations d’appareil d’un utilisateur vous permet de créer des expériences beaucoup plus riches, par exemple :

* Enregistrer et partager de courtes vidéos
* Enregistrez de courtes mémos audio et enregistrez-les pour plus tard
* Utiliser les informations d’emplacement de l’utilisateur pour afficher les informations pertinentes

Bien que l’accès à ces fonctionnalités soit standard dans la plupart des navigateurs web modernes, vous devez faire savoir à Teams les fonctionnalités que vous souhaitez utiliser en mettant à jour votre manifeste d’application. Cela vous permettra de demander des autorisations, comme vous le feriez dans un navigateur, pendant que votre application est en cours d’exécution sur le client de bureau Teams.

## <a name="manage-permissions"></a>Gérer les autorisations

# <a name="desktop"></a>[Desktop](#tab/desktop)

1. Ouvrez Teams.
1. Dans le coin supérieur droit de la fenêtre, sélectionnez l’icône de votre profil.
1. Sélectionnez **Les**  ->  **autorisations des paramètres** dans le menu déroulant.
1. Choisissez les paramètres souhaités.

![Écran des paramètres de bureau des autorisations d’appareil](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

1. Ouvrez Teams.
1. Go to **Settings**  ->  **App Permissions**.
1. Sélectionnez l’application dont vous avez besoin pour choisir les paramètres.
1. Choisissez les paramètres souhaités.

![Écran des paramètres mobiles des autorisations d’appareil](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a>Propriétés

Mettez à jour les propriétés de votre application en ajoutant et en spécifiant les cinq propriétés que vous souhaitez `manifest.json` utiliser dans votre application `devicePermissions` :

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```
> [!Note]
>
> Le média est également utilisé pour les autorisations d’appareil photo sur mobile.

Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement :

| Propriété      | Description   |
| --- | --- |
| media         | autorisation d’utiliser la caméra, le microphone, les haut-parleurs et l’accès à la galerie multimédia |
| géolocalisation   | autorisation de renvoyer l’emplacement de l’utilisateur      |
| notifications | autorisation d’envoyer des notifications à l’utilisateur      |
| midi          | autorisation d’envoyer et de recevoir des informations midi à partir d’un instrument de musique numérique   |
| openExternal  | autorisation d’ouvrir des liens dans des applications externes  |

## <a name="checking-permissions-from-your-tab"></a>Vérification des autorisations à partir de votre onglet

Une fois que vous avez ajouté le manifeste de votre application, vous pouvez vérifier les autorisations à l’aide de l’API HTML5 « autorisations » sans provoquer `devicePermissions` d’invite.

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

## <a name="prompting-the-user"></a>Invite de l’utilisateur

Pour afficher une invite pour obtenir l’autorisation d’accéder aux autorisations d’appareil, vous devez utiliser l’API HTML5 ou Teams appropriée. 

Par exemple, pour demander à l’utilisateur d’accéder à son emplacement, vous devez appeler `getCurrentPosition` :

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

Pour utiliser l’appareil photo sur ordinateur de bureau ou web, Teams affiche une invite d’autorisation lorsque vous appelez `getUserMedia` :

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

Pour capturer l’image sur un appareil mobile, Teams mobile vous demandera l’autorisation lorsque vous appelez `captureImage()` :

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

Les notifications inviteront l’utilisateur à appeler `requestPermission` :

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

Pour utiliser l’appareil photo ou accéder à la galerie de photos, Teams Mobile demande l’autorisation lorsque vous appelez `selectMedia()` :

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Pour utiliser le micro, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()` :

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Pour demander à l’utilisateur de partager un emplacement sur l’interface de carte, Teams mobile demandera l’autorisation lorsque vous appelez `getLocation()` :

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[Desktop](#tab/desktop)

![Invite d’autorisations d’appareil de bureau Onglets](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

![Invite d’autorisations d’appareil mobile Onglets](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a>Comportement des autorisations entre les sessions de connexion

Les autorisations d’appareil natives sont stockées pour chaque session de connexion. Cela signifie que si vous vous connectez à une autre instance de Teams (par exemple, sur un autre ordinateur), les autorisations de votre appareil à partir de vos sessions précédentes ne seront pas disponibles. Au lieu de cela, vous devrez consentir à nouveau aux autorisations d’appareil pour la nouvelle session de connexion. Cela signifie également que, si vous vous déconnectez de Teams (ou que vous changez de client dans Teams), les autorisations de votre appareil seront supprimées pour cette session de connexion précédente. Gardez ceci à l’esprit lorsque vous développez des autorisations d’appareil natives : les fonctionnalités natives que vous consentez sont uniquement pour votre session _de_ connexion actuelle.
