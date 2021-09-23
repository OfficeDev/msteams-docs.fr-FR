---
title: Conditions préalables et références d’API pour les applications dans les réunions Teams
author: surbhigupta
description: Identifier les conditions préalables avec les applications pour Teams réunions
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: e3392e92965d03c33cd07ae5b65d607d3f86aa5d
ms.sourcegitcommit: d6917d41233a530dc5fd564a67d24731edeb50f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2021
ms.locfileid: "59487479"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Conditions préalables et références d’API pour les applications dans les réunions Teams

Les applications pour Teams réunions, vous pouvez développer les fonctionnalités de vos applications tout au long du cycle de vie des réunions. Avant de travailler avec des applications pour Teams réunions, vous devez remplir les conditions préalables suivantes :

* Savoir comment développer des Teams applications. Pour plus d’informations sur le développement d’Teams’application, voir [Teams développement d’applications.](../overview.md)

* Mettez à jour Teams manifeste de l’application pour indiquer que l’application est disponible pour les réunions. Pour plus d’informations, voir [le manifeste de l’application.](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)

* Utilisez votre application qui prend en charge les onglets configurables dans l’étendue groupchat. Pour plus d’informations, voir [l’étendue de conversation de groupe](../resources/schema/manifest-schema.md#configurabletabs) et créer un onglet de [groupe.](../build-your-first-app/build-channel-tab.md)

* Respectez les recommandations Teams la conception d’onglets pour les scénarios préalables et post-réunion. Pour les expériences pendant les réunions, reportez-vous aux instructions de conception de l’onglet réunion et de la boîte de dialogue en réunion. Pour plus d’informations, [voir Teams recommandations](../tabs/design/tabs.md)en matière de conception d’onglets, [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)de recommandations en matière de conception d’onglets en réunion et de conception de boîte de dialogue en [réunion.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

* Prendre en `groupchat` charge l’étendue pour activer votre application dans les conversations préalables à la réunion et post-réunion. Avec l’expérience d’application de pré-réunion, vous pouvez rechercher et ajouter des applications de réunion et effectuer les tâches préalables à la réunion. Avec l’expérience d’application post-réunion, vous pouvez afficher les résultats de la réunion, tels que les résultats ou les frais d’enquête.
* Les paramètres d’URL de l’API de réunion doivent avoir `meetingId` `userId` , et `tenantId` . Les paramètres sont disponibles dans le cadre de l’activité Teams Client SDK et bot. En outre, vous pouvez récupérer des informations fiables pour l’ID d’utilisateur et l’ID de locataire à l’aide de l’authentification [SSO onglet](../tabs/how-to/authentication/auth-aad-sso.md).

* `GetParticipant`L’API doit avoir un ID et une inscription de bot pour générer des jetons d’th. Pour plus d’informations, voir [l’inscription et l’ID du bot.](../build-your-first-app/build-bot.md)

* Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités d’événements de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue en réunion et dans d’autres étapes du cycle de vie de la réunion. Pour la boîte de dialogue de réunion, voir paramètre `bot Id` d’achèvement dans `NotificationSignal` l’API.

* `Meeting Details`L’API doit avoir un enregistrement de bot et un ID de bot. Il nécessite le SDK bot pour obtenir `TurnContext` .

* Pour les événements de réunion en temps réel, vous devez connaître `TurnContext` l’objet disponible via le Bot SDK. `Activity`L’objet dans contient la charge utile avec `TurnContext` l’heure de début et de fin réelle. Les événements de réunion en temps réel nécessitent un ID de bot inscrit à partir de la Teams web.

Une fois que vous avez passé en compte les conditions préalables, vous pouvez utiliser les références d’API d’applications de réunion , et qui vous permettent d’accéder aux informations à l’aide d’attributs et d’afficher le `GetUserContext` `GetParticipant` contenu `NotificationSignal` `Meeting Details` pertinent.

## <a name="meeting-apps-api-references"></a>Références API des applications de réunion

Les nouvelles extensibilités de réunion suivantes fournissent des API pour transformer l’expérience de réunion :

* Créez des applications ou intégrez des applications existantes dans le cycle de vie des réunions.
* Utilisez les API pour que votre application soit au courant de la réunion.
* Sélectionnez les API que vous souhaitez utiliser pour améliorer l’expérience de réunion.

Le tableau suivant fournit la liste de ces API :

|API|Description|Demande|Source|
|---|---|----|---|
|**GetUserContext**| Cette API vous permet d’obtenir des informations contextuelles pour afficher du contenu pertinent dans Teams onglet. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|Microsoft Teams Client SDK|
|**GetParticipant**| Cette API permet à un bot de récupérer les informations des participants par ID de réunion et ID de participant. |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Cette API vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot. Il vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|
|**Détails de la réunion** | Cette API vous permet d’obtenir des métadonnées de réunion statiques. |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |

Le tableau suivant fournit les méthodes du SDK Bot Framework pour les API :

|API|Méthode du SDK Bot Framework|
|---|---|
|**GetParticipant**| `GetMeetingParticipantAsync (Microsoft.Bot.Builder.ITurnContext turnContext, string meetingId = default, string participantId = default, string tenantId = default, System.Threading.CancellationToken cancellationToken = default);` |
|**NotificationSignal** | `activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<title>&completionBotId=BOT_APP_ID");` |
|**Détails de la réunion** | `TeamsMeetingInfo (string id = default);` |

### <a name="getusercontext-api"></a>GetUserContext API

Pour identifier et récupérer des informations contextuelles pour le contenu de votre onglet, voir obtenir le [contexte de Teams onglet .](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library) est utilisé par un onglet lors de l’exécution dans le contexte de réunion et est `meetingId` ajouté pour la charge utile de réponse.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * Ne pas mettre en cache les rôles des participants, car l’organisateur de la réunion peut modifier les rôles à tout moment.
> * Teams ne prend actuellement pas en charge les grandes listes de distribution ou les tailles de liste de plus de 350 participants pour `GetParticipant` l’API.

L’API permet à un bot de récupérer les informations des participants par ID de réunion et `GetParticipant` ID de participant. L’API inclut des paramètres de requête, des exemples et des codes de réponse. L’API est prise en charge dans les réunions privées programmées ou périodiques et les réunions de canal programmées ou périodiques. 

#### <a name="query-parameters"></a>Paramètres de requête

`GetParticipant`L’API inclut les paramètres de requête suivants :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| Chaîne | Oui | L’identificateur de réunion est disponible via Bot Invoke et Teams Client SDK.|
|**participantId**| Chaîne | Oui | L’ID de participant est l’ID utilisateur. Il est disponible dans tabulation SSO, Bot Invoke et Teams Client SDK. Il est recommandé d’obtenir un ID de participant à partir de l' sso tabulation. |
|**tenantId**| String | Oui | L’ID de client est requis pour les utilisateurs du client. Il est disponible dans tabulation SSO, Bot Invoke et Teams Client SDK. Il est recommandé d’obtenir un ID de client à partir de l' sso onglet. |

#### <a name="example"></a>Exemple

`GetParticipant`L’API inclut les exemples suivants :

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

---

Le corps de la réponse JSON pour `GetParticipant` l’API est :

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
      "isGroup":true
   }
}
```

#### <a name="response-codes"></a>Codes de réponse

`GetParticipant`L’API renvoie les codes de réponse suivants :

|Code de réponse|Description|
|---|---|
| **403** | Obtenir des informations sur les participants n’est pas partagé avec l’application. Si l’application n’est pas installée dans la réunion, elle déclenche la réponse d’erreur 403 la plus courante. Si l’administrateur client désactive ou bloque l’application pendant la migration du site en direct, la réponse d’erreur 403 est déclenchée. |
| **200** | Les informations sur les participants sont récupérées avec succès.|
| **401** | L’application répond avec un jeton non valide.|
| **404** | La réunion a expiré ou le participant est in retrouve.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Tous les utilisateurs d’une réunion reçoivent les notifications envoyées via `NotificationSignal` l’API.

> [!NOTE]
> * Lorsqu’une boîte de dialogue de réunion est invoquée, le contenu est présenté comme un message de conversation.
> * Actuellement, l’envoi de notifications ciblées n’est pas pris en charge.

L’API vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation `NotificationSignal` utilisateur-bot. Cette API vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion. L’API inclut le paramètre de requête, des exemples et des codes de réponse.

#### <a name="query-parameter"></a>Paramètre de requête

`NotificationSignal`L’API inclut le paramètre de requête suivant :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**conversationId**| String | Oui | L’identificateur de conversation est disponible dans le cadre de Bot Invoke. |

#### <a name="examples"></a>Exemples

`Bot ID`L’objet est déclaré dans le manifeste et le bot reçoit un objet de résultat.

> [!NOTE]
> * Le `completionBotId` paramètre est facultatif dans `externalResourceUrl` l’exemple de charge utile demandé. `Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.
> * Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels. Pour vous assurer que les dimensions sont dans les limites autorisées, consultez les [instructions de conception.](design/designing-apps-in-meetings.md)
> * L’URL est la page chargée en tant que dans la boîte de `<iframe>` dialogue de la réunion. Le domaine doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.

