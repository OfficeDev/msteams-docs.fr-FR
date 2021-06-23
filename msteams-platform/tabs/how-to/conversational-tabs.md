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
# <a name="create-conversational-tabs"></a><span data-ttu-id="e4914-104">Créer des onglets de conversation</span><span class="sxs-lookup"><span data-stu-id="e4914-104">Create conversational tabs</span></span>

<span data-ttu-id="e4914-105">Les sous-entités de conversation permettent aux utilisateurs d’avoir des conversations sur des sous-entités dans votre onglet, telles que des tâches spécifiques, des patients et des opportunités de vente, au lieu de discuter de l’onglet entier, également appelé entité.</span><span class="sxs-lookup"><span data-stu-id="e4914-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="e4914-106">Un canal traditionnel ou un onglet configurable permet à l’utilisateur d’avoir une conversation sur un onglet, mais il peut vouloir une conversation plus axée.</span><span class="sxs-lookup"><span data-stu-id="e4914-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user may want a more focused conversation.</span></span> <span data-ttu-id="e4914-107">L’exigence d’une conversation plus axée peut se produire si le contenu est trop important pour qu’une discussion centralisée soit modifiée au fil du temps, ce qui rend la conversation non pertinente par rapport au contenu affiché.</span><span class="sxs-lookup"><span data-stu-id="e4914-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="e4914-108">Les sous-entités de conversation offrent une expérience de conversation beaucoup plus axée sur les onglets dynamiques.</span><span class="sxs-lookup"><span data-stu-id="e4914-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="e4914-109">Les sous-entités de conversation sont uniquement pris en charge dans les canaux.</span><span class="sxs-lookup"><span data-stu-id="e4914-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="e4914-110">Toutefois, ils peuvent être utilisés à partir d’un onglet  personnel ou statique pour créer ou poursuivre des conversations dans des onglets déjà épinglés à un canal.</span><span class="sxs-lookup"><span data-stu-id="e4914-110">However, they can be used from a personal or static tab to create or continue conversations in tabs that are *already* pinned to a channel.</span></span> <span data-ttu-id="e4914-111">L’onglet statique est utile si vous souhaitez fournir un emplacement à un utilisateur pour afficher et accéder aux conversations qui se produisent sur plusieurs canaux.</span><span class="sxs-lookup"><span data-stu-id="e4914-111">The static tab is useful if you wish to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4914-112">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e4914-112">Prerequisites</span></span>

<span data-ttu-id="e4914-113">Pour prendre en charge les sous-entités conversationnelles, votre application web d’onglet doit pouvoir stocker un mappage entre les sous-entités ↔ conversations dans une base de données principale.</span><span class="sxs-lookup"><span data-stu-id="e4914-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="e4914-114">Nous vous fournirons les informations, mais il vous incombera de les stocker et de les renvoyer à Teams afin que les utilisateurs poursuivent `conversationId` `conversationId` la conversation.</span><span class="sxs-lookup"><span data-stu-id="e4914-114">We will provide you with the `conversationId`, but it will be your responsibility to store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="e4914-115">Démarrer une nouvelle conversation</span><span class="sxs-lookup"><span data-stu-id="e4914-115">Start a new conversation</span></span>

<span data-ttu-id="e4914-116">Pour démarrer une nouvelle conversation, utilisez la `openConversation()` fonction.</span><span class="sxs-lookup"><span data-stu-id="e4914-116">To start a new conversation, you use the `openConversation()` function.</span></span> <span data-ttu-id="e4914-117">Le démarrage et la poursuite d’une conversation sont tous gérés par cette méthode, toutefois, les entrées de la fonction changent en fonction de l’action que vous souhaitez prendre.</span><span class="sxs-lookup"><span data-stu-id="e4914-117">Starting and continuing a conversation are all handled by this method, however, the inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="e4914-118">Du point de vue des utilisateurs, le panneau de conversation s’ouvre à droite de l’écran, soit pour initier une conversation, soit poursuivre une conversation.</span><span class="sxs-lookup"><span data-stu-id="e4914-118">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="e4914-119">**openConversation prend les** entrées suivantes pour démarrer une conversation dans un canal :</span><span class="sxs-lookup"><span data-stu-id="e4914-119">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="e4914-120">**subEntityId**: il s’agit de l’ID de votre sous-entité spécifique.</span><span class="sxs-lookup"><span data-stu-id="e4914-120">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="e4914-121">Par exemple, task-123.</span><span class="sxs-lookup"><span data-stu-id="e4914-121">For example, task-123.</span></span>
* <span data-ttu-id="e4914-122">**entityId**: il s’agit de l’ID de l’instance d’onglet lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="e4914-122">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="e4914-123">L’ID est important pour renvoyer à la même instance d’onglet.</span><span class="sxs-lookup"><span data-stu-id="e4914-123">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="e4914-124">**channelId**: il s’agit du canal dans lequel réside l’instance d’onglet.</span><span class="sxs-lookup"><span data-stu-id="e4914-124">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="e4914-125">Le **channelId est** facultatif pour les onglets de canal.</span><span class="sxs-lookup"><span data-stu-id="e4914-125">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="e4914-126">Toutefois, il est recommandé si vous souhaitez conserver votre implémentation entre les onglets de canal et statiques.</span><span class="sxs-lookup"><span data-stu-id="e4914-126">However, it is recommended if you wish to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="e4914-127">**title**: il s’agit du titre affiché à l’utilisateur dans le panneau de conversation.</span><span class="sxs-lookup"><span data-stu-id="e4914-127">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="e4914-128">La plupart de ces valeurs peuvent également être récupérées à partir de `getContext` l’API.</span><span class="sxs-lookup"><span data-stu-id="e4914-128">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="e4914-129">Cette commande ouvre le panneau de conversation.</span><span class="sxs-lookup"><span data-stu-id="e4914-129">This will open the conversation panel.</span></span>

