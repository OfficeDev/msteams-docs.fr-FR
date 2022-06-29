---
title: Tester et déboguer votre bot localement
author: surbhigupta
description: En savoir plus sur le test et le débogage de votre bot localement avec un IDE dans l’environnement Teams via le chargement indépendant et bien plus encore
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 3e1225991ad240f74e045a6941002b9eb7b5e81d
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503717"
---
# <a name="test-and-debug-your-bot-locally-with-ide"></a>Tester et déboguer votre bot localement avec l’IDE

Lors du test de votre bot, vous devez prendre en compte à la fois les contextes dans lesquels vous souhaitez que votre bot s’exécute et toutes les fonctionnalités que vous avez ajoutées à votre bot qui nécessitent des données spécifiques à Microsoft Teams. Assurez-vous que la méthode que vous choisissez pour tester votre bot s’aligne sur ses fonctionnalités.

## <a name="test-by-uploading-to-teams"></a>Tester en chargeant dans Teams

La méthode la plus complète pour tester votre bot consiste à créer un package d’application et à le charger dans Teams. Il s’agit de la seule méthode permettant de tester toutes les fonctionnalités disponibles pour votre bot, dans toutes les étendues.

Il existe deux méthodes pour charger votre application :

* Utilisez [App Studio](~/concepts/build-and-test/app-studio-overview.md).
* [Créer un package d’application](~/concepts/build-and-test/apps-package.md) manuellement, puis [charger votre application](~/concepts/deploy-and-publish/apps-upload.md).

