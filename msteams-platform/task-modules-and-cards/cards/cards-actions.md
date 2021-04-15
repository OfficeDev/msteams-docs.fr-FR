---
title: Ajouter des actions de carte dans un bot
description: Décrit les actions de carte dans Microsoft Teams et leur utilisation dans vos bots
ms.topic: conceptual
keywords: actions de cartes de bots teams
ms.openlocfilehash: f02e195f619fdfa2ebbc4b2ef00669a1cb5b38f6
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696023"
---
# <a name="card-actions"></a><span data-ttu-id="06926-104">Actions de carte</span><span class="sxs-lookup"><span data-stu-id="06926-104">Card actions</span></span>

<span data-ttu-id="06926-105">Les cartes utilisées par les bots et les extensions de messagerie dans Teams supportent les types d'activité [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ( ) suivants.</span><span class="sxs-lookup"><span data-stu-id="06926-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="06926-106">Notez que ces actions diffèrent des cartes de connecteur `potentialActions` Office 365 lorsqu'elles sont utilisées à partir de connecteurs.</span><span class="sxs-lookup"><span data-stu-id="06926-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="06926-107">Type</span><span class="sxs-lookup"><span data-stu-id="06926-107">Type</span></span> | <span data-ttu-id="06926-108">Action</span><span class="sxs-lookup"><span data-stu-id="06926-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="06926-109">Ouvre une URL dans le navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="06926-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="06926-110">Envoie un message et une charge utile au bot (à partir de l'utilisateur qui a cliqué sur le bouton ou a tapé la carte) et envoie un message distinct au flux de conversation.</span><span class="sxs-lookup"><span data-stu-id="06926-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="06926-111">Envoie un message au bot (à partir de l'utilisateur qui a cliqué sur le bouton ou a tapé la carte).</span><span class="sxs-lookup"><span data-stu-id="06926-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="06926-112">Ce message (de l'utilisateur au bot) est visible par tous les participants à la conversation.</span><span class="sxs-lookup"><span data-stu-id="06926-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="06926-113">Envoie un message et une charge utile au bot (à partir de l'utilisateur qui a cliqué sur le bouton ou a tapé la carte).</span><span class="sxs-lookup"><span data-stu-id="06926-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="06926-114">Ce message n'est pas visible.</span><span class="sxs-lookup"><span data-stu-id="06926-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="06926-115">Lance le flux OAuth, ce qui permet aux bots de se connecter à des services sécurisés.</span><span class="sxs-lookup"><span data-stu-id="06926-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="06926-116">Teams ne prend pas en charge `CardAction` les types non répertoriés dans le tableau précédent.</span><span class="sxs-lookup"><span data-stu-id="06926-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="06926-117">Teams ne prend pas en charge la `potentialActions` propriété.</span><span class="sxs-lookup"><span data-stu-id="06926-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="06926-118">Les actions de carte sont différentes [des actions suggérées](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) dans Bot Framework/Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="06926-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="06926-119">Les actions suggérées ne sont pas prises en charge dans Microsoft Teams : si vous souhaitez que les boutons apparaissent dans un message de bot Teams, utilisez une carte.</span><span class="sxs-lookup"><span data-stu-id="06926-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="06926-120">Si vous utilisez une action de carte dans le cadre d'une extension de messagerie, les actions ne fonctionneront pas tant que la carte n'aura pas été envoyée au canal (elles ne fonctionneront pas tant que la carte ne sera pas dans la zone de composition du message).</span><span class="sxs-lookup"><span data-stu-id="06926-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="06926-121">Teams prend également en [charge les actions de cartes adaptatives,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)qui sont utilisées uniquement par les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="06926-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="06926-122">Ces actions sont répertoriées dans leur propre section à la fin de cette référence.</span><span class="sxs-lookup"><span data-stu-id="06926-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="06926-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="06926-123">openUrl</span></span>

