---
title: Fonctionnalités média de Live Share
description: Dans ce module, découvrez-en plus sur les fonctionnalités multimédias Live Share, les suspensions et les points d’attente, l’abaissement audio et la synchronisation vidéo et audio.
ms.topic: concept
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 662a0204793eaf2ef4702a447a4a61c79964112c
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142478"
---
---

# <a name="live-share-media-capabilities"></a>Fonctionnalités média de Live Share

La vidéo et l’audio sont des parties instrumentales du monde moderne et du lieu de travail. Nous avons entendu de nombreux commentaires indiquant que nous pouvons faire davantage pour améliorer la qualité, l’accessibilité et la protection des licences pour regarder ensemble des vidéos lors de réunions.

Le Kit de développement logiciel (SDK) Live Share permet la **synchronisation multimédia** dans n’importe quel élément HTML `<video>` et `<audio>` de manière plus simple qu’avant. En synchronisant le multimédia à l’état du lecteur et de la couche de contrôles de transport, vous pouvez attribuer individuellement des vues et des licences, tout en fournissant la qualité la plus élevée possible disponible via votre application.

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

| Classes                                                                                                                  | Description                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| [EphemeralMediaSession](/javascript/api/@microsoft/live-share-media/ephemeralmediasession)     | Objet éphémère personnalisé conçu pour coordonner les contrôles de transport multimédia et l’état de lecture dans les flux multimédias indépendants. |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | Synchronise un élément multimédia HTML local avec un groupe d’éléments multimédias HTML distants pour un `EphemeralMediaSession`.|

Exemple :

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
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
const allowedRoles = ["Organizer", "Presenter"];
await mediaSession.start(allowedRoles);
```

`EphemeralMediaSession` écoute automatiquement les modifications apportées à l’état de lecture du groupe et applique les modifications via le `MediaPlayerSynchronizer`. Pour éviter les modifications d’état de lecture qu’un utilisateur n’a pas intentionnellement initiées, telles qu’un événement de mémoire tampon, nous devons appeler des contrôles de transport via le synchronisateur, plutôt que directement par le lecteur.

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

 > [!Note]
 > Bien que vous puissiez utiliser l’objet `EphemeralMediaSession` pour synchroniser directement le multimédia, utilisez le `MediaPlayerSynchronizer` à moins que vous ne vouliez un contrôle plus précis de la logique de synchronisation. Selon le lecteur que vous utilisez dans votre application, vous souhaiterez peut-être créer un shim délégué pour que l’interface de votre lecteur web corresponde à l’interface multimédia HTML.

## <a name="suspensions-and-wait-points"></a>Suspensions et points d’attente

Si vous souhaitez suspendre temporairement la synchronisation de l’objet `EphemeralMediaSession`, vous pouvez utiliser des suspensions. Un objet [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/ephemeralmediasessioncoordinatorsuspension) est local par défaut, ce qui peut être utile dans les cas où un utilisateur peut vouloir se rattraper sur quelque chose qu’il a manqué, faire une pause, etc. Si l’utilisateur met fin à la suspension, la synchronisation reprend automatiquement.

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

Lorsque vous commencez une suspension, vous pouvez également inclure un paramètre [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint) facultatif qui permet aux utilisateurs de définir les horodatages dans lesquels une suspension doit se produire pour tous les utilisateurs. La synchronisation ne reprendra pas tant que tous les utilisateurs n’auront pas mis fin à la suspension de ce point d’attente. Cela est utile pour des éléments tels que l’ajout d’un questionnaire ou d’une enquête à certains moments de la vidéo.

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension();
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

## <a name="audio-ducking"></a>Abaissement audio

Le Kit de développement logiciel (SDK) Live Share prend en charge l’abaissement audio intelligent. Vous pouvez utiliser la fonctionnalité _expérimentale_ dans votre application, puis ajouter ce qui suit à votre code :

```javascript
import * as microsoftTeams from "@microsoft/teams-js";

// ...

let volumeTimer;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

Pour activer l’abaissement audio, ajoutez les autorisations [RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) suivantes dans le manifeste de votre application :

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

> [!Note]
> L’API `registerSpeakingStateChangeHandler` utilisée pour l’abaissement audio fonctionne actuellement uniquement pour les utilisateurs non locaux qui parlent.

## <a name="code-samples"></a>Exemples de code

| Exemple de nom   | Description | JavaScript |
| -------------------- | ----------------------------| -----------------|
| Vidéo React          | Exemple de base montrant le fonctionnement de l’objet EphemeralMediaSession avec la vidéo HTML5.                                                        | [View](https://aka.ms/liveshare-reactvideo)    |
| Modèle multimédia React | Permettre à tous les clients connectés de regarder ensemble des vidéos, de créer une playlist partagée, de transférer qui a le contrôle et d’effectuer des annotations sur la vidéo. | [View](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Didacticiel Poker agile](../sbs-teams-live-share.yml)

## <a name="see-also"></a>Voir aussi

* [FAQ sur le Kit de développement logiciel (SDK) de partage en direct](teams-live-share-faq.md)
* [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
* [Documents de référence](https://aka.ms/livesharedocs)
* [Applications Teams dans les réunions](teams-apps-in-meetings.md)
