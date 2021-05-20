---
title: Ajouter des actions de carte dans un bot
description: Décrit les actions de Microsoft Teams et comment les utiliser dans vos bots
localization_priority: Normal
ms.topic: conceptual
keywords: équipes bots cartes actions
ms.openlocfilehash: b9276c7197070df43ba447707e6fa4d3d4098591
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566851"
---
# <a name="card-actions"></a><span data-ttu-id="51900-104">Actions de carte</span><span class="sxs-lookup"><span data-stu-id="51900-104">Card actions</span></span>

<span data-ttu-id="51900-105">Cartes utilisées par les bots et les extensions de messagerie dans Teams soutenir les types d’activité [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) suivants ( )</span><span class="sxs-lookup"><span data-stu-id="51900-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="51900-106">Notez que ces actions diffèrent de celles `potentialActions` des cartes connecteur Office 365 lorsqu’elles sont utilisées à partir de connecteurs.</span><span class="sxs-lookup"><span data-stu-id="51900-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="51900-107">Type</span><span class="sxs-lookup"><span data-stu-id="51900-107">Type</span></span> | <span data-ttu-id="51900-108">Action</span><span class="sxs-lookup"><span data-stu-id="51900-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="51900-109">Ouvre une URL dans le navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="51900-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="51900-110">Envoie un message et une charge utile au bot de l’utilisateur qui a cliqué sur le bouton ou tapé la carte et envoie un message distinct au flux de chat.</span><span class="sxs-lookup"><span data-stu-id="51900-110">Sends a message and payload to the bot from the user who clicked the button or tapped the card and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="51900-111">Envoie un message au bot de l’utilisateur qui a cliqué sur le bouton ou a tapé la carte.</span><span class="sxs-lookup"><span data-stu-id="51900-111">Sends a message to the bot from the user who clicked the button or tapped the card.</span></span> <span data-ttu-id="51900-112">Ce message (de l’utilisateur au bot) est visible par tous les participants à la conversation.</span><span class="sxs-lookup"><span data-stu-id="51900-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="51900-113">Envoie un message et une charge utile au bot de l’utilisateur qui a cliqué sur le bouton ou a tapé la carte.</span><span class="sxs-lookup"><span data-stu-id="51900-113">Sends a message and payload to the bot from the user who clicked the button or tapped the card.</span></span> <span data-ttu-id="51900-114">Ce message n’est pas visible.</span><span class="sxs-lookup"><span data-stu-id="51900-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="51900-115">Lance le flux OAuth, permettant aux bots de se connecter à des services sécurisés.</span><span class="sxs-lookup"><span data-stu-id="51900-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="51900-116">Teams ne prend pas en charge `CardAction` les types non répertoriés dans le tableau précédent.</span><span class="sxs-lookup"><span data-stu-id="51900-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="51900-117">Teams ne supporte pas la `potentialActions` propriété.</span><span class="sxs-lookup"><span data-stu-id="51900-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="51900-118">Les actions de carte sont différentes [des actions suggérées](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) dans Bot Framework/Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="51900-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="51900-119">Les actions suggérées ne sont pas prises en Microsoft Teams : si vous souhaitez que les boutons apparaissent sur un message Teams bot, utilisez une carte.</span><span class="sxs-lookup"><span data-stu-id="51900-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="51900-120">Si vous utilisez une action de carte dans le cadre d’une extension de messagerie, les actions ne fonctionnent pas tant que la carte n’est pas soumise au canal.</span><span class="sxs-lookup"><span data-stu-id="51900-120">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="51900-121">Ils ne fonctionnent pas pendant que la carte est dans la boîte de message de composition.</span><span class="sxs-lookup"><span data-stu-id="51900-121">They do not work while the card is in the compose message box.</span></span>

<span data-ttu-id="51900-122">Teams prend également en charge les [actions de cartes adaptatives,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)qui ne sont utilisées que par les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="51900-122">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="51900-123">Ces actions sont répertoriées dans leur propre section à la fin de cette référence.</span><span class="sxs-lookup"><span data-stu-id="51900-123">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="51900-124">openUrl</span><span class="sxs-lookup"><span data-stu-id="51900-124">openUrl</span></span>

