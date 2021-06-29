---
title: Créer des onglets de conversation
author: surbhigupta
description: Créer une conversation de sous-entité conversationnelle pour vos onglets de canal
keywords: Canal d’onglets teams configurable
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: b563510b9ce232a98572430c76f1b8e59ddb4886
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179691"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="961ea-104">Créer des onglets de conversation</span><span class="sxs-lookup"><span data-stu-id="961ea-104">Create conversational tabs</span></span>

<span data-ttu-id="961ea-105">Les sous-entités de conversation permettent aux utilisateurs d’avoir des conversations sur des sous-entités dans votre onglet, telles que des tâches spécifiques, des patients et des opportunités de vente, au lieu de discuter de l’onglet entier, également appelé entité.</span><span class="sxs-lookup"><span data-stu-id="961ea-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="961ea-106">Un canal classique ou un onglet configurable permet à l’utilisateur d’avoir une conversation sur un onglet, mais l’utilisateur a besoin d’une conversation plus axée.</span><span class="sxs-lookup"><span data-stu-id="961ea-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user requires a more focused conversation.</span></span> <span data-ttu-id="961ea-107">L’exigence d’une conversation plus axée peut se produire soit s’il y a trop de contenu pour avoir une discussion centralisée, soit parce que le contenu a changé au fil du temps, ce qui rend la conversation non pertinente pour le contenu affiché.</span><span class="sxs-lookup"><span data-stu-id="961ea-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or because the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="961ea-108">Les sous-entités de conversation offrent une expérience de conversation beaucoup plus axée sur les onglets dynamiques.</span><span class="sxs-lookup"><span data-stu-id="961ea-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="961ea-109">Les sous-entités de conversation sont uniquement pris en charge dans les canaux.</span><span class="sxs-lookup"><span data-stu-id="961ea-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="961ea-110">Ils peuvent être utilisés à partir d’un onglet personnel ou statique pour créer ou poursuivre des conversations dans des onglets déjà épinglés à un canal.</span><span class="sxs-lookup"><span data-stu-id="961ea-110">They can be used from a personal or static tab to create or continue conversations in tabs that are already pinned to a channel.</span></span> <span data-ttu-id="961ea-111">L’onglet statique est utile si vous souhaitez fournir un emplacement à un utilisateur pour afficher et accéder aux conversations qui se produisent sur plusieurs canaux.</span><span class="sxs-lookup"><span data-stu-id="961ea-111">The static tab is useful if you want to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="961ea-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="961ea-112">Prerequisites</span></span>

<span data-ttu-id="961ea-113">Pour prendre en charge les sous-entités conversationnelles, votre application web d’onglet doit pouvoir stocker un mappage entre les sous-entités ↔ conversations dans une base de données principale.</span><span class="sxs-lookup"><span data-stu-id="961ea-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="961ea-114">L’offre est fournie, mais vous devez la stocker et la renvoyer à Teams pour que les utilisateurs `conversationId` `conversationId` poursuivent la conversation.</span><span class="sxs-lookup"><span data-stu-id="961ea-114">The `conversationId` is provided, but you must store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="961ea-115">Démarrer une nouvelle conversation</span><span class="sxs-lookup"><span data-stu-id="961ea-115">Start a new conversation</span></span>

<span data-ttu-id="961ea-116">Pour démarrer une nouvelle conversation, utilisez la `openConversation()` fonction.</span><span class="sxs-lookup"><span data-stu-id="961ea-116">To start a new conversation, use the `openConversation()` function.</span></span> <span data-ttu-id="961ea-117">Le démarrage et la poursuite d’une conversation sont tous gérés par cette méthode.</span><span class="sxs-lookup"><span data-stu-id="961ea-117">Starting and continuing a conversation are all handled by this method.</span></span> <span data-ttu-id="961ea-118">Les entrées de la fonction changent en fonction de l’action que vous souhaitez prendre.</span><span class="sxs-lookup"><span data-stu-id="961ea-118">The inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="961ea-119">Du point de vue des utilisateurs, le panneau de conversation s’ouvre à droite de l’écran, soit pour initier une conversation, soit poursuivre une conversation.</span><span class="sxs-lookup"><span data-stu-id="961ea-119">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="961ea-120">**openConversation prend les** entrées suivantes pour démarrer une conversation dans un canal :</span><span class="sxs-lookup"><span data-stu-id="961ea-120">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="961ea-121">**subEntityId**: il s’agit de l’ID de votre sous-entité spécifique.</span><span class="sxs-lookup"><span data-stu-id="961ea-121">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="961ea-122">Par exemple, task-123.</span><span class="sxs-lookup"><span data-stu-id="961ea-122">For example, task-123.</span></span>
* <span data-ttu-id="961ea-123">**entityId**: il s’agit de l’ID de l’instance d’onglet lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="961ea-123">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="961ea-124">L’ID est important pour renvoyer à la même instance d’onglet.</span><span class="sxs-lookup"><span data-stu-id="961ea-124">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="961ea-125">**channelId**: il s’agit du canal dans lequel réside l’instance d’onglet.</span><span class="sxs-lookup"><span data-stu-id="961ea-125">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="961ea-126">ChannelId **est** facultatif pour les onglets de canal.</span><span class="sxs-lookup"><span data-stu-id="961ea-126">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="961ea-127">Toutefois, il est recommandé si vous souhaitez conserver votre implémentation entre les onglets de canal et statiques.</span><span class="sxs-lookup"><span data-stu-id="961ea-127">However, it is recommended if you want to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="961ea-128">**title**: il s’agit du titre affiché à l’utilisateur dans le panneau de conversation.</span><span class="sxs-lookup"><span data-stu-id="961ea-128">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="961ea-129">La plupart de ces valeurs peuvent également être récupérées à partir de `getContext` l’API.</span><span class="sxs-lookup"><span data-stu-id="961ea-129">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="961ea-130">L’image suivante montre le panneau de conversation :</span><span class="sxs-lookup"><span data-stu-id="961ea-130">The following image shows the conversation panel:</span></span>

