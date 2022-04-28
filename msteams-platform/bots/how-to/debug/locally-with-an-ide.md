---
title: Tester et déboguer votre bot localement
author: surbhigupta
description: Découvrez comment tester et déboguer votre bot localement avec un IDE dans Teams environnement via le chargement indépendant, en dehors de Teams à l’aide de l’émulateur bot et en parlant directement à votre bot.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a673f1cd260c9b53de477cdd5084bd521c79bd41
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103985"
---
# <a name="test-and-debug-your-bot-locally"></a>Tester et déboguer votre bot localement

Lors du test de votre bot, vous devez prendre en compte à la fois les contextes dans lesquels vous souhaitez que votre bot s’exécute et toutes les fonctionnalités que vous avez ajoutées à votre bot qui nécessitent des données spécifiques à Microsoft Teams. Assurez-vous que la méthode que vous choisissez de tester votre bot s’aligne sur ses fonctionnalités.

## <a name="test-by-uploading-to-teams"></a>Tester en chargeant sur Teams

La méthode la plus complète pour tester votre bot consiste à créer un package d’application et à le charger dans Teams. Il s’agit de la seule méthode permettant de tester toutes les fonctionnalités disponibles pour votre bot, dans toutes les étendues.

Il existe deux méthodes pour charger votre application :

* Utilisez [App Studio](~/concepts/build-and-test/app-studio-overview.md).
* [Créez un package d’application](~/concepts/build-and-test/apps-package.md) manuellement, puis [chargez votre application](~/concepts/deploy-and-publish/apps-upload.md).

