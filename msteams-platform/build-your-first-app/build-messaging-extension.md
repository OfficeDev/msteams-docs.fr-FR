---
title: Créer une extension de messagerie teams
author: heath-hamilton
description: Découvrez comment créer une extension de messagerie pour votre première application Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: 0475fcea7d865849fa60c5b3b23788bf90ee5e25
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210130"
---
# <a name="build-a-teams-messaging-extension"></a>Créer une extension de messagerie teams

Il existe deux types d' *extensions de messagerie*teams : [commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) et commandes d' [action](../messaging-extensions/how-to/action-commands/define-action-command.md).

Dans cette leçon, vous allez créer une *commande de recherche* (également appelée *extension de messagerie basée sur la recherche*), qui est un raccourci permettant de trouver du contenu externe et de le partager dans Teams. Les utilisateurs peuvent accéder aux commandes de recherche à partir de la [zone de composition ou de commande teams](../messaging-extensions/what-are-messaging-extensions.md).

## <a name="your-assignment"></a>Votre affectation

Le service d’assistance de votre organisation communique avec les utilisateurs par le biais de teams, mais les tickets se trouvent dans un système distinct. Cela signifie que le personnel de support technique doit constamment basculer entre les applications. Vous allez examiner la manière dont vous pouvez réduire ce pourcentage de changement de contexte en créant une simple extension de messagerie basée sur la recherche pour Teams.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application et un bot d’extension de messagerie à l’aide de Microsoft teams Toolkit pour Visual Studio code
> * Identifier les propriétés du manifeste de l’application et une partie de la structure relative aux extensions de messagerie
> * Héberger une application localement
> * Configurer le bot pour votre extension de messagerie
> * Chargement et test d’une extension de messagerie dans teams

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).

## <a name="create-your-app-project"></a>Créer votre projet d’application

Microsoft teams Toolkit vous permet de configurer les composants suivants pour votre extension de messagerie :

* **Manifeste de l’application et génération** d’une structure correspondant aux extensions de messagerie
* **Robot** de votre extension de messagerie enregistré automatiquement avec le service Microsoft Azure bot

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez extension de **messagerie** , puis **suivant**.
1. Dans l’écran **configurer l’extension de messagerie** , procédez comme suit :
    1. Choisissez uniquement l’option **basée sur la recherche** pour le type d’extension de messagerie.
    1. Sélectionnez **créer un nouveau robot** et **Connectez** -vous pour vous connecter à l’aide de votre compte de développement Microsoft 365.
    1. Stockez votre ID de robot et votre mot de passe (vous en aurez besoin plus tard).
    1. Module Entrez un nom personnalisé pour votre bot et sélectionnez **créer**. (Il ne s’agit pas du nom de l’application teams que vous avez déjà spécifiée.)
    1. Pour le moment, sélectionnez **non** pour l’option lien unfurling.</br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="Illustration illustrant comment, dans Team Toolkit, connectez-vous à votre compte Microsoft 365 afin de créer un nouveau bot pour votre extension de messagerie.":::
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.

## <a name="identify-relevant-app-project-components"></a>Identifier les composants de projet d’application pertinents

La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams.

### <a name="app-manifest"></a>Manifeste de l’application

L’extrait de code suivant du manifeste de l’application ( `manifest.json` fichier dans le répertoire de votre projet `.publish` ) affiche les propriétés et les valeurs par défaut relatives aux extensions de messagerie.

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

Nous allons comprendre quelques-unes des propriétés que le kit de outils a créées pour vous. (Consultez la liste complète des propriétés prises en charge [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) .)

* `botId`: ID du bot que vous avez créé lors de la création de votre projet. (Stocké dans `{botId0}` , vous pouvez trouver l’ID réel dans `Development.env` .)
* `commands`: Commandes disponibles pour l’extension de messagerie. Le kit de outils vous a fourni une génération de modèles pour une commande de recherche.
* `context`: Où les utilisateurs peuvent appeler l’extension de messagerie. Dans ce cas, vous pouvez lancer l’extension de messagerie à partir de la zone de commande ou de composition de teams.
* `description`: Texte d’aide de l’interface utilisateur indiquant ce que fait la commande ou comment l’utiliser.
* `parameters`: Inclut tous les paramètres acceptés par une commande (vous devez en avoir au moins un et peut avoir jusqu’à cinq).
* `parameters.description`: Texte d’aide de l’interface utilisateur décrivant l’objectif ou l’exemple d’entrée du paramètre.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

Le échafaudage de l’application inclut un `.env` fichier, situé dans le répertoire racine de votre projet, qui stocke l’ID et le mot de passe du bot de votre extension de messagerie.

