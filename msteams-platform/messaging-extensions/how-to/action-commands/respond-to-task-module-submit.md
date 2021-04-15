---
title: Répondre à l'action d'soumission du module de tâche
author: clearab
description: Décrit comment répondre à l'action d'envoi du module de tâche à partir d'une commande d'action d'extension de messagerie
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: af2bbbbe6ffff224f5b74c9b1472ba3cb21effc0
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696214"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="75aa5-103">Répondre à l'action d'soumission du module de tâche</span><span class="sxs-lookup"><span data-stu-id="75aa5-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="75aa5-104">Ce document vous guide sur la façon dont votre application répond aux commandes d'action, telles que l'action d'soumission du module de tâche de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="75aa5-104">This document guides you on how your app responds to the action commands, such as user's task module submit action.</span></span>
<span data-ttu-id="75aa5-105">Une fois qu'un utilisateur a soumis le module de tâche, votre service web reçoit un message d'appel avec l'ID de commande et les valeurs `composeExtension/submitAction` de paramètre.</span><span class="sxs-lookup"><span data-stu-id="75aa5-105">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="75aa5-106">Votre application dispose de cinq secondes pour répondre à l'appel, sinon l'utilisateur reçoit un **message** d'erreur « Impossible d'atteindre l'application » et toute réponse à l'appel est ignorée par le client Teams.</span><span class="sxs-lookup"><span data-stu-id="75aa5-106">Your app has five seconds to respond to the invoke, otherwise the user receives an error message **Unable to reach the app**, and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="75aa5-107">Vous avez les options suivantes pour répondre :</span><span class="sxs-lookup"><span data-stu-id="75aa5-107">You have the following options to respond:</span></span>

