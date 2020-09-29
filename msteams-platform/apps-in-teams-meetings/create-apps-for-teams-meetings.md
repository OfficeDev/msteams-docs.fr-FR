---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions teams
ms.topic: conceptual
ms.author: lajanuar
keywords: applications Team Apps Meeting User Role Role API
ms.openlocfilehash: a489a2a439c8aaacc2900e4c62084f13b34b3e30
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279675"
---
# <a name="create-apps-for-teams-meetings-preview"></a>Créer des applications pour les réunions Teams (aperçu)

>[!IMPORTANT]
> Les fonctionnalités incluses dans l’aperçu de Microsoft teams sont fournies à des fins d’accès anticipé, de test et de commentaires uniquement. Ils peuvent être soumis à des modifications avant de devenir disponibles dans la publication publique et ne doivent pas être utilisés dans les applications de production.

## <a name="prerequisites-and-considerations"></a>Conditions préalables et considérations

1. Les applications dans les réunions nécessitent des connaissances de base sur le [développement d’applications teams](../overview.md). Une application dans une réunion peut comprendre des fonctionnalités d' [onglets](../tabs/what-are-tabs.md), de [robots](../bots/what-are-bots.md)et d' [extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md) , et nécessitera des mises à jour du manifeste d' [application](#update-your-app-manifest) teams pour indiquer que l’application est disponible pour les réunions.

