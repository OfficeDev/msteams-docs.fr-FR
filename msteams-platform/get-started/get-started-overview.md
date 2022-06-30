---
title: Démarrage - Vue d’ensemble
description: Dans ce module, découvrez comment prendre en main la documentation des développeurs Microsoft Teams qui vous présente les outils courants, les concepts fondamentaux et les fonctionnalités avancées.
ms.localizationpriority: high
ms.topic: reference
ms.openlocfilehash: 4a53466aab1a896e99b91210dbc93d8467df52d1
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503899"
---
# <a name="get-started"></a>Prise en main

Bienvenue dans Démarrage pour créer et déployer des applications personnalisées pour Microsoft Teams !

Suivez les étapes pour créer une application Teams de base et réelle. Le Démarrage vous présente également des outils courants, des concepts fondamentaux et des fonctionnalités plus avancées.

Voici une idée de ce que vous allez apprendre :

- Devenez rapidement opérationnel avec le Kit de ressources Microsoft Teams (extension Visual Studio Code).
- Bénéficiez d’une expérience avec le Kit de ressources et les Kits de développement logiciel (SDK).
- Configurez et générez différents types d’applications Teams.

Examinons rapidement les options d’environnement de build parmi lesquelles vous pouvez choisir, ainsi que la feuille de route pour créer et déployer une application Teams.

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="Illustration montrant les étapes de base pour créer et déployer une application Teams" border="true":::

## <a name="app-capabilities-and-development-tools"></a>Fonctionnalités d’application et outils de développement

Selon les fonctionnalités souhaitées pour votre application, choisissez un ensemble d’outils de développement approprié.

| Fonctionnalités de l’application | Interactions utilisateur | Outils recommandés | Kits de développement logiciel (SDK) | Piles/langues technologiques |
|--------|-------------|--------|--------|--------|
| Onglets | Une expérience web incorporée en plein écran. | Microsoft Visual Studio Code avec une extension de kit de ressources Teams, ou [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) si vous préférez utiliser CLI | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) pour les bibliothèques principales et [SDK client Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) pour les fonctionnalités de l’interface utilisateur | Technologie web en général, HTML, CSS et JavaScript (incl. React). |
| Bots | Bot de conversation qui discute avec les membres. | Visual Studio Code avec une extension de kit de ressources Teams ,ou [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) et [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C#, Java et Python. |
| Extensions de messages | Raccourcis permettant d’insérer du contenu externe dans une conversation ou d’agir sur des messages. | Visual Studio Code avec une extension de kit de ressources Teams ,ou [CLI TeamsFx](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [SDK TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) et [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C#, Java et Python. |

*Vous n’êtes pas limité à l’utilisation de ces piles particulières !*

Si vous êtes déjà familiarisé avec le workflow Yeoman, vous préférerez peut-être utiliser [Générateur Yeoman yoTeams](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) pour créer vos applications.

> [!WARNING]
> Si vous utilisez App Studio, nous vous recommandons d’essayer le Developer Portal pour configurer, distribuer et gérer vos applications Teams.<br> App Studio sera déconseillé d’ici le 30 juin 2022.

## <a name="build-your-first-teams-app"></a>Créer votre première application Teams

Nous allons maintenant créer votre première application Teams. Tout d’abord, choisissez votre langage (ou infrastructure) et préparez votre environnement de développement.

> [!div class="nextstepaction"]
> [Créer une application d’onglet Teams avec JavaScript à l’aide de React](../sbs-gs-javascript.yml)
> [!div class="nextstepaction"]
> [Créer une application de bot Teams avec JavaScript](../sbs-gs-bot.yml)
> [!div class="nextstepaction"]
> [Créer une application à extension messagerie Teams avec JavaScript à l’aide de React](../sbs-gs-msgext.yml)
> [!div class="nextstepaction"]
> [Créer une application Teams à l’aide de Blazor](../sbs-gs-blazorupdate.yml)
> [!div class="nextstepaction"]
> [Créer une application Teams avec SPFx](../sbs-gs-spfx.yml)
> [!div class="nextstepaction"]
> [Créer une application Teams avec C# ou .NET](../sbs-gs-csharp.yml)
> [!div class="nextstepaction"]
> [Créer une application Teams avec node.js](../sbs-gs-nodejs.yml)
> [!div class="nextstepaction"]
> [Générer un bot de notification avec JavaScript](../sbs-gs-notificationbot.yml)
> [!div class="nextstepaction"]
> [Créer un bot de commandes avec JavaScript](../sbs-gs-commandbot.yml)
> [!div class="nextstepaction"]

## <a name="see-also"></a>Voir aussi

* [Exemples Microsoft Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples#microsoft-teams-samples)
* [Ressources Git et GitHub](/contribute/additional-resources)
