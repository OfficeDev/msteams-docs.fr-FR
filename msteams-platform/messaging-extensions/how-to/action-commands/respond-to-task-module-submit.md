---
title: Répondre à l’action soumettre du module de tâche
author: clearab
description: Indique comment répondre à l’action d’envoi d’un module de tâche à partir d’une commande action d’extension de messagerie
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: a876275f5f4f9c3a7c1fea275eecb9c26b780fd0
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2020
ms.locfileid: "45103012"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="6d3ff-103">Répondre à l’action soumettre du module de tâche</span><span class="sxs-lookup"><span data-stu-id="6d3ff-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="6d3ff-104">Une fois qu’un utilisateur soumet le module de tâche, votre service Web reçoit un `composeExtension/submitAction` message d’appel avec l’ID de commande et les valeurs de paramètre définies.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-104">Once a user submits the task module, your web service will receive a `composeExtension/submitAction` invoke message with the command id and parameter values set.</span></span> <span data-ttu-id="6d3ff-105">Votre application disposera de cinq secondes pour répondre à l’appel, sinon l’utilisateur recevra un message d’erreur « Impossible d’atteindre l’application », et toute réponse à l’appel sera ignorée par le client Teams.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-105">Your app will have five seconds to respond to the invoke, otherwise the user will receive an "Unable to reach the app" error message, and any reply to the invoke will be ignored by the Teams client.</span></span>

<span data-ttu-id="6d3ff-106">Vous disposez des options suivantes pour répondre.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-106">You have the following options for responding.</span></span>

