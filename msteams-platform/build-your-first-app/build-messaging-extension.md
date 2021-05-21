---
title: Get started - Build a messaging extension
author: girliemac
description: Créez rapidement une extension Microsoft Teams messagerie à l’aide du Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: c120a5b5d878c549cde008c3e1ccc71743a4e24f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566060"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a>Créez votre première extension de messagerie pour Microsoft Teams

Il existe deux types d’extensions Teams *messagerie électronique*: les commandes [de recherche et](../messaging-extensions/how-to/search-commands/define-search-command.md) les commandes [d’action.](../messaging-extensions/how-to/action-commands/define-action-command.md)

Ce didacticiel vous apprend à créer une commande de recherche *(également* appelée *extension* de messagerie basée sur la recherche), qui est un raccourci pour rechercher du contenu externe et le partager dans Teams. Les utilisateurs peuvent accéder aux commandes de recherche à partir Teams la zone de composition ou de commande.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

* Créez un projet d’application et un bot d’extension de messagerie à l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.
* Comprendre les configurations d’application et la échafaudage pertinente pour les extensions de messagerie.
* Hébergez une application localement.
* Configurez le bot pour votre extension de messagerie.
* Chargez et testez une extension de messagerie dans Teams.

## <a name="prerequisites"></a>Conditions préalables

Assurez-vous que vous comprenez comment configurer et créer une application Teams simple. Pour plus d’informations, [voir créer votre première Microsoft Teams application « Hello World!](../build-your-first-app/build-and-run.md)».

## <a name="1-create-your-app-project"></a>1. Créer votre projet d’application

Le Microsoft Teams Shared Computer Toolkit vous permet de configurer les composants suivants pour votre extension de messagerie :

* **Configurations d’application et échafaudage pertinents** pour les extensions de messagerie.
* **Bot** pour votre extension de messagerie qui est automatiquement inscrite auprès du Microsoft Azure Bot Service.

**Pour créer votre projet d’application**

1. In Visual Studio Code, select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Create a new **Teams app**.
1. Lorsque vous y invitez, connectez-vous avec votre Microsoft 365 de développement.
1. Dans **l’écran Sélectionner un** projet, dans **recherche d’extensions** de  >  messagerie, cliquez **sur JS (JavaScript).** 
1. Entrez un nom pour votre application Teams de messagerie. Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.
1. Sélectionnez **Créer un bot,** puis cliquez **sur Créer l’inscription du** bot. Si elle réussit, votre nouveau bot aura *l’état* Inscrit. Votre bot est désormais inscrit automatiquement auprès du service Microsoft Azure Bot. 
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet et enregistrez-le sur votre ordinateur local.

## <a name="2-understand-your-app-project-components"></a>2. Comprendre les composants de votre projet d’application

La plupart des configurations d’application et de la création de la Teams Shared Computer Toolkit sont automatiquement définies.

