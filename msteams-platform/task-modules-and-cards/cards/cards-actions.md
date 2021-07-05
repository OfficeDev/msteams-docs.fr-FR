---
title: Ajouter des actions de carte dans un bot
description: Décrit les actions de carte dans Microsoft Teams et comment les utiliser dans vos bots
localization_priority: Normal
ms.topic: conceptual
keywords: actions de cartes de bots teams
ms.openlocfilehash: 4af152f6179785687d4fd7371d202c56e1aee170
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254201"
---
# <a name="card-actions"></a><span data-ttu-id="6a45a-104">Actions de carte</span><span class="sxs-lookup"><span data-stu-id="6a45a-104">Card actions</span></span>

<span data-ttu-id="6a45a-105">Les cartes utilisées par les bots et les extensions de messagerie Teams les types d’activité [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) suivants :</span><span class="sxs-lookup"><span data-stu-id="6a45a-105">Cards used by bots and messaging extensions in Teams support the following activity [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) types:</span></span>

> [!NOTE]
> <span data-ttu-id="6a45a-106">Les `CardAction` actions diffèrent des cartes Office 365 connecteur `potentialActions` lorsqu’elles sont utilisées à partir de connecteurs.</span><span class="sxs-lookup"><span data-stu-id="6a45a-106">The `CardAction` actions differ from `potentialActions` for Office 365 Connector cards when used from connectors.</span></span>

| <span data-ttu-id="6a45a-107">Type</span><span class="sxs-lookup"><span data-stu-id="6a45a-107">Type</span></span> | <span data-ttu-id="6a45a-108">Action</span><span class="sxs-lookup"><span data-stu-id="6a45a-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="6a45a-109">Ouvre une URL dans le navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="6a45a-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="6a45a-110">Envoie un message et une charge utile au bot à partir de l’utilisateur qui a sélectionné le bouton ou a tapé la carte.</span><span class="sxs-lookup"><span data-stu-id="6a45a-110">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="6a45a-111">Envoie un message distinct au flux de conversation.</span><span class="sxs-lookup"><span data-stu-id="6a45a-111">Sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="6a45a-112">Envoie un message au bot de l’utilisateur qui a sélectionné le bouton ou a tapé la carte.</span><span class="sxs-lookup"><span data-stu-id="6a45a-112">Sends a message to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="6a45a-113">Ce message de l’utilisateur au bot est visible par tous les participants à la conversation.</span><span class="sxs-lookup"><span data-stu-id="6a45a-113">This message from user to bot is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="6a45a-114">Envoie un message et une charge utile au bot à partir de l’utilisateur qui a sélectionné le bouton ou a tapé la carte.</span><span class="sxs-lookup"><span data-stu-id="6a45a-114">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="6a45a-115">Ce message n’est pas visible.</span><span class="sxs-lookup"><span data-stu-id="6a45a-115">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="6a45a-116">Lance le flux OAuth, ce qui permet aux bots de se connecter à des services sécurisés.</span><span class="sxs-lookup"><span data-stu-id="6a45a-116">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="6a45a-117">Teams ne prend pas en charge `CardAction` les types non répertoriés dans le tableau précédent.</span><span class="sxs-lookup"><span data-stu-id="6a45a-117">Teams does not support `CardAction` types not listed in the previous table.</span></span>
>* <span data-ttu-id="6a45a-118">Teams ne prend pas en charge la `potentialActions` propriété.</span><span class="sxs-lookup"><span data-stu-id="6a45a-118">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="6a45a-119">Les actions de carte sont différentes [des actions suggérées](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) dans Bot Framework ou Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="6a45a-119">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework or Azure Bot Service.</span></span> <span data-ttu-id="6a45a-120">Les actions suggérées ne sont pas prises en charge dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6a45a-120">Suggested actions are not supported in Microsoft Teams.</span></span> <span data-ttu-id="6a45a-121">Si vous souhaitez que les boutons apparaissent dans un message Teams bot, utilisez une carte.</span><span class="sxs-lookup"><span data-stu-id="6a45a-121">If you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="6a45a-122">Si vous utilisez une action de carte dans le cadre d’une extension de messagerie, les actions ne fonctionnent pas tant que la carte n’est pas envoyée au canal.</span><span class="sxs-lookup"><span data-stu-id="6a45a-122">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="6a45a-123">Les actions ne fonctionnent pas lorsque la carte se trouve dans la zone composer un message.</span><span class="sxs-lookup"><span data-stu-id="6a45a-123">The actions do not work while the card is in the compose message box.</span></span>

