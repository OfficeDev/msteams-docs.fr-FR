---
title: Get started - Build a bot
author: girliemac
description: Créez rapidement un bot Microsoft Teams à l’aide du Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: d54766d739ceaf585ab4a1e026f4a6e1150e3a2e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630977"
---
# <a name="create-your-first-bot-for-teams"></a>Créez votre premier bot pour Teams

Ce didacticiel vous apprend à créer une application de bot de base. Un bot fait office d’intermédiaire entre Teams utilisateurs et votre application web ou service avec une interface de conversation. Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

* Créez un projet d’application et un bot à l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.
* Comprendre les configurations Teams d’application pertinentes pour les bots.
* Hébergez et exécutez une application localement à l’aide d’une solution de tunnel localhost.
* Chargez une version test d’un bot dans Teams.

## <a name="prerequisites"></a>Configuration requise

Assurez-vous que vous comprenez comment configurer et créer une application Teams simple. Pour plus d’informations, [voir créer votre première Microsoft Teams application « Hello World!](../build-your-first-app/build-and-run.md)». 

## <a name="1-create-your-app-project"></a>1. Créer votre projet d’application

Le Microsoft Teams Shared Computer Toolkit vous aide à configurer les composants suivants pour votre application : 

* **Configurations d’application et échafaudage pertinents** pour les bots.
* **Bot** inscrit automatiquement auprès du service Microsoft Azure Bot.

**Pour créer votre projet d’application**

1. In Visual Studio Code, select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Create a new **Teams app**.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Capture d’écran montrant comment créer une application dans le Teams Shared Computer Toolkit.":::

1. Lorsque vous y invitez, connectez-vous avec votre Microsoft 365 de développement. 
1. Dans l’écran Sélectionner un projet, sélectionnez Bots de conversation : 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Capture d’écran montrant comment créer un bot dans le Teams Shared Computer Toolkit.":::

1. Dans **l’écran Configurer le projet,** entrez un nom pour votre bot. Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.
1. Sélectionnez **Créer un bot d’inscription**  >  **de bot,** comme illustré dans l’image suivante :

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Capture d’écran montrant l’attribution d’un nom à un nouveau bot dans Teams Shared Computer Toolkit.":::

    Si elle réussit, votre nouveau bot aura **l’état** Inscrit. Votre bot est désormais inscrit automatiquement auprès du service Microsoft Azure Bot. 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Capture d’écran montrant l’inscription d’un nouveau bot dans Teams Shared Computer Toolkit.":::

1. Sélectionnez **Terminer** en bas de l’écran et enregistrez votre projet sur votre ordinateur.  

## <a name="2-understand-your-app-project-components"></a>2. Comprendre les composants de votre projet d’application

La plupart des configurations d’application et de la création de la Teams Shared Computer Toolkit sont automatiquement définies. Examinons les principaux composants de la création d’un bot :

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Capture d’écran montrant la échafaudage d’un projet dans la Teams Shared Computer Toolkit.":::

