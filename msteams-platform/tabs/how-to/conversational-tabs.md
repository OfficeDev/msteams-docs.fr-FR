---
title: Créer des onglets de conversation
author: surbhigupta
description: Créer une conversation de sous-entité conversationnelle pour vos onglets de canal
keywords: Canal d’onglets teams configurable
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: dffd4eb468167561735dbc292a400416c9bb11af
ms.sourcegitcommit: 95e0c767ca0f2a51c4a7ca87700ce50b7b154b7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2021
ms.locfileid: "58529006"
---
# <a name="create-conversational-tabs"></a>Créer des onglets de conversation

Les sous-entités de conversation permettent aux utilisateurs d’avoir des conversations sur des sous-entités dans votre onglet, telles que des tâches spécifiques, des patients et des opportunités de vente, au lieu de discuter de l’onglet entier, également appelé entité. Un canal classique ou un onglet configurable permet à l’utilisateur d’avoir une conversation sur un onglet, mais l’utilisateur a besoin d’une conversation plus axée. L’exigence d’une conversation plus axée peut se produire soit s’il y a trop de contenu pour avoir une discussion centralisée, soit parce que le contenu a changé au fil du temps, ce qui rend la conversation non pertinente pour le contenu affiché. Les sous-entités de conversation offrent une expérience de conversation beaucoup plus axée sur les onglets dynamiques.

Les sous-entités de conversation sont uniquement pris en charge dans les canaux. Ils peuvent être utilisés à partir d’un onglet personnel ou statique pour créer ou poursuivre des conversations dans des onglets déjà épinglés à un canal. L’onglet statique est utile si vous souhaitez fournir un emplacement à un utilisateur pour afficher et accéder aux conversations qui se produisent sur plusieurs canaux.

## <a name="prerequisites"></a>Configuration requise

Pour prendre en charge les sous-entités conversationnelles, votre application web d’onglet doit pouvoir stocker un mappage entre les sous-entités ↔ conversations dans une base de données principale. L’offre est fournie, mais vous devez la stocker et la renvoyer à Teams pour que les utilisateurs `conversationId` `conversationId` poursuivent la conversation.

## <a name="start-a-new-conversation"></a>Démarrer une nouvelle conversation

Pour démarrer une nouvelle conversation, utilisez la `openConversation()` fonction. Le démarrage et la poursuite d’une conversation sont tous gérés par cette méthode. Les entrées de la fonction changent en fonction de l’action que vous souhaitez prendre. Du point de vue des utilisateurs, le panneau de conversation s’ouvre à droite de l’écran, soit pour initier une conversation, soit poursuivre une conversation.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation prend les** entrées suivantes pour démarrer une conversation dans un canal :

* **subEntityId**: il s’agit de l’ID de votre sous-entité spécifique. Par exemple, task-123.
* **entityId**: il s’agit de l’ID de l’instance d’onglet lors de sa création. L’ID est important pour renvoyer à la même instance d’onglet.
* **channelId**: il s’agit du canal dans lequel réside l’instance d’onglet.
   > [!NOTE]
   > ChannelId **est** facultatif pour les onglets de canal. Toutefois, il est recommandé si vous souhaitez conserver votre implémentation entre les onglets de canal et statiques.
* **title**: il s’agit du titre affiché à l’utilisateur dans le panneau de conversation.

La plupart de ces valeurs peuvent également être récupérées à partir de `getContext` l’API.

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

L’image suivante montre le panneau de conversation :

![Sous-entités de conversation : démarrer une conversation](~/assets/images/tabs/conversational-subentities/start-conversation.png)

Si l’utilisateur démarre une conversation, il est important d’écouter le rappel de cet événement afin de récupérer et d’enregistrer la **conversationId**:

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

`conversationResponse`L’objet contient des informations relatives à la conversation qui a été démarrée. Il est recommandé d’enregistrer toutes les propriétés de cet objet de réponse pour une utilisation ultérieure.

## <a name="continue-a-conversation"></a>Poursuivre une conversation

Après le démarrage d’une conversation, les appels suivants nécessitent que vous fournissiez également les mêmes entrées que dans le démarrage d’une nouvelle conversation, mais incluez également `openConversation()` **la conversationId**. [](#start-a-new-conversation) Le panneau de conversation s’ouvre pour l’utilisateur avec la conversation appropriée en vue. Les utilisateurs peuvent voir les messages nouveaux ou entrants en temps réel.

L’image suivante montre le panneau de conversation avec la conversation appropriée :

![Sous-entités de conversation : poursuivre la conversation](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>Améliorer une conversation

Il est important que votre onglet inclut [des liens profonds vers votre sous-entité.](~/concepts/build-and-test/deep-links.md) Par exemple, l’utilisateur qui sélectionne le lien profond de l’onglet dans la conversation de canal. Le comportement attendu consiste à recevoir le lien profond, à ouvrir cette sous-entité, puis à ouvrir le panneau de conversation pour cette sous-entité.

Pour prendre en charge les sous-entités de conversation à partir de votre onglet personnel ou statique, vous n’avez rien à modifier dans votre implémentation. Nous viennent uniquement en charge le démarrage ou la poursuite des conversations à partir d’onglets de canal qui sont déjà épinglés. La prise en charge des onglets statiques vous permet de fournir un emplacement unique permettant à vos utilisateurs d’interagir avec toutes vos sous-entités. Il est important que vous enregistrez le , et lorsque votre onglet est initialement créé dans un canal pour avoir les propriétés droites lors de l’ouverture de l’affichage de conversation dans un `subEntityId` `entityId` onglet `channelId` statique.

## <a name="close-a-conversation"></a>Fermer une conversation

Vous pouvez fermer manuellement l’affichage conversation en appelant la `closeConversation()` fonction.

```javascript
microsoftTeams.conversations.closeConversation();
```

Vous pouvez également écouter un événement lorsque l’affichage conversation est fermé par un utilisateur.

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|Créer un onglet Conversationnel| Microsoft Teams exemple d’application d’onglet pour démontrer la création d’un onglet de conversation. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Modifications des marges de l’onglet](~/resources/removing-tab-margins.md)