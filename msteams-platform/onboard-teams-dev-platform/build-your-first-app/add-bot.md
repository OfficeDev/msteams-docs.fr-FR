---
title: Créer un robot pour Teams
author: heath-hamilton
description: Découvrez comment créer un bot dans votre première application Microsoft Teams.
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
ms.openlocfilehash: f1307bcc7bb864ddfa97b9297f34fa4f7d5fcb0d
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964724"
---
# <a name="create-a-bot-for-teams"></a>Créer un robot pour Teams

Vous allez créer une application *bot* de base dans ce didacticiel. Un bot agit comme un intermédiaire entre les utilisateurs de teams et votre service Web. Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.

## <a name="your-assignment"></a>Votre affectation

Votre espace de travail a utilisé des [onglets](../build-your-first-app/add-personal-tab.md) pour exposer les informations de contact importantes dans Teams. Par exemple, les collègues ont un accès rapide au numéro de téléphone du support technique. Mais au lieu d’appeler, que se passe-t-il si des personnes peuvent contacter le support technique à l’aide d’un chatbot ? Votre patron vous demande de consulter la rapidité avec laquelle vous pouvez faire fonctionner un robot de conversation de base dans Teams.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application et un bot à l’aide de Microsoft teams Toolkit pour Visual Studio code
> * Identifier les propriétés du manifeste de l’application et une partie de la structure concernant les robots
> * Héberger un bot localement
> * Configurer un bot pour teams
> * Chargement et tester un bot dans teams

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l’avez pas encore fait, configurez votre [compte](building-real-world-app.md#set-up-your-development-account) de développement Microsoft 365 et les outils de l' [application teams](building-real-world-app.md#install-your-development-tools).

## <a name="create-your-app-project-and-bot"></a>Création de votre projet d’application et de votre robot

La boîte à outils Microsoft teams vous permet de configurer les composants suivants pour votre application :

* **Projet d’application**: inclut le manifeste de l’application et la génération de modèles adaptés aux robots
* **Bot**: configure un nouveau Bot et l’enregistre avec le service Microsoft Azure bot.

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **bot** puis **suivant**.
1. Sélectionnez **créer un nouveau robot** et **Connectez** -vous pour vous connecter à l’aide de votre compte de développement Microsoft 365.<br/>
:::image type="content" source="../doc-links/images/vsc-create-bot.png" alt-text="Illustration illustrant comment, dans la boîte à outils Teams, connectez-vous à votre compte Microsoft 365 pour créer un nouveau Bot.":::
1. Module Entrez un nom personnalisé pour votre bot et sélectionnez **créer**. (Rappelez-vous qu’il s’agit du nom de votre bot et non du nom de l’application teams que vous avez déjà spécifiée.)
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.

## <a name="identify-relevant-app-project-components"></a>Identifier les composants de projet d’application pertinents

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

Pour le moment, nous allons nous concentrer sur les propriétés requises suivantes. (Consultez la liste complète des propriétés prises en charge [`bots`](../../resources/schema/manifest-schema.md#bots) .)

* `botId`: ID du bot que vous avez créé lors de la création de votre projet. (Stocké dans `{botId0}` , vous pouvez trouver l’ID réel dans `Development.env` .)
* `scopes`: Spécifie si votre bot est disponible dans les `personal` `groupchat` `team` contextes, ou (c’est-à-dire, canal).
* `commands`: Commandes disponibles que les utilisateurs peuvent envoyer à votre robot.
* `title`: Nom de la commande de bot que les utilisateurs voient dans le client Teams.
* `description`: Brève description ou exemple de la syntaxe et des arguments pour aider les utilisateurs à comprendre ce que fait la commande bot.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

La génération de modèles automatique d’application fournit un `botActivityHandler.js` fichier, situé dans le répertoire racine de votre projet, pour la gestion de la manière dont votre bot traite les activités dans Teams (par exemple, la façon dont le bot répond à des messages spécifiques, tels que « Hello »).

## <a name="set-up-a-secure-tunnel-to-your-app"></a>Configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre robot sur un serveur Web local (port 3978).

1. Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .
1. Copiez l’URL HTTPs dans la sortie, car teams nécessite des connexions HTTPs.
1. Dans votre `.publish` répertoire, ouvrez `Development.env` .
1. Remplacez la `baseUrl0` valeur par l’URL copiée. (Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ca5.ngrok.io` .)

Le manifeste de votre application pointe vers l’emplacement où vous hébergez le robot.

## <a name="configuring-your-bot"></a>Configuration de votre robot

Pour utiliser un bot dans Teams, vous devez l’enregistrer auprès du service Microsoft Azure bot. Heureusement, cette opération est exécutée automatiquement lorsque vous configurez votre application à l’aide de Team Toolkit.

### <a name="add-the-bot-endpoint-address"></a>Ajouter l’adresse du point de terminaison du bot

Vous devez spécifier une URL de point de terminaison pour recevoir et traiter les messages utilisateur (par exemple, les demandes) envoyées au bot. En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` : Vous pouvez configurer cet outil rapidement dans Team Toolkit.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. Accédez à **gestion des robots > inscriptions des robots existants** et sélectionnez le robot que vous avez créé lors de l’installation.
1. Dans le champ **adresse du point de terminaison de robot** , entrez le serveur Web local sur lequel vous hébergez le bot et ajoutez-le `/api/messages` à celui-ci.

    :::image type="content" source="../doc-links/images/bot-config-endpoint-url.png" alt-text="Illustration illustrant l’emplacement où vous pouvez configurer l’URL du point de terminaison du bot dans Team Toolkit.":::

Votre robot pourra répondre aux messages dans Teams.

## <a name="run-your-app"></a>Exécuter votre application

Vous avez configuré une URL pour héberger votre robot et le configurer pour qu’il gère les messages. Il est temps de faire fonctionner votre robot.

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` .

Si elle réussit, un message semblable à celui-ci s’affiche, indiquant que votre robot est à l’écoute de l’activité `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a>Chargement de votre robot dans teams

Une fois que votre robot est en cours d’exécution, vous pouvez l’installer dans Teams.

> [!TIP]
> Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).

1. Connectez-vous au client teams avec votre compte qui autorise l’application chargement.
1. Sélectionnez **applications**, puis **Télécharger une application personnalisée**.
1. Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` .
1. Dans la fenêtre installation modale, sélectionnez **Ajouter** pour installer votre application.

## <a name="test-your-bot"></a>Tester votre robot

Maintenant pour la partie amusante : disons « Hello » à votre bot dans une conversation en un seul.

1. Dans Teams, sélectionnez **autres** :::image type="icon" source="../doc-links/images/teams-client-more.png"::: sur le côté gauche.
1. Recherchez et sélectionnez le robot que vous venez de versions test chargées.<br/>
   :::image type="content" source="../doc-links/images/bot-teams-access.png" alt-text="Illustration illustrant l’emplacement où vous accédez à votre bot dans Teams.":::
1. Dans la zone de composition, envoyez un `Hello` message.

Votre robot répond avec un message semblable à celui-ci.

:::image type="content" source="../doc-links/images/contoso-chatbot.png" alt-text="Capture d’écran illustrant un utilisateur dire « Hello » à un bot de teams et obtenant une réponse.":::

> [!NOTE]
> Si vous effectuez des modifications de code après avoir testé votre bot (par exemple, vous mettez à jour `botActivityHandler.js` ), vous devez réexécuter votre application pour voir ces modifications reflétées dans Teams.

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’un bot de teams de base qui peut communiquer avec des utilisateurs un-sur-un ou des paramètres de groupe (canaux et conversations).

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.

### <a name="toolkit-setup-fails"></a>Échec de l’installation de la boîte à outils

Lors de la configuration de votre projet d’application avec Team Toolkit, vous obtenez une erreur après avoir sélectionné l’option **créer un nouveau Bot** et vous être connecté avec votre compte de développement Microsoft 365.

Il peut s’agir d’un problème d’authentification. Procédez comme suit pour terminer la configuration de votre projet.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis **déconnectez-vous**.
1. Recommencez le processus d’installation en vous connectant avec le même compte et en créant un nouveau Bot.

### <a name="bot-isnt-connected-to-teams"></a>Le bot n’est pas connecté à teams

Si vous avez installé votre application, mais que le bot ne fonctionne pas, vérifiez que le bot est [connecté au *canal*teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams. Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>Si vous souhaitez en savoir plus

* [Voir les autres robots que les robots peuvent faire avec l’un de nos exemples (GitHub)](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Concepts de base d’une conversation de bot](../../bots/how-to/conversations/conversation-basics.md)
* [Authentification de robot dans teams](../../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
