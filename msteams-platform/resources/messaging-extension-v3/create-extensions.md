---
title: Initier des actions à l’aide des extensions de messagerie
description: Créer des extensions de messagerie basées sur des actions pour permettre aux utilisateurs de déclencher des services externes
keywords: extensions de messagerie teams
ms.openlocfilehash: 4eb5984f4a75f185accfe7ba87e9389361946959
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801372"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="6fc64-104">Initier des actions à l’aide des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="6fc64-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="6fc64-105">Les extensions de messagerie basées sur les actions permettent à vos utilisateurs de déclencher des actions dans des services externes dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6fc64-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="6fc64-107">Les sections suivantes décrivent la procédure à suivre.</span><span class="sxs-lookup"><span data-stu-id="6fc64-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="6fc64-108">Extensions de message de type d’action</span><span class="sxs-lookup"><span data-stu-id="6fc64-108">Action type message extensions</span></span>

<span data-ttu-id="6fc64-109">Pour initier des actions à partir d’une extension de messagerie, définissez le `type` paramètre sur `action` .</span><span class="sxs-lookup"><span data-stu-id="6fc64-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="6fc64-110">Voici un exemple de manifeste avec une recherche et une commande Create.</span><span class="sxs-lookup"><span data-stu-id="6fc64-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="6fc64-111">Une extension de messagerie unique peut comporter jusqu’à 10 commandes différentes.</span><span class="sxs-lookup"><span data-stu-id="6fc64-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="6fc64-112">Il peut s’agir de plusieurs commandes de recherche et de commandes basées sur une action.</span><span class="sxs-lookup"><span data-stu-id="6fc64-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="6fc64-113">Exemple de manifeste d’application complet</span><span class="sxs-lookup"><span data-stu-id="6fc64-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="6fc64-114">Initier des actions à partir de messages</span><span class="sxs-lookup"><span data-stu-id="6fc64-114">Initiate actions from messages</span></span>

<span data-ttu-id="6fc64-115">En plus d’initier des actions à partir de la zone de message de composition, vous pouvez également utiliser votre extension de messagerie pour initier une action à partir d’un message.</span><span class="sxs-lookup"><span data-stu-id="6fc64-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="6fc64-116">Cela vous permettra d’envoyer le contenu du message à votre bot à des fins de traitement et, si vous le souhaitez, de répondre à ce message avec une réponse en utilisant la méthode décrite dans [réponse à envoyer](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="6fc64-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="6fc64-117">La réponse est insérée en tant que réponse au message que vos utilisateurs peuvent modifier avant de les envoyer.</span><span class="sxs-lookup"><span data-stu-id="6fc64-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="6fc64-118">Vos utilisateurs peuvent accéder à votre extension de messagerie à partir du menu de dépassement de capacité `...` , puis en sélectionnant `Take action` comme dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fc64-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the image below.</span></span>