![Sous-entités de conversation : démarrer une conversation](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="961ea-132">Si l’utilisateur démarre une conversation, il est important d’écouter le rappel de cet événement afin de récupérer et d’enregistrer la **conversationId**:</span><span class="sxs-lookup"><span data-stu-id="961ea-132">If the user starts a conversation, it is important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="961ea-133">`conversationResponse`L’objet contient des informations relatives à la conversation qui a été démarrée.</span><span class="sxs-lookup"><span data-stu-id="961ea-133">The `conversationResponse` object contains information related to the conversation that was started.</span></span> <span data-ttu-id="961ea-134">Il est recommandé d’enregistrer toutes les propriétés de cet objet de réponse pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="961ea-134">It is recommended that you save all the properties of this response object for later use.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="961ea-135">Poursuivre une conversation</span><span class="sxs-lookup"><span data-stu-id="961ea-135">Continue a conversation</span></span>

<span data-ttu-id="961ea-136">Après le démarrage d’une conversation, les appels suivants nécessitent que vous fournissiez également les mêmes entrées que dans le démarrage d’une nouvelle conversation, mais incluez également `openConversation()` **la conversationId**. [](#start-a-new-conversation)</span><span class="sxs-lookup"><span data-stu-id="961ea-136">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [start a new conversation](#start-a-new-conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="961ea-137">Le panneau de conversation s’ouvre pour l’utilisateur avec la conversation appropriée en vue.</span><span class="sxs-lookup"><span data-stu-id="961ea-137">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="961ea-138">Les utilisateurs peuvent voir les messages nouveaux ou entrants en temps réel.</span><span class="sxs-lookup"><span data-stu-id="961ea-138">Users are able to see new or incoming messages in real-time.</span></span>

<span data-ttu-id="961ea-139">L’image suivante montre le panneau de conversation avec la conversation appropriée :</span><span class="sxs-lookup"><span data-stu-id="961ea-139">The following image shows the conversation panel with the appropriate conversation:</span></span>

![Sous-entités de conversation : poursuivre la conversation](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="961ea-141">Améliorer une conversation</span><span class="sxs-lookup"><span data-stu-id="961ea-141">Enhance a conversation</span></span>

<span data-ttu-id="961ea-142">Il est important que votre onglet inclut [des liens profonds vers votre sous-entité.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="961ea-142">It is important that your tab includes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="961ea-143">Par exemple, l’utilisateur qui sélectionne le lien profond de l’onglet dans la conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="961ea-143">For example, user selecting the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="961ea-144">Le comportement attendu consiste à recevoir le lien profond, à ouvrir cette sous-entité, puis à ouvrir le panneau de conversation pour cette sous-entité.</span><span class="sxs-lookup"><span data-stu-id="961ea-144">The expected behavior is to receive the deeplink, open that sub-entity, and then open the conversation panel for that sub-entity.</span></span>

<span data-ttu-id="961ea-145">Pour prendre en charge les sous-entités de conversation à partir de votre onglet personnel ou statique, vous n’avez rien à modifier dans votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="961ea-145">To support conversational sub-entities from your personal or static tab, you do not have to change anything in your implementation.</span></span> <span data-ttu-id="961ea-146">Nous viennent uniquement en charge le démarrage ou la poursuite des conversations à partir d’onglets de canal qui sont déjà épinglés.</span><span class="sxs-lookup"><span data-stu-id="961ea-146">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="961ea-147">La prise en charge des onglets statiques vous permet de fournir un emplacement unique permettant à vos utilisateurs d’interagir avec toutes vos sous-entités.</span><span class="sxs-lookup"><span data-stu-id="961ea-147">Supporting static tabs allows you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="961ea-148">Il est important que vous enregistrez le , et lorsque votre onglet est initialement créé dans un canal pour avoir les propriétés droites lors de l’ouverture de l’affichage de conversation dans un `subEntityId` `entityId` onglet `channelId` statique.</span><span class="sxs-lookup"><span data-stu-id="961ea-148">It is important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="961ea-149">Fermer une conversation</span><span class="sxs-lookup"><span data-stu-id="961ea-149">Close a conversation</span></span>

<span data-ttu-id="961ea-150">Vous pouvez fermer manuellement l’affichage conversation en appelant la `closeConversation()` fonction.</span><span class="sxs-lookup"><span data-stu-id="961ea-150">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="961ea-151">Vous pouvez également écouter un événement lorsque l’affichage conversation est fermé par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="961ea-151">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="see-also"></a><span data-ttu-id="961ea-152">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="961ea-152">See also</span></span>

* [<span data-ttu-id="961ea-153">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="961ea-153">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="961ea-154">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="961ea-154">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="961ea-155">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="961ea-155">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="961ea-156">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="961ea-156">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="961ea-157">Créer des onglets avec les Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="961ea-157">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="next-step"></a><span data-ttu-id="961ea-158">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="961ea-158">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="961ea-159">Modifications des marges de l’onglet</span><span class="sxs-lookup"><span data-stu-id="961ea-159">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)