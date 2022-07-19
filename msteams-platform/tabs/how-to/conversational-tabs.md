---
title: Créer des onglets de conversation
author: surbhigupta
description: Dans ce module, apprenez à créer une conversation de sous-entité conversationnelle pour vos onglets de canal, afin de gérer les conversations à l’aide d’exemples de code
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: medium
ms.openlocfilehash: f039c8cb03aa874993f64d32030eb226c59a707d
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841981"
---
# <a name="create-conversational-tabs"></a>Créer des onglets de conversation

Les sous-entités conversationnelles permettent aux utilisateurs d’avoir des conversations sur les sous-entités de votre onglet. Par exemple, une tâche spécifique, un patient et une opportunité de vente, au lieu de discuter de l’ensemble de l’onglet, également appelé entité. Un canal traditionnel ou un onglet configurable permet à l’utilisateur d’avoir une conversation sur un onglet, mais l’utilisateur a besoin d’une conversation plus ciblée. L’exigence d’une conversation plus ciblée peut survenir soit s’il y a trop de contenu pour avoir une discussion centralisée, soit parce que le contenu a changé au fil du temps, ce qui rend la conversation non pertinente pour le contenu affiché. Les sous-entités conversationnelles offrent une expérience de conversation beaucoup plus ciblée pour les onglets dynamiques.

Les sous-entités conversationnelles sont prises en charge uniquement dans les canaux. Ils peuvent être utilisés à partir d’un onglet personnel ou statique pour créer ou poursuivre des conversations dans des onglets déjà épinglés à un canal. L’onglet statique est utile si vous souhaitez fournir un emplacement permettant à un utilisateur d’afficher et d’accéder aux conversations qui se produisent sur plusieurs canaux.

## <a name="prerequisites"></a>Configuration requise

Pour prendre en charge les sous-entités conversationnelles, votre application web onglet doit avoir la possibilité de stocker un mappage entre les conversations de sous-entités ↔ dans une base de données principale. Il `conversationId` est fourni, mais vous devez le stocker et le renvoyer à Teams afin que `conversationId` les utilisateurs poursuivent la conversation.

## <a name="start-a-new-conversation"></a>Démarrer une nouvelle conversation

Pour démarrer une nouvelle conversation, utilisez la `openConversation()` fonction. Le démarrage et la poursuite d’une conversation sont tous gérés par cette méthode. Les entrées de la fonction changent en fonction de l’action que vous souhaitez effectuer, du point de vue de l’utilisateur, ce qui ouvre le panneau de conversation à droite de l’écran, soit pour lancer une conversation, soit pour poursuivre une conversation.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** prend les entrées suivantes pour démarrer une conversation dans un canal :

* **subEntityId** : ID de votre sous-entité spécifique. Par exemple, la tâche 123.
* **entityId** : ID de l’instance d’onglet lors de sa création. L’ID est important pour renvoyer à la même instance d’onglet.
* **channelId** : canal dans lequel réside l’instance d’onglet.
   > [!NOTE]
   > **ChannelId** est facultatif pour les onglets de canal. Toutefois, il est recommandé de conserver votre implémentation sur plusieurs canaux et onglets statiques de la même manière.
* **title**: Titre affiché à l’utilisateur dans le panneau de conversation.

La plupart de ces valeurs peuvent également être récupérées à partir de l’API [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) (`microsoftTeams.getContext()` dans TeamsJS v1). Pour plus d’informations, consultez [l’interface PageInfo](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

L’image suivante montre le panneau de conversation :

:::image type="content" source="../../assets/images/tabs/conversational-subentities/start-conversation.png" alt-text="démarrer des conversations":::

Si l’utilisateur démarre une conversation, il est important d’écouter le rappel de cet événement pour récupérer et enregistrer l’ID de **conversation** :

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

L’objet `conversationResponse` contient des informations relatives à la conversation qui a été démarrée. Il est recommandé d’enregistrer toutes les propriétés de cet objet de réponse pour une utilisation ultérieure.

## <a name="continue-a-conversation"></a>Poursuivre une conversation

Après le démarrage d’une conversation, les appels suivants à `openConversation()` exiger, que vous fournissez également les mêmes entrées que dans [le démarrage d’une nouvelle conversation](#start-a-new-conversation), mais également inclure **l’ID de conversation**. Le panneau de conversation s’ouvre pour les utilisateurs avec la conversation appropriée en vue. Les utilisateurs peuvent voir les messages nouveaux ou entrants en temps réel.

L’image suivante montre le panneau de conversation avec la conversation appropriée :

:::image type="content" source="../../assets/images/tabs/conversational-subentities/continue-conversation.png" alt-text="continuer les conversations":::

## <a name="enhance-a-conversation"></a>Améliorer une conversation

Il est important que votre onglet inclue des [liens profonds vers votre sous-entité](~/concepts/build-and-test/deep-links.md). Par exemple, l’utilisateur sélectionne le lien profond de chiclet d’onglet dans la conversation de canal. Le comportement attendu consiste à recevoir le lien profond, à ouvrir cette sous-entité, puis à ouvrir le panneau de conversation pour cette sous-entité.

Pour prendre en charge les sous-entités conversationnelles à partir de votre onglet personnel ou statique, vous n’avez rien à modifier dans votre implémentation. Nous prenons uniquement en charge le démarrage ou la poursuite des conversations à partir d’onglets de canal déjà épinglés. La prise en charge des onglets statiques vous permet de fournir un emplacement unique pour permettre à vos utilisateurs d’interagir avec toutes vos sous-entités. Il est important d’enregistrer le , `entityId`et `channelId` lorsque votre onglet est créé à l’origine `subEntityId`dans un canal pour avoir les propriétés appropriées lors de l’ouverture de la vue de conversation dans un onglet statique.

## <a name="close-a-conversation"></a>Fermer une conversation

Vous pouvez fermer manuellement l’affichage de conversation en appelant la `closeConversation()` fonction.

```javascript
microsoftTeams.conversations.closeConversation();
```

Vous pouvez également écouter un événement lorsque l’affichage de conversation est fermé par un utilisateur.

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|Onglet Créer une conversation| Exemple d’application de l’onglet Microsoft Teams pour illustrer l’onglet Créer une conversation. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Modifications des marges de l’onglet](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>Voir aussi

* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
