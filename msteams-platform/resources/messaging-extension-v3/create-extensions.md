---
title: Lancer des actions avec des extensions de messagerie
description: Créer des extensions de messagerie basées sur l’action pour permettre aux utilisateurs de déclencher des services externes
localization_priority: Normal
ms.topic: how-to
keywords: équipes de messagerie extensions de recherche d’extensions de messagerie
ms.openlocfilehash: bfb3295726c355164f080c15e3759ea36a99d914
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566739"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="9eae3-104">Lancer des actions avec des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="9eae3-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="9eae3-105">Les extensions de messagerie basées sur l’action permettent à vos utilisateurs de déclencher des actions dans des services externes à l’intérieur Teams.</span><span class="sxs-lookup"><span data-stu-id="9eae3-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="9eae3-107">Les sections suivantes décrivent comment le faire.</span><span class="sxs-lookup"><span data-stu-id="9eae3-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="9eae3-108">Extensions de messages de type action</span><span class="sxs-lookup"><span data-stu-id="9eae3-108">Action type message extensions</span></span>

<span data-ttu-id="9eae3-109">Pour lancer des actions à partir d’une extension de messagerie définir `type` le paramètre à `action` .</span><span class="sxs-lookup"><span data-stu-id="9eae3-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="9eae3-110">Voici un exemple d’un manifeste avec une recherche et une commande de création.</span><span class="sxs-lookup"><span data-stu-id="9eae3-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="9eae3-111">Une seule extension de messagerie peut avoir jusqu’à 10 commandes différentes.</span><span class="sxs-lookup"><span data-stu-id="9eae3-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="9eae3-112">Cela peut inclure à la fois plusieurs recherches et plusieurs commandes basées sur l’action.</span><span class="sxs-lookup"><span data-stu-id="9eae3-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="9eae3-113">Exemple complet de manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="9eae3-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="9eae3-114">Initier des actions à partir de messages</span><span class="sxs-lookup"><span data-stu-id="9eae3-114">Initiate actions from messages</span></span>

<span data-ttu-id="9eae3-115">En plus d’initier des actions à partir de la zone de message de composition, vous pouvez également utiliser votre extension de messagerie pour lancer une action à partir d’un message.</span><span class="sxs-lookup"><span data-stu-id="9eae3-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="9eae3-116">Cela vous permettra d’envoyer le contenu du message à votre bot pour le traitement, et en option répondre à ce message avec une réponse en utilisant la méthode décrite [dans Répondre à soumettre](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="9eae3-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="9eae3-117">La réponse sera insérée en réponse au message que vos utilisateurs peuvent modifier avant de soumettre.</span><span class="sxs-lookup"><span data-stu-id="9eae3-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="9eae3-118">Vos utilisateurs peuvent accéder à votre extension de messagerie à partir du `...` menu de débordement, puis choisir `Take action` comme dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="9eae3-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the following image:</span></span>