Si vous avez créé un onglet dans un autre didacticiel, la création de la modèle d’application pour le bot est différente. Contrairement aux onglets, le développement de bots ne nécessite pas la création de composants web frontaux ou l’utilisation Teams SDK client JavaScript.  Au lieu de cela, la création de la forme utilise la [Microsoft Bot Framework](https://dev.botframework.com/), qui est un SDK open source pour créer des bots intelligents et de niveau entreprise qui peuvent fonctionner sur le web, mobile et bien sûr Teams! 

La création de la échafaudage d’application fournit un fichier, situé dans le répertoire racine de votre projet, qui est le handler spécifique à Teams qui gère les activités du bot, telles que la façon dont le bot répond à des `botActivityHandler.js` messages spécifiques.

## <a name="3-securely-expose-your-localhost-to-the-internet"></a>3. Exposer en toute sécurité votre localhost sur Internet

Consultez le fichier, qui crée un serveur HTTP et gère le routage pour écouter les demandes entrantes `index.js` à votre bot. Url du point de terminaison de votre application `/api/messages` pour répondre aux demandes des clients : 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

Pour que les demandes soient transmis à la logique de votre bot, vous devez configurer une URL accessible publiquement, par exemple, au `https://example.com/api/messages` lieu de `https://localhost` . Étant donné que votre application s’exécute à partir de votre localhost actuellement, vous devez *tunneler* le réseau.

Le tunneling est un protocole qui vous permet de transporter des données sur un réseau. La tunneling localhost vous permet d’établir une connexion entre votre ordinateur local et une connexion distante. Pour exposer en toute sécurité votre localhost sur Internet, nous vous recommandons d’utiliser l’outil tiers appelé **ngrok**. Cela vous donne une URL sécurisée. 

1. Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment. 
    
    Ajoutez le chemin d’accès complet au ngrok.exe que vous avez installé à la variable d’environnement PATH système. Les étapes exactes sont spécifiques à l’shell que vous utilisez.

1.  Une fois la configuration terminée, ouvrez un terminal et `ngrok http -host-header=rewrite 3978` exécutez. 

    Maintenant que ngrok vous fournit une URL publique et sécurisée qui est transmis à votre localhost au port 3978, copiez l’URL HTTPS, par exemple, comme illustré dans la capture d’écran ci-dessous, dans la mesure où Teams nécessite des `https://287a4f4223bc.ngrok.io` connexions HTTPS : 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Screenshot showing tunnelling of localhost with ngrok.":::

1. Inscrivez l’URL dans le manifeste de votre application. 

## <a name="4-register-your-bot-endpoint"></a>4. Inscrire le point de terminaison de votre bot

Pour utiliser un bot dans Teams, vous devez l’inscrire auprès d’Azure Bot Service. Cette mise à jour est effectuée automatiquement lorsque vous définissez votre application à l’aide du Teams Shared Computer Toolkit.

Vous devez toujours spécifier une adresse de point de terminaison pour recevoir et traiter les messages des utilisateurs, ou les demandes envoyées au bot. En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à . Vous pouvez le configurer dans le kit de ressources.

1. Dans Visual Studio Code, ouvrez **Microsoft Teams Shared Computer Toolkit**.
1. Sélectionnez **Bots**  >  **Existing bot registrations** and select the bot you created during setup. 
1. Dans le **champ d’adresse** du point de terminaison bot, entrez l’URL ngrok, par exemple, où vous hébergez le bot et y `https://287a4f4223bc.ngrok.io` `/api/messages` appendez :

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Capture d’écran montrant comment tunneler localhost avec ngrok.":::

    Votre bot peut répondre aux messages dans Teams, une fois que vous avez correctement installé le point de terminaison. 

## <a name="5-build-and-run-your-app"></a>5. Créer et exécuter votre application

Vous avez configuré une URL pour héberger votre bot et configurée pour gérer les messages. Il est temps de rendre votre application opérationnel.

1. Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécutez `npm start`.

   Si l’opération réussit, vous voyez le message suivant indiquant que votre bot est à l’écoute de l’activité au niveau de votre `localhost` :

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Chargement d’une version de version de votre bot dans Teams

Une fois votre bot en cours d’exécution, vous pouvez l’installer dans Teams.

> [!TIP]
> Si vous n’avez pas chargé une version de version Teams’application avant et que vous avez des problèmes, suivez ces [instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. Dans Visual Studio Code, sélectionnez la **touche F5** pour lancer un client Teams web.
1. Dans la boîte de dialogue d’installation de l’application, **sélectionnez Ajouter pour moi.** 

   > [!Note]
   > Par défaut, l’application est ajoutée à votre message de conversation directe 1:1, mais vous pouvez choisir de l’installer dans une équipe ou une conversation en cliquant sur la petite flèche à côté d’Ajouter pour **moi.** Dans ce didacticiel, nous allons simplement cliquer sur Ajouter.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Capture d’écran montrant le tunnelage localhost avec ngrok.":::

## <a name="7-test-your-bot"></a>7. Testez votre bot

Dites « Hello » à votre bot.

* Dans la zone de composition, envoyez un `Hello` message.
    Votre bot répond par le message suivant :

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Capture d’écran montrant un utilisateur dire « Hello » à un bot Teams et obtenir une réponse.":::

    Vous avez maintenant créé un bot Teams de base qui peut communiquer avec les utilisateurs un-à-un ou dans des paramètres de groupe (canaux et conversations) 🎉.

## <a name="troubleshoot-your-bot"></a>Résoudre les problèmes de votre bot

Les informations suivantes peuvent vous aider si vous avez des problèmes lors de la réalisation de ce didacticiel.

### <a name="bot-isnt-connected-to-teams"></a>Le bot n’est pas connecté à Teams


Si vous avez installé votre application, mais que le bot ne fonctionne pas, assurez-vous que le bot est connecté au canal Teams [ *Azure* Bot Service.](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Il est important de comprendre que ce n’est pas le même qu’un canal dans Teams. Dans ce cas, un canal est la façon dont azure Bot Service connecte votre bot à Teams ou à une autre application de communication Microsoft ou tierce [prise en charge.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="see-also"></a>Voir aussi

* [Informations de base sur les bots](../bots/bot-basics.md)
* [Créer un onglet personnel pour Microsoft Teams](../build-your-first-app/build-personal-tab.md)
* [Découvrez les autres Teams bots peuvent faire avec l’un de nos exemples](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Concepts de base d’une conversation de bot](../bots/how-to/conversations/conversation-basics.md)
* [Instructions de conception](../bots/design/bots.md) 
* [Modèles d’interface utilisateur prêts pour la production](../concepts/design/design-teams-app-ui-templates.md)
* [Authentification de bot dans Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [Créer un bot sans le kit de ressources](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une extension de messagerie](../build-your-first-app/build-messaging-extension.md)
