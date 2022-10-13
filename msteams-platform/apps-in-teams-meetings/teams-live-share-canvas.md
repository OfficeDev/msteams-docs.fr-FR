---
title: Vue d’ensemble du canevas Live Share
author: surbhigupta
description: Dans ce module, découvrez-en plus sur le canevas Live Share, une extension activant l’entrée manuscrite, les pointeurs laser et les curseurs pour les applications de réunion.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 10/04/2022
ms.openlocfilehash: 9d1a776432f728c1e56caa357089be6e47c17e4c
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560609"
---
# <a name="live-share-canvas-overview"></a>Vue d’ensemble du canevas Live Share

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-docs-feature-1.png" alt-text="Capture d’écran montrant un exemple de canevas synchronisé avec d’autres participants à une réunion Teams.":::

Dans les salles de conférence et les salles de classe du monde entier, les tableaux blancs sont un élément essentiel de la collaboration. Dans les temps modernes cependant, le tableau blanc n’est plus suffisant. Avec de nombreux outils numériques tels que PowerPoint étant le point focal de collaboration à l’ère moderne, il est essentiel d’activer le même potentiel créatif.

Pour permettre une collaboration plus transparente, Microsoft a créé PowerPoint Live, qui est devenu essentiel à la façon dont les utilisateurs travaillent dans Teams. Les présentateurs peuvent annoter les diapositives pour que tout le monde puisse les voir, en utilisant des stylos, des surligneurs et des pointeurs laser pour attirer l’attention sur les concepts clés. À l’aide du canevas Live Share, votre application peut apporter la puissance de PowerPoint Live outils d’entrée manuscrite avec un minimum d’efforts.

## <a name="install"></a>Installer

Pour ajouter la dernière version du Kit de développement logiciel (SDK) à votre application à l’aide de npm :

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-canvas@next --save
```

OR

Pour ajouter la dernière version du Kit de développement logiciel (SDK) à votre application à l’aide de [Yarn](https://yarnpkg.com/) :

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-canvas@next
```

## <a name="setting-up-the-package"></a>Configuration du package

Le canevas Live Share a deux classes principales qui permettent la collaboration clé en temps réel : `InkingManager` et `LiveCanvas`. `InkingManager` est responsable de l’attachement d’un élément complet `<canvas>` à votre application, tout en `LiveCanvas` gérant la synchronisation à distance avec d’autres participants à la réunion. Utilisée ensemble, votre application peut avoir des fonctionnalités de tableau blanc complètes en quelques lignes de code.

| Classes                                                                     | Description                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [InkingManager](/javascript/api/@microsoft/live-share-canvas/inkingmanager) | Classe qui attache un `<canvas>` élément à un donné `<div>` pour gérer automatiquement les traits de stylet ou de surligneur, le pointeur laser, les lignes et les flèches et les gommes. Expose un ensemble d’API (pour contrôler l’outil actif) et les paramètres de configuration de base. |
| [LiveCanvas](/javascript/api/@microsoft/live-share-canvas/livecanvas)      | Classe `SharedObject` qui synchronise les traits et les positions des curseurs à partir de `InkingManager` tous les utilisateurs d’une session Live Share.                                                                                                                   |

Exemple :

```html
<body>
  <div id="canvas-host"></div>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const { liveCanvas } = container.initialObjects;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";
import { ContainerSchema } from "fluid-framework";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const liveCanvas = container.initialObjects.liveCanvas as LiveCanvas;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

---

## <a name="canvas-tools-and-cursors"></a>Outils et curseurs de canevas

Maintenant que le canevas Live Share est configuré et synchronisé, vous pouvez configurer le canevas pour l’interaction utilisateur, par exemple des boutons pour sélectionner un outil de stylet. Dans cette section, nous allons discuter des outils disponibles et de leur utilisation.

### <a name="inking-tools"></a>Outils d’entrée manuscrite

Chaque outil d’entrée manuscrite dans le canevas Live Share affiche des traits au fur et à mesure que les utilisateurs dessinent. Si vous utilisez un écran tactile ou un stylet, les outils prennent également en charge la dynamique de pression, ce qui affecte la largeur du trait. Les paramètres de configuration incluent la couleur du pinceau, l’épaisseur, la forme et une flèche de fin facultative.

#### <a name="pen-tool"></a>Outil Stylet

:::image type="content" source="../assets/images/teams-live-share/canvas-pen-tool.gif" alt-text="GIF montre un exemple de traits de dessin sur le canevas à l’aide de l’outil de stylet.":::

L’outil de stylet dessine des traits solides qui sont stockés dans le canevas. La forme d’extrémité par défaut est un cercle.

```html
<div>
  <button id="pen">Enable Pen</button>
  <label for="pen-color">Select a color:</label>
  <input type="color" id="color" name="color" value="#000000" />
  <button id="pen-tip-size">Increase pen size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to pen
