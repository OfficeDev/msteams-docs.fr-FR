---
title: Créer des onglets de conversation
author: surbhigupta
description: Apprenez à créer des onglets conversationnels dans Microsoft Teams pour démarrer, continuer, améliorer et fermer une conversation.
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: high
ms.openlocfilehash: fa54221a413b19704d80ec62feb1cf068e42d1a0
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820121"
---
# <a name="create-conversational-tabs"></a>Créer des onglets de conversation

Les sous-entités conversationnelles permettent aux utilisateurs d’avoir des conversations sur les sous-entités dans votre onglet. Par exemple, une tâche spécifique, un patient et une opportunité de vente, au lieu de discuter de l’onglet entier, également appelé entité. Un canal traditionnel ou un onglet configurable permet à l’utilisateur d’avoir une conversation sur un onglet, mais l’utilisateur a besoin d’une conversation plus ciblée. L’exigence d’une conversation plus ciblée peut survenir, soit s’il y a trop de contenu pour avoir une discussion centralisée, soit parce que le contenu a changé au fil du temps, rendant la conversation non pertinente pour le contenu affiché. Les sous-entités conversationnelles fournissent une expérience de conversation beaucoup plus ciblée pour les onglets dynamiques.

Les sous-entités conversationnelles sont uniquement prises en charge dans les canaux. Ils peuvent être utilisés à partir d’un onglet personnel ou statique pour créer ou poursuivre des conversations dans des onglets déjà épinglés à un canal. L’onglet statique est utile si vous souhaitez fournir un emplacement pour qu’un utilisateur affiche les conversations qui se passent sur plusieurs canaux et y accède.

## <a name="prerequisites"></a>Configuration requise

Pour prendre en charge les sous-entités conversationnelles, votre application web d’onglet doit avoir la possibilité de stocker un mappage entre les conversations de sous-entités ↔ dans une base de données principale. Est `conversationId` fourni, mais vous devez le stocker `conversationId` et le retourner à Teams pour que les utilisateurs puissent poursuivre la conversation.

## <a name="start-a-new-conversation"></a>Démarrer une nouvelle conversation

Pour démarrer une nouvelle conversation, utilisez la `openConversation()` fonction . Le démarrage et la poursuite d’une conversation sont tous gérés par cette méthode. Les entrées de la fonction changent en fonction de l’action que vous souhaitez effectuer. Du point de vue de l’utilisateur, le panneau de conversation s’ouvre à droite de l’écran, soit pour lancer une conversation, soit pour poursuivre une conversation.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** prend les entrées suivantes pour démarrer une conversation dans un canal :

* **subEntityId** : ID de votre sous-entité spécifique. Par exemple, tâche 123.
* **entityId** : ID de l’instance d’onglet lors de sa création. L’ID est important pour renvoyer à la même instance d’onglet.
* **channelId** : canal dans lequel réside l’instance d’onglet.
   > [!NOTE]
   > **ChannelId** est facultatif pour les onglets de canal. Toutefois, il est recommandé si vous souhaitez conserver la même implémentation entre les canaux et les onglets statiques.
* **title** : titre affiché à l’utilisateur dans le panneau de conversation.

La plupart de ces valeurs peuvent également être récupérées à partir de l’API [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) (`microsoftTeams.getContext()` dans TeamsJS v1). Pour plus d’informations, consultez [Interface PageInfo](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

L’image suivante montre le panneau de conversation :

:::image type="content" source="../../assets/images/tabs/conversational-subentities/start-conversation.png" alt-text="démarrer des conversations":::

Si l’utilisateur démarre une conversation, il est important d’écouter le rappel de cet événement pour récupérer et enregistrer **conversationId** :

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onStartConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

L’objet `conversationResponse` contient des informations relatives à la conversation qui a été démarrée. Il est recommandé d’enregistrer toutes les propriétés de cet objet de réponse pour une utilisation ultérieure.

## <a name="continue-a-conversation"></a>Poursuivre une conversation

Après le démarrage d’une conversation, les appels `openConversation()` suivants exigent que vous fournissiez également les mêmes entrées que dans [démarrer une nouvelle conversation](#start-a-new-conversation), mais que vous incluiez également **conversationId**. Le panneau de conversation s’ouvre pour les utilisateurs avec la conversation appropriée en vue. Les utilisateurs peuvent voir les messages nouveaux ou entrants en temps réel.

L’image suivante montre le panneau de conversation avec la conversation appropriée :

:::image type="content" source="../../assets/images/tabs/conversational-subentities/continue-conversation.png" alt-text="poursuivre les conversations":::

## <a name="enhance-a-conversation"></a>Améliorer une conversation

Il est important que votre onglet inclue [des liens profonds vers votre sous-entité](~/concepts/build-and-test/deep-links.md). Par exemple, l’utilisateur sélectionnant le lien profond de la tabulation chiclet à partir de la conversation de canal. Le comportement attendu est de recevoir le lien profond, d’ouvrir cette sous-entité, puis d’ouvrir le panneau de conversation pour cette sous-entité.

Pour prendre en charge les sous-entités conversationnelles à partir de votre onglet personnel ou statique, vous n’avez rien à modifier dans votre implémentation. Nous prenons uniquement en charge le démarrage ou la poursuite des conversations à partir d’onglets de canal déjà épinglés. La prise en charge des onglets statiques vous permet de fournir un emplacement unique à vos utilisateurs pour interagir avec toutes vos sous-entités. Il est important d’enregistrer , et `channelId` lorsque votre onglet est créé à l’origine `subEntityId``entityId`dans un canal pour avoir les propriétés appropriées lors de l’ouverture de l’affichage conversation dans un onglet statique.

## <a name="close-a-conversation"></a>Fermer une conversation

Vous pouvez fermer manuellement la vue de conversation en appelant la `closeConversation()` fonction .

```javascript
microsoftTeams.conversations.closeConversation();
```

Vous pouvez également écouter un événement lorsque les utilisateurs **sélectionnent Fermer (X)** dans la vue de conversation.

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onCloseConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|Onglet Créer une conversation| Exemple d’application d’onglet Microsoft Teams pour montrer l’onglet Créer une conversation. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Modifications des marges de l’onglet](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>Voir aussi

* [Créer des onglets pour Teams](../what-are-tabs.md)
* [Créer un onglet personnel](create-personal-tab.md)
* [Créer un onglet de canal ou un onglet de groupe](create-channel-group-tab.md)
* [Créer des onglets avec les Cartes adaptatives](build-adaptive-card-tabs.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