* <span data-ttu-id="75aa5-108">Aucune réponse : utilisez l'action d'soumission pour déclencher un processus dans un système externe et ne pas fournir de commentaires à l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="75aa5-108">No response: Use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="75aa5-109">Cela est utile pour les processus de longue durée, et vous pouvez choisir de fournir des commentaires en alternative.</span><span class="sxs-lookup"><span data-stu-id="75aa5-109">This is useful for long-running processes, and you can select to provide feedback alternately.</span></span> <span data-ttu-id="75aa5-110">Par exemple, vous pouvez envoyer des commentaires avec un [message proactif.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="75aa5-110">For example, you can give feedback with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="75aa5-111">[Autre module de tâche](#respond-with-another-task-module): vous pouvez répondre avec un module de tâche supplémentaire dans le cadre d'une interaction en plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="75aa5-111">[Another task module](#respond-with-another-task-module): You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="75aa5-112">[Réponse de carte](#respond-with-a-card-inserted-into-the-compose-message-area): vous pouvez répondre avec une carte avec qui l'utilisateur peut interagir ou l'insérer dans un message.</span><span class="sxs-lookup"><span data-stu-id="75aa5-112">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area): You can respond with a card that the user can interact with or insert into a message.</span></span>
* <span data-ttu-id="75aa5-113">[Carte adaptative du bot](#bot-response-with-adaptive-card): insérez une carte adaptative directement dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="75aa5-113">[Adaptive Card from bot](#bot-response-with-adaptive-card): Insert an Adaptive Card directly into the conversation.</span></span>
* <span data-ttu-id="75aa5-114">[Demandez à l'utilisateur de s'authentifier.](~/messaging-extensions/how-to/add-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="75aa5-114">[Request the user to authenticate](~/messaging-extensions/how-to/add-authentication.md).</span></span>
* <span data-ttu-id="75aa5-115">[Demandez à l'utilisateur de fournir une configuration supplémentaire.](~/messaging-extensions/how-to/add-configuration-page.md)</span><span class="sxs-lookup"><span data-stu-id="75aa5-115">[Request the user to provide additional configuration](~/messaging-extensions/how-to/add-configuration-page.md).</span></span>

<span data-ttu-id="75aa5-116">Pour l'authentification ou la configuration, une fois que l'utilisateur a terminé le processus, l'appel d'origine est resenté à votre service web.</span><span class="sxs-lookup"><span data-stu-id="75aa5-116">For authentication or configuration, after the user completes the process, the original invoke is resent to your web service.</span></span> <span data-ttu-id="75aa5-117">Le tableau suivant indique les types de réponses disponibles en fonction de l'emplacement d'appel `commandContext` de l'extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="75aa5-117">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="75aa5-118">Type de réponse</span><span class="sxs-lookup"><span data-stu-id="75aa5-118">Response Type</span></span> | <span data-ttu-id="75aa5-119">Composition</span><span class="sxs-lookup"><span data-stu-id="75aa5-119">Compose</span></span> | <span data-ttu-id="75aa5-120">Barre de commandes</span><span class="sxs-lookup"><span data-stu-id="75aa5-120">Command bar</span></span> | <span data-ttu-id="75aa5-121">Message</span><span class="sxs-lookup"><span data-stu-id="75aa5-121">Message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="75aa5-122">Réponse de carte</span><span class="sxs-lookup"><span data-stu-id="75aa5-122">Card response</span></span> | <span data-ttu-id="75aa5-123">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-123">✔</span></span> | <span data-ttu-id="75aa5-124">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-124">✔</span></span> | <span data-ttu-id="75aa5-125">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-125">✔</span></span> |
|<span data-ttu-id="75aa5-126">Un autre module de tâche</span><span class="sxs-lookup"><span data-stu-id="75aa5-126">Another task module</span></span> | <span data-ttu-id="75aa5-127">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-127">✔</span></span> | <span data-ttu-id="75aa5-128">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-128">✔</span></span> | <span data-ttu-id="75aa5-129">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-129">✔</span></span> |
|<span data-ttu-id="75aa5-130">Bot avec carte adaptative</span><span class="sxs-lookup"><span data-stu-id="75aa5-130">Bot with Adaptive Card</span></span> | <span data-ttu-id="75aa5-131">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-131">✔</span></span> | <span data-ttu-id="75aa5-132">x</span><span class="sxs-lookup"><span data-stu-id="75aa5-132">x</span></span> | <span data-ttu-id="75aa5-133">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-133">✔</span></span> |
| <span data-ttu-id="75aa5-134">Aucune réponse</span><span class="sxs-lookup"><span data-stu-id="75aa5-134">No response</span></span> | <span data-ttu-id="75aa5-135">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-135">✔</span></span> | <span data-ttu-id="75aa5-136">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-136">✔</span></span> | <span data-ttu-id="75aa5-137">✔</span><span class="sxs-lookup"><span data-stu-id="75aa5-137">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="75aa5-138">Lorsque vous sélectionnez **Action.Submit** par le biais de cartes ME, il envoie l'activité d'appel avec le nom **composeExtension**, où la valeur est égale à la charge utile habituelle.</span><span class="sxs-lookup"><span data-stu-id="75aa5-138">When you select **Action.Submit** through ME cards, it sends invoke activity with the name **composeExtension**, where the value is equal to the usual payload.</span></span>
> * <span data-ttu-id="75aa5-139">Lorsque vous sélectionnez **Action.Submit** par le biais d'une conversation, vous recevez une activité de message avec le nom **onCardButtonClicked**, où la valeur est égale à la charge utile habituelle.</span><span class="sxs-lookup"><span data-stu-id="75aa5-139">When you select **Action.Submit** through conversation, you receive message activity with the name **onCardButtonClicked**, where the value is equal to the usual payload.</span></span>

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="75aa5-140">Événement d'appel submitAction</span><span class="sxs-lookup"><span data-stu-id="75aa5-140">The submitAction invoke event</span></span>

<span data-ttu-id="75aa5-141">Voici quelques exemples de réception du message d'appel :</span><span class="sxs-lookup"><span data-stu-id="75aa5-141">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="75aa5-142">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="75aa5-142">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="75aa5-143">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="75aa5-143">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="75aa5-144">JSON</span><span class="sxs-lookup"><span data-stu-id="75aa5-144">JSON</span></span>](#tab/json)

<span data-ttu-id="75aa5-145">Voici un exemple de l'objet JSON que vous recevez.</span><span class="sxs-lookup"><span data-stu-id="75aa5-145">This is an example of the JSON object that you receive.</span></span> <span data-ttu-id="75aa5-146">Le `commandContext` paramètre indique d'où votre extension de messagerie a été déclenchée.</span><span class="sxs-lookup"><span data-stu-id="75aa5-146">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="75aa5-147">`data`L'objet contient les champs du formulaire en tant que paramètres et les valeurs envoyées par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="75aa5-147">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="75aa5-148">L'objet JSON est raccourci ici pour mettre en évidence les champs les plus pertinents.</span><span class="sxs-lookup"><span data-stu-id="75aa5-148">The JSON object here is shortened to highlight the most relevant fields.</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith",
  "serviceUrl": "https://smba.trafficmanager.net/amer/",
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "id": "submitButton",
      "formField1": "formField1_value",
      "formField2": "formField2_value",
      "formField3": "formField3_value"
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  }
}
```

* * *

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="75aa5-149">Répondre avec une carte insérée dans la zone composer un message</span><span class="sxs-lookup"><span data-stu-id="75aa5-149">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="75aa5-150">Le moyen le plus courant de répondre à la demande consiste à insérer une carte `composeExtension/submitAction` dans la zone de composition du message.</span><span class="sxs-lookup"><span data-stu-id="75aa5-150">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="75aa5-151">L'utilisateur soumet la carte à la conversation.</span><span class="sxs-lookup"><span data-stu-id="75aa5-151">The user submits the card to the conversation.</span></span> <span data-ttu-id="75aa5-152">Pour plus d'informations sur l'utilisation des cartes, voir [cartes et actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="75aa5-152">For more information on using cards, see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="75aa5-153">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="75aa5-153">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var createCardData = ((JObject)action.Data).ToObject<CreateCardData>();
var card = new HeroCard
{
     Title = createCardData.Title,
     Subtitle = createCardData.Subtitle,
     Text = createCardData.Text,
};
    var attachments = new List<MessagingExtensionAttachment>();
    attachments.Add(new MessagingExtensionAttachment
    {
        Content = card,
        ContentType = HeroCard.ContentType,
        Preview = card.ToAttachment(),
    });
    response.ComposeExtension.Attachments = attachments;
    return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="75aa5-154">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="75aa5-154">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const data = action.data;
    const heroCard = CardFactory.heroCard(data.title, data.text);
    heroCard.content.subtitle = data.subTitle;
    const attachment = { contentType: heroCard.contentType, content: heroCard.content, preview: heroCard };

    return {
      composeExtension: {
        type: 'result',
        attachmentLayout: 'list',
        attachments: [
          attachment
        ]
      }
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="75aa5-155">JSON</span><span class="sxs-lookup"><span data-stu-id="75aa5-155">JSON</span></span>](#tab/json)

```json
{
  "composeExtension": {
    "attachmentLayout": "list",
    "type": "result",
    "attachments": [
      {
        "preview": {
          "contentType": "application/vnd.microsoft.card.hero",
          "content": {
            "title": "formField1_value",
            "subtitle": "formField2_value",
            "text": "formField3_value"
          }
        },
        "contentType": "application/vnd.microsoft.card.hero",
        "content": {
          "title": "formField1_value",
          "subtitle": "formField2_value",
          "text": "formField3_value"
        }
      }
    ]
  }
}
```

* * *

## <a name="respond-with-another-task-module"></a><span data-ttu-id="75aa5-156">Répondre avec un autre module de tâche</span><span class="sxs-lookup"><span data-stu-id="75aa5-156">Respond with another task module</span></span>

<span data-ttu-id="75aa5-157">Vous pouvez choisir de répondre à `submitAction` l'événement avec un module de tâche supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="75aa5-157">You can select to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="75aa5-158">Cela est utile dans les cas ci-après :</span><span class="sxs-lookup"><span data-stu-id="75aa5-158">This is useful when:</span></span>

* <span data-ttu-id="75aa5-159">Vous devez collecter de grandes quantités d'informations.</span><span class="sxs-lookup"><span data-stu-id="75aa5-159">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="75aa5-160">Vous devez modifier dynamiquement les informations que vous collectez en fonction de l'entrée de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="75aa5-160">You need to dynamically change the information you are collecting based on user input.</span></span>
* <span data-ttu-id="75aa5-161">Vous devez valider les informations envoyées par l'utilisateur et renvoyer le formulaire avec un message d'erreur en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="75aa5-161">You need to validate the information submitted by the user and resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="75aa5-162">La méthode de réponse est la même que [pour répondre à l'événement `fetchTask` initial.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="75aa5-162">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="75aa5-163">Si vous utilisez le SDK Bot Framework, les mêmes déclencheurs d'événements pour les deux actions d'soumission.</span><span class="sxs-lookup"><span data-stu-id="75aa5-163">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="75aa5-164">Pour que cela fonctionne, vous devez ajouter une logique qui détermine la réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="75aa5-164">To make this work, you must add logic that determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="75aa5-165">Réponse du bot avec carte adaptative</span><span class="sxs-lookup"><span data-stu-id="75aa5-165">Bot response with Adaptive Card</span></span>

> [!NOTE]
> <span data-ttu-id="75aa5-166">La condition préalable pour obtenir la réponse du bot avec une carte adaptative est que vous devez ajouter l'objet au manifeste de votre application et définir l'étendue requise `bot` pour le bot.</span><span class="sxs-lookup"><span data-stu-id="75aa5-166">The prerequisite to get the bot response with an Adaptive card is that you must add the `bot` object to your app manifest, and define the required scope for the bot.</span></span> <span data-ttu-id="75aa5-167">Utilisez le même ID que votre extension de messagerie pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="75aa5-167">Use the same ID as your messaging extension for your bot.</span></span>
 
<span data-ttu-id="75aa5-168">Vous pouvez également y répondre en insérant un message avec une carte adaptative `submitAction` dans le canal avec un bot.</span><span class="sxs-lookup"><span data-stu-id="75aa5-168">You can also respond to the `submitAction` by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="75aa5-169">L'utilisateur peut afficher un aperçu du message avant de l'envoyer.</span><span class="sxs-lookup"><span data-stu-id="75aa5-169">The user can preview the message before submitting it.</span></span> <span data-ttu-id="75aa5-170">Cela est très utile dans les scénarios où vous collectez des informations auprès des utilisateurs avant de créer une réponse de carte adaptative, ou lorsque vous mettez à jour la carte après qu'une personne interagit avec elle.</span><span class="sxs-lookup"><span data-stu-id="75aa5-170">This is very useful in scenarios where you gather information from the users before creating an Adaptive Card response, or when you update the card after someone interacts with it.</span></span> 

<span data-ttu-id="75aa5-171">Le scénario suivant montre comment l'application Polly configure un sondage sans inclure les étapes de configuration dans la conversation de canal :</span><span class="sxs-lookup"><span data-stu-id="75aa5-171">The following scenario shows how the app Polly configures a poll without including the configuration steps in the channel conversation:</span></span>

<span data-ttu-id="75aa5-172">**Pour configurer le sondage**</span><span class="sxs-lookup"><span data-stu-id="75aa5-172">**To configure the poll**</span></span>

1. <span data-ttu-id="75aa5-173">L'utilisateur sélectionne l'extension de messagerie pour appeler le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="75aa5-173">The user selects the messaging extension to invoke the task module.</span></span>
1. <span data-ttu-id="75aa5-174">L'utilisateur configure le sondage avec le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="75aa5-174">The user configures the poll with the task module.</span></span>
1. <span data-ttu-id="75aa5-175">Après avoir soumis le module de tâche, l'application utilise les informations fournies pour créer le sondage en tant que carte adaptative et l'envoie en réponse `botMessagePreview` au client.</span><span class="sxs-lookup"><span data-stu-id="75aa5-175">After submitting the task module, the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="75aa5-176">L'utilisateur peut ensuite afficher un aperçu du message de carte adaptative avant que le bot l'insère dans le canal.</span><span class="sxs-lookup"><span data-stu-id="75aa5-176">The user can then preview the Adaptive Card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="75aa5-177">Si l'application n'est pas déjà membre du canal, `Send` sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="75aa5-177">If the app is not already a member of the channel, select `Send` to add it.</span></span>

    > [!NOTE] 
    > * <span data-ttu-id="75aa5-178">Les utilisateurs peuvent également sélectionner `Edit` le message, qui les renvoie au module de tâche d'origine.</span><span class="sxs-lookup"><span data-stu-id="75aa5-178">The users can also select to `Edit` the message, which returns them to the original task module.</span></span> 
    > * <span data-ttu-id="75aa5-179">L'interaction avec la carte adaptative modifie le message avant de l'envoyer.</span><span class="sxs-lookup"><span data-stu-id="75aa5-179">Interaction with the Adaptive Card changes the message before sending it.</span></span>
1. <span data-ttu-id="75aa5-180">Une fois que l'utilisateur `Send` a sélectionné le bot, il publie le message sur le canal.</span><span class="sxs-lookup"><span data-stu-id="75aa5-180">After the user selects `Send` the bot posts the message to the channel.</span></span>

## <a name="respond-to-initial-submit-action"></a><span data-ttu-id="75aa5-181">Répondre à l'action d'soumission initiale</span><span class="sxs-lookup"><span data-stu-id="75aa5-181">Respond to initial submit action</span></span>

<span data-ttu-id="75aa5-182">Votre module de tâche doit répondre au message initial avec un aperçu de la carte que le `composeExtension/submitAction` bot envoie au canal.</span><span class="sxs-lookup"><span data-stu-id="75aa5-182">Your task module must respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot sends to the channel.</span></span> <span data-ttu-id="75aa5-183">L'utilisateur peut vérifier la carte avant l'envoi, et également essayer d'installer votre bot dans la conversation si le bot n'est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="75aa5-183">The user can verify the card before sending, and also try to install your bot in the conversation if the bot is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="75aa5-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="75aa5-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic createCardData = ((JObject) action.Data).ToObject(typeof(JObject));
  var response = new MessagingExtensionActionResponse
  {
    ComposeExtension = new MessagingExtensionResult
    {
      Type = "botMessagePreview",
      ActivityPreview = MessageFactory.Attachment(new Attachment
      {
        Content = new AdaptiveCard("1.0")
        {
          Body = new List<AdaptiveElement>()
          {
            new AdaptiveTextBlock() { Text = "FormField1 value was:", Size = AdaptiveTextSize.Large },
            new AdaptiveTextBlock() { Text = Data["FormField1"] as string }
          },
          Height = AdaptiveHeight.Auto,
          Actions = new List<AdaptiveAction>()
          {
            new AdaptiveSubmitAction
            {
              Type = AdaptiveSubmitAction.TypeName,
              Title = "Submit",
              Data = new JObject { { "submitLocation", "messagingExtensionFetchTask" } },
            },
          }
        },
        ContentType = AdaptiveCard.ContentType
      }) as Activity
    }
  };

  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="75aa5-185">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="75aa5-185">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const submittedData = action.data;
    const adaptiveCard = CardFactory.adaptiveCard({
      actions: [
        { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
      ],
      body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submittedData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
        {
          choices: [
            { title: submittedData.Option1, value: submittedData.Option1 },
            { title: submittedData.Option2, value: submittedData.Option2 },
            { title: submittedData.Option3, value: submittedData.Option3 }
          ],
          id: 'Choices',
          isMultiSelect: submittedData.MultiSelect,
          style: 'expanded',
          type: 'Input.ChoiceSet'
        }
      ],
      type: 'AdaptiveCard',
      version: '1.0'
    });
    return {
      composeExtension: {
        activityPreview: MessageFactory.attachment(adaptiveCard, null, null, InputHints.ExpectingInput),
        type: 'botMessagePreview'
      }
    };
  }
}
```

# <a name="json"></a>[<span data-ttu-id="75aa5-186">JSON</span><span class="sxs-lookup"><span data-stu-id="75aa5-186">JSON</span></span>](#tab/json)

> [!NOTE]
> * <span data-ttu-id="75aa5-187">Le `activityPreview` doit contenir une `message` activité avec exactement une pièce jointe de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="75aa5-187">The `activityPreview` must contain a `message` activity with exactly one Adaptive Card attachment.</span></span> <span data-ttu-id="75aa5-188">La `<< Card Payload >>` valeur est un espace réservé pour la carte que vous souhaitez envoyer.</span><span class="sxs-lookup"><span data-stu-id="75aa5-188">The `<< Card Payload >>` value is a placeholder for the card you want to send.</span></span>

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

* * *

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="75aa5-189">Événements d'envoi et de modification botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="75aa5-189">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="75aa5-190">Votre extension de messagerie doit répondre à deux nouveaux types d'appel, `composeExtension/submitAction` où `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="75aa5-190">Your messaging extension must respond to two new types of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="75aa5-191">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="75aa5-191">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewEditAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="75aa5-192">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="75aa5-192">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionBotMessagePreviewEdit(context, action) {

    //handle the event
  }
  
  handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {

    //handle the event
  }
}

```

# <a name="json"></a>[<span data-ttu-id="75aa5-193">JSON</span><span class="sxs-lookup"><span data-stu-id="75aa5-193">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "edit | send",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

* * *

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="75aa5-194">Répondre à la modification botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="75aa5-194">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="75aa5-195">Si l'utilisateur modifie la carte avant l'envoi, en sélectionnant **Modifier,** vous recevez un `composeExtension/submitAction` appel avec `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="75aa5-195">If the user edits the card before sending, by selecting **Edit**, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="75aa5-196">Vous devez répondre en renvoyant le module de tâche que vous avez envoyé, en réponse à l'appel initial `composeExtension/fetchTask` qui a commencé l'interaction.</span><span class="sxs-lookup"><span data-stu-id="75aa5-196">You must respond by returning the task module you sent, in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="75aa5-197">Cela permet à l'utilisateur de démarrer le processus en entrant à nouveau les informations d'origine.</span><span class="sxs-lookup"><span data-stu-id="75aa5-197">This allows the user to start the process by re-entering the original information.</span></span> <span data-ttu-id="75aa5-198">Utilisez les informations disponibles pour mettre à jour le module de tâche afin que l'utilisateur n'a pas besoin de remplir toutes les informations de A à Z.</span><span class="sxs-lookup"><span data-stu-id="75aa5-198">Use the available information to update the task module so that the user need not fill out all information from scratch.</span></span>
<span data-ttu-id="75aa5-199">Pour plus d'informations sur la réponse à l'événement initial, voir `fetchTask` [répondre à l'événement `fetchTask` initial.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="75aa5-199">For more information on responding to the initial `fetchTask` event, see [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="75aa5-200">Répondre à l'envoi botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="75aa5-200">Respond to botMessagePreview send</span></span>

<span data-ttu-id="75aa5-201">Une fois que l'utilisateur a sélectionné **l'envoi,** vous recevez un `composeExtension/submitAction` appel avec `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="75aa5-201">After the user selects the **Send**, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="75aa5-202">Votre service web doit créer et envoyer un message proactif avec la carte adaptative à la conversation, ainsi que répondre à l'appel.</span><span class="sxs-lookup"><span data-stu-id="75aa5-202">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="75aa5-203">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="75aa5-203">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var activityPreview = action.BotActivityPreview[0];
  var attachmentContent = activityPreview.Attachments[0].Content;
  var previewedCard = JsonConvert.DeserializeObject<AdaptiveCard>(attachmentContent.ToString(),
          new JsonSerializerSettings { NullValueHandling = NullValueHandling.Ignore });
  
  previewedCard.Version = "1.0";

  var responseActivity = Activity.CreateMessageActivity();
  Attachment attachment = new Attachment()
  {
    ContentType = AdaptiveCard.ContentType,
    Content = previewedCard
  };
  responseActivity.Attachments.Add(attachment);
  
  // Attribute the message to the user on whose behalf the bot is posting
  responseActivity.ChannelData = new {
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }
  };
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="75aa5-204">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="75aa5-204">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {
      // The data has been returned to the bot in the action structure.
      const activityPreview = action.botActivityPreview[0];
      const attachmentContent = activityPreview.attachments[0].content;
      const userText = attachmentContent.body[1].text;
      const choiceSet = attachmentContent.body[3];

      const submitData = {
        MultiSelect: choiceSet.isMultiSelect ? 'true' : 'false',
        Option1: choiceSet.choices[0].title,
        Option2: choiceSet.choices[1].title,
        Option3: choiceSet.choices[2].title,
        Question: userText
      };

      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [
          { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
        ],
        body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submitData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
          {
            choices: [
                { title: submitData.Option1, value: submitData.Option1 },
                { title: submitData.Option2, value: submitData.Option2 },
                { title: submitData.Option3, value: submitData.Option3 }
            ],
            id: 'Choices',
            isMultiSelect: submitData.MultiSelect,
            style: 'expanded',
            type: 'Input.ChoiceSet'
          }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });
      const responseActivity = { type: 'message', attachments: [adaptiveCard], channelData: {
          onBehalfOf: [
              { itemId: 0, mentionType: 'person', mri: context.activity.from.id, displayname: context.activity.from.name }
          ]
      }};

      await context.sendActivity(responseActivity);
    }
}
```

# <a name="json"></a>[<span data-ttu-id="75aa5-205">JSON</span><span class="sxs-lookup"><span data-stu-id="75aa5-205">JSON</span></span>](#tab/json)

<span data-ttu-id="75aa5-206">Vous recevez un `composeExtension/submitAction` nouveau message semblable au suivant :</span><span class="sxs-lookup"><span data-stu-id="75aa5-206">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

* * *

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="75aa5-207">Attribution des utilisateurs pour les messages de bots</span><span class="sxs-lookup"><span data-stu-id="75aa5-207">User attribution for bots messages</span></span> 

<span data-ttu-id="75aa5-208">Dans les scénarios où un bot envoie des messages pour le compte d'un utilisateur, l'attribution du message à cet utilisateur facilite l'engagement et présente un flux d'interaction plus naturel.</span><span class="sxs-lookup"><span data-stu-id="75aa5-208">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user helps with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="75aa5-209">Cette fonctionnalité vous permet d'attribuer un message de votre bot à un utilisateur au nom de qui il a été envoyé.</span><span class="sxs-lookup"><span data-stu-id="75aa5-209">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="75aa5-210">Dans l'image suivante, à gauche se trouve un message de carte envoyé par un bot sans attribution d'utilisateur et à droite une carte envoyée par un bot avec attribution d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="75aa5-210">In the following image, on the left is a card message sent by a bot without user attribution and on the right is a card sent by a bot with user attribution.</span></span>

![bots d'attribution d'utilisateur](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="75aa5-212">Pour utiliser l'attribution d'utilisateur dans Teams, vous devez ajouter l'entité de mention à votre charge utile `OnBehalfOf` qui est envoyée à `ChannelData` `Activity` Teams.</span><span class="sxs-lookup"><span data-stu-id="75aa5-212">To use the user attribution in teams, you must add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="75aa5-213">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="75aa5-213">C#/.NET</span></span>](#tab/dotnet-1)

```csharp
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }

```

# <a name="json"></a>[<span data-ttu-id="75aa5-214">JSON</span><span class="sxs-lookup"><span data-stu-id="75aa5-214">JSON</span></span>](#tab/json-1)

```json
{
    "text": "Hello World!",
    "ChannelData": {
        "OnBehalfOf": [{
            "itemid": 0,
            "mentionType": "person",
            "mri": "29:orgid:89e6508d-6c0f-4ffe-9f6a-b58416d965ae",
            "displayName": "Sowrabh N R S"
        }]
    }
}
```

* * *

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="75aa5-215">Détails du  `OnBehalfOf` schéma d'entité</span><span class="sxs-lookup"><span data-stu-id="75aa5-215">Details of  `OnBehalfOf` entity schema</span></span>

<span data-ttu-id="75aa5-216">La section suivante décrit les entités du `OnBehalfOf` tableau :</span><span class="sxs-lookup"><span data-stu-id="75aa5-216">The following section is a description of the entities in the `OnBehalfOf` Array:</span></span>

|<span data-ttu-id="75aa5-217">Champ</span><span class="sxs-lookup"><span data-stu-id="75aa5-217">Field</span></span>|<span data-ttu-id="75aa5-218">Type</span><span class="sxs-lookup"><span data-stu-id="75aa5-218">Type</span></span>|<span data-ttu-id="75aa5-219">Description</span><span class="sxs-lookup"><span data-stu-id="75aa5-219">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="75aa5-220">Entier</span><span class="sxs-lookup"><span data-stu-id="75aa5-220">Integer</span></span>|<span data-ttu-id="75aa5-221">Décrit l'identification de l'élément.</span><span class="sxs-lookup"><span data-stu-id="75aa5-221">Describes identification of the item.</span></span> <span data-ttu-id="75aa5-222">Sa valeur doit être `0` .</span><span class="sxs-lookup"><span data-stu-id="75aa5-222">Its value must be `0`.</span></span>|
|`mentionType`|<span data-ttu-id="75aa5-223">Chaîne</span><span class="sxs-lookup"><span data-stu-id="75aa5-223">String</span></span>|<span data-ttu-id="75aa5-224">Décrit la mention d'une « personne ».</span><span class="sxs-lookup"><span data-stu-id="75aa5-224">Describes the mention of a "person".</span></span>|
|`mri`|<span data-ttu-id="75aa5-225">Chaîne</span><span class="sxs-lookup"><span data-stu-id="75aa5-225">String</span></span>|<span data-ttu-id="75aa5-226">Identificateur de ressource de message (IRM) de la personne au nom de laquelle le message est envoyé.</span><span class="sxs-lookup"><span data-stu-id="75aa5-226">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="75aa5-227">Le nom de l'expéditeur du message s'affiche comme « \<user\> \<bot name\> jusqu'à ».</span><span class="sxs-lookup"><span data-stu-id="75aa5-227">Message sender name would appear as "\<user\> through \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="75aa5-228">Chaîne</span><span class="sxs-lookup"><span data-stu-id="75aa5-228">String</span></span>|<span data-ttu-id="75aa5-229">Nom de la personne.</span><span class="sxs-lookup"><span data-stu-id="75aa5-229">Name of the person.</span></span> <span data-ttu-id="75aa5-230">Utilisé comme solution de retour en cas d'indisponibilité de la résolution des noms.</span><span class="sxs-lookup"><span data-stu-id="75aa5-230">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="code-sample"></a><span data-ttu-id="75aa5-231">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="75aa5-231">Code sample</span></span>

| <span data-ttu-id="75aa5-232">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="75aa5-232">Sample Name</span></span>           | <span data-ttu-id="75aa5-233">Description</span><span class="sxs-lookup"><span data-stu-id="75aa5-233">Description</span></span> | <span data-ttu-id="75aa5-234">.NET</span><span class="sxs-lookup"><span data-stu-id="75aa5-234">.NET</span></span>    | <span data-ttu-id="75aa5-235">Node.js</span><span class="sxs-lookup"><span data-stu-id="75aa5-235">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="75aa5-236">Action d'extension de messagerie Teams</span><span class="sxs-lookup"><span data-stu-id="75aa5-236">Teams messaging extension action</span></span>| <span data-ttu-id="75aa5-237">Décrit comment définir des commandes d'action, créer un module de tâche et répondre à une action d'soumission de module de tâche.</span><span class="sxs-lookup"><span data-stu-id="75aa5-237">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="75aa5-238">View</span><span class="sxs-lookup"><span data-stu-id="75aa5-238">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="75aa5-239">View</span><span class="sxs-lookup"><span data-stu-id="75aa5-239">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="75aa5-240">Recherche d’extension de messagerie Teams</span><span class="sxs-lookup"><span data-stu-id="75aa5-240">Teams messaging extension search</span></span>   |  <span data-ttu-id="75aa5-241">Décrit comment définir des commandes de recherche et répondre aux recherches.</span><span class="sxs-lookup"><span data-stu-id="75aa5-241">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="75aa5-242">View</span><span class="sxs-lookup"><span data-stu-id="75aa5-242">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="75aa5-243">View</span><span class="sxs-lookup"><span data-stu-id="75aa5-243">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="75aa5-244">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="75aa5-244">Next Step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75aa5-245">Définir les commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="75aa5-245">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

