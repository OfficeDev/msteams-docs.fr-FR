---
title: Ajouter des actions de carte dans un bot
description: Décrit les actions de carte dans Microsoft Teams et comment les utiliser dans vos bots
ms.localizationpriority: medium
ms.topic: conceptual
keywords: actions de cartes de bots teams
ms.openlocfilehash: 3509ab49f8e2031176743a9330ee3b6757b70277
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889327"
---
# <a name="card-actions"></a>Actions de carte

Les cartes utilisées par les bots et les extensions de messagerie Teams les types d’activité [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) suivants :

> [!NOTE]
> Les `CardAction` actions diffèrent des cartes Office 365 connecteur `potentialActions` lorsqu’elles sont utilisées à partir de connecteurs.

| Type | Action |
| --- | --- |
| `openUrl` | Ouvre une URL dans le navigateur par défaut. |
| `messageBack` | Envoie un message et une charge utile au bot à partir de l’utilisateur qui a sélectionné le bouton ou a tapé la carte. Envoie un message distinct au flux de conversation. |
| `imBack`| Envoie un message au bot de l’utilisateur qui a sélectionné le bouton ou a tapé la carte. Ce message de l’utilisateur au bot est visible par tous les participants à la conversation. |
| `invoke` | Envoie un message et une charge utile au bot à partir de l’utilisateur qui a sélectionné le bouton ou a tapé la carte. Ce message n’est pas visible. |
| `signin` | Lance le flux OAuth, ce qui permet aux bots de se connecter à des services sécurisés. |

> [!NOTE]
>* Teams ne prend pas en charge `CardAction` les types non répertoriés dans le tableau précédent.
>* Teams ne prend pas en charge la `potentialActions` propriété.
>* Les actions de carte sont différentes [des actions suggérées](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) dans Bot Framework ou Azure Bot Service. Les actions suggérées ne sont pas prises en charge dans Microsoft Teams. Si vous souhaitez que les boutons apparaissent sur un message Teams bot, utilisez une carte.
>* Si vous utilisez une action de carte dans le cadre d’une extension de messagerie, les actions ne fonctionnent pas tant que la carte n’est pas envoyée au canal. Les actions ne fonctionnent pas lorsque la carte se trouve dans la zone composer un message.

## <a name="action-type-openurl"></a>Type d’action openUrl

`openUrl` le type d’action spécifie une URL à lancer dans le navigateur par défaut.

> [!NOTE]
> Votre bot ne reçoit aucune notification sur le bouton sélectionné.

Avec `openUrl` , vous pouvez créer une action avec les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `title` | Apparaît en tant qu’étiquette de bouton. |
| `value` | Ce champ doit contenir une URL complète et correctement formée. |

# <a name="json"></a>[JSON](#tab/json)

