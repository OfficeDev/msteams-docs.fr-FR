---
title: Tester et déboguer votre bot
description: Décrit comment tester des bots dans Microsoft Teams
keywords: Tests de bots teams
ms.topic: how-to
localization_priority: Normal
ms.date: 03/20/2019
ms.openlocfilehash: 269b0680e45d764cf4cb0269c40d3d202145edb8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566459"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Tester et déboguer votre bot Microsoft Teams de test

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Lorsque vous testez votre bot, vous devez prendre en considération le ou les contextes dans lequel vous souhaitez que votre bot s’exécute, ainsi que les fonctionnalités que vous avez peut-être ajoutées à votre bot qui nécessitent des données spécifiques à Microsoft Teams. Assurez-vous que la méthode que vous avez choisie pour tester votre bot s’aligne sur ses fonctionnalités.

## <a name="test-by-uploading-to-teams"></a>Testez en chargeant vers Teams

La façon la plus complète de tester votre bot consiste à créer un package d’application et à le télécharger sur Teams. Il s’agit de la seule méthode pour tester les fonctionnalités complètes disponibles pour votre bot, dans toutes les étendues.

Il existe deux méthodes pour charger votre application. Vous pouvez utiliser [App Studio](~/concepts/build-and-test/app-studio-overview.md) pour vous aider, ou vous pouvez créer manuellement un [package](~/concepts/build-and-test/apps-package.md) d’application et télécharger [votre application.](~/concepts/deploy-and-publish/apps-upload.md) Si vous avez besoin de modifier votre manifeste et de retélé télécharger votre application, vous devez supprimer votre [bot](#deleting-a-bot-from-teams) avant de télécharger votre package d’application modifié.

## <a name="debug-your-bot-locally"></a>Déboguer votre bot localement

Si vous hébergez votre bot localement pendant le développement, vous devez utiliser un service de tunneling comme [ngrok](https://ngrok.com/) pour tester votre bot. Une fois que vous avez téléchargé et installé ngrok, exécutez la commande ci-dessous pour démarrer le service de tunneling. Vous devrez peut-être ajouter ngrok à votre chemin d’accès.

```bash
ngrok http <port> -host-header=localhost:<port>
```

Utilisez le point de terminaison https fourni par ngrok dans le manifeste de votre application. Si vous fermez votre fenêtre de commande et redémarrez, vous obtenez une nouvelle URL, et vous devez mettre à jour l’adresse de votre point de terminaison du bot pour l’utiliser également.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Test de votre bot sans téléchargement vers Teams

Parfois, il peut être nécessaire de tester votre bot sans l’installer en tant qu’application Teams. Nous vous fournissons deux méthodes pour le faire ci-dessous. Il peut être utile de tester votre bot sans l’installer en tant qu’application pour vous assurer qu’il est disponible et de répondre. Toutefois, il ne vous permettra pas de tester l’ensemble des fonctionnalités Microsoft Teams que vous avez peut-être ajoutées à votre bot. Si vous avez besoin de tester entièrement votre bot, suivez les instructions de [test en chargeant](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utiliser l’émulateur de bot

Le Bot Framework Emulator est une application de bureau qui permet aux développeurs de bots de tester et déboguer leurs bots, localement ou à distance. À l’aide de l’émulateur, vous pouvez discuter avec votre bot et inspecter les messages qu’il envoie et reçoit. Cela peut être utile pour vérifier que votre bot est disponible et y répondre, mais l’émulateur ne vous permettra pas de tester les fonctionnalités spécifiques Teams que vous avez ajoutées à votre bot, et les réponses de votre bot ne constitueront pas une représentation visuelle précise de leur rendu dans Teams. Si vous devez tester l’un de ces éléments, il est préférable de [télécharger votre bot.](#test-by-uploading-to-teams)

Les instructions complètes sur le Bot Framework Emulator sont [ici.](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)

### <a name="talk-to-your-bot-directly-by-id"></a>Parlez directement à votre bot par ID

>[!Important]
>Le fait de parler à votre bot par ID est destiné uniquement à des fins de test.

Vous pouvez également initier une conversation avec votre bot à l’aide de son ID. Deux méthodes pour ce faire sont données ci-dessous. Lorsqu’un bot a été ajouté via l’une de ces méthodes, il ne pourra pas être adressaçable dans les conversations de canal et vous ne pouvez pas tirer parti des autres fonctionnalités d’application Microsoft Teams telles que les onglets ou les extensions de messagerie.

1. Dans la page [Tableau de bord](https://dev.botframework.com/bots) du bot pour votre bot, sous **Canaux,** **sélectionnez** Ajouter à Microsoft Teams . Microsoft Teams lancement avec une conversation personnelle avec votre bot.
2. Référencez directement l’ID d’application de votre bot à partir de Microsoft Teams :
   * Dans la page [Tableau de bord](https://dev.botframework.com/bots) du bot de votre bot, sous **Détails,** copiez l’ID d’application **Microsoft** de votre bot.
  
     ![Obtention de l’AppID pour le bot](~/assets/images/bots_appid_botframework.png)
  
   * Dans Microsoft Teams, dans le volet **de** conversation, sélectionnez l’icône Ajouter **une conversation.** Pour **:**, collez l’ID d’application Microsoft de votre bot.
  
     ![Téléchargement de l’AppID pour le bot](~/assets/images/bots_uploading.png)

     L’ID d’application doit être résolu en nom de bot.

   * Sélectionnez votre bot et envoyez un message pour lancer une conversation.
   * Vous pouvez également coller l’ID d’application de votre bot dans la zone de recherche en haut à gauche Microsoft Teams. Dans la page des résultats de la recherche, accédez à l’onglet Personnes pour voir votre bot et commencer à discuter avec lui.

Votre bot recevra l’événement de la même façon que les bots ajoutés à une équipe, mais sans les informations de `conversationUpdate` l’équipe dans `channelData` l’objet.

## <a name="blocking-a-bot-in-personal-chat"></a>Blocage d’un bot dans une conversation personnelle

Notez que les utilisateurs peuvent choisir d’empêcher votre bot d’envoyer des messages de conversation personnels. Ils peuvent le faire en cliquant avec le bouton droit sur votre bot dans le canal de conversation et en choisissant Bloquer **la conversation du bot.** Cela signifie que vos bots continueront d’envoyer des messages, mais que l’utilisateur ne recevra pas ces messages.

![Blocage d’un bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Suppression d’un bot d’une équipe

Les utilisateurs peuvent supprimer le bot en choisissant l’icône de corbeille dans la liste des bots dans l’affichage de leurs équipes. Notez que cela supprime uniquement le bot de l’utilisation de cette équipe . les utilisateurs individuels pourront toujours interagir dans un contexte personnel.

Les bots dans un contexte personnel ne peuvent pas être désactivés ou supprimés par un utilisateur, à moins de supprimer complètement le bot de Teams.

## <a name="disabling-a-bot-in-teams"></a>Désactivation d’un bot dans Teams

Pour arrêter la réception de messages par votre bot, go to your Bot Dashboard and edit the Microsoft Teams channel. Clear the **Enable on Microsoft Teams** option. Cela empêche les utilisateurs d’interagir avec le bot, mais il sera toujours découvrable et les utilisateurs pourront toujours l’ajouter aux équipes.

## <a name="deleting-a-bot-from-teams"></a>Suppression d’un bot d’Teams

Pour supprimer complètement votre bot de Teams, go to your Bot Dashboard and edit the Microsoft Teams channel. Sélectionnez **le bouton** Supprimer en bas. Cela empêche les utilisateurs de découvrir, d’ajouter ou d’interagir avec votre bot. Notez que cela ne supprime pas le bot des instances de Teams d’autres utilisateurs, bien qu’il cesse également de fonctionner pour eux.

## <a name="removing-your-bot-from-appsource"></a>Suppression de votre bot d’AppSource

Si vous souhaitez supprimer votre bot de votre application Teams dans AppSource (précédemment Office Store), vous devez supprimer le bot du manifeste de votre application et le resoumettre pour validation. Pour plus d’informations, voir [Publier votre Microsoft Teams sur AppSource.](~/concepts/deploy-and-publish/apps-publish.md)