Dans le répertoire racine, il existe un `botActivityHandler.js` fichier permettant de gérer la manière dont votre extension de messagerie (ou techniquement, le [bot de l’extension de messagerie](#configuring-the-bot-for-your-messaging-extension)) répond aux requêtes de recherche dans Teams.

## <a name="set-up-a-secure-tunnel-to-your-app"></a>Configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre extension de messagerie sur un serveur Web local (port 3978).

1. Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .
1. Copiez l’URL HTTPs dans la sortie, car teams nécessite des connexions HTTPs.
1. Dans votre `.publish` répertoire, ouvrez `Development.env` .
1. Remplacez la `baseUrl0` valeur par l’URL copiée. (Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ca5.ngrok.io` .)

Votre manifeste d’application pointe vers l’emplacement où vous hébergez le bot utilisé par l’extension de messagerie.

## <a name="configuring-the-bot-for-your-messaging-extension"></a>Configuration du bot pour votre extension de messagerie

Les extensions de messagerie s’appuient sur les robots pour envoyer et traiter les demandes des utilisateurs de teams vers votre service hébergé.

Le bot doit être enregistré avec le service Azure bot, qui a été créé lors de la configuration de votre application à l’aide du kit de outils Teams.

### <a name="specify-your-bot-id-and-password"></a>Spécifier l’ID et le mot de passe de votre robot

Lorsque votre bot est enregistré avec le service Azure bot, il reçoit un ID et un mot de passe sur lesquels votre application teams doit être informée.

1. Localisez l’ID et le mot de passe du robot stocké lors de l’installation de la boîte à outils.
1. Dans le répertoire racine, ouvrez le `.env` fichier.
1. Définissez l’ID et le mot de passe de votre robot sur les `BotId` `BotPassword` Propriétés et, respectivement.

### <a name="add-the-bot-endpoint-address"></a>Ajouter l’adresse du point de terminaison du bot

Vous devez spécifier une URL de point de terminaison bot pour recevoir et traiter des requêtes de recherche dans votre extension de messagerie. En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` : Vous pouvez configurer cet outil rapidement dans Team Toolkit.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. Accédez à **gestion des robots > inscriptions des robots existants** et sélectionnez le robot que vous avez créé lors de l’installation.
1. Dans le champ **adresse du point de terminaison de robot** , entrez le serveur Web local où vous hébergez le bot ( `baseUrl10` valeur) et ajoutez `/api/messages` -y.

Votre robot pourra gérer les requêtes dans votre extension de messagerie.

## <a name="run-your-app"></a>Exécuter votre application

Vous avez configuré une URL pour héberger votre extension de messagerie et la configurer pour qu’elle gère les recherches. Il est temps de faire fonctionner votre application.

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` .

Si elle réussit, un message semblable au suivant s’affiche, indiquant que votre service d’extension de messagerie est à l’écoute de l’activité `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-messaging-extension-in-teams"></a>Chargement de votre extension de messagerie dans teams

Une fois que votre extension de messagerie est en cours d’exécution, vous pouvez l’installer dans Teams.

> [!TIP]
> Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).

1. Connectez-vous au client teams avec votre compte qui autorise l’application chargement.
1. Sélectionnez **applications**, puis **Télécharger une application personnalisée**.
1. Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` .
1. Dans la fenêtre installation modale, sélectionnez **Ajouter** pour installer votre application.

## <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

Découvrez comment fonctionnent les extensions de messagerie dans une conversation Teams.

1. Démarrez une nouvelle conversation. Dans la zone de composition, sélectionnez **plus** , :::image type="icon" source="../assets/icons/teams-client-more.png"::: puis choisissez l’application de l’extension de messagerie que vous venez de versions test chargées.<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="Illustration illustrant comment accéder à une extension de messagerie basée sur la recherche dans la zone de composition de teams.":::
1. Essayez de rechercher un article (par exemple, « tickets »). Si votre application fonctionne, vous verrez des exemples de résultats de recherche (vous pouvez ajouter votre propre version ultérieure).<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Capture d’écran illustrant l’utilisation d’une extension de messagerie basée sur la recherche dans la zone de composition de teams.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’une extension de messagerie teams de base qui est configurée pour rechercher du contenu externe dans la zone de composition ou de commande.

## <a name="next-steps"></a>Étapes suivantes

Consultez les pages suivantes pour continuer et créer une extension de messagerie complète :

1. [Définir des commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) pertinentes pour votre service.
1. Configurez votre service pour [répondre aux recherches des utilisateurs](../messaging-extensions/how-to/search-commands/respond-to-search.md).

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.

### <a name="toolkit-setup-fails"></a>Échec de l’installation de la boîte à outils

Lors de la configuration de votre projet d’application avec Team Toolkit, vous obtenez une erreur après avoir sélectionné l’option **créer un nouveau Bot** et vous être connecté avec votre compte de développement Microsoft 365.

Il peut s’agir d’un problème d’authentification. Procédez comme suit pour terminer la configuration de votre projet.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis **déconnectez-vous**.
1. Recommencez le processus d’installation en vous connectant avec le même compte et en créant un nouveau Bot.

### <a name="bot-isnt-connected-to-teams"></a>Le bot n’est pas connecté à teams

Si vous avez installé votre application, mais qu’elle ne fonctionne pas, vérifiez que le robot de l’extension de messagerie est [connecté au *canal*teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams. Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>Si vous souhaitez en savoir plus

* [Inclure une fonctionnalité de unfurling de liens](../messaging-extensions/how-to/link-unfurling.md)
* [Ajouter une authentification](../messaging-extensions/how-to/add-authentication.md)
* [Créer une extension de messagerie basée sur une action](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
