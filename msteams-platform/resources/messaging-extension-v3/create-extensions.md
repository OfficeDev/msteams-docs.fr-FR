---
title: Lancer des actions avec des extensions de messagerie
description: Créer des extensions de messagerie basées sur l’action pour permettre aux utilisateurs de déclencher des services externes
localization_priority: Normal
ms.topic: how-to
keywords: teams messaging extensions messaging extensions search
ms.openlocfilehash: bfb3295726c355164f080c15e3759ea36a99d914
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566739"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="83103-104">Lancer des actions avec des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="83103-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="83103-105">Les extensions de messagerie basées sur l’action permettent à vos utilisateurs de déclencher des actions dans des services externes à l’intérieur Teams.</span><span class="sxs-lookup"><span data-stu-id="83103-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="83103-107">Les sections suivantes décrivent comment faire.</span><span class="sxs-lookup"><span data-stu-id="83103-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="83103-108">Extensions de message de type d’action</span><span class="sxs-lookup"><span data-stu-id="83103-108">Action type message extensions</span></span>

<span data-ttu-id="83103-109">Pour lancer des actions à partir d’une extension de messagerie, définissez `type` le paramètre sur `action` .</span><span class="sxs-lookup"><span data-stu-id="83103-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="83103-110">Voici un exemple de manifeste avec une recherche et une commande de création.</span><span class="sxs-lookup"><span data-stu-id="83103-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="83103-111">Une seule extension de messagerie peut avoir jusqu’à 10 commandes différentes.</span><span class="sxs-lookup"><span data-stu-id="83103-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="83103-112">Cela peut inclure à la fois plusieurs commandes de recherche et plusieurs commandes basées sur l’action.</span><span class="sxs-lookup"><span data-stu-id="83103-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="83103-113">Exemple de manifeste d’application complet</span><span class="sxs-lookup"><span data-stu-id="83103-113">Complete app manifest example</span></span>

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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="83103-114">Lancer des actions à partir de messages</span><span class="sxs-lookup"><span data-stu-id="83103-114">Initiate actions from messages</span></span>

<span data-ttu-id="83103-115">En plus de lancer des actions à partir de la zone composer un message, vous pouvez également utiliser votre extension de messagerie pour lancer une action à partir d’un message.</span><span class="sxs-lookup"><span data-stu-id="83103-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="83103-116">Cela vous permettra d’envoyer le contenu du message à votre bot pour traitement et éventuellement de répondre à ce message avec une réponse à l’aide de la méthode décrite dans Répondre à [l’envoi.](#responding-to-submit)</span><span class="sxs-lookup"><span data-stu-id="83103-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="83103-117">La réponse est insérée en tant que réponse au message que vos utilisateurs peuvent modifier avant d’envoyer.</span><span class="sxs-lookup"><span data-stu-id="83103-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="83103-118">Vos utilisateurs peuvent accéder à votre extension de messagerie à partir du menu de dépassement, puis en sélectionnant comme `...` `Take action` dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="83103-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the following image:</span></span>

