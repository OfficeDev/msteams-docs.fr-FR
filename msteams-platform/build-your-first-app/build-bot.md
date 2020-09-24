---
title: Créer un bot teams
author: heath-hamilton
description: Découvrez comment créer un bot pour votre première application Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: cc004bd0d86eca1e4e63c2a96a72f9c11d2269db
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237824"
---
# <a name="build-a-teams-bot"></a>Créer un bot teams

Vous allez créer une application *bot* de base dans ce didacticiel. Un bot agit comme un intermédiaire entre les utilisateurs de teams et votre service Web. Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.

## <a name="your-assignment"></a>Votre affectation

Votre espace de travail a utilisé des [onglets](../build-your-first-app/build-personal-tab.md) pour exposer les informations de contact importantes dans Teams. Par exemple, les collègues ont un accès rapide au numéro de téléphone du support technique. Mais au lieu d’appeler, que se passe-t-il si des personnes peuvent contacter le support technique à l’aide d’un chatbot ? Votre patron vous demande de consulter la rapidité avec laquelle vous pouvez faire fonctionner un robot de conversation de base dans Teams.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application et un bot à l’aide de Microsoft teams Toolkit pour Visual Studio code
> * Identifier certaines des propriétés de manifeste de l’application et la génération de modèles automatique correspondant aux robots
> * Héberger une application localement
> * Configurer un bot pour teams
> * Chargement et tester un bot dans teams

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).

## <a name="1-create-your-app-project"></a>1. créer votre projet d’application

La boîte à outils Microsoft teams vous permet de configurer les composants suivants pour votre application :

* **Manifeste de l’application et génération** d’une structure correspondant aux robots
* **Robot** enregistré automatiquement avec le service Microsoft Azure bot

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **bot** puis **suivant**.
1. Sélectionnez **créer un nouveau robot** et **Connectez** -vous pour vous connecter à l’aide de votre compte de développement Microsoft 365.<br/>
:::image type="content" source="../assets/images/build-your-first-app/vsc-create-bot.png" alt-text="Illustration illustrant comment, dans la boîte à outils Teams, connectez-vous à votre compte Microsoft 365 pour créer un nouveau Bot.":::
1. Stockez votre ID de robot et votre mot de passe (vous en aurez besoin plus tard).
1. Module Entrez un nom personnalisé pour votre bot et sélectionnez **créer**. (Rappelez-vous qu’il s’agit du nom de votre bot et non du nom de l’application teams que vous avez déjà spécifiée.)
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.

## <a name="2-identify-relevant-app-project-components"></a>2. identifier les composants de projet d’application pertinents

La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams. Examinons les principaux composants de la création d’un bot.

### <a name="app-manifest"></a>Manifeste de l’application

L’extrait de code suivant du manifeste de l’application ( `manifest.json` fichier dans le répertoire de votre projet `.publish` ) affiche les propriétés et les valeurs par défaut relatives aux robots.

```JSON
"bots": [
    {
        "botId": "{botId0}",
        "scopes": [
            "personal",
            "groupchat",
            "team"
        ],
        "supportsFiles": false,
        "isNotificationOnly": false,
        "commandLists": [
            {
                "scopes": [
                    "personal",
                    "groupchat",
                    "team"
                ],
                "commands": [
                    {
                        "title": "Hello",
                        "description": "Sends a hello message and @mention the sender"
                    }
                ]
            }
        ]
    }
],
```

