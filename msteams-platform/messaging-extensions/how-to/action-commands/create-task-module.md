---
title: Créer et envoyer le module de tâches
author: clearab
description: Comment gérer l’action d’appel initiale et répondre avec un module de tâches à partir d’une commande d’extension de messagerie d’action
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f5f96e71517d45f52d17d2d70c583ec1eec3babd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673855"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="337a8-103">Créer et envoyer le module de tâches</span><span class="sxs-lookup"><span data-stu-id="337a8-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="337a8-104">Si vous ne remplissez pas votre module de tâches avec des paramètres définis dans le manifeste de votre application, vous devez créer le module de tâches qui doit être présenté aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="337a8-104">If you are not populating your task module with parameters defined in your app manifest, you'll need to create the task module to be presented to your users.</span></span> <span data-ttu-id="337a8-105">Vous pouvez utiliser une carte adaptative ou une vue Web incorporée.</span><span class="sxs-lookup"><span data-stu-id="337a8-105">You can use either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="337a8-106">La demande d’appel initiale</span><span class="sxs-lookup"><span data-stu-id="337a8-106">The initial invoke request</span></span>

<span data-ttu-id="337a8-107">À l’aide de cette méthode, vous `Activity` recevrez un `composeExtension/fetchTask`objet de type, et vous devrez répondre avec `task` un objet contenant soit la carte adaptative, soit une URL de l’affichage Web intégré.</span><span class="sxs-lookup"><span data-stu-id="337a8-107">Using this method you service will receive an `Activity` object of type `composeExtension/fetchTask`, and you'll need to respond with a `task` object containing either the adaptive card or a URL to the embedded web view.</span></span> <span data-ttu-id="337a8-108">En plus des propriétés d’activité de robot standard, la charge utile Invoke initiale contient les métadonnées de requête suivantes :</span><span class="sxs-lookup"><span data-stu-id="337a8-108">In addition to the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="337a8-109">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="337a8-109">Property name</span></span>|<span data-ttu-id="337a8-110">Objectif</span><span class="sxs-lookup"><span data-stu-id="337a8-110">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="337a8-111">Type de demande ; doit être `invoke`.</span><span class="sxs-lookup"><span data-stu-id="337a8-111">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="337a8-112">Type de commande qui est émise pour votre service.</span><span class="sxs-lookup"><span data-stu-id="337a8-112">Type of command that is issued to your service.</span></span> <span data-ttu-id="337a8-113">Sera `composeExtension/fetchTask`.</span><span class="sxs-lookup"><span data-stu-id="337a8-113">Will be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="337a8-114">ID de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="337a8-114">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="337a8-115">Nom de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="337a8-115">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="337a8-116">ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="337a8-116">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="337a8-117">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="337a8-117">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="337a8-118">ID de canal (si la demande a été effectuée dans un canal).</span><span class="sxs-lookup"><span data-stu-id="337a8-118">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="337a8-119">ID d’équipe (si la demande a été effectuée dans un canal).</span><span class="sxs-lookup"><span data-stu-id="337a8-119">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="337a8-120">Contient l’ID de la commande appelée.</span><span class="sxs-lookup"><span data-stu-id="337a8-120">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="337a8-121">Contexte ayant déclenché l’événement.</span><span class="sxs-lookup"><span data-stu-id="337a8-121">The context that triggered the event.</span></span> <span data-ttu-id="337a8-122">Sera `compose`.</span><span class="sxs-lookup"><span data-stu-id="337a8-122">Will be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="337a8-123">Le thème client de l’utilisateur, utile pour la mise en forme Web incorporée.</span><span class="sxs-lookup"><span data-stu-id="337a8-123">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="337a8-124">Est `default`, `contrast` ou `dark`.</span><span class="sxs-lookup"><span data-stu-id="337a8-124">Will be `default`, `contrast` or `dark`.</span></span> |

### <a name="example-fetchtask-request"></a><span data-ttu-id="337a8-125">Exemple de requête fetchTask</span><span class="sxs-lookup"><span data-stu-id="337a8-125">Example fetchTask request</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="337a8-126">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="337a8-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="337a8-127">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="337a8-127">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="337a8-128">JSON</span><span class="sxs-lookup"><span data-stu-id="337a8-128">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="337a8-129">Demande initiale d’appel à partir d’un message</span><span class="sxs-lookup"><span data-stu-id="337a8-129">Initial invoke request from a message</span></span>

<span data-ttu-id="337a8-130">Lorsque votre bot est appelé à partir d’un message plutôt que de la zone de composition ou de la barre `value` de commandes, l’objet de la demande initiale contiendra les détails du message à partir duquel votre extension de messagerie a été appelée.</span><span class="sxs-lookup"><span data-stu-id="337a8-130">When your bot is invoked from a message rather than the compose area or the command bar, the `value` object in the initial request will contain the details of the message your messaging extension was invoked from.</span></span> <span data-ttu-id="337a8-131">Vous trouverez ci-dessous un exemple de cet objet.</span><span class="sxs-lookup"><span data-stu-id="337a8-131">An example of this object is below.</span></span> <span data-ttu-id="337a8-132">Les `reactions` tableaux `mentions` et sont facultatifs et ne sont pas présents s’il n’y a pas de réactions ni de mentions dans le message d’origine.</span><span class="sxs-lookup"><span data-stu-id="337a8-132">The `reactions` and `mentions` arrays are optional, and will not be present if there are no reactions or mentions in the original message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="337a8-133">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="337a8-133">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="337a8-134">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="337a8-134">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="337a8-135">JSON</span><span class="sxs-lookup"><span data-stu-id="337a8-135">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="337a8-136">Répondre au fetchTask</span><span class="sxs-lookup"><span data-stu-id="337a8-136">Respond to the fetchTask</span></span>

