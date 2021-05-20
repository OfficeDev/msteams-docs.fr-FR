---
title: Démarrer - Construire une extension de messagerie
author: girliemac
description: Créez rapidement une extension de messagerie Microsoft Teams en utilisant le Microsoft Teams Shared Computer Toolkit.
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

Il existe deux types *d’extensions* Teams messagerie : les [commandes de recherche et les](../messaging-extensions/how-to/search-commands/define-search-command.md) commandes [d’action](../messaging-extensions/how-to/action-commands/define-action-command.md).

Ce tutoriel vous apprend à créer une commande *de recherche* (également connu sous le nom *d’extension de messagerie basée sur la* recherche), qui est un raccourci pour trouver du contenu externe et le partager dans Teams. Les utilisateurs peuvent accéder aux commandes de recherche à partir de Teams composez ou commandez la boîte.

## <a name="what-youll-learn"></a>Ce que vous apprendrez

* Créez un projet d’application et un bot d’extension de messagerie en utilisant Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.
* Comprendre les configurations de l’application et l’échafaudage pertinent pour les extensions de messagerie.
* Hébergez une application localement.
* Configurez le bot pour votre extension de messagerie.
* Chargez latéralement et testez une extension de messagerie dans Teams.

## <a name="prerequisites"></a>Configuration requise

Assurez-vous de bien comprendre comment configurer et construire une application Teams simple. Pour plus d’informations, [consultez la première Microsoft Teams application « Hello, World! »](../build-your-first-app/build-and-run.md).

## <a name="1-create-your-app-project"></a>1. Créez votre projet d’application

Le Microsoft Teams Shared Computer Toolkit vous aide à configurer les composants suivants pour votre extension de messagerie :

* **Configurations d’applications et échafaudages** pertinents pour les extensions de messagerie.
* **Bot** pour votre extension de messagerie qui est automatiquement enregistrée auprès du Microsoft Azure Bot Service.

**Pour créer votre projet d’application**

1. Dans Visual Studio Code, sélectionnez **Microsoft Teams la** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: barre d’activité gauche et **choisissez Créer une nouvelle application Teams.**
1. Lorsque cela est demandé, connectez-vous à votre compte Microsoft 365 développement de votre entreprise.
1. Sur **l’écran du** projet Select, **à messaging extensions**  >  **search**, cliquez **sur JS (JavaScript)**. 
1. Entrez un nom pour votre application Teams’argent. Il s’agit du nom par défaut de votre application et aussi du nom de l’annuaire du projet d’application sur votre machine locale.
1. Sélectionnez **Créer un nouveau bot, puis** cliquez sur Créer le bouton **d’enregistrement** bot. En cas de succès, votre nouveau bot aura un *statut* enregistré. Maintenant, votre bot est automatiquement enregistré auprès du Microsoft Azure Bot Service. 
1. Sélectionnez **Finition** en bas de l’écran pour configurer votre projet et enregistrer votre projet sur votre machine locale.

## <a name="2-understand-your-app-project-components"></a>2. Comprendre les composants de votre projet d’application

Une grande partie des configurations d’applications et des échafaudages sont mis en place automatiquement lorsque vous créez votre projet avec Teams Shared Computer Toolkit.