> [!NOTE]
> Pour modifier le manifeste et charger à nouveau votre application, [supprimez le bot](#delete-a-bot-from-teams) avant de charger le package d’application modifié.
> Pour tester le bot, activez le chargement indépendant dans Teams. Voir [activer le chargement indépendant](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

## <a name="debug-your-bot-locally"></a>Déboguer votre bot localement

Si vous hébergez votre bot localement pendant le développement, vous devez utiliser un service de tunneling comme [ngrok](https://ngrok.com/) pour tester votre bot. Après avoir téléchargé et installé ngrok, ajoutez `ngrok` votre chemin d’accès et exécutez la commande suivante pour démarrer le service de tunneling :

```bash
ngrok http <port> -host-header=localhost:<port>
```

Utilisez le point de terminaison https fourni par ngrok dans le manifeste de votre application.

> [!NOTE]
> Si vous fermez votre fenêtre de commande et redémarrez, une nouvelle URL est générée et vous devez mettre à jour l’adresse du point de terminaison de votre bot pour l’utiliser.

## <a name="test-your-bot-without-uploading-to-teams"></a>Tester votre bot sans le charger dans Teams

Parfois, il peut être nécessaire de tester votre bot sans l’installer en tant qu’application dans Teams. Nous fournissons deux méthodes pour tester le bot. Le test de votre bot sans l’installer en tant qu’application peut être utile pour vous assurer que votre bot est disponible et répond, mais il ne vous permettra pas de tester l’étendue complète de Microsoft Teams fonctionnalités que vous avez peut-être ajoutées à votre bot. Si vous avez besoin de tester entièrement votre bot, consultez [le test en téléchargeant](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utiliser le bot Emulator

Le Bot Framework Emulator est une application de bureau qui permet aux développeurs de bots de tester et de déboguer leurs bots localement ou à distance. L’émulateur vous permet de discuter avec votre bot et d’inspecter les messages que votre bot envoie et reçoit. Cela peut être utile pour vérifier que votre bot est disponible et répondre. Toutefois, l’émulateur ne vous permet pas de tester les fonctionnalités spécifiques à Teams que vous avez ajoutées au bot, ni les réponses de votre bot sont une représentation visuelle précise de la façon dont elles sont affichées dans Teams. Si vous devez tester l’une de ces choses, il est préférable de [charger votre bot](#test-by-uploading-to-teams).

Pour plus d’informations, consultez [des instructions complètes sur le Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Communiquer directement avec votre bot par ID

> [!Important]
> La conversation avec votre bot par ID est destinée uniquement à des fins de test de base. Toutes les fonctionnalités spécifiques à Teams que vous avez ajoutées à votre bot ne fonctionnent pas.

Vous pouvez également lancer une conversation avec votre bot à l’aide de son ID. Lorsqu’un bot a été ajouté via l’une de ces méthodes, il n’est pas adressable dans les conversations de canal et vous ne pouvez pas tirer parti d’autres fonctionnalités d’application Microsoft Teams telles que les onglets ou les extensions de message. Vous pouvez lancer une conversation de l’une des manières suivantes :

* Dans la page [Tableau de bord](https://dev.botframework.com/bots) du bot de votre bot, sous **Canaux**, **sélectionnez Ajouter à Microsoft Teams**. Microsoft Teams lance une conversation personnelle avec votre bot.

* Référencez directement l’ID d’application de votre bot à partir de Microsoft Teams :
   1. Dans la page [Tableau de bord](https://dev.botframework.com/bots) du bot de votre bot, sous **Détails**, copiez **l’ID d’application Microsoft** pour votre bot.
  
      ![Obtention de l’ID d’application pour le bot](~/assets/images/bots_appid_botframework.png)
  
   2. Ouvrez Microsoft Teams, dans le volet **De** conversation, sélectionnez l’icône **Ajouter une conversation**. Dans **To:**, collez l’ID d’application Microsoft de votre bot.
  
      ![Chargement de bots](~/assets/images/bots_uploading.png)

      L’ID d’application doit être résolu en nom de bot.

   3. Sélectionnez votre bot et envoyez un message pour lancer une conversation.
      Vous pouvez également coller l’ID d’application de votre bot dans la zone de recherche en haut à gauche dans Microsoft Teams. Dans la page des résultats de la recherche, **accédez** à l’onglet Contacts pour voir votre bot et commencer à discuter avec lui.

> [!Note]
> Pour Microsoft Teams faire référence à l’ID d’application de votre bot, activez le [chargement indépendant des applications](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

Votre bot reçoit l’événement `conversationUpdate` lorsque vous ajoutez les bots à une équipe, sans les informations de l’équipe dans l’objet `channelData` .

## <a name="block-a-bot-in-personal-chat"></a>Bloquer un bot dans une conversation personnelle

Les utilisateurs peuvent choisir d’empêcher votre bot d’envoyer des messages de conversation personnels. Ils peuvent activer cette option en cliquant avec le bouton droit sur votre bot dans le canal de conversation et en choisissant **Bloquer la conversation du bot**. Cela signifie que vos bots continuent à envoyer des messages, mais l’utilisateur ne reçoit pas les messages.

![Blocage d’un bot](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a>Supprimer un bot d’une équipe

Les utilisateurs peuvent supprimer le bot en choisissant l’icône corbeille dans la liste des bots dans l’affichage de leur équipe. Cela supprime uniquement le bot de l’utilisation de cette équipe, les utilisateurs individuels peuvent toujours interagir dans un contexte personnel. Les bots dans un contexte personnel ne peuvent pas être désactivés ou supprimés par les utilisateurs.

## <a name="disable-a-bot-in-teams"></a>Désactiver un bot dans Teams

Pour empêcher votre bot de recevoir des messages, accédez à votre **tableau de bord** bot et modifiez le canal Microsoft Teams. Désactivez l’option **Activer sur Microsoft Teams**. Cela empêche les utilisateurs d’interagir avec le bot. Toutefois, il sera toujours détectable et les utilisateurs pourront toujours l’ajouter à Teams.

## <a name="delete-a-bot-from-teams"></a>Supprimer un bot de Teams

Pour supprimer complètement votre bot de Teams, accédez à votre **tableau de bord** bot et modifiez le canal Microsoft Teams. Choisissez le bouton **Supprimer** en bas. Cela empêche les utilisateurs de découvrir, d’ajouter et d’interagir avec votre bot. Cela ne supprime pas le bot des instances Teams d’autres utilisateurs, mais il cesse également de fonctionner pour eux.

## <a name="see-also"></a>Voir aussi

* [Déboguer votre robot avec inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware)
* [Déboguer votre robot d’appel et de réunion localement](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