<span data-ttu-id="06926-124">Ce type d'action spécifie une URL à lancer dans le navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="06926-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="06926-125">Notez que votre bot ne reçoit aucune notification sur le bouton sur lequel vous avez cliqué.</span><span class="sxs-lookup"><span data-stu-id="06926-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="06926-126">Le `value` champ doit contenir une URL complète et correctement formée.</span><span class="sxs-lookup"><span data-stu-id="06926-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="06926-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="06926-127">messageBack</span></span>

<span data-ttu-id="06926-128">Avec `messageBack` , vous pouvez créer une action entièrement personnalisée avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="06926-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="06926-129">Propriété</span><span class="sxs-lookup"><span data-stu-id="06926-129">Property</span></span> | <span data-ttu-id="06926-130">Description</span><span class="sxs-lookup"><span data-stu-id="06926-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="06926-131">Apparaît en tant qu'étiquette de bouton.</span><span class="sxs-lookup"><span data-stu-id="06926-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="06926-132">Facultatif.</span><span class="sxs-lookup"><span data-stu-id="06926-132">Optional.</span></span> <span data-ttu-id="06926-133">Écho de l'utilisateur dans le flux de conversation lorsque l'action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="06926-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="06926-134">Ce texte *n'est* pas envoyé à votre bot.</span><span class="sxs-lookup"><span data-stu-id="06926-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="06926-135">Envoyé à votre bot lorsque l'action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="06926-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="06926-136">Vous pouvez coder le contexte de l'action, par exemple des identificateurs uniques ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="06926-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="06926-137">Envoyé à votre bot lorsque l'action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="06926-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="06926-138">Utilisez cette propriété pour simplifier le développement de bots : votre code peut vérifier une propriété de niveau supérieur unique pour envoyer la logique du bot.</span><span class="sxs-lookup"><span data-stu-id="06926-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="06926-139">La flexibilité des moyens que votre code peut choisir de ne pas laisser un message utilisateur visible dans l'historique `messageBack` simplement en n'utilisant pas `displayText` .</span><span class="sxs-lookup"><span data-stu-id="06926-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="06926-140">La `value` propriété peut être une chaîne JSON sérialisée ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="06926-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="06926-141">Exemple de message entrant</span><span class="sxs-lookup"><span data-stu-id="06926-141">Inbound message example</span></span>

<span data-ttu-id="06926-142">`replyToId` contient l'ID du message d'où provenait l'action de carte.</span><span class="sxs-lookup"><span data-stu-id="06926-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="06926-143">Utilisez-le si vous souhaitez mettre à jour le message.</span><span class="sxs-lookup"><span data-stu-id="06926-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="06926-144">imBack</span><span class="sxs-lookup"><span data-stu-id="06926-144">imBack</span></span>

<span data-ttu-id="06926-145">Cette action déclenche un message de retour à votre bot, comme si l'utilisateur l'avait tapé dans un message de conversation normal.</span><span class="sxs-lookup"><span data-stu-id="06926-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="06926-146">Votre utilisateur et tous les autres utilisateurs, s'ils sont dans un canal, voient cette réponse de bouton.</span><span class="sxs-lookup"><span data-stu-id="06926-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="06926-147">Le champ doit contenir la chaîne de texte résoyée dans la conversation et `value` par conséquent renvoyée au bot.</span><span class="sxs-lookup"><span data-stu-id="06926-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="06926-148">Il s'agit du texte du message que vous allez traiter dans votre bot pour effectuer la logique souhaitée.</span><span class="sxs-lookup"><span data-stu-id="06926-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="06926-149">Remarque : ce champ est une chaîne simple : il n'existe aucune prise en charge de la mise en forme ou des caractères masqués.</span><span class="sxs-lookup"><span data-stu-id="06926-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="06926-150">invoke</span><span class="sxs-lookup"><span data-stu-id="06926-150">invoke</span></span>

