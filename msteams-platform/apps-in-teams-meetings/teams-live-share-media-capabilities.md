---
title: Fonctionnalités média de Live Share
author: surbhigupta
description: Dans ce module, découvrez-en plus sur les fonctionnalités multimédias Live Share, les suspensions et les points d’attente, l’abaissement audio et la synchronisation vidéo et audio.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 31b962d747a792b58a9efc9e2c52e42dc841ed18
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552491"
---
# <a name="live-share-media-capabilities"></a>Fonctionnalités média de Live Share

:::image type="content" source="../assets/images/teams-live-share/live-share-media-capabilities-docs-feature-1.png" alt-text="Synchronisation des médias Teams Live Share":::

La vidéo et l’audio sont des parties instrumentales du monde moderne et du lieu de travail. Nous avons entendu de nombreux commentaires indiquant que nous pouvons faire davantage pour améliorer la qualité, l’accessibilité et la protection des licences pour regarder ensemble des vidéos lors de réunions.

Le Kit de développement logiciel (SDK) Live Share permet une **synchronisation de média** robuste pour n’importe quel élément et `<audio>` HTML `<video>` avec seulement quelques lignes de code. En synchronisant le multimédia à l’état du lecteur et de la couche de contrôles de transport, vous pouvez attribuer individuellement des vues et des licences, tout en fournissant la qualité la plus élevée possible disponible via votre application.

## <a name="install"></a>Installer

Pour ajouter la dernière version du Kit de développement logiciel (SDK) à votre application à l’aide de npm :

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-media@next --save
```

OR

Pour ajouter la dernière version du Kit de développement logiciel (SDK) à votre application à l’aide de [Yarn](https://yarnpkg.com/) :

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-media@next
```

## <a name="media-sync-overview"></a>Vue d’ensemble de la synchronisation des multimédias

Le Kit de développement logiciel (SDK) Live Share a deux classes principales liées à la synchronisation des multimédias :

| Classes                                                                                        | Description                                                                                                                                       |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [LiveMediaSession](/javascript/api/@microsoft/live-share-media/livemediasession)     | Objet live personnalisé conçu pour coordonner les contrôles de transport multimédia et l’état de lecture dans les flux multimédias indépendants.                          |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | Synchronise tout objet qui implémente l’interface `IMediaPlayer` , y compris HTML5 `<video>` et `<audio>` - à l’aide `LiveMediaSession`de . |

Exemple :

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, UserMeetingRole } from "@microsoft/live-share";
import { LiveMediaSession } from "@microsoft/live-share-media";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { mediaSession: LiveMediaSession },
};
const { container } = await liveShare.joinContainer(schema);
const { mediaSession } = container.initialObjects;

// Get the player from your document and create synchronizer
const player = document.getElementById("player");
const synchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, UserMeetingRole } from "@microsoft/live-share";
import { LiveMediaSession, IMediaPlayer, MediaPlayerSynchronizer } from "@microsoft/live-share-media";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { mediaSession: LiveMediaSession },
};
const { container } = await liveShare.joinContainer(schema);
const mediaSession = container.initialObjects.mediaSession as LiveMediaSession;

// Get the player from your document and create synchronizer
const player: IMediaPlayer = document.getElementById("player") as HTMLVideoElement;
const synchronizer: MediaPlayerSynchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

---

L’utilisateur `LiveMediaSession` écoute automatiquement les modifications apportées à l’état de lecture du groupe. `MediaPlayerSynchronizer` écoute les modifications d’état émises par `LiveMediaSession` et les applique à l’objet fourni `IMediaPlayer` , tel qu’un html5 `<video>` ou `<audio>` un élément. Pour éviter les modifications d’état de lecture qu’un utilisateur n’a pas intentionnellement initiées, telles qu’un événement de mémoire tampon, nous devons appeler des contrôles de transport via le synchronisateur, plutôt que directement par le lecteur.

Exemple :

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
  <div class="player-controls">
    <button id="play-button">Play</button>
    <button id="pause-button">Pause</button>
    <button id="restart-button">Restart</button>
    <button id="change-track-button">Change track</button>
  </div>
</body>
```

```javascript
// ...

document.getElementById("play-button").onclick = () => {
  synchronizer.play();
};

