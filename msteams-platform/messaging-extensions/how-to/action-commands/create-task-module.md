---
title: Créer et envoyer un module de tâche
author: surbhigupta
description: Dans ce module, découvrez comment gérer l’action d’appel initiale et répondre avec un module de tâche à partir d’une commande d’extension de messagerie d’action
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58b5d246c113262fa478a36246a224a52d160154
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035183"
---
# <a name="create-and-send-task-module"></a>Créer et envoyer un module de tâche

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Vous pouvez créer le module de tâches en utilisant une carte adaptative ou une vue Web intégrée. Pour créer un module de tâches, vous devez effectuer le processus appelé demande d'invocation initiale. Ce document couvre la demande initiale d'invocation, les propriétés de l'activité de la charge utile lorsqu'un module de tâches est invoqué à partir d'un chat 1:1, d'un chat de groupe, d'un canal (nouveau message), d'un canal (réponse à un fil de discussion) et d'une boîte de commande.
> [!NOTE]
> Si vous ne remplissez pas le module de tâches avec les paramètres définis dans le manifeste de l'application, vous devez créer le module de tâches pour les utilisateurs avec une carte adaptative ou une vue Web intégrée.

## <a name="the-initial-invoke-request"></a>La demande initiale d'invocation

Au cours de la demande d'invocation initiale, votre service reçoit un `Activity`objet de type`composeExtension/fetchTask` , et vous devez répondre avec un`task` objet contenant soit une carte adaptative, soit une URL vers la vue Web intégrée. En plus des propriétés standard de l'activité du bot, la charge utile de l'invocation initiale contient les métadonnées de demande suivantes :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de requête. Il doit être `invoke`. |
|`name`| Type de commande envoyée à votre service. Il doit être `composeExtension/fetchTask`. |
|`from.id`| Identification de l'utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l'utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| Identification de l'objet Azure Active Directory de l'utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.channel.id`| Identification du canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| Identification de l'équipe (si la demande a été faite dans un canal). |
|`value.commandId` | Contient le numéro d'identification de la commande qui a été invoquée. |
|`value.commandContext` | Le contexte qui a déclenché l'événement. Il doit être `compose`. |
|`value.context.theme` | Le thème client de l'utilisateur, utile pour le formatage des vues Web intégrées. Il doit être`default` ,`contrast` ou`dark`. |

### <a name="example"></a>Exemple

Le code de la demande initiale d'invocation est donné dans l'exemple suivant :

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a>Propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'un chat 1:1.

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir du chat 1:1 sont énumérées ci-dessous :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de requête. Il doit être `invoke`. |
|`name`| Type de commande envoyée à votre service. Il doit être `composeExtension/fetchTask`. |
|`from.id`| Identification de l'utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l'utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| Identification de l'objet Azure Active Directory de l'utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.source.name`| Le nom de la source à partir de laquelle le module de tâche est invoqué. |
|`ChannelData.legacy. replyToId`| Obtient ou définit le numéro d'identification du message auquel ce message est une réponse. |
|`value.commandId` | Contient le numéro d'identification de la commande qui a été invoquée. |
|`value.commandContext` | Le contexte qui a déclenché l'événement. Il doit être `compose`. |
|`value.context.theme` | Le thème client de l'utilisateur, utile pour le formatage des vues Web intégrées. Il doit être`default` ,`contrast` ou`dark`. |