Le code suivant montre un exemple de `openUrl` type d’action dans JSON :

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[C#](#tab/csharp)

Le code suivant montre un exemple de `openUrl` type d’action dans C# :

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Le code suivant montre un exemple de `openUrl` type d’action en JavaScript :

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a>Type d’action messageBack

Avec `messageBack` , vous pouvez créer une action entièrement personnalisée avec les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `title` | Apparaît en tant qu’étiquette de bouton. |
| `displayText` | Facultatif. Utilisé par l’utilisateur dans le flux de conversation lorsque l’action est effectuée. Ce texte n’est pas envoyé à votre bot. |
| `value` | Envoyé à votre bot lorsque l’action est effectuée. Vous pouvez coder le contexte de l’action, par exemple des identificateurs uniques ou un objet JSON. |
| `text` | Envoyé à votre bot lorsque l’action est effectuée. Utilisez cette propriété pour simplifier le développement de bots. Votre code peut vérifier une propriété de niveau supérieur unique pour envoyer la logique du bot. |

La flexibilité des moyens que votre code ne peut pas laisser un message utilisateur visible dans l’historique simplement `messageBack` en n’utilisant pas `displayText` .

# <a name="json"></a>[JSON](#tab/json)

Le code suivant montre un exemple de `messageBack` type d’action dans JSON :

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

La `value` propriété peut être une chaîne JSON sérialisée ou un objet JSON.

# <a name="c"></a>[C#](#tab/csharp)

Le code suivant montre un exemple de `messageBack` type d’action dans C# :

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Le code suivant montre un exemple de `messageBack` type d’action en JavaScript :

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

### <a name="inbound-message-example"></a>Exemple de message entrant

`replyToId` contient l’ID du message d’où provenait l’action de carte. Utilisez-le si vous souhaitez mettre à jour le message.

Le code suivant montre un exemple de message entrant :

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

## <a name="action-type-imback"></a>Type d’action imBack

L’action déclenche un message de retour à votre bot, comme si l’utilisateur l’avait tapé `imBack` dans un message de conversation normal. Votre utilisateur et tous les autres utilisateurs d’un canal peuvent voir la réponse du bouton.

Avec `imBack` , vous pouvez créer une action avec les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `title` | Apparaît en tant qu’étiquette de bouton. |
| `value` | Ce champ doit contenir la chaîne de texte utilisée dans la conversation et par conséquent renvoyée au bot. Il s’agit du texte du message que vous traiterez dans votre bot pour effectuer la logique souhaitée. |

> [!NOTE]
> Le `value` champ est une chaîne simple. Il n’existe aucune prise en charge de la mise en forme ou des caractères masqués.

# <a name="json"></a>[JSON](#tab/json)

Le code suivant montre un exemple de `imBack` type d’action dans JSON :

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[C#](#tab/csharp)

Le code suivant montre un exemple de `imBack` type d’action dans C# :

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Le code suivant montre un exemple de `imBack` type d’action en JavaScript :

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a>Appel de type d’action

`invoke`L’action est utilisée pour l’facturation des [modules de tâche.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

`invoke`L’action contient trois `type` propriétés, et `title` `value` .

Avec `invoke` , vous pouvez créer une action avec les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `title` | Apparaît en tant qu’étiquette de bouton. |
| `value` | Cette propriété peut contenir une chaîne, un objet JSON stringified ou un objet JSON. |

# <a name="json"></a>[JSON](#tab/json)

Le code suivant montre un exemple de `invoke` type d’action dans JSON :

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Lorsqu’un utilisateur sélectionne le bouton, votre bot reçoit `value` l’objet avec des informations supplémentaires.

> [!NOTE]
> Le type d’activité `invoke` est au lieu de ce qui est `message` `activity.Type == "invoke"` .

# <a name="c"></a>[C#](#tab/csharp)

Le code suivant montre un exemple de `invoke` type d’action dans C# :

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Le code suivant montre un exemple de `invoke` type d’action dans Node.js :

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

### <a name="example-of-incoming-invoke-message"></a>Exemple de message d’appel entrant

La propriété de niveau `replyToId` supérieur contient l’ID du message d’où provenait l’action de carte. Utilisez-le si vous souhaitez mettre à jour le message.

Le code suivant montre un exemple de message d’appel entrant :

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

## <a name="action-type-signin"></a>Signin du type d’action

`signin` le type d’action lance un flux OAuth qui permet aux bots de se connecter à des services sécurisés. Pour plus d’informations, voir [flux d’authentification dans les bots.](~/bots/how-to/authentication/auth-flow-bot.md)

Teams prend également en charge [les actions de cartes adaptatives](#adaptive-cards-actions) qui sont utilisées uniquement par les cartes adaptatives.

# <a name="json"></a>[JSON](#tab/json)

Le code suivant montre un exemple de `signin` type d’action dans JSON :

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[C#](#tab/csharp)

Le code suivant montre un exemple de `signin` type d’action dans C# :

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Le code suivant montre un exemple de `signin` type d’action en JavaScript :

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a>Actions de cartes adaptatives

Les cartes adaptatives peuvent prendre en charge quatre types d’action :

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

Vous pouvez également modifier la charge utile de carte adaptative pour prendre en charge les actions Bot Framework existantes à l’aide d’une `Action.Submit` `msteams` propriété dans `data` l’objet de `Action.Submit` . La section suivante fournit des détails sur l’utilisation des actions Bot Framework existantes avec des cartes adaptatives.

> [!NOTE]
> L’ajout de données avec une action Bot Framework ne fonctionne pas avec un module de tâche carte `msteams` adaptative.

### <a name="adaptive-cards-with-messageback-action"></a>Cartes adaptatives avec action messageBack

Pour inclure une `messageBack` action avec une carte adaptative, incluez les détails suivants dans l’objet `msteams` :

> [!NOTE]
> Vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet, si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Définir sur `messageBack` . |
| `displayText` | Facultatif. Utilisé par l’utilisateur dans le flux de conversation lorsque l’action est effectuée. Ce texte n’est pas envoyé à votre bot. |
| `value` | Envoyé à votre bot lorsque l’action est effectuée. Vous pouvez coder le contexte de l’action, par exemple des identificateurs uniques ou un objet JSON. |
| `text` | Envoyé à votre bot lorsque l’action est effectuée. Utilisez cette propriété pour simplifier le développement de bots. Votre code peut vérifier une propriété de niveau supérieur unique pour envoyer la logique du bot. |

Le code suivant illustre un exemple de cartes adaptatives avec `messageBack` action :

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

### <a name="adaptive-cards-with-imback-action"></a>Cartes adaptatives avec action imBack

Pour inclure une `imBack` action avec une carte adaptative, incluez les détails suivants dans l’objet `msteams` :

> [!NOTE]
> Vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet, si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Définir sur `imBack` . |
| `value` | Chaîne qui doit être réassée dans la conversation. |

Le code suivant illustre un exemple de cartes adaptatives avec `imBack` action :

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

### <a name="adaptive-cards-with-signin-action"></a>Cartes adaptatives avec action de signin

Pour inclure une `signin` action avec une carte adaptative, incluez les détails suivants dans l’objet `msteams` :

> [!NOTE]
> Vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet, si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Définir sur `signin` . |
| `value` | Définissez l’URL vers laquelle vous souhaitez rediriger.  |

Le code suivant illustre un exemple de cartes adaptatives avec `signin` action :

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

### <a name="adaptive-cards-with-invoke-action"></a>Cartes adaptatives avec action d’appel

Pour inclure une `invoke` action avec une carte adaptative, incluez les détails suivants dans l’objet `msteams` :

> [!NOTE]
> Vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet, si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Définir sur `task/fetch` . |
| `data` | Définissez la valeur.  |

Le code suivant illustre un exemple de cartes adaptatives avec `invoke` action :

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

Le code suivant illustre un exemple de cartes adaptatives `invoke` avec une action avec des données de charge utile supplémentaires :

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
## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Actions universelles pour les cartes adaptatives](../cards/Universal-actions-for-adaptive-cards/Overview.md)

## <a name="see-also"></a>Voir aussi

* [Référence de cartes](./cards-reference.md)
* [Utiliser des modules de tâches à partir de bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [Cartes adaptatives dans les bots](../../bots/how-to/conversations/conversation-messages.md#adaptive-cards)
* [Actions universelles pour les cartes adaptatives](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md)