![Sous-entités de conversation - Démarrer la conversation](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="e4914-131">Si l’utilisateur démarre une conversation, il est important d’écouter le rappel de cet événement afin de récupérer et d’enregistrer la **conversationId**:</span><span class="sxs-lookup"><span data-stu-id="e4914-131">If the user starts a conversation, it’s important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="e4914-132">`conversationReponse`L’objet contient des informations relatives à la conversation qui vient de commencer.</span><span class="sxs-lookup"><span data-stu-id="e4914-132">The `conversationReponse` object contains information related to the conversation that was just started.</span></span> <span data-ttu-id="e4914-133">Nous vous recommandons d’enregistrer toutes les propriétés de cet objet de réponse pour les réutiliser ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e4914-133">We recommend you save all the properties of this response object for reuse later.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="e4914-134">Poursuivre une conversation</span><span class="sxs-lookup"><span data-stu-id="e4914-134">Continue a conversation</span></span>

<span data-ttu-id="e4914-135">Après le démarrage d’une conversation, les appels suivants à nécessite que vous fournissiez également les mêmes entrées que dans démarrer une nouvelle conversation d’onglet de canal, mais également inclure la `openConversation()` **conversationId** [](#Starting a new channel tab conversation).</span><span class="sxs-lookup"><span data-stu-id="e4914-135">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [Starting a new channel tab conversation](#Starting a new channel tab conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="e4914-136">Le panneau de conversation s’ouvre pour l’utilisateur avec la conversation appropriée en vue.</span><span class="sxs-lookup"><span data-stu-id="e4914-136">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="e4914-137">Les utilisateurs peuvent voir les messages nouveaux ou entrants en temps réel.</span><span class="sxs-lookup"><span data-stu-id="e4914-137">Users are able to see new or incoming messages in real-time.</span></span>

![Sous-entités de conversation - Continuer la conversation](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="e4914-139">Améliorer une conversation</span><span class="sxs-lookup"><span data-stu-id="e4914-139">Enhance a conversation</span></span>

<span data-ttu-id="e4914-140">Enfin, il est important que votre onglet utilise des [liens profonds vers votre sous-entité.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="e4914-140">Finally, it’s important that your tab consumes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="e4914-141">Par exemple, un utilisateur clique sur le lien profond de l’onglet à partir de la conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="e4914-141">For example, user clicking the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="e4914-142">Le comportement attendu consiste à recevoir le lien profond, à ouvrir cette sous-entité, puis à ouvrir le panneau de conversation pour cette sous-entité spécifique.</span><span class="sxs-lookup"><span data-stu-id="e4914-142">The expected behavior is for you to receive the deeplink, open that sub-entity, and then open the conversation panel for that specific sub-entity.</span></span>

<span data-ttu-id="e4914-143">Pour prendre en charge les sous-entités de conversation à partir de votre onglet personnel ou statique, vous n’avez rien à modifier concernant votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="e4914-143">To support conversational sub-entities from your personal or static tab, you do not have to change anything about your implementation.</span></span> <span data-ttu-id="e4914-144">Nous viennent uniquement en charge le démarrage ou la poursuite des conversations à partir d’onglets de canal qui sont déjà épinglés.</span><span class="sxs-lookup"><span data-stu-id="e4914-144">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="e4914-145">La prise en charge des onglets statiques vous permet de fournir un emplacement unique permettant à vos utilisateurs d’interagir avec toutes vos sous-entités.</span><span class="sxs-lookup"><span data-stu-id="e4914-145">Supporting static tabs allow you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="e4914-146">Toutefois, il est important que vous enregistrez l’onglet , et lorsque votre onglet est créé à l’origine dans un canal afin de pouvoir avoir les bonnes propriétés lors de l’ouverture de l’affichage conversation dans un onglet `subEntityId` `entityId` `channelId` statique.</span><span class="sxs-lookup"><span data-stu-id="e4914-146">It is, however, important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel in order for you to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="e4914-147">Fermer une conversation</span><span class="sxs-lookup"><span data-stu-id="e4914-147">Close a conversation</span></span>

<span data-ttu-id="e4914-148">Vous pouvez fermer manuellement l’affichage conversation en appelant la `closeConversation()` fonction.</span><span class="sxs-lookup"><span data-stu-id="e4914-148">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="e4914-149">Vous pouvez également écouter un événement lorsque l’affichage conversation est fermé par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e4914-149">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```
