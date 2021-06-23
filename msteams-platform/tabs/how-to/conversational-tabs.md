---
title: Créer des onglets de conversation
author: surbhigupta
description: Créer une conversation de sous-entité conversationnelle pour vos onglets de canal
keywords: Canal d’onglets teams configurable
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: 343cbe26ded2792489640ae3d86ec94c7c6db72b
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069229"
---
# <a name="create-conversational-tabs"></a>Créer des onglets de conversation

Les sous-entités de conversation permettent aux utilisateurs d’avoir des conversations sur des sous-entités dans votre onglet, telles que des tâches spécifiques, des patients et des opportunités de vente, au lieu de discuter de l’onglet entier, également appelé entité. Un canal traditionnel ou un onglet configurable permet à l’utilisateur d’avoir une conversation sur un onglet, mais il peut vouloir une conversation plus axée. L’exigence d’une conversation plus axée peut se produire si le contenu est trop important pour qu’une discussion centralisée soit modifiée au fil du temps, ce qui rend la conversation non pertinente par rapport au contenu affiché. Les sous-entités de conversation offrent une expérience de conversation beaucoup plus axée sur les onglets dynamiques.

Les sous-entités de conversation sont uniquement pris en charge dans les canaux. Toutefois, ils peuvent être utilisés à partir d’un onglet  personnel ou statique pour créer ou poursuivre des conversations dans des onglets déjà épinglés à un canal. L’onglet statique est utile si vous souhaitez fournir un emplacement à un utilisateur pour afficher et accéder aux conversations qui se produisent sur plusieurs canaux.

## <a name="prerequisites"></a>Conditions préalables

Pour prendre en charge les sous-entités conversationnelles, votre application web d’onglet doit pouvoir stocker un mappage entre les sous-entités ↔ conversations dans une base de données principale. Nous vous fournirons les informations, mais il vous incombera de les stocker et de les renvoyer à Teams afin que les utilisateurs poursuivent `conversationId` `conversationId` la conversation.

## <a name="start-a-new-conversation"></a>Démarrer une nouvelle conversation

Pour démarrer une nouvelle conversation, utilisez la `openConversation()` fonction. Le démarrage et la poursuite d’une conversation sont tous gérés par cette méthode, toutefois, les entrées de la fonction changent en fonction de l’action que vous souhaitez prendre. Du point de vue des utilisateurs, le panneau de conversation s’ouvre à droite de l’écran, soit pour initier une conversation, soit poursuivre une conversation.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation prend les** entrées suivantes pour démarrer une conversation dans un canal :

* **subEntityId**: il s’agit de l’ID de votre sous-entité spécifique. Par exemple, task-123.
* **entityId**: il s’agit de l’ID de l’instance d’onglet lors de sa création. L’ID est important pour renvoyer à la même instance d’onglet.
* **channelId**: il s’agit du canal dans lequel réside l’instance d’onglet.
   > [!NOTE]
   > Le **channelId est** facultatif pour les onglets de canal. Toutefois, il est recommandé si vous souhaitez conserver votre implémentation entre les onglets de canal et statiques.
* **title**: il s’agit du titre affiché à l’utilisateur dans le panneau de conversation.

La plupart de ces valeurs peuvent également être récupérées à partir de `getContext` l’API.

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

Cette commande ouvre le panneau de conversation.

![Sous-entités de conversation - Démarrer la conversation](~/assets/images/tabs/conversational-subentities/start-conversation.png)

Si l’utilisateur démarre une conversation, il est important d’écouter le rappel de cet événement afin de récupérer et d’enregistrer la **conversationId**:

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

`conversationReponse`L’objet contient des informations relatives à la conversation qui vient de commencer. Nous vous recommandons d’enregistrer toutes les propriétés de cet objet de réponse pour les réutiliser ultérieurement.

## <a name="continue-a-conversation"></a>Poursuivre une conversation

Après le démarrage d’une conversation, les appels suivants à nécessite que vous fournissiez également les mêmes entrées que dans démarrer une nouvelle conversation d’onglet de canal, mais également inclure la `openConversation()` **conversationId** [](#Starting a new channel tab conversation). Le panneau de conversation s’ouvre pour l’utilisateur avec la conversation appropriée en vue. Les utilisateurs peuvent voir les messages nouveaux ou entrants en temps réel.

![Sous-entités de conversation - Continuer la conversation](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>Améliorer une conversation

Enfin, il est important que votre onglet utilise des [liens profonds vers votre sous-entité.](~/concepts/build-and-test/deep-links.md) Par exemple, un utilisateur clique sur le lien profond de l’onglet à partir de la conversation de canal. Le comportement attendu consiste à recevoir le lien profond, à ouvrir cette sous-entité, puis à ouvrir le panneau de conversation pour cette sous-entité spécifique.

Pour prendre en charge les sous-entités de conversation à partir de votre onglet personnel ou statique, vous n’avez rien à modifier concernant votre implémentation. Nous viennent uniquement en charge le démarrage ou la poursuite des conversations à partir d’onglets de canal qui sont déjà épinglés. La prise en charge des onglets statiques vous permet de fournir un emplacement unique permettant à vos utilisateurs d’interagir avec toutes vos sous-entités. Toutefois, il est important que vous enregistrez l’onglet , et lorsque votre onglet est créé à l’origine dans un canal afin de pouvoir avoir les bonnes propriétés lors de l’ouverture de l’affichage conversation dans un onglet `subEntityId` `entityId` `channelId` statique.

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
