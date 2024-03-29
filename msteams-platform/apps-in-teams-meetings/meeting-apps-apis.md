---
title: API des applications de réunion
author: v-sdhakshina
description: Dans cet article, découvrez les références d’API des applications de réunion disponibles pour le client Teams et les SDK Bot Framework avec des exemples, des exemples de code et des codes de réponse.
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: f3d44317dbc8ea317e8fe3c5bdeb19404df75265
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789862"
---
# <a name="meeting-apps-apis"></a>API des applications de réunion

L’extensibilité de réunion fournit des API pour améliorer l’expérience de réunion. Vous pouvez effectuer les opérations suivantes à l’aide des API répertoriées :

* Créez des applications ou intégrez des applications existantes dans le cycle de vie des réunions.
* Utilisez des API pour informer votre application de la réunion.
* Sélectionnez les API requises pour améliorer l’expérience de réunion.

> [!NOTE]
> Utilisez Teams [JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) (*Version* 1.10 et ultérieure) pour que le SSO fonctionne dans le panneau latéral de la réunion.

Le tableau suivant fournit la liste des API disponibles dans la bibliothèque JavaScript microsoft Teams et les kits de développement logiciel (SDK) Microsoft Bot Framework :

|Méthode| Description| Source|
|---|---|----|
|[**Obtenir l’accès avec le contexte utilisateur**](#get-user-context-api)| Obtenez des informations contextuelles pour afficher du contenu pertinent dans un onglet Microsoft Teams.| [Kit de développement logiciel (SDK) de la bibliothèque JavaScript Microsoft Teams](/microsoftteams/platform/tabs/how-to/access-teams-context#get-context-by-using-the-microsoft-teams-javascript-library) |
|[**Obtenir des Participants**](#get-participant-api)| Récupérez les informations du participant par ID de réunion et ID de participant. | [Kit de développement logiciel (SDK) Microsoft Bot Framework](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetingparticipantasync?view=botbuilder-dotnet-stable&preserve-view=true)
|[**Envoyer une notification en réunion**](#send-an-in-meeting-notification)| Fournissez des signaux de réunion à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot et permet de notifier l’action de l’utilisateur qui affiche une notification en réunion. | [Kit de développement logiciel (SDK) Microsoft Bot Framework](/dotnet/api/microsoft.bot.builder.teams.teamsactivityextensions.teamsnotifyuser?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**Obtenir les détails de la réunion**](#get-meeting-details-api)| Obtenez les métadonnées statiques d’une réunion. | [Kit de développement logiciel (SDK) Microsoft Bot Framework](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetinginfoasync?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**Envoyer des légendes en temps réel**](#send-real-time-captions-api)| Envoyez des sous-titres en temps réel à une réunion en cours. | [Kit de développement logiciel (SDK) de la bibliothèque JavaScript Microsoft Teams](/azure/cognitive-services/speech-service/speech-sdk?tabs=nodejs%2Cubuntu%2Cios-xcode%2Cmac-xcode%2Candroid-studio#get-the-speech-sdk&preserve-view=true) |
|[**Partager le contenu de l’application à l’étape**](build-apps-for-teams-meeting-stage.md#share-app-content-to-stage-api)| Partagez des parties spécifiques de l’application à la phase de réunion à partir du panneau côté application dans une réunion. | [Kit de développement logiciel (SDK) de la bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting) |
|[**Obtenir des événements de réunion Teams en temps réel**](#get-real-time-teams-meeting-events-api)|Récupérez les événements de réunion en temps réel, tels que l’heure de début et de fin réelle.| [Kit de développement logiciel (SDK) Microsoft Bot Framework](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingstartasync?view=botbuilder-dotnet-stable&preserve-view=true) |
| [**Obtenir l’état audio entrant**](#get-incoming-audio-state) | Permet à une application d’obtenir le paramètre d’état audio entrant pour l’utilisateur de la réunion.| [Kit de développement logiciel (SDK) de la bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |
| [**Activer/désactiver l’audio entrant**](#toggle-incoming-audio) | Permet à une application de basculer le paramètre d’état audio entrant pour l’utilisateur de la réunion du son muet à l’activation ou inversement.| [Kit de développement logiciel (SDK) de la bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |

## <a name="get-user-context-api"></a>Obtenir l’API de contexte utilisateur

Pour identifier et récupérer des informations contextuelles pour le contenu de votre onglet, consultez [obtenir le contexte de votre onglet Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` Est utilisé par un onglet en cours d’exécution dans le contexte de la réunion et ajouté pour la charge utile de réponse.

## <a name="get-participant-api"></a>Obtenir l’API du participant

L’API `GetParticipant` doit disposer d’une inscription et d’un ID de bot pour générer des jetons d’authentification. Pour plus d’informations, consultez [l’inscription et l’ID du bot](../build-your-first-app/build-bot.md).

> [!NOTE]
>
> * Le type d’utilisateur n’est pas inclus dans l’API **getParticipantRole** .
> * Ne mettez pas en cache les rôles de participant, car l’organisateur de la réunion peut modifier les rôles à tout moment.
> * Actuellement, l’API `GetParticipant` est uniquement prise en charge pour les listes de distribution ou les listes de moins de 350 participants.

### <a name="query-parameters"></a>Paramètres de requête

> [!TIP]
> Obtenez les ID de participant et les ID de locataire à partir de [l’authentification SSO de l’onglet](../tabs/how-to/authentication/tab-sso-overview.md).

L’API `Meeting` doit avoir `meetingId`, `participantId`et `tenantId` en tant que paramètres d’URL. Les paramètres sont disponibles dans le cadre du kit de développement logiciel (SDK) client Teams et de l’activité du bot.

Le tableau ci-dessous décrit chaque paramètre de chaîne de requête.

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| Chaîne | Oui | L’identificateur de réunion est disponible via Bot Invoke et Teams SDK client.|
|**participantId**| Chaîne | Oui | L’ID du participant est l’ID d’utilisateur. Il est disponible dans Tab SSO, Bot Invoke et Teams Client SDK. Il est recommandé d’obtenir un ID de participant à partir de l’authentification unique Tab. |
|**tenantId**| String | Oui | L’ID de locataire est requis pour les utilisateurs du locataire. Il est disponible dans Tab SSO, Bot Invoke et Teams Client SDK. Il est recommandé d’obtenir un ID de locataire à partir de l’authentification unique Tab. |

### <a name="example"></a>Exemple

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = await TeamsInfo.GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourParticipantTenantId").ConfigureAwait(false);
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "conversationType": "groupChat", 
      "isGroup":true
   }
}
```

---

| Nom de la propriété | Description |
|---|---|
| **user.id** | ID de l’utilisateur. |
| **user.aadObjectId** | ID d’objet Azure Active Directory de l’utilisateur. |
| **user.name** | Nom de l'utilisateur. |
| **user.givenName** | Prénom de l’utilisateur.|
| **user.surname** | Nom de l’utilisateur. |
| **user.email** | ID de messagerie de l’utilisateur. |
| **user.userPrincipalName** | UPN de l’utilisateur. |
| **user.tenantId** | ID du client Azure Active Directory. |
| **user.userRole** | Rôle de l’utilisateur. Par exemple, « admin » ou « user ». |
| **meeting.role** | Rôle du participant dans la réunion. Par exemple, « Organisateur », « Présentateur » ou « Participant ». |
| **meeting.inMeeting** | Valeur indiquant si le participant est dans la réunion. |
| **conversation.id** | ID de conversation de réunion. |
| **conversation.isGroup** | Boolean indiquant si la conversation a plus de deux participants. |

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant présente les codes de réponse :

|Code de réponse|Description|
|---|---|
| **403** | Les informations sur les participants ne sont pas partagées avec l'application. Si l’application n’est pas installée dans la réunion, elle déclenche la réponse d’erreur 403. Si l’administrateur locataire désactive ou bloque l’application pendant la migration de site en direct, il déclenche la réponse d’erreur 403. |
| **200** | Les informations du participant sont récupérées avec succès.|
| **401** | L’application répond avec un jeton non valide.|
| **404** | La réunion a expiré ou les participants ne sont pas disponibles.|

## <a name="send-an-in-meeting-notification"></a>Envoyer une notification en réunion

Tous les utilisateurs d’une réunion reçoivent les notifications envoyées par le biais de la charge utile de notification en réunion. La charge utile de notification en réunion déclenche une notification en réunion et vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot. Vous pouvez envoyer une notification en réunion en fonction de l’action de l’utilisateur. La charge utile est disponible via Bot Services.

> [!NOTE]
>
> * Lorsqu’une notification en réunion est appelée, le contenu est présenté sous la forme d’un message de conversation.
> * Actuellement, l’envoi de notifications ciblées et la prise en charge de webapp ne sont pas pris en charge.
> * Vous devez appeler la fonction [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) pour ignorer automatiquement une fois qu’un utilisateur a fait une action dans la vue web. Il s'agit d'une exigence pour la soumission d'une application. Pour plus d'informations, consultez [Module de tâches du SDK Teams](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
> * Si vous souhaitez que votre application prenne en charge les utilisateurs anonymes, la charge utile de la demande d’appel initial doit s’appuyer sur les métadonnées de la demande dans `from.id` l’objet, `from`et non sur `from.aadObjectId` les métadonnées de la demande. `from.id`est l’ID d’utilisateur et `from.aadObjectId` est l’ID Microsoft Azure Active Directory (Azure AD) de l’utilisateur. Pour plus d’informations, consultez [l’utilisation de modules de tâches dans des onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) et [créez et envoyez le module de tâche](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut le paramètre de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**conversationId**| String | Oui | L’identificateur de conversation est disponible dans le cadre de Bot Invoke. |

### <a name="examples"></a>Exemples

L’objet `Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.

> [!NOTE]
>
> * Le `completionBotId` paramètre est `externalResourceUrl` facultatif dans l’exemple de charge utile demandée.
> * Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels. Pour plus d'informations, consultez [Directives de conception Teams](design/designing-apps-in-meetings.md).
> * L’URL est la page, qui se charge comme `<iframe>` dans la notification en réunion. Le domaine doit se trouver dans le tableau des `validDomains`apps de votre manifeste d'application.

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID");
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

# <a name="json"></a>[JSON](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities
```

```json

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&<completionBotId>=<BOT_APP_ID>"
        }
    },
    "replyToId": "1493070356924"
}
```

---

| Nom de la propriété | Description |
|---|---|
| **type** | Type d’activité. |
| **text** | Contenu texte du message. |
| **summary** | Texte récapitulative du message. |
| **channelData.notification.alertInMeeting** | Boolean indiquant si une notification doit être affichée à l’utilisateur lors d’une réunion. |
| **channelData.notification.externalResourceUrl** | Valeur de l’URL de ressource externe de la notification.|
| **replyToId** | ID du message parent ou racine du thread. |
| **APP_ID** | ID d’application déclaré dans le manifeste. |
| **completionBotId** | ID de l’application bot |

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant inclut les codes de réponse :

|Code de réponse|Description|
|---|---|
| **201** | L’activité avec le signal est envoyée avec succès. |
| **401** | L’application répond avec un jeton non valide. |
| **403** | L’application ne peut pas envoyer le signal. Le code de réponse 403 peut se produire pour différentes raisons, telles que la désactivation et le blocage de l’application par l’administrateur client lors de la migration de site en direct. Dans ce cas, la charge utile contient un message d’erreur détaillé. |
| **404** | La conversation de réunion n’existe pas. |

## <a name="get-meeting-details-api"></a>Obtenir l’API détails de la réunion

L’API Détails de la réunion permet à votre application d’obtenir les métadonnées statiques d’une réunion. Les métadonnées fournissent des points de données qui ne changent pas dynamiquement. L’API est disponible via Bot Services. Actuellement, les réunions privées planifiées ou périodiques et les réunions planifiées par canal ou périodiques prennent respectivement en charge l’API avec des autorisations RSC différentes.

L’API `Meeting Details` doit disposer d’une inscription de bot et d’un ID de bot. Il nécessite le Kit de développement logiciel (SDK) bot pour obtenir `TurnContext`. Pour utiliser l’API Détails de la réunion, vous devez obtenir différentes autorisations RSC en fonction de l’étendue de toute réunion, telle qu’une réunion privée ou une réunion de canal.

### <a name="prerequisite"></a>Conditions préalables

Pour utiliser l’API Détails de la réunion, vous devez obtenir différentes autorisations RSC en fonction de l’étendue de toute réunion, telle qu’une réunion privée ou une réunion de canal.

<br>

<details>

<summary><b>Pour le manifeste d’application version 1.12 et ultérieure</b></summary>

Utilisez l’exemple suivant pour configurer les propriétés et `authorization` le manifeste de `webApplicationInfo` votre application pour toute réunion privée :

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]
    }
}
 ```

Utilisez l’exemple suivant pour configurer les propriétés et `authorization` le manifeste de `webApplicationInfo` votre application pour n’importe quelle réunion de canal :

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChannelMeeting.ReadBasic.Group",
                "type": "Application"
            }
        ]
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>Pour le manifeste d’application version 1.11 et antérieure</b></summary>

Utilisez l’exemple suivant pour configurer la propriété du manifeste de `webApplicationInfo` votre application pour toute réunion privée :

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

Utilisez l’exemple suivant pour configurer la propriété de votre manifeste d’application `webApplicationInfo` pour toute réunion de canal :

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "ChannelMeeting.ReadBasic.Group"
    ]
}
 ```

<br>

</details>

> [!NOTE]
>
> * Le bot peut recevoir automatiquement des événements de début ou de fin de réunion à partir de toutes les réunions créées dans tous les canaux en ajoutant `ChannelMeeting.ReadBasic.Group` au manifeste pour l’autorisation RSC.
> * Pour un appel `organizer` en tête-à-tête est l’initiateur de la conversation et pour les appels `organizer` de groupe est l’initiateur d’appel. Pour les réunions `organizer` de canal public est la personne qui a créé le billet de canal.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant répertorie quelques exemples où le paramètre de requête  est utilisé.

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| Chaîne | Oui | L’identificateur de réunion est disponible via Bot Invoke et Teams SDK client. |

### <a name="example"></a>Exemple

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript

Not available

```

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

Le corps de la réponse JSON pour l’API Détails de la réunion est le suivant :

* **Réunions planifiées :**

    ```json

    {
       "details":  { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "Scheduled" 
         },
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
             }, 
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    } 
    ```

* **Réunions de canal planifiées :**

    ```json
    { 
        "details": { 
        "msGraphResourceId": "MSoxNmUwYjdiYi05M2Q1LTQzNTItOTllMC0yM2VlNWYyZmZmZTIqMTY2MDc1ODYwNzc0MCoqMTk6a0RtQkpEWFZsYWl0QWhHcVB2SzBtRExZbHVTWnJub01WX1MxeFNkTjQxNDFAdGhyZWFkLnRhY3Yy", 
        "scheduledStartTime": "2022-08-17T18:00:00Z", 
        "scheduledEndTime": "2022-08-17T18:30:00Z", 
        "type": "ChannelScheduled", 
        "id": "MCMxOTprRG1CSkRYVmxhaXRBaEdxUHZLMG1ETFlsdVNacm5vTVZfUzF4U2RONDE0MUB0aHJlYWQudGFjdjIjMTY2MDc1ODYwNzc0MA==", 
        "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3akDmBJDXVlaitAhGqPvK0mDLYluSZrnoMV_S1xSdN4141%40thread.tacv2/1660758607740?context=%7b%22Tid%22%3a%229f044231-b634-4bdd-b29d-2776e3dbd699%22%2c%22Oid%22%3a%2216e0b7bb-93d5-4352-99e0-23ee5f2fffe2%22%7d", 
        "title": "Test channel meeting"
    }, 
    "conversation": { 
        "isGroup": true, 
        "conversationType": "channel", 
        "id": "19:kDmBJDXVlaitAhGqPvK0mDLYluSZrnoMV_S1xSdN4141@thread.tacv2;messageid=1660758607740"
    }, 
    "organizer": { 
        "tenantId": "9f044231-b634-4bdd-b29d-2776e3dbd699", 
        "objectId": "16e0b7bb-93d5-4352-99e0-23ee5f2fffe2", 
        "id": "29:1q4D6ekLXEAALkrqyLXUIcwtVSdXx31bf6vMdfahmkTb9euYVYSsN9x4133pXLV_I2idpVriFe40e19XEZt57bQ", 
        "aadObjectId": "16e0b7bb-93d5-4352-99e0-23ee5f2fffe2"
    }
    }
    ```

* **Appels en tête-à-tête :**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "OneToOneCall"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer  ": {
             "id": "<organizer user ID>",
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **Appels de groupe :**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "GroupCall",
             "joinUrl": "https://teams.microsoft.com/l/xx"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer": {
             "id": "<organizer user ID>",
             "objectId": "<organizer object ID>",
             "aadObjectId": "<AAD object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **Réunions instantanées :**

    ```json
    { 
       "details": { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "MeetNow" 
         }, 
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
         },
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>", 
             "tenantId": "<Tenant ID>" ,
             "objectId": "<organizer object ID>"
         }
    }
    
    ```

---

| Nom de la propriété | Description |
|---|---|
| **details.id** | ID de la réunion, encodé en tant que chaîne BASE64. |
| **details.msGraphResourceId** | MsGraphResourceId, utilisé spécifiquement pour les appels ms API Graph. |
| **details.scheduledStartTime** | Heure de début planifiée de la réunion, au format UTC. |
| **details.scheduledEndTime** | Heure de fin planifiée de la réunion, au format UTC. |
| **details.joinUrl** | URL utilisée pour rejoindre la réunion. |
| **details.title** | Titre de la réunion. |
| **details.type** | Type de réunion (OneToOneCall, GroupCall, Scheduled, Recurring, MeetNow, ChannelScheduled et ChannelRecurring). |
| **conversation.isGroup** | Boolean indiquant si la conversation a plus de deux participants. |
| **conversation.conversationType** | Type de conversation. |
| **conversation.id** | ID de conversation de réunion. |
| **organizer.id** | ID d’utilisateur de l’organisateur. |
| **organizer.aadObjectId** | ID d’objet Azure Active Directory de l’organisateur. |
| **organizer.tenantId** | ID de locataire Azure Active Directory de l’organisateur. |

En cas de type de réunion périodique,

**startDate** : spécifie la date de début de l’application du modèle. La valeur de startDate doit correspondre à la valeur de date de la propriété start sur la ressource d’événement. Notez que la première occurrence de la réunion peut ne pas se produire à cette date si elle ne correspond pas au modèle.

**endDate** : spécifie la date d’arrêt de l’application du modèle. Notez que la dernière occurrence de la réunion peut ne pas se produire à cette date si elle ne correspond pas au modèle.

## <a name="send-real-time-captions-api"></a>API Envoyer des légendes en temps réel

L’API d’envoi de sous-titres en temps réel expose un point de terminaison POST pour les sous-titres de traduction en temps réel (CART) d’accès aux communications Teams, les sous-titres de type humain. Le contenu textuel envoyé à ce point de terminaison apparaît aux utilisateurs finaux dans une réunion Teams quand les sous-titres sont activés.

### <a name="cart-url"></a>URL CART

Vous pouvez obtenir l’URL CART du point de terminaison POST à partir de la page **Options de réunion** d’une réunion Teams. Pour plus d’informations, consultez [les légendes CART dans une réunion Microsoft Teams](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47). Vous n’avez pas besoin de modifier l’URL CART pour utiliser des légendes CART.

#### <a name="query-parameter"></a>Paramètre de requête

L’URL CART inclut les paramètres de requête suivants :

|Valeur|Type|Requis|Description|
|---|---|----|----|
|**meetingId**| Chaîne | Oui |L’identificateur de réunion est disponible via Bot Invoke et Teams SDK client. <br/>Par exemple, meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**Jeton**| Chaîne | Oui |Jeton d’autorisation<br/> Par exemple, token=04751eac |

#### <a name="example"></a>Exemple

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>Méthode

|Ressource|Méthode|Description|
|----|----|----|
|/cartcaption|POST|Gérer les légendes pour la réunion, qui a été démarrée|

> [!NOTE]
> Vérifiez que le type de contenu pour toutes les demandes est du texte brut avec encodage UTF-8. Le corps de la requête contient uniquement des légendes.

#### <a name="example"></a>Exemple

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!NOTE]  
> Chaque requête POST génère une nouvelle ligne de légendes. Pour vous assurer que l’utilisateur final dispose de suffisamment de temps pour lire le contenu, limitez chaque corps de requête POST à 80 à 120 caractères.

### <a name="error-codes"></a>Codes d’erreur

Le tableau suivant décrit les codes d'erreur.

|Code d'erreur|Description|
|---|---|
| **400** | Demande incorrecte Le corps de la réponse contient plus d’informations. Par exemple, tous les paramètres requis ne sont pas présentés.|
| **401** | Non autorisé Jeton incorrect ou expiré Si vous recevez cette erreur, générez une nouvelle URL CART dans Teams. |
| **404** | Réunion introuvable ou non démarrée Si vous recevez cette erreur, veillez à démarrer la réunion et à sélectionner les légendes de début. Une fois les légendes activées dans la réunion, vous pouvez commencer à ajouter des sous-titres à la réunion.|
| **500** |Erreur interne au serveur. Pour plus d’informations, [contactez le support technique ou fournissez des commentaires](../feedback.md).|

## <a name="get-real-time-teams-meeting-events-api"></a>Obtenir l’API d’événements de réunion Teams en temps réel

> [!NOTE]
> Les événements de réunion Teams en temps réel sont pris en charge uniquement pour les réunions planifiées.

L’utilisateur peut recevoir des événements de réunion en temps réel. Dès qu’une application est associée à une réunion, l’heure de début et de fin de la réunion réelle est partagée avec le bot. L’heure de début et de fin réelle d’une réunion est différente de l’heure de début et de fin planifiée. L’API Détails de la réunion fournit l’heure de début et de fin planifiée. L’événement fournit l’heure de début et de fin réelle.

Vous devez connaître l’objet `TurnContext` disponible via le Kit de développement logiciel (SDK) Bot. L’objet `Activity` dans `TurnContext` contient la charge utile avec l’heure de début et de fin réelle. Les événements de réunion en temps réel nécessitent un ID de bot inscrit à partir de la plateforme Teams. Le bot peut recevoir automatiquement l’événement de début ou de fin de la réunion en l’ajoutant `ChannelMeeting.ReadBasic.Group` dans le manifeste.

### <a name="prerequisite"></a>Conditions préalables

Le manifeste de votre application doit avoir la `webApplicationInfo` propriété pour recevoir les événements de début et de fin de la réunion. Utilisez les exemples suivants pour configurer votre manifeste :

<br>

<details>

<summary><b>Pour le manifeste d’application version 1.12 et ultérieure</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]    
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>Pour le manifeste d’application version 1.11 et antérieure</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

<br>

</details>

### <a name="example-of-getting-meetingstartendeventvalue"></a>Exemple d’obtention `MeetingStartEndEventvalue`

Le bot reçoit l’événement par le biais du `OnEventActivityAsync` gestionnaire. Pour désérialiser la charge utile JSON, un objet de modèle est introduit pour obtenir les métadonnées d’une réunion. Les métadonnées d’une réunion se trouve dans la `value` propriété dans la charge utile de l’événement. L’objet `MeetingStartEndEventvalue` modèle est créé, dont les variables membres correspondent aux clés sous la `value` propriété dans la charge utile de l’événement.

> [!NOTE]
>
> * Obtenir l’ID de réunion à partir de `turnContext.ChannelData`
> * N’utilisez pas l’ID de conversation comme ID de réunion.
> * N’utilisez pas l’ID de réunion à partir de la charge utile `turncontext.activity.value`des événements de réunion.

Le code suivant montre comment capturer les métadonnées d’une réunion qui est `MeetingType`, `Title`, `Id``JoinUrl`, `StartTime`et `EndTime` à partir d’un événement de début/fin de réunion :

Événement de début de réunion

```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingStartEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

Événement de fin de réunion

```csharp
protected override async Task OnTeamsMeetingEndAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

### <a name="example-of-meeting-start-event-payload"></a>Exemple de charge utile d’événement de début de réunion

Le code suivant fournit un exemple de charge utile d’événement de début de réunion :

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id": "meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a>Exemple de charge utile d’événement de fin de réunion

Le code suivant fournit un exemple de charge utile d’événement de fin de réunion :

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

| Nom de la propriété | Description |
|---|---|
| **name** | Nom de l'utilisateur.|
| **type** | Type d’activité. |
| **timestamp** | Date et heure locales du message, exprimées au format ISO-8601. |
| **id** | ID de l’activité. |
| **channelId** | Canal à lequel cette activité est associée. |
| **serviceUrl** | URL du service où les réponses à cette activité doivent être envoyées. |
| **from.id** | Identification de l'utilisateur qui a envoyé la demande. |
| **from.aadObjectId** | Identification de l'objet Azure Active Directory de l'utilisateur qui a envoyé la demande. |
| **conversation.isGroup** | Boolean indiquant si la conversation a plus de deux participants. |
| **conversation.tenantId** | ID de locataire Azure Active Directory de la conversation ou de la réunion. |
| **conversation.id** | ID de conversation de réunion. |
| **recipient.id** | ID de l’utilisateur qui reçoit la demande. |
| **recipient.name** | Nom de l’utilisateur qui reçoit la demande. |
| **entities.locale** | entité qui contient des métadonnées sur les paramètres régionaux. |
| **entities.country** | entité qui contient des métadonnées sur le pays. |
| **entities.type** | entité qui contient des métadonnées sur le client. |
| **channelData.tenant.id** | ID du client Azure Active Directory. |
| **channelData.source** | Nom source à partir duquel l’événement est déclenché ou appelé. |
| **channelData.meeting.id** | ID par défaut associé à la réunion. |
| **Valeur. MeetingType** | Type de réunion. |
| **Valeur. Titre** | Objet de la réunion. |
| **Valeur. Id** | ID par défaut associé à la réunion. |
| **Valeur. JoinUrl** | URL de participation de la réunion. |
| **Valeur. Starttime** | Heure de début de la réunion au format UTC. |
| **Valeur. Heure de fin** | Heure de fin de la réunion au format UTC. |
| **locale**| Paramètres régionaux du message définis par le client. |

## <a name="get-incoming-audio-state"></a>Obtenir l’état audio entrant

L’API `getIncomingClientAudioState` permet à une application d’obtenir le paramètre d’état audio entrant pour l’utilisateur de la réunion. L’API est disponible via le SDK client Teams.

> [!NOTE]
>
> * L’API `getIncomingClientAudioState` pour mobile est actuellement disponible dans [la préversion publique pour les développeurs](../resources/dev-preview/developer-preview-intro.md).
> * Le consentement spécifique à la ressource est disponible pour la version de manifeste 1.12 et les versions ultérieures. Par conséquent, cette API ne fonctionne pas pour le manifeste version 1.11 et les versions antérieures.

### <a name="manifest"></a>Manifeste

```JSON
"authorization": {
    "permissions": {
      "resourceSpecific": [
        {
          "name": "OnlineMeetingParticipant.ToggleIncomingAudio.Chat",
          "type": "Delegated"
        }
      ]
    }
  }
```
  
### <a name="example"></a>Exemple

```javascript
callback = (errcode, result) => {
        if (errcode) {
            // Handle error code
        }
        else {
            // Handle success code
        }
    }

microsoftTeams.meeting.getIncomingClientAudioState(this.callback)
```

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut le paramètre de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres `error` et `result`. *L’erreur* peut contenir un type `SdkError` d’erreur ou `null` lorsque l’extraction audio réussit. Le *résultat* peut contenir la valeur true ou false lorsque l’extraction audio réussit ou null en cas d’échec de l’extraction audio. L’audio entrant est désactivé si le résultat est true et désactivé si le résultat est false. |
  
### <a name="response-codes"></a>Codes de réponse

Le tableau suivant présente les codes de réponse :

|Code de réponse|Description|
|---|---|
| **500** | Erreur interne. |
| **501** | L’API n’est pas prise en charge dans le contexte actuel.|
| **1 000** | L’application ne dispose pas des autorisations appropriées pour autoriser le partage à mettre en scène.|

## <a name="toggle-incoming-audio"></a>Activer/désactiver l’audio entrant

L’API `toggleIncomingClientAudio` permet à une application de basculer le paramètre d’état audio entrant pour l’utilisateur de la réunion du son muet à l’activation ou inversement. L’API est disponible via le SDK client Teams.

> [!NOTE]
>
> * L’API `toggleIncomingClientAudio` pour mobile est actuellement disponible dans [la préversion publique pour les développeurs](../resources/dev-preview/developer-preview-intro.md).
> * Le consentement spécifique à la ressource est disponible pour la version de manifeste 1.12 et les versions ultérieures. Par conséquent, cette API ne fonctionne pas pour le manifeste version 1.11 et les versions antérieures.

### <a name="manifest"></a>Manifeste

```JSON
"authorization": {
 "permissions": {
  "resourceSpecific": [
   {
    "name": "OnlineMeetingParticipant.ToggleIncomingAudio.Chat",
    "type": "Delegated"
   }
  ]
 }
}
```

### <a name="example"></a>Exemple

```javascript
callback = (error, result) => {
        if (error) {
            // Handle error code
        }
        else {
            // Handle success code
        }
    }

microsoftTeams.meeting.toggleIncomingClientAudio(this.callback)
```
  
### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut le paramètre de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres `error` et `result`. *L’erreur* peut contenir un type `SdkError` d’erreur ou `null` lorsque le bouton bascule réussit. Le *résultat* peut contenir une valeur true ou false, lorsque le bouton bascule réussit ou null en cas d’échec du bouton bascule. L’audio entrant est désactivé si le résultat est true et désactivé si le résultat est false.
  
### <a name="response-code"></a>Code de réponse

Le tableau suivant présente les codes de réponse :

|Code de réponse|Description|
|---|---|
| **500** | Erreur interne. |
| **501** | L’API n’est pas prise en charge dans le contexte actuel.|
| **1 000** | L’application ne dispose pas des autorisations appropriées pour autoriser le partage à mettre en scène.|

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Extensibilité des réunions | Exemple d’extensibilité de réunion Teams pour le passage de jetons. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Bot de bulles de contenu de réunion | Exemple d’extensibilité de réunion Teams pour interagir avec le bot de bulles de contenu dans une réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Panneau latéral de la réunion | Exemple d’extensibilité de réunion Teams pour interagir avec le panneau latéral en réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Onglet Détails de la réunion | Exemple d’extensibilité de réunion Teams pour interagir avec l’onglet Détails dans la réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
| Exemple d’événements de réunion | Exemple d’application pour afficher des événements de réunion Teams en temps réel|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
| Exemple de recrutement de réunions |Exemple d’application pour afficher l’expérience de réunion pour le scénario de recrutement|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
| Installation de l’application à l’aide du code QR |Exemple d’application qui génère le code QR et installe l’application à l’aide du code QR|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>Voir aussi

* [Flux d’authentification Teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Applications pour les réunions Teams](teams-apps-in-meetings.md)
* [FAQ sur le Kit de développement logiciel (SDK) de Live Share](teams-live-share-overview.md)
* [Enregistrement de réunion cloud Teams](/microsoftteams/cloud-recording)

## <a name="next-steps"></a>Prochaines étapes

[Onglets générer pour la réunion](build-tabs-for-meeting.md)