<span data-ttu-id="51900-125">Ce type d’action spécifie une URL à lancer dans le navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="51900-125">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="51900-126">Notez que votre bot ne reçoit aucun avis sur quel bouton a été cliqué.</span><span class="sxs-lookup"><span data-stu-id="51900-126">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="51900-127">Le `value` champ doit contenir une URL complète et correctement formée.</span><span class="sxs-lookup"><span data-stu-id="51900-127">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="51900-128">messageBack</span><span class="sxs-lookup"><span data-stu-id="51900-128">messageBack</span></span>

<span data-ttu-id="51900-129">Avec `messageBack` , vous pouvez créer une action entièrement personnalisée avec les propriétés suivantes:</span><span class="sxs-lookup"><span data-stu-id="51900-129">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="51900-130">Propriété</span><span class="sxs-lookup"><span data-stu-id="51900-130">Property</span></span> | <span data-ttu-id="51900-131">Description</span><span class="sxs-lookup"><span data-stu-id="51900-131">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="51900-132">Apparaît sous forme d’étiquette de bouton.</span><span class="sxs-lookup"><span data-stu-id="51900-132">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="51900-133">Facultatif.</span><span class="sxs-lookup"><span data-stu-id="51900-133">Optional.</span></span> <span data-ttu-id="51900-134">Écho de l’utilisateur dans le flux de chat lorsque l’action est exécutée.</span><span class="sxs-lookup"><span data-stu-id="51900-134">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="51900-135">Ce texte *n’est* pas envoyé à votre bot.</span><span class="sxs-lookup"><span data-stu-id="51900-135">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="51900-136">Envoyé à votre bot lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="51900-136">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="51900-137">Vous pouvez coder le contexte de l’action, comme des identificateurs uniques ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="51900-137">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="51900-138">Envoyé à votre bot lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="51900-138">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="51900-139">Utilisez cette propriété pour simplifier le développement de bots : votre code peut vérifier une seule propriété de haut niveau pour envoyer la logique du bot.</span><span class="sxs-lookup"><span data-stu-id="51900-139">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="51900-140">La flexibilité des moyens `messageBack` que votre code peut choisir de ne pas laisser un message utilisateur visible dans l’histoire simplement en n’utilisant pas `displayText` .</span><span class="sxs-lookup"><span data-stu-id="51900-140">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="51900-141">La `value` propriété peut être soit une chaîne JSON sérialisée, soit un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="51900-141">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="51900-142">Exemple de message entrant</span><span class="sxs-lookup"><span data-stu-id="51900-142">Inbound message example</span></span>

<span data-ttu-id="51900-143">`replyToId` contient l’iD du message d’où provenait l’action de la carte.</span><span class="sxs-lookup"><span data-stu-id="51900-143">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="51900-144">Utilisez-le si vous souhaitez mettre à jour le message.</span><span class="sxs-lookup"><span data-stu-id="51900-144">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="51900-145">imBack imBack</span><span class="sxs-lookup"><span data-stu-id="51900-145">imBack</span></span>

<span data-ttu-id="51900-146">Cette action déclenche un message de retour à votre bot, comme si l’utilisateur l’avait tapé dans un message de chat normal.</span><span class="sxs-lookup"><span data-stu-id="51900-146">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="51900-147">Votre utilisateur, et tous les autres utilisateurs si dans un canal, verra cette réponse bouton.</span><span class="sxs-lookup"><span data-stu-id="51900-147">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="51900-148">Le `value` champ doit contenir la chaîne de texte écho dans le chat et donc renvoyé au bot.</span><span class="sxs-lookup"><span data-stu-id="51900-148">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="51900-149">C’est le texte de message que vous traiterez dans votre bot pour exécuter la logique désirée.</span><span class="sxs-lookup"><span data-stu-id="51900-149">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="51900-150">Remarque : ce champ est une chaîne simple - il n’y a pas de prise en charge pour le formatage ou les caractères cachés.</span><span class="sxs-lookup"><span data-stu-id="51900-150">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="51900-151">invoquer</span><span class="sxs-lookup"><span data-stu-id="51900-151">invoke</span></span>

