---
title: Démarrer - Construire un bot
author: girliemac
description: Créez rapidement un bot Microsoft Teams en utilisant le Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: 2cbd90b293e8ac8343febc7b3d23278d5bb5bf82
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565885"
---
# <a name="create-your-first-bot-for-teams"></a>Créez votre premier bot pour Teams

Ce tutoriel vous apprend à construire une application de bot de base. Un bot agit comme un intermédiaire entre Teams utilisateurs et votre application web ou service avec une interface conversationnelle. Les gens peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des workflows et des tâches effectuées par votre service.

## <a name="what-youll-learn"></a>Ce que vous apprendrez

* Créez un projet d’application et un bot en utilisant Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.
* Comprendre les configurations Teams’applications pertinentes pour les bots.
* Hébergez et exécutez une application localement à l’aide d’une solution de tunneling localhost.
* Sideload et tester un bot dans Teams.

## <a name="prerequisites"></a>Configuration requise

Assurez-vous de bien comprendre comment configurer et construire une application Teams simple. Pour plus d’informations, [consultez la première Microsoft Teams application « Hello, World! »](../build-your-first-app/build-and-run.md). 

## <a name="1-create-your-app-project"></a>1. Créez votre projet d’application

Le Microsoft Teams Shared Computer Toolkit vous aide à configurer les composants suivants pour votre application : 

* **Configurations d’applications et échafaudages** pertinents pour les bots.
* **Bot** qui est automatiquement enregistré auprès du Microsoft Azure Bot Service.

**Pour créer votre projet d’application**

1. Dans Visual Studio Code, sélectionnez **Microsoft Teams la** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: barre d’activité gauche et **choisissez Créer une nouvelle application Teams.**

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Capture d’écran montrant comment créer une application dans le Teams Shared Computer Toolkit.":::

1. Lorsque cela est demandé, connectez-vous à votre compte Microsoft 365 développement de votre entreprise. 
1. Sur l’écran du projet Select, sélectionnez Robots conversation : 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Capture d’écran montrant comment créer un nouveau bot dans le Teams Shared Computer Toolkit.":::

1. Sur **l’écran du** projet Configure, entrez un nom pour votre bot. Il s’agit du nom par défaut de votre application et aussi du nom de l’annuaire du projet d’application sur votre machine locale.
1. Sélectionnez **Créer un nouveau Bot** Créer  >  **l’enregistrement bot** comme indiqué dans l’image suivante:

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Capture d’écran montrant nommer un nouveau bot dans Teams Shared Computer Toolkit.":::

    En cas de succès, votre nouveau bot aura un **statut** enregistré. Maintenant, votre bot est automatiquement enregistré auprès du Microsoft Azure Bot Service. 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Capture d’écran montrant l’enregistrement du nouveau bot dans Teams Shared Computer Toolkit.":::

1. Sélectionnez **Finition** en bas de l’écran et enregistrez votre projet sur votre machine.  

## <a name="2-understand-your-app-project-components"></a>2. Comprendre les composants de votre projet d’application

Une grande partie des configurations d’applications et des échafaudages sont mis en place automatiquement lorsque vous créez votre projet avec Teams Shared Computer Toolkit. Examinons les principaux composants pour la construction d’un bot:

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Capture d’écran montrant un échafaudage de projet dans Teams Shared Computer Toolkit.":::

