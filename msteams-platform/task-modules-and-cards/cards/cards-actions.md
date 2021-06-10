---
title: Ajouter des actions de carte dans un bot
description: Décrit les actions de carte dans Microsoft Teams et comment les utiliser dans vos bots
localization_priority: Normal
ms.topic: conceptual
keywords: actions de cartes de bots teams
ms.openlocfilehash: b9276c7197070df43ba447707e6fa4d3d4098591
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566851"
---
# <a name="card-actions"></a>Actions de carte

Les cartes utilisées par les bots et les extensions de messagerie Teams les types d’activité [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) suivants ( ). Notez que ces actions diffèrent des cartes `potentialActions` Office 365 connecteur lorsqu’elles sont utilisées à partir de connecteurs.

| Type | Action |
| --- | --- |
| `openUrl` | Ouvre une URL dans le navigateur par défaut. |
| `messageBack` | Envoie un message et une charge utile au bot à partir de l’utilisateur qui a cliqué sur le bouton ou a tapé la carte et envoie un message distinct au flux de conversation. |
| `imBack`| Envoie un message au bot de l’utilisateur qui a cliqué sur le bouton ou a tapé la carte. Ce message (de l’utilisateur au bot) est visible par tous les participants à la conversation. |
| `invoke` | Envoie un message et une charge utile au bot à partir de l’utilisateur qui a cliqué sur le bouton ou a tapé la carte. Ce message n’est pas visible. |
| `signin` | Lance le flux OAuth, ce qui permet aux bots de se connecter à des services sécurisés. |

> [!NOTE]
>* Teams ne prend pas en charge `CardAction` les types non répertoriés dans le tableau précédent.
>* Teams ne prend pas en charge la `potentialActions` propriété.
>* Les actions de carte sont différentes [des actions suggérées](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) dans Bot Framework/Azure Bot Service. Les actions suggérées ne sont pas prises en charge dans Microsoft Teams : si vous souhaitez que les boutons apparaissent sur un message Teams bot, utilisez une carte.
>* Si vous utilisez une action de carte dans le cadre d’une extension de messagerie, les actions ne fonctionnent pas tant que la carte n’est pas envoyée au canal. Elles ne fonctionnent pas lorsque la carte se trouve dans la zone composer un message.

Teams prend également en charge [les actions de cartes adaptatives,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)qui sont utilisées uniquement par les cartes adaptatives. Ces actions sont répertoriées dans leur propre section à la fin de cette référence.

## <a name="openurl"></a>openUrl

Ce type d’action spécifie une URL à lancer dans le navigateur par défaut. Notez que votre bot ne reçoit aucune notification sur le bouton sur lequel vous avez cliqué.

Le `value` champ doit contenir une URL complète et correctement formée.

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

Avec `messageBack` , vous pouvez créer une action entièrement personnalisée avec les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `title` | Apparaît en tant qu’étiquette de bouton. |
| `displayText` | Facultatif. Écho de l’utilisateur dans le flux de conversation lorsque l’action est effectuée. Ce texte *n’est pas* envoyé à votre bot. |
| `value` | Envoyé à votre bot lorsque l’action est effectuée. Vous pouvez coder le contexte de l’action, par exemple des identificateurs uniques ou un objet JSON. |
| `text` | Envoyé à votre bot lorsque l’action est effectuée. Utilisez cette propriété pour simplifier le développement de bots : votre code peut vérifier une propriété de niveau supérieur unique pour envoyer la logique du bot. |

La flexibilité des moyens que votre code peut choisir de ne pas laisser de message utilisateur visible dans l’historique simplement `messageBack` en n’utilisant pas `displayText` .

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

`replyToId` contient l’ID du message d’où provenait l’action de carte. Utilisez-le si vous souhaitez mettre à jour le message.

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

## <a name="imback"></a>imBack

Cette action déclenche un message de retour à votre bot, comme si l’utilisateur l’avait tapé dans un message de conversation normal. Votre utilisateur et tous les autres utilisateurs, s’ils sont dans un canal, voient cette réponse de bouton.