![Exemple de l’initiative d’une action à partir d’un message](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="83103-120">Pour que votre extension de messagerie fonctionne à partir d’un message, vous devez ajouter le paramètre à l’objet de votre extension de messagerie dans le manifeste de votre application, comme dans `context` `commands` l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="83103-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="83103-121">Les chaînes `context` valides pour le tableau `"message"` sont , et `"commandBox"` `"compose"` .</span><span class="sxs-lookup"><span data-stu-id="83103-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="83103-122">La valeur par défaut est `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="83103-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="83103-123">Consultez la section [Définir les commandes](#define-commands) pour obtenir des détails complets sur le `context` paramètre.</span><span class="sxs-lookup"><span data-stu-id="83103-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

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

<span data-ttu-id="83103-124">Voici un exemple de l’objet contenant les détails du message qui sera envoyé dans le cadre de la `value` `composeExtension` demande à votre bot.</span><span class="sxs-lookup"><span data-stu-id="83103-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="83103-125">Test via le téléchargement</span><span class="sxs-lookup"><span data-stu-id="83103-125">Test via uploading</span></span>

<span data-ttu-id="83103-126">Vous pouvez tester votre extension de messagerie en chargeant votre application.</span><span class="sxs-lookup"><span data-stu-id="83103-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="83103-127">Pour plus d’informations, [voir Téléchargement de votre application dans une équipe.](~/concepts/deploy-and-publish/apps-upload.md)</span><span class="sxs-lookup"><span data-stu-id="83103-127">For more information, see [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

<span data-ttu-id="83103-128">Pour ouvrir votre extension de messagerie, accédez à vos conversations ou canaux.</span><span class="sxs-lookup"><span data-stu-id="83103-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="83103-129">Choisissez le **bouton Plus d’options** (**&#8943;**) dans la zone de composition, puis choisissez votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="83103-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="83103-130">Collecte des entrées des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="83103-130">Collecting input from users</span></span>

<span data-ttu-id="83103-131">Il existe trois façons de collecter des informations d’un utilisateur final Teams.</span><span class="sxs-lookup"><span data-stu-id="83103-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="83103-132">Liste des paramètres statiques</span><span class="sxs-lookup"><span data-stu-id="83103-132">Static parameter list</span></span>

<span data-ttu-id="83103-133">Dans cette méthode, il vous suffit de définir une liste statique de paramètres dans le manifeste, comme indiqué ci-dessus dans la commande « Créer To Do ».</span><span class="sxs-lookup"><span data-stu-id="83103-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="83103-134">Pour utiliser cette méthode, assurez-vous qu’elle est définie sur et que vous `fetchTask` `false` définissez vos paramètres dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="83103-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="83103-135">Lorsqu’un utilisateur choisit une commande avec des paramètres statiques, Teams génère un formulaire dans un module de tâche avec les paramètres définis dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="83103-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="83103-136">Sur la touche Envoyer, a `composeExtension/submitAction` est envoyé au bot.</span><span class="sxs-lookup"><span data-stu-id="83103-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="83103-137">Pour plus d’informations sur l’ensemble attendu de réponses, voir [Répondre pour envoyer](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="83103-137">For more information on the expected set of responses, see [Responding to submit](#responding-to-submit).</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="83103-138">Entrée dynamique à l’aide d’une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="83103-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="83103-139">Dans cette méthode, votre service peut définir une carte adaptative personnalisée pour collecter les entrées de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="83103-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="83103-140">Pour cette approche, définissez `fetchTask` le paramètre sur dans le `true` manifeste.</span><span class="sxs-lookup"><span data-stu-id="83103-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="83103-141">Notez que si vous `fetchTask` définissez des `true` paramètres statiques définis pour la commande, ils seront ignorés.</span><span class="sxs-lookup"><span data-stu-id="83103-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="83103-142">Dans cette méthode, votre service reçoit un événement et doit répondre avec une réponse de module de tâche basée sur une carte `composeExtension/fetchTask` [adaptative.](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="83103-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="83103-143">Voici un exemple de réponse avec une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="83103-143">Following is a sample response with an adaptive card:</span></span>

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

<span data-ttu-id="83103-144">Le bot peut également répondre avec une réponse d’authentification/configuration si l’utilisateur doit authentifier ou configurer l’extension avant d’obtenir l’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="83103-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="83103-145">Entrée dynamique à l’aide d’un affichage web</span><span class="sxs-lookup"><span data-stu-id="83103-145">Dynamic input using a web view</span></span>

<span data-ttu-id="83103-146">Dans cette méthode, votre service peut afficher un widget basé pour afficher n’importe quelle interface utilisateur `<iframe>` personnalisée et collecter les entrées utilisateur.</span><span class="sxs-lookup"><span data-stu-id="83103-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="83103-147">Pour cette approche, définissez `fetchTask` le paramètre sur dans le `true` manifeste.</span><span class="sxs-lookup"><span data-stu-id="83103-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="83103-148">Tout comme dans le flux de carte adaptative, votre service enverra un événement et doit répondre avec une réponse de module de tâche basée sur `fetchTask` [une](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)URL.</span><span class="sxs-lookup"><span data-stu-id="83103-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="83103-149">Voici un exemple de réponse avec une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="83103-149">Following is a sample response with an Adaptive card:</span></span>

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="83103-150">Demande d’installation de votre bot de conversation</span><span class="sxs-lookup"><span data-stu-id="83103-150">Request to install your conversational bot</span></span>

<span data-ttu-id="83103-151">Si votre application contient également un bot de conversation, il peut être nécessaire de s’assurer que votre bot est installé dans la conversation avant de charger votre module de tâche.</span><span class="sxs-lookup"><span data-stu-id="83103-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="83103-152">Cela peut être utile dans les situations où vous devez obtenir un contexte supplémentaire pour votre module de tâche.</span><span class="sxs-lookup"><span data-stu-id="83103-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="83103-153">Par exemple, vous devrez peut-être extraire la liste de membres pour remplir un contrôle de s picker de personnes ou la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="83103-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="83103-154">Pour faciliter ce flux, lorsque votre extension de messagerie reçoit d’abord la vérification d’appel pour voir si votre bot est `composeExtension/fetchTask` installé dans le contexte actuel.</span><span class="sxs-lookup"><span data-stu-id="83103-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context.</span></span> <span data-ttu-id="83103-155">Pour ce faire, vous pouvez essayer d’obtenir un appel de liste de liste, par exemple, si votre bot n’est pas installé, vous renvoyez une carte adaptative avec une action qui demande à l’utilisateur d’installer votre bot. Consultez l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="83103-155">You could accomplish this by attempting the get roster call, for example, If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="83103-156">Notez que l’utilisateur doit avoir l’autorisation d’installer des applications à cet emplacement . Si ce n’est pas le cas, un message leur demande de contacter leur administrateur.</span><span class="sxs-lookup"><span data-stu-id="83103-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="83103-157">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="83103-157">Here's an example of the response:</span></span>

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

<span data-ttu-id="83103-158">Une fois que l’utilisateur a terminé l’installation, votre bot reçoit un autre message d’appel `name = composeExtension/submitAction` avec , et `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="83103-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="83103-159">Voici un exemple d’appel :</span><span class="sxs-lookup"><span data-stu-id="83103-159">Here's an example of the invoke:</span></span>

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

<span data-ttu-id="83103-160">Vous devez répondre à cet appel avec la même réponse à la tâche avec qui vous ariez répondu si le bot était déjà installé.</span><span class="sxs-lookup"><span data-stu-id="83103-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="83103-161">Réponse à l’soumission</span><span class="sxs-lookup"><span data-stu-id="83103-161">Responding to submit</span></span>

<span data-ttu-id="83103-162">Une fois qu’un utilisateur a entré son entrée, votre bot reçoit un événement avec l’ID de commande et les valeurs de paramètre `composeExtension/submitAction` définies.</span><span class="sxs-lookup"><span data-stu-id="83103-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="83103-163">Voici les différentes réponses attendues à un `submitAction` .</span><span class="sxs-lookup"><span data-stu-id="83103-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="83103-164">Réponse du module de tâche</span><span class="sxs-lookup"><span data-stu-id="83103-164">Task Module response</span></span>

<span data-ttu-id="83103-165">Cette valeur est utilisée lorsque votre extension doit chaîner des boîtes de dialogue pour obtenir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="83103-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="83103-166">La réponse est identique à ce qui a `fetchTask` été mentionné précédemment.</span><span class="sxs-lookup"><span data-stu-id="83103-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="83103-167">Réponse d’th/config d’extension de composition</span><span class="sxs-lookup"><span data-stu-id="83103-167">Compose extension auth/config response</span></span>

<span data-ttu-id="83103-168">Il est utilisé lorsque votre extension doit s’authentifier ou configurer pour continuer.</span><span class="sxs-lookup"><span data-stu-id="83103-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="83103-169">Pour plus d’informations, voir [la section sur l’authentification](~/resources/messaging-extension-v3/search-extensions.md#authentication) dans la section de recherche.</span><span class="sxs-lookup"><span data-stu-id="83103-169">For more information, see [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="83103-170">Réponse aux résultats de l’extension de composition</span><span class="sxs-lookup"><span data-stu-id="83103-170">Compose extension result response</span></span>

<span data-ttu-id="83103-171">Cette commande sert à insérer une carte dans la zone de composition à la suite d’une commande.</span><span class="sxs-lookup"><span data-stu-id="83103-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="83103-172">Il s’agit de la même réponse que celle utilisée dans la commande de recherche, mais elle est limitée à une carte ou à un résultat dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="83103-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="83103-173">Répondre avec un message de carte adaptative envoyé à partir d’un bot</span><span class="sxs-lookup"><span data-stu-id="83103-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="83103-174">Vous pouvez également répondre à l’action d’envoyer en insérant un message avec une carte adaptative dans le canal avec un bot.</span><span class="sxs-lookup"><span data-stu-id="83103-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="83103-175">Votre utilisateur pourra afficher un aperçu du message avant de l’envoyer, et éventuellement le modifier/interagir avec celui-ci.</span><span class="sxs-lookup"><span data-stu-id="83103-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="83103-176">Cela peut être très utile dans les scénarios où vous devez collecter des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="83103-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="83103-177">Le scénario suivant montre comment utiliser ce flux pour configurer un sondage sans inclure les étapes de configuration dans le message de canal.</span><span class="sxs-lookup"><span data-stu-id="83103-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="83103-178">L’utilisateur clique sur l’extension de messagerie pour déclencher le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="83103-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="83103-179">L’utilisateur utilise le module de tâche pour configurer le sondage.</span><span class="sxs-lookup"><span data-stu-id="83103-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="83103-180">Après avoir soumis le module de tâche de configuration, l’application utilise les informations fournies dans le module de tâche pour créer une carte adaptative et l’envoie en réponse `botMessagePreview` au client.</span><span class="sxs-lookup"><span data-stu-id="83103-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="83103-181">L’utilisateur peut ensuite afficher un aperçu du message de carte adaptative avant que le bot l’insère dans le canal.</span><span class="sxs-lookup"><span data-stu-id="83103-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="83103-182">Si le bot n’est pas déjà membre du canal, un clic `Send` ajoute le bot.</span><span class="sxs-lookup"><span data-stu-id="83103-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="83103-183">L’interaction avec la carte adaptative modifie le message avant de l’envoyer.</span><span class="sxs-lookup"><span data-stu-id="83103-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="83103-184">Une fois que l’utilisateur `Send` clique sur le bot, il publie le message sur le canal.</span><span class="sxs-lookup"><span data-stu-id="83103-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="83103-185">Pour activer ce flux, votre module de tâche doit répondre comme dans l’exemple ci-dessous, qui présente le message d’aperçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="83103-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="83103-186">Le `activityPreview` doit contenir une activité avec exactement 1 pièce jointe `message` de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="83103-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="83103-187">Votre extension de message devra désormais répondre à deux nouveaux types d’interactions, `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="83103-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="83103-188">Voici un exemple de `value` l’objet que vous devrez traiter :</span><span class="sxs-lookup"><span data-stu-id="83103-188">Below is an example of the `value` object you will need to process:</span></span>

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

<span data-ttu-id="83103-189">Lorsque vous répondez à la demande, vous devez répondre par une réponse avec les valeurs remplies avec les informations que `edit` `task` l’utilisateur a déjà envoyées.</span><span class="sxs-lookup"><span data-stu-id="83103-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="83103-190">Lorsque vous répondez à la demande, vous devez envoyer un message au canal `send` contenant la carte adaptative finalisée.</span><span class="sxs-lookup"><span data-stu-id="83103-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="83103-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="83103-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="cnet"></a>[<span data-ttu-id="83103-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="83103-192">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="83103-193">Cet exemple illustre ce flux à l’aide du [SDK Microsoft.Bot.Connector.Teams (v3).](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="83103-193">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

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

## <a name="see-also"></a><span data-ttu-id="83103-194">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="83103-194">See also</span></span>

[<span data-ttu-id="83103-195">Exemples Bot Framework</span><span class="sxs-lookup"><span data-stu-id="83103-195">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)