## <a name="action-type-openurl"></a><span data-ttu-id="6a45a-124">Type d’action openUrl</span><span class="sxs-lookup"><span data-stu-id="6a45a-124">Action type openUrl</span></span>

<span data-ttu-id="6a45a-125">`openUrl` le type d’action spécifie une URL à lancer dans le navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="6a45a-125">`openUrl` action type specifies a URL to launch in the default browser.</span></span>

> [!NOTE]
> <span data-ttu-id="6a45a-126">Votre bot ne reçoit aucune notification sur le bouton sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6a45a-126">Your bot does not receive any notice on which button was selected.</span></span>

<span data-ttu-id="6a45a-127">Avec `openUrl` , vous pouvez créer une action avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a45a-127">With `openUrl`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="6a45a-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="6a45a-128">Property</span></span> | <span data-ttu-id="6a45a-129">Description</span><span class="sxs-lookup"><span data-stu-id="6a45a-129">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="6a45a-130">Apparaît en tant qu’étiquette de bouton.</span><span class="sxs-lookup"><span data-stu-id="6a45a-130">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="6a45a-131">Ce champ doit contenir une URL complète et correctement formée.</span><span class="sxs-lookup"><span data-stu-id="6a45a-131">This field must contain a full and properly formed URL.</span></span> |

# <a name="json"></a>[<span data-ttu-id="6a45a-132">JSON</span><span class="sxs-lookup"><span data-stu-id="6a45a-132">JSON</span></span>](#tab/json)