> [!NOTE]
> Pour modifier le manifeste et charger à nouveau votre application, [supprimer le bot](#delete-a-bot-from-teams) avant de charger le package d’application modifié.
> Pour tester le bot, activez le chargement indépendant dans Teams. Consultez [activer le chargement indépendant](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

## <a name="debug-your-bot-locally"></a>Déboguer votre bot localement

Si vous hébergez votre bot localement pendant le développement, vous devez utiliser un service de tunnel comme [ngrok](https://ngrok.com/) afin de tester votre bot. Après avoir téléchargé et installé ngrok, ajoutez `ngrok` à votre chemin d’accès et exécutez la commande suivante pour démarrer le service de tunneling :

```bash
ngrok http <port> --host-header=localhost:<port>
```

Utilisez le point de terminaison https fourni par ngrok dans le manifeste de votre application.

> [!NOTE]
> Si vous fermez votre fenêtre de commande et redémarrez, une nouvelle URL est générée et vous devez mettre à jour l’adresse de votre point de terminaison de bot pour l’utiliser.

## <a name="test-your-bot-without-uploading-to-teams"></a>Tester votre bot sans le charger dans Teams

Parfois, il est nécessaire de tester votre bot sans l’installer en tant qu’application dans Teams. Nous fournissons deux méthodes pour tester le bot. Le test de votre bot sans l’installer en tant qu’application peut être utile pour vous assurer que votre bot est disponible et répond. Toutefois, cela ne vous permettra pas de tester l’étendue complète des fonctionnalités Microsoft Teams que vous avez ajoutées à votre bot. Si vous souhaitez tester entièrement votre bot, consultez [tester en téléchargeant des fichiers](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utiliser l’émulateur de bot

Le Bot Framework Emulator est une application de bureau qui permet aux développeurs de bots de tester et de déboguer leurs bots localement ou à distance. L’émulateur vous permet de discuter avec votre bot et d’inspecter les messages que votre bot envoie et reçoit. Cela est utile pour vérifier que votre bot est disponible et répond. Cependant, l’émulateur ne vous permet pas de tester les fonctionnalités spécifiques à Teams que vous avez ajoutées au bot, et les réponses de votre bot ne sont pas une représentation visuelle précise de la façon dont elles sont rendues dans Teams. Si vous avez besoin de tester l’un ou l’autre de ces éléments, il est préférable de [télécharger votre bot](#test-by-uploading-to-teams).

Pour plus d’informations, consultez [instructions complètes sur le Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Contactez votre bot directement par ID

> [!Important]
> La communication avec votre bot par ID est destinée uniquement à des fins de test de base. Les fonctionnalités spécifiques à Teams que vous avez ajoutées à votre bot ne fonctionnent pas.

Lancez une conversation avec votre bot à l’aide de son ID. Lorsqu’un bot est ajouté via l’une de ces méthodes, il n’est pas adressable dans les conversations de canal et vous ne pouvez pas tirer parti d’autres fonctionnalités d’application Teams telles que des onglets ou des extensions de message. Lancez une conversation de l’une des manières suivantes :

* Dans la page [tableau de bord du bot](https://dev.botframework.com/bots) pour votre bot, sous **Canaux**, sélectionnez **Ajouter à Microsoft Teams**. Teams lance une conversation personnelle avec votre bot.

* Référencez directement l’ID d’application de votre bot à partir de Teams :
   1. Dans la page du [tableau de bord du bot](https://dev.botframework.com/bots) pour votre bot, sous **Détails**, copiez **l’ID d’application Microsoft** pour votre bot.
  
      ![Obtention de l’AppID pour le bot](~/assets/images/bots_appid_botframework.png)
  
   2. Ouvrez Microsoft Teams, dans le volet **Conversation** , sélectionnez l’icône **Ajouter une conversation** . Dans **À :**, collez l’ID d’application Microsoft de votre bot.
  
      ![Chargement de bots](~/assets/images/bots_uploading.png)

      L’ID d’application doit correspondre au nom de votre bot.

   3. Sélectionnez votre bot et envoyez un message pour lancer une conversation.
      Vous pouvez également coller l’ID d’application de votre bot dans la zone de recherche en haut à gauche dans Teams. Dans la page des résultats de recherche, accédez à l’onglet **Personnes** pour voir votre bot et commencer à discuter avec lui.

> [!Note]
> Pour que Teams fasse référence à l’ID d’application de votre bot, activez le [chargement indépendant des applications](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

Votre bot reçoit l’événement `conversationUpdate` lorsque vous ajoutez les bots à une équipe, sans les informations de l’équipe dans l’objet `channelData`.

## <a name="block-a-bot-in-personal-chat"></a>Bloquer un bot dans une conversation personnelle

Les utilisateurs peuvent choisir d’empêcher votre bot d’envoyer des messages de conversation personnels. Ils peuvent activer/désactiver cette option en cliquant avec le bouton droit sur votre bot dans le canal de conversation et en choisissant **bloquer la conversation du bot**. Cela signifie que vos bots continuent à envoyer des messages, mais l’utilisateur ne reçoit pas les messages.

![Blocage d’un bot](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>Supprimer un bot d’une équipe

Les utilisateurs peuvent supprimer le bot en choisissant l’icône de corbeille dans la liste des bots dans l’affichage de leur équipe. Cela supprime uniquement le bot de l’utilisation de cette équipe. Les utilisateurs individuels peuvent toujours interagir dans un contexte personnel. Les bots dans un contexte personnel ne peuvent pas être désactivés ou supprimés par les utilisateurs.

## <a name="disable-a-bot-in-teams"></a>Désactiver un bot dans Teams

Pour empêcher votre bot de recevoir des messages, accédez à votre **tableau de bord** de bot et modifiez le canal Teams. Désactivez l’option **Activer sur Microsoft Teams**. Cela empêche les utilisateurs d’interagir avec le bot, cependant, il est toujours détectable et les utilisateurs peuvent l’ajouter à Teams.

## <a name="delete-a-bot-from-teams"></a>Supprimer un bot de Teams

Pour supprimer complètement votre bot de Teams, accédez à votre **tableau de bord de bot** et modifiez le canal Teams. Choisissez le bouton **Supprimer** en bas. Cela empêche les utilisateurs de découvrir, d’ajouter et d’interagir avec votre bot. Cela ne supprime pas le bot des instances Teams des autres utilisateurs, mais il cesse également de fonctionner pour eux.

## <a name="see-also"></a>Voir aussi

* [Déboguer votre robot avec inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware)
* [Déboguer votre robot d’appel et de réunion localement](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
