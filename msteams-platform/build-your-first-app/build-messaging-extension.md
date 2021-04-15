---
title: Get started - Build a messaging extension
author: heath-hamilton
description: Créez rapidement une extension de messagerie Microsoft Teams à l'aide de microsoft Teams Shared Computer Toolkit.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 09e851820314efd3dc114b926a0111603cac18a4
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696877"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>Créer une extension de messagerie pour Microsoft Teams

Il existe deux types *d'extensions de messagerie* Teams : les commandes [de recherche et](../messaging-extensions/how-to/search-commands/define-search-command.md) les commandes [d'action.](../messaging-extensions/how-to/action-commands/define-action-command.md)

Dans cette leçon, vous allez créer une commande de recherche *(également* appelée *extension* de messagerie basée sur la recherche), qui est un raccourci pour rechercher du contenu externe et le partager dans Teams. Les utilisateurs peuvent accéder aux commandes de recherche à partir de la zone de [composition ou de commande Teams.](../messaging-extensions/what-are-messaging-extensions.md)

## <a name="your-assignment"></a>Votre affectation

Le service d'aide de votre organisation communique avec les utilisateurs via Teams, mais les tickets résident dans un système distinct. Cela signifie que le personnel de support technique doit constamment faire des allers-retours entre les applications. Vous allez étudier comment réduire cette quantité de changement de contexte en créant une simple extension de messagerie basée sur la recherche pour Teams.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d'application et un bot d'extension de messagerie à l'aide de la Shared Computer Toolkit Microsoft Teams Visual Studio Code
> * Identifier les configurations d'application et une partie de la échafaudage pertinente pour les extensions de messagerie
> * Héberger une application localement
> * Configurer le bot pour votre extension de messagerie
> * Chargement de version test et test d'une extension de messagerie dans Teams

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l'avez pas encore fait, assurez-vous de bien comprendre et [d'installer les conditions préalables de développement teams.](build-first-app-overview.md#get-prerequisites)

## <a name="1-create-your-app-project"></a>1. Créer votre projet d'application

L'Shared Computer Toolkit Microsoft Teams vous aide à configurer les composants suivants pour votre extension de messagerie :

* **Configurations d'application et échafaudage pertinents** pour les extensions de messagerie
* **Bot** pour votre extension de messagerie qui est automatiquement inscrite auprès du service Microsoft Azure Bot

> [!TIP]
> Si vous n'avez pas encore créé de projet d'application Teams, il peut vous être utile de suivre ces [instructions](../build-your-first-app/build-and-run.md) qui expliquent les projets plus en détail.

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.
1. Dans **l'écran Ajouter des fonctionnalités,** **sélectionnez Extension de messagerie,** puis **Suivant**.
1. Entrez un nom pour votre application Teams. (Il s'agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d'application sur votre ordinateur local.)
1. Dans **l'écran Configurer l'extension de** messagerie, faites les choses suivantes :
    1. Choisissez uniquement **l'option de recherche** pour le type d'extension de messagerie.
    1. Sélectionnez **Créer un bot,** puis **Créer l'inscription du bot.** Si elle réussit, votre nouveau bot aura un **état** inscrit.
    1. Pour l'instant, **sélectionnez Non** pour l'option de déploiement de lien.
1. Sélectionnez **Terminer** en bas de l'écran pour configurer votre projet.

## <a name="2-identify-relevant-app-project-components"></a>2. Identifier les composants de projet d'application pertinents

La plupart des configurations d'application et de la création de la Shared Computer Toolkit sont automatiquement définies lorsque vous créez votre projet.

### <a name="app-configurations"></a>Configurations d'application

Pour afficher ou mettre à jour les configurations de votre extension de messagerie, sélectionnez **App Studio** dans le kit de ressources et allez aux **extensions de messagerie.**

### <a name="app-scaffolding"></a>Échafaudage d'application

La création de la échafaudage de l'application fournit un fichier, situé dans le répertoire racine de votre projet, pour gérer la façon dont votre extension de messagerie (ou techniquement, le bot de l'extension de messagerie) répond aux requêtes de recherche dans `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre extension de messagerie sur un serveur web local (port 3978).

1. Si ce n'est pas déjà fait, installez [ngrok](https://ngrok.com/download).
1. Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .
1. Copiez l'URL HTTPS dans la sortie (par exemple), car `https://468b9ab725e9.ngrok.io` Teams requiert des connexions HTTPS.

