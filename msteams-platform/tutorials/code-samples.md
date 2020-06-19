---
title: Exemples de code Microsoft teams
description: Liens et descriptions des exemples d’applications pour la plateforme de développement Microsoft teams
keywords: Exemples de développeurs Microsoft teams
ms.openlocfilehash: 955588608fde694b163104d0a9e9e94289719003
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801111"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Didacticiels et exemples de code pour la plateforme de développement Microsoft teams

Vous trouverez ici une liste de didacticiels et d’exemples de code qui montrent comment vous pouvez étendre les fonctionnalités de la plateforme de développement teams en créant des applications personnalisées.

## <a name="getting-started-with-microsoft-learn"></a>Prise en main de Microsoft apprendre

| Fonctionnalité| Module d’apprentissage|
|--------|-------------|
| Onglets — expériences Web intégrées  |  [Créez des expériences web incorporées avec les onglets pour Microsoft Teams](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Webhooks et connecteurs  |  [Connecter des services web à Microsoft Teams à l’aide de webhooks et de connecteurs Office 365](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|Extensions de messagerie  | [Interactions orientées sur des tâches dans Microsoft Teams avec les extensions de messagerie](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| Modules de tâche |  [Collecter des entrées dans Microsoft teams à l’aide de modules de tâches](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| Bots de conversation  | [Créer des bots conversationnels interactifs pour Microsoft Teams](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>Prise en main des exemples de code

Pour télécharger nos exemples à partir de GitHub :

1. Sélectionnez l’un des projets mentionnés ci-dessous et ouvrez le projet dans GitHub.
2. Choisissez le **Clone ou** le bouton Télécharger, puis copiez l’URL.
3. Ouvrez une invite de commandes dans le répertoire parent dans lequel vous souhaitez installer l’exemple de projet.
4. Générer`git clone <pasted url>`

### <a name="for-netc-samples"></a>Pour obtenir des exemples .NET/C#

Chacun de nos exemples .NET comprend un fichier de solution Visual Studio qui peut créer entièrement la solution, y compris la restauration des packages NuGet.

### <a name="for-nodejs-samples"></a>Pour obtenir des exemples de Node.js

Nous fournissons une packages.jssur le fichier qui répertorie tous les packages requis pour un exemple. Il suffit de `npm install` l’exécuter à partir de la ligne de commande dans votre répertoire de projet Node.js pour installer les packages requis. Vous êtes maintenant prêt à ouvrir le projet dans Visual Studio code et à commencer à expérimenter.

### <a name="for-other-samples"></a>Pour d’autres exemples

Comme toujours, le fichier Lisez-moi du projet doit contenir plus d’informations sur les besoins spécifiques d’exemples spécifiques.

## <a name="bots-using-the-v4-sdk"></a>Robots (avec le kit de développement logiciel v4)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>Visitez le [référentiel d’exemples de l’infrastructure bot](https://github.com/Microsoft/BotBuilder-Samples) pour afficher des exemples centrés sur les tâches de Microsoft bot Framework v4 SDK pour C#, JavaScript, la machine à écrire et Python.

## <a name="messaging-extensions-using-the-v4-sdk"></a>Extensions de messagerie (à l’aide du kit de développement v4)

| Exemple | Description | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| Commande de recherche | Extension de messagerie simple avec une commande de recherche | [Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)| [Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|[Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/50.teams-messaging-extension-search)|
| Commande action | Extension de messagerie simple avec une commande action. Réponse insérée dans la zone de message de composition. | [Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)|[Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/51.teams-messaging-extensions-action)|
| Commande d’action avec réponse de robot | Extension de messagerie avec une commande action. Réponse insérée dans la conversation par le bot. | [Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview)|[Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview)|[Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/53.teams-messaging-extensions-action-preview)|
| Commande de recherche | extension de messagerie avec une commande de recherche, ainsi qu’une authentification et une configuration | [Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)| [Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|[Afficher](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/52.teams-messaging-extensions-search-auth-config)|

## <a name="outgoing-webhooks"></a>Webhooks sortants

| Exemple | Description
|--------|-------------
| [Webhook sortant pour C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Illustre comment créer un **webhook sortant** pour Microsoft teams dans C#/.net.
| [Webhook sortant pour Node.js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Illustre comment créer un **webhook sortant** simple pour Microsoft teams dans des lignes de Node.js environ 50.

## <a name="connectors"></a>Connecteurs

| Exemple | Description
|--------|-------------
| [Exemple de connecteur pour Node.js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | Cet exemple, écrit en Node.js, explique comment créer un connecteur pour Microsoft teams à l’aide de GitHub comme exemple pour générer des notifications de connecteur.
| [Exemple de connecteur pour C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | Cet exemple, écrit en C#, montre comment créer un connecteur pour Microsoft teams à l’aide d’un exemple d’application de liste de tâches comme exemple pour générer des notifications de connecteur.

## <a name="graph-api"></a>API Graph

| Exemple | Description
|--------|-------------
| [Exemples d’API Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | Ces exemples montrent comment utiliser les appels de l’API Microsoft Graph pour effectuer des tâches telles que l’interrogation de teams et de canaux à partir d’un service Web s’exécutant en dehors de Microsoft Teams.

### <a name="bot-framework-sdk-v3-samples"></a>Exemples du kit de développement logiciel SDK v3

| Exemple | Description |
|--------|------------- |
| [Exemple de bot pour C#/.NET](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Exemples de bot Framework v3|
| [Exemple de bot pour Node.js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Exemples de bot Framework v3 |
