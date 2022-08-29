---
title: Prise en main de Live Share
author: surbhigupta
description: Dans ce module, découvrez-en plus sur les fonctionnalités du Kit de développement logiciel (SDK) Live Share, les autorisations RSC et les structures de données éphémères.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 35b39f062bcdaf79e0c32d33260dbd0940a4fe2c
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425602"
---
# <a name="live-share-core-capabilities"></a>Fonctionnalités principales de Live Share

Le Kit de développement logiciel (SDK) Live Share peut être ajouté aux contextes `sidePanel` et `meetingStage`  de l’extension de votre réunion avec un minimum d’efforts. Cet article se concentre sur la façon d’intégrer le Kit de développement logiciel (SDK) Live Share dans votre application et les fonctionnalités clés du Kit de développement logiciel (SDK).

> [!NOTE]
> Seules les réunions planifiées sont actuellement prises en charge et tous les participants doivent figurer dans le calendrier de la réunion. Les types de réunion tels que les appels en tête-à-tête, les appels de groupe et les réunions instantanées ne sont actuellement pas pris en charge.

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-dashboard.png" alt-text="Live Share Teams":::

## <a name="install-the-javascript-sdk"></a>Installer le Kit de développement logiciel (SDK) JavaScript

Le [Kit de développement logiciel (SDK) Live Share](https://github.com/microsoft/live-share-sdk) est un package JavaScript publié sur [npm](https://www.npmjs.com/package/@microsoft/live-share) et vous pouvez le télécharger via npm ou Yarn.

### <a name="npm"></a>npm

```bash
npm install @microsoft/live-share --save
```

### <a name="yarn"></a>Fil

```bash
yarn add @microsoft/live-share
```

## <a name="register-rsc-permissions"></a>Inscrire des autorisations RSC

Pour activer le Kit de développement logiciel (SDK) Live Share pour votre extension de réunion, vous devez d’abord ajouter les autorisations RSC suivantes dans le manifeste de votre application :

```json
{
  // ...rest of your manifest here
  "configurableTabs": [
    {
        "configurationUrl": "https://<<BASE_URI_ORIGIN>>/config",
        "canUpdateConfiguration": false,
        "scopes": [
            "groupchat"
        ],
        "context": [
            "meetingSidePanel",
            "meetingStage"
        ]
    }
  ],
  "validDomains": [
    "<<BASE_URI_ORIGIN>>"
  ],
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "LiveShareSession.ReadWrite.Chat",
          "type": "Delegated"
        },
        {
          "name": "LiveShareSession.ReadWrite.Group",
          "type": "Delegated"
        },
        {
          "name": "MeetingStage.Write.Chat",
          "type": "Delegated"
        },
        {
          "name": "ChannelMeetingStage.Write.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

## <a name="join-a-meeting-session"></a>Participer à une session de réunion

Suivez les étapes pour rejoindre une session associée à la réunion d’un utilisateur :

1. Initialisez le Kit de développement logiciel (SDK) client Teams.
2. Initialisez le [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient).
3. Définir les structure de données que vous voulez synchroniser. Par exemple : `SharedMap`.
4. Rejoindre le conteneur.

Exemple :

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

---

C’est tout ce qu’il a fallu pour configurer votre conteneur et participer à la session de réunion. À présent, examinons les différents types de _structures des données distribuées_ que vous pouvez utiliser avec le Kit de développement logiciel (SDK) Live Share.

## <a name="fluid-distributed-data-structures"></a>Structures de données distribuées Fluid

Le Kit de développement logiciel (SDK) Live Share prend en charge toute [structure de données distribuées](https://fluidframework.com/docs/data-structures/overview/) incluse dans Infrastructure Fluid. Voici une vue d’ensemble rapide de quelques-uns des différents types d’objets disponibles :

| Objet partagé                                                                       | Description                                                                                                                             |
| ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [SharedMap](https://fluidframework.com/docs/data-structures/map/)                   | Un magasin de valeurs clés distribué. Définissez un objet JSON sérialisable pour une clé donnée afin de synchroniser cet objet pour tous les membres de la session. |
| [SharedSegmentSequence](https://fluidframework.com/docs/data-structures/sequences/) | Structure de données de type liste permettant de stocker un groupe d’éléments (appelés segments) dans des positions définies.                                               |
| [SharedString](https://fluidframework.com/docs/data-structures/string/)             | Séquence de chaînes distribuées optimisée pour la modification du texte du document.                                                                |

Voyons comment `SharedMap` fonctionne. Dans cet exemple, nous avons utilisé `SharedMap` pour créer une fonctionnalité de sélection.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { playlistMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed, local) => {
  const video = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap, IValueChanged } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Declare interface for object being stored in map
interface IVideo {
  id: string;
  url: string;
}

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed: IValueChanged, local: boolean) => {
  const video: IVideo | undefined = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video: IVideo) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

---

> [!NOTE]
> Les objets principaux DDS Infrastructure Fluid ne prennent pas en charge la vérification du rôle de la réunion. Tous les participants à la réunion peuvent modifier des données stockées par le biais de ces objets.

## <a name="live-share-ephemeral-data-structures"></a>Structures de données éphémères Live Share

Le Kit de développement logiciel (SDK) Live Share inclut un ensemble de nouvelles classes `SharedObject` éphémères qui fournissent des objets avec état et sans état qui ne sont pas stockés dans le conteneur Fluid. Par exemple, si vous souhaitez créer une fonctionnalité de pointeur laser dans votre application, telle que l’intégration populaire PowerPoint Live, vous pouvez utiliser notre objet `EphemeralEvent` ou nos objets `EphemeralState`.

| Objet éphémère                                                             | Description                                                                                                                             |
| ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [EphemeralPresence](/javascript/api/@microsoft/live-share/ephemeralpresence) | Découvrez quels utilisateurs sont en ligne, définissez des propriétés personnalisées pour chaque utilisateur et diffusez les modifications apportées à leur participation.                               |
| [EphemeralEvent](/javascript/api/@microsoft/live-share/ephemeralevent)       | Diffusez des événements individuels avec des attributs de données personnalisés dans la charge utile.                                                             |
| [EphemeralState](/javascript/api/@microsoft/live-share/ephemeralstate)       | À l’instar de SharedMap, un magasin de valeurs clés distribué qui permet des modifications d’état restreintes en fonction du rôle, par exemple, le présentateur. |

### <a name="ephemeralpresence-example"></a>Exemple EphemeralPresence

La `EphemeralPresence` classe facilite plus que jamais le suivi des personnes qui se trouve dans la session. Lorsque vous appelez la `.initialize()` ou `.updatePresence()` les méthodes, vous pouvez affecter des métadonnées personnalisées pour cet utilisateur, telles que le nom ou l’image de profil. En écoutant les `presenceChanged` événements, chaque client reçoit l’objet le plus récent `EphemeralPresenceUser` , réduisant toutes les mises à jour de présence en un seul enregistrement pour chaque objet unique `userId`.

> [!NOTE]
> La valeur par défaut `userId` assignée à chacun `EphemeralPresenceUser` est un UUID aléatoire et n’est pas directement liée à une identité AAD. Vous pouvez remplacer cela en définissant une valeur personnalisée `userId` comme clé primaire, comme illustré dans l’exemple ci-dessous.

Exemple :

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  TeamsFluidClient,
  EphemeralPresence,
  PresenceState,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
  },
};
const { container } = await client.joinContainer(schema);
const presence = container.initialObjects.presence;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence, local) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName, profilePicture) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence, PresenceState, EphemeralPresenceUser } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomUserData {
  name: string;
  picture: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    presence: EphemeralPresence<ICustomUserData>,
  },
};
const { container } = await client.joinContainer(schema);
const presence = container.initialObjects.presence as EphemeralPresence<ICustomUserData>;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence: EphemeralPresenceUser<ICustomUserData>, local: boolean) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName: string, profilePicture: string) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

---

### <a name="ephemeralevent-example"></a>Exemple EphemeralEvent

`EphemeralEvent` est un excellent moyen d’envoyer des événements simples vers d’autres clients dans une réunion. Il est utile pour des scénarios tels que l’envoi de notifications de session.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralEvent } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { notifications: EphemeralEvent },
};
const { container } = await client.joinContainer(schema);
const { notifications } = container.initialObjects;

// Register listener for incoming notifications
notifications.on("received", (event, local) => {
  let notificationToDisplay;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralEvent, IEphemeralEvent } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomEvent extends IEphemeralEvent {
  senderName: string;
  text: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    notifications: EphemeralEvent<ICustomEvent>,
  },
};
const { container } = await client.joinContainer(schema);
const notifications = container.initialObjects.notifications as EphemeralEvent<ICustomEvent>;

// Register listener for incoming notifications
notifications.on("received", (event: ICustomEvent, local: boolean) => {
  let notificationToDisplay: string;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

---

### <a name="ephemeraltimer-example"></a>Exemple EphemeralTimer

`EphemeralTimer` active les scénarios qui ont une limite de temps, comme un minuteur de méditation de groupe ou un minuteur rond pour un jeu.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralTimer } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { timer: EphemeralTimer },
};
const { container } = await client.joinContainer(schema);
const { timer } = container.initialObjects;

// Register listener for when the timer starts its countdown
timer.on("started", (config, local) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on("played", (config, local) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on("paused", (config, local) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on("finished", (config) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on("onTick", (milliRemaining) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events for users in session
await timer.initialize();

// Start a 60 second timer
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  TeamsFluidClient,
  EphemeralTimer,
  EphemeralTimerEvents,
  ITimerConfig,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { timer: EphemeralTimer },
};
const { container } = await client.joinContainer(schema);
const timer = container.initialObjects.timer as EphemeralTimer;

// Register listener for when the timer starts its countdown
timer.on(EphemeralTimerEvents.started, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on(EphemeralTimerEvents.played, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on(EphemeralTimerEvents.paused, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on(EphemeralTimerEvents.finished, (config: ITimerConfig) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on(EphemeralTimerEvents.onTick, (milliRemaining: number) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events
await timer.initialize();

// Start a 60 second timer for users in session
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

---

## <a name="role-verification-for-ephemeral-data-structures"></a>Vérification de rôles pour les structures de données éphémères

Les réunions dans Teams peuvent aller des appels en tête-à-tête aux réunions de tout le personnel et elles peuvent inclure des membres au sein des organisations. Les objets éphémères sont conçus pour prendre en charge la vérification de rôle, ce qui vous permet de définir les rôles autorisés à envoyer des messages pour chaque objet éphémère individuel. Par exemple, vous pouvez choisir que seuls les présentateurs et les organisateurs de réunion peuvent contrôler la lecture vidéo, tout en permettant aux invités et aux participants de demander à regarder des vidéos par la suite.

> [!NOTE]
> La `EphemeralPresence` classe ne prend pas en charge la vérification de rôle. L’objet `EphemeralPresenceUser` a une `getRoles` méthode, qui retourne les rôles de réunion pour un utilisateur donné.

Exemple utilisant :`EphemeralState`

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  TeamsFluidClient,
  EphemeralState,
  UserMeetingRole,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { appState: EphemeralState },
};
const { container } = await client.joinContainer(schema);
const { appState } = container.initialObjects;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state, data, local) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralState, UserMeetingRole } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomState {
  documentId: string;
  presentingUserId?: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    appState: EphemeralState<ICustomState>,
  },
};
const { container } = await client.joinContainer(schema);
const appState = container.initialObjects.appState as EphemeralState<ICustomState>;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state: string, data: ICustomState | undefined, local: boolean) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId: string) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId: string) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

---

Écoutez vos clients pour comprendre leurs scénarios avant d’implémenter la vérification de rôle dans votre application, en particulier pour le rôle d’**Organisateur**. Il n’existe aucune garantie qu’un organisateur de réunion soit présent dans la réunion. En règle générale, tous les utilisateurs seront **Organisateur** ou **Présentateur** lors de la collaboration au sein d’une organisation. Si un utilisateur est un **Participant**, il s’agit généralement d’une décision intentionnelle au nom d’un organisateur de la réunion.

## <a name="code-samples"></a>Exemples de code

| Exemple de nom | Description                                                     | JavaScript                                  |
| ----------- | --------------------------------------------------------------- | ------------------------------------------- |
| Lanceur de dés | Permettre à tous les clients connectés de lancer un dé et de visualiser le résultat. | [View](https://aka.ms/liveshare-diceroller) |
| Agile Poker | Permettre à tous les clients connectés de jouer à Agile Poker.               | [View](https://aka.ms/liveshare-agilepoker) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Fonctionnalités média de Live Share](teams-live-share-media-capabilities.md)

## <a name="see-also"></a>Voir aussi

* [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
* [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Documents de référence du kit SDK Live Share Media](/javascript/api/@microsoft/live-share-media/)
* [FAQ Live Share](teams-live-share-faq.md)
* [Applications Teams dans les réunions](teams-apps-in-meetings.md)
