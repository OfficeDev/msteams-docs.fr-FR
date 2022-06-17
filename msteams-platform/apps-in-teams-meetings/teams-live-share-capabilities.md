---
title: Prise en main de Live Share
description: Dans ce module, découvrez-en plus sur les fonctionnalités du Kit de développement logiciel (SDK) Live Share, les autorisations RSC et les structures de données éphémères.
ms.topic: concept
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: f5986515f9916a0138524b919dca46d0cf0ee8d4
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143241"
---
---

# <a name="live-share-capabilities"></a>Fonctionnalités de Live Share

Le Kit de développement logiciel (SDK) Live Share peut être ajouté aux contextes `sidePanel` et `meetingStage`  de l’extension de votre réunion avec un minimum d’efforts. Cet article se concentre sur la façon d’intégrer le Kit de développement logiciel (SDK) Live Share dans votre application et les fonctionnalités clés du Kit de développement logiciel (SDK).

> [!Note]
> Seules les réunions planifiées sont actuellement prises en charge et tous les participants doivent figurer dans le calendrier de la réunion. Les types de réunion tels que les appels en tête-à-tête, les appels de groupe et les réunions instantanées ne sont actuellement pas pris en charge.

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-dashboard.png" alt-text="Live Share Teams":::

## <a name="install-the-javascript-sdk"></a>Installer le Kit de développement logiciel (SDK) JavaScript