![Exemple d’initiation d’une action à partir d’un message](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="9eae3-120">Pour activer votre extension de messagerie à partir d’un message, vous devrez ajouter le `context` paramètre à l’objet de votre extension de `commands` messagerie dans votre manifeste d’application comme dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9eae3-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="9eae3-121">Les chaînes valides pour `context` le tableau `"message"` `"commandBox"` sont, , et `"compose"` .</span><span class="sxs-lookup"><span data-stu-id="9eae3-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="9eae3-122">La valeur par défaut est `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="9eae3-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="9eae3-123">Consultez la section [définir les commandes pour](#define-commands) plus de détails sur le `context` paramètre.</span><span class="sxs-lookup"><span data-stu-id="9eae3-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

<span data-ttu-id="9eae3-124">Voici un exemple de `value` l’objet contenant les détails du message qui seront envoyés dans le cadre de la `composeExtension` demande être envoyé à votre bot.</span><span class="sxs-lookup"><span data-stu-id="9eae3-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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
        "content": "this is the message"
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

### <a name="test-via-uploading"></a><span data-ttu-id="9eae3-125">Test via le téléchargement</span><span class="sxs-lookup"><span data-stu-id="9eae3-125">Test via uploading</span></span>

<span data-ttu-id="9eae3-126">Vous pouvez tester votre extension de messagerie en téléchargeant votre application.</span><span class="sxs-lookup"><span data-stu-id="9eae3-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="9eae3-127">Pour plus d’informations, [voir Télécharger votre application dans une équipe](~/concepts/deploy-and-publish/apps-upload.md).</span><span class="sxs-lookup"><span data-stu-id="9eae3-127">For more information, see [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

<span data-ttu-id="9eae3-128">Pour ouvrir votre extension de messagerie, accédez à l’un de vos chats ou canaux.</span><span class="sxs-lookup"><span data-stu-id="9eae3-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="9eae3-129">Choisissez le **bouton Plus d’options** **(&#8943;)** dans la boîte de composition, et choisissez votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9eae3-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="9eae3-130">Collecte des commentaires des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="9eae3-130">Collecting input from users</span></span>

<span data-ttu-id="9eae3-131">Il existe trois façons de recueillir des informations auprès d’un utilisateur final dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9eae3-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="9eae3-132">Liste de paramètres statiques</span><span class="sxs-lookup"><span data-stu-id="9eae3-132">Static parameter list</span></span>

<span data-ttu-id="9eae3-133">Dans cette méthode, tout ce que vous devez faire est de définir une liste statique de paramètres dans le manifeste comme indiqué ci-dessus dans la commande « Créer To Do ».</span><span class="sxs-lookup"><span data-stu-id="9eae3-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="9eae3-134">Pour utiliser cette méthode `fetchTask` assurez-vous est `false` défini et que vous définissez vos paramètres dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="9eae3-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="9eae3-135">Lorsqu’un utilisateur choisit une commande avec des paramètres statiques, Teams générera un formulaire dans un module de tâches avec les paramètres définis dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="9eae3-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="9eae3-136">En appuyant sur Soumettre un `composeExtension/submitAction` est envoyé au bot.</span><span class="sxs-lookup"><span data-stu-id="9eae3-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="9eae3-137">Pour plus d’informations sur l’ensemble attendu des réponses, [voir Répondre à soumettre](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="9eae3-137">For more information on the expected set of responses, see [Responding to submit](#responding-to-submit).</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="9eae3-138">Entrée dynamique à l’aide d’une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="9eae3-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="9eae3-139">Dans cette méthode, votre service peut définir une carte adaptative personnalisée pour collecter l’entrée utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="9eae3-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="9eae3-140">Pour cette approche, définissez le `fetchTask` paramètre `true` dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="9eae3-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="9eae3-141">Notez que si vous `fetchTask` définissez `true` des paramètres statiques définis pour la commande seront ignorés.</span><span class="sxs-lookup"><span data-stu-id="9eae3-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="9eae3-142">Dans cette méthode, votre service recevra un événement `composeExtension/fetchTask` et doit répondre par une réponse de module de tâche basée sur la carte [adaptative.](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="9eae3-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="9eae3-143">Voici un exemple de réponse avec une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="9eae3-143">Following is a sample response with an adaptive card:</span></span>

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

<span data-ttu-id="9eae3-144">Le bot peut également répondre par une réponse auth/config si l’utilisateur a besoin d’authentifier ou de configurer l’extension avant d’obtenir l’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9eae3-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="9eae3-145">Entrée dynamique à l’aide d’une vue Web</span><span class="sxs-lookup"><span data-stu-id="9eae3-145">Dynamic input using a web view</span></span>

<span data-ttu-id="9eae3-146">Dans cette méthode, votre service peut afficher un widget basé `<iframe>` pour afficher n’importe quelle interface utilisateur personnalisée et collecter l’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9eae3-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="9eae3-147">Pour cette approche, définissez le `fetchTask` paramètre `true` dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="9eae3-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="9eae3-148">Tout comme dans le flux de carte adaptative de votre service sera envoyer un événement et doit `fetchTask` répondre avec une réponse de module de tâche basée sur [l’URL](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span><span class="sxs-lookup"><span data-stu-id="9eae3-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="9eae3-149">Voici un exemple de réponse avec une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="9eae3-149">Following is a sample response with an Adaptive card:</span></span>

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="9eae3-150">Demande d’installation de votre bot conversationnel</span><span class="sxs-lookup"><span data-stu-id="9eae3-150">Request to install your conversational bot</span></span>

<span data-ttu-id="9eae3-151">Si votre application contient également un bot conversationnel, il peut être nécessaire de s’assurer que votre bot est installé dans la conversation avant de charger votre module de tâches.</span><span class="sxs-lookup"><span data-stu-id="9eae3-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="9eae3-152">Cela peut être utile dans les situations où vous devez obtenir un contexte supplémentaire pour votre module de tâche.</span><span class="sxs-lookup"><span data-stu-id="9eae3-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="9eae3-153">Par exemple, vous devrez peut-être aller chercher la liste pour remplir un contrôle de ramasseur de personnes, ou la liste des canaux dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="9eae3-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="9eae3-154">Pour faciliter ce flux, lorsque votre extension de messagerie reçoit pour la première fois la `composeExtension/fetchTask` vérification d’invocation pour voir si votre bot est installé dans le contexte actuel.</span><span class="sxs-lookup"><span data-stu-id="9eae3-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context.</span></span> <span data-ttu-id="9eae3-155">Vous pouvez y parvenir en essayant d’obtenir l’appel de liste, par exemple, Si votre bot n’est pas installé, vous retournez une carte adaptative avec une action qui demande à l’utilisateur d’installer votre bot Voir l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9eae3-155">You could accomplish this by attempting the get roster call, for example, If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="9eae3-156">Notez que cela nécessite que l’utilisateur a la permission d’installer des applications à cet endroit; s’ils ne peuvent pas, ils recevront un message leur demandant de contacter leur administrateur.</span><span class="sxs-lookup"><span data-stu-id="9eae3-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="9eae3-157">Voici un exemple de la réponse :</span><span class="sxs-lookup"><span data-stu-id="9eae3-157">Here's an example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="9eae3-158">Une fois que l’utilisateur a terminé l’installation, votre bot recevra un autre message d’invocer `name = composeExtension/submitAction` avec , et `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="9eae3-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="9eae3-159">Voici un exemple de l’invocant :</span><span class="sxs-lookup"><span data-stu-id="9eae3-159">Here's an example of the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="9eae3-160">Vous devez répondre à cette invocant avec la même réponse de tâche que vous auriez répondu avec si le bot était déjà installé.</span><span class="sxs-lookup"><span data-stu-id="9eae3-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="9eae3-161">Répondre à soumettre</span><span class="sxs-lookup"><span data-stu-id="9eae3-161">Responding to submit</span></span>

<span data-ttu-id="9eae3-162">Une fois qu’un utilisateur a terminé la saisie de son entrée, votre bot recevra un événement `composeExtension/submitAction` avec l’id de commande et les valeurs de paramètres définies.</span><span class="sxs-lookup"><span data-stu-id="9eae3-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="9eae3-163">Ce sont les différentes réponses attendues à un `submitAction` .</span><span class="sxs-lookup"><span data-stu-id="9eae3-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="9eae3-164">Réponse du module de tâche</span><span class="sxs-lookup"><span data-stu-id="9eae3-164">Task Module response</span></span>

<span data-ttu-id="9eae3-165">Ceci est utilisé lorsque votre extension a besoin d’enchaîner les dialogues ensemble pour obtenir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9eae3-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="9eae3-166">La réponse est exactement la même que mentionnée `fetchTask` précédemment.</span><span class="sxs-lookup"><span data-stu-id="9eae3-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="9eae3-167">Composer l’extension auth/config réponse</span><span class="sxs-lookup"><span data-stu-id="9eae3-167">Compose extension auth/config response</span></span>

<span data-ttu-id="9eae3-168">Ceci est utilisé lorsque votre extension doit authentifier ou configurer afin de continuer.</span><span class="sxs-lookup"><span data-stu-id="9eae3-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="9eae3-169">Pour plus d’informations, consultez la [section authentification](~/resources/messaging-extension-v3/search-extensions.md#authentication) dans la section recherche.</span><span class="sxs-lookup"><span data-stu-id="9eae3-169">For more information, see [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="9eae3-170">Composer la réponse de résultat d’extension</span><span class="sxs-lookup"><span data-stu-id="9eae3-170">Compose extension result response</span></span>

<span data-ttu-id="9eae3-171">Cela a servi à insérer une carte dans la boîte de composition à la suite d’une commande.</span><span class="sxs-lookup"><span data-stu-id="9eae3-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="9eae3-172">C’est la même réponse qui est utilisée dans la commande de recherche, mais elle est limitée à une carte ou un résultat dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="9eae3-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="9eae3-173">Répondez par un message de carte adaptative envoyé à partir d’un bot</span><span class="sxs-lookup"><span data-stu-id="9eae3-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="9eae3-174">Vous pouvez également répondre à l’action soumettre en insérant un message avec une carte adaptative dans le canal avec un bot.</span><span class="sxs-lookup"><span data-stu-id="9eae3-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="9eae3-175">Votre utilisateur sera en mesure de prévisualiser le message avant de le soumettre, et potentiellement modifier / interagir avec lui ainsi.</span><span class="sxs-lookup"><span data-stu-id="9eae3-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="9eae3-176">Cela peut être très utile dans les scénarios où vous devez recueillir des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="9eae3-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="9eae3-177">Le scénario suivant montre comment vous pouvez utiliser ce flux pour configurer un sondage sans inclure les étapes de configuration dans le message du canal.</span><span class="sxs-lookup"><span data-stu-id="9eae3-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="9eae3-178">L’utilisateur clique sur l’extension de messagerie pour déclencher le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="9eae3-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="9eae3-179">L’utilisateur utilise le module de tâches pour configurer le sondage.</span><span class="sxs-lookup"><span data-stu-id="9eae3-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="9eae3-180">Après avoir soumis le module de tâche de configuration, l’application utilise les informations fournies dans le module de tâches pour concevoir une carte adaptative et `botMessagePreview` l’envoie en réponse au client.</span><span class="sxs-lookup"><span data-stu-id="9eae3-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="9eae3-181">L’utilisateur peut alors prévisualiser le message de la carte adaptative avant que le bot ne l’insère dans le canal.</span><span class="sxs-lookup"><span data-stu-id="9eae3-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="9eae3-182">Si le bot n’est pas déjà membre du canal, en cliquant `Send` ajoutera le bot.</span><span class="sxs-lookup"><span data-stu-id="9eae3-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="9eae3-183">Interagir avec la carte adaptative changera le message avant de l’envoyer.</span><span class="sxs-lookup"><span data-stu-id="9eae3-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="9eae3-184">Une fois que `Send` l’utilisateur clique sur le bot affichera le message sur le canal.</span><span class="sxs-lookup"><span data-stu-id="9eae3-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="9eae3-185">Pour activer ce flux, votre module de tâches doit répondre comme dans l’exemple ci-dessous, qui présentera le message d’aperçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9eae3-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="9eae3-186">Le `activityPreview` must contient une activité avec exactement `message` 1 pièce jointe de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="9eae3-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="9eae3-187">Votre extension de message devra maintenant répondre à deux nouveaux types d’interactions, `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="9eae3-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="9eae3-188">Voici un exemple de `value` l’objet que vous devrez traiter :</span><span class="sxs-lookup"><span data-stu-id="9eae3-188">Below is an example of the `value` object you will need to process:</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
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

<span data-ttu-id="9eae3-189">Lorsque vous répondez à `edit` la demande, vous devez répondre `task` par une réponse avec les valeurs remplies des informations que l’utilisateur a déjà soumises.</span><span class="sxs-lookup"><span data-stu-id="9eae3-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="9eae3-190">Lorsque vous répondez à `send` la demande, vous devez envoyer un message au canal contenant la carte adaptative finalisée.</span><span class="sxs-lookup"><span data-stu-id="9eae3-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="9eae3-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9eae3-191">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

# <a name="cnet"></a>[<span data-ttu-id="9eae3-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9eae3-192">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="9eae3-193">Cet exemple montre ce flux à [l’aide de la Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span><span class="sxs-lookup"><span data-stu-id="9eae3-193">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```

## <a name="see-also"></a><span data-ttu-id="9eae3-194">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9eae3-194">See also</span></span>

[<span data-ttu-id="9eae3-195">Échantillons de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9eae3-195">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)