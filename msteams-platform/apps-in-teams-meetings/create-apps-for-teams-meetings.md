---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions d’équipes
ms.topic: conceptual
ms.author: lajanuar
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 7f6d8fec735aa21033c6bcb2462c20458634f10a
ms.sourcegitcommit: 843da1730443ff8474a05295f60a6b376ed140da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2021
ms.locfileid: "50073095"
---
# <a name="create-apps-for-teams-meetings"></a>Créer des applications pour les réunions Teams

## <a name="prerequisites-and-considerations"></a>Conditions préalables et considérations

* Les applications dans les réunions nécessitent une connaissance de base du [développement d’applications Teams.](../overview.md) Une application dans une réunion peut comprendre des [onglets,](../tabs/what-are-tabs.md)des [bots](../bots/what-are-bots.md)et des [fonctionnalités d’extensions](../messaging-extensions/what-are-messaging-extensions.md) de messagerie et nécessitera des mises à jour du manifeste de l’application [Teams](#update-your-app-manifest) pour indiquer que l’application est disponible pour les réunions

* Pour que votre application fonctionne dans le cycle de vie de la réunion sous la mesure d’un onglet, elle doit prendre en charge les onglets configurables dans l’étendue [groupchat](../resources/schema/manifest-schema.md#configurabletabs) (voir comment créer un [onglet de groupe).](../build-your-first-app/build-channel-tab.md) La prise en charge de l’étendue active votre application dans les `groupchat` [conversations préalables à la réunion](teams-apps-in-meetings.md#pre-meeting-app-experience) et [post-réunion.](teams-apps-in-meetings.md#post-meeting-app-experience)

* Les paramètres d’URL de l’API de réunion peuvent nécessiter , et le tenantId, ceux-ci sont disponibles dans le cadre de l’activité du bot et du `meetingId` `userId` SDK [](/onedrive/find-your-office-365-tenant-id) client Teams. En outre, des informations fiables pour l’ID d’utilisateur et l’ID de locataire peuvent être récupérées à l’aide de l’authentification [sso tabulation.](../tabs/how-to/authentication/auth-aad-sso.md)

* Certaines API de réunion, telles que , nécessitent une inscription et un ID de bot pour générer des jetons `GetParticipant` d’th. [](../build-your-first-app/build-bot.md)

* Vous devez respecter les instructions générales de conception [de l’onglet Teams](../tabs/design/tabs.md) pour les scénarios préalables et post-réunion. Pour les expériences pendant les réunions, [reportez-vous](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) aux recommandations en matière de conception de l’onglet réunion et de la boîte [de](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) dialogue en réunion.

* Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités d’événements de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue en réunion (reportez-vous au paramètre d’achèvement dans ) et d’autres surfaces tout au long du cycle `bot Id` de vie de la `Notification Signal API` réunion

## <a name="meeting-apps-api-reference"></a>Référence de l’API des applications de réunion

|API|Description|Demande|Source|
|---|---|----|---|
|**GetUserContext**| Obtenez des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|Microsoft Teams client SDK|
|**GetParticipant**|Cette API permet à un bot de récupérer les informations d’un participant par ID de réunion et ID de participant.|**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** |Les signaux de réunion seront remis à l’aide de l’API de notification de conversation existante suivante (pour la conversation utilisateur-bot). Cette API permet aux développeurs de signaler en fonction de l’action de l’utilisateur final d’afficher une bulle de boîte de dialogue en réunion.|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

Pour obtenir des instructions sur l’identification et la récupération d’informations contextuelles pour le contenu de votre onglet, reportez-vous à notre documentation de l’onglet Obtenir du contexte pour votre onglet [Teams.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) Dans le cadre de l’extensibilité des réunions, une nouvelle valeur a été ajoutée pour la charge utile de réponse :

✔ **meetingId**: utilisé par un onglet lors de l’exécution dans le contexte de la réunion.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * Ne pas mettre en cache les rôles des participants, car l’organisateur de la réunion peut modifier un rôle à tout moment.
>
> * Teams ne prend actuellement pas en charge les grandes listes de distribution ou les tailles de liste de plus de 350 participants pour `GetParticipant` l’API.

#### <a name="query-parameters"></a>Paramètres de requête

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| string | Oui | L’identificateur de réunion est disponible via Bot Invoke et le SDK client Teams.|
|**participantId**| string | Oui | L’ID de participant est l’ID utilisateur. Il est disponible dans le SSO Onglet, l’appel de bot et le SDK client Teams. Il est vivement recommandé d’obtenir un participantId à partir de l' ssO Onglet. |
|**tenantId**| string | Oui | Le tenantId est requis pour les utilisateurs du client. Il est disponible dans le SSO Onglet, l’appel de bot et le SDK client Teams. Il est vivement recommandé d’obtenir un tenantId à partir de l' ssO Onglet. |

#### <a name="example"></a>Exemple

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
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
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
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
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

Le corps de la réponse est :

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

* * *

#### <a name="response-codes"></a>Codes de réponse

* **403**: l’application n’est pas autorisée à obtenir des informations sur les participants.  Il s’agit de la réponse d’erreur la plus courante et est déclenchée si l’application n’est pas installée dans la réunion. Par exemple, si l’application est désactivée par l’administrateur client ou bloquée lors de la migration de site en direct.
* **200**: Informations de participant correctement récupérées.
* **401 :** jeton non valide.
* **404 :** Le participant est in found.
* **500**: la réunion a expiré (plus de 60 jours depuis la fin de la réunion) ou le participant ne dispose pas d’autorisations en fonction de son rôle.


**Bientôt disponible**

* **404 :** la réunion a expiré ou le participant est in peut-être trouvé.


### <a name="notificationsignal-api"></a>NotificationSignal API

> [!NOTE]
> Lorsqu’une boîte de dialogue de réunion est invoquée, le même contenu est également présenté en tant que message de conversation.

#### <a name="query-parameters"></a>Paramètres de requête

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**conversationId**| string | Oui | L’identificateur de conversation est disponible dans le cadre de l’appel de bot |

#### <a name="example"></a>Exemple

> [!NOTE]
>
Le `completionBotId` paramètre est facultatif dans `externalResourceUrl` l’exemple de charge utile demandé. `Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.
> * Les paramètres largeur et hauteur externalResourceUrl doivent être en pixels. Reportez-vous [aux instructions de](design/designing-apps-in-meetings.md) conception pour vous assurer que les dimensions sont dans les limites autorisées.
> * L’URL est la page chargée en tant que `<iframe>` dans la boîte de dialogue de la réunion. Le domaine doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
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

* * *

#### <a name="response-codes"></a>Codes de réponse

* **201 :** l’activité avec le signal est correctement envoyée  
* **401 :** jeton non valide  
* **201 : l’activité** avec le signal est correctement envoyée. 
* **401 :** jeton non valide.
* **403**: l’application ne parvient pas à envoyer le signal. Cela peut se produire pour diverses raisons, telles que la désactivation de l’application par l’administrateur client, le blocage de l’application pendant la migration du site en direct, etc. Dans ce cas, la charge utile contient un message d’erreur détaillé. 
* **404 :** La conversation de réunion n’existe pas.
 

## <a name="enable-your-app-for-teams-meetings"></a>Activer votre application pour les réunions Teams

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Les fonctionnalités de l’application réunions sont déclarées dans le manifeste de votre application via les **étendues configurableTabs** et les  ->   tableaux de contexte.  *L’étendue* définit à qui et *le contexte* définit l’endroit où votre application sera disponible.

> [!NOTE]
> Utilisez le [schéma de manifeste d’aperçu du](../resources/schema/manifest-schema-dev-preview.md) développeur pour l’essayer dans le manifeste de votre application.

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

### <a name="context-property"></a>Propriété Context

L’onglet et les propriétés fonctionnent en harmonie pour vous permettre de déterminer où `context` `scopes` vous souhaitez que votre application apparaisse. Les onglets de la `team` ou `groupchat` de l’étendue peuvent avoir plusieurs contextes. Les valeurs possibles pour la propriété de contexte sont les suivantes :

* **channelTab**: onglet dans l’en-tête d’un canal d’équipe.
* **privateChatTab**: un onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs non dans le contexte d’une équipe ou d’une réunion.
* **meetingChatTab**: onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le cadre d’une réunion programmée.
* **meetingDetailsTab**: un onglet dans l’en-tête de l’affichage détails de la réunion du calendrier.
* **meetingSidePanel**: un panneau en réunion ouvert via la barre unifiée (u-bar).

> [!NOTE]
> La propriété « Context » n’est actuellement pas prise en charge et sera donc ignorée sur les clients mobiles

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurer votre application pour les scénarios de réunion

> [!NOTE]
> * Pour que votre application soit visible dans la galerie d’onglets, elle doit prendre en charge les **onglets configurables** et **l’étendue de conversation de groupe.**
>
> * Les clients mobiles ne supportent les onglets que dans les surfaces de pré et de post-réunion. Les expériences en réunion (boîte de dialogue de réunion et onglet) sur mobile seront bientôt disponibles. Suivez les [instructions pour les onglets sur mobile](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour appareils mobiles.

### <a name="before-a-meeting"></a>Avant une réunion

Les utilisateurs ayant des rôles d’organisateur et/ou de présentateur ajoutent des onglets à une réunion à l’aide du bouton ➕ plus dans les pages de **détails** et de conversation de réunion.  Les extensions de messagerie sont ajoutées via le menu ellipses/overflow &#x25CF;&#x25CF;&#x25CF; située sous la zone de composition de message dans la conversation. Les bots sont ajoutés à une conversation de réunion à l’aide de la clé « « et **@** en sélectionnant **Obtenir des bots**».

✔ l’identité *de l’utilisateur* doit être confirmée via l' [ssO Onglets.](../tabs/how-to/authentication/auth-aad-sso.md) Après cette authentification, l’application peut récupérer le rôle d’utilisateur via l’API GetParticipant.

 ✔ en fonction du rôle d’utilisateur, l’application aura désormais la possibilité de présenter des expériences spécifiques au rôle. Par exemple, une application de sondage peut autoriser uniquement les organisateurs et les présentateurs à créer un sondage.

> **REMARQUE**: les attributions de rôle peuvent être modifiées lors d’une réunion en cours.  *Voir rôles* [dans une réunion Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019) 

### <a name="during-a-meeting"></a>Pendant une réunion

#### <a name="sidepanel"></a>**sidePanel**

✔ dans le manifeste de votre application, ajoutez **sidePanel** **au** tableau de contexte comme décrit ci-dessus.

✔ dans la réunion, ainsi que dans tous les scénarios, l’application s’restituera dans un onglet de réunion de 320 px de largeur. Votre onglet doit être optimisé pour cela. *Voir*, [Interface FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔ [SDK Teams](../tabs/how-to/access-teams-context.md#user-context) pour utiliser l’API **userContext** afin d’router les demandes en conséquence.

✔ faire référence au flux [d’authentification Teams pour les onglets.](../tabs/how-to/authentication/auth-flow-tab.md) Le flux d’authentification pour les onglets est très similaire au flux d’authentification pour les sites web. Par conséquent, les onglets peuvent utiliser OAuth 2.0 directement. *Voir aussi*, plateforme d’identité Microsoft et flux de code d’autorisation [OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

✔'extension de message doit fonctionner comme prévu lorsqu’un utilisateur est dans un affichage en réunion et doit être en mesure de publier des cartes d’extension de message de composition.

✔ AppName en réunion : l’outil doit faire état du nom de l’application dans la barre U de la réunion.

#### <a name="in-meeting-dialog"></a>**Boîtes de dialogue en réunion**

✔ vous devez respecter les instructions de conception de boîte de [dialogue en réunion.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

✔ faire référence au flux [d’authentification Teams pour les onglets.](../tabs/how-to/authentication/auth-flow-tab.md)

✔ l’API [NotificationSignal](create-apps-for-teams-meetings.md#notificationsignal-api) pour signaler qu’une notification de bulle doit être déclenchée.

✔ dans le cadre de la charge utile de demande de notification, incluez l’URL où le contenu à présenter est hébergé.

✔ dialogue En réunion ne doit pas utiliser le module de tâche.

> [!NOTE]
>
> * Ces notifications sont de nature persistante. Vous devez appeler la [**fonction submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour le faire disparaître automatiquement après qu’un utilisateur a pris une action dans l’affichage web. Il s’agit d’une condition requise pour la soumission d’application. *Voir aussi*, [SDK Teams : module de tâche](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
>
> * Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, votre charge utile de demande d’appel initiale doit reposer sur les métadonnées de demande (ID de l’utilisateur) dans l’objet, et non sur les métadonnées de demande `from.id` `from` `from.aadObjectId` (ID Azure Active Directory de l’utilisateur). *Voir* [Utilisation des modules de tâche dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) et Créer et envoyer le module de [tâche.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

### <a name="after-a-meeting"></a>Après une réunion

Les configurations post-réunion et préalable à la réunion sont équivalentes.

## <a name="meeting-app-sample"></a>Exemple d’application de réunion

 > [!div class="nextstepaction"]
> [Application générateur de jetons de réunion](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