<span data-ttu-id="6a45a-133">Le code suivant montre un exemple de `openUrl` type d’action dans JSON :</span><span class="sxs-lookup"><span data-stu-id="6a45a-133">The following code shows an example of `openUrl` action type in JSON:</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[<span data-ttu-id="6a45a-134">C#</span><span class="sxs-lookup"><span data-stu-id="6a45a-134">C#</span></span>](#tab/csharp)

<span data-ttu-id="6a45a-135">Le code suivant montre un exemple de `openUrl` type d’action dans C# :</span><span class="sxs-lookup"><span data-stu-id="6a45a-135">The following code shows an example of `openUrl` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6a45a-136">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6a45a-136">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6a45a-137">Le code suivant montre un exemple de `openUrl` type d’action en JavaScript :</span><span class="sxs-lookup"><span data-stu-id="6a45a-137">The following code shows an example of `openUrl` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a><span data-ttu-id="6a45a-138">Type d’action messageBack</span><span class="sxs-lookup"><span data-stu-id="6a45a-138">Action type messageBack</span></span>

<span data-ttu-id="6a45a-139">Avec `messageBack` , vous pouvez créer une action entièrement personnalisée avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a45a-139">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="6a45a-140">Propriété</span><span class="sxs-lookup"><span data-stu-id="6a45a-140">Property</span></span> | <span data-ttu-id="6a45a-141">Description</span><span class="sxs-lookup"><span data-stu-id="6a45a-141">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="6a45a-142">Apparaît en tant qu’étiquette de bouton.</span><span class="sxs-lookup"><span data-stu-id="6a45a-142">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="6a45a-143">Facultatif.</span><span class="sxs-lookup"><span data-stu-id="6a45a-143">Optional.</span></span> <span data-ttu-id="6a45a-144">Utilisé par l’utilisateur dans le flux de conversation lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="6a45a-144">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="6a45a-145">Ce texte n’est pas envoyé à votre bot.</span><span class="sxs-lookup"><span data-stu-id="6a45a-145">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="6a45a-146">Envoyé à votre bot lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="6a45a-146">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="6a45a-147">Vous pouvez coder le contexte de l’action, par exemple des identificateurs uniques ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="6a45a-147">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="6a45a-148">Envoyé à votre bot lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="6a45a-148">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="6a45a-149">Utilisez cette propriété pour simplifier le développement de bots.</span><span class="sxs-lookup"><span data-stu-id="6a45a-149">Use this property to simplify bot development.</span></span> <span data-ttu-id="6a45a-150">Votre code peut vérifier une propriété de niveau supérieur unique pour envoyer la logique du bot.</span><span class="sxs-lookup"><span data-stu-id="6a45a-150">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="6a45a-151">La flexibilité des moyens que votre code ne peut pas laisser un message utilisateur visible dans l’historique simplement `messageBack` en n’utilisant pas `displayText` .</span><span class="sxs-lookup"><span data-stu-id="6a45a-151">The flexibility of `messageBack` means that your code cannot leave a visible user message in the history simply by not using `displayText`.</span></span>

# <a name="json"></a>[<span data-ttu-id="6a45a-152">JSON</span><span class="sxs-lookup"><span data-stu-id="6a45a-152">JSON</span></span>](#tab/json)

<span data-ttu-id="6a45a-153">Le code suivant montre un exemple de `messageBack` type d’action dans JSON :</span><span class="sxs-lookup"><span data-stu-id="6a45a-153">The following code shows an example of `messageBack` action type in JSON:</span></span>

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

<span data-ttu-id="6a45a-154">La `value` propriété peut être une chaîne JSON sérialisée ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="6a45a-154">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

# <a name="c"></a>[<span data-ttu-id="6a45a-155">C#</span><span class="sxs-lookup"><span data-stu-id="6a45a-155">C#</span></span>](#tab/csharp)

<span data-ttu-id="6a45a-156">Le code suivant montre un exemple de `messageBack` type d’action dans C# :</span><span class="sxs-lookup"><span data-stu-id="6a45a-156">The following code shows an example of `messageBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6a45a-157">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6a45a-157">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6a45a-158">Le code suivant montre un exemple de `messageBack` type d’action en JavaScript :</span><span class="sxs-lookup"><span data-stu-id="6a45a-158">The following code shows an example of `messageBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a><span data-ttu-id="6a45a-159">Exemple de message entrant</span><span class="sxs-lookup"><span data-stu-id="6a45a-159">Inbound message example</span></span>

<span data-ttu-id="6a45a-160">`replyToId` contient l’ID du message d’où provenait l’action de carte.</span><span class="sxs-lookup"><span data-stu-id="6a45a-160">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="6a45a-161">Utilisez-le si vous souhaitez mettre à jour le message.</span><span class="sxs-lookup"><span data-stu-id="6a45a-161">Use it if you want to update the message.</span></span>

<span data-ttu-id="6a45a-162">Le code suivant illustre un exemple de message entrant :</span><span class="sxs-lookup"><span data-stu-id="6a45a-162">The following code shows an example of inbound message:</span></span>

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="action-type-imback"></a><span data-ttu-id="6a45a-163">Type d’action imBack</span><span class="sxs-lookup"><span data-stu-id="6a45a-163">Action type imBack</span></span>

<span data-ttu-id="6a45a-164">L’action déclenche un message de retour à votre bot, comme si l’utilisateur l’avait tapé `imBack` dans un message de conversation normal.</span><span class="sxs-lookup"><span data-stu-id="6a45a-164">The `imBack` action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="6a45a-165">Votre utilisateur et tous les autres utilisateurs d’un canal peuvent voir la réponse du bouton.</span><span class="sxs-lookup"><span data-stu-id="6a45a-165">Your user and all other users in a channel can see the button response.</span></span>

<span data-ttu-id="6a45a-166">Avec `imBack` , vous pouvez créer une action avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a45a-166">With `imBack`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="6a45a-167">Propriété</span><span class="sxs-lookup"><span data-stu-id="6a45a-167">Property</span></span> | <span data-ttu-id="6a45a-168">Description</span><span class="sxs-lookup"><span data-stu-id="6a45a-168">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="6a45a-169">Apparaît en tant qu’étiquette de bouton.</span><span class="sxs-lookup"><span data-stu-id="6a45a-169">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="6a45a-170">Ce champ doit contenir la chaîne de texte utilisée dans la conversation et par conséquent renvoyée au bot.</span><span class="sxs-lookup"><span data-stu-id="6a45a-170">This field must contain the text string used in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="6a45a-171">Il s’agit du texte du message que vous traiterez dans votre bot pour effectuer la logique souhaitée.</span><span class="sxs-lookup"><span data-stu-id="6a45a-171">This is the message text you process in your bot to perform the desired logic.</span></span> |

> [!NOTE]
> <span data-ttu-id="6a45a-172">Le `value` champ est une chaîne simple.</span><span class="sxs-lookup"><span data-stu-id="6a45a-172">The `value` field is a simple string.</span></span> <span data-ttu-id="6a45a-173">Il n’existe aucune prise en charge de la mise en forme ou des caractères masqués.</span><span class="sxs-lookup"><span data-stu-id="6a45a-173">There is no support for formatting or hidden characters.</span></span>

# <a name="json"></a>[<span data-ttu-id="6a45a-174">JSON</span><span class="sxs-lookup"><span data-stu-id="6a45a-174">JSON</span></span>](#tab/json)

<span data-ttu-id="6a45a-175">Le code suivant montre un exemple de `imBack` type d’action dans JSON :</span><span class="sxs-lookup"><span data-stu-id="6a45a-175">The following code shows an example of `imBack` action type in JSON:</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[<span data-ttu-id="6a45a-176">C#</span><span class="sxs-lookup"><span data-stu-id="6a45a-176">C#</span></span>](#tab/csharp)

<span data-ttu-id="6a45a-177">Le code suivant montre un exemple de `imBack` type d’action dans C# :</span><span class="sxs-lookup"><span data-stu-id="6a45a-177">The following code shows an example of `imBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6a45a-178">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6a45a-178">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6a45a-179">Le code suivant montre un exemple de `imBack` type d’action en JavaScript :</span><span class="sxs-lookup"><span data-stu-id="6a45a-179">The following code shows an example of `imBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a><span data-ttu-id="6a45a-180">Appel de type d’action</span><span class="sxs-lookup"><span data-stu-id="6a45a-180">Action type invoke</span></span>

<span data-ttu-id="6a45a-181">`invoke`L’action est utilisée pour l’facturation des [modules de tâche.](~/task-modules-and-cards/task-modules/task-modules-bots.md)</span><span class="sxs-lookup"><span data-stu-id="6a45a-181">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="6a45a-182">`invoke`L’action contient trois `type` propriétés, et `title` `value` .</span><span class="sxs-lookup"><span data-stu-id="6a45a-182">The `invoke` action contains three properties, `type`, `title`, and `value`.</span></span>

<span data-ttu-id="6a45a-183">Avec `invoke` , vous pouvez créer une action avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a45a-183">With `invoke`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="6a45a-184">Propriété</span><span class="sxs-lookup"><span data-stu-id="6a45a-184">Property</span></span> | <span data-ttu-id="6a45a-185">Description</span><span class="sxs-lookup"><span data-stu-id="6a45a-185">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="6a45a-186">Apparaît en tant qu’étiquette de bouton.</span><span class="sxs-lookup"><span data-stu-id="6a45a-186">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="6a45a-187">Cette propriété peut contenir une chaîne, un objet JSON stringified ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="6a45a-187">This property can contain a string, a stringified JSON object, or a JSON object.</span></span> |

# <a name="json"></a>[<span data-ttu-id="6a45a-188">JSON</span><span class="sxs-lookup"><span data-stu-id="6a45a-188">JSON</span></span>](#tab/json)

<span data-ttu-id="6a45a-189">Le code suivant montre un exemple de `invoke` type d’action dans JSON :</span><span class="sxs-lookup"><span data-stu-id="6a45a-189">The following code shows an example of `invoke` action type in JSON:</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="6a45a-190">Lorsqu’un utilisateur sélectionne le bouton, votre bot reçoit `value` l’objet avec des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6a45a-190">When a user selects the button, your bot receives the `value` object with some additional information.</span></span>

> [!NOTE]
> <span data-ttu-id="6a45a-191">Le type d’activité `invoke` est au lieu de ce qui est `message` `activity.Type == "invoke"` .</span><span class="sxs-lookup"><span data-stu-id="6a45a-191">The activity type is `invoke` instead of `message` that is `activity.Type == "invoke"`.</span></span>

# <a name="c"></a>[<span data-ttu-id="6a45a-192">C#</span><span class="sxs-lookup"><span data-stu-id="6a45a-192">C#</span></span>](#tab/csharp)

<span data-ttu-id="6a45a-193">Le code suivant montre un exemple de `invoke` type d’action dans C# :</span><span class="sxs-lookup"><span data-stu-id="6a45a-193">The following code shows an example of `invoke` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6a45a-194">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6a45a-194">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6a45a-195">Le code suivant montre un exemple de `invoke` type d’action dans Node.js :</span><span class="sxs-lookup"><span data-stu-id="6a45a-195">The following code shows an example of `invoke` action type in Node.js:</span></span>

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a><span data-ttu-id="6a45a-196">Exemple de message d’appel entrant</span><span class="sxs-lookup"><span data-stu-id="6a45a-196">Example of incoming invoke message</span></span>

<span data-ttu-id="6a45a-197">La propriété de niveau `replyToId` supérieur contient l’ID du message d’où provenait l’action de carte.</span><span class="sxs-lookup"><span data-stu-id="6a45a-197">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="6a45a-198">Utilisez-le si vous souhaitez mettre à jour le message.</span><span class="sxs-lookup"><span data-stu-id="6a45a-198">Use it if you want to update the message.</span></span>

<span data-ttu-id="6a45a-199">Le code suivant illustre un exemple de message d’appel entrant :</span><span class="sxs-lookup"><span data-stu-id="6a45a-199">The following code shows an example of incoming invoke message:</span></span>

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="action-type-signin"></a><span data-ttu-id="6a45a-200">Signin du type d’action</span><span class="sxs-lookup"><span data-stu-id="6a45a-200">Action type signin</span></span>

<span data-ttu-id="6a45a-201">`signin` le type d’action lance un flux OAuth qui permet aux bots de se connecter à des services sécurisés.</span><span class="sxs-lookup"><span data-stu-id="6a45a-201">`signin` action type initiates an OAuth flow that permits bots to connect with secure services.</span></span> <span data-ttu-id="6a45a-202">Pour plus d’informations, voir [flux d’authentification dans les bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="6a45a-202">For more information, see [authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="6a45a-203">Teams prend également en charge [les actions de cartes adaptatives](#adaptive-cards-actions) qui sont utilisées uniquement par les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="6a45a-203">Teams also supports [Adaptive Cards actions](#adaptive-cards-actions) that are only used by Adaptive Cards.</span></span>

# <a name="json"></a>[<span data-ttu-id="6a45a-204">JSON</span><span class="sxs-lookup"><span data-stu-id="6a45a-204">JSON</span></span>](#tab/json)

<span data-ttu-id="6a45a-205">Le code suivant montre un exemple de `signin` type d’action dans JSON :</span><span class="sxs-lookup"><span data-stu-id="6a45a-205">The following code shows an example of `signin` action type in JSON:</span></span>

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[<span data-ttu-id="6a45a-206">C#</span><span class="sxs-lookup"><span data-stu-id="6a45a-206">C#</span></span>](#tab/csharp)

<span data-ttu-id="6a45a-207">Le code suivant montre un exemple de `signin` type d’action dans C# :</span><span class="sxs-lookup"><span data-stu-id="6a45a-207">The following code shows an example of `signin` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6a45a-208">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6a45a-208">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6a45a-209">Le code suivant montre un exemple de `signin` type d’action en JavaScript :</span><span class="sxs-lookup"><span data-stu-id="6a45a-209">The following code shows an example of `signin` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a><span data-ttu-id="6a45a-210">Actions de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="6a45a-210">Adaptive Cards actions</span></span>

<span data-ttu-id="6a45a-211">Les cartes adaptatives peuvent prendre en charge quatre types d’action :</span><span class="sxs-lookup"><span data-stu-id="6a45a-211">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="6a45a-212">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="6a45a-212">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="6a45a-213">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="6a45a-213">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="6a45a-214">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="6a45a-214">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="6a45a-215">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="6a45a-215">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="6a45a-216">Vous pouvez également modifier la charge utile de carte adaptative pour prendre en charge les actions Bot Framework existantes à l’aide d’une `Action.Submit` `msteams` propriété dans `data` l’objet de `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="6a45a-216">You can also modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using an `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="6a45a-217">La section suivante fournit des détails sur l’utilisation des actions Bot Framework existantes avec des cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="6a45a-217">The next section provide details on how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="6a45a-218">L’ajout de données avec une action Bot Framework ne fonctionne pas avec un module de tâche carte `msteams` adaptative.</span><span class="sxs-lookup"><span data-stu-id="6a45a-218">Adding `msteams` to data with a Bot Framework action does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="6a45a-219">Cartes adaptatives avec action messageBack</span><span class="sxs-lookup"><span data-stu-id="6a45a-219">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="6a45a-220">Pour inclure une `messageBack` action avec une carte adaptative, incluez les détails suivants dans l’objet `msteams` :</span><span class="sxs-lookup"><span data-stu-id="6a45a-220">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="6a45a-221">Vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6a45a-221">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="6a45a-222">Propriété</span><span class="sxs-lookup"><span data-stu-id="6a45a-222">Property</span></span> | <span data-ttu-id="6a45a-223">Description</span><span class="sxs-lookup"><span data-stu-id="6a45a-223">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="6a45a-224">Définir sur `messageBack` .</span><span class="sxs-lookup"><span data-stu-id="6a45a-224">Set to `messageBack`.</span></span> |
| `displayText` | <span data-ttu-id="6a45a-225">Facultatif.</span><span class="sxs-lookup"><span data-stu-id="6a45a-225">Optional.</span></span> <span data-ttu-id="6a45a-226">Utilisé par l’utilisateur dans le flux de conversation lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="6a45a-226">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="6a45a-227">Ce texte n’est pas envoyé à votre bot.</span><span class="sxs-lookup"><span data-stu-id="6a45a-227">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="6a45a-228">Envoyé à votre bot lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="6a45a-228">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="6a45a-229">Vous pouvez coder le contexte de l’action, par exemple des identificateurs uniques ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="6a45a-229">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="6a45a-230">Envoyé à votre bot lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="6a45a-230">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="6a45a-231">Utilisez cette propriété pour simplifier le développement de bots.</span><span class="sxs-lookup"><span data-stu-id="6a45a-231">Use this property to simplify bot development.</span></span> <span data-ttu-id="6a45a-232">Votre code peut vérifier une propriété de niveau supérieur unique pour envoyer la logique du bot.</span><span class="sxs-lookup"><span data-stu-id="6a45a-232">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="6a45a-233">Le code suivant illustre un exemple de cartes adaptatives avec `messageBack` action :</span><span class="sxs-lookup"><span data-stu-id="6a45a-233">The following code shows an example of Adaptive Cards with `messageBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="6a45a-234">Cartes adaptatives avec action imBack</span><span class="sxs-lookup"><span data-stu-id="6a45a-234">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="6a45a-235">Pour inclure une `imBack` action avec une carte adaptative, incluez les détails suivants dans l’objet `msteams` :</span><span class="sxs-lookup"><span data-stu-id="6a45a-235">To include an `imBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="6a45a-236">Vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6a45a-236">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="6a45a-237">Propriété</span><span class="sxs-lookup"><span data-stu-id="6a45a-237">Property</span></span> | <span data-ttu-id="6a45a-238">Description</span><span class="sxs-lookup"><span data-stu-id="6a45a-238">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="6a45a-239">Définir sur `imBack` .</span><span class="sxs-lookup"><span data-stu-id="6a45a-239">Set to `imBack`.</span></span> |
| `value` | <span data-ttu-id="6a45a-240">Chaîne qui doit être réassée dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="6a45a-240">String that needs to be echoed back in the chat.</span></span> |

<span data-ttu-id="6a45a-241">Le code suivant illustre un exemple de cartes adaptatives avec `imBack` action :</span><span class="sxs-lookup"><span data-stu-id="6a45a-241">The following code shows an example of Adaptive Cards with `imBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="6a45a-242">Cartes adaptatives avec action de signin</span><span class="sxs-lookup"><span data-stu-id="6a45a-242">Adaptive Cards with signin action</span></span>

<span data-ttu-id="6a45a-243">Pour inclure une `signin` action avec une carte adaptative, incluez les détails suivants dans l’objet `msteams` :</span><span class="sxs-lookup"><span data-stu-id="6a45a-243">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="6a45a-244">Vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6a45a-244">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="6a45a-245">Propriété</span><span class="sxs-lookup"><span data-stu-id="6a45a-245">Property</span></span> | <span data-ttu-id="6a45a-246">Description</span><span class="sxs-lookup"><span data-stu-id="6a45a-246">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="6a45a-247">Définir sur `signin` .</span><span class="sxs-lookup"><span data-stu-id="6a45a-247">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="6a45a-248">Définissez l’URL vers laquelle vous souhaitez rediriger.</span><span class="sxs-lookup"><span data-stu-id="6a45a-248">Set to the URL where you want to redirect.</span></span>  |

<span data-ttu-id="6a45a-249">Le code suivant illustre un exemple de cartes adaptatives avec `signin` action :</span><span class="sxs-lookup"><span data-stu-id="6a45a-249">The following code shows an example of Adaptive Cards with `signin` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="6a45a-250">Cartes adaptatives avec action d’appel</span><span class="sxs-lookup"><span data-stu-id="6a45a-250">Adaptive Cards with invoke action</span></span>

<span data-ttu-id="6a45a-251">Pour inclure une `invoke` action avec une carte adaptative, incluez les détails suivants dans l’objet `msteams` :</span><span class="sxs-lookup"><span data-stu-id="6a45a-251">To include an `invoke` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="6a45a-252">Vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6a45a-252">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="6a45a-253">Propriété</span><span class="sxs-lookup"><span data-stu-id="6a45a-253">Property</span></span> | <span data-ttu-id="6a45a-254">Description</span><span class="sxs-lookup"><span data-stu-id="6a45a-254">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="6a45a-255">Définir sur `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="6a45a-255">Set to `task/fetch`.</span></span> |
| `data` | <span data-ttu-id="6a45a-256">Définissez la valeur.</span><span class="sxs-lookup"><span data-stu-id="6a45a-256">Set the value.</span></span>  |

<span data-ttu-id="6a45a-257">Le code suivant illustre un exemple de cartes adaptatives avec `invoke` action :</span><span class="sxs-lookup"><span data-stu-id="6a45a-257">The following code shows an example of Adaptive Cards with `invoke` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit",
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

<span data-ttu-id="6a45a-258">Le code suivant illustre un exemple de cartes adaptatives `invoke` avec une action avec des données de charge utile supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="6a45a-258">The following code shows an example of Adaptive Cards with `invoke` action with additional payload data:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```

## <a name="see-also"></a><span data-ttu-id="6a45a-259">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6a45a-259">See also</span></span>

[<span data-ttu-id="6a45a-260">Référence de cartes</span><span class="sxs-lookup"><span data-stu-id="6a45a-260">Cards reference</span></span>](./cards-reference.md)

## <a name="next-step"></a><span data-ttu-id="6a45a-261">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="6a45a-261">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a45a-262">Actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="6a45a-262">Universal Actions for Adaptive Cards</span></span>](../cards/Universal-actions-for-adaptive-cards/Overview.md)
