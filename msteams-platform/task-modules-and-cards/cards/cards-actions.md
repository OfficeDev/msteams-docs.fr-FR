---
title: Ajouter des actions de carte dans un bot
description: Décrit les actions de carte dans Microsoft teams et explique comment les utiliser dans vos robots
keywords: actions des cartes des robots teams
ms.openlocfilehash: e0b050cde9adf5bd811d5d95ce1c6f1bf60546a1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673744"
---
# <a name="card-actions"></a>Actions de carte

Les cartes utilisées par les robots et les extensions de messagerie dans teams[`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)prennent en charge les types d’activités () suivants. Notez que ces actions diffèrent `potentialActions` des cartes de connecteur Office 365 lorsqu’elles sont utilisées à partir de connecteurs.

| Type | Action |
| --- | --- |
| `openUrl` | Ouvre une URL dans le navigateur par défaut. |
| `messageBack` | Envoie un message et une charge utile au bot (à partir de l’utilisateur qui a cliqué sur le bouton ou a cliqué sur la carte) et envoie un message distinct au flux de conversation. |
| `imBack`| Envoie un message au bot (à partir de l’utilisateur qui a cliqué sur le bouton ou a cliqué sur la carte). Ce message (d’un utilisateur à un bot) est visible par tous les participants à la conversation. |
| `invoke` | Envoie un message et une charge utile au bot (à partir de l’utilisateur qui a cliqué sur le bouton ou a cliqué sur la carte). Ce message n’est pas visible. |
| `signin` | Lance le flux OAuth, ce qui permet aux robots de se connecter aux services sécurisés. |

> [!NOTE]
>* Teams ne prend `CardAction` pas en charge les types qui ne sont pas repris dans le tableau précédent.
>* Teams ne prend pas `potentialActions` en charge la propriété.
>* Les actions de carte diffèrent des [actions suggérées](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button) dans l’infrastructure bot/service de robot Azure. Les actions suggérées ne sont pas prises en charge dans Microsoft teams : Si vous souhaitez que les boutons apparaissent dans un message Team bot, utilisez une carte.
>* Si vous utilisez une action de carte dans le cadre d’une extension de messagerie, les actions ne fonctionnent pas tant que la carte n’est pas envoyée au canal (elles ne fonctionneront pas tant que la carte ne se trouve pas dans la boîte de message de composition).

Teams prend également en charge les [actions de cartes adaptatives](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), qui ne sont utilisées que par des cartes adaptatives. Ces actions sont répertoriées dans leur propre section à la fin de cette référence.

## <a name="openurl"></a>openUrl

Ce type d’action spécifie une URL à lancer dans le navigateur par défaut. Notez que votre bot ne reçoit pas de notification sur le bouton sur lequel l’utilisateur a cliqué.

Le `value` champ doit contenir une URL complète et correctement formée.

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

Avec `messageBack`, vous pouvez créer une action entièrement personnalisée avec les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `title` | S’affiche sous la forme de l’étiquette du bouton. |
| `displayText` | Facultatif. En écho par l’utilisateur dans le flux de conversation lors de l’exécution de l’action. Ce texte n’est *pas* envoyé à votre bot. |
| `value` | Envoyé à votre bot lors de l’exécution de l’action. Vous pouvez coder le contexte de l’action, comme des identificateurs uniques ou un objet JSON. |
| `text` | Envoyé à votre bot lors de l’exécution de l’action. Utilisez cette propriété pour simplifier le développement de robots : votre code peut vérifier une seule propriété de niveau supérieur pour répartir la logique du bot. |

La flexibilité de `messageBack` signifie que votre code peut choisir de ne pas laisser un message utilisateur visible dans l’historique simplement en ne `displayText`l’utilisant pas.

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

### <a name="inbound-message-example"></a>Exemple de message entrant

`replyToId`contient l’ID du message depuis lequel l’action de la carte provient. Utilisez-le si vous souhaitez mettre à jour le message.

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

## <a name="imback"></a>Annulation

Cette action déclenche un message de retour à votre bot, comme si l’utilisateur l’a tapée dans un message de conversation normal. Votre utilisateur, ainsi que tous les autres utilisateurs s’il s’agit d’un canal, verront cette réponse.

Le `value` champ doit contenir la chaîne de texte en écho dans la conversation et donc renvoyé au bot. Il s’agit du texte du message que vous allez traiter dans votre bot pour effectuer la logique souhaitée. Remarque : ce champ est une chaîne simple-il n’y a pas de prise en charge de la mise en forme ou des caractères masqués.

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>Appelez

L' `invoke` action est utilisée pour l’appel des [modules de tâches](~/task-modules-and-cards/task-modules/task-modules-bots.md).

L' `invoke` action contient trois propriétés : `type`, `title`et `value`. La `value` propriété peut contenir une chaîne, un objet JSON JSON ou un objet JSON.

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Lorsqu’un utilisateur clique sur le bouton, votre bot reçoit `value` l’objet avec des informations supplémentaires. Veuillez noter que le type d’activité sera `invoke` au lieu `message` de`activity.Type == "invoke"`().

### <a name="example-invoke-button-definition-net"></a>Exemple : définition du bouton Invoke (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>Exemple : message d’appel entrant

La propriété de niveau `replyToId` supérieur contient l’ID du message depuis lequel l’action de la carte provient. Utilisez-le si vous souhaitez mettre à jour le message.

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

## <a name="signin"></a>SignIn

Lance un flux OAuth, ce qui permet aux robots de se connecter à des services sécurisés, comme décrit plus en détail ici : [flux d’authentification dans les robots](~/bots/how-to/authentication/auth-flow-bot.md).

## <a name="adaptive-cards-actions"></a>Actions de cartes adaptatives

Les cartes adaptatives prennent en charge trois types d’actions :

* [Action. OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action. ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)

Outre les actions mentionnées ci-dessus, vous pouvez modifier la charge utile de `Action.Submit` la carte adaptative pour prendre en charge les actions `msteams` de l’infrastructure `data` de robot `Action.Submit`existantes à l’aide d’une propriété de l’objet de. Les sections ci-dessous expliquent en détail comment utiliser les actions de l’infrastructure bot existantes avec des cartes adaptatives.

### <a name="adaptive-cards-with-messageback-action"></a>Cartes adaptatives avec action messageBack

Pour inclure une `messageBack` action avec une carte adaptative, incluez les détails suivants dans `msteams` l’objet. Notez que vous pouvez inclure des propriétés masquées supplémentaires `data` dans l’objet si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Défini sur`messageBack` |
| `displayText` | Facultatif. En écho par l’utilisateur dans le flux de conversation lors de l’exécution de l’action. Ce texte n’est *pas* envoyé à votre bot. |
| `value` | Envoyé à votre bot lors de l’exécution de l’action. Vous pouvez coder le contexte de l’action, comme des identificateurs uniques ou un objet JSON. |
| `text` | Envoyé à votre bot lors de l’exécution de l’action. Utilisez cette propriété pour simplifier le développement de robots : votre code peut vérifier une seule propriété de niveau supérieur pour répartir la logique du bot. |

#### <a name="example"></a>Exemple

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

### <a name="adaptive-cards-with-imback-action"></a>Cartes adaptatives avec action d’annulation

Pour inclure une `imBack` action avec une carte adaptative, incluez les détails suivants dans `msteams` l’objet. Notez que vous pouvez inclure des propriétés masquées supplémentaires `data` dans l’objet si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Défini sur`imBack` |
| `value` | Chaîne qui doit être renvoyée en écho dans la conversation |

#### <a name="example"></a>Exemple

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

### <a name="adaptive-cards-with-signin-action"></a>Cartes adaptatives avec une action de connexion

Pour inclure une `signin` action avec une carte adaptative, incluez les détails suivants dans `msteams` l’objet. Notez que vous pouvez inclure des propriétés masquées supplémentaires `data` dans l’objet si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Défini sur`signin` |
| `value` | Défini sur l’URL vers laquelle vous voulez rediriger  |

#### <a name="example"></a>Exemple

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