<span data-ttu-id="337a8-137">Répondez à la demande Invoke avec `task` un objet qui contient soit `taskInfo` un objet avec la carte adaptative, soit une URL Web, ou un message de chaîne simple.</span><span class="sxs-lookup"><span data-stu-id="337a8-137">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the adaptive card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="337a8-138">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="337a8-138">Property name</span></span>|<span data-ttu-id="337a8-139">Objectif</span><span class="sxs-lookup"><span data-stu-id="337a8-139">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="337a8-140">Il peut s' `continue` agir soit de présenter un formulaire `message` , soit d’un menu contextuel simple.</span><span class="sxs-lookup"><span data-stu-id="337a8-140">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="337a8-141">Soit un `taskInfo` objet pour un formulaire, soit un `string` pour un message.</span><span class="sxs-lookup"><span data-stu-id="337a8-141">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="337a8-142">Le schéma de l’objet taskInfo est le suivant :</span><span class="sxs-lookup"><span data-stu-id="337a8-142">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="337a8-143">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="337a8-143">Property name</span></span>|<span data-ttu-id="337a8-144">Objectif</span><span class="sxs-lookup"><span data-stu-id="337a8-144">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="337a8-145">Titre du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="337a8-145">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="337a8-146">Peut être un entier (en pixels) ou `small`, `medium`,. `large`</span><span class="sxs-lookup"><span data-stu-id="337a8-146">Can be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="337a8-147">Peut être un entier (en pixels) ou `small`, `medium`,. `large`</span><span class="sxs-lookup"><span data-stu-id="337a8-147">Can be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="337a8-148">Carte adaptative définissant le formulaire (si vous en utilisez un).</span><span class="sxs-lookup"><span data-stu-id="337a8-148">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="337a8-149">URL à ouvrir dans le module de tâches en tant qu’affichage Web incorporé.</span><span class="sxs-lookup"><span data-stu-id="337a8-149">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="337a8-150">Si un client ne prend pas en charge la fonctionnalité de module de tâche, cette URL est ouverte dans un onglet de navigateur.</span><span class="sxs-lookup"><span data-stu-id="337a8-150">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="with-an-adaptive-card"></a><span data-ttu-id="337a8-151">Avec une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="337a8-151">With an adaptive card</span></span>

<span data-ttu-id="337a8-152">Lorsque vous utilisez une carte adaptative, vous devez répondre avec un `task` objet avec l' `value` objet contenant une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="337a8-152">When using an adaptive card, you'll need to respond with a `task` object with the `value` object containing an adaptive card.</span></span>

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a><span data-ttu-id="337a8-153">Exemple de réponse fetchTask avec une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="337a8-153">Example fetchTask response with an adaptive card</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="337a8-154">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="337a8-154">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="337a8-155">Cet exemple utilise le [package NuGet AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) en plus du kit de développement logiciel (SDK) de l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="337a8-155">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="337a8-156">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="337a8-156">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="337a8-157">JSON</span><span class="sxs-lookup"><span data-stu-id="337a8-157">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "card":
      {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ],
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json"
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a><span data-ttu-id="337a8-158">Avec une vue Web incorporée</span><span class="sxs-lookup"><span data-stu-id="337a8-158">With an embedded web view</span></span>

<span data-ttu-id="337a8-159">Lorsque vous utilisez une vue Web incorporée, vous devez répondre avec un `task` objet avec l' `value` objet contenant l’URL du formulaire Web que vous souhaitez charger.</span><span class="sxs-lookup"><span data-stu-id="337a8-159">When using an embedded web view, you'll need to respond with a `task` object with the `value` object containing the URL to the web form you'd like to load.</span></span> <span data-ttu-id="337a8-160">Les domaines de n’importe quelle URL que vous souhaitez charger doivent être inclus `validDomains` dans le tableau dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="337a8-160">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="337a8-161">Pour plus d’informations sur la création de votre vue Web incorporée, voir la [documentation du module tâches](~/task-modules-and-cards/what-are-task-modules.md) .</span><span class="sxs-lookup"><span data-stu-id="337a8-161">See the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md) for complete information on building your embedded web view.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="337a8-162">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="337a8-162">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="337a8-163">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="337a8-163">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="337a8-164">JSON</span><span class="sxs-lookup"><span data-stu-id="337a8-164">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

## <a name="next-steps"></a><span data-ttu-id="337a8-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="337a8-165">Next steps</span></span>

<span data-ttu-id="337a8-166">Si vous permettez à vos utilisateurs d’envoyer une réponse à partir du module de tâches, vous devez gérer l’action Submit.</span><span class="sxs-lookup"><span data-stu-id="337a8-166">If you allow your users to send a response back from the task module, you'll need to handle the submit action.</span></span>

* [<span data-ttu-id="337a8-167">Créer et répondre à l’aide d’un module de tâches</span><span class="sxs-lookup"><span data-stu-id="337a8-167">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