Si vous avez créé un onglet dans un autre tutoriel, l’échafaudage de l’application pour le bot est différent. Contrairement aux onglets, le développement de bots ne vous oblige pas à construire des composants Web front-end ou à utiliser les Teams client JavaScript SDK.  Au lieu de cela, [l’échafaudage utilise le Microsoft Bot Framework](https://dev.botframework.com/), qui est un SDK open-source pour la construction intelligente, bots de qualité entreprise qui peuvent travailler sur le web, mobile, et bien sûr Teams! 

Le `botActivityHandler.js` fichier, situé dans l’annuaire racine de votre projet, est le gestionnaire spécifique à Teams qui gère les activités de bot, telles que la façon dont le bot répond à des messages spécifiques. L’échafaudage de `botActivityHandler.js` l’application fournit un fichier situé dans l’annuaire racine de votre projet, est le gestionnaire spécifique Teams qui gère les activités bot telles que la façon dont le bot répond à des messages spécifiques.

## <a name="3-securely-expose-your-localhost-to-the-internet"></a>3. Exposez en toute sécurité votre heure locale à Internet

Jetez un oeil au `index.js` fichier, qui crée un serveur HTTP et gère le routage pour écouter les demandes entrantes à votre bot. `/api/messages`L’URL du point de terminaison de votre application est la réponse aux demandes des clients : 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

Pour transmettre les demandes à la logique de votre bot, vous devez configurer une URL accessible au public, par `https://example.com/api/messages` exemple, au lieu de `https://localhost` . Étant donné que votre application est en cours d’exécution à partir de votre localhost actuellement, vous *devez tunnel* le réseau.

Tunneling est un protocole qui vous permet de transporter des données sur un réseau. Et le tunnelage local vous donne une connexion entre votre machine locale et une connexion distante. Pour exposer en toute sécurité votre localhost à l’Internet, nous vous recommandons d’utiliser l’outil tiers appelé, **ngrok**. Cela vous donnera une URL sécurisée. 

1. Rendez-vous [sur ngrok.com](https://ngrok.com/download) site et suivez les instructions d’installation et de mise en place de ngrok dans votre environnement. 
    
    Ajoutez le chemin complet au fichier ngrok.exe que vous avez installé à la variable environnement PATH du système. Les étapes exactes sont spécifiques à la coquille que vous utilisez.

1.  Une fois que vous avez terminé sa mise en place, ouvrez un terminal et `ngrok http -host-header=rewrite 3978` exécutez. 

    Maintenant ngrok vous fournit une URL publique et sécurisée qui est transmise à votre localhost au port 3978, alors copiez l’URL HTTPS, par exemple, comme le montre la `https://287a4f4223bc.ngrok.io` capture d’écran ci-dessous, puisque Teams nécessite des connexions HTTPS : 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Capture d’écran montrant tunnelling de localhost avec ngrok.":::

1. Enregistrez l’URL dans le manifeste de votre application. 

## <a name="4-register-your-bot-endpoint"></a>4. Enregistrez votre point de terminaison bot

Pour utiliser un bot dans Teams, vous devez l’enregistrer auprès du Service Bot Azure. Cela se fait automatiquement lorsque vous configurez votre application à l’aide de la Teams Shared Computer Toolkit.

Vous devez toujours spécifier une adresse de point de terminaison pour recevoir et traiter les messages utilisateur, ou les demandes envoyées au bot. En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à . Vous pouvez configurer cela dans la boîte à outils.

1. En Visual Studio Code, ouvrez **Microsoft Teams Shared Computer Toolkit**.
1. Sélectionnez **bots**  >  **enregistrements bot existants et** sélectionnez le bot que vous avez créé lors de la configuration. 
1. Dans le **champ d’adresse bot,** entrez l’URL ngrok, par `https://287a4f4223bc.ngrok.io` exemple, où vous hébergez le bot et `/api/messages` annexez-le :

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Capture d’écran montrant comment tunnel localhost avec ngrok.":::

    Votre bot sera en mesure de répondre aux messages dans Teams, après avoir correctement défini le point de terminaison. 

## <a name="5-build-and-run-your-app"></a>5. Créez et exécutez votre application

Vous avez configuré une URL pour héberger votre bot et l’avez configurée pour gérer les messages. Il est temps de mettre votre application en marche.

1. Dans un terminal, allez à l’annuaire racine de votre projet d’application et `npm install` exécutez.
1. Exécutez `npm start`.

   En cas de succès, vous voyez le message suivant indiquant que votre bot est à l’écoute de l’activité à votre `localhost` :

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Chargez votre bot dans Teams

Avec votre bot en cours d’exécution, vous pouvez l’installer Teams.

> [!TIP]
> Si vous n’avez pas déchargé une application Teams avant et que vous ne vous êtes pas aperçu de problèmes, suivez [ces instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. Dans Visual Studio Code, sélectionnez **la clé F5** pour lancer un client web Teams et spécial.
1. Dans le dialogue d’installation de l’application, **sélectionnez Ajouter pour moi**. 

   > [!Note]
   > Par défaut, l’application est ajoutée à votre message de chat direct 1:1, mais vous pouvez choisir de l’installer à une équipe ou de discuter en cliquant sur la petite flèche **à côté ajouter pour moi**. Dans ce tutoriel, il suffit de cliquer sur Ajouter.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Capture d’écran montrant tunnelling localhost avec ngrok.":::

## <a name="7-test-your-bot"></a>7. Testez votre bot

Disons « Bonjour » à votre bot.

* Dans la boîte de composition, envoyez un `Hello` message.
    Votre bot répond par quelque chose comme le message suivant:

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Une capture d’écran montrant un utilisateur dire « Bonjour » à un bot Teams et obtenir une réponse.":::

    Vous avez maintenant créé un bot de Teams de base qui peut communiquer avec les utilisateurs en tête-à-tête ou en groupe (canaux et chats) 🎉.

## <a name="troubleshoot-your-bot"></a>Dépanner votre bot

Les informations suivantes peuvent vous aider si vous avez eu des problèmes pour terminer ce tutoriel.

### <a name="bot-isnt-connected-to-teams"></a>Bot n’est pas connecté à Teams


Si vous avez installé votre application mais que le bot ne fonctionne pas, assurez-vous que le bot [est connecté au canal de Teams Azure Bot Service. ](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Il est important de comprendre que ce n’est pas la même chose qu’un canal dans Teams. Dans ce cas, un canal est la façon dont le Service Bot Azure connecte votre bot à Teams ou une autre application de [communication Microsoft ou tierce prise en charge](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="see-also"></a>Voir aussi

* [Bases bot](../bots/bot-basics.md)
* [Créez un onglet personnel pour Microsoft Teams](../build-your-first-app/build-personal-tab.md)
* [Voyez ce que Teams bots peuvent faire avec un de nos échantillons](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Concepts de base d’une conversation de bot](../bots/how-to/conversations/conversation-basics.md)
* [Instructions de conception](../bots/design/bots.md) 
* [Modèles d’interface utilisateur prêts à la production](../concepts/design/design-teams-app-ui-templates.md)
* [Authentification bot dans Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [Créer un bot sans la boîte à outils](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une extension de messagerie](../build-your-first-app/build-messaging-extension.md)