### <a name="example"></a>Exemple

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir du chat 1:1 sont données dans l'exemple suivant :

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a>Propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir de la conversation de groupe.

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir de la conversation de groupe sont énumérées ci-dessous :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de requête. Il doit être `invoke`. |
|`name`| Type de commande envoyée à votre service. Il doit être `composeExtension/fetchTask`. |
|`from.id`| Identification de l'utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l'utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| Identification de l'objet Azure Active Directory de l'utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.source.name`| Le nom de la source à partir de laquelle le module de tâche est invoqué. |
|`ChannelData.legacy. replyToId`| Obtient ou définit le numéro d'identification du message auquel ce message est une réponse. |
|`value.commandId` | Contient le numéro d'identification de la commande qui a été invoquée. |
|`value.commandContext` | Le contexte qui a déclenché l'événement. Il doit être `compose`. |
|`value.context.theme` | Le thème client de l'utilisateur, utile pour le formatage des vues Web intégrées. Il doit être`default` ,`contrast` ou`dark`. |

### <a name="example"></a>Exemple

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'un chat de groupe sont données dans l'exemple suivant :

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-meeting-chat"></a>Propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir de la conversation d'une réunion.

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir de la conversation de réunion sont données dans l'exemple suivant :

```json
{
   "type": "invoke",
   "id": "f:4d271f11-4eed-622f-e820-6d82bf91692f",
   "channelId": "msteams",
   "from": {
      "id": "29:1yLsdbTM1UjxqqD8cjduNUCI1jm8xZaH3lx9u5JQ04t2bknuTCkP45TXdfROTOWk1LzN1AqTgFZUEqHIVGn_qUA",
      "name": "MOD Administrator",
      "aadObjectId": "ef16aa89-5b26-4a2c-aebb-761b551577c0"
   },
   "conversation": {
      "tenantId": "c9f9aafd-64ac-4f38-8e05-12feba3fb090",
      "id": "19:meeting_NTk4ZDY4ZmYtOWEzZS00OTRkLThhY2EtZmUzZmUzMDQyM2M0@thread.v2",
      "name": "Test meeting"
   },   
   "channelData": {
      "tenant": {
         "id": "c9f9aafd-64ac-4f38-8e05-12feba3fb090"
      },
      "source": {
         "name": "compose"
      },
      "meeting": {
         "id": "MCMxOTptZWV0aW5nX05UazRaRFk0Wm1ZdE9XRXpaUzAwT1RSa0xUaGhZMkV0Wm1VelptVXpNRFF5TTJNMEB0aHJlYWQudjIjMA=="
      }
   },
   "value": {
      "commandId": "Test",
      "commandContext": "compose",
      "requestId": "c46a6b53573f42b5bc801716e5ccc960",
      "context": {
         "theme": "default"
      }
   },
   "name": "composeExtension/fetchTask",
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a>Propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'un canal (new post)

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'un canal (nouveau poste) sont énumérées ci-dessous :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de requête. Il doit être `invoke`. |
|`name`| Type de commande envoyée à votre service. Il doit être `composeExtension/fetchTask`. |
|`from.id`| Identification de l'utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l'utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| Identification de l'objet Azure Active Directory de l'utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.channel.id`| Identification du canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| Identification de l'équipe (si la demande a été faite dans un canal). |
|`channelData.source.name`| Le nom de la source à partir de laquelle le module de tâche est invoqué. |
|`ChannelData.legacy. replyToId`| Obtient ou définit le numéro d'identification du message auquel ce message est une réponse. |
|`value.commandId` | Contient le numéro d'identification de la commande qui a été invoquée. |
|`value.commandContext` | Le contexte qui a déclenché l'événement. Il doit être `compose`. |
|`value.context.theme` | Le thème client de l'utilisateur, utile pour le formatage des vues Web intégrées. Il doit être`default` ,`contrast` , ou`dark`. |

### <a name="example"></a>Exemple

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'un canal (nouveau poste) sont données dans l'exemple suivant :

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a>Propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'un canal ( réponse au fil de discussion)

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'un canal (réponse à un fil discussion) sont les suivantes :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de requête. Il doit être `invoke`. |
|`name`| Type de commande envoyée à votre service. Il doit être `composeExtension/fetchTask`. |
|`from.id`| Identification de l'utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l'utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| Identification de l'objet Azure Active Directory de l'utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.channel.id`| Identification du canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| Identification de l'équipe (si la demande a été faite dans un canal). |
|`channelData.source.name`| Le nom de la source à partir de laquelle le module de tâche est invoqué. |
|`ChannelData.legacy. replyToId`| Obtient ou définit le numéro d'identification du message auquel ce message est une réponse. |
|`value.commandId` | Contient le numéro d'identification de la commande qui a été invoquée. |
|`value.commandContext` | Le contexte qui a déclenché l'événement. Il doit être `compose`. |
|`value.context.theme` | Le thème client de l'utilisateur, utile pour le formatage des vues Web intégrées. Il doit être`default` ,`contrast` ou`dark`. |

### <a name="example"></a>Exemple

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'un canal (réponse à un fil discussion) sont données dans l'exemple suivant :

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a>Propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'une boîte de commande.

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'une boîte de commande sont énumérées ci-dessous :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de requête. Il doit être `invoke`. |
|`name`| Type de commande envoyée à votre service. Il doit être `composeExtension/fetchTask`. |
|`from.id`| Identification de l'utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l'utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| Identification de l'objet Azure Active Directory de l'utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.source.name`| Le nom de la source à partir de laquelle le module de tâche est invoqué. |
|`value.commandId` | Contient le numéro d'identification de la commande qui a été invoquée. |
|`value.commandContext` | Le contexte qui a déclenché l'événement. Il doit être `compose`. |
|`value.context.theme` | Le thème client de l'utilisateur, utile pour le formatage des vues Web intégrées. Il doit être`default` ,`contrast` , ou`dark`. |

### <a name="example"></a>Exemple

Les propriétés de l'activité de la charge utile lorsqu'un module de tâche est invoqué à partir d'une boîte de commande sont données dans l'exemple suivant :

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a>Exemple

La section de code suivante est un exemple de `fetchTask`demande :

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

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

## <a name="initial-invoke-request-from-a-message"></a>Demande initiale d'invocation à partir d'un message

Lorsque votre robot est invoqué à partir d'un message, `value`l'objet de la requête d'invocation initiale doit contenir les détails du message à partir duquel votre extension de message est invoquée. Les tableaux `reactions`et`mentions` sont facultatifs, et ils ne sont pas présents s'il n'y a pas de réactions ou de mentions dans le message original.
La section suivante est un exemple de l'objet `value`:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

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

## <a name="respond-to-the-fetchtask"></a>Répondre à la tache fetchTask

Répondre à la requête invoquée avec un `task`objet qui contient`taskInfo` soit un objet avec la carte adaptative ou l'URL web, soit un simple message de type chaîne.

|Nom de la propriété|Objectif|
|---|---|
|`type`| Peut être `continue` soit pour présenter un formulaire, soit `message` pour une simple fenêtre contextuelle. |
|`value`| Soit un `taskInfo`objet pour un formulaire`string`, soit un pour un message. |

Le schéma de l'objet taskInfo est le suivant :

|Nom de la propriété|Objectif|
|---|---|
|`title`| Le titre du module de tâche.|
|`height`| Il doit être soit un nombre entier (en pixels), ou `small`, `medium`, `large`.|
|`width`| Il doit être soit un nombre entier (en pixels), ou `small`, `medium`, `large`.|
|`card`| La carte adaptative définissant le formulaire (si vous en utilisez une).
|`url`| L'URL à ouvrir à l'intérieur du module de tâches en tant que vue Web intégrée.|
|`fallbackUrl`| Si un client ne prend pas en charge la fonction de module de tâches, cette URL est ouverte dans un onglet du navigateur. |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a>Répondre à la fetchTask avec une carte adaptative

Lorsque vous utilisez une carte adaptative, vous devez répondre par un`task` objet dont l'objet`value` contient une carte adaptative..

#### <a name="example"></a>Exemple

La section de code suivante est un exemple de `fetchTask`réponse avec une carte adaptative :

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Cet échantillon utilise le [paquet NuGet AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) en plus du Bot Framework SDK.

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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
        ]
      }
    }
  }
}
```

* * *

### <a name="create-a-task-module-with-an-embedded-web-view"></a>Créer un module de tâches avec une vue web intégrée

Lorsque vous utilisez une vue Web intégrée, vous devez répondre `task`avec un objet`value` contenant l'URL du formulaire Web que vous souhaitez charger. Les domaines de toutes les URL que vous souhaitez charger doivent être inclus dans le tableau du `validDomains`manifeste de votre application. Pour plus d'informations sur la création de votre vue Web embarquée, consultez la [documentation du module de tâches](~/task-modules-and-cards/what-are-task-modules.md).

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

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

### <a name="request-to-install-your-conversational-bot"></a>Demande d'installation de votre robot conversationnel

Si l'application contient un robot conversationnel, installez le robot dans la conversation, puis chargez le module de tâches. Le robot est utile pour obtenir un contexte supplémentaire pour le module de tâche. Un exemple pour ce scénario est de récupérer la liste des personnes pour alimenter un contrôle de sélection de personnes ou la liste des canaux dans une équipe.

Lorsque l'extension de message reçoit `composeExtension/fetchTask`l'invocation, elle vérifie si le bot est installé dans le contexte actuel pour faciliter le flux. Par exemple, vérifiez le flux avec un appel à la liste d'attente. Si le robot n'est pas installé, il renvoie une carte adaptative avec une action qui demande à l'utilisateur d'installer le robot. L'utilisateur doit avoir l'autorisation d'installer les applications à cet endroit pour les vérifier. Si l'installation de l'application n'aboutit pas, l'utilisateur reçoit un message l'invitant à contacter l'administrateur.

#### <a name="example"></a>Exemple

La section de code suivante est un exemple de la réponse :

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

Après l'installation du robot conversationnel, il reçoit un autre message invoqué avec `name = composeExtension/submitAction`, et `value.data.msteams.justInTimeInstall = true`.

#### <a name="example"></a>Exemple

La section de code suivante est un exemple de la réponse de la tâche à l'invocation :

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

La réponse de la tâche à l'invocation doit être similaire à celle du robot installé.

#### <a name="example"></a>Exemple

La section de code suivante est un exemple d'installation en temps réel d'une application avec une carte adaptative :

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="code-sample"></a>Exemple de code

| Exemple de nom           | Description | .NET    | Node.js   | Python |
|:---------------------|:--------------|:---------|:--------|
|Action d’extension de message Teams| Décrit comment définir des commandes d’action, créer un module de tâche et répondre à l’action d’envoi du module de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
|Recherche d'extension des messages Teams   |  Décrit comment définir les commandes de recherche et répondre aux recherches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Répondre à une commande d'action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

## <a name="see-also"></a>Voir aussi

[Définir les commandes d’action](~/messaging-extensions/how-to/action-commands/define-action-command.md)