<span data-ttu-id="51900-152">`invoke`L’action est utilisée pour invoquer des [modules de tâches](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="51900-152">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="51900-153">`invoke`L’action contient trois propriétés: , `type` , et `title` `value` .</span><span class="sxs-lookup"><span data-stu-id="51900-153">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="51900-154">La `value` propriété peut contenir une chaîne, un objet JSON stringifié ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="51900-154">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="51900-155">Lorsqu’un utilisateur clique sur le bouton, votre bot reçoit `value` l’objet avec quelques informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="51900-155">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="51900-156">Veuillez noter que le type d’activité sera `invoke` au lieu de ( `message` `activity.Type == "invoke"` ).</span><span class="sxs-lookup"><span data-stu-id="51900-156">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="51900-157">Exemple : Invoquer la définition du bouton (.NET)</span><span class="sxs-lookup"><span data-stu-id="51900-157">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="51900-158">Exemple : Message d’invocer entrant</span><span class="sxs-lookup"><span data-stu-id="51900-158">Example: Incoming invoke message</span></span>

<span data-ttu-id="51900-159">La propriété de haut `replyToId` niveau contient l’ID du message d’où provenait l’action de la carte.</span><span class="sxs-lookup"><span data-stu-id="51900-159">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="51900-160">Utilisez-le si vous souhaitez mettre à jour le message.</span><span class="sxs-lookup"><span data-stu-id="51900-160">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="51900-161">signin (signin)</span><span class="sxs-lookup"><span data-stu-id="51900-161">signin</span></span>

<span data-ttu-id="51900-162">Lance un flux OAuth, permettant aux bots de se connecter avec des services sécurisés, comme décrit plus en détail ici: Flux [d’authentification dans les bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="51900-162">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="51900-163">Actions cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="51900-163">Adaptive Cards actions</span></span>

<span data-ttu-id="51900-164">Les cartes adaptatives soutiennent quatre types d’action :</span><span class="sxs-lookup"><span data-stu-id="51900-164">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="51900-165">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="51900-165">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="51900-166">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="51900-166">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="51900-167">Action.ShowCard (en)</span><span class="sxs-lookup"><span data-stu-id="51900-167">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="51900-168">Action.Exemignon</span><span class="sxs-lookup"><span data-stu-id="51900-168">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="51900-169">En plus des actions mentionnées ci-dessus, vous pouvez modifier la charge utile de la carte `Action.Submit` adaptative pour prendre en charge les actions existantes bot framework en utilisant `msteams` une propriété dans `data` l’objet de `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="51900-169">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="51900-170">Les sections ci-dessous détaillent comment utiliser les actions existantes du Bot Framework avec les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="51900-170">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="51900-171">`msteams`L’ajout de données, avec une action Bot Framework, ne fonctionne pas avec un module de tâche de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="51900-171">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="51900-172">Cartes adaptatives avec action messageBack</span><span class="sxs-lookup"><span data-stu-id="51900-172">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="51900-173">Pour inclure une `messageBack` action avec une carte adaptative, incluez les détails suivants dans l’objet. `msteams`</span><span class="sxs-lookup"><span data-stu-id="51900-173">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="51900-174">Notez que vous pouvez inclure des propriétés cachées supplémentaires dans `data` l’objet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="51900-174">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="51900-175">Propriété</span><span class="sxs-lookup"><span data-stu-id="51900-175">Property</span></span> | <span data-ttu-id="51900-176">Description</span><span class="sxs-lookup"><span data-stu-id="51900-176">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="51900-177">se mettre à `messageBack`</span><span class="sxs-lookup"><span data-stu-id="51900-177">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="51900-178">Facultatif.</span><span class="sxs-lookup"><span data-stu-id="51900-178">Optional.</span></span> <span data-ttu-id="51900-179">Écho de l’utilisateur dans le flux de chat lorsque l’action est exécutée.</span><span class="sxs-lookup"><span data-stu-id="51900-179">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="51900-180">Ce texte *n’est* pas envoyé à votre bot.</span><span class="sxs-lookup"><span data-stu-id="51900-180">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="51900-181">Envoyé à votre bot lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="51900-181">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="51900-182">Vous pouvez coder le contexte de l’action, comme des identificateurs uniques ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="51900-182">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="51900-183">Envoyé à votre bot lorsque l’action est effectuée.</span><span class="sxs-lookup"><span data-stu-id="51900-183">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="51900-184">Utilisez cette propriété pour simplifier le développement de bots : votre code peut vérifier une seule propriété de haut niveau pour envoyer la logique du bot.</span><span class="sxs-lookup"><span data-stu-id="51900-184">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="51900-185">Exemple</span><span class="sxs-lookup"><span data-stu-id="51900-185">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="51900-186">Cartes adaptatives avec action imBack</span><span class="sxs-lookup"><span data-stu-id="51900-186">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="51900-187">Pour inclure une `imBack` action avec une carte adaptative, incluez les détails suivants dans l’objet. `msteams`</span><span class="sxs-lookup"><span data-stu-id="51900-187">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="51900-188">Notez que vous pouvez inclure des propriétés cachées supplémentaires dans `data` l’objet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="51900-188">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="51900-189">Propriété</span><span class="sxs-lookup"><span data-stu-id="51900-189">Property</span></span> | <span data-ttu-id="51900-190">Description</span><span class="sxs-lookup"><span data-stu-id="51900-190">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="51900-191">se mettre à `imBack`</span><span class="sxs-lookup"><span data-stu-id="51900-191">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="51900-192">Chaîne qui doit être repris dans le chat</span><span class="sxs-lookup"><span data-stu-id="51900-192">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="51900-193">Exemple</span><span class="sxs-lookup"><span data-stu-id="51900-193">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="51900-194">Cartes adaptatives avec action signin</span><span class="sxs-lookup"><span data-stu-id="51900-194">Adaptive Cards with signin action</span></span>

<span data-ttu-id="51900-195">Pour inclure une `signin` action avec une carte adaptative, incluez les détails suivants dans l’objet. `msteams`</span><span class="sxs-lookup"><span data-stu-id="51900-195">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="51900-196">Notez que vous pouvez inclure des propriétés cachées supplémentaires dans `data` l’objet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="51900-196">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="51900-197">Propriété</span><span class="sxs-lookup"><span data-stu-id="51900-197">Property</span></span> | <span data-ttu-id="51900-198">Description</span><span class="sxs-lookup"><span data-stu-id="51900-198">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="51900-199">Mis à `signin` .</span><span class="sxs-lookup"><span data-stu-id="51900-199">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="51900-200">Définissez l’URL vers qui vous souhaitez rediriger.</span><span class="sxs-lookup"><span data-stu-id="51900-200">Set to the URL that you want to redirect to.</span></span>  |

#### <a name="example"></a><span data-ttu-id="51900-201">Exemple</span><span class="sxs-lookup"><span data-stu-id="51900-201">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="51900-202">Cartes adaptatives avec action invocative</span><span class="sxs-lookup"><span data-stu-id="51900-202">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="51900-203">Pour inclure une `invoke` action avec une carte adaptative, incluez les détails suivants dans l’objet. `msteams`</span><span class="sxs-lookup"><span data-stu-id="51900-203">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="51900-204">Notez que vous pouvez inclure des propriétés cachées supplémentaires dans `data` l’objet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="51900-204">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="51900-205">Propriété</span><span class="sxs-lookup"><span data-stu-id="51900-205">Property</span></span> | <span data-ttu-id="51900-206">Description</span><span class="sxs-lookup"><span data-stu-id="51900-206">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="51900-207">se mettre à `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="51900-207">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="51900-208">Définir la valeur</span><span class="sxs-lookup"><span data-stu-id="51900-208">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="51900-209">Exemple</span><span class="sxs-lookup"><span data-stu-id="51900-209">Example</span></span>

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

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="51900-210">Exemple 2 (avec des données utiles supplémentaires)</span><span class="sxs-lookup"><span data-stu-id="51900-210">Example 2 (with additional payload data)</span></span>

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
