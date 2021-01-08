---
title: Demander des autorisations de périphérique pour votre onglet Microsoft teams
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui requièrent généralement le consentement de l’utilisateur
keywords: développement d’onglets teams
ms.openlocfilehash: 6be183d2610616f3bd3bdf32554976322193c132
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731978"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Demander des autorisations de périphérique pour votre onglet Microsoft teams

Vous voudrez peut-être enrichir votre onglet avec des fonctionnalités qui nécessitent un accès à des fonctionnalités d’appareil natives, telles que :

> [!div class="checklist"]
>
> * Appareil photo
> * Micro
> * Emplacement
> * Notifications

[!Note] Pour intégrer les capacités de l’appareil photo et de l’image dans votre application mobile Microsoft Teams, reportez-vous à la rubrique [fonctionnalités de l’appareil photo](../../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!IMPORTANT]
>
> * Pour le moment, le client mobile teams prend uniquement en charge l’accès aux fonctionnalités de l’appareil,, `camera` `gallery` `mic` et `location` via les fonctionnalités natives, et est disponible sur toutes les constructions d’applications, y compris les onglets. </br>
> * La prise en charge de `camera` , de `gallery` et de `mic` est activée via l' [**API selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true). Pour la capture d’image unique, vous pouvez utiliser l' [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).
> * La prise en charge de `location` est activée via l' [**API GetLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true). Il est recommandé d’utiliser cette API car l' [**API de géolocalisation**](../../resources/schema/manifest-schema.md#devicepermissions) n’est pas entièrement prise en charge sur tous les clients de bureau.

## <a name="device-permissions"></a>Autorisations de l’appareil

L’accès aux autorisations de l’appareil d’un utilisateur vous permet de créer des expériences plus riches, par exemple :

* Enregistrer et partager des courtes vidéos
* Enregistrez des mémos audio courts et enregistrez-les pour une version ultérieure.
* Utiliser les informations relatives à l’emplacement de l’utilisateur pour afficher les informations pertinentes

Bien que l’accès à ces fonctionnalités soit standard dans la plupart des navigateurs Web modernes, vous devez informer teams des fonctionnalités que vous souhaitez utiliser en mettant à jour votre manifeste d’application. Cela vous permettra de demander des autorisations, de la même façon que vous le feriez dans un navigateur, tandis que votre application est exécutée sur le client de bureau Teams.

## <a name="manage-permissions"></a>Gérer les autorisations

# <a name="desktop"></a>[Desktop](#tab/desktop)

1. Ouvrez Teams.
1. Dans le coin supérieur droit de la fenêtre, sélectionnez l’icône de votre profil.
1. Sélectionnez   ->  **autorisations** des paramètres dans le menu déroulant.
1. Choisissez les paramètres de votre choix.

![Écran des paramètres de bureau des autorisations de périphérique](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

1. Ouvrez Teams.
1. Accédez à **paramètres**  ->  **app permissions**.
1. Sélectionnez l’application pour laquelle vous devez choisir des paramètres.
1. Choisissez les paramètres de votre choix.

![Écran des paramètres mobiles des autorisations de l’appareil](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a>Propriétés

Mettez à jour votre application `manifest.json` en ajoutant `devicePermissions` et en spécifiant les cinq propriétés que vous souhaitez utiliser dans votre application :

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
> Le support est également utilisé pour les autorisations d’appareil photo sur mobile.

Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement :

| Propriété      | Description   |
| --- | --- |
| panne         | autorisation d’utilisation de l’appareil photo, du microphone, des haut-parleurs et de la Galerie multimédia Access |
| géolocalisation   | autorisation de retourner l’emplacement de l’utilisateur      |
| notifications | autorisation d’envoyer les notifications de l’utilisateur      |
| midi          | autorisation d’envoyer et de recevoir des informations midi à partir d’un instrument musical numérique   |
| openExternal  | autorisation d’ouvrir des liens dans des applications externes  |

## <a name="checking-permissions-from-your-tab"></a>Vérification des autorisations à partir de votre onglet

Une fois que vous avez ajouté `devicePermissions` à votre manifeste d’application, vous pouvez vérifier les autorisations à l’aide de l’API HTML5 « autorisations » sans générer d’invite.

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

## <a name="prompting-the-user"></a>Demander à l’utilisateur

Pour afficher une invite permettant d’obtenir le consentement pour accéder aux autorisations des appareils, vous devez tirer parti de l’API HTML5 ou teams appropriée. 

Par exemple, pour inviter l’utilisateur à accéder à son emplacement, vous devez appeler `getCurrentPosition` :

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

Pour utiliser l’appareil photo sur un ordinateur de bureau ou sur le Web, teams affiche une invite d’autorisation lorsque vous appelez `getUserMedia` :

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

Pour capturer l’image sur mobile, teams mobile vous demande des autorisations lors de l’appel `captureImage()` :

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

Les notifications invitent l’utilisateur à appeler les `requestPermission` éléments suivants :

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

Pour utiliser l’appareil photo ou la Galerie de photos Access, teams mobile demande des autorisations lorsque vous appelez `selectMedia()` :

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Pour utiliser le micro, teams mobile demande des autorisations lorsque vous appelez `selectMedia()` :

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

Pour inviter l’utilisateur à partager son emplacement sur l’interface de carte, teams mobile demande l’autorisation lorsque vous appelez `getLocation()` :

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[Desktop](#tab/desktop)

![Invite des autorisations des appareils de bureau des onglets](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

![Invite des autorisations de l’appareil mobile onglets](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a>Comportement des autorisations entre les sessions de connexion

Les autorisations d’appareil Native sont stockées pour chaque session de connexion. Cela signifie que si vous vous connectez à une autre instance de Teams (par exemple, sur un autre ordinateur), les autorisations de votre appareil pour vos sessions précédentes ne seront pas disponibles. Au lieu de cela, vous devrez redéfinir les autorisations des appareils pour la nouvelle session de connexion. Cela signifie également que si vous vous déconnectez de Teams (ou que vous changez de locataire dans Teams), vos autorisations sur les appareils seront supprimées pour cette session précédente. Gardez cela à l’esprit lorsque vous développez des autorisations d’appareil natives : les fonctionnalités natives que vous acceptez pour votre session de connexion _actuelle_ .