`NotificationSignal`L’API inclut les exemples suivants :

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

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

---

#### <a name="response-codes"></a>Codes de réponse

`NotificationSignal`L’API inclut les codes de réponse suivants :

|Code de réponse|Description|
|---|---|
| **201** | L’activité avec le signal est envoyée avec succès. |
| **401** | L’application répond avec un jeton non valide. |
| **403** | L’application ne peut pas envoyer le signal. Le code de réponse 403 peut se produire pour diverses raisons, telles que la désactivation et le blocage de l’application par l’administrateur client lors de la migration de site en direct. Dans ce cas, la charge utile contient un message d’erreur détaillé. |
| **404** | La conversation de réunion n’existe pas. |

### <a name="meeting-details-api"></a>API Détails de la réunion

> [!NOTE]
> Cette fonctionnalité est actuellement disponible en prévisualisation [pour les](../resources/dev-preview/developer-preview-intro.md) développeurs publics uniquement.

`Meeting Details`L’API permet à votre application d’obtenir des métadonnées de réunion statiques. Les métadonnées fournissent des points de données qui ne changent pas dynamiquement.
L’API est disponible via Bot Services.

#### <a name="prerequisite"></a>Conditions préalables

Pour utiliser `Meeting Details` l’API, vous devez obtenir des autorisations RSC. Utilisez l’exemple suivant pour configurer la propriété du manifeste de votre `webApplicationInfo` application :

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
#### <a name="query-parameter"></a>Paramètre de requête

