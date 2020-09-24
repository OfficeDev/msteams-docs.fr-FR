---
title: Exemples de code Microsoft teams
description: Liens et descriptions des exemples d’applications pour la plateforme de développement Microsoft teams
keywords: Exemples de développeurs Microsoft teams
ms.openlocfilehash: 7a81494d7808c27c495c660b5d58f7779ba87c83
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237957"
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
4. Générer `git clone <pasted url>`

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
| Extensions de messagerie-recherche | Extension de messagerie qui accepte les demandes de recherche et renvoie les résultats. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
| Extensions de messagerie-action | Extension de messagerie qui accepte des paramètres et renvoie une carte. De plus, la procédure de réception d’un message transféré en tant que paramètre dans une extension de messagerie. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extensions de messagerie : auth et config | Extension de messagerie ayant une page de configuration, accepte les demandes de recherche et renvoie les résultats une fois que l’utilisateur s’est connecté. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) |
| Extensions de messagerie-aperçu de l’action | Montre comment créer un flux d’aperçu et de modification pour une extension de messagerie. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/53.teams-messaging-extensions-action-preview) |
| Déploiement de lien | Extension de messagerie qui effectue la liaison unfurling. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/55.teams-link-unfurling) |


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