* Configurations d’application : pour afficher ou mettre à jour les configurations de votre extension de messagerie, sélectionnez **App Studio** dans le kit de ressources et allez aux **extensions de messagerie.**
* Création de la forme de l’application : la création de la forme de l’application fournit un fichier, situé dans le répertoire racine de votre projet, pour gérer la façon dont votre extension de messagerie (ou techniquement, le bot de l’extension de messagerie) répond aux requêtes de recherche dans `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre extension de messagerie sur un serveur web local (port 3978). Vous allez utiliser [ngrok](https://ngrok.com/download) pour configurer un tunnel sécurisé vers localhost. Pour [plus d’informations, voir](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) créer Microsoft Teams bot. 

1. Si ce n’est pas déjà fait, installez [ngrok](https://ngrok.com/download).
1. Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .
1. Copiez l’URL HTTPS dans la sortie (par exemple), car Teams `https://468b9ab725e9.ngrok.io` nécessite des connexions HTTPS.

   Avec cette URL, Teams (qui nécessite des connexions HTTPS) pourra tunneler vers l’endroit où vous hébergez votre application ( sur le `localhost` port 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. Configurer le bot pour votre extension de messagerie

Les extensions de messagerie s’appuient sur des bots pour envoyer et traiter les demandes des utilisateurs Teams à votre service hébergé. Le bot doit être inscrit auprès d’Azure Bot Service, ce qui a été fait lorsque vous avez installé votre application à l’aide du Teams Shared Computer Toolkit.

Vous devez toujours spécifier une URL de point de terminaison de bot pour recevoir et traiter les requêtes de recherche dans votre extension de messagerie. En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à . Vous pouvez configurer cette configuration rapidement dans le kit de ressources.

1. In Visual Studio Code, select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Open **Microsoft Teams Shared Computer Toolkit**.
1. Go to **Bots > Existing bot registrations** and select the bot you created during setup.
1. Dans le **champ d’adresse** du point de terminaison bot, entrez l’URL ngrok (par exemple, ) où vous hébergez le bot et y `https://468b9ab725e9.ngrok.io` `/api/messages` appendez-le.

   Votre bot sera en mesure de gérer les requêtes dans votre extension de messagerie.

## <a name="5-build-and-run-your-app"></a>5. Créer et exécuter votre application

Vous avez configuré une URL pour héberger votre extension de messagerie et configurée pour gérer les recherches. Il est temps de rendre votre application opérationnel.

1. Ouvrez le terminal et allez dans le répertoire racine de votre projet d’application.
1. Exécutez `npm install`.
1. Exécutez `npm start`.

   Si l’opération réussit, le message suivant indique que votre service d’extension de messagerie est à l’écoute de l’activité sur votre `localhost` :

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Chargement d’une version de version de votre extension de messagerie dans Teams

Une fois votre extension de messagerie en cours d’exécution, vous pouvez l’installer dans Teams.

> [!TIP]
> Si vous n’avez pas chargé une version de version Teams’application avant et que vous avez des problèmes, suivez ces [instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. Dans Visual Studio Code, sélectionnez la **touche F5** pour lancer un client Teams web.
1. Dans la boîte de dialogue d’installation de l’application, **sélectionnez Ajouter pour moi.**

## <a name="7-test-your-messaging-extension"></a>7. Tester votre extension de messagerie

Découvrez comment fonctionnent les extensions de messagerie dans Teams conversation instantanée.

1. Démarrez une nouvelle conversation. Dans la zone de composition, sélectionnez **Plus** et sélectionnez l’application d’extension de messagerie :::image type="icon" source="../assets/icons/teams-client-more.png"::: que vous avez chargé de côté.
1. Essayez de rechercher quelque chose (par exemple, **Tickets).** Si votre application fonctionne, vous verrez des exemples de résultats de recherche (vous pourrez en ajouter d’autres ultérieurement).

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Capture d’écran montrant comment une extension de messagerie basée sur la recherche est utilisée dans la Teams de composition.":::

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous aider si vous avez des problèmes lors de la réalisation de ce didacticiel.

**Le bot n’est pas connecté à Teams**

Si vous avez installé votre application, mais qu’elle ne fonctionne pas, assurez-vous que le bot de l’extension de messagerie est connecté au canal Teams [ *azure* Bot Service.](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Il est important de comprendre que ce n’est pas le même qu’un canal dans Teams. Dans ce cas, un canal est la façon dont azure Bot Service connecte votre bot à Teams ou à une autre application de communication microsoft ou [tierce prise en charge.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)

## <a name="see-also"></a>Voir aussi

* [Teams de composition ou de commande](../messaging-extensions/what-are-messaging-extensions.md) 
* [Inclure une fonctionnalité de déploiement de lien](../messaging-extensions/how-to/link-unfurling.md)
* [Instructions de conception](../messaging-extensions/design/messaging-extension-design.md) 
* [Modèles d’interface utilisateur prêts pour la production](../concepts/design/design-teams-app-ui-templates.md) 
* [Ajouter une authentification](../messaging-extensions/how-to/add-authentication.md)
* [Créer une extension de messagerie basée sur une action](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)

## <a name="next-steps"></a>Prochaines étapes

> [!div class="nextstepaction"]
> [Définir les commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [Répondre aux recherches des utilisateurs](../messaging-extensions/how-to/search-commands/respond-to-search.md)