<span data-ttu-id="06926-151">`invoke`L'action est utilisée pour l'facturation des [modules de tâche.](~/task-modules-and-cards/task-modules/task-modules-bots.md)</span><span class="sxs-lookup"><span data-stu-id="06926-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="06926-152">`invoke`L'action contient trois propriétés : `type` , et `title` `value` .</span><span class="sxs-lookup"><span data-stu-id="06926-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="06926-153">La `value` propriété peut contenir une chaîne, un objet JSON stringified ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="06926-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="06926-154">Lorsqu'un utilisateur clique sur le bouton, votre bot reçoit `value` l'objet avec des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="06926-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="06926-155">Veuillez noter que le type d'activité sera `invoke` au lieu de ( `message` `activity.Type == "invoke"` ).</span><span class="sxs-lookup"><span data-stu-id="06926-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="06926-156">Exemple : Définition du bouton d'appel (.NET)</span><span class="sxs-lookup"><span data-stu-id="06926-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="06926-157">Exemple : Message d'appel entrant</span><span class="sxs-lookup"><span data-stu-id="06926-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="06926-158">La propriété de niveau `replyToId` supérieur contient l'ID du message d'où provenait l'action de carte.</span><span class="sxs-lookup"><span data-stu-id="06926-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="06926-159">Utilisez-le si vous souhaitez mettre à jour le message.</span><span class="sxs-lookup"><span data-stu-id="06926-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="06926-160">signin</span><span class="sxs-lookup"><span data-stu-id="06926-160">signin</span></span>

<span data-ttu-id="06926-161">Lance un flux OAuth, ce qui permet aux bots de se connecter à des services sécurisés, comme décrit plus en détail ici : Flux d'authentification [dans les bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="06926-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="06926-162">Actions de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="06926-162">Adaptive Cards actions</span></span>

<span data-ttu-id="06926-163">Les cartes adaptatives peuvent prendre en charge trois types d'action :</span><span class="sxs-lookup"><span data-stu-id="06926-163">Adaptive Cards support three action types:</span></span>

* [<span data-ttu-id="06926-164">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="06926-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="06926-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="06926-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="06926-166">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="06926-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)

