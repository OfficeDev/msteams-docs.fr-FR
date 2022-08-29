---
title: Fonctionnalités média de Live Share
author: surbhigupta
description: Dans ce module, découvrez-en plus sur les fonctionnalités multimédias Live Share, les suspensions et les points d’attente, l’abaissement audio et la synchronisation vidéo et audio.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 0ab0bf436ce3ca27b55a68ea2c80f1451f4d967e
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425585"
---
# <a name="live-share-media-capabilities"></a>Fonctionnalités média de Live Share

:::image type="content" source="../assets/images/teams-live-share/live-share-media-capabilities-docs-feature-1.png" alt-text="Synchronisation des médias Teams Live Share":::

La vidéo et l’audio sont des parties instrumentales du monde moderne et du lieu de travail. Nous avons entendu de nombreux commentaires indiquant que nous pouvons faire davantage pour améliorer la qualité, l’accessibilité et la protection des licences pour regarder ensemble des vidéos lors de réunions.

Le Kit de développement logiciel (SDK) Live Share permet une **synchronisation de média** robuste pour n’importe quel élément et `<audio>` HTML `<video>` avec seulement quelques lignes de code. En synchronisant le multimédia à l’état du lecteur et de la couche de contrôles de transport, vous pouvez attribuer individuellement des vues et des licences, tout en fournissant la qualité la plus élevée possible disponible via votre application.

## <a name="install"></a>Installer

Pour ajouter la dernière version du Kit de développement logiciel (SDK) à votre application à l’aide de npm :

```bash
npm install @microsoft/live-share --save
npm install @microsoft/live-share-media --save
```

OR

Pour ajouter la dernière version du Kit de développement logiciel (SDK) à votre application à l’aide de [Yarn](https://yarnpkg.com/) :

```bash
yarn add @microsoft/live-share
yarn add @microsoft/live-share-media
```

## <a name="media-sync-overview"></a>Vue d’ensemble de la synchronisation des multimédias

Le Kit de développement logiciel (SDK) Live Share a deux classes principales liées à la synchronisation des multimédias :

| Classes                                                                                        | Description                                                                                                                                       |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [EphemeralMediaSession](/javascript/api/@microsoft/live-share-media/ephemeralmediasession)     | Objet éphémère personnalisé conçu pour coordonner les contrôles de transport multimédia et l’état de lecture dans les flux multimédias indépendants.                          |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | Synchronise tout objet qui implémente l’interface `IMediaPlayer` , y compris HTML5 `<video>` et `<audio>` - à l’aide `EphemeralMediaSession`de . |

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
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient, UserMeetingRole } from "@microsoft/live-share";
import { EphemeralMediaSession } from "@microsoft/live-share-media";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Setup the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { mediaSession: EphemeralMediaSession },
};
const { container } = await client.joinContainer(schema);
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
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient, UserMeetingRole } from "@microsoft/live-share";
import { EphemeralMediaSession, IMediaPlayer, MediaPlayerSynchronizer } from "@microsoft/live-share-media";
import { ContainerSchema } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { mediaSession: EphemeralMediaSession },
};
const { container } = await client.joinContainer(schema);
const mediaSession = container.initialObjects.mediaSession as EphemeralMediaSession;

// Get the player from your document and create synchronizer
const player: IMediaPlayer = document.getElementById("player") as HTMLVideoElement;
const synchronizer: MediaPlayerSynchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

---

L’utilisateur `EphemeralMediaSession` écoute automatiquement les modifications apportées à l’état de lecture du groupe. `MediaPlayerSynchronizer` écoute les modifications d’état émises par `EphemeralMediaSession` et les applique à l’objet fourni `IMediaPlayer` , tel qu’un html5 `<video>` ou `<audio>` un élément. Pour éviter les modifications d’état de lecture qu’un utilisateur n’a pas intentionnellement initiées, telles qu’un événement de mémoire tampon, nous devons appeler des contrôles de transport via le synchronisateur, plutôt que directement par le lecteur.

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
> Bien que vous puissiez utiliser l’objet `EphemeralMediaSession` pour synchroniser le média manuellement, il est généralement recommandé d’utiliser le `MediaPlayerSynchronizer`. Selon le lecteur que vous utilisez dans votre application, vous devrez peut-être créer un shim délégué pour que l’interface de votre lecteur web corresponde à l’interface [IMediaPlayer](/javascript/api/@microsoft/live-share-media/imediaplayer) .

## <a name="suspensions-and-wait-points"></a>Suspensions et points d’attente

:::image type="content" source="../assets/images/teams-live-share/live-share-media-out-of-sync.png" alt-text="Capture d’écran montrant une synchronisation de suspension avec le présentateur.":::

Si vous souhaitez suspendre temporairement la synchronisation de l’objet `EphemeralMediaSession`, vous pouvez utiliser des suspensions. Un objet [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/ephemeralmediasessioncoordinatorsuspension) est local par défaut, ce qui peut être utile dans les cas où un utilisateur peut vouloir se rattraper sur quelque chose qu’il a manqué, faire une pause, etc. Si l’utilisateur met fin à la suspension, la synchronisation reprend automatiquement.

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

Le Kit de développement logiciel (SDK) Live Share prend en charge l’abaissement audio intelligent. Vous pouvez utiliser la fonctionnalité _expérimentale_ dans votre application en ajoutant ce qui suit à votre code :

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import * as microsoftTeams from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState) => {
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
import * as microsoftTeams from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer: NodeJS.Timeout | undefined;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState: microsoftTeams.meeting.ISpeakingState) => {
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
> L’API `registerSpeakingStateChangeHandler` utilisée pour l’abaissement audio fonctionne actuellement uniquement pour les utilisateurs non locaux qui parlent.

## <a name="code-samples"></a>Exemples de code

| Exemple de nom          | Description                                                                                                                               | JavaScript                                     |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Vidéo React          | Exemple de base montrant le fonctionnement de l’objet EphemeralMediaSession avec la vidéo HTML5.                                                        | [View](https://aka.ms/liveshare-reactvideo)    |
| Modèle multimédia React | Permettre à tous les clients connectés de regarder ensemble des vidéos, de créer une playlist partagée, de transférer qui a le contrôle et d’effectuer des annotations sur la vidéo. | [View](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Didacticiel Poker agile](../sbs-teams-live-share.yml)

## <a name="see-also"></a>Voir aussi

- [FAQ sur le Kit de développement logiciel (SDK) de partage en direct](teams-live-share-faq.md)
- [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
- [Documents de référence](https://aka.ms/livesharedocs)
- [Applications Teams dans les réunions](teams-apps-in-meetings.md)