document.getElementById("pause-button").onclick = () => {
  synchronizer.pause();
};

document.getElementById("restart-button").onclick = () => {
  synchronizer.seekTo(0);
};

document.getElementById("change-track-button").onclick = () => {
  synchronizer.setTrack({
    trackIdentifier: "SOME_OTHER_VIDEO_SRC",
  });
};
```

> [!NOTE]
> Bien que vous puissiez utiliser l’objet `LiveMediaSession` pour synchroniser le média manuellement, il est généralement recommandé d’utiliser le `MediaPlayerSynchronizer`. Selon le lecteur que vous utilisez dans votre application, vous devrez peut-être créer un shim délégué pour que l’interface de votre lecteur web corresponde à l’interface [IMediaPlayer](/javascript/api/@microsoft/live-share-media/imediaplayer) .

## <a name="suspensions-and-wait-points"></a>Suspensions et points d’attente

:::image type="content" source="../assets/images/teams-live-share/live-share-media-out-of-sync.png" alt-text="Capture d’écran montrant une synchronisation de suspension avec le présentateur.":::

Si vous souhaitez suspendre temporairement la synchronisation de l’objet `LiveMediaSession`, vous pouvez utiliser des suspensions. Un objet [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/livemediasessioncoordinatorsuspension) est local par défaut, ce qui peut être utile dans les cas où un utilisateur peut vouloir se rattraper sur quelque chose qu’il a manqué, faire une pause, etc. Si l’utilisateur met fin à la suspension, la synchronisation reprend automatiquement.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const suspension: MediaSessionCoordinatorSuspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

---

Lorsque vous commencez une suspension, vous pouvez également inclure un paramètre [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint) facultatif qui permet aux utilisateurs de définir les horodatages dans lesquels une suspension doit se produire pour tous les utilisateurs. La synchronisation ne reprendra pas tant que tous les utilisateurs n’auront pas mis fin à la suspension de ce point d’attente.

Voici quelques scénarios où les points d’attente sont particulièrement utiles :

- Ajout d’un questionnaire ou d’une enquête à certains points de la vidéo.
- En attendant que tout le monde charge correctement une vidéo avant son démarrage ou lors de la mise en mémoire tampon.
- Autoriser un présentateur à choisir des points dans la vidéo pour une discussion de groupe.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension, CoordinationWaitPoint } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const waitPoint: CoordinationWaitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);

// End the suspension when the user readies up
document.getElementById("ready-up-button")!.onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

---

## <a name="audio-ducking"></a>Abaissement audio

Le Kit de développement logiciel (SDK) Live Share prend en charge l’abaissement audio intelligent. Vous pouvez utiliser la fonctionnalité dans votre application en ajoutant ce qui suit à votre code :

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { meeting } from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer;
meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { meeting } from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer: NodeJS.Timeout | undefined;
meeting.registerSpeakingStateChangeHandler((speakingState: meeting.ISpeakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

---

En outre, ajoutez les autorisations [RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) suivantes dans le manifeste de votre application :

```json
{
  // ...rest of your manifest here
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Chat",
          "type": "Delegated"
        },
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

> [!NOTE]
> L’API `registerSpeakingStateChangeHandler` utilisée pour le ducking audio ne fonctionne actuellement que sur le bureau Microsoft Teams et dans les types de réunions planifiées et de réunions.

## <a name="code-samples"></a>Exemples de code

| Exemple de nom          | Description                                                                                                                               | JavaScript                                     |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Vidéo React          | Exemple de base montrant le fonctionnement de l’objet LiveMediaSession avec la vidéo HTML5.                                                        | [View](https://aka.ms/liveshare-reactvideo)    |
| Modèle multimédia React | Permettre à tous les clients connectés de regarder ensemble des vidéos, de créer une playlist partagée, de transférer qui a le contrôle et d’effectuer des annotations sur la vidéo. | [View](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Canevas Live Share](teams-live-share-canvas.md)

## <a name="see-also"></a>Voir aussi

- [FAQ sur le Kit de développement logiciel (SDK) de partage en direct](teams-live-share-faq.md)
- [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
- [Applications Teams dans les réunions](teams-apps-in-meetings.md)
