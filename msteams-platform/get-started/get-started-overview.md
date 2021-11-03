---
title: Mise en place - Vue d’ensemble
description: Vue d’ensemble de la documentation Microsoft Teams développeur
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams exemples de développeur
ms.openlocfilehash: 0b2ded130bf68f1db8715c8ff6e10336db6aeb2c
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720088"
---
# <a name="get-started"></a>Prise en main

Bienvenue dans la création et le déploiement d’applications personnalisées pour Microsoft Teams !

Parcourir les étapes pour créer une application de base Teams réelle. La mise en place vous présente également des outils courants, des concepts fondamentaux et des fonctionnalités plus avancées.

Voici une idée de ce que vous allez apprendre :

- Rapidement opérationnel avec le Microsoft Teams Shared Computer Toolkit (une extension Visual Studio Code).
- Obtenez de l’expérience avec les Shared Computer Toolkit et les SDK.
- Configurez et créez différents types d’Teams applications.

Examinons rapidement les options de l’environnement de création que vous pouvez choisir et la feuille de route pour la création et le déploiement d’Teams app.

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="Illustration montrant les étapes de base pour créer et déployer une Teams application.":::

## <a name="app-capabilities-and-development-tools"></a>Fonctionnalités d’application et outils de développement

Selon les fonctionnalités de votre application, choisissez un ensemble d’outils de développement approprié.

| Fonctionnalités de l’application | Interactions avec l’utilisateur | Outils recommandés | Kits de développement logiciel (SDK) | Piles/langues technologiques |
|--------|-------------|--------|--------|--------|
| Onglets | Une expérience web incorporée en plein écran. | VS Code avec une extension Teams Shared Computer Toolkit ou [l’CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) si vous préférez utiliser CLI | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) pour lesibs principaux et [SDK Teams client pour](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) les fonctionnalités d’interface utilisateur | Technologie web en général, HTML, CSS et JavaScript (incl. React). |
| Bots | Bot de conversation qui converse avec les membres. | VS Code avec une extension Teams Shared Computer Toolkit, ou [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) et [SDK Bot Framework](https://dev.botframework.com/) | Node.js, C#, Java et Python. |
| Extensions de messagerie | Raccourcis pour insérer du contenu externe dans une conversation ou prendre des mesures sur les messages. | VS Code avec une extension Teams Shared Computer Toolkit, ou [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) et [SDK Bot Framework](https://dev.botframework.com/) | Node.js, C#, Java et Python. |

*Vous n’êtes pas limité à l’utilisation de ces piles particulières !*

Si vous connaissez déjà le flux de travail Yeoman, vous préférez peut-être utiliser le générateur [Yeoman YoTeams](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) pour créer vos applications.

> [!NOTE]
> Si vous utilisez App Studio, nous vous recommandons d’essayer le Portail des développeurs pour configurer, distribuer et gérer vos applications Teams client.


## <a name="build-your-first-teams-app"></a>Créer votre première application Teams de messagerie

Maintenant, nous allons créer votre première Teams application. Tout d’abord, sélectionnez votre langue (ou votre infrastructure) et préparez votre environnement de développement.

> [!div class="nextstepaction"]
> [Créer une application Teams avec JavaScript à l’aide de React](../sbs-gs-javascript.yml)

> [!div class="nextstepaction"]
> [Créer une application Teams avec Blazor](../sbs-gs-blazor.yml)

> [!div class="nextstepaction"]
> [Créer une application Teams avec SPFx](../sbs-gs-spfx.yml)

> [!div class="nextstepaction"]
> [Créer une application Teams avec C# ou .NET](../sbs-gs-csharp.yml)

> [!div class="nextstepaction"]
> [Créer une application Teams avec Node.js](../sbs-gs-nodejs.yml)

