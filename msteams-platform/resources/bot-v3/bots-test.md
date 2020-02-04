---
title: Tester et déboguer votre robot
description: Décrit comment tester les robots dans Microsoft teams
keywords: test des robots teams
ms.date: 03/20/2019
ms.openlocfilehash: bb376b1c122b367c9fe74357751459f053d3d44b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673840"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Test et débogage de votre robot Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Lors du test de votre robot, vous devez prendre en compte à la fois le ou les contexte (s) dans lequel vous souhaitez que votre bot s’exécute, ainsi que toutes les fonctionnalités que vous avez peut-être ajoutées à votre bot et qui nécessitent des données spécifiques à Microsoft Teams. Assurez-vous que la méthode que vous avez choisie pour tester votre bot s’aligne sur ses fonctionnalités.

## <a name="test-by-uploading-to-teams"></a>Tester en téléchargeant vers teams

La façon la plus complète de tester votre bot est de créer un package d’application et de le charger dans Teams. Il s’agit de la seule méthode permettant de tester toutes les fonctionnalités disponibles pour votre bot, sur toutes les étendues.

Il existe deux méthodes pour télécharger votre application. Vous pouvez utiliser [app Studio](~/concepts/build-and-test/app-studio-overview.md) pour vous aider, ou vous pouvez créer manuellement [un package d’application](~/concepts/build-and-test/apps-package.md) et [charger votre application](~/concepts/deploy-and-publish/apps-upload.md). Si vous avez besoin de modifier votre manifeste et de recharger votre application, vous devez [supprimer votre robot](#deleting-a-bot-from-teams) avant de télécharger votre package d’application modifié.

## <a name="debug-your-bot-locally"></a>Débogage de votre bot localement

Si vous hébergez votre robot localement lors du développement, vous devez utiliser un service de tunneling comme [ngrok](https://ngrok.com/) afin de tester votre robot. Une fois que vous avez téléchargé et installé ngrok, exécutez la commande ci-dessous pour démarrer le service de tunneling (il se peut que vous deviez ajouter ngrok à votre chemin d’accès).

```bash
ngrok http <port> -host-header=localhost:<port>
```

Utilisez le point de terminaison HTTPS fourni par ngrok dans le manifeste de votre application. Si vous fermez votre fenêtre de commande et que vous redémarrez, vous obtiendrez une nouvelle URL et vous devrez mettre à jour votre adresse de point de terminaison de robot pour l’utiliser également.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Test de votre robot sans chargement vers teams

Parfois, il peut s’avérer nécessaire de tester votre robot sans l’installer en tant qu’application dans Teams. Nous proposons deux méthodes pour effectuer cette opération ci-dessous. Le test de votre robot sans l’installer en tant qu’application peut être utile pour garantir la disponibilité et la réponse de votre robot, mais il ne vous permet pas de tester la gamme complète des fonctionnalités de Microsoft teams que vous avez peut-être ajoutées à votre bot. Si vous avez besoin de tester entièrement votre robot, suivez les instructions de [test en le téléchargeant](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utiliser l’émulateur bot

L’émulateur de l’infrastructure bot est une application de bureau qui permet aux développeurs de robots de tester et de déboguer leurs robots, localement ou à distance. À l’aide de l’émulateur, vous pouvez converser avec votre robot et inspecter les messages que votre robot envoie et reçoit. Cela peut être utile pour vérifier que votre robot est disponible et qu’il répond, mais que l’émulateur ne vous permet pas de tester les fonctionnalités propres à teams que vous avez ajoutées à votre bot, ni les réponses de votre bot à une représentation visuelle précise de la façon dont ils vont être affichés dans Teams. Si vous avez besoin de tester l’un de ces éléments, il est préférable de [charger votre bot](#test-by-uploading-to-teams).

Vous trouverez des instructions complètes sur l’émulateur de l’infrastructure bot [ici](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0).

### <a name="talk-to-your-bot-directly-by-id"></a>Parler directement à votre bot par ID

>[!Important]
>Le fait de parler à votre bot par ID est destiné uniquement à des fins de test.

Vous pouvez également démarrer une conversation avec votre robot à l’aide de son ID. Deux méthodes sont indiquées ci-dessous. Lorsqu’un bot a été ajouté par le biais de l’une de ces méthodes, il ne sera pas adressable dans les conversations de canal, et vous ne pouvez pas tirer parti d’autres fonctionnalités d’applications Microsoft teams telles que les onglets ou les extensions de messagerie.

1. Sur la page du [tableau de bord du bot](https://dev.botframework.com/bots) de votre robot, sous **canaux**, sélectionnez **Ajouter à Microsoft teams**. Microsoft teams s’ouvre avec une conversation personnelle avec votre robot.
2. Référencez directement l’ID d’application de votre robot à partir de Microsoft teams :
   * Sur la page du [tableau de bord du bot](https://dev.botframework.com/bots) de votre robot, sous **Détails**, copiez l' **ID d’application Microsoft** de votre robot.
  
     ![Obtention de l’AppID pour le bot](~/assets/images/bots_appid_botframework.png)
  
   * À partir de Microsoft Teams, dans le volet **conversation** , sélectionnez l’icône **Ajouter une conversation** . Pour **:**, collez l’ID d’application Microsoft de votre robot.
  
     ![Obtention de l’AppID pour le bot](~/assets/images/bots_uploading.png)

     L’ID de l’application doit correspondre au nom de votre bot.

   * Sélectionnez votre robot et envoyez un message pour lancer une conversation.
   * Vous pouvez également coller l’ID de l’application de votre robot dans la zone de recherche située en haut à gauche de Microsoft Teams. Dans la page des résultats de la recherche, accédez à l’onglet personnes pour voir votre bot et commencer à la discuter.

Votre bot reçoit l' `conversationUpdate` événement comme les robots ajoutés à une équipe, mais sans les informations d’équipe dans l' `channelData` objet.

## <a name="blocking-a-bot-in-personal-chat"></a>Blocage d’un bot dans une conversation personnelle

Notez que les utilisateurs peuvent choisir de bloquer votre robot pour envoyer des messages de conversation personnelle. Ils peuvent le faire en cliquant avec le bouton droit de la souris sur votre bot dans le canal de conversation et en choisissant **bloquer la conversation de robot**. Cela signifie que vos robots continueront à envoyer des messages, mais l’utilisateur ne recevra pas ces messages.

![Blocage d’un bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Suppression d’un bot d’une équipe

Les utilisateurs peuvent supprimer le bot en sélectionnant l’icône de la corbeille dans la liste des robots dans leur affichage Teams. Notez que cette opération ne supprime que le bot de l’utilisation de l’équipe ; les utilisateurs individuels pourront toujours interagir dans le contexte personnel.

Les robots dans le contexte personnel ne peuvent pas être désactivés ou supprimés par un utilisateur, mais il est possible de supprimer complètement le robot de teams.

## <a name="disabling-a-bot-in-teams"></a>Désactivation d’un bot dans teams

Pour arrêter la réception de messages, accédez au tableau de bord de votre bot et modifiez le canal Microsoft Teams. Désactivez l’option **activer sur Microsoft teams** . Cela empêche les utilisateurs d’interagir avec le bot, mais il pourra toujours être découvert et les utilisateurs pourront toujours l’ajouter à Teams.

## <a name="deleting-a-bot-from-teams"></a>Suppression d’un bot de teams

Pour supprimer complètement votre bot de teams, accédez au tableau de bord de votre bot et modifiez le canal Microsoft Teams. Cliquez sur le bouton **supprimer** en bas. Cela empêche les utilisateurs de découvrir, d’ajouter ou d’interagir avec votre robot. Notez que cette opération ne supprime pas le bot des instances d’autres utilisateurs de teams, bien qu’il ne fonctionnera pas également.

## <a name="removing-your-bot-from-appsource"></a>Suppression de votre robot de AppSource

Si vous souhaitez supprimer votre bot de votre application teams dans AppSource (anciennement Office Store), vous devez supprimer le bot de votre manifeste de l’application et renvoyer votre application pour validation. Pour plus d’informations, reportez-vous [à publier votre application Microsoft teams vers AppSource](~/concepts/deploy-and-publish/apps-publish.md) .
