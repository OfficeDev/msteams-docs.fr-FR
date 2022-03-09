---
title: Références API des applications de réunion
author: surbhigupta
description: Identifier les références d’API d’applications de réunion avec des exemples et des exemples de code
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: Requête de signal de notification de contexte utilisateur de l’api de rôle de participant aux réunions teams
ms.openlocfilehash: 3f77e0c1c24ad624fae268d4ca0621f7217ab24a
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398868"
---
# <a name="meeting-apps-api-references"></a>Références API des applications de réunion

L’extensibilité de réunion fournit des API pour améliorer l’expérience de réunion. Vous pouvez effectuer les choses suivantes à l’aide des API répertoriées :

* Créez des applications ou intégrez des applications existantes dans le cycle de vie des réunions.
* Utilisez les API pour rendre votre application sensible à la réunion.
* Sélectionnez les API requises pour améliorer l’expérience de réunion.

Le tableau suivant fournit une liste des API disponibles dans les SDK Microsoft Teams Client (MSTC) et Microsoft Bot Framework (MSBF) :

|Méthode| Description| Source|
|---|---|----|
|[**Obtenir le contexte utilisateur**](#get-user-context-api)| Obtenez des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams’écran.| MSTC SDK|
|[**Obtenir des Participants**](#get-participant-api)| Récupérer les informations des participants par ID de réunion et ID de participant. |MSBF SDK|
|[**Envoyer une notification en réunion**](#send-an-in-meeting-notification)| Fournir des signaux de réunion à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot et permet d’avertir l’action de l’utilisateur qui affiche une notification de réunion. |MSBF SDK|
|[**Obtenir les détails de la réunion**](#get-meeting-details-api)| Obtenir les métadonnées statiques d’une réunion. |MSBF SDK |
|[**Envoyer des légendes en temps réel**](#send-real-time-captions-api)| Envoyer des légendes en temps réel à une réunion en cours. |MSTC SDK|
|[**Partager du contenu d’application pour la phase**](#share-app-content-to-stage-api)| Partagez des parties spécifiques de l’application pour la phase de réunion à partir du volet côté application d’une réunion. |MSTC SDK|
|[**Obtenir l’état de partage de la phase de contenu de l’application**](#get-app-content-stage-sharing-state-api)| Récupérer des informations sur l’état de partage de l’application lors de la phase de réunion. |MSTC SDK|
|[**Obtenir les fonctionnalités de partage de la phase de contenu de l’application**](#get-app-content-stage-sharing-capabilities-api)| Récupérer les fonctionnalités de l’application pour le partage sur la phase de réunion. |MSTC SDK|
|[**Obtenir des événements de réunion Teams en temps réel**](#get-real-time-teams-meeting-events-api)|Récupérer les événements de réunion en temps réel, tels que l’heure réelle de début et de fin.| MSBF SDK|

## <a name="get-user-context-api"></a>API Obtenir le contexte utilisateur

Pour identifier et récupérer des informations contextuelles pour le contenu de votre onglet, voir obtenir le contexte de votre onglet [Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` Est utilisé par un onglet en cours d’exécution dans le contexte de la réunion et est ajouté pour la charge utile de réponse.

## <a name="get-participant-api"></a>Obtenir l’API de participant

> [!NOTE]
>
> * Ne pas mettre en cache les rôles des participants, car l’organisateur de la réunion peut modifier les rôles à tout moment.
> * Actuellement, l’API `GetParticipant` est uniquement prise en charge pour les listes de distribution ou les listes de listes de moins de 350 participants.

### <a name="query-parameters"></a>Paramètres de requête

> [!TIP]
> Obtenez les ID de participant et les ID de client à partir de l’ssO Onglet.

Le tableau suivant inclut les paramètres de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| Chaîne | Oui | L’identificateur de réunion est disponible via Bot Invoke et Teams Client SDK.|
|**participantId**| Chaîne | Oui | L’ID de participant est l’ID utilisateur. Il est disponible dans tabulation SSO, Bot Invoke et Teams Client SDK. Il est recommandé d’obtenir un ID de participant à partir de l’sso tabulation. |
|**tenantId**| String | Oui | L’ID de client est requis pour les utilisateurs du client. Il est disponible dans tabulation SSO, Bot Invoke et Teams Client SDK. Il est recommandé d’obtenir un ID de client à partir de l’sso onglet. |

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

---

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

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant fournit les codes de réponse :

|Code de réponse|Description|
|---|---|
| **403** | Obtenir des informations sur les participants n’est pas partagé avec l’application. Si l’application n’est pas installée dans la réunion, elle déclenche la réponse d’erreur 403. Si l’administrateur client désactive ou bloque l’application pendant la migration du site en direct, il déclenche la réponse d’erreur 403. |
| **200** | Les informations sur les participants sont récupérées avec succès.|
| **401** | L’application répond avec un jeton non valide.|
| **404** | La réunion a expiré ou les participants ne sont pas disponibles.|

## <a name="send-an-in-meeting-notification"></a>Envoyer une notification de réunion

Tous les utilisateurs d’une réunion reçoivent les notifications envoyées par le biais de la charge utile de notification de réunion. La charge utile de notification en réunion déclenche une notification de réunion et vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot. Vous pouvez envoyer une notification de réunion en fonction de l’action de l’utilisateur. La charge utile est disponible via Bot Services.

> [!NOTE]
>
> * Lorsqu’une notification de réunion est invoquée, le contenu est présenté comme un message de conversation.
> * Actuellement, l’envoi de notifications ciblées et la prise en charge de webapp ne sont pas pris en charge.
> * Vous devez appeler la [fonction submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) pour ignorer automatiquement une fois qu’un utilisateur effectue une action dans l’affichage web. Il s’agit d’une condition requise pour la soumission d’application. Pour plus d’informations, [Teams module de tâche du SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true). 
> * Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, la charge utile de la demande d’appel initial `from.id` doit reposer sur les métadonnées `from` de demande dans l’objet, et non sur les `from.aadObjectId` métadonnées de demande. `from.id`est l’ID d’utilisateur `from.aadObjectId` et Microsoft Azure Active Directory (Azure AD) de l’utilisateur. Pour plus d’informations, voir [l’utilisation de modules de tâche dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) [et créer et envoyer le module de tâche](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).
>
### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut les paramètres de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**conversationId**| String | Oui | L’identificateur de conversation est disponible dans le cadre de Bot Invoke. |

### <a name="examples"></a>Exemples

L’objet `Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.

> [!NOTE]
>
> * Le `completionBotId` paramètre est facultatif `externalResourceUrl` dans l’exemple de charge utile demandé.
> * Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels. Pour plus d’informations, voir [les instructions de conception](design/designing-apps-in-meetings.md).
> * L’URL est la page, qui se charge comme dans `<iframe>` la notification de réunion. Le domaine doit se trouver dans le tableau des `validDomains` applications dans le manifeste de votre application.

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

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant inclut les codes de réponse :

|Code de réponse|Description|
|---|---|
| **201** | L’activité avec le signal est envoyée avec succès. |
| **401** | L’application répond avec un jeton non valide. |
| **403** | L’application ne peut pas envoyer le signal. Le code de réponse 403 peut se produire pour diverses raisons, telles que la désactivation et le blocage de l’application par l’administrateur client lors de la migration du site en direct. Dans ce cas, la charge utile contient un message d’erreur détaillé. |
| **404** | La conversation de réunion n’existe pas. |

## <a name="get-meeting-details-api"></a>API Obtenir les détails de la réunion

L’API Détails de la réunion permet à votre application d’obtenir les métadonnées statiques d’une réunion. Les métadonnées fournissent des points de données qui ne changent pas dynamiquement. L’API est disponible via Bot Services. Actuellement, les réunions privées programmées ou périodiques et les réunions de canal programmées ou périodiques supportent les API avec différentes autorisations RSC respectivement.

### <a name="prerequisite"></a>Conditions préalables

Pour utiliser l’API Détails de la réunion, vous devez obtenir différentes autorisations RSC en fonction de l’étendue d’une réunion, telle qu’une réunion privée ou une réunion de canal.

<br>

<details>

<summary><b>Pour la version 1.12 du manifeste de l’application</b></summary>

Utilisez l’exemple suivant pour configurer le manifeste et les propriétés `webApplicationInfo` `authorization` de votre application pour toute réunion privée :

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

Utilisez l’exemple suivant pour configurer le manifeste et les propriétés `webApplicationInfo` `authorization` de votre application pour n’importe quelle réunion de canal :

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

<summary><b>Pour la version 1.11 ou antérieure du manifeste de l’application</b></summary>

Utilisez l’exemple suivant pour configurer la propriété de votre manifeste d’application `webApplicationInfo` pour toute réunion privée :

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

Utilisez l’exemple suivant pour configurer la propriété de votre manifeste d’application pour n’importe `webApplicationInfo` quelle réunion de canal :

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
> Le bot peut recevoir automatiquement des événements de début ou de fin de réunion à partir de toutes les réunions créées `ChannelMeeting.ReadBasic.Group` dans tous les canaux en ajoutant au manifeste pour l’autorisation RSC.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant répertorie le paramètre de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| Chaîne | Oui | L’identificateur de réunion est disponible via Bot Invoke et Teams Client SDK. |

### <a name="example"></a>Exemple

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Non disponible

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

Le corps de la réponse JSON pour l’API Détails de la réunion est le suivant :

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
            "conversationType": "groupchat", 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="send-real-time-captions-api"></a>API Envoyer des légendes en temps réel

L’API d’envoi de légendes en temps réel expose un point de terminaison POST pour les légendes de traduction en temps réel (CART) d’accès aux communications Microsoft Teams, ainsi que des légendes fermées de type humain. Le contenu texte envoyé à ce point de terminaison apparaît aux utilisateurs finaux dans une Microsoft Teams réunion lorsqu’ils ont activé les légendes.

### <a name="cart-url"></a>URL DE PANIER

Vous pouvez obtenir l’URL cart pour le point de terminaison POST à partir de la page **Options** de réunion dans une Microsoft Teams réunion. Pour plus d’informations, voir [les légendes CART dans une Microsoft Teams réunion.](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47) Vous n’avez pas besoin de modifier l’URL cart pour utiliser les légendes CART.

#### <a name="query-parameter"></a>Paramètre de requête

L’URL CART inclut les paramètres de requête suivants :

|Valeur|Type|Requis|Description|
|---|---|----|----|
|**meetingId**| Chaîne | Oui |L’identificateur de réunion est disponible via Bot Invoke et Teams Client SDK. <br/>Par exemple, meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-42411-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**token**| String | Oui |Jeton d’autorisation.<br/> Par exemple, token=04751eac |

#### <a name="example"></a>Exemple

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>Méthode

|Resource|Méthode|Description|
|----|----|----|
|/cartcaption|POST|Gérer les légendes pour la réunion, qui a été démarrée|

> [!NOTE]
> Assurez-vous que le type de contenu pour toutes les demandes est en texte simple avec le codage UTF-8. Le corps de la demande contient uniquement des légendes.

#### <a name="example"></a>Exemple

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> Chaque requête POST génère une nouvelle ligne de légendes. Pour vous assurer que l’utilisateur final dispose de suffisamment de temps pour lire le contenu, limitez chaque corps de requête POST à 80 à 120 caractères.

### <a name="error-codes"></a>Codes d’erreur

Le tableau suivant fournit les codes d’erreur :

|Code d'erreur|Description|
|---|---|
| **400** | Demande non bonne. Le corps de la réponse a plus d’informations. Par exemple, tous les paramètres requis ne sont pas présentés.|
| **401** | Non autorisé. Jeton non bon ou expiré. Si vous recevez cette erreur, générez une nouvelle URL de panier dans Teams. |
| **404** | Réunion in trouvée ou non démarrée. Si vous recevez cette erreur, veillez à démarrer la réunion et à sélectionner les légendes de début. Une fois que les légendes sont activées dans la réunion, vous pouvez commencer à les ajouter à la réunion.|
| **500** |Erreur interne au serveur. Pour plus d’informations, [contactez le support technique ou fournissez des commentaires](../feedback.md).|

## <a name="share-app-content-to-stage-api"></a>Partager du contenu d’application pour l’API de la phase

L’API `shareAppContentToStage` vous permet de partager des parties spécifiques de votre application à la phase de réunion. L’API est disponible via le SDK Teams client.

### <a name="prerequisite"></a>Conditions préalables

Pour utiliser l’API `shareAppContentToStage` , vous devez obtenir les autorisations RSC. Dans le manifeste de l’application, configurez la `authorization` propriété, ainsi que le `name` et `type` dans le `resourceSpecific` champ. Par exemple :

```json
"authorization": {
    "permissions": { 
    "resourceSpecific": [
      { 
      "name": "MeetingStage.Write.Chat",
      "type": "Delegated"
      }
    ]
   }
}
 ```

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut les paramètres de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres, erreur et résultat. *L’erreur* peut contenir une erreur de type *SdkError* ou null lorsque le partage réussit. Le *résultat peut* contenir une valeur true, en cas de réussite d’un partage, ou null en cas d’échec du partage.|
|**appContentURL**| String | Oui | URL qui sera partagée sur l’étape.|

### <a name="example"></a>Exemple

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant fournit les codes de réponse :

|Code de réponse|Description|
|---|---|
| **500** | Erreur interne. |
| **501** | L’API n’est pas prise en charge dans le contexte actuel.|
| **1000** | L’application n’a pas les autorisations adéquates pour autoriser le partage à se mettre en scène.|

## <a name="get-app-content-stage-sharing-state-api"></a>API obtenir l’état de partage de la phase de contenu de l’application

L’API `getAppContentStageSharingState` vous permet d’extraire des informations sur le partage des applications lors de la phase de réunion.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut les paramètres de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| String | Oui | Le rappel contient deux paramètres, erreur et résultat. *L’erreur* peut contenir une erreur de type *SdkError*, en cas d’erreur, ou null lorsque le partage réussit. Le *résultat* peut contenir un `AppContentStageSharingState` objet, indiquant une récupération réussie, ou null, indiquant l’échec de la récupération.|

### <a name="example"></a>Exemple

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

Le corps de la réponse JSON pour l’API `getAppContentStageSharingState` est :

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant fournit les codes de réponse :

|Code de réponse|Description|
|---|---|
| **500** | Erreur interne. |
| **501** | L’API n’est pas prise en charge dans le contexte actuel.|
| **1000** | L’application n’a pas les autorisations adéquates pour autoriser le partage à se mettre en scène.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>API Obtenir les fonctionnalités de partage de la phase de contenu de l’application

L’API `getAppContentStageSharingCapabilities` vous permet d’extraire les fonctionnalités de l’application pour le partage à la phase de réunion.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut les paramètres de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| String | Oui | Le rappel contient deux paramètres, erreur et résultat. *L’erreur* peut contenir une erreur de type *SdkError* ou null lorsque le partage réussit. Le résultat peut contenir un `AppContentStageSharingState` objet, indiquant une récupération réussie, ou null, indiquant l’échec de la récupération.|

### <a name="example"></a>Exemple

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

Le corps de la réponse JSON pour l’API `getAppContentStageSharingCapabilities` est :

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant fournit les codes de réponse :

|Code de réponse|Description|
|---|---|
| **500** | Erreur interne. |
| **1000** | L’application n’est pas autorisée à autoriser le partage à se mettre en scène.|

## <a name="get-real-time-teams-meeting-events-api"></a>API Obtenir des événements de réunion Teams en temps réel

L’utilisateur peut recevoir des événements de réunion en temps réel. Dès qu’une application est associée à une réunion, l’heure de début et de fin de la réunion réelle est partagée avec le bot. Les heures de début et de fin réelles d’une réunion sont différentes des heures de début et de fin prévues. L’API Détails de la réunion fournit l’heure de début et de fin prévues. L’événement fournit l’heure réelle de début et de fin.

### <a name="prerequisite"></a>Conditions préalables

Le manifeste de votre application doit avoir la propriété `webApplicationInfo` pour recevoir les événements de début et de fin de réunion. Utilisez les exemples suivants pour configurer votre manifeste :

<br>

<details>

<summary><b>Pour la version 1.12 du manifeste de l’application</b></summary>

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

<summary><b>Pour la version 1.11 ou antérieure du manifeste de l’application</b></summary>

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

Le bot reçoit l’événement via le `OnEventActivityAsync` handler. Pour désérialiser la charge utile JSON, un objet modèle est introduit pour obtenir les métadonnées d’une réunion. Les métadonnées d’une réunion se trouve dans la propriété `value` dans la charge utile de l’événement. L’objet `MeetingStartEndEventvalue` modèle est créé, dont les variables membres correspondent aux clés sous la `value` propriété dans la charge utile de l’événement.

> [!NOTE]
>
> * Obtenir l’ID de réunion à partir de `turnContext.ChannelData`.
> * N’utilisez pas l’ID de conversation comme ID de réunion.
> * N’utilisez pas l’ID de réunion de la charge utile des événements de réunion `turncontext.activity.value`.

Le code suivant montre comment capturer `MeetingType`les métadonnées d’une réunion qui est , `Title`, `Id`, `JoinUrl`, et `StartTime``EndTime` à partir d’un événement de début/fin de réunion :

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

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Extensibilité des réunions | Microsoft Teams d’extensibilité de réunion pour transmettre des jetons. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Bot de bulles de contenu de réunion | Microsoft Teams exemple d’extensibilité de réunion pour l’interaction avec le bot de bulles de contenu dans une réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| MeetingSidePanel | Microsoft Teams exemple d’extensibilité de réunion pour interagir avec le panneau latéral en réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Onglet Détails de la réunion | Microsoft Teams exemple d’extensibilité de réunion pour l’interaction avec l’onglet Détails en réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|Exemple d’événements de réunion|Exemple d’application pour afficher les événements de Teams en temps réel|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|Exemple de recrutement de réunion|Exemple d’application pour afficher l’expérience de réunion pour le scénario de recrutement.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|Installation de l’application à l’aide du code QR|Exemple d’application qui génère le code QR et installe l’application à l’aide du code QR|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>Voir aussi

* [Teams’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Applications pour les réunions Teams](teams-apps-in-meetings.md)

## <a name="next-steps"></a>Prochaines étapes

> [!div class="nextstepaction"]
> [Activer et configurer vos applications pour Teams réunions](enable-and-configure-your-app-for-teams-meetings.md)