`Meeting Details`L’API inclut le paramètre de requête suivant :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| Chaîne | Oui | L’identificateur de réunion est disponible via Bot Invoke et Teams Client SDK. |

#### <a name="example"></a>Exemple

`Meeting Details`L’API inclut les exemples suivants :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Non disponible

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

Le corps de la réponse JSON pour `Meeting Details` l’API est le suivant :

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="real-time-teams-meeting-events"></a>Événements de réunion Teams en temps réel

> [!NOTE]
> Cette fonctionnalité est actuellement disponible en prévisualisation [pour les](../resources/dev-preview/developer-preview-intro.md) développeurs publics uniquement.

L’utilisateur peut recevoir des événements de réunion en temps réel. Dès qu’une application est associée à une réunion, les heures de début et de fin de réunion réelles sont partagées avec le bot.

Les heures de début et de fin réelles d’une réunion sont différentes des heures de début et de fin prévues. `Meeting Details`L’API fournit l’heure de début et de fin prévues. L’événement fournit l’heure réelle de début et de fin.

### <a name="prerequisite"></a>Conditions préalables

Le manifeste de votre application doit avoir la propriété pour recevoir les événements de `webApplicationInfo` début et de fin de réunion. Utilisez l’exemple suivant pour configurer votre manifeste :

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
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

### <a name="example-of-getting-metadata-of-a-meeting"></a>Exemple d’obtention des métadonnées d’une réunion

Votre bot reçoit l’événement via `OnEventActivityAsync` le handler.

Pour désérialiser la charge utile JSON, un objet modèle est introduit pour obtenir les métadonnées d’une réunion. Les métadonnées d’une réunion se trouve dans la `value` propriété dans la charge utile de l’événement. L’objet modèle est créé, dont les variables membres correspondent aux clés sous `MeetingStartEndEventvalue` la propriété dans la charge utile de `value` l’événement.
     
> [!NOTE]      
> * Obtenir l’ID de réunion à partir `turnContext.ChannelData` de .    
> * N’utilisez pas l’ID de conversation comme ID de réunion.     
> * N’utilisez pas l’ID de réunion de la charge utile des événements de `turncontext.activity.value` réunion. 
      
Le code suivant montre comment capturer les métadonnées d’une réunion qui est , , , , et à partir d’un événement de début `MeetingType` et de fin de réunion `Title` `Id` `JoinUrl` `StartTime` `EndTime` :

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```
* Avoir des paramètres `meetingId` `userId` et dans `tenantId` l’URL de l’API de réunion. Les paramètres sont disponibles dans le cadre de l’activité Teams Client SDK et bot. En outre, vous pouvez récupérer des informations fiables pour l’ID d’utilisateur et l’ID de locataire à l’aide de l’authentification [SSO onglet](../tabs/how-to/authentication/auth-aad-sso.md).

* Avoir un ID et une inscription de bot dans `GetParticipant` l’API pour générer des jetons d’th. Pour plus d’informations, voir [l’inscription et l’ID du bot.](../build-your-first-app/build-bot.md)

* Maintenez votre application à jour en fonction des activités d’événements de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue de réunion et dans d’autres étapes du cycle de vie de la réunion. Pour la boîte de dialogue de réunion, vérifiez le paramètre `bot Id` d’achèvement dans `NotificationSignal` l’API.

* Avoir un enregistrement de bot et un ID de bot dans `MeetingDetails` l’API. Il nécessite le SDK bot pour obtenir `TurnContext` .

* Familiarisez-vous `TurnContext` avec l’objet disponible via le Bot SDK. `Activity`L’objet dans contient la charge utile avec `TurnContext` l’heure de début et de fin réelle. Les événements de réunion en temps réel nécessitent un ID de bot inscrit à partir de la Teams web.

## <a name="see-also"></a>Voir aussi

* [Recommandations en matière de conception de boîte de dialogue en réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams d’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Applications pour Teams réunions](teams-apps-in-meetings.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Références API des applications de réunion](API-references.md)