* <span data-ttu-id="6d3ff-107">Aucune réponse : vous pouvez choisir d’utiliser l’action envoyer pour déclencher un processus dans un système externe et ne pas fournir de commentaires à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="6d3ff-108">Cela peut être utile pour les processus de longue durée et vous pouvez choisir de fournir des commentaires d’une autre manière (par exemple, avec un [message proactif](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="6d3ff-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="6d3ff-109">[Un autre module de tâches](#respond-with-another-task-module) -vous pouvez répondre avec un module de tâche supplémentaire dans le cadre d’une interaction en plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="6d3ff-110">[Réponse](#respond-with-a-card-inserted-into-the-compose-message-area) de la carte : vous pouvez répondre avec une carte à laquelle l’utilisateur peut interagir et/ou insérer dans un message.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="6d3ff-111">[Carte adaptative à partir de bot](#bot-response-with-adaptive-card) : Insérez une carte adaptative directement dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="6d3ff-112">Demander à l’utilisateur de s’authentifier</span><span class="sxs-lookup"><span data-stu-id="6d3ff-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="6d3ff-113">Demander à l’utilisateur de fournir une configuration supplémentaire</span><span class="sxs-lookup"><span data-stu-id="6d3ff-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="6d3ff-114">Le tableau ci-dessous indique les types de réponses disponibles en fonction de l’emplacement `commandContext` d’appel () de l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-114">The table below shows which types of responses are available based on the invoke location (`commandContext`) of the messaging extension.</span></span> <span data-ttu-id="6d3ff-115">Pour l’authentification ou la configuration, une fois que l’utilisateur a terminé le flux, l’appel d’origine sera renvoyé à votre service Web.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-115">For authentication or configuration, once the user completes the flow the original invoke will be re-sent to your web service.</span></span>

|<span data-ttu-id="6d3ff-116">Type de réponse</span><span class="sxs-lookup"><span data-stu-id="6d3ff-116">Response Type</span></span> | <span data-ttu-id="6d3ff-117">composition</span><span class="sxs-lookup"><span data-stu-id="6d3ff-117">compose</span></span> | <span data-ttu-id="6d3ff-118">barre de commande</span><span class="sxs-lookup"><span data-stu-id="6d3ff-118">command bar</span></span> | <span data-ttu-id="6d3ff-119">message</span><span class="sxs-lookup"><span data-stu-id="6d3ff-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="6d3ff-120">Réponse de carte</span><span class="sxs-lookup"><span data-stu-id="6d3ff-120">Card response</span></span> | <span data-ttu-id="6d3ff-121">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-121">x</span></span> | <span data-ttu-id="6d3ff-122">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-122">x</span></span> | <span data-ttu-id="6d3ff-123">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-123">x</span></span> |
|<span data-ttu-id="6d3ff-124">Un autre module de tâches</span><span class="sxs-lookup"><span data-stu-id="6d3ff-124">Another task module</span></span> | <span data-ttu-id="6d3ff-125">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-125">x</span></span> | <span data-ttu-id="6d3ff-126">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-126">x</span></span> | <span data-ttu-id="6d3ff-127">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-127">x</span></span> |
|<span data-ttu-id="6d3ff-128">Robot avec carte adaptative</span><span class="sxs-lookup"><span data-stu-id="6d3ff-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="6d3ff-129">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-129">x</span></span> |  | <span data-ttu-id="6d3ff-130">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-130">x</span></span> |
| <span data-ttu-id="6d3ff-131">Aucune réponse</span><span class="sxs-lookup"><span data-stu-id="6d3ff-131">No response</span></span> | <span data-ttu-id="6d3ff-132">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-132">x</span></span> | <span data-ttu-id="6d3ff-133">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-133">x</span></span> | <span data-ttu-id="6d3ff-134">x</span><span class="sxs-lookup"><span data-stu-id="6d3ff-134">x</span></span> |

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="6d3ff-135">Événement d’appel submitAction</span><span class="sxs-lookup"><span data-stu-id="6d3ff-135">The submitAction invoke event</span></span>

<span data-ttu-id="6d3ff-136">Vous trouverez ci-dessous des exemples de réception du message d’appel.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-136">Below are examples of receiving the invoke message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6d3ff-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6d3ff-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6d3ff-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6d3ff-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="6d3ff-139">JSON</span><span class="sxs-lookup"><span data-stu-id="6d3ff-139">JSON</span></span>](#tab/json)

<span data-ttu-id="6d3ff-140">Voici un exemple de l’objet JSON que vous recevrez.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-140">This is an example of the JSON object you will receive.</span></span> <span data-ttu-id="6d3ff-141">Le `commandContext` paramètre indique l’emplacement à partir duquel votre extension de messagerie a été déclenchée.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-141">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="6d3ff-142">L' `data` objet contient les champs du formulaire en tant que paramètres, ainsi que les valeurs que l’utilisateur a envoyées.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-142">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="6d3ff-143">L’objet JSON ici est raccourci pour mettre en surbrillance les champs les plus pertinents.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-143">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="6d3ff-144">Répondre avec une carte insérée dans la zone de message de composition</span><span class="sxs-lookup"><span data-stu-id="6d3ff-144">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="6d3ff-145">La façon la plus courante de répondre à la `composeExtension/submitAction` demande est d’insérer une carte insérée dans la zone de message de composition.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-145">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="6d3ff-146">L’utilisateur peut alors choisir de soumettre la carte à la conversation.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-146">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="6d3ff-147">Pour plus d’informations sur l’utilisation des cartes [, voir cartes et](~/task-modules-and-cards/cards/cards-actions.md)cartes.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-147">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6d3ff-148">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6d3ff-148">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    dynamic Data = JObject.Parse(action.Data.ToString());
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var card = new HeroCard
    {
        Title = Data["formField1"] as string,
        Subtitle = Data["formField2"]  as string,
        Text = Data["formField3"]  as string,
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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6d3ff-149">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6d3ff-149">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6d3ff-150">JSON</span><span class="sxs-lookup"><span data-stu-id="6d3ff-150">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="6d3ff-151">Répondre à l’aide d’un autre module de tâches</span><span class="sxs-lookup"><span data-stu-id="6d3ff-151">Respond with another task module</span></span>

<span data-ttu-id="6d3ff-152">Vous pouvez choisir de répondre à l' `submitAction` événement à l’aide d’un module de tâche supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-152">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="6d3ff-153">Cela peut être utile dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="6d3ff-153">This can be useful when:</span></span>

* <span data-ttu-id="6d3ff-154">Vous devez collecter de grandes quantités d’informations.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-154">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="6d3ff-155">Si vous devez modifier dynamiquement les informations que vous collectez en fonction de l’entrée de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6d3ff-155">If you need to dynamically change what information you're collecting based on user input</span></span>
* <span data-ttu-id="6d3ff-156">Si vous devez valider les informations envoyées par l’utilisateur et éventuellement renvoyer le formulaire avec un message d’erreur si un problème se produit.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-156">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="6d3ff-157">La méthode pour la réponse est la même que pour [répondre à l' `fetchTask` événement initial](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="6d3ff-157">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="6d3ff-158">Si vous utilisez le kit de développement logiciel (SDK) de robot, le même événement se déclenche pour les deux actions d’envoi.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-158">If you're using the Bot Framework SDK the same event will trigger for both submit actions.</span></span> <span data-ttu-id="6d3ff-159">Cela signifie que vous devez être sûr d’ajouter une logique qui détermine la bonne réponse.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-159">This mean you need to be sure to add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="6d3ff-160">Réponse à un bot avec carte adaptative</span><span class="sxs-lookup"><span data-stu-id="6d3ff-160">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="6d3ff-161">Ce flux nécessite que vous ajoutiez l' `bot` objet à votre manifeste d’application et que vous disposez de l’étendue nécessaire définie pour le bot.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-161">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="6d3ff-162">Utilisez le même ID que votre extension de messagerie pour votre robot.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-162">Use the same Id as your messaging extension for your bot.</span></span>

<span data-ttu-id="6d3ff-163">Vous pouvez également répondre à l’action d’envoi en insérant un message avec une carte adaptative dans le canal avec un bot.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-163">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="6d3ff-164">Votre utilisateur pourra prévisualiser le message avant de l’envoyer et éventuellement modifier/interagir avec.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-164">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="6d3ff-165">Cela peut être très utile dans les scénarios où vous devez recueillir des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative, ou lorsque vous devez mettre à jour la carte après qu’une personne interagit avec elle.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-165">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response, or when you're going to need to update the card after someone interacts with it.</span></span> <span data-ttu-id="6d3ff-166">Le scénario suivant montre comment l’application Polly utilise ce flux pour configurer un sondage sans inclure les étapes de configuration dans la conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-166">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation.</span></span>

1. <span data-ttu-id="6d3ff-167">L’utilisateur clique sur l’extension de messagerie pour déclencher le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-167">The user clicks the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="6d3ff-168">L’utilisateur configure le sondage avec le module tâches.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-168">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="6d3ff-169">Après avoir soumis le module de tâches, l’application utilise les informations fournies pour créer le sondage en tant que carte adaptative et l’envoie en `botMessagePreview` réponse au client.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-169">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="6d3ff-170">L’utilisateur peut alors prévisualiser le message de la carte adaptative avant de l’insérer dans le canal.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-170">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="6d3ff-171">Si l’application n’est pas déjà membre du canal, le fait de cliquer sur `Send` l’ajoutera.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-171">If the app is not already a member of the channel, clicking `Send` will add the it.</span></span>
   1. <span data-ttu-id="6d3ff-172">L’utilisateur peut également choisir d' `Edit` utiliser le message, qui le renvoie au module de tâche d’origine.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-172">The user can also chose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="6d3ff-173">L’interaction avec la carte adaptative modifie le message avant de l’envoyer.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-173">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="6d3ff-174">Une fois que l’utilisateur clique sur `Send` le robot envoie le message au canal.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-174">Once the user clicks `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="6d3ff-175">Répondre à l’action d’envoi initiale</span><span class="sxs-lookup"><span data-stu-id="6d3ff-175">Respond to initial submit action</span></span>

<span data-ttu-id="6d3ff-176">Pour activer ce flux, votre module de tâches doit répondre au `composeExtension/submitAction` message initial avec un aperçu de la carte que le bot enverra au canal.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-176">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot will send to the channel.</span></span> <span data-ttu-id="6d3ff-177">Cela permet à l’utilisateur de vérifier la carte avant de l’envoyer et d’essayer d’installer votre robot dans la conversation si celle-ci n’est pas déjà installée.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-177">This gives the user the opportunity to verify the card before sending, and also will attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6d3ff-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6d3ff-178">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic Data = JObject.Parse(action.Data.ToString());
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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6d3ff-179">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6d3ff-179">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6d3ff-180">JSON</span><span class="sxs-lookup"><span data-stu-id="6d3ff-180">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="6d3ff-181">Le `activityPreview` doit contenir une `message` activité avec exactement 1 pièce jointe de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-181">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="6d3ff-182">La `<< Card Payload >>` valeur est un espace réservé pour la carte que vous souhaitez envoyer.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-182">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="6d3ff-183">Événements d’envoi et de modification botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="6d3ff-183">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="6d3ff-184">Votre extension de message doit maintenant répondre à deux nouvelles variétés de l' `composeExtension/submitAction` appel, où `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="6d3ff-184">Your message extension will now need to respond to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6d3ff-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6d3ff-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6d3ff-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6d3ff-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6d3ff-187">JSON</span><span class="sxs-lookup"><span data-stu-id="6d3ff-187">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="6d3ff-188">Répondre à botMessagePreview modifier</span><span class="sxs-lookup"><span data-stu-id="6d3ff-188">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="6d3ff-189">Si l’utilisateur décide de modifier la carte avant de l’envoyer en cliquant sur le bouton **modifier** , vous recevrez un `composeExtension/submitAction` appel avec `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="6d3ff-189">If the user decides to edit the card before sending by clicking the **Edit** button, you will receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="6d3ff-190">Vous devez généralement répondre en renvoyant le module de tâches que vous avez envoyé en réponse à l' `composeExtension/fetchTask` appel initial qui a commencé l’interaction.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-190">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="6d3ff-191">Cela permet à l’utilisateur de commencer le processus en entrant de nouveau les informations d’origine.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-191">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="6d3ff-192">Vous devez également envisager d’utiliser les informations dont vous disposez maintenant pour pré-remplir le module de tâche afin que l’utilisateur n’ait pas rempli toutes les informations de toutes pièces.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-192">You should also consider using the information you now have available to pre-populate the task module so the user doesn't have fill out all of the information from scratch.</span></span>

<span data-ttu-id="6d3ff-193">Consultez [la rubrique relative à la réponse à l' `fetchTask` événement initial](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="6d3ff-193">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="6d3ff-194">Répondre à l’envoi botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="6d3ff-194">Respond to botMessagePreview send</span></span>

<span data-ttu-id="6d3ff-195">Une fois que l’utilisateur clique sur le bouton **Envoyer** , vous recevrez un `composeExtension/submitAction` appel avec `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="6d3ff-195">Once the user clicks the **Send** button, you will receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="6d3ff-196">Votre service Web devra créer et envoyer un message proactif avec la carte adaptative à la conversation, ainsi que répondre à l’appel.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-196">Your web service will need to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6d3ff-197">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6d3ff-197">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6d3ff-198">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6d3ff-198">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6d3ff-199">JSON</span><span class="sxs-lookup"><span data-stu-id="6d3ff-199">JSON</span></span>](#tab/json)

<span data-ttu-id="6d3ff-200">Vous recevrez un nouveau `composeExtension/submitAction` message similaire à celui ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-200">You will receive a new `composeExtension/submitAction` message similar to the one below.</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="6d3ff-201">Attribution d’utilisateur pour les messages robots</span><span class="sxs-lookup"><span data-stu-id="6d3ff-201">User attribution for bots messages</span></span> 

<span data-ttu-id="6d3ff-202">Dans les scénarios où un bot envoie des messages au nom d’un utilisateur, l’attribution du message à cet utilisateur peut contribuer à l’engagement et présenter un flux d’interaction plus naturel.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-202">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="6d3ff-203">Cette fonctionnalité vous permet d’envoyer des messages au nom de l’utilisateur qui initie le message.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-203">This feature allows you to send messages on behalf of the user who is initiating the message.</span></span>

<span data-ttu-id="6d3ff-204">Dans l’image ci-dessous, à gauche se trouve un message de carte envoyé par un bot *sans* attribution d’utilisateur et à droite est une carte envoyée par un bot *avec* attribution utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-204">In the image below, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![Capture d’écran](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="6d3ff-206">Pour utiliser l’attribution utilisateur dans Teams, vous devez ajouter l' `OnBehalfOf` entité mentionner à `ChannelData` dans votre `Activity` charge utile envoyée à Teams.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-206">To use user attribution in teams, you need to add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6d3ff-207">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6d3ff-207">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="6d3ff-208">JSON</span><span class="sxs-lookup"><span data-stu-id="6d3ff-208">JSON</span></span>](#tab/json-1)

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

<span data-ttu-id="6d3ff-209">Vous trouverez ci-dessous une description des entités du `OnBehalfOf` tableau :</span><span class="sxs-lookup"><span data-stu-id="6d3ff-209">Below is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="6d3ff-210">Détails du `OnBehalfOf` schéma d’entité</span><span class="sxs-lookup"><span data-stu-id="6d3ff-210">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="6d3ff-211">Champ</span><span class="sxs-lookup"><span data-stu-id="6d3ff-211">Field</span></span>|<span data-ttu-id="6d3ff-212">Type</span><span class="sxs-lookup"><span data-stu-id="6d3ff-212">Type</span></span>|<span data-ttu-id="6d3ff-213">Description</span><span class="sxs-lookup"><span data-stu-id="6d3ff-213">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="6d3ff-214">Entier</span><span class="sxs-lookup"><span data-stu-id="6d3ff-214">Integer</span></span>|<span data-ttu-id="6d3ff-215">Doit être égal à 0</span><span class="sxs-lookup"><span data-stu-id="6d3ff-215">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="6d3ff-216">Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d3ff-216">String</span></span>|<span data-ttu-id="6d3ff-217">Doit être « person »</span><span class="sxs-lookup"><span data-stu-id="6d3ff-217">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="6d3ff-218">Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d3ff-218">String</span></span>|<span data-ttu-id="6d3ff-219">Identificateur de ressource de message (MRI) de la personne au nom de laquelle le message est envoyé.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-219">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="6d3ff-220">Le nom de l’expéditeur du message apparaît sous la forme « \<user\> via \<bot name\> ».</span><span class="sxs-lookup"><span data-stu-id="6d3ff-220">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="6d3ff-221">Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d3ff-221">String</span></span>|<span data-ttu-id="6d3ff-222">Nom de la personne.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-222">Name of the person.</span></span> <span data-ttu-id="6d3ff-223">Utilisé comme secours en cas d’indisponibilité de la résolution de noms.</span><span class="sxs-lookup"><span data-stu-id="6d3ff-223">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="6d3ff-224">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d3ff-224">Next Steps</span></span>

<span data-ttu-id="6d3ff-225">Ajouter une commande de recherche</span><span class="sxs-lookup"><span data-stu-id="6d3ff-225">Add a search command</span></span>

* [<span data-ttu-id="6d3ff-226">Définir les commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="6d3ff-226">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