1. Pour que votre application fonctionne dans le cycle de vie de la réunion sous la forme d’un onglet, elle doit prendre en charge les onglets configurables dans l' [étendue groupchat](../resources/schema/manifest-schema.md#configurabletabs). *Voir* [étendre votre application teams avec un onglet personnalisé](../tabs/how-to/add-tab.md). La prise en charge de l' `groupchat` étendue activera votre application dans les conversations [pré-réunion](teams-apps-in-meetings.md#pre-meeting-app-experience) et [post-réunion](teams-apps-in-meetings.md#post-meeting-app-experience) .

1. Les paramètres de l’URL de l’API de réunion peuvent exiger `meetingId` , `userId` et les [tenantId](/onedrive/find-your-office-365-tenant-id) disponibles dans le cadre du kit de développement logiciel client teams et de l’activité du robot. En outre, des informations fiables pour l’ID d’utilisateur et l’ID de client peuvent être récupérées à l’aide de [l’authentification SSO de tabulation](../tabs/how-to/authentication/auth-aad-sso.md).

1. Certaines API de réunion, telles que `GetParticipant` nécessiteront un [ID d’enregistrement et d’application bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) pour générer des jetons d’authentification.

1. Les développeurs doivent respecter [les conseils généraux de conception des onglets teams](../tabs/design/tabs.md) pour les scénarios pré-et post-réunion, ainsi que pendant les réunions (consultez les instructions [de la boîte de dialogue](../apps-in-teams-meetings/design/designing-in-meeting-dialog.md) et les [onglets de conception des onglets dans](../apps-in-teams-meetings/design/designing-in-meeting-tab.md) les réunions).

## <a name="meeting-apps-api-reference"></a>Référence de l’API des applications de réunion

|API|Description|Demande|Source|
|---|---|----|---|
|**GetUserContext**| Obtenir des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams. |_**microsoftTeams. getContext (() => {/*...* / } )**_|Kit de développement logiciel client Microsoft teams|
|**GetParticipant**|Cette API permet à un bot d’extraire des informations sur les participants par ID de réunion et ID de participant.|**Obtenir** _ **/v1/meetings/{meetingId}/participants/{participantId} ? tenantId = {tenantId}**_ |Kit de développement logiciel (SDK) Microsoft bot Framework|
|**NotificationSignal** |Les signaux de réunion seront remis à l’aide de l’API de notification de conversation existante suivante (pour la conversation utilisateur-bot). Cette API permet aux développeurs de signaler en fonction de l’action de l’utilisateur final à afficher-case une bulle de dialogue de réunion.|**Post** _ **/v3/conversations/{conversationId}/Activities**_|Kit de développement logiciel (SDK) Microsoft bot Framework|

### <a name="getusercontext"></a>GetUserContext

Pour obtenir des instructions sur l’identification et la récupération des informations contextuelles pour votre contenu d’onglet, consultez notre [contexte de l’onglet teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) . Dans le cadre de l’extensibilité des réunions, une nouvelle valeur a été ajoutée pour la charge utile de la réponse :

✔ **meetingId**: utilisé par un onglet lors de l’exécution dans le contexte de la réunion.

### <a name="getparticipant-api"></a>API GetParticipant

> [!NOTE]
>
> * Ne pas mettre en cache les rôles des participants étant donné que l’organisateur de la réunion peut modifier un rôle à tout moment.
>
> * Teams ne prend actuellement pas en charge les listes de distribution volumineuses ni les tailles de liste de plus de 350 participants pour l' `GetParticipant` API.
>
> * La prise en charge du kit de développement logiciel (SDK) de robot sera bientôt disponible.

#### <a name="request"></a>Demande

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

*Voir* la référence de l’API de l' [infrastructure bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).

<!-- markdownlint-disable MD025 -->

**Exemple C#**

```csharp
string meetingId = "meetingid?";
string participantId = "participantidhere";
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage();
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
request.Method = new HttpMethod("GET");
request.RequestUri = new System.Uri(Path.Combine(connectorClient.BaseUri.OriginalString, $"/meetings/{meetingId}/participants/{participantId}"));
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, cancellationToken).ConfigureAwait(false);
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    var content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
    var theObject = Rest.Serialization.SafeJsonConvert.DeserializeObject<WhateverObjectIsReturned>(content, connectorClient.DeserializationSettings);
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a>Paramètres de requête

**meetingId**. L’identificateur de la réunion est obligatoire.  
**participantId**. L’identificateur du participant est obligatoire.  
**tenantId**. [ID de client](/onedrive/find-your-office-365-tenant-id) du participant. Obligatoire pour l’utilisateur client.

#### <a name="response-payload"></a>Charge utile de réponse
<!-- markdownlint-disable MD036 -->

**Exemple 1**

```json
{
   "meetingRole":"Presenter",
   "conversation":{
      "isGroup":true,
      "id":"19:meeting_NDQxMzg1YjUtMGIzNC00Yjc1LWFmYWYtYzk1MGY2MTMwNjE0@thread.v2"
   }
}
```

**meetingRole** peut être *organisateur*, *présentateur*ou *participant*.

**Exemple 2**

```json
{
   "meetingRole":"Attendee",
   "conversation":{
      "isGroup":true,
      "id":"19:meeting_OWIyYWVhZWMtM2ExMi00ZTc2LTg0OGEtYWNhMTM4MmZlZTNj@thread.v2"
   }
}
```

#### <a name="response-codes"></a>Codes de réponse

**403**: l’application n’est pas autorisée à obtenir des informations sur les participants. Il s’agit de la réponse d’erreur la plus courante, qui est déclenchée lorsque l’application n’est pas installée dans la réunion, par exemple lorsque l’application est désactivée par l’administrateur client ou bloquée lors de l’atténuation du site actif.  
**200**: informations sur les participants récupérées avec succès  
**401**: jeton non valide  
**404**: la réunion n’existe pas ou le participant est introuvable.

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a>API NotificationSignal

> [!NOTE]
> Lorsqu’une boîte de dialogue de réunion est appelée, le même contenu s’affiche également sous la forme d’un message de conversation.

#### <a name="request"></a>Demande

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a>Paramètres de requête

**conversationId**: identificateur de conversation. Obligatoire

#### <a name="request-payload"></a>Charge utile de la demande

# <a name="json"></a>[JSON](#tab/json)

```json
{
   "type":"message",
   "text":"John Phillips assigned you a weekly todo",
   "summary":"Don't forget to meet with Marketing next week",
   "channelData":{
      "notification":{
         "alert":true,
         "externalResourceUrl":"https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
      }
   },
   "replyToId":"1493070356924"
}
```

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
{
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
};
activity.ChannelData = new TeamsChannelData
{
    Notification = notification
};
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
        replyActivity.channelData = {
            notification: {
                alertInMeeting: true,
                externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>’
            }
        };
        await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> L’URL dans la bulle de contenu (URL de taskInfo) doit être incluse dans la liste des [domaines valide](../resources/schema/manifest-schema.md#validdomains) incluse dans le manifeste de l’application Teams.

#### <a name="response-codes"></a>Codes de réponse

**201**: l’activité avec le signal est correctement envoyée  
**401**: jeton non valide  
**403**: l’application n’est pas autorisée à envoyer le signal. Dans ce cas, la charge utile doit contenir plus de détails sur les messages d’erreur. Il peut y avoir plusieurs raisons : l’application est désactivée par l’administrateur client, bloquée lors de la limitation du site actif, etc.  
**404**: la conversation de réunion n’existe pas  

## <a name="enable-your-app-for-teams-meetings"></a>Activer votre application pour les réunions teams

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Les fonctionnalités des applications de réunion sont déclarées dans le manifeste **configurableTabs**de votre application via les  ->  **étendues** configurableTabs et les tableaux de **contexte** . L' *étendue* définit la personne et le *contexte* définissant où votre application sera disponible.

```json
"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a>Context, propriété

L’onglet `context` et les `scopes` propriétés fonctionnent en harmonie pour vous permettre de déterminer où vous souhaitez que votre application apparaisse. Alors que les onglets de l' `personal` étendue ne peuvent avoir qu’un seul contexte, c’est-à-dire, `personalTab`  `team` ou les `groupchat` onglets de portée peuvent contenir plusieurs contextes. Les valeurs possibles pour la propriété Context sont les suivantes :

* **channelTab**: onglet de l’en-tête d’un canal d’équipe.
* **privateChatTab**: onglet de l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs qui n’est pas dans le contexte d’une équipe ou d’une réunion.
* **meetingChatTab**: onglet de l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le contexte d’une réunion planifiée.
* **meetingDetailsTab**: onglet de l’en-tête de l’affichage Détails de la réunion du calendrier.
* **meetingSidePanel**: un panneau de réunion ouvert par le biais de la barre unifiée (u-bar).

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurer votre application pour les scénarios de réunion

> [!NOTE]
> Pour que votre application soit visible dans la Galerie d’onglets, elle doit **prendre en charge les onglets configurables** et l' **étendue de conversation de groupe**.

### <a name="pre-meeting"></a>Pré-réunion

Les utilisateurs disposant de rôles d’organisateur et/ou de présentateur ajoutent des onglets à une réunion en utilisant le bouton plus ➕ dans les pages **conversation** de réunion et **Détails** de la réunion. Les extensions de messagerie sont ajoutées à via le menu ellipses/Overflow &#x25CF;&#x25CF;&#x25CF; située sous la zone de message composer dans la conversation. Les robots sont ajoutés à une conversation de réunion à l’aide de la **@** touche «» et en sélectionnant **obtenir les bots**.

✔ L’identité de l’utilisateur *doit* être confirmée via les [onglets SSO](../tabs/how-to/authentication/auth-aad-sso.md). À la suite de cette authentification, l’application peut récupérer le rôle d’utilisateur via l’API GetParticipant.

 ✔ En fonction du rôle d’utilisateur, l’application est désormais capable de présenter des expériences spécifiques de rôle. Par exemple, une application d’interrogation peut autoriser uniquement les organisateurs et les présentateurs à créer une nouvelle interrogation.

> **Remarque**: les attributions de rôles peuvent être modifiées lorsqu’une réunion est en cours.  *Voir* [rôles dans une réunion teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019). 

### <a name="in-meeting"></a>Réunion

#### <a name="side-panel"></a>**panneau latéral**

✔ Dans votre manifeste d’application, ajoutez **sidePanel** au tableau **meetingSurfaces** , comme décrit ci-dessus.

✔ Dans la réunion, ainsi que dans tous les scénarios, l’application sera affichée sous la forme d’un onglet dans la réunion 320 px. Pour ce faire, vous devez optimiser l’onglet. *Voir*, [interface FrameContext](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)

✔ Reportez-vous au [Kit de développement logiciel teams](../tabs/how-to/access-teams-context.md#user-context) pour utiliser l’API **userContext** pour acheminer les demandes en conséquence.

✔ Reportez-vous au [flux d’authentification teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md). Le flux d’authentification des onglets est très similaire au flux d’authentification pour les sites Web. Par conséquent, les onglets peuvent utiliser OAuth 2,0 directement. *Voir aussi*la [plateforme d’identité Microsoft et le flux de code d’autorisation OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

#### <a name="in-meeting-dialog"></a>**boîte de dialogue de réunion**

✔ Vous devez respecter les [instructions de conception de la boîte de dialogue de réunion](../apps-in-teams-meetings/design/designing-in-meeting-dialog.md).

✔ Reportez-vous au [flux d’authentification teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md).

✔ Utiliser l’API de [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) pour signaler qu’une notification de bulle doit être déclenchée.

✔ Dans le cadre de la charge utile de la demande de notification, incluez l’URL où le contenu à présenter est hébergé.

> [!NOTE]
> Ces notifications sont permanentes. Vous devez appeler la fonction [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour faire une fermeture automatique après qu’un utilisateur a effectué une action dans l’affichage Web. Il s’agit d’une condition requise pour l’envoi d’une application. *Voir aussi*, [Kit de développement logiciel (SDK) teams : module de tâches](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).

### <a name="post-meeting"></a>Post-réunion

Les configurations post-réunion et de réunion sont équivalentes.

## <a name="meeting-app-sample"></a>Exemple d’application de réunion

 > [!div class="nextstepaction"]
> [Application du générateur de jetons de réunion](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)