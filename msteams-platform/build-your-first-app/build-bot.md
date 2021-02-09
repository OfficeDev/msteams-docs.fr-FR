---
title: Get started - Build a bot
author: heath-hamilton
description: Créez rapidement un bot Microsoft Teams à l’aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 3e07c148e1b03431dc419a4e3679abac0229ff72
ms.sourcegitcommit: e08f309f62db2cf0f505f2aadfe728e5b46c17a5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/08/2021
ms.locfileid: "50140467"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Créer un bot pour Microsoft Teams

Vous allez créer une application *de bot* de base dans ce didacticiel. Un bot fait office d’intermédiaire entre les utilisateurs de Teams et votre service web. Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.

## <a name="your-assignment"></a>Votre affectation

Votre espace de travail a créé une application Teams qui utilise [des onglets](../build-your-first-app/build-personal-tab.md) pour mettre en avant des informations de contact importantes. Par exemple, les collègues ont un accès rapide au numéro de téléphone du service d’aide. Mais au lieu d’appeler, que se passe-t-il si des personnes peuvent contacter le service d’aide à l’aide d’un chatbot ? Votre responsable vous demande de voir à quelle vitesse vous pouvez obtenir un bot de conversation de base opérationnel dans Teams.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application et un bot à l’aide de microsoft Teams Shared Computer Toolkit pour Visual Studio code
> * Identifier certaines configurations d’application et la échafaudage pertinentes pour les bots
> * Héberger une application localement
> * Configurer un bot pour Teams
> * Chargement de version test et test d’un bot dans Teams

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l’avez pas encore fait, assurez-vous que vous comprenez et installez les [conditions préalables de développement teams.](build-first-app-overview.md#get-prerequisites)

## <a name="1-create-your-app-project"></a>1. Créer votre projet d’application

La Shared Computer Toolkit Microsoft Teams vous aide à configurer les composants suivants pour votre application :

* **Configurations d’application et échafaudage pertinents** pour les bots
* **Bot** inscrit automatiquement auprès du service de bot Microsoft Azure

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut vous être utile de suivre ces [instructions](../build-your-first-app/build-and-run.md) qui expliquent les projets plus en détail.

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.
1. Dans **l’écran Ajouter des fonctionnalités,** **sélectionnez Bot,** puis **Suivant.**
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.)
1. Go to **Configure bot** and select **Create a new Bot** then Create Bot **Registration**. Si elle réussit, votre nouveau bot aura un **état** inscrit.
1. Sélectionnez **Terminer** en bas de l’écran et choisissez un emplacement pour créer votre projet.

## <a name="2-identify-relevant-app-project-components"></a>2. Identifier les composants de projet d’application pertinents

La plupart des configurations d’application et de la création de la Shared Computer Toolkit sont automatiquement définies lorsque vous créez votre projet. Examinons les principaux composants de la création d’un bot.

### <a name="app-configurations"></a>Configurations d’application

Pour afficher ou mettre à jour les configurations de votre bot, sélectionnez **App Studio** dans le kit de ressources et allez à **Bots**.

### <a name="app-scaffolding"></a>Échafaudage d’application

La création de modèles d’application fournit un fichier, situé dans le répertoire racine de votre projet, pour gérer la façon dont votre bot traite les activités dans Teams (par exemple, la façon dont le bot répond à des messages spécifiques tels que « `botActivityHandler.js` Hello »).

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre application sur un serveur web local (port 3978).

1. Si ce n’est pas déjà fait, installez [ngrok](https://ngrok.com/download).
1. Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .
1. Copiez l’URL HTTPS dans la sortie (par exemple), car `https://468b9ab725e9.ngrok.io` Teams requiert des connexions HTTPS.

Avec cette URL, Teams (qui nécessite des connexions HTTPS) pourra tunneler vers l’endroit où vous hébergez votre application ( `localhost` sur le port 3978).

## <a name="4-configure-your-bot"></a>4. Configurer votre bot

Pour utiliser un bot dans Teams, vous devez l’inscrire auprès d’Azure Bot Service. Pour vous, cela s’effectue automatiquement lorsque vous définissez votre application à l’aide de la Shared Computer Toolkit Teams.

Vous devez toujours spécifier une adresse de point de terminaison pour recevoir et traiter les messages utilisateur (c’est-à-dire, les demandes) envoyés au bot. En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à . Vous pouvez configurer cette configuration rapidement dans le kit de ressources.

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Shared Computer Toolkit**.
1. Go to **Bots > Existing bot registrations** and select the bot you created during setup.
1. Dans le **champ d’adresse** du point de terminaison bot, entrez l’URL ngrok (par exemple, ) où vous hébergez le bot et y `https://468b9ab725e9.ngrok.io` `/api/messages` appendez-le.<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Illustration montrant où vous pouvez configurer l’URL du point de terminaison du bot dans la Shared Computer Toolkit Teams.":::

Votre bot pourra répondre aux messages dans Teams.

## <a name="5-build-and-run-your-app"></a>5. Créer et exécuter votre application

Vous avez configuré une URL pour héberger votre bot et configurée pour gérer les messages. Il est temps de rendre votre application opérationnel.

1. Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécutez `npm start` .

Si l’opération réussit, vous voyez le message suivant indiquant que votre bot est à l’écoute de l’activité sur votre `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Chargement d’une version de version de votre bot dans Teams

Une fois votre bot en cours d’exécution, vous pouvez l’installer dans Teams.

> [!TIP]
> Si vous n’avez pas encore chargé une application Teams et que vous avez des problèmes, suivez ces [instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. Dans Visual Studio Code, appuyez sur la **touche F5** pour lancer un client web Teams.
1. Dans la boîte de dialogue d’installation de l’application, **sélectionnez Ajouter pour moi.** (Vous pouvez ajouter le bot à un canal ou une conversation, mais il est moins intrusif pour d’autres personnes de tester un bot dans une conversation un-à-un.)

## <a name="7-test-your-bot"></a>7. Testez votre bot

Maintenant, nous allons dire « Hello » à votre bot.

1. Dans la zone de composition, envoyez un `Hello` message.

Votre bot répond par un message du même genre que celui-ci.

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Capture d’écran montrant un utilisateur dire « Hello » à un bot Teams et obtenir une réponse.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous avez un bot Teams de base qui peut communiquer avec les utilisateurs un-à-un ou dans les paramètres de groupe (canaux et conversations).

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous aider si vous avez des problèmes lors de la réalisation de ce didacticiel.

### <a name="bot-isnt-connected-to-teams"></a>Le bot n’est pas connecté à Teams

Si vous avez installé votre application, mais que le bot ne fonctionne pas, assurez-vous que le bot est connecté au canal [Teams d’Azure Bot Service.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Il est important de comprendre que ce n’est pas le même qu’un canal dans Teams. Dans ce cas, un canal est la façon dont azure Bot Service connecte votre bot à Teams ou à une autre application de communication microsoft ou [tierce prise en charge.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="learn-more"></a>En savoir plus

* [Voir les autres choses que les bots Teams peuvent faire avec l’un de nos exemples](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Concepts de base d’une conversation de bot](../bots/how-to/conversations/conversation-basics.md)
* Suivez nos [instructions de conception](../bots/design/bots.md) et créez avec des [modèles d’interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) prêts pour la production pour créer une expérience transparente.
* [Authentification de bot dans Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [Créer un bot sans le kit de ressources](../resources/bot-v3/bots-create.md)
