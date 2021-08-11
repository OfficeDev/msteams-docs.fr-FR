---
title: Tester et déboguer votre bot localement
author: surbhigupta
description: Test et débogage de votre bot localement avec un IDE
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 5774833806940fcd4a2cc771687ecfcd9126c835582f71c21f26b92314a1df40
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706315"
---
# <a name="test-and-debug-your-bot-locally"></a>Tester et déboguer votre bot localement

Lorsque vous testez votre bot, vous devez prendre en compte les contextes dans lequel vous souhaitez que votre bot s’exécute, ainsi que les fonctionnalités que vous avez peut-être ajoutées à votre bot qui nécessitent des données spécifiques à Microsoft Teams. Assurez-vous que la méthode que vous choisissez pour tester votre bot s’aligne sur ses fonctionnalités.

## <a name="test-by-uploading-to-teams"></a>Testez en chargeant vers Teams

La façon la plus complète de tester votre bot consiste à créer un package d’application et à le télécharger sur Teams. Il s’agit de la seule méthode pour tester les fonctionnalités complètes disponibles pour votre bot, dans toutes les étendues.

Il existe deux méthodes pour charger votre application :
* Utilisez [App Studio.](~/concepts/build-and-test/app-studio-overview.md)
* [Créez un package d’application](~/concepts/build-and-test/apps-package.md) manuellement, puis [téléchargez votre application.](~/concepts/deploy-and-publish/apps-upload.md)