Avec cette URL, Teams (qui nécessite des connexions HTTPS) pourra tunneler vers l'endroit où vous hébergez votre application ( `localhost` sur le port 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. Configurer le bot pour votre extension de messagerie

Les extensions de messagerie s'appuient sur des bots pour envoyer et traiter les demandes des utilisateurs de Teams vers votre service hébergé. Le bot doit être inscrit auprès d'Azure Bot Service, ce qui a été fait lorsque vous avez installé votre application à l'aide de la Shared Computer Toolkit Teams.

Vous devez toujours spécifier une URL de point de terminaison de bot pour recevoir et traiter les requêtes de recherche dans votre extension de messagerie. En règle générale, l'URL ressemble `https://HOST_URL/api/messages` à . Vous pouvez configurer cette configuration rapidement dans le kit de ressources.

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Shared Computer Toolkit**.
1. Go to **Bots > Existing bot registrations** and select the bot you created during setup.
1. Dans le **champ d'adresse** du point de terminaison bot, entrez l'URL ngrok (par exemple, ) où vous hébergez le bot et y `https://468b9ab725e9.ngrok.io` `/api/messages` appendez-le.

Votre bot sera en mesure de gérer les requêtes dans votre extension de messagerie.

## <a name="5-build-and-run-your-app"></a>5. Créer et exécuter votre application

Vous avez configuré une URL pour héberger votre extension de messagerie et configurée pour gérer les recherches. Il est temps de rendre votre application opérationnel.

1. Dans un terminal, allez dans le répertoire racine de votre projet d'application et exécutez `npm install` .
1. Exécutez `npm start` .

Si l'opération réussit, le message suivant indique que votre service d'extension de messagerie est à l'écoute de l'activité sur votre `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Chargement d'une version de version de votre extension de messagerie dans Teams

Une fois votre extension de messagerie en cours d'exécution, vous pouvez l'installer dans Teams.

> [!TIP]
> Si vous n'avez pas encore chargé une application Teams et que vous avez des problèmes, suivez ces [instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. Dans Visual Studio Code, appuyez sur la **touche F5** pour lancer un client web Teams.
1. Dans la boîte de dialogue d'installation de l'application, **sélectionnez Ajouter pour moi.**

## <a name="7-test-your-messaging-extension"></a>7. Tester votre extension de messagerie

Découvrez comment fonctionnent les extensions de messagerie dans une conversation Teams.

1. Démarrez une nouvelle conversation. Dans la zone de composition, sélectionnez **Plus** et choisissez l'application d'extension de messagerie :::image type="icon" source="../assets/icons/teams-client-more.png"::: que vous avez juste chargé de côté.
1. Essayez de rechercher quelque chose (par exemple, **Tickets).** Si votre application fonctionne, vous verrez des exemples de résultats de recherche (vous pourrez en ajouter d'autres ultérieurement).<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Capture d'écran montrant comment une extension de messagerie basée sur la recherche est utilisée dans la zone de composition Teams.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous avez une extension de messagerie Teams de base qui est définie pour rechercher du contenu externe dans la zone de composition ou de commande.

## <a name="next-steps"></a>Étapes suivantes

Consultez les pages suivantes pour continuer et créer une extension de messagerie complète :

1. [Définissez les commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) qui sont pertinentes pour votre service.
1. Configurez votre service pour [répondre aux recherches des utilisateurs.](../messaging-extensions/how-to/search-commands/respond-to-search.md)

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous aider si vous avez des problèmes lors de la réalisation de ce didacticiel.

### <a name="bot-isnt-connected-to-teams"></a>Le bot n'est pas connecté à Teams

Si vous avez installé votre application, mais qu'elle ne fonctionne pas, assurez-vous que le bot de l'extension de messagerie est connecté au canal [Teams d'Azure Bot Service.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Il est important de comprendre que ce n'est pas le même qu'un canal dans Teams. Dans ce cas, un canal est la façon dont azure Bot Service connecte votre bot à Teams ou à une autre application de communication microsoft ou [tierce prise en charge.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="learn-more"></a>En savoir plus

* [Inclure une fonctionnalité de déploiement de lien](../messaging-extensions/how-to/link-unfurling.md)
* Suivez nos [instructions de conception](../messaging-extensions/design/messaging-extension-design.md) et créez avec des [modèles d'interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) prêts pour la production pour créer une expérience transparente.
* [Ajouter une authentification](../messaging-extensions/how-to/add-authentication.md)
* [Créer une extension de messagerie basée sur une action](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)

