---
title: Exemples de code d’application
description: Liens et descriptions d’exemples d’applications pour la plateforme de développement Microsoft Teams
ms.topic: reference
keywords: Exemples de développement Microsoft Teams
ms.openlocfilehash: f51ffb22a5e6b3b757d1971422adf955d95fb223
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014109"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Didacticiels et exemples de code pour la plateforme de développement Microsoft Teams

Vous y trouverez une liste de didacticiels et d’exemples de code qui montrent comment étendre les fonctionnalités de la plateforme de développement Teams en créant des applications personnalisées.

## <a name="getting-started-with-microsoft-learn"></a>Mise en place de Microsoft Learn

| Fonctionnalité| Module Learn|
|--------|-------------|
| Onglets : expériences web incorporées  |  [Créez des expériences web incorporées avec les onglets pour Microsoft Teams](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Webhooks et connecteurs  |  [Connecter des services web à Microsoft Teams à l’aide de webhooks et de connecteurs Office 365](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|Extensions de messagerie  | [Interactions orientées sur des tâches dans Microsoft Teams avec les extensions de messagerie](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| Modules de tâche |  [Collecter des entrées dans Microsoft Teams à l’aide de modules de tâche](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| Bots conversationnels  | [Créer des bots conversationnels interactifs pour Microsoft Teams](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>Prise en route des exemples de code

Pour télécharger nos exemples à partir de GitHub :

1. Sélectionnez l’un des projets répertoriés ci-dessous et ouvrez le projet dans GitHub.
2. Choisissez le **bouton Cloner ou télécharger** et copiez l’URL
3. Ouvrez une invite de commandes dans le répertoire parent dans lequel vous souhaitez installer l’exemple de projet
4. Exécuter `git clone <pasted url>`

### <a name="for-netc-samples"></a>Pour les exemples .NET/C#

Chacun de nos exemples .NET inclut un fichier Visual Studio solution qui peut créer la solution entièrement, y compris la restauration des packages NuGet.

### <a name="for-nodejs-samples"></a>Pour obtenir Node.js exemples

Nous fournissons une packages.jsfichier qui répertorie tous les packages requis pour un exemple. Exécutez simplement à partir de la ligne de commande `npm install` de votre Node.js de projet pour installer les packages requis. Vous êtes maintenant prêt à ouvrir le projet dans Visual Studio Code et commencer à expérimenter.

### <a name="for-other-samples"></a>Pour d’autres exemples

Comme toujours, le fichier README du projet doit avoir plus d’informations sur les besoins spécifiques d’exemples spécifiques.

## <a name="bots-using-the-v4-sdk"></a>Bots (à l’aide du SDK v4)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>Visitez le référentiel [Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples) pour afficher les exemples du SDK Microsoft Bot Framework v4 pour C#, JavaScript, TypeScript et Python.

## <a name="messaging-extensions-using-the-v4-sdk"></a>Extensions de messagerie (à l’aide du SDK v4)

| Exemple | Description | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| Extensions de messagerie : recherche | Extension de messagerie qui accepte les demandes de recherche et renvoie des résultats. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
| Extensions de messagerie : action | Extension de messagerie qui accepte les paramètres et renvoie une carte. En outre, comment recevoir un message transmis en tant que paramètre dans une extension de messagerie. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extensions de messagerie : th et config | Extension de messagerie qui possède une page de configuration, accepte les demandes de recherche et renvoie des résultats une fois que l’utilisateur s’est inscrit. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) |
| Extensions de messagerie : aperçu de l’action | Montre comment créer un flux d’aperçu et de modification pour une extension de messagerie. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/53.teams-messaging-extensions-action-preview) |
| Déploiement de lien | Extension de messagerie qui effectue le déploiement de lien. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/55.teams-link-unfurling) |


## <a name="outgoing-webhooks"></a>Webhooks sortants

| Exemple | Description
|--------|-------------
| [Webhook sortant pour C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | Illustre comment créer un **webhook** sortant pour Microsoft Teams en C#/.NET.
| [Webhook sortant pour Node.js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Illustre comment créer un **webhook** sortant simple pour Microsoft Teams en ~50 lignes de code Node.js.

## <a name="connectors"></a>Connecteurs

| Exemple | Description
|--------|-------------
| [Exemple de connecteur pour Node.js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | Cet exemple, écrit en Node.js, explique comment créer un connecteur pour Microsoft Teams à l’aide de GitHub comme exemple pour générer des notifications de connecteur.
| [Exemple de connecteur pour C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | Cet exemple, écrit en C#, montre comment créer un connecteur pour Microsoft Teams à l’aide d’un exemple d’application de liste de tâches comme exemple pour générer des notifications de connecteur. Cet exemple montre également comment implémenter la fonctionnalité de connexion dans la page de configuration du connecteur. 

## <a name="graph-api"></a>Graph API

| Exemple | Description
|--------|-------------
| [Exemples d’API Microsoft Graph](https://github.com/OfficeDev/microsoft-teams-sample-graph) | Ces exemples illustrent l’utilisation d’appels d’API Microsoft Graph pour effectuer des tâches telles que l’interrogation d’équipes et de canaux à partir d’un service web exécuté en dehors de Microsoft Teams.

### <a name="bot-framework-sdk-v3-samples"></a>Exemples du SDK Bot Framework v3

| Exemple | Description |
|--------|------------- |
| [Exemple de bot pour C#/.NET](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Exemples de Bot Framework v3|
| [Exemple de bot pour Node.js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Exemples de Bot Framework v3 |