Le champ doit contenir la chaîne de texte résoyée dans la conversation et `value` par conséquent renvoyée au bot. Il s’agit du texte du message que vous allez traiter dans votre bot pour effectuer la logique souhaitée. Remarque : ce champ est une chaîne simple : il n’existe aucune prise en charge de la mise en forme ou des caractères masqués.

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>invoke

`invoke`L’action est utilisée pour l’facturation des [modules de tâche.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

`invoke`L’action contient trois propriétés : `type` , et `title` `value` . La `value` propriété peut contenir une chaîne, un objet JSON stringified ou un objet JSON.

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Lorsqu’un utilisateur clique sur le bouton, votre bot reçoit `value` l’objet avec des informations supplémentaires. Veuillez noter que le type d’activité sera `invoke` au lieu de ( `message` `activity.Type == "invoke"` ).

### <a name="example-invoke-button-definition-net"></a>Exemple : Définition du bouton d’appel (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>Exemple : message d’appel entrant

La propriété de niveau `replyToId` supérieur contient l’ID du message d’où provenait l’action de carte. Utilisez-le si vous souhaitez mettre à jour le message.

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

## <a name="signin"></a>signin

Lance un flux OAuth, ce qui permet aux bots de se connecter à des services sécurisés, comme décrit plus en détail ici : Flux d’authentification [dans les bots](~/bots/how-to/authentication/auth-flow-bot.md).

## <a name="adaptive-cards-actions"></a>Actions de cartes adaptatives

Les cartes adaptatives peuvent prendre en charge quatre types d’action :

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

Outre les actions mentionnées ci-dessus, vous pouvez modifier la charge utile de carte adaptative pour prendre en charge les actions Bot Framework existantes à l’aide d’une propriété dans `Action.Submit` `msteams` `data` l’objet de `Action.Submit` . Les sections ci-dessous détaillent l’utilisation des actions Bot Framework existantes avec des cartes adaptatives.

> [!NOTE]
> L’ajout à des données, avec une action Bot Framework, ne fonctionne pas avec un module de tâche de `msteams` carte adaptative.

### <a name="adaptive-cards-with-messageback-action"></a>Cartes adaptatives avec action messageBack

Pour inclure une `messageBack` action avec une carte adaptative, incluez les détails suivants dans `msteams` l’objet. Notez que vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Définir sur `messageBack` |
| `displayText` | Facultatif. Écho de l’utilisateur dans le flux de conversation lorsque l’action est effectuée. Ce texte *n’est pas* envoyé à votre bot. |
| `value` | Envoyé à votre bot lorsque l’action est effectuée. Vous pouvez coder le contexte de l’action, par exemple des identificateurs uniques ou un objet JSON. |
| `text` | Envoyé à votre bot lorsque l’action est effectuée. Utilisez cette propriété pour simplifier le développement de bots : votre code peut vérifier une propriété de niveau supérieur unique pour envoyer la logique du bot. |

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

### <a name="adaptive-cards-with-imback-action"></a>Cartes adaptatives avec action imBack

Pour inclure une `imBack` action avec une carte adaptative, incluez les détails suivants dans `msteams` l’objet. Notez que vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Définir sur `imBack` |
| `value` | Chaîne devant faire l’écho dans la conversation |

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

### <a name="adaptive-cards-with-signin-action"></a>Cartes adaptatives avec action de signin

Pour inclure une `signin` action avec une carte adaptative, incluez les détails suivants dans `msteams` l’objet. Notez que vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Définir sur `signin` . |
| `value` | Définissez l’URL vers qui vous souhaitez rediriger.  |

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

### <a name="adaptive-cards-with-invoke-action"></a>Cartes adaptatives avec action d’appel
 
Pour inclure une `invoke` action avec une carte adaptative, incluez les détails suivants dans `msteams` l’objet. Notez que vous pouvez inclure des propriétés masquées supplémentaires dans `data` l’objet si nécessaire.

| Propriété | Description |
| --- | --- |
| `type` | Définir sur `task/fetch` |
| `data` | Définir la valeur  |

#### <a name="example"></a>Exemple

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

#### <a name="example-2-with-additional-payload-data"></a>Exemple 2 (avec des données de charge utile supplémentaires)

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
