---
title: Demander des autorisations de périphérique pour votre onglet Microsoft teams
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui requièrent généralement le consentement de l’utilisateur
keywords: développement d’onglets teams
ms.openlocfilehash: 454466ff17ecf275f6ae6c7413df8e117335f3c8
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673540"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Demander des autorisations de périphérique pour votre onglet Microsoft teams

Vous souhaiterez peut-être enrichir votre onglet avec des fonctionnalités qui nécessitent l’accès à des fonctionnalités d’appareil natives comme :

* Appareil photo
* Micro
* L’emplacement
* Notifications

![Écran des paramètres d’autorisations des appareils](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> La fonctionnalité d’appareil Native n’est actuellement pas prise en charge pour les onglets sur les clients mobiles, mais la prise en charge complète sera bientôt disponible. Pour vous préparer à ce changement, suivez les [instructions pour les onglets sur mobile](~/tabs/design/tabs-mobile.md) lors de la création des onglets. Les applications personnelles (onglets statiques) sont actuellement disponibles dans l’Aperçu pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md).
>
> Lorsque la prise en charge complète des onglets est publiée :
>
> * Tous les onglets seront toujours disponibles sur mobile
> * Votre `contentUrl` **sera chargé dans le client teams mobile**.
> * Pour les onglets canal/groupe, les utilisateurs peuvent toujours ouvrir l’onglet dans un navigateur `websiteUrl`distinct via votre `contentUrl` , mais votre sera chargé en premier.  

## <a name="device-permissions"></a>Autorisations de l’appareil

L’accès aux autorisations de l’appareil d’un utilisateur vous permet de créer des expériences plus riches, par exemple :

* Enregistrer et partager des courtes vidéos
* Enregistrez des mémos audio courts et enregistrez-les pour une version ultérieure.
* Utiliser les informations relatives à l’emplacement de l’utilisateur pour afficher les informations pertinentes

Bien que l’accès à ces fonctionnalités soit standard dans la plupart des navigateurs Web modernes, vous devez informer teams des fonctionnalités que vous souhaitez utiliser en mettant à jour votre manifeste d’application. Cela vous permettra de demander des autorisations, de la même façon que vous le feriez dans un navigateur, tandis que votre application est exécutée sur le client de bureau Teams.

## <a name="properties"></a>Propriétés

Mettez à jour votre `manifest.json` application en `devicePermissions` ajoutant et en spécifiant les cinq propriétés que vous souhaitez utiliser dans votre application :

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement.

| Propriété      | Description   |
| --- | --- |
| panne         | autorisation d’utilisation de l’appareil photo, du microphone et des haut-parleurs |
| géolocalisation   | autorisation de retourner l’emplacement de l’utilisateur      |
| notifications | autorisation d’envoyer les notifications de l’utilisateur      |
| midi          | autorisation d’envoyer et de recevoir des informations midi à partir d’un instrument musical numérique   |
| openExternal  | autorisation d’ouvrir des liens dans des applications externes  |

## <a name="checking-permissions-from-your-tab"></a>Vérification des autorisations à partir de votre onglet

Une fois que vous `devicePermissions` avez ajouté à votre manifeste d’application, vous pouvez vérifier les autorisations à l’aide de l’API HTML5 « autorisations » sans générer d’invite.

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

Pour afficher une invite permettant d’obtenir le consentement pour accéder aux autorisations des appareils, vous devez tirer parti de l’API HTML5 appropriée. Par exemple, pour inviter l’utilisateur à accéder à sa caméra, vous devez appeler`getUserMedia`

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

La géolocalisation affiche une invite d’autorisation lorsque vous appelez`getCurrentPosition`

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

Les notifications invitent l’utilisateur lorsque vous appelez`requestPermission`

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Invite des autorisations des appareils de tabulation](~/assets/images/tabs/device-permissions-prompt.png)