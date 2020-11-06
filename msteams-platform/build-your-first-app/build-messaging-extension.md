---
title: Prise en main-créer une extension de messagerie
author: heath-hamilton
description: Créez rapidement une extension de messagerie Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 160878d92969d57680e6fa25eb6fc13e82bf2a82
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931749"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>Créer une extension de messagerie pour Microsoft teams

Il existe deux types d’extensions de *messagerie* d’application teams : [commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) et [commandes d’action](../messaging-extensions/how-to/action-commands/define-action-command.md).

Dans cette leçon, vous allez créer une *commande de recherche* (également appelée *extension de messagerie basée sur la recherche* ), qui est un raccourci permettant de trouver du contenu externe et de le partager dans Teams. Les utilisateurs peuvent accéder aux commandes de recherche à partir de la [zone de composition ou de commande teams](../messaging-extensions/what-are-messaging-extensions.md).

## <a name="your-assignment"></a>Votre affectation

Le service d’assistance de votre organisation communique avec les utilisateurs par le biais de teams, mais les tickets se trouvent dans un système distinct. Cela signifie que le personnel de support technique doit constamment basculer entre les applications. Vous allez examiner la manière dont vous pouvez réduire ce pourcentage de changement de contexte en créant une simple extension de messagerie basée sur la recherche pour Teams.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application et un bot d’extension de messagerie à l’aide de Microsoft teams Toolkit pour Visual Studio code
> * Identifier les configurations des applications et une partie de la structure relative aux extensions de messagerie
> * Héberger une application localement
> * Configurer le bot pour votre extension de messagerie
> * Chargement et test d’une extension de messagerie dans teams

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).

## <a name="1-create-your-app-project"></a>1. créer votre projet d’application

Microsoft teams Toolkit vous permet de configurer les composants suivants pour votre extension de messagerie :

* **Configurations d’application et génération de modèles d’application concernant les** extensions de messagerie
* **Robot** de votre extension de messagerie enregistré automatiquement avec le service Microsoft Azure bot

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez extension de **messagerie** , puis **suivant**.
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Dans l’écran **configurer l’extension de messagerie** , procédez comme suit :
    1. Choisissez uniquement l’option **basée sur la recherche** pour le type d’extension de messagerie.
    1. Sélectionnez **créer un robot** , puis **inscrire un bot**. Si elle réussit, votre nouveau Bot aura un statut **enregistré** .
    1. Pour le moment, sélectionnez **non** pour l’option lien unfurling.
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.

## <a name="2-identify-relevant-app-project-components"></a>2. identifier les composants de projet d’application pertinents

La plupart des configurations et des modèles d’application sont configurés automatiquement lorsque vous créez votre projet à l’aide de Team Toolkit.

### <a name="app-configurations"></a>Configurations d’application

Pour afficher ou mettre à jour les configurations de votre extension de messagerie, sélectionnez **app Studio** dans la boîte à outils et accédez à **extensions de messagerie**.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

La génération de modèles automatique de l’application fournit un `botActivityHandler.js` fichier, situé dans le répertoire racine de votre projet, pour la gestion de la façon dont votre extension de messagerie (ou techniquement, le [bot de l’extension de messagerie](#4-configure-the-bot-for-your-messaging-extension)) répond aux requêtes de recherche dans Teams.

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre extension de messagerie sur un serveur Web local (port 3978).

1. Si vous ne l’avez pas encore fait, installez [ngrok](https://ngrok.com/download).
1. Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .
1. Copiez l’URL HTTPs dans la sortie (par exemple, `https://468b9ab725e9.ngrok.io` ) puisque teams requiert des connexions HTTPS.

Avec cette URL, Teams (qui requiert des connexions HTTPs) peut être utilisé pour effectuer un tunnel vers l’endroit où vous hébergez votre application ( `localhost` sur le port 3978).

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. configurer le bot pour votre extension de messagerie

Les extensions de messagerie s’appuient sur les robots pour envoyer et traiter les demandes des utilisateurs de teams vers votre service hébergé. Le bot doit être enregistré avec le service Azure bot, qui a été créé lors de la configuration de votre application à l’aide du kit de outils Teams.

Vous devez toujours spécifier une URL de point de terminaison de bot pour recevoir et traiter des requêtes de recherche dans votre extension de messagerie. En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` : Vous pouvez le configurer rapidement dans la boîte à outils.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. Accédez à **robots > inscriptions de robots existantes** et sélectionnez le robot que vous avez créé lors de l’installation.
1. Dans le champ **adresse du point de terminaison de robot** , entrez l’URL ngrok (par exemple, `https://468b9ab725e9.ngrok.io` ) où vous hébergez le bot et ajoutez `/api/messages` -y.

Votre robot pourra gérer les requêtes dans votre extension de messagerie.

## <a name="5-build-and-run-your-app"></a>5. générez et exécutez votre application

Vous avez configuré une URL pour héberger votre extension de messagerie et la configurer pour qu’elle gère les recherches. Il est temps de faire fonctionner votre application.

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` .

Si elle réussit, vous voyez le message suivant indiquant que votre service d’extension de messagerie est à l’écoute de l’activité `localhost` :

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. chargement votre extension de messagerie dans teams

Une fois que votre extension de messagerie est en cours d’exécution, vous pouvez l’installer dans Teams.

> [!TIP]
> Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).

1. Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.
1. Dans la boîte de dialogue d’installation de l’application, sélectionnez **Ajouter pour moi**.

## <a name="7-test-your-messaging-extension"></a>7. tester votre extension de messagerie

Découvrez comment fonctionnent les extensions de messagerie dans une conversation Teams.

1. Démarrez une nouvelle conversation. Dans la zone de composition, sélectionnez **plus** , :::image type="icon" source="../assets/icons/teams-client-more.png"::: puis choisissez l’application de l’extension de messagerie que vous venez de versions test chargées.
1. Essayez de rechercher un article (par exemple, **tickets** ). Si votre application fonctionne, vous verrez des exemples de résultats de recherche (vous pouvez ajouter votre propre version ultérieure).<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Capture d’écran illustrant l’utilisation d’une extension de messagerie basée sur la recherche dans la zone de composition de teams.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’une extension de messagerie teams de base qui est configurée pour rechercher du contenu externe dans la zone de composition ou de commande.

## <a name="next-steps"></a>Étapes suivantes

Consultez les pages suivantes pour continuer et créer une extension de messagerie complète :

1. [Définir des commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) pertinentes pour votre service.
1. Configurez votre service pour [répondre aux recherches des utilisateurs](../messaging-extensions/how-to/search-commands/respond-to-search.md).

## <a name="troubleshooting"></a>Résolution des problèmes

Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.

### <a name="bot-isnt-connected-to-teams"></a>Le bot n’est pas connecté à teams

Si vous avez installé votre application, mais qu’elle ne fonctionne pas, vérifiez que le robot de l’extension de messagerie est [connecté au *canal* teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).

Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams. Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).

## <a name="learn-more"></a>En savoir plus

* [Inclure une fonctionnalité de unfurling de liens](../messaging-extensions/how-to/link-unfurling.md)
* [Ajouter une authentification](../messaging-extensions/how-to/add-authentication.md)
* [Créer une extension de messagerie basée sur une action](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft bot Framework](https://dev.botframework.com/)