document.getElementById("pen").onclick = () => {
  inkingManager.tool = InkingTool.pen;
};
// Change the selected color for pen
document.getElementById("pen-color").onchange = () => {
  const colorPicker = document.getElementById("color");
  inkingManager.penBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for pen
document.getElementById("pen-tip-size").onclick = () => {
  inkingManager.penBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="highlighter-tool"></a>Outil de surligneur

:::image type="content" source="../assets/images/teams-live-share/canvas-highlighter-tool.gif" alt-text="GIF montre un exemple de dessin de traits translucides sur le canevas à l’aide de l’outil de surligneur.":::

L’outil de surligneur dessine des traits translucides qui sont stockés dans le canevas. La forme d’extrémité par défaut est un carré.

```html
<div>
  <button id="highlighter">Enable Highlighter</button><br />
  <label for="highlighter-color">Select a color:</label>
  <input type="color" id="highlighter-color" name="highlighter-color" value="#FFFC00" />
  <button id="highlighter-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to highlighter
document.getElementById("highlighter").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for highlighter
document.getElementById("highlighter-color").onchange = () => {
  const colorPicker = document.getElementById("highlighter-color");
  inkingManager.highlighterBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for highlighter
document.getElementById("highlighter-tip-size").onclick = () => {
  inkingManager.highlighterBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="eraser-tool"></a>Outil Gomme

:::image type="content" source="../assets/images/teams-live-share/canvas-eraser-tool.gif" alt-text="GIF montre un exemple d’effacement de traits sur le canevas à l’aide de l’outil gomme.":::

L’outil gomme efface les traits entiers qui croisent son chemin.

```html
<div>
  <button id="eraser">Enable Eraser</button><br />
  <button id="eraser-size">Increase eraser size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("eraser").onclick = () => {
  inkingManager.tool = InkingTool.eraser;
};
// Increase the tip size for eraser
document.getElementById("eraser-size").onclick = () => {
  inkingManager.eraserSize = inkingManager.eraserSize + 1;
};
```

#### <a name="point-eraser-tool"></a>Outil d’effacement de point

:::image type="content" source="../assets/images/teams-live-share/canvas-point-eraser-tool.gif" alt-text="GIF montre un exemple de suppression de points individuels dans des traits sur le canevas à l’aide de l’outil d’effacement de points.":::

L’outil d’effacement de points efface les points individuels dans les traits qui croisent son chemin en fractionnant les traits existants en deux. Cet outil est coûteux sur le plan du calcul et peut entraîner des taux d’images plus lents pour vos utilisateurs.

> [!NOTE]
> L’effaceur de points partage la même taille de point de gomme que l’outil gomme standard.

```html
<div>
  <button id="point-eraser">Enable Point Eraser</button><br />
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("point-eraser").onclick = () => {
  inkingManager.tool = InkingTool.pointEraser;
};
```

#### <a name="laser-pointer"></a>Pointeur laser

:::image type="content" source="../assets/images/teams-live-share/canvas-laser-tool.gif" alt-text="GIF montre un exemple de traits de dessin sur le canevas à l’aide de l’outil pointeur laser.":::

Le pointeur laser est unique car l’extrémité du laser a un effet de fin lorsque vous déplacez votre souris. Lorsque vous dessinez des traits, l’effet de fin s’affiche pendant une courte période avant qu’il ne s’efface complètement. Cet outil est parfait pour signaler des informations à l’écran lors d’une réunion, car le présentateur n’a pas besoin de basculer entre les outils pour effacer les traits.

```html
<div>
  <button id="laser">Enable Laser Pointer</button><br />
  <label for="laser-color">Select a color:</label>
  <input type="color" id="laser-color" name="laser-color" value="#000000" />
  <button id="laser-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to laser pointer
document.getElementById("laser").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for laser pointer
document.getElementById("laser-color").onchange = () => {
  const colorPicker = document.getElementById("laser-color");
  inkingManager.laserPointerBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for laser pointer
document.getElementById("laser-tip-size").onclick = () => {
  inkingManager.laserPointerBrush.tipSize = inkingManager.laserPointerBrush.tipSize + 1;
};
```

#### <a name="line-and-arrow-tools"></a>Outils de ligne et de flèche

:::image type="content" source="../assets/images/teams-live-share/canvas-line-tool.gif" alt-text="GIF montre un exemple de dessin de lignes droites sur un canevas à l’aide de l’outil de ligne et de flèche.":::

L’outil de ligne permet aux utilisateurs de dessiner des lignes droites d’un point à un autre, avec une flèche facultative qui peut être appliquée à la fin.

```html
<div>
  <button id="line">Enable Line</button><br />
  <button id="line-arrow">Enable Arrow</button><br />
  <input type="color" id="line-color" name="line-color" value="#000000" />
  <button id="line-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to line
document.getElementById("line").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "none";
};
// Change the selected tool to line
document.getElementById("line-arrow").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "open";
};
// Change the selected color for lineBrush
document.getElementById("line-color").onchange = () => {
  const colorPicker = document.getElementById("line-color");
  inkingManager.lineBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for lineBrush
document.getElementById("line-tip-size").onclick = () => {
  inkingManager.lineBrush.tipSize = inkingManager.lineBrush.tipSize + 1;
};
```

#### <a name="clear-all-strokes"></a>Effacer tous les traits

Vous pouvez effacer tous les traits dans le canevas en appelant `inkingManager.clear()`. Cela supprime tous les traits du canevas.

### <a name="cursors"></a>Curseurs

:::image type="content" source="../assets/images/teams-live-share/canvas-cursors.gif" alt-text="GIF montre un exemple d’utilisateurs partageant un curseur sur un canevas.":::

Vous pouvez activer les curseurs actifs dans votre application pour permettre aux utilisateurs de suivre les positions des curseurs les uns des autres sur le canevas. Contrairement aux outils d’entrée manuscrite, les curseurs fonctionnent entièrement via la `LiveCanvas` classe. Vous pouvez éventuellement fournir un nom et une image pour identifier chaque utilisateur. Vous pouvez activer les curseurs séparément ou avec les outils d’entrée manuscrite.

```javascript
// Optional. Set user display info
liveCanvas.onGetLocalUserInfo = () => {
  return {
    displayName: "YOUR USER NAME",
    pictureUri: "YOUR USER PICTURE URI",
  };
};
// Toggle Live Canvas cursor enabled state
liveCanvas.isCursorShared = !isCursorShared;
```

## <a name="optimizing-across-devices"></a>Optimisation entre les appareils

Pour la plupart des applications sur le web, le contenu s’affiche différemment en fonction de la taille de l’écran ou de l’état variable de l’application. Si `InkingManager` elle n’est pas optimisée correctement pour votre application, cela peut entraîner l’apparition de traits et de curseurs différemment pour chaque utilisateur. Le canevas Live Share prend en charge un ensemble simple d’API, qui permet d’ajuster les `<canvas>` positions des traits pour s’aligner correctement avec votre contenu.

Par défaut, le canevas Live Share fonctionne beaucoup comme une application de tableau blanc, le contenu étant centré sur la fenêtre d’affichage avec un niveau de zoom 1x. Seule une partie du contenu est affichée dans les limites visibles du `<canvas>`. D’un point de vue conceptuel, c’est comme enregistrer une vidéo à partir d’une vue aérienne. Alors que la fenêtre d’affichage de la caméra enregistre une partie du monde en dessous, le monde réel s’étire presque à l’infini dans toutes les directions.

Voici un diagramme simple pour vous aider à visualiser ce concept :

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-capabilities-docs-diagram-1.png" alt-text="Capture d’écran montrant la disposition du canevas en plein écran pour les utilisateurs de bureau et mobiles ensemble.":::

Vous pouvez personnaliser ce comportement de la manière suivante :

- Modification du point de référence de départ vers le coin supérieur gauche du canevas.
- Modifiez les positions x et y du décalage de pixels de la fenêtre d’affichage.
- Modifiez le niveau d’échelle de la fenêtre d’affichage.

> [!NOTE]
> Les points de référence, les décalages et les niveaux de mise à l’échelle sont locaux pour le client et ne sont pas synchronisés entre les participants à la réunion.

Exemple :

```html
<body>
  <button id="pan-left">Pan left</button>
  <button id="pan-up">Pan up</button>
  <button id="pan-right">Pan right</button>
  <button id="pan-down">Pan down</button>
  <button id="zoom-out">Zoom out</button>
  <button id="zoom-in">Zoom in</button>
  <button id="change-reference">Change reference</button>
</body>
```

```javascript
// ...

// Pan left
document.getElementById("pan-left").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x - 10,
    y: inkingManager.offset.y,
  };
};
// Pan up
document.getElementById("pan-up").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y - 10,
  };
};
// Pan right
document.getElementById("pan-right").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x + 10,
    y: inkingManager.offset.y,
  };
};
// Pan down
document.getElementById("pan-down").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y + 10,
  };
};
// Zoom out
document.getElementById("zoom-out").onclick = () => {
  if (inkingManager.scale > 0.1) {
    inkingManager.scale -= 0.1;
  }
};
// Zoom in
document.getElementById("zoom-in").onclick = () => {
  inkingManager.scale += 0.1;
};
// Change reference
document.getElementById("change-reference").onclick = () => {
  if (inkingManager.referencePoint === "center") {
    inkingManager.referencePoint = "topLeft";
  } else {
    inkingManager.referencePoint = "center";
  }
};
```

## <a name="ideal-scenarios"></a>Scénarios idéaux

Avec les pages web disponibles dans toutes les formes et tailles, il n’est pas possible de créer un canevas Live Share pour prendre en charge tous les scénarios. Le package est idéal pour les scénarios dans lesquels tous les utilisateurs regardent le même contenu en même temps. Bien que tous les contenus ne doivent pas être visibles à l’écran, il doit s’agir d’un contenu qui est mis à l’échelle de manière linéaire sur les appareils.

Voici quelques exemples de scénarios dans lesquels le canevas Live Share est une excellente option pour votre application :

- Superposer des images et des vidéos qui s’affichent avec le même rapport d’aspects sur tous les clients.
- Affichage d’une carte, d’un modèle 3D ou d’un tableau blanc à partir du même angle de rotation.

Les deux scénarios fonctionnent bien, car le contenu peut être affiché de la même manière sur tous les appareils, même si les utilisateurs le regardent avec des niveaux de zoom et des décalages différents. Si la disposition ou le contenu de votre application change en fonction de la taille de l’écran et qu’il n’est pas possible de générer une vue commune pour tous les participants, le canevas Live Share peut ne pas être adapté à votre scénario.

## <a name="code-samples"></a>Exemples de code

| Exemple de nom          | Description                            | JavaScript                                                                                |
| -------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------- |
| Démonstration live canvas     | Application de tableau blanc simple.         | [View](https://github.com/microsoft/live-share-sdk/tree/main/samples/03.live-canvas-demo) |
| Modèle multimédia React | Dessiner sur un lecteur vidéo synchronisé. | [View](https://aka.ms/liveshare-mediatemplate)                                            |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Didacticiel Poker agile](../sbs-teams-live-share.yml)

## <a name="see-also"></a>Voir aussi

- [FAQ sur le Kit de développement logiciel (SDK) de partage en direct](teams-live-share-faq.md)
- [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Documentation de référence sur le Kit de développement logiciel (SDK) Canvas Live Share](/javascript/api/@microsoft/live-share-canvas/)
- [Applications Teams dans les réunions](teams-apps-in-meetings.md)