Pour le moment, nous allons nous concentrer sur les propriétés requises suivantes. (Consultez la liste complète des propriétés prises en charge [`bots`](../resources/schema/manifest-schema.md#bots) .)

* `botId`: ID du bot que vous avez créé lors de la création de votre projet. (Stocké dans `{botId0}` , vous pouvez trouver l’ID réel dans `Development.env` .)
* `scopes`: Spécifie si votre bot est disponible dans les `personal` `groupchat` `team` contextes, ou (c’est-à-dire, canal).
* `commands`: Commandes disponibles que les utilisateurs peuvent envoyer à votre robot.
* `title`: Nom de la commande bot qui s’affiche dans le client Teams.
* `description`: Brève description ou exemple de la syntaxe et des arguments pour aider les utilisateurs à comprendre ce que fait la commande bot.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

La génération de modèles automatique d’application fournit un `botActivityHandler.js` fichier, situé dans le répertoire racine de votre projet, pour la gestion de la manière dont votre bot traite les activités dans Teams (par exemple, la façon dont le bot répond à des messages spécifiques, tels que « Hello »).

Le `.env` fichier, également dans le répertoire racine, stocke l’ID et le mot de passe de votre bot.

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre robot sur un serveur Web local (port 3978).

1. Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .
1. Copiez l’URL HTTPs dans la sortie, car teams nécessite des connexions HTTPs.
1. Dans votre `.publish` répertoire, ouvrez `Development.env` .
1. Remplacez la `baseUrl0` valeur par l’URL copiée. (Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ca5.ngrok.io` .)

Le manifeste de votre application pointe vers l’emplacement où vous hébergez le robot.

## <a name="4-configure-your-bot"></a>4. configurer votre robot

Pour utiliser un bot dans Teams, vous devez l’enregistrer auprès du service Microsoft Azure bot. Heureusement, cette opération est exécutée automatiquement lorsque vous configurez votre application à l’aide de Team Toolkit.

### <a name="specify-your-bot-id-and-password"></a>Spécifier l’ID et le mot de passe de votre robot

Lorsque votre bot est enregistré avec le service Azure bot, il reçoit un ID et un mot de passe sur lesquels votre application teams doit être informée.

1. Localisez l’ID et le mot de passe du robot stocké lors de l’installation de la boîte à outils.
1. Dans le répertoire racine, ouvrez le `.env` fichier.
1. Ajoutez votre ID de robot et votre mot de passe à `BotId` et `BotPassword` , respectivement.

### <a name="add-the-bot-endpoint-address"></a>Ajouter l’adresse du point de terminaison du bot

Vous devez spécifier une URL de point de terminaison pour recevoir et traiter les messages utilisateur (par exemple, les demandes) envoyées au bot. En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` : Vous pouvez configurer cet outil rapidement dans Team Toolkit.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. Accédez à **gestion des robots > inscriptions des robots existants** et sélectionnez le robot que vous avez créé lors de l’installation.
1. Dans le champ **adresse du point de terminaison de robot** , entrez le serveur Web local où vous hébergez le bot ( `baseUrl10` valeur) et ajoutez `/api/messages` -y.

    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Illustration illustrant l’emplacement où vous pouvez configurer l’URL du point de terminaison du bot dans Team Toolkit.":::

Votre robot pourra répondre aux messages dans Teams.

## <a name="5-run-your-app"></a>5. exécuter votre application

Vous avez configuré une URL pour héberger votre robot et le configurer pour qu’il gère les messages. Il est temps de faire fonctionner votre robot.

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` .

Si elle réussit, un message semblable à celui-ci s’affiche, indiquant que votre robot est à l’écoute de l’activité `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. chargement de votre robot dans teams

Une fois que votre robot est en cours d’exécution, vous pouvez l’installer dans Teams.

> [!TIP]
> Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).

1. Connectez-vous au client teams avec votre compte qui autorise l’application chargement.
1. Sélectionnez **applications**, puis **Télécharger une application personnalisée**.
1. Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` .
1. Dans la fenêtre installation modale, sélectionnez **Ajouter** pour installer votre application.

## <a name="7-test-your-bot"></a>7. tester votre robot

Maintenant pour la partie amusante : disons « Hello » à votre bot dans une conversation en un seul.

1. Dans Teams, sélectionnez **autres** :::image type="icon" source="../assets/icons/teams-client-more.png"::: sur le côté gauche.
1. Recherchez et sélectionnez le robot que vous venez de versions test chargées.<br/>
   :::image type="content" source="../assets/images/build-your-first-app/bot-teams-access.png" alt-text="Illustration illustrant l’emplacement où vous accédez à votre bot dans Teams.":::
1. Dans la zone de composition, envoyez un `Hello` message.

Votre robot répond avec un message semblable à celui-ci.

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Capture d’écran illustrant un utilisateur dire « Hello » à un bot de teams et obtenant une réponse.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’un bot de teams de base qui peut communiquer avec des utilisateurs un-sur-un ou des paramètres de groupe (canaux et conversations).

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.

### <a name="toolkit-setup-fails"></a>Échec de l’installation de la boîte à outils

Lors de la configuration de votre projet d’application avec Team Toolkit, vous obtenez une erreur après avoir sélectionné l’option **créer un nouveau Bot** et vous être connecté avec votre compte de développement Microsoft 365.

Il peut s’agir d’un problème d’authentification. Procédez comme suit pour terminer la configuration de votre projet.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis **déconnectez-vous**.
1. Recommencez le processus d’installation en vous connectant avec le même compte et en créant un nouveau Bot.

### <a name="bot-isnt-connected-to-teams"></a>Le bot n’est pas connecté à teams

Si vous avez installé votre application, mais que le bot ne fonctionne pas, vérifiez que le bot est [connecté au *canal*teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams. Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>En savoir plus

* [Voir les autres robots que les robots peuvent faire avec l’un de nos exemples](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Concepts de base d’une conversation de bot](../bots/how-to/conversations/conversation-basics.md)
* [Authentification de robot dans teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
* [Créer un bot sans la boîte à outils](../bots/how-to/create-a-bot-for-teams.md)
