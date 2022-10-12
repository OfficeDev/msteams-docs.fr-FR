---
title: Tutoriel de code de partage en direct
author: surbhigupta
description: Dans ce module, apprenez à démarrer avec Live Share SDK et à créer un échantillon de lanceur de dés à l'aide de Live Share SDK.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: stevenic
ms.date: 04/07/2022
ms.openlocfilehash: ee88797d007e736eb7958e462d8697f379c99413
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552573"
---
# <a name="dice-roller-code-tutorial"></a>Tutoriel de code pour le lanceur de dés

Dans l'application modèle du lanceur de dés, les utilisateurs voient un dé avec un bouton pour le lancer. Lorsque le dé est lancé, le kit SDK de partage en direct utilise le Fluid Framework pour synchroniser les données entre les clients, de sorte que tout le monde voit le même résultat. Pour synchroniser les données, effectuez les étapes suivantes dans le [fichier](https://github.com/microsoft/live-share-sdk/blob/main/samples/01.dice-roller/src/app.js) app.js :

1. [Configurer l'application](#set-up-the-application)
2. [Joindre un conteneur Fluid](#join-a-fluid-container)
3. [Écrire la vue d’étape](#write-the-stage-view)
4. [Connecter vue d’étape aux données Fluid](#connect-stage-view-to-fluid-data)
5. [Écrire l’affichage du panneau latéral](#write-the-side-panel-view)
6. [Écrire la vue paramètres](#write-the-settings-view)

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Echantillon de dés à rouler":::

## <a name="set-up-the-application"></a>Configurer l'application

Commencez par importer les modules nécessaires. L’exemple utilise le [DDS SharedMap](https://fluidframework.com/docs/data-structures/map/) de Fluid Framework et la classe [LiveShareClient](/javascript/api/@microsoft/live-share/liveshareclient) . L'échantillon prend en charge l'extensibilité de la réunion Teams. Nous devrons donc inclure le [SDK client Teams](https://github.com/OfficeDev/microsoft-teams-library-js). Enfin, l'échantillon est conçu pour être exécuté à la fois localement et dans une réunion Teams. Nous devrons donc inclure quelques éléments supplémentaires de Fluid Framework nécessaires pour [tester l'échantillon localement](https://fluidframework.com/docs/testing/testing/#azure-fluid-relay-as-an-abstraction-for-tinylicious).

Les applications créent des conteneurs Fluid à l'aide d'un schéma qui définit un ensemble _d'objets initiaux_ qui seront disponibles pour le conteneur. L'exemple utilise un SharedMap pour stocker la valeur la plus récente du dé qui a été lancé. Pour plus d'informations, voir [Modélisation des données](https://fluidframework.com/docs/build/data-modeling/).

Les applications de réunion Teams nécessitent plusieurs vues (contenu, configuration et scène). Nous allons créer une `start()` fonction qui nous aidera à identifier la vue à rendre et à effectuer toute initialisation nécessaire. Nous voulons que notre application puisse fonctionner à la fois localement dans un navigateur Web et à partir d'une réunion Teams. `start()`La fonction recherche donc un paramètre de `inTeams=true`requête pour déterminer si elle fonctionne dans Teams. Lors de l'exécution dans Teams, votre application doit appeler avant d'appeler `app.initialize()` toute autre méthode teams-js.

En plus du paramètre de `inTeams=true` requête, nous pouvons utiliser`view=content|config|stage` un paramètre de requête pour déterminer la vue qui doit être rendue.

```js
import { SharedMap } from "fluid-framework";
import { app, pages } from "@microsoft/teams-js";
import { LiveShareClient, testLiveShare } from "@microsoft/live-share";
import { InsecureTokenProvider } from "@fluidframework/test-client-utils";

const searchParams = new URL(window.location).searchParams;
const root = document.getElementById("content");

// Define container schema

const diceValueKey = "dice-value-key";

const containerSchema = {
  initialObjects: { diceMap: SharedMap },
};

function onContainerFirstCreated(container) {
  // Set initial state of the rolled dice to 1.
  container.initialObjects.diceMap.set(diceValueKey, 1);
}

// STARTUP LOGIC

async function start() {
  // Check for page to display
  let view = searchParams.get("view") || "stage";

  // Check if we are running on stage.
  if (!!searchParams.get("inTeams")) {
    // Initialize teams app
    await app.initialize();

    // Get our frameContext from context of our app in Teams
    const context = await app.getContext();
    if (context.page.frameContext == "meetingStage") {
      view = "stage";
    }
  }

  // Load the requested view
  switch (view) {
    case "content":
      renderSidePanel(root);
      break;
    case "config":
      renderSettings(root);
      break;
    case "stage":
    default:
      const { container } = await joinContainer();
      renderStage(container.initialObjects.diceMap, root);
      break;
  }
}

start().catch((error) => console.error(error));
```

## <a name="join-a-fluid-container"></a>Rejoindre un conteneur Fluid

Toutes les vues de vos applications n'auront pas besoin d'être collaboratives. La `stage`vue _a toujours besoin_ de fonctionnalités collaboratives, la `content`vue _peut avoir_ besoin de fonctionnalités collaboratives, et la `config`vue ne devrait _jamais_ avoir besoin de fonctionnalités collaboratives. Pour les vues qui nécessitent des fonctions de collaboration, vous devrez rejoindre un conteneur Fluid associé à la réunion en cours.

Rejoindre le conteneur pour la réunion est aussi simple que d’initialiser [LiveShareClient](/javascript/api/@microsoft/live-share/liveshareclient) et d’appeler sa méthode [joinContainer().](/javascript/api/@microsoft/live-share/liveshareclient#@microsoft-live-share-liveshareclient-joincontainer)

Lors de l’exécution locale, vous pouvez importer [testLiveShare](/javascript/api/@microsoft/live-share/testliveshare) et appeler sa méthode [initialize().](/javascript/api/@microsoft/live-share.testliveshare#@microsoft-live-share-testliveshare-initialize) Ensuite, utilisez la méthode [joinContainer()](/javascript/api/@microsoft/live-share.testliveshare#@microsoft-live-share-testliveshare-joincontainer) pour vous connecter à une session.

```js
async function joinContainer() {
  // Are we running in teams?
  if (!!searchParams.get("inTeams")) {
    // Create client
    const liveShare = new LiveShareClient();
    // Join container
    return await liveShare.joinContainer(containerSchema, onContainerFirstCreated);
  }
  // Create client and configure for testing
  testLiveShare.initialize();
  return await testLiveShare.joinContainer(containerSchema, onContainerFirstCreated);
}
```

Lors d’un test local, `testLiveShare` met à jour l’URL du navigateur pour qu’elle contienne l’ID du conteneur de test qui a été créé. La copie de ce lien vers d’autres onglets de navigateur entraîne la `testLiveShare` jointure du conteneur de test qui a été créé. Si la modification de l’URL des applications interfère avec le fonctionnement de l’application, la stratégie utilisée pour stocker l’ID des conteneurs de test peut être personnalisée à l’aide des options [setLocalTestContainerId](/javascript/api/@microsoft/live-share.iliveshareclientoptions#@microsoft-live-share-iliveshareclientoptions-setlocaltestcontainerid) et [getLocalTestContainerId](/javascript/api/@microsoft/live-share.iliveshareclientoptions#@microsoft-live-share-iliveshareclientoptions-getlocaltestcontainerid) passées à `LiveShareClient`.

## <a name="write-the-stage-view"></a>Écrire la vue d’étape

De nombreuses applications d'extensibilité pour réunions d'équipes sont conçues pour utiliser le cadre de visualisation React, mais ce n'est pas obligatoire. Par exemple, cet exemple utilise des méthodes HTML/DOM standard pour rendre une vue.

### <a name="start-with-a-static-view"></a>Commencez par une vue statique

Il est facile de créer la vue en utilisant des données locales sans aucune fonctionnalité Fluid, puis d'ajouter Fluid en modifiant certains éléments clés de l'application.

La `renderStage`fonction ajoute le à l'élément `stageTemplate` HTML transmis et crée un rouleau de dés fonctionnel avec une valeur de dés aléatoire chaque fois que le bouton **Roll** est sélectionné. Le `diceMap` est utilisé dans les étapes suivantes.

```js
const stageTemplate = document.createElement("template");

stageTemplate["innerHTML"] = `
  <div class="wrapper">
    <div class="dice"></div>
    <button class="roll"> Roll </button>
  </div>
`;
function renderStage(diceMap, elem) {
  elem.appendChild(stageTemplate.content.cloneNode(true));
  const rollButton = elem.querySelector(".roll");
  const dice = elem.querySelector(".dice");

  rollButton.onclick = () => updateDice(Math.floor(Math.random() * 6) + 1);

  const updateDice = (value) => {
    // Unicode 0x2680-0x2685 are the sides of a die (⚀⚁⚂⚃⚄⚅).
    dice.textContent = String.fromCodePoint(0x267f + value);
  };
  updateDice(1);
}
```

## <a name="connect-stage-view-to-fluid-data"></a>Connecter la vue de la scène aux données sur les fluides

### <a name="modify-fluid-data"></a>Modifier les données sur les fluides

Pour commencer à utiliser Fluid dans l'application, la première chose à changer est ce qui se passe lorsque l'utilisateur sélectionne l'icône `rollButton` . Au lieu de mettre à jour l'état local directement, le bouton met à jour le nombre stocké dans la `value`clé de l'objet passé en`diceMap`. Comme le `diceMap`est un fluide`SharedMap`, les changements sont distribués à tous les clients. Toute modification de la vue `diceMap`provoquera`valueChanged` l'émission d'un événement, et un gestionnaire d'événements pourra déclencher une mise à jour de la vue.

Ce modèle est courant dans Fluid car il permet à la vue de se comporter de la même manière pour les modifications locales et à distance.

```js
rollButton.onclick = () =>
  diceMap.set("dice-value-key", Math.floor(Math.random() * 6) + 1);
```

### <a name="rely-on-fluid-data"></a>S'appuyer sur les données relatives aux fluides

La prochaine modification à apporter est de changer la `updateDice`fonction pour qu'elle n'accepte plus une valeur arbitraire. Cela signifie que l'application ne peut plus modifier directement la valeur locale des dés. Au lieu de cela, la valeur est récupérée dans la base de données à `SharedMap`chaque fois`updateDice` qu'elle est appelée.

```js
const updateDice = () => {
  const diceValue = diceMap.get("dice-value-key");
  dice.textContent = String.fromCodePoint(0x267f + diceValue);
};
updateDice();
```

### <a name="handle-remote-changes"></a>Gérer les changements à distance

Les valeurs renvoyées ne `diceMap` sont qu'un instantané dans le temps. Pour que les données restent à jour au fur et à mesure de leur modification, un gestionnaire d'événement doit être défini sur `diceMap`l'appel`updateDice` à chaque fois`valueChanged` que l'événement est envoyé. Pour obtenir une liste des événements déclenchés et des valeurs transmises à ces événements, voir [SharedMap](https://fluidframework.com/docs/data-structures/map/).

```js
diceMap.on("valueChanged", updateDice);
```

## <a name="write-the-side-panel-view"></a>Écrire la vue du panneau latéral

La vue du panneau latéral, chargée par l'intermédiaire de l'onglet `contentUrl`avec le`sidePanel` contexte du cadre, est affichée à l'utilisateur dans un panneau latéral lorsqu'il ouvre votre application dans une réunion. L'objectif de cette vue est de permettre à l'utilisateur de sélectionner le contenu de l'application avant de la partager avec la scène de réunion. Pour les applications SDK Live Share, la vue du panneau latéral peut également être utilisée comme expérience complémentaire pour l'application. L'appel de [joinContainer()](/javascript/api/@microsoft/live-share/liveshareclient#@microsoft-live-share-liveshareclient-joincontainer) à partir de la vue du panneau latéral permet de se connecter au même conteneur Fluid que celui auquel la vue de la scène est connectée. Ce conteneur peut ensuite être utilisé pour communiquer avec la vue de la scène. Assurez-vous que vous communiquez avec la vue de la scène _et_ du panneau latéral de chacun.

La vue du panneau latéral de l'échantillon invite l'utilisateur à sélectionner le bouton «Partager sur scène».

```js
const sidePanelTemplate = document.createElement("template");

sidePanelTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Lets get started</p>
    <p class="text">Press the share to stage button to share Dice Roller to the meeting stage.</p>
  </div>
`;

function renderSidePanel(elem) {
  elem.appendChild(sidePanelTemplate.content.cloneNode(true));
}
```

## <a name="write-the-settings-view"></a>Écrire la vue des paramètres

La vue des paramètres, chargée dans le manifeste de `configurationUrl` votre application, est présentée à l'utilisateur lorsqu'il ajoute pour la première fois votre application à une réunion Teams. Cette vue permet au développeur de configurer `contentUrl` l'onglet qui est épinglé à la réunion en fonction des entrées de l'utilisateur. Cette page est actuellement requise même si aucune entrée utilisateur n'est nécessaire pour définir le `contentUrl`.

> [!NOTE]
> [JoinContainer() du partage](/javascript/api/@microsoft/live-share/liveshareclient#@microsoft-live-share-liveshareclient-joincontainer) en direct n’est pas pris en charge dans le contexte de l’onglet`settings`.

La vue des paramètres de l'échantillon invite l'utilisateur à sélectionner le bouton d'enregistrement.

```js
const settingsTemplate = document.createElement("template");

settingsTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Welcome to Dice Roller!</p>
    <p class="text">Press the save button to continue.</p>
  </div>
`;

function renderSettings(elem) {
  elem.appendChild(settingsTemplate.content.cloneNode(true));

  // Save the configurable tab
  pages.config.registerOnSaveHandler((saveEvent) => {
    pages.config.setConfig({
      websiteUrl: window.location.origin,
      contentUrl: window.location.origin + "?inTeams=1&view=content",
      entityId: "DiceRollerFluidLiveShare",
      suggestedDisplayName: "DiceRollerFluidLiveShare",
    });
    saveEvent.notifySuccess();
  });

  // Enable the Save button in config dialog
  pages.config.setValidityState(true);
}
```

## <a name="test-locally"></a>Test local

Vous pouvez tester votre application localement, en utilisant `npm run start`. Pour plus d'informations, voir le [Guide de démarrage rapide](./teams-live-share-quick-start.md).

## <a name="test-in-teams"></a>Tester dans Teams

Une fois que vous avez commencé à exécuter votre application localement avec `npm run start` , vous pouvez ensuite tester votre application sur Teams. Si vous souhaitez tester votre application sans la déployer, téléchargez et utilisez le service de [`ngrok`](https://ngrok.com/) tunneling.

### <a name="create-a-ngrok-tunnel-to-allow-teams-to-reach-your-app"></a>Créez un tunnel ngrok pour permettre aux équipes d'atteindre votre application.

1. [Téléchargez ngrok](https://ngrok.com/download).

1. Utilisez ngrok pour créer un tunnel avec le port 8080. Exécutez la commande suivante :

   ```bash
    ngrok http 8080 --host-header=localhost
   ```

   Un nouveau terminal ngrok s'ouvre avec une nouvelle url, par exemple `https:...ngrok.io`. La nouvelle URL est le tunnel qui pointe vers votre application, qui doit être mise à jour dans votre application `manifest.json`.

### <a name="create-the-app-package-to-sideload-into-teams"></a>Créez le paquet d'applications à charger dans Teams.

1. Allez dans le dossier d'échantillons`\live-share-sdk\samples\01.dice-roller` du lanceur de dés sur votre ordinateur. Vous pouvez également vérifier [`.\manifest\manifest.json`](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller/manifest) l'échantillon de Dice Roller sur GitHub.

1. Ouvrez manifest.json et mettez à jour l'URL de configuration.

   Remplacez `https://<<BASE_URI_DOMAIN>>` par votre point de terminaison http de ngrok.

1. Vous pouvez mettre à jour les champs suivants :

   - Définissez `developer.name` votre nom.
   - Mettez à jour `developer.websiteUrl` avec votre site web.
   - Mettez à jour `developer.privacyUrl` avec votre stratégie de confidentialité.
   - Mettez à jour `developer.termsOfUseUrl` avec vos conditions d'utilisation.

1. Zippez le contenu du dossier du manifeste pour créer un fichier `manifest.zip`. Assurez-vous que le `manifest.zip`contient uniquement le `manifest.json`fichier source`color`, l'icône et `outline`l'icône.

   1. Sous Windows, sélectionnez tous les fichiers du `.\manifest` répertoire et compressez-les.

   > [!NOTE]
   >
   > - Ne zippez pas le dossier qui le contient.
   > - Donnez un nom descriptif à votre fichier zip. Par exemple : `DiceRollerLiveShare`.

   Pour plus d'informations sur le manifeste, visitez la [documentation sur le manifeste Teams](../resources/schema/manifest-schema.md) 

### <a name="sideload-your-app-into-a-meeting"></a>Chargez votre application dans une réunion

1. Ouvrir Teams.

1. Planifiez une réunion à partir du calendrier dans Teams. Veillez à inviter au moins un participant à la réunion.

1. Rejoindre la réunion.

1. Dans la fenêtre de réunion en haut, sélectionnez **+ Applications** > **Gérer les applications**.

1. Dans le volet **Gérer les applications**, sélectionnez **Télécharger une application** personnalisée .

   1. Si vous ne voyez pas l'option **Télécharger une application personnalisée**, suivez les [instructions](/microsoftteams/teams-custom-app-policies-and-settings) pour activer les applications personnalisées dans votre locataire.

1. Sélectionnez et téléchargez le `manifest.zip` fichier depuis votre ordinateur.

1. Sélectionnez **Ajouter** pour ajouter votre application modèle à la réunion.

1. Sélectionnez **+ Applications**, tapez Lancer de dés dans le champ de **recherche Trouver une** application.

1. Sélectionnez l'application pour l'activer dans la réunion.

1. Sélectionnez **Enregistrer**.

   L'application du lanceur de dés est ajoutée au panneau de réunion Teams.

1. Dans le panneau latéral, sélectionnez l'icône de partage vers la scène. Teams lance une synchronisation en direct avec les utilisateurs de la scène de la réunion.

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-to-stage.png" alt-text="icône partager vers une étape":::

   Vous devriez maintenant voir le lanceur de dés sur la scène de la réunion.

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-meeting-stage.png" alt-text="image de la phase de réunion":::

Les utilisateurs invités à la réunion peuvent voir votre application sur scène lorsqu'ils rejoignent la réunion.

## <a name="deployment"></a>Déploiement

Lorsque vous êtes prêt à déployer votre code, vous pouvez utiliser [Teams Toolkit](../toolkit/provision.md#provision-using-teams-toolkit-in-visual-studio-code) ou [le portail des développeurs Teams](https://dev.teams.microsoft.com/apps) pour provisionner et télécharger le fichier zip de votre application.

> [!NOTE]
> Vous devez ajouter votre appId provisionné à la liste`manifest.json` avant de télécharger ou de distribuer l'application.

## <a name="code-samples"></a>Exemples de code

| Exemple de nom | Description                                                     | JavaScript                                                                           |
| :---------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Lanceur de dés | Permettre à tous les clients connectés de lancer un dé et de visualiser le résultat. | [View](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Capacités principales](teams-live-share-capabilities.md)

## <a name="see-also"></a>Voir aussi

- [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
- [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Documents de référence du kit SDK Live Share Media](/javascript/api/@microsoft/live-share-media/)
- [FAQ Live Share](teams-live-share-faq.md)
- [Applications Teams dans les réunions](teams-apps-in-meetings.md)