* Configurations d’applications : Pour afficher ou mettre à jour les configurations de votre extension de messagerie, **sélectionnez App Studio dans** la boîte à outils et passez aux **extensions messagerie.**
* Échafaudage de l’application : L’échafaudage de l’application fournit un fichier, situé dans l’annuaire racine de votre projet, pour gérer la façon dont votre `botActivityHandler.js` extension de messagerie (ou techniquement, [le bot de l’extension de](#4-configure-the-bot-for-your-messaging-extension)messagerie) répond aux requêtes de recherche en Teams.

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Configurer un tunnel sécurisé vers votre application

À des fins de test, hébergeons votre extension de messagerie sur un serveur Web local (port 3978). Vous allez utiliser [ngrok pour mettre](https://ngrok.com/download) en place un tunnel sécurisé à localhost. Voir [construire votre premier bot pour plus de Microsoft Teams détails.](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) 

1. Si vous n’avez pas déjà, [installez ngrok](https://ngrok.com/download).
1. Dans un terminal, exécuter `ngrok http -host-header=rewrite 3978` .
1. Copiez l’URL HTTPS dans la sortie (par exemple, `https://468b9ab725e9.ngrok.io` ) car il Teams nécessite des connexions HTTPS.

   Avec cette URL, Teams (qui nécessite des connexions HTTPS) sera en mesure tunnel à l’endroit où vous hébergez votre application `localhost` (sur le port 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. Configurez le bot pour votre extension de messagerie

Les extensions de messagerie s’appuient sur les bots pour envoyer et traiter les demandes des utilisateurs Teams à votre service hébergé. Le bot doit être enregistré auprès du Service Bot Azure, qui a été réalisé lorsque vous configurez votre application en utilisant le Teams Shared Computer Toolkit.

Vous devez toujours spécifier une URL de point de terminaison bot pour recevoir et traiter les requêtes de recherche dans votre extension de messagerie. En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à . Vous pouvez configurer cela rapidement dans la boîte à outils.

1. Dans Visual Studio Code, sélectionnez **Microsoft Teams barre** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: d’activité gauche et choisissez **Open Microsoft Teams Shared Computer Toolkit**.
1. Allez sur **Bots > enregistrements de bot existants et sélectionnez** le bot que vous avez créé lors de la configuration.
1. Dans le **champ d’adresses bot,** entrez l’URL ngrok (par exemple, `https://468b9ab725e9.ngrok.io` ) où vous hébergez le bot et `/api/messages` annexez-le.

   Votre bot sera en mesure de traiter les requêtes dans votre extension de messagerie.

## <a name="5-build-and-run-your-app"></a>5. Créez et exécutez votre application

Vous avez configuré une URL pour héberger votre extension de messagerie et l’avez configurée pour gérer les recherches. Il est temps de mettre votre application en marche.

1. Ouvrez le terminal et allez à l’annuaire racine de votre projet d’application.
1. Exécutez `npm install`.
1. Exécutez `npm start`.

   En cas de succès, vous voyez le message suivant indiquant que votre service d’extension de messagerie est à l’écoute de l’activité à votre `localhost` :

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Chargez latéralement votre extension de messagerie dans Teams

Avec votre extension de messagerie en cours d’exécution, vous pouvez l’installer Teams.

> [!TIP]
> Si vous n’avez pas déchargé une application Teams avant et que vous ne vous êtes pas aperçu de problèmes, suivez [ces instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. Dans Visual Studio Code, sélectionnez **la clé F5** pour lancer un client web Teams et spécial.
1. Dans le dialogue d’installation de l’application, **sélectionnez Ajouter pour moi**.

## <a name="7-test-your-messaging-extension"></a>7. Testez votre extension de messagerie

Découvrez comment fonctionnent les extensions de messagerie dans un chat Teams’eau.

1. Commencez une nouvelle conversation. Dans la boîte de composition, sélectionnez **Plus et** :::image type="icon" source="../assets/icons/teams-client-more.png"::: sélectionnez l’application d’extension de messagerie que vous venez de sideloaded.
1. Essayez de chercher quelque chose (par exemple, **billets).** Si votre application fonctionne, vous verrez des résultats de recherche d’échantillons (vous pouvez ajouter le vôtre plus tard).

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Une capture d’écran montrant comment une extension de messagerie basée sur la recherche est utilisée dans Teams la boîte.":::

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous aider si vous avez eu des problèmes pour terminer ce tutoriel.

**Bot n’est pas connecté à Teams**

Si vous avez installé votre application mais qu’elle ne fonctionne pas, assurez-vous que le bot de l’extension de messagerie [est connecté au canal de messagerie du service Teams Azure Bot . ](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Il est important de comprendre que ce n’est pas la même chose qu’un canal dans Teams. Dans ce cas, un canal est la façon dont le Service Bot Azure connecte votre bot à Teams ou une autre application de [communication Microsoft ou tierce prise en charge](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="see-also"></a>Voir aussi

* [Teams composez ou commandez la boîte](../messaging-extensions/what-are-messaging-extensions.md) 
* [Inclure une fonction de déploiement de lien](../messaging-extensions/how-to/link-unfurling.md)
* [Instructions de conception](../messaging-extensions/design/messaging-extension-design.md) 
* [Modèles d’interface utilisateur prêts à la production](../concepts/design/design-teams-app-ui-templates.md) 
* [Ajouter une authentification](../messaging-extensions/how-to/add-authentication.md)
* [Créer une extension de messagerie basée sur l’action](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Définir les commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [Répondre aux recherches des utilisateurs](../messaging-extensions/how-to/search-commands/respond-to-search.md)
