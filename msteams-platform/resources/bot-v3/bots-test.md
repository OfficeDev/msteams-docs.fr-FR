---
title: Tester et déboguer votre bot
description: Dans cet article, vous saurez comment tester et déboguer vos bots dans Microsoft Teams et tester votre bot sans le charger dans Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/20/2019
ms.openlocfilehash: 3cfb76443566a0ca5c279547f7b3db490c6095d3
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143696"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Tester et déboguer votre bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Lorsque vous testez votre bot, vous devez prendre en compte à la fois le ou les contextes dans lesquels vous souhaitez que votre bot s’exécute, ainsi que les fonctionnalités que vous avez peut-être ajoutées à votre bot qui nécessitent des données spécifiques à Microsoft Teams. Vérifiez que la méthode que vous avez choisie pour tester votre bot s’aligne sur ses fonctionnalités.

## <a name="test-by-uploading-to-teams"></a>Tester en chargeant dans Teams

La méthode la plus complète pour tester votre bot consiste à créer un package d’application et à le charger dans Teams. Il s’agit de la seule méthode permettant de tester toutes les fonctionnalités disponibles pour votre bot, dans toutes les étendues.

Il existe deux méthodes pour charger votre application. Vous pouvez utiliser [App Studio](~/concepts/build-and-test/app-studio-overview.md) ou vous pouvez créer manuellement [un package d’application](~/concepts/build-and-test/apps-package.md) et [charger votre](~/concepts/deploy-and-publish/apps-upload.md)d’application. Si vous devez modifier votre manifeste et recharger votre application, vous devez [supprimer votre bot](#deleting-a-bot-from-teams) avant de charger votre package d’application modifié.

## <a name="debug-your-bot-locally"></a>Déboguer votre bot localement

Si vous hébergez votre bot localement pendant le développement, vous devez utiliser un service de tunneling comme [ngrok](https://ngrok.com/) pour tester votre bot. Une fois que vous avez téléchargé et installé ngrok, exécutez la commande ci-dessous pour démarrer le service de tunneling. Vous devrez peut-être ajouter ngrok à votre chemin d’accès.

```bash
ngrok http <port> -host-header=localhost:<port>
```

Utilisez le point de terminaison https fourni par ngrok dans le manifeste de votre application. Si vous fermez votre fenêtre de commande et redémarrez, vous obtenez une nouvelle URL et devez mettre à jour l’adresse de votre point de terminaison de bot pour l’utiliser également.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Test de votre bot sans chargement dans Teams

Il est parfois nécessaire de tester votre bot sans l’installer en tant qu’application dans Teams. Nous fournissons deux méthodes de test. Le test de votre bot sans l’installer en tant qu’application peut être utile pour vous assurer que votre bot est disponible et répond, mais il ne vous permettra pas de tester toute la gamme des fonctionnalités de Microsoft Teams que vous avez peut-être ajoutées à votre bot. Si vous devez tester complètement votre bot, suivez les instructions pour [test en chargeant](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utiliser l’émulateur de bot

Le Bot Framework Emulator est une application de bureau qui permet aux développeurs de bots de tester et de déboguer leurs bots, localement ou à distance. À l’aide de l’émulateur, vous pouvez discuter avec votre bot et inspecter les messages que votre bot envoie et reçoit. Cela peut être utile pour vérifier que votre bot est disponible et répond, mais l’émulateur ne vous permettra pas de tester les fonctionnalités spécifiques à Teams que vous avez ajoutées à votre bot, et les réponses de votre bot ne seront pas une représentation visuelle précise de la façon dont ils sont rendus dans Teams. Si vous avez besoin de tester l’un de ces éléments, il n’est pas préférable de [charger votre bot](#test-by-uploading-to-teams).

Vous trouverez des instructions complètes sur le Bot Framework Emulator [ici](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Contactez votre bot directement par ID

>[!Important]
>La communication avec votre bot par ID est destinée uniquement à des fins de test.

Vous pouvez également lancer une conversation avec votre bot à l’aide de son ID. Deux méthodes sont fournies ci-dessous. Lorsqu’un bot a été ajouté via l’une de ces méthodes, il n’est pas adressable dans les conversations de canal, et vous ne pouvez pas tirer parti d’autres fonctionnalités d’application Microsoft Teams telles que les onglets ou les extensions de message.

1. Dans la page [tableau de bord du bot](https://dev.botframework.com/bots) pour votre bot, sous **Canaux**, sélectionnez **Ajouter à Microsoft Teams**. Microsoft Teams démarre avec une conversation personnelle avec votre bot.
2. Référencez directement l’ID d’application de votre bot à partir de Microsoft Teams :
   * Dans la page du [tableau de bord du bot](https://dev.botframework.com/bots) pour votre bot, sous **Détails**, copiez **l’ID d’application Microsoft** pour votre bot.
  
      :::image type="content" source="../../assets/images/bots_appid_botframework.png" alt-text="Tableau de bord du bot":::
  
   * Dans Microsoft Teams, dans le volet **Conversation** , sélectionnez l’icône **Ajouter une conversation** . Pour **À :**, collez l’ID d’application Microsoft de votre bot.
  
      :::image type="content" source="../../assets/images/bots_uploading.png" alt-text="Chargement de l’AppID pour le bot"border="true":::

     L’ID d’application doit correspondre au nom de votre bot.

   * Sélectionnez votre bot et envoyez un message pour lancer une conversation.
   * Vous pouvez également coller l’ID d’application de votre bot dans la zone de recherche en haut à gauche dans Microsoft Teams. Dans la page des résultats de la recherche, accédez à l’onglet Contacts pour voir votre bot et commencer à discuter avec lui.

Votre bot recevra l’événement `conversationUpdate` comme les bots ajoutés à une équipe, mais sans les informations d’équipe dans l’objet `channelData`.

## <a name="blocking-a-bot-in-personal-chat"></a>Blocage d’un bot dans une conversation personnelle

Les utilisateurs peuvent choisir d’empêcher votre bot d’envoyer des messages de conversation personnels. Ils peuvent activer/désactiver cette option en cliquant avec le bouton droit sur votre bot dans le canal de conversation et en choisissant **bloquer la conversation du bot**. Cela signifie que vos bots continueront d’envoyer des messages, mais que l’utilisateur ne recevra pas ces messages.

  :::image type="content" source="../../assets/images/bots/botdisable.png" alt-text="Blocage d’un bot"border="true":::

## <a name="removing-a-bot-from-a-team"></a>Suppression d’un bot d’une équipe

Les utilisateurs peuvent supprimer le bot en choisissant l’icône de corbeille dans la liste des bots dans l’affichage Teams. Notez que cela supprime uniquement le bot de l’utilisation de cette équipe. Les utilisateurs individuels peuvent interagir dans un contexte personnel.

Les bots dans un contexte personnel ne peuvent pas être désactivés ou supprimés par un utilisateur, à moins de supprimer complètement le bot de Teams.

## <a name="disabling-a-bot-in-teams"></a>Désactivation d’un bot dans Teams

Pour arrêter votre bot de recevoir des messages, accédez à votre tableau de bord du bot et modifiez le canal Microsoft Teams. Désactivez l’option **Activer sur Microsoft Teams**. Cela empêche les utilisateurs d’interagir avec le bot, mais il reste détectable et les utilisateurs peuvent l’ajouter aux équipes.

## <a name="deleting-a-bot-from-teams"></a>Suppression d’un bot de Teams

Pour supprimer complètement votre bot de Teams, accédez à votre tableau de bord du bot et modifiez le canal Microsoft Teams. Choisissez le bouton **Supprimer** en bas. Cela empêche les utilisateurs de découvrir, d’ajouter ou d’interagir avec votre bot. Cela ne supprime pas le bot des instances Teams d’autres utilisateurs, bien qu’il cesse également de fonctionner pour eux.

## <a name="removing-your-bot-from-appsource"></a>Suppression de votre bot d’AppSource

Si vous souhaitez supprimer votre bot de votre application Teams dans AppSource (précédemment Office Store), vous devez supprimer le bot de votre manifeste d’application et renvoyer votre application pour validation. Pour plus d’informations, consultez [Publier votre application Microsoft Teams sur AppSource](~/concepts/deploy-and-publish/apps-publish.md).