<span data-ttu-id="06926-167">Outre les actions mentionnées ci-dessus, vous pouvez modifier la charge utile de carte adaptative pour prendre en charge les actions Bot Framework existantes à l'aide d'une propriété dans `Action.Submit` `msteams` `data` l'objet de `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="06926-167">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="06926-168">Les sections ci-dessous détaillent l'utilisation des actions Bot Framework existantes avec des cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="06926-168">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="06926-169">L'ajout à des données, avec une action Bot Framework, ne fonctionne pas avec un module de tâche de `msteams` carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="06926-169">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="06926-170">Cartes adaptatives avec action messageBack</span><span class="sxs-lookup"><span data-stu-id="06926-170">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="06926-171">Pour inclure une `messageBack` action avec une carte adaptative, incluez les détails suivants dans `msteams` l'objet.</span><span class="sxs-lookup"><span data-stu-id="06926-171">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="06926-172">Notez que vous pouvez inclure des propriétés masquées supplémentaires dans `data` l'objet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="06926-172">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="06926-173">Propriété</span><span class="sxs-lookup"><span data-stu-id="06926-173">Property</span></span> | <span data-ttu-id="06926-174">Description</span><span class="sxs-lookup"><span data-stu-id="06926-174">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="06926-175">Définir sur `messageBack`</span><span class="sxs-lookup"><span data-stu-id="06926-175">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="06926-176">Facultatif.</span><span class="sxs-lookup"><span data-stu-id="06926-176">Optional.</span></span> <span data-ttu-id="06926-177">Écho de l'utilisateur dans le flux de conversation lorsque l'action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="06926-177">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="06926-178">Ce texte *n'est pas* envoyé à votre bot.</span><span class="sxs-lookup"><span data-stu-id="06926-178">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="06926-179">Envoyé à votre bot lorsque l'action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="06926-179">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="06926-180">Vous pouvez coder le contexte de l'action, par exemple des identificateurs uniques ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="06926-180">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="06926-181">Envoyé à votre bot lorsque l'action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="06926-181">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="06926-182">Utilisez cette propriété pour simplifier le développement de bots : votre code peut vérifier une propriété de niveau supérieur unique pour envoyer la logique du bot.</span><span class="sxs-lookup"><span data-stu-id="06926-182">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="06926-183">Exemple</span><span class="sxs-lookup"><span data-stu-id="06926-183">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="06926-184">Cartes adaptatives avec action imBack</span><span class="sxs-lookup"><span data-stu-id="06926-184">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="06926-185">Pour inclure une `imBack` action avec une carte adaptative, incluez les détails suivants dans `msteams` l'objet.</span><span class="sxs-lookup"><span data-stu-id="06926-185">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="06926-186">Notez que vous pouvez inclure des propriétés masquées supplémentaires dans `data` l'objet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="06926-186">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="06926-187">Propriété</span><span class="sxs-lookup"><span data-stu-id="06926-187">Property</span></span> | <span data-ttu-id="06926-188">Description</span><span class="sxs-lookup"><span data-stu-id="06926-188">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="06926-189">Définir sur `imBack`</span><span class="sxs-lookup"><span data-stu-id="06926-189">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="06926-190">Chaîne qui doit être ré-reprise dans la conversation</span><span class="sxs-lookup"><span data-stu-id="06926-190">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="06926-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="06926-191">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="06926-192">Cartes adaptatives avec action de signin</span><span class="sxs-lookup"><span data-stu-id="06926-192">Adaptive Cards with signin action</span></span>

<span data-ttu-id="06926-193">Pour inclure une `signin` action avec une carte adaptative, incluez les détails suivants dans `msteams` l'objet.</span><span class="sxs-lookup"><span data-stu-id="06926-193">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="06926-194">Notez que vous pouvez inclure des propriétés masquées supplémentaires dans `data` l'objet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="06926-194">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="06926-195">Propriété</span><span class="sxs-lookup"><span data-stu-id="06926-195">Property</span></span> | <span data-ttu-id="06926-196">Description</span><span class="sxs-lookup"><span data-stu-id="06926-196">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="06926-197">Définir sur `signin`</span><span class="sxs-lookup"><span data-stu-id="06926-197">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="06926-198">Définir sur l'URL vers qui vous souhaitez rediriger</span><span class="sxs-lookup"><span data-stu-id="06926-198">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="06926-199">Exemple</span><span class="sxs-lookup"><span data-stu-id="06926-199">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="06926-200">Cartes adaptatives avec action d'appel</span><span class="sxs-lookup"><span data-stu-id="06926-200">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="06926-201">Pour inclure une `invoke` action avec une carte adaptative, incluez les détails suivants dans `msteams` l'objet.</span><span class="sxs-lookup"><span data-stu-id="06926-201">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="06926-202">Notez que vous pouvez inclure des propriétés masquées supplémentaires dans `data` l'objet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="06926-202">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="06926-203">Propriété</span><span class="sxs-lookup"><span data-stu-id="06926-203">Property</span></span> | <span data-ttu-id="06926-204">Description</span><span class="sxs-lookup"><span data-stu-id="06926-204">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="06926-205">Définir sur `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="06926-205">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="06926-206">Définir la valeur</span><span class="sxs-lookup"><span data-stu-id="06926-206">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="06926-207">Exemple</span><span class="sxs-lookup"><span data-stu-id="06926-207">Example</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="06926-208">Exemple 2 (avec des données de charge utile supplémentaires)</span><span class="sxs-lookup"><span data-stu-id="06926-208">Example 2 (with additional payload data)</span></span>

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
