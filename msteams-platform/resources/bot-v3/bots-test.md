---
title: Tester et déboguer votre bot
description: Décrit comment tester des bots dans Microsoft Teams
keywords: Tests de bots teams
ms.topic: how-to
ms.date: 03/20/2019
ms.openlocfilehash: 6403d9ba16510860492735944899285058d9c0f3
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696604"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Tester et déboguer votre bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Lorsque vous testez votre bot, vous devez prendre en compte le ou les contextes dans lequel vous souhaitez que votre bot s'exécute, ainsi que les fonctionnalités que vous avez peut-être ajoutées à votre bot qui nécessitent des données spécifiques à Microsoft Teams. Assurez-vous que la méthode que vous avez choisie pour tester votre bot s'aligne sur ses fonctionnalités.

## <a name="test-by-uploading-to-teams"></a>Tester en chargeant teams

La façon la plus complète de tester votre bot consiste à créer un package d'application et à le télécharger dans Teams. Il s'agit de la seule méthode pour tester les fonctionnalités complètes disponibles pour votre bot, dans toutes les étendues.

Il existe deux méthodes pour charger votre application. Vous pouvez utiliser [App Studio](~/concepts/build-and-test/app-studio-overview.md) pour vous aider, ou vous pouvez créer manuellement un [package](~/concepts/build-and-test/apps-package.md) d'application et télécharger [votre application.](~/concepts/deploy-and-publish/apps-upload.md) Si vous avez besoin de modifier votre manifeste et de retélé télécharger votre application, vous devez supprimer votre [bot](#deleting-a-bot-from-teams) avant de télécharger votre package d'application modifié.

## <a name="debug-your-bot-locally"></a>Déboguer votre bot localement