Le [Kit de développement logiciel (SDK) Live Share](https://github.com/microsoft/live-share-sdk) est un package JavaScript publié sur [npm](https://www.npmjs.com/package/@microsoft/live-share) et vous pouvez le télécharger via npm ou Yarn.

**npm**

```bash
npm install @microsoft/live-share --save
```

**Yarn**

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

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Setup the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

C’est tout ce qu’il a fallu pour configurer votre conteneur et participer à la session de réunion. À présent, examinons les différents types de _structures des données distribuées_ que vous pouvez utiliser avec le Kit de développement logiciel (SDK) Live Share.

## <a name="fluid-distributed-data-structures"></a>Structures de données distribuées Fluid

Le Kit de développement logiciel (SDK) Live Share prend en charge toute [structure de données distribuées](https://fluidframework.com/docs/data-structures/overview/) incluse dans Infrastructure Fluid. Voici une vue d’ensemble rapide de quelques-uns des différents types d’objets disponibles :

| Objet partagé                                                                       | Description                                                                                                                                  |
| ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [SharedMap](https://fluidframework.com/docs/data-structures/map/)                   | Un magasin de valeurs clés distribué. Définissez un objet JSON sérialisable pour une clé donnée afin de synchroniser cet objet pour tous les membres de la session. |
| [SharedSegmentSequence](https://fluidframework.com/docs/data-structures/sequences/) | Structure de données de type liste permettant de stocker un groupe d’éléments (appelés segments) dans des positions définies.                                                    |
| [SharedString](https://fluidframework.com/docs/data-structures/string/)             | Séquence de chaînes distribuées optimisée pour la modification du texte du document.                                                                     |

Voyons comment `SharedMap` fonctionne. Dans cet exemple, nous avons utilisé `SharedMap` pour créer une fonctionnalité de sélection.

```javascript
import { SharedMap } from "fluid-framework";
// ...
const schema = {
  initialObjects: { playlistMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
const { playlistMap } = container.initialObjects;

// Listen for changes to values in the map
playlistMap.on("valueChanged", (changed, local) => {
  const video = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video) {
  // Add video to map
  playlistMap.set(video.id, video);
}
// ...
```

> [!Note]
> Les objets principaux DDS Infrastructure Fluid ne prennent pas en charge la vérification du rôle de la réunion. Tous les participants à la réunion peuvent modifier des données stockées par le biais de ces objets.

## <a name="live-share-ephemeral-data-structures"></a>Structures de données éphémères Live Share

Le Kit de développement logiciel (SDK) Live Share inclut un ensemble de nouvelles classes `SharedObject` éphémères qui fournissent des objets avec état et sans état qui ne sont pas stockés dans le conteneur Fluid. Par exemple, si vous souhaitez créer une fonctionnalité de pointeur laser dans votre application, telle que l’intégration populaire PowerPoint Live, vous pouvez utiliser notre objet `EphemeralEvent` ou nos objets `EphemeralState`.

| Objet éphémère                                                                                                       | Description                                                                                                                     |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| [EphemeralPresence](/javascript/api/@microsoft/live-share/ephemeralpresence) | Découvrez quels utilisateurs sont en ligne, définissez des propriétés personnalisées pour chaque utilisateur et diffusez les modifications apportées à leur participation.                       |
| [EphemeralEvent](/javascript/api/@microsoft/live-share/ephemeralevent)       | Diffusez des événements individuels avec des attributs de données personnalisés dans la charge utile.                                                     |
| [EphemeralState](/javascript/api/@microsoft/live-share/ephemeralstate)       | À l’instar de SharedMap, un magasin de valeurs clés distribué qui permet des modifications d’état restreintes en fonction du rôle, par exemple, le présentateur.|

### <a name="ephemeralpresence-example"></a>Exemple EphemeralPresence

La classe `EphemeralPresence` facilite plus que jamais le suivi des personnes qui participent à une réunion. Lorsque vous appelez la méthode `.start()` ou les méthodes `.updatePresence()`, vous pouvez affecter des métadonnées personnalisées pour cet utilisateur, telles qu’un identificateur ou un nom unique.

Exemple :

```javascript
import { EphemeralPresence, PresenceState } from "@microsoft/live-share";
// ...
const schema = {
  initialObjects: { presence: EphemeralPresence },
};
const { container } = await client.joinContainer(schema);
const { presence } = container.initialObjects;

// Listen for changes to presence
presence.on("presenceChanged", (userPresence, local) => {
  // Update UI with presence
});

// Start tracking presence
presence.start("YOUR_CUSTOM_USER_ID", {
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

### <a name="ephemeralevent-example"></a>Exemple EphemeralEvent

`EphemeralEvent` est un excellent moyen d’envoyer des événements simples vers d’autres clients dans une réunion. Il est utile pour des scénarios tels que l’envoi de notifications de session.

```javascript
import { EphemeralEvent } from "@microsoft/live-share";
// ...
const schema = {
  initialObjects: { notifications: EphemeralEvent },
};
const { container } = await client.joinContainer(schema);
const { notifications } = container.initialObjects;

// Listen for incoming notifications
notifications.on("received", (event, local) => {
  let notificationToDisplay;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start tracking notifications
await notifications.start();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

## <a name="role-verification-for-ephemeral-data-structures"></a>Vérification de rôles pour les structures de données éphémères

Les réunions dans Teams peuvent aller des appels en tête-à-tête aux réunions de tout le personnel et elles peuvent inclure des membres au sein des organisations. Les objets éphémères sont conçus pour prendre en charge la vérification de rôle, ce qui vous permet de définir les rôles autorisés à envoyer des messages pour chaque objet éphémère individuel. Par exemple, vous pouvez choisir que seuls les présentateurs et les organisateurs de réunion peuvent contrôler la lecture vidéo, tout en permettant aux invités et aux participants de demander à regarder des vidéos par la suite.

Exemple :

```javascript
import { EphemeralState, UserMeetingRole } from "@microsoft/live-share";
// ...
const schema = {
  initialObjects: { appState: EphemeralState },
};
const { container } = await client.joinContainer(schema);
const { appState } = container.initialObjects;

// Listen for changes to values in the map
appState.on("stateChanged", (state, value, local) => {
  // Update local app state
});

// Set roles who can change state and start
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.start(allowedRoles);

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

Écoutez vos clients pour comprendre leurs scénarios avant d’implémenter la vérification de rôle dans votre application, en particulier pour le rôle d’**Organisateur**. Il n’existe aucune garantie qu’un organisateur de réunion soit présent dans la réunion. En règle générale, tous les utilisateurs seront **Organisateur** ou **Présentateur** lors de la collaboration au sein d’une organisation. Si un utilisateur est un **Participant**, il s’agit généralement d’une décision intentionnelle au nom d’un organisateur de la réunion.

## <a name="code-samples"></a>Exemples de code

| Exemple de nom | Description  | JavaScript  |
| ----------- | ---------------------------------------------- | -------------- |
| Lanceur de dés | Permettre à tous les clients connectés de lancer un dé et de visualiser le résultat. | [View](https://aka.ms/liveshare-diceroller) |
| Agile Poker | Permettre à tous les clients connectés de jouer à Agile Poker.| [View](https://aka.ms/liveshare-agilepoker) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Fonctionnalités média de Live Share](teams-live-share-media-capabilities.md)

## <a name="see-also"></a>Voir aussi

* [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
* [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Documents de référence du kit SDK Live Share Media](/javascript/api/@microsoft/live-share-media/)
* [FAQ Live Share](teams-live-share-faq.md)
* [Applications Teams dans les réunions](teams-apps-in-meetings.md)