![Exemple d’initiation d’une action à partir d’un message](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="6fc64-120">Pour permettre à votre extension de messagerie de fonctionner à partir d’un message, vous devez ajouter le `context` paramètre à l’objet de votre extension de messagerie `commands` dans votre manifeste de l’application, comme dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fc64-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="6fc64-121">Les chaînes valides pour le `context` tableau sont `"message"` , `"commandBox"` et `"compose"` .</span><span class="sxs-lookup"><span data-stu-id="6fc64-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="6fc64-122">La valeur par défaut est `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="6fc64-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="6fc64-123">Pour plus d’informations sur le paramètre, reportez-vous à la section [define Commands](#define-commands) `context` .</span><span class="sxs-lookup"><span data-stu-id="6fc64-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

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

<span data-ttu-id="6fc64-124">Vous trouverez ci-dessous un exemple de l' `value` objet contenant les détails du message qui seront envoyés dans le cadre de l’envoi de la `composeExtension` demande à votre bot.</span><span class="sxs-lookup"><span data-stu-id="6fc64-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="6fc64-125">Test via téléchargement</span><span class="sxs-lookup"><span data-stu-id="6fc64-125">Test via uploading</span></span>

<span data-ttu-id="6fc64-126">Vous pouvez tester votre extension de messagerie en téléchargeant votre application.</span><span class="sxs-lookup"><span data-stu-id="6fc64-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="6fc64-127">Pour plus d’informations, consultez [la rubrique téléchargement de votre application dans une équipe](~/concepts/deploy-and-publish/apps-upload.md) .</span><span class="sxs-lookup"><span data-stu-id="6fc64-127">See [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for details.</span></span>

<span data-ttu-id="6fc64-128">Pour ouvrir votre extension de messagerie, accédez à l’une de vos conversations ou de vos canaux.</span><span class="sxs-lookup"><span data-stu-id="6fc64-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="6fc64-129">Sélectionnez le bouton **autres options** (**&#8943;**) dans la zone de composition, puis choisissez votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="6fc64-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="6fc64-130">Collecte d’entrées auprès des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6fc64-130">Collecting input from users</span></span>

<span data-ttu-id="6fc64-131">Il existe trois façons de collecter des informations auprès d’un utilisateur final dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6fc64-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="6fc64-132">Liste de paramètres statiques</span><span class="sxs-lookup"><span data-stu-id="6fc64-132">Static parameter list</span></span>

<span data-ttu-id="6fc64-133">Dans cette méthode, tout ce que vous avez à faire est de définir une liste statique de paramètres dans le manifeste, comme indiqué ci-dessus dans la commande « créer une tâche ».</span><span class="sxs-lookup"><span data-stu-id="6fc64-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="6fc64-134">Pour utiliser cette méthode, vérifiez que `fetchTask` la valeur est définie sur `false` et que vous définissez vos paramètres dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="6fc64-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="6fc64-135">Lorsqu’un utilisateur choisit une commande avec des paramètres statiques, teams génère un formulaire dans un module de tâches avec les paramètres définis dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="6fc64-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="6fc64-136">Lors de l’envoi d’un `composeExtension/submitAction` est envoyé au bot.</span><span class="sxs-lookup"><span data-stu-id="6fc64-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="6fc64-137">Pour plus d’informations sur le jeu de réponses attendu, reportez-vous à la rubrique [réponse à envoyer](#responding-to-submit) .</span><span class="sxs-lookup"><span data-stu-id="6fc64-137">See the topic [Responding to submit](#responding-to-submit) for more information on the expected set of responses.</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="6fc64-138">Entrée dynamique à l’aide d’une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="6fc64-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="6fc64-139">Dans cette méthode, votre service peut définir une carte adaptative personnalisée pour collecter l’entrée de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="6fc64-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="6fc64-140">Pour cette approche, définissez le `fetchTask` paramètre sur `true` dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="6fc64-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="6fc64-141">Notez que si vous avez défini `fetchTask` sur `true` un paramètre statique défini pour la commande sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="6fc64-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="6fc64-142">Dans cette méthode, votre service reçoit un `composeExtension/fetchTask` événement et doit répondre avec une [réponse de module de tâche](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)basée sur une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="6fc64-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="6fc64-143">Vous trouverez ci-dessous un exemple de réponse avec une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="6fc64-143">Below is an sample response with an adaptive card:</span></span>

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

<span data-ttu-id="6fc64-144">Le bot peut également répondre avec une réponse auth/config si l’utilisateur doit authentifier ou configurer l’extension avant d’obtenir l’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fc64-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="6fc64-145">Entrée dynamique à l’aide d’une vue Web</span><span class="sxs-lookup"><span data-stu-id="6fc64-145">Dynamic input using a web view</span></span>

<span data-ttu-id="6fc64-146">Dans cette méthode, votre service peut afficher un `<iframe>` widget basé pour afficher une interface utilisateur personnalisée et collecter les données entrées par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fc64-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="6fc64-147">Pour cette approche, définissez le `fetchTask` paramètre sur `true` dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="6fc64-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="6fc64-148">Tout comme dans le flux de carte adaptative votre service enverra un `fetchTask` événement et doit répondre par une [réponse de module de tâche](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)basée sur une URL.</span><span class="sxs-lookup"><span data-stu-id="6fc64-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="6fc64-149">Vous trouverez ci-dessous un exemple de réponse avec une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="6fc64-149">Below is an sample response with an Adaptive card:</span></span>

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="6fc64-150">Demande d’installation de votre bot de conversation</span><span class="sxs-lookup"><span data-stu-id="6fc64-150">Request to install your conversational bot</span></span>

<span data-ttu-id="6fc64-151">Si votre application contient également un bot de conversation, il peut s’avérer nécessaire de vous assurer que votre bot est installé dans la conversation avant de charger votre module de tâches.</span><span class="sxs-lookup"><span data-stu-id="6fc64-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="6fc64-152">Cela peut être utile dans les situations où vous devez obtenir un contexte supplémentaire pour le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="6fc64-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="6fc64-153">Par exemple, il se peut que vous deviez extraire la liste pour remplir un contrôle sélecteur de personnes ou la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="6fc64-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="6fc64-154">Pour faciliter ce flux, lorsque votre extension de messagerie reçoit d’abord le `composeExtension/fetchTask` contrôle d’appel pour déterminer si votre bot est installé dans le contexte actuel (vous pouvez effectuer cette étape en tentant l’appel Get de la liste, par exemple).</span><span class="sxs-lookup"><span data-stu-id="6fc64-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context (you could accomplish this by attempting the get roster call, for example).</span></span> <span data-ttu-id="6fc64-155">Si votre bot n’est pas installé, vous devez renvoyer une carte adaptative avec une action qui demande à l’utilisateur d’installer votre robot, comme dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fc64-155">If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="6fc64-156">Notez que l’utilisateur doit avoir l’autorisation d’installer des applications à cet emplacement ; s’ils ne peuvent pas se présenter, un message leur demande de contacter leur administrateur.</span><span class="sxs-lookup"><span data-stu-id="6fc64-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="6fc64-157">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="6fc64-157">Here's an example of the response:</span></span>

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

<span data-ttu-id="6fc64-158">Une fois l’installation terminée, votre bot reçoit un autre message d’appel avec `name = composeExtension/submitAction` , et `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="6fc64-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="6fc64-159">Voici un exemple de l’appel :</span><span class="sxs-lookup"><span data-stu-id="6fc64-159">Here's an example of the invoke:</span></span>

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

<span data-ttu-id="6fc64-160">Vous devez répondre à cet appel à l’aide de la même réponse de tâche que si le robot était déjà installé.</span><span class="sxs-lookup"><span data-stu-id="6fc64-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="6fc64-161">Réponse à l’envoi</span><span class="sxs-lookup"><span data-stu-id="6fc64-161">Responding to submit</span></span>

<span data-ttu-id="6fc64-162">Une fois qu’un utilisateur a terminé de saisir son entrée, le robot reçoit un `composeExtension/submitAction` événement avec l’ID de commande et les valeurs de paramètre définies.</span><span class="sxs-lookup"><span data-stu-id="6fc64-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="6fc64-163">Voici les différentes réponses attendues vers un `submitAction` .</span><span class="sxs-lookup"><span data-stu-id="6fc64-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="6fc64-164">Réponse du module de tâche</span><span class="sxs-lookup"><span data-stu-id="6fc64-164">Task Module response</span></span>

<span data-ttu-id="6fc64-165">Elle est utilisée lorsque votre extension doit regrouper les boîtes de dialogue pour obtenir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6fc64-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="6fc64-166">La réponse est exactement la même que celle `fetchTask` mentionnée précédemment.</span><span class="sxs-lookup"><span data-stu-id="6fc64-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="6fc64-167">Réponse d’authentification/configuration de l’extension de composition</span><span class="sxs-lookup"><span data-stu-id="6fc64-167">Compose extension auth/config response</span></span>

<span data-ttu-id="6fc64-168">Cette valeur est utilisée lorsque votre extension doit être authentifiée ou configurée pour continuer.</span><span class="sxs-lookup"><span data-stu-id="6fc64-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="6fc64-169">Pour plus d’informations, consultez la [section authentification](~/resources/messaging-extension-v3/search-extensions.md#authentication) dans la section recherche.</span><span class="sxs-lookup"><span data-stu-id="6fc64-169">See [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section for more details.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="6fc64-170">Réponse aux résultats de l’extension de composition</span><span class="sxs-lookup"><span data-stu-id="6fc64-170">Compose extension result response</span></span>

<span data-ttu-id="6fc64-171">Cette commande permet d’insérer une carte dans la zone de composition à la suite de la commande.</span><span class="sxs-lookup"><span data-stu-id="6fc64-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="6fc64-172">Il s’agit de la même réponse que celle utilisée dans la commande de recherche, mais il est limité à une carte ou à un résultat dans la matrice.</span><span class="sxs-lookup"><span data-stu-id="6fc64-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="6fc64-173">Répondre avec un message de carte adaptative envoyé à partir d’un bot</span><span class="sxs-lookup"><span data-stu-id="6fc64-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="6fc64-174">Vous pouvez également répondre à l’action d’envoi en insérant un message avec une carte adaptative dans le canal avec un bot.</span><span class="sxs-lookup"><span data-stu-id="6fc64-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="6fc64-175">Votre utilisateur pourra prévisualiser le message avant de l’envoyer et éventuellement modifier/interagir avec.</span><span class="sxs-lookup"><span data-stu-id="6fc64-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="6fc64-176">Cela peut être très utile dans les scénarios où vous devez recueillir des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="6fc64-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="6fc64-177">Le scénario suivant montre comment vous pouvez utiliser ce flux pour configurer un sondage sans inclure les étapes de configuration dans le message du canal.</span><span class="sxs-lookup"><span data-stu-id="6fc64-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="6fc64-178">L’utilisateur clique sur l’extension de messagerie pour déclencher le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="6fc64-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="6fc64-179">L’utilisateur utilise le module tâches pour configurer le sondage.</span><span class="sxs-lookup"><span data-stu-id="6fc64-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="6fc64-180">Après avoir soumis le module de tâches de configuration, l’application utilise les informations fournies dans le module de tâches pour concevoir une carte adaptative et l’envoie en `botMessagePreview` réponse au client.</span><span class="sxs-lookup"><span data-stu-id="6fc64-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="6fc64-181">L’utilisateur peut alors prévisualiser le message de la carte adaptative avant de l’insérer dans le canal.</span><span class="sxs-lookup"><span data-stu-id="6fc64-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="6fc64-182">Si le bot n’est pas déjà membre du canal, le fait de cliquer sur `Send` ajoutera le bot.</span><span class="sxs-lookup"><span data-stu-id="6fc64-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="6fc64-183">L’interaction avec la carte adaptative modifiera le message avant de l’envoyer.</span><span class="sxs-lookup"><span data-stu-id="6fc64-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="6fc64-184">Une fois que l’utilisateur clique sur `Send` le bot, le message est publié vers le canal.</span><span class="sxs-lookup"><span data-stu-id="6fc64-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="6fc64-185">Pour activer ce flux, votre module de tâches doit répondre comme dans l’exemple ci-dessous, qui présente l’aperçu du message à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fc64-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="6fc64-186">Le `activityPreview` doit contenir une `message` activité avec exactement 1 pièce jointe de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="6fc64-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="6fc64-187">Votre extension de message doit maintenant répondre à deux nouveaux types d’interactions `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="6fc64-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="6fc64-188">Vous trouverez ci-dessous un exemple de l' `value` objet que vous devrez traiter :</span><span class="sxs-lookup"><span data-stu-id="6fc64-188">Below is an example of the `value` object you will need to process:</span></span>

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

<span data-ttu-id="6fc64-189">Lors de la réponse à la `edit` demande, vous devez répondre avec une `task` réponse dont les valeurs sont remplies avec les informations que l’utilisateur a déjà envoyées.</span><span class="sxs-lookup"><span data-stu-id="6fc64-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="6fc64-190">Lors de la réponse à la `send` demande, vous devez envoyer un message au canal contenant la carte adaptative finalisée.</span><span class="sxs-lookup"><span data-stu-id="6fc64-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6fc64-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6fc64-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

<span data-ttu-id="6fc64-192">*Voir aussi* [exemples de robots d’infrastructure](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="6fc64-192">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6fc64-193">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6fc64-193">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="6fc64-194">Cet exemple illustre ce flux à l’aide du [Kit de développement logiciel (SDK) Microsoft. Bot. Connector. Teams (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span><span class="sxs-lookup"><span data-stu-id="6fc64-194">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

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