> [!NOTE]
> Si vous avez besoin de modifier votre manifeste et de retélé télécharger votre application, vous devez supprimer votre [bot](#delete-a-bot-from-teams) avant de télécharger votre package d’application modifié.

## <a name="debug-your-bot-locally"></a>Déboguer votre bot localement

Si vous hébergez votre bot localement pendant le développement, vous devez utiliser un service de tunneling comme [ngrok](https://ngrok.com/) pour tester votre bot. Après avoir téléchargé et installé ngrok, ajoutez votre chemin d’accès et exécutez la commande suivante pour démarrer `ngrok` le service de tunneling :

```bash
ngrok http <port> -host-header=localhost:<port>
```

Utilisez le point de terminaison https fourni par ngrok dans le manifeste de votre application. 

> [!NOTE]
> Si vous fermez votre fenêtre de commande et redémarrez, une nouvelle URL est générée et vous devez mettre à jour l’adresse de votre point de terminaison du bot pour l’utiliser.

## <a name="test-your-bot-without-uploading-to-teams"></a>Testez votre bot sans télécharger vers Teams

Parfois, il peut être nécessaire de tester votre bot sans l’installer en tant qu’application dans Teams. Nous fournissons deux méthodes pour tester le bot. Il peut être utile de tester votre bot sans l’installer en tant qu’application pour vous assurer qu’il est disponible et de répondre. Toutefois, il ne vous permettra pas de tester l’ensemble des fonctionnalités Microsoft Teams que vous avez peut-être ajoutées à votre bot. Si vous avez besoin de tester entièrement votre bot, consultez [les tests en chargeant](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utiliser le bot Emulator

Le Bot Framework Emulator est une application de bureau qui permet aux développeurs de bots de tester et déboguer leurs bots localement ou à distance. L’émulateur vous permet de discuter avec votre bot et d’inspecter les messages qu’il envoie et reçoit. Cela peut être utile pour vérifier que votre bot est disponible et y répondre. Toutefois, l’émulateur ne vous permet pas de tester les fonctionnalités spécifiques à Teams que vous avez ajoutées au bot, ni les réponses de votre bot ne sont une représentation visuelle précise de leur rendu dans Teams. Si vous devez tester l’un de ces éléments, il est préférable de [télécharger votre bot.](#test-by-uploading-to-teams)

Pour plus d’informations, [voir les instructions complètes sur le Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Parlez directement à votre bot par ID

> [!Important]
> Le fait de parler à votre bot par ID est destiné uniquement à des fins de test de base. Les Teams fonctionnalités spécifiques que vous avez ajoutées à votre bot ne fonctionnent pas.

Vous pouvez également initier une conversation avec votre bot à l’aide de son ID. Lorsqu’un bot a été ajouté via l’une de ces méthodes, il n’est pas adressaçable dans les conversations de canal et vous ne pouvez pas tirer parti des autres fonctionnalités d’application Microsoft Teams telles que les onglets ou les extensions de messagerie. Vous pouvez initier une conversation de l’une des manières suivantes :

* Dans la page [Tableau de bord](https://dev.botframework.com/bots) du bot de votre bot, sous **Canaux,** **sélectionnez** Ajouter à Microsoft Teams . Microsoft Teams lance une conversation personnelle avec votre bot.

* Référencez directement l’ID d’application de votre bot à partir de Microsoft Teams :
   1. Dans la page [Tableau de bord](https://dev.botframework.com/bots) du bot de votre bot, sous **Détails,** copiez l’ID d’application **Microsoft** de votre bot.
  
      ![Obtention de l’AppID pour le bot](~/assets/images/bots_appid_botframework.png)
  
   2. Ouvrez Microsoft Teams, dans **le** volet De conversation, sélectionnez l’icône Ajouter **une conversation.** Dans **:**, collez l’ID d’application Microsoft de votre bot.
  
      ![Téléchargement de bots](~/assets/images/bots_uploading.png)

      L’ID d’application doit être résolu en nom de bot.

   3. Sélectionnez votre bot et envoyez un message pour lancer une conversation.
      Vous pouvez également coller l’ID d’application de votre bot dans la zone de recherche en haut à gauche dans Microsoft Teams. Dans la page des résultats de la recherche, accédez à l’onglet **Personnes** pour voir votre bot et commencer à discuter avec celui-ci.

Votre bot reçoit l’événement lorsque vous ajoutez les bots à une équipe, sans les informations de `conversationUpdate` l’équipe dans `channelData` l’objet.

## <a name="block-a-bot-in-personal-chat"></a>Bloquer un bot dans une conversation personnelle

Les utilisateurs peuvent choisir d’empêcher votre bot d’envoyer des messages de conversation personnels. Ils peuvent le faire en cliquant avec le bouton droit sur votre bot dans le canal de conversation et en choisissant Bloquer **la conversation du bot.** Cela signifie que vos bots continuent d’envoyer des messages, mais que l’utilisateur ne les reçoit pas.

![Blocage d’un bot](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>Supprimer un bot d’une équipe

Les utilisateurs peuvent supprimer le bot en choisissant l’icône de corbeille dans la liste des bots dans l’affichage de leur équipe. Cela supprime uniquement le bot de l’utilisation de cette équipe, les utilisateurs individuels peuvent toujours interagir dans un contexte personnel. Les bots dans un contexte personnel ne peuvent pas être désactivés ou supprimés par les utilisateurs.

## <a name="disable-a-bot-in-teams"></a>Désactiver un bot dans Teams

Pour empêcher votre bot de recevoir des messages, go to your **Bot Dashboard** and edit the Microsoft Teams channel. Clear the **Enable on Microsoft Teams** option. Cela empêche les utilisateurs d’interagir avec le bot, mais il sera toujours découvrable et les utilisateurs pourront toujours l’ajouter à Teams.

## <a name="delete-a-bot-from-teams"></a>Supprimer un bot d’Teams

Pour supprimer complètement votre bot de Teams, go to your **Bot Dashboard** and edit the Microsoft Teams channel. Sélectionnez **le bouton** Supprimer en bas. Cela empêche les utilisateurs de découvrir, d’ajouter et d’interagir avec votre bot. Cela ne supprime pas le bot des instances de Teams d’autres utilisateurs, mais il cesse également de fonctionner pour eux.

## <a name="see-also"></a>Voir aussi

* [Déboguer votre robot avec inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware)
* [Déboguer votre robot d’appel et de réunion localement](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
