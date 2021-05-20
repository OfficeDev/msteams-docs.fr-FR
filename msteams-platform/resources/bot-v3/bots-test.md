---
title: Testez et débogez votre bot
description: Décrit comment tester les bots dans Microsoft Teams
keywords: équipes bots test
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
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Testez et débogez votre bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Lors de l’essai de votre bot, vous devez prendre en considération à la fois le contexte (s) que vous souhaitez que votre bot s’exécute, ainsi que toutes les fonctionnalités que vous avez peut-être ajouté à votre bot qui nécessite des données spécifiques à Microsoft Teams. Assurez-vous que la méthode que vous avez choisie pour tester votre bot s’aligne sur ses fonctionnalités.

## <a name="test-by-uploading-to-teams"></a>Testez en téléchargeant sur Teams

La façon la plus complète de tester votre bot est de créer un paquet d’applications et de le télécharger sur Teams. C’est la seule méthode pour tester toutes les fonctionnalités disponibles pour votre bot, dans toutes les étendues.

Il existe deux méthodes pour télécharger votre application. Vous pouvez soit utiliser [App Studio pour](~/concepts/build-and-test/app-studio-overview.md) vous aider, soit créer manuellement un package [d’application et](~/concepts/build-and-test/apps-package.md) télécharger votre [application.](~/concepts/deploy-and-publish/apps-upload.md) Si vous devez modifier votre manifeste et re-télécharger votre application, vous devez [supprimer votre bot avant](#deleting-a-bot-from-teams) de télécharger votre paquet d’application modifié.

## <a name="debug-your-bot-locally"></a>Débogez votre bot localement

Si vous hébergez votre bot localement pendant le développement, vous devrez utiliser un service de tunnelage [comme ngrok](https://ngrok.com/) afin de tester votre bot. Une fois que vous avez téléchargé et installé ngrok, exécutez la commande ci-dessous pour démarrer le service de tunneling. Vous devrez peut-être ajouter du ngrok à votre chemin.

```bash
ngrok http <port> -host-header=localhost:<port>
```

Utilisez le point de terminaison https fourni par ngrok dans votre manifeste d’application. Si vous fermez votre fenêtre de commande et redémarrez, vous obtiendrez une nouvelle URL, et vous devrez mettre à jour votre adresse de point de terminaison bot pour l’utiliser également.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Testez votre bot sans le télécharger sur Teams

Parfois, il peut être nécessaire de tester votre bot sans l’installer comme une application dans Teams. Nous fournissons deux méthodes pour le faire ci-dessous. Tester votre bot sans l’installer comme une application peut être utile pour s’assurer que votre bot est disponible et de répondre, mais il ne vous permettra pas de tester toute la gamme des fonctionnalités de Microsoft Teams que vous avez peut-être ajouté à votre bot. Si vous avez besoin de tester entièrement votre bot, s’il vous plaît suivre les instructions [pour les tests en téléchargeant](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Utilisez l’émulateur Bot

Le Bot Framework Emulator une application de bureau qui permet aux développeurs de bots de tester et de déboger leurs bots, localement ou à distance. À l’aide de l’émulateur, vous pouvez discuter avec votre bot et inspecter les messages que votre bot envoie et reçoit. Cela peut être utile pour vérifier que votre bot est disponible et de répondre, mais l’émulateur ne vous permettra pas de tester toutes les fonctionnalités spécifiques à Teams que vous avez ajouté à votre bot, ni les réponses de votre bot sera une représentation visuelle précise de la façon dont ils seront rendus en Teams. Si vous avez besoin de tester l’une ou l’autre de ces choses, il est préférable [de télécharger votre bot](#test-by-uploading-to-teams).

Des instructions complètes sur Bot Framework Emulator peuvent être trouvées [ici](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Parlez directement à votre bot par Id

>[!Important]
>Parler à votre bot par Id est destiné à des fins de test seulement.

Vous pouvez également entamer une conversation avec votre bot en utilisant son Id. Deux méthodes pour ce faire sont données ci-dessous. Lorsqu’un bot a été ajouté par l’une de ces méthodes, il ne sera pas adressable dans les conversations de canaux, et vous ne pouvez pas profiter d’autres fonctionnalités d’application Microsoft Teams comme les onglets ou les extensions de messagerie.

1. Sur la page [Bot Dashboard](https://dev.botframework.com/bots) pour votre bot, sous **Canaux,** sélectionnez **Ajouter à Microsoft Teams**. Microsoft Teams lancera avec une conversation personnelle avec votre bot.
2. Référez directement l’iD de l’application de votre bot de Microsoft Teams :
   * Sur la page [Bot Dashboard](https://dev.botframework.com/bots) pour votre bot, sous **Détails,** copiez l’IDENTIFIANT **Microsoft App** pour votre bot.
  
     ![Obtenir l’AppID pour le bot](~/assets/images/bots_appid_botframework.png)
  
   * De l’Microsoft Teams, sur le **volet Chat,** sélectionnez l’icône **Ajouter le chat.** Pour **: ,** coller l’identifiant microsoft app de votre bot.
  
     ![Téléchargement de l’AppID pour le bot](~/assets/images/bots_uploading.png)

     L’ID de l’application doit se résoudre à votre nom de bot.

   * Sélectionnez votre bot et envoyez un message pour lancer une conversation.
   * Alternativement, vous pouvez coller l’iD de l’application de votre bot dans la boîte de recherche en haut à gauche Microsoft Teams. Dans la page des résultats de recherche, accédez à l’onglet Personnes pour voir votre bot et commencer à discuter avec elle.

Votre bot recevra l’événement `conversationUpdate` tout comme les bots ajoutés à une équipe, mais sans les informations de l’équipe dans l’objet. `channelData`

## <a name="blocking-a-bot-in-personal-chat"></a>Blocage d’un bot dans le chat personnel

Notez que les utilisateurs peuvent choisir de bloquer votre bot d’envoyer des messages de chat personnel. Ils peuvent basculer cela en cliquant à droite sur votre bot dans le canal de chat et en **choisissant block bot conversation**. Cela signifie que vos bots continueront d’envoyer des messages, mais l’utilisateur ne recevra pas ces messages.

![Blocage d’un bot](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Retrait d’un bot d’une équipe

Les utilisateurs peuvent supprimer le bot en choisissant l’icône poubelle sur la liste des bots dans la vue de leurs équipes. Notez que cela supprime uniquement le bot de l’utilisation de cette équipe; les utilisateurs individuels seront toujours en mesure d’interagir dans leur contexte personnel.

Les bots dans leur contexte personnel ne peuvent pas être désactivés ou supprimés par un utilisateur, à moins de supprimer complètement le bot Teams.

## <a name="disabling-a-bot-in-teams"></a>Désactiver un bot dans Teams

Pour empêcher votre bot de recevoir des messages, rendez-vous sur votre tableau de bord Bot et modifiez Microsoft Teams canal. Effacer **l’option Activer** Microsoft Teams’achat. Cela empêche les utilisateurs d’interagir avec le bot, mais il sera toujours détectable et les utilisateurs seront toujours en mesure de l’ajouter aux équipes.

## <a name="deleting-a-bot-from-teams"></a>Suppression d’un bot de Teams

Pour supprimer complètement votre bot de votre Teams, rendez-vous sur votre tableau de bord Bot et modifiez le canal Microsoft Teams’eau. Choisissez le **bouton** Supprimer en bas. Cela empêche les utilisateurs de découvrir, d’ajouter ou d’interagir avec votre bot. Notez que cela ne supprime pas le bot des instances d’Teams utilisateurs, bien qu’il cesse de fonctionner pour eux aussi.

## <a name="removing-your-bot-from-appsource"></a>Suppression de votre bot d’AppSource

Si vous souhaitez supprimer votre bot de votre application Teams dans AppSource (précédemment Office Store), vous devez supprimer le bot de votre manifeste d’application et soumettre à nouveau votre application pour validation. Pour plus d’informations, [consultez l’application Microsoft Teams votre application à AppSource](~/concepts/deploy-and-publish/apps-publish.md).