Si vous hébergez votre bot localement pendant le développement, vous devez utiliser un service de tunneling comme [ngrok](https://ngrok.com/) pour tester votre bot. Une fois que vous avez téléchargé et installé ngrok, exécutez la commande ci-dessous pour démarrer le service de tunneling (vous devrez peut-être ajouter ngrok à votre chemin d'accès).

```bash
ngrok http <port> -host-header=localhost:<port>
```

Utilisez le point de terminaison https fourni par ngrok dans le manifeste de votre application. Si vous fermez votre fenêtre de commande et redémarrez, vous obtenez une nouvelle URL, et vous devez mettre à jour l'adresse de votre point de terminaison du bot pour l'utiliser également.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Test de votre bot sans téléchargement vers Teams

Il peut parfois être nécessaire de tester votre bot sans l'installer en tant qu'application dans Teams. Nous vous fournissons deux méthodes pour le faire ci-dessous. Il peut être utile de tester votre bot sans l'installer en tant qu'application pour vous assurer qu'il est disponible et de répondre. Toutefois, il ne vous permettra pas de tester l'ensemble des fonctionnalités De Microsoft Teams que vous avez peut-être ajoutées à votre bot. Si vous avez besoin de tester entièrement votre bot, suivez les instructions de [test en chargeant](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utiliser l'émulateur de bot

L'émulateur Bot Framework est une application de bureau qui permet aux développeurs de bots de tester et déboguer leurs bots, localement ou à distance. À l'aide de l'émulateur, vous pouvez discuter avec votre bot et inspecter les messages qu'il envoie et reçoit. Cela peut être utile pour vérifier que votre bot est disponible et y répondre, mais l'émulateur ne vous permettra pas de tester les fonctionnalités spécifiques de Teams que vous avez ajoutées à votre bot, et les réponses de votre bot ne constitueront pas une représentation visuelle précise de la façon dont elles seront rendues dans Teams. Si vous devez tester l'un de ces éléments, il est préférable de [télécharger votre bot.](#test-by-uploading-to-teams)

Vous pouvez trouver des instructions complètes sur l'émulateur Bot Framework [ici.](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)

### <a name="talk-to-your-bot-directly-by-id"></a>Parlez directement à votre bot par ID

>[!Important]
>Le fait de parler à votre bot par ID est destiné uniquement à des fins de test.

Vous pouvez également initier une conversation avec votre bot à l'aide de son ID. Deux méthodes pour ce faire sont données ci-dessous. Lorsqu'un bot a été ajouté par l'une de ces méthodes, il ne sera pas adressaçable dans les conversations de canal et vous ne pouvez pas tirer parti des autres fonctionnalités de l'application Microsoft Teams telles que les onglets ou les extensions de messagerie.

1. Dans la page [Tableau de bord](https://dev.botframework.com/bots) du bot de votre bot, sous **Canaux,** sélectionnez Ajouter **à Microsoft Teams.** Microsoft Teams s'lancera avec une conversation personnelle avec votre bot.
2. Référencez directement l'ID d'application de votre bot à partir de Microsoft Teams :
   * Dans la page [Tableau de bord](https://dev.botframework.com/bots) du bot de votre bot, sous **Détails,** copiez l'ID d'application **Microsoft** de votre bot.
  
     ![Obtention de l'AppID pour le bot](~/assets/images/bots_appid_botframework.png)
  
   * Dans Microsoft Teams, dans le volet **De** conversation, sélectionnez l'icône Ajouter **une conversation.** Pour **:**, collez l'ID d'application Microsoft de votre bot.
  
     ![Téléchargement de l'AppID pour le bot](~/assets/images/bots_uploading.png)

     L'ID d'application doit être résolu en nom de bot.

   * Sélectionnez votre bot et envoyez un message pour lancer une conversation.
   * Vous pouvez également coller l'ID d'application de votre bot dans la zone de recherche en haut à gauche dans Microsoft Teams. Dans la page des résultats de la recherche, accédez à l'onglet Personnes pour voir votre bot et commencer à discuter avec lui.

Votre bot recevra l'événement de la même façon que les bots ajoutés à une équipe, mais sans les informations de `conversationUpdate` l'équipe dans `channelData` l'objet.

## <a name="blocking-a-bot-in-personal-chat"></a>Blocage d'un bot dans une conversation personnelle

Notez que les utilisateurs peuvent choisir d'empêcher votre bot d'envoyer des messages de conversation personnels. Ils peuvent le faire en cliquant avec le bouton droit sur votre bot dans le canal de conversation et en choisissant Bloquer **la conversation du bot.** Cela signifie que vos bots continueront d'envoyer des messages, mais que l'utilisateur ne recevra pas ces messages.

![Blocage d'un bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Suppression d'un bot d'une équipe

Les utilisateurs peuvent supprimer le bot en choisissant l'icône de corbeille dans la liste des bots dans l'affichage de leurs équipes. Notez que cela supprime uniquement le bot de l'utilisation de cette équipe . les utilisateurs individuels pourront toujours interagir dans un contexte personnel.

Les bots dans un contexte personnel ne peuvent pas être désactivés ou supprimés par un utilisateur, à moins de supprimer complètement le bot de Teams.

## <a name="disabling-a-bot-in-teams"></a>Désactivation d'un bot dans Teams

Pour arrêter la réception de messages par votre bot, go to your Bot Dashboard and edit the Microsoft Teams channel. Effacer **l'option Activer sur Microsoft Teams.** Cela empêche les utilisateurs d'interagir avec le bot, mais il sera toujours découvrable et les utilisateurs pourront toujours l'ajouter aux équipes.

## <a name="deleting-a-bot-from-teams"></a>Suppression d'un bot dans Teams

Pour supprimer complètement votre bot de Teams, go to your Bot Dashboard and edit the Microsoft Teams channel. Sélectionnez **le bouton** Supprimer en bas. Cela empêche les utilisateurs de découvrir, d'ajouter ou d'interagir avec votre bot. Notez que cela ne supprime pas le bot des instances Teams d'autres utilisateurs, bien qu'il cesse de fonctionner pour eux également.

## <a name="removing-your-bot-from-appsource"></a>Suppression de votre bot d'AppSource

Si vous souhaitez supprimer votre bot de votre application Teams dans AppSource (anciennement Office Store), vous devez supprimer le bot du manifeste de votre application et le resoumettre pour validation. Pour [plus d'informations, voir Publier votre application Microsoft Teams sur AppSource.](~/concepts/deploy-and-publish/apps-publish.md)
