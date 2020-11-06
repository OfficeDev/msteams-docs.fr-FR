---
title: Prise en main-créer un bot
author: heath-hamilton
description: Créez rapidement un robot Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931737"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Créer un robot pour Microsoft teams

Vous allez créer une application *bot* de base dans ce didacticiel. Un bot agit comme un intermédiaire entre les utilisateurs de teams et votre service Web. Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.

## <a name="your-assignment"></a>Votre affectation

Votre espace de travail a créé une application teams qui utilise des [onglets](../build-your-first-app/build-personal-tab.md) pour exposer les informations de contact importantes. Par exemple, les collègues ont un accès rapide au numéro de téléphone du support technique. Mais au lieu d’appeler, que se passe-t-il si des personnes peuvent contacter le support technique à l’aide d’un chatbot ? Votre patron vous demande de consulter la rapidité avec laquelle vous pouvez faire fonctionner un robot de conversation de base dans Teams.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application et un bot à l’aide de Microsoft teams Toolkit pour Visual Studio code
> * Identifier certaines configurations d’application et la génération de modèles automatique propres aux robots
> * Héberger une application localement
> * Configurer un bot pour teams
> * Chargement et tester un bot dans teams

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).

## <a name="1-create-your-app-project"></a>1. créer votre projet d’application

La boîte à outils Microsoft teams vous permet de configurer les composants suivants pour votre application :

* **Configurations d’application et génération** d’une structure adaptée aux robots
* **Robot** enregistré automatiquement avec le service Microsoft Azure bot

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **bot** puis **suivant**.
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Accédez à **configurer bot** et sélectionnez **créer un nouveau robot** , puis **inscrire un bot**. Si elle réussit, votre nouveau Bot aura un statut **enregistré** .
1. Sélectionnez **Terminer** en bas de l’écran et choisissez un emplacement pour créer votre projet.

## <a name="2-identify-relevant-app-project-components"></a>2. identifier les composants de projet d’application pertinents

La plupart des configurations et des modèles d’application sont configurés automatiquement lorsque vous créez votre projet à l’aide de Team Toolkit. Examinons les principaux composants de la création d’un bot.

### <a name="app-configurations"></a>Configurations d’application

Pour afficher ou mettre à jour les configurations de votre bot, sélectionnez **app Studio** dans la boîte à outils et accédez à **robots**.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

La génération de modèles automatique d’application fournit un `botActivityHandler.js` fichier, situé dans le répertoire racine de votre projet, pour la gestion de la manière dont votre bot traite les activités dans Teams (par exemple, la façon dont le bot répond à des messages spécifiques, tels que « Hello »).

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre application sur un serveur Web local (port 3978).

1. Si vous ne l’avez pas encore fait, installez [ngrok](https://ngrok.com/download).
1. Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .
1. Copiez l’URL HTTPs dans la sortie (par exemple, `https://468b9ab725e9.ngrok.io` ) puisque teams requiert des connexions HTTPS.

Avec cette URL, Teams (qui requiert des connexions HTTPs) peut être utilisé pour effectuer un tunnel vers l’endroit où vous hébergez votre application ( `localhost` sur le port 3978).

## <a name="4-configure-your-bot"></a>4. configurer votre robot

Pour utiliser un bot dans Teams, vous devez l’enregistrer auprès du service Microsoft Azure bot. Heureusement, cette opération est exécutée automatiquement lorsque vous configurez votre application à l’aide de Team Toolkit.

Vous devez toujours spécifier une adresse de point de terminaison pour recevoir et traiter les messages utilisateur (par exemple, les demandes) envoyées au bot. En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` : Vous pouvez le configurer rapidement dans la boîte à outils.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. Accédez à **robots > inscriptions de robots existantes** et sélectionnez le robot que vous avez créé lors de l’installation.
1. Dans le champ **adresse du point de terminaison de robot** , entrez l’URL ngrok (par exemple, `https://468b9ab725e9.ngrok.io` ) où vous hébergez le bot et ajoutez `/api/messages` -y.<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Illustration illustrant l’emplacement où vous pouvez configurer l’URL du point de terminaison du bot dans Team Toolkit.":::

Votre robot pourra répondre aux messages dans Teams.

## <a name="5-build-and-run-your-app"></a>5. générez et exécutez votre application

Vous avez configuré une URL pour héberger votre robot et le configurer pour qu’il gère les messages. Il est temps de faire fonctionner votre application.

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` .

Si elle réussit, vous voyez le message suivant indiquant que votre robot est à l’écoute des activités sur le `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. chargement de votre robot dans teams

Une fois que votre robot est en cours d’exécution, vous pouvez l’installer dans Teams.

> [!TIP]
> Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).

1. Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.
1. Dans la boîte de dialogue d’installation de l’application, sélectionnez **Ajouter pour moi**. (Vous pouvez ajouter le bot à un canal ou une conversation, mais il est moins gênant pour les autres personnes de tester un bot dans une conversation en un seul.)

## <a name="7-test-your-bot"></a>7. tester votre robot

Maintenant pour la partie amusante : disons « Hello » à votre bot.

1. Dans la zone de composition, envoyez un `Hello` message.

Votre robot répond avec un message semblable à celui-ci.

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Capture d’écran illustrant un utilisateur dire « Hello » à un bot de teams et obtenant une réponse.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’un bot de teams de base qui peut communiquer avec des utilisateurs un-sur-un ou des paramètres de groupe (canaux et conversations).

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.

### <a name="bot-isnt-connected-to-teams"></a>Le bot n’est pas connecté à teams

Si vous avez installé votre application, mais que le bot ne fonctionne pas, vérifiez que le bot est [connecté au *canal* teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams. Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>En savoir plus

* [Voir les autres robots que les robots peuvent faire avec l’un de nos exemples](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Concepts de base d’une conversation de bot](../bots/how-to/conversations/conversation-basics.md)
* [Authentification de robot dans teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
* [Créer un bot sans la boîte à outils](../bots/how-to/create-a-bot-for-teams.md)
