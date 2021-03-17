---
title: Répondre à l’action d’soumission du module de tâche
author: clearab
description: Décrit comment répondre à l’action d’envoi du module de tâche à partir d’une commande d’action d’extension de messagerie
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fecc0ace5f767da3764529a9e8a590b37e547bb0
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827941"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="94df8-103">Répondre à l’action d’soumission du module de tâche</span><span class="sxs-lookup"><span data-stu-id="94df8-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="94df8-104">Une fois qu’un utilisateur a soumis le module de tâche, votre service web reçoit un message d’appel avec l’ID de commande et les valeurs `composeExtension/submitAction` de paramètre.</span><span class="sxs-lookup"><span data-stu-id="94df8-104">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="94df8-105">Votre application dispose de cinq secondes pour répondre à l’appel, sinon l’utilisateur reçoit un **message** d’erreur impossible d’atteindre l’application et toute réponse à l’appel est ignorée par le client Teams.</span><span class="sxs-lookup"><span data-stu-id="94df8-105">Your app has five seconds to respond to the invoke, otherwise the user receives an error message **Unable to reach the app** and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="94df8-106">Vous avez les options suivantes pour répondre :</span><span class="sxs-lookup"><span data-stu-id="94df8-106">You have the following options for responding:</span></span>

* <span data-ttu-id="94df8-107">Aucune réponse : vous pouvez choisir d’utiliser l’action d’soumission pour déclencher un processus dans un système externe et ne pas fournir de commentaires à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="94df8-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="94df8-108">Cela peut être utile pour les processus de longue durée, et vous pouvez choisir de fournir des commentaires d’une autre manière (par exemple, avec un [message proactif.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="94df8-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="94df8-109">[Autre module de tâche](#respond-with-another-task-module) : vous pouvez répondre avec un module de tâche supplémentaire dans le cadre d’une interaction en plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="94df8-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="94df8-110">[Réponse de carte](#respond-with-a-card-inserted-into-the-compose-message-area) : vous pouvez répondre avec une carte avec qui l’utilisateur peut interagir et/ou l’insérer dans un message.</span><span class="sxs-lookup"><span data-stu-id="94df8-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="94df8-111">[Carte adaptative à partir d’un bot](#bot-response-with-adaptive-card) : insérez une carte adaptative directement dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="94df8-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="94df8-112">Demander l’authentification de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="94df8-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="94df8-113">Demander à l’utilisateur de fournir une configuration supplémentaire</span><span class="sxs-lookup"><span data-stu-id="94df8-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="94df8-114">Pour l’authentification ou la configuration, une fois que l’utilisateur a terminé le flux, l’appel d’origine est renvoyé à votre service web.</span><span class="sxs-lookup"><span data-stu-id="94df8-114">For authentication or configuration, after the user completes the flow the original invoke is re-sent to your web service.</span></span> <span data-ttu-id="94df8-115">Le tableau suivant indique les types de réponses disponibles en fonction de l’emplacement d’appel `commandContext` de l’extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="94df8-115">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="94df8-116">Type de réponse</span><span class="sxs-lookup"><span data-stu-id="94df8-116">Response Type</span></span> | <span data-ttu-id="94df8-117">composer</span><span class="sxs-lookup"><span data-stu-id="94df8-117">compose</span></span> | <span data-ttu-id="94df8-118">barre de commande</span><span class="sxs-lookup"><span data-stu-id="94df8-118">command bar</span></span> | <span data-ttu-id="94df8-119">message</span><span class="sxs-lookup"><span data-stu-id="94df8-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="94df8-120">Réponse de carte</span><span class="sxs-lookup"><span data-stu-id="94df8-120">Card response</span></span> | <span data-ttu-id="94df8-121">x</span><span class="sxs-lookup"><span data-stu-id="94df8-121">x</span></span> | <span data-ttu-id="94df8-122">x</span><span class="sxs-lookup"><span data-stu-id="94df8-122">x</span></span> | <span data-ttu-id="94df8-123">x</span><span class="sxs-lookup"><span data-stu-id="94df8-123">x</span></span> |
|<span data-ttu-id="94df8-124">Un autre module de tâche</span><span class="sxs-lookup"><span data-stu-id="94df8-124">Another task module</span></span> | <span data-ttu-id="94df8-125">x</span><span class="sxs-lookup"><span data-stu-id="94df8-125">x</span></span> | <span data-ttu-id="94df8-126">x</span><span class="sxs-lookup"><span data-stu-id="94df8-126">x</span></span> | <span data-ttu-id="94df8-127">x</span><span class="sxs-lookup"><span data-stu-id="94df8-127">x</span></span> |
|<span data-ttu-id="94df8-128">Bot avec carte adaptative</span><span class="sxs-lookup"><span data-stu-id="94df8-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="94df8-129">x</span><span class="sxs-lookup"><span data-stu-id="94df8-129">x</span></span> |  | <span data-ttu-id="94df8-130">x</span><span class="sxs-lookup"><span data-stu-id="94df8-130">x</span></span> |
| <span data-ttu-id="94df8-131">Aucune réponse</span><span class="sxs-lookup"><span data-stu-id="94df8-131">No response</span></span> | <span data-ttu-id="94df8-132">x</span><span class="sxs-lookup"><span data-stu-id="94df8-132">x</span></span> | <span data-ttu-id="94df8-133">x</span><span class="sxs-lookup"><span data-stu-id="94df8-133">x</span></span> | <span data-ttu-id="94df8-134">x</span><span class="sxs-lookup"><span data-stu-id="94df8-134">x</span></span> |

> [!NOTE]
> * <span data-ttu-id="94df8-135">Lorsque vous sélectionnez **Action.Submit** par le biais de cartes ME, il envoie l’activité d’appel avec le nom **composeExtension**, où la valeur est égale à la charge utile habituelle.</span><span class="sxs-lookup"><span data-stu-id="94df8-135">When you select **Action.Submit** through ME cards, it sends invoke activity with the name **composeExtension**, where the value is equal to the usual payload.</span></span>
> * <span data-ttu-id="94df8-136">Lorsque vous sélectionnez **Action.Submit** par le biais d’une conversation, vous recevez une activité de message avec le nom **onCardButtonClicked**, où la valeur est égale à la charge utile habituelle.</span><span class="sxs-lookup"><span data-stu-id="94df8-136">When you select **Action.Submit** through conversation, you receive message activity with the name **onCardButtonClicked**, where the value is equal to the usual payload.</span></span>

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="94df8-137">Événement d’appel submitAction</span><span class="sxs-lookup"><span data-stu-id="94df8-137">The submitAction invoke event</span></span>

<span data-ttu-id="94df8-138">Voici quelques exemples de réception du message d’appel :</span><span class="sxs-lookup"><span data-stu-id="94df8-138">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="94df8-139">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="94df8-139">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="94df8-140">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="94df8-140">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="94df8-141">JSON</span><span class="sxs-lookup"><span data-stu-id="94df8-141">JSON</span></span>](#tab/json)

<span data-ttu-id="94df8-142">Voici un exemple de l’objet JSON que vous recevez.</span><span class="sxs-lookup"><span data-stu-id="94df8-142">This is an example of the JSON object you receive.</span></span> <span data-ttu-id="94df8-143">Le `commandContext` paramètre indique d’où votre extension de messagerie a été déclenchée.</span><span class="sxs-lookup"><span data-stu-id="94df8-143">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="94df8-144">`data`L’objet contient les champs du formulaire en tant que paramètres et les valeurs envoyées par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="94df8-144">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="94df8-145">L’objet JSON est raccourci ici pour mettre en évidence les champs les plus pertinents.</span><span class="sxs-lookup"><span data-stu-id="94df8-145">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="94df8-146">Répondre avec une carte insérée dans la zone composer un message</span><span class="sxs-lookup"><span data-stu-id="94df8-146">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="94df8-147">Le moyen le plus courant de répondre à la demande consiste à insérer une carte `composeExtension/submitAction` dans la zone de composition d’un message.</span><span class="sxs-lookup"><span data-stu-id="94df8-147">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="94df8-148">L’utilisateur peut ensuite choisir d’envoyer la carte à la conversation.</span><span class="sxs-lookup"><span data-stu-id="94df8-148">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="94df8-149">Pour plus d’informations sur l’utilisation des cartes, voir [cartes et actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="94df8-149">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="94df8-150">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="94df8-150">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="94df8-151">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="94df8-151">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="94df8-152">JSON</span><span class="sxs-lookup"><span data-stu-id="94df8-152">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="94df8-153">Répondre avec un autre module de tâche</span><span class="sxs-lookup"><span data-stu-id="94df8-153">Respond with another task module</span></span>

<span data-ttu-id="94df8-154">Vous pouvez choisir de répondre à `submitAction` l’événement avec un module de tâche supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="94df8-154">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="94df8-155">Cela peut être utile dans les cas ci-après :</span><span class="sxs-lookup"><span data-stu-id="94df8-155">This can be useful when:</span></span>

* <span data-ttu-id="94df8-156">Vous devez collecter de grandes quantités d’informations.</span><span class="sxs-lookup"><span data-stu-id="94df8-156">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="94df8-157">Si vous devez modifier dynamiquement les informations que vous collectez en fonction de l’entrée de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="94df8-157">If you need to dynamically change what information you are collecting based on user input</span></span>
* <span data-ttu-id="94df8-158">Si vous devez valider les informations envoyées par l’utilisateur et éventuellement renvoyer le formulaire avec un message d’erreur en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="94df8-158">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="94df8-159">La méthode de réponse est la même que [pour répondre à l’événement `fetchTask` initial.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="94df8-159">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="94df8-160">Si vous utilisez le SDK Bot Framework, les mêmes déclencheurs d’événements pour les deux actions d’soumission.</span><span class="sxs-lookup"><span data-stu-id="94df8-160">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="94df8-161">Cela signifie que vous devez ajouter une logique qui détermine la réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="94df8-161">This means you must add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="94df8-162">Réponse du bot avec carte adaptative</span><span class="sxs-lookup"><span data-stu-id="94df8-162">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="94df8-163">Ce flux nécessite que vous ajoutiez l’objet au manifeste de votre application et que l’étendue nécessaire soit définie `bot` pour le bot.</span><span class="sxs-lookup"><span data-stu-id="94df8-163">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="94df8-164">Utilisez le même ID que votre extension de messagerie pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="94df8-164">Use the same ID as your messaging extension for your bot.</span></span>

<span data-ttu-id="94df8-165">Vous pouvez également répondre à l’action d’envoyer en insérant un message avec une carte adaptative dans le canal avec un bot.</span><span class="sxs-lookup"><span data-stu-id="94df8-165">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="94df8-166">Votre utilisateur peut afficher un aperçu du message avant de l’envoyer, et éventuellement le modifier ou interagir avec celui-ci.</span><span class="sxs-lookup"><span data-stu-id="94df8-166">Your user can preview the message before submitting it, and potentially edit or interact with it as well.</span></span> <span data-ttu-id="94df8-167">Cela peut être très utile dans les scénarios où vous collectez des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative, ou lorsque vous mettez à jour la carte après qu’une personne interagit avec elle.</span><span class="sxs-lookup"><span data-stu-id="94df8-167">This can be very useful in scenarios where you gather information from your users before creating an adaptive card response, or when you update the card after someone interacts with it.</span></span> <span data-ttu-id="94df8-168">Le scénario suivant montre comment l’application Polly utilise ce flux pour configurer un sondage sans inclure les étapes de configuration dans la conversation de canal :</span><span class="sxs-lookup"><span data-stu-id="94df8-168">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation:</span></span>

1. <span data-ttu-id="94df8-169">L’utilisateur sélectionne l’extension de messagerie pour déclencher le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="94df8-169">The user selects the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="94df8-170">L’utilisateur configure le sondage avec le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="94df8-170">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="94df8-171">Après avoir soumis le module de tâche, l’application utilise les informations fournies pour créer le sondage en tant que carte adaptative et l’envoie en réponse `botMessagePreview` au client.</span><span class="sxs-lookup"><span data-stu-id="94df8-171">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="94df8-172">L’utilisateur peut ensuite afficher un aperçu du message de carte adaptative avant que le bot l’insère dans le canal.</span><span class="sxs-lookup"><span data-stu-id="94df8-172">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="94df8-173">Si l’application n’est pas déjà membre du canal, la sélection `Send` l’ajoute.</span><span class="sxs-lookup"><span data-stu-id="94df8-173">If the app is not already a member of the channel, selecting `Send` adds it.</span></span>
   1. <span data-ttu-id="94df8-174">L’utilisateur peut également choisir le message, qui le renvoie au module de `Edit` tâche d’origine.</span><span class="sxs-lookup"><span data-stu-id="94df8-174">The user can also choose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="94df8-175">L’interaction avec la carte adaptative modifie le message avant de l’envoyer.</span><span class="sxs-lookup"><span data-stu-id="94df8-175">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="94df8-176">Une fois que l’utilisateur `Send` a sélectionné le bot, il publie le message sur le canal.</span><span class="sxs-lookup"><span data-stu-id="94df8-176">After the user selects `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="94df8-177">Répondre à l’action d’soumission initiale</span><span class="sxs-lookup"><span data-stu-id="94df8-177">Respond to initial submit action</span></span>

<span data-ttu-id="94df8-178">Pour activer ce flux, votre module de tâche doit répondre au message initial avec un aperçu de la carte que le `composeExtension/submitAction` bot envoie au canal.</span><span class="sxs-lookup"><span data-stu-id="94df8-178">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot send to the channel.</span></span> <span data-ttu-id="94df8-179">Cela permet à l’utilisateur de vérifier la carte avant son envoi et d’essayer d’installer votre bot dans la conversation s’il n’est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="94df8-179">This gives the user the opportunity to verify the card before sending, and also attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="94df8-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="94df8-180">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="94df8-181">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="94df8-181">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="94df8-182">JSON</span><span class="sxs-lookup"><span data-stu-id="94df8-182">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="94df8-183">Le `activityPreview` doit contenir une activité avec exactement 1 pièce jointe `message` de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="94df8-183">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="94df8-184">La `<< Card Payload >>` valeur est un espace réservé pour la carte que vous souhaitez envoyer.</span><span class="sxs-lookup"><span data-stu-id="94df8-184">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="94df8-185">Événements d’envoi et de modification botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="94df8-185">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="94df8-186">Votre extension de message doit répondre maintenant à deux nouvelles variétés de `composeExtension/submitAction` l’appel, où `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="94df8-186">Your message extension must respond now to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="94df8-187">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="94df8-187">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="94df8-188">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="94df8-188">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="94df8-189">JSON</span><span class="sxs-lookup"><span data-stu-id="94df8-189">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="94df8-190">Répondre à la modification botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="94df8-190">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="94df8-191">Si l’utilisateur modifie la carte avant  de l’envoyer en sélectionnant le bouton Modifier, vous recevez un `composeExtension/submitAction` appel avec `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="94df8-191">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="94df8-192">Vous devez généralement répondre en renvoyant le module de tâche que vous avez envoyé en réponse à l’appel initial `composeExtension/fetchTask` qui a commencé l’interaction.</span><span class="sxs-lookup"><span data-stu-id="94df8-192">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="94df8-193">Cela permet à l’utilisateur de recommencer le processus en entrant à nouveau les informations d’origine.</span><span class="sxs-lookup"><span data-stu-id="94df8-193">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="94df8-194">Utilisez les informations disponibles pour pré-remplir le module de tâche afin que l’utilisateur n’a pas à remplir toutes les informations à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="94df8-194">Use the available information to pre-populate the task module so the user does not have to fill out all of the information from scratch.</span></span>

<span data-ttu-id="94df8-195">Voir [la réponse à l’événement `fetchTask` initial.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="94df8-195">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="94df8-196">Répondre à l’envoi botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="94df8-196">Respond to botMessagePreview send</span></span>

<span data-ttu-id="94df8-197">Une fois que l’utilisateur a sélectionné le **bouton** Envoyer, vous recevez un `composeExtension/submitAction` appel avec `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="94df8-197">After the user selects the **Send** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="94df8-198">Votre service web doit créer et envoyer un message proactif avec la carte adaptative à la conversation, ainsi que répondre à l’appel.</span><span class="sxs-lookup"><span data-stu-id="94df8-198">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="94df8-199">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="94df8-199">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="94df8-200">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="94df8-200">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="94df8-201">JSON</span><span class="sxs-lookup"><span data-stu-id="94df8-201">JSON</span></span>](#tab/json)

<span data-ttu-id="94df8-202">Vous recevez un `composeExtension/submitAction` nouveau message semblable au suivant :</span><span class="sxs-lookup"><span data-stu-id="94df8-202">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="94df8-203">Attribution des utilisateurs pour les messages de bots</span><span class="sxs-lookup"><span data-stu-id="94df8-203">User attribution for bots messages</span></span> 

<span data-ttu-id="94df8-204">Dans les scénarios où un bot envoie des messages pour le compte d’un utilisateur, l’attribution du message à cet utilisateur peut aider à l’engagement et à présenter un flux d’interaction plus naturel.</span><span class="sxs-lookup"><span data-stu-id="94df8-204">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="94df8-205">Cette fonctionnalité vous permet d’attribuer un message de votre bot à un utilisateur au nom de qui il a été envoyé.</span><span class="sxs-lookup"><span data-stu-id="94df8-205">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="94df8-206">Dans l’image suivante, à gauche se trouve un message de carte envoyé par un *bot* sans attribution d’utilisateur et à droite une carte envoyée par un *bot* avec attribution d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="94df8-206">In the following image, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![Capture d’écran](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="94df8-208">Pour utiliser l’attribution d’utilisateur dans Teams, vous devez ajouter l’entité de mention à votre charge utile `OnBehalfOf` qui est envoyée à `ChannelData` `Activity` Teams.</span><span class="sxs-lookup"><span data-stu-id="94df8-208">To use the user attribution in teams, you must  add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="94df8-209">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="94df8-209">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="94df8-210">JSON</span><span class="sxs-lookup"><span data-stu-id="94df8-210">JSON</span></span>](#tab/json-1)

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

<span data-ttu-id="94df8-211">La section suivante décrit les entités du `OnBehalfOf` tableau :</span><span class="sxs-lookup"><span data-stu-id="94df8-211">The following section is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="94df8-212">Détails du  `OnBehalfOf` schéma d’entité</span><span class="sxs-lookup"><span data-stu-id="94df8-212">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="94df8-213">Champ</span><span class="sxs-lookup"><span data-stu-id="94df8-213">Field</span></span>|<span data-ttu-id="94df8-214">Type</span><span class="sxs-lookup"><span data-stu-id="94df8-214">Type</span></span>|<span data-ttu-id="94df8-215">Description</span><span class="sxs-lookup"><span data-stu-id="94df8-215">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="94df8-216">Entier</span><span class="sxs-lookup"><span data-stu-id="94df8-216">Integer</span></span>|<span data-ttu-id="94df8-217">Doit être 0</span><span class="sxs-lookup"><span data-stu-id="94df8-217">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="94df8-218">String</span><span class="sxs-lookup"><span data-stu-id="94df8-218">String</span></span>|<span data-ttu-id="94df8-219">Doit être « person »</span><span class="sxs-lookup"><span data-stu-id="94df8-219">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="94df8-220">String</span><span class="sxs-lookup"><span data-stu-id="94df8-220">String</span></span>|<span data-ttu-id="94df8-221">Identificateur de ressource de message (IRM) de la personne au nom de laquelle le message est envoyé.</span><span class="sxs-lookup"><span data-stu-id="94df8-221">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="94df8-222">Le nom de l’expéditeur du message s’affiche comme « \<user\> via \<bot name\> ».</span><span class="sxs-lookup"><span data-stu-id="94df8-222">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="94df8-223">String</span><span class="sxs-lookup"><span data-stu-id="94df8-223">String</span></span>|<span data-ttu-id="94df8-224">Nom de la personne.</span><span class="sxs-lookup"><span data-stu-id="94df8-224">Name of the person.</span></span> <span data-ttu-id="94df8-225">Utilisé comme solution de retour en cas d’indisponibilité de la résolution des noms.</span><span class="sxs-lookup"><span data-stu-id="94df8-225">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="94df8-226">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94df8-226">Next Steps</span></span>

<span data-ttu-id="94df8-227">Ajouter une commande de recherche</span><span class="sxs-lookup"><span data-stu-id="94df8-227">Add a search command</span></span>

* [<span data-ttu-id="94df8-228">Définir les commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="94df8-228">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
