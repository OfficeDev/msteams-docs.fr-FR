---
title: Exemples de code Microsoft teams
description: Liens et descriptions des exemples d’applications pour la plateforme de développement Microsoft teams
keywords: Exemples de développeurs Microsoft teams
ms.openlocfilehash: eb7794e788f8eb39102ac874748e23d8621f281e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673523"
---
# <a name="code-samples-for-the-microsoft-teams-developer-platform"></a>Exemples de code pour la plateforme de développement Microsoft teams

Vous trouverez ici une liste d’exemples de code qui illustrent les différentes fonctionnalités de la plateforme de développement Microsoft teams et comment créer des applications pour tirer parti de ces fonctionnalités.

## <a name="getting-samples"></a>Obtenir des exemples

Pour télécharger nos exemples à partir de GitHub :

1. Sélectionnez l’un des projets mentionnés ci-dessous et ouvrez le projet dans GitHub.
2. Choisissez le **Clone ou** le bouton Télécharger, puis copiez l’URL.
3. Ouvrez une invite de commandes dans le répertoire parent dans lequel vous souhaitez installer l’exemple de projet.
4. Générer`git clone <pasted url>`

### <a name="for-netc-samples"></a>Pour obtenir des exemples .NET/C#

Chacun de nos exemples .NET comprend un fichier de solution Visual Studio qui peut créer entièrement la solution, y compris la restauration des packages NuGet.

### <a name="for-nodejs-samples"></a>Pour les exemples node. js

Nous fournissons un fichier Packages. JSON qui répertorie tous les packages requis pour un exemple. Il suffit `npm install` de l’exécuter à partir de la ligne de commande dans le répertoire de votre projet node. js pour installer les packages requis. Vous êtes maintenant prêt à ouvrir le projet dans Visual Studio code et à commencer à expérimenter.

### <a name="for-other-samples"></a>Pour d’autres exemples

Comme toujours, le fichier Lisez-moi du projet doit contenir plus d’informations sur les besoins spécifiques d’exemples spécifiques.

## <a name="get-started"></a>Prise en main

| Exemple | Description|
|--------|-------------|
| [Hello World dans Microsoft teams avec node. js](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) | Exemple d’application de `Node.js` teams qui vous présente les fonctionnalités de base de l’application.|
| [Hello World dans Microsoft teams avec C# .NET](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) | Exemple d’application de `C# .NET` teams qui vous présente les fonctionnalités de base de l’application.|
| [Prise en main du générateur Yeoman pour teams](~/tutorials/get-started-yeoman.md) | Créer une application teams de toutes pièces à l’aide du générateur Yeoman pour Microsoft Teams. |

## <a name="bots-using-the-v4-sdk"></a>Robots (avec le kit de développement logiciel v4)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="messaging-extensions-using-the-v4-sdk"></a>Extensions de messagerie (à l’aide du kit de développement v4)

| Exemple | Description | .NET Core | JavaScript |
|--------|------------- |---|---|
| Commande de recherche | Extension de messagerie simple avec une commande de recherche | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|
| Commande action | Extension de messagerie simple avec une commande action. Réponse insérée dans la zone de message de composition. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)|
| Commande d’action avec réponse de robot | Extension de messagerie avec une commande action. Réponse insérée dans la conversation par le bot. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview)|
| Commande de recherche | extension de messagerie avec une commande de recherche, ainsi qu’une authentification et une configuration | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="outgoing-webhooks"></a>Webhooks sortants

| Exemple | Description
|--------|-------------
| [Webhook sortant pour C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Illustre comment créer un **webhook sortant** pour Microsoft teams dans C#/.net.
| [Webhook sortant pour node. js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Illustre comment créer un **webhook sortant** simple pour Microsoft teams dans les lignes ~ 50 du code node. js.

## <a name="connectors"></a>Connecteurs

| Exemple | Description
|--------|-------------
| [Exemple de connecteur pour node. js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | Cet exemple, écrit dans node. js, montre comment créer un connecteur pour Microsoft teams à l’aide de GitHub comme exemple pour générer des notifications de connecteur.
| [Exemple de connecteur pour C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | Cet exemple, écrit en C#, montre comment créer un connecteur pour Microsoft teams à l’aide d’un exemple d’application de liste de tâches comme exemple pour générer des notifications de connecteur.

## <a name="graph-api"></a>API Graph

| Exemple | Description
|--------|-------------
| [Exemples d’API Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | Ces exemples montrent comment utiliser les appels de l’API Microsoft Graph pour effectuer des tâches telles que l’interrogation de teams et de canaux à partir d’un service Web s’exécutant en dehors de Microsoft Teams.

## <a name="others"></a>Autres

| Code | Description |
|------|------------- |
| [Exemple complet dans node. js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) | Cet exemple montre comment utiliser toutes les fonctionnalités de la plateforme Microsoft Teams. Remarque : cet exemple utilise le kit de développement logiciel (SDK) de robot v3.|
| [Exemple complet en C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) | Cet exemple montre comment utiliser toutes les fonctionnalités de la plateforme Microsoft Teams. Remarque : cet exemple utilise le kit de développement logiciel (SDK) de robot v3. |
| [Applications métiers en C#/.NET](https://github.com/OfficeDev/msteams-sample-line-of-business-apps-csharp) | Ce référentiel contient plusieurs exemples d’applications professionnelles pouvant être utilisées pour l’inspiration ou en tant que modèles à développer. Remarque : ces exemples utilisent le kit de développement logiciel (SDK) de robot v3.|
| [Exemple d’application d’onglet de liste de tâches](https://github.com/OfficeDev/microsoft-teams-sample-todo) | Cet exemple node. js montre combien il est facile de convertir une application Web existante en onglet. |
| [Orky](https://github.com/OfficeDev/Orky) | Vous pouvez utiliser Orky pour enregistrer votre propre robot local dans Microsoft teams et exécuter des scripts depuis n’importe quel endroit. |
| [Build 2017 météo](https://github.com/OfficeDev/microsoft-teams-build2017-weather) | Obsolètes. Code source de la session//Build 2017 pour ajouter un onglet météo à l’application squelette générée précédemment dans la session. |

### <a name="bot-framework-sdk-v3-samples"></a>Exemples du kit de développement logiciel SDK v3

| Exemple | Description |
|--------|------------- |
| [Exemple de bot pour C#/.NET](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Exemples de bot Framework v3|
| [Exemple de bot pour node. js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Exemples de bot Framework v3 |
