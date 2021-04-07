---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions d’équipes
ms.topic: conceptual
ms.author: lajanuar
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: d9356e37a0c2b5b70d23fc6805b0af5340a1efc6
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596230"
---
# <a name="create-apps-for-teams-meetings"></a>Créer des applications pour les réunions Teams

## <a name="prerequisites-and-considerations"></a>Conditions préalables et considérations

Avant de créer des applications pour les réunions Teams, vous devez avoir les connaissances suivantes :

* Vous devez savoir comment développer des applications Teams. Pour plus d’informations, voir [Développement d’applications Teams.](../overview.md)

* Vous devez mettre à jour le manifeste de l’application Teams pour indiquer que l’application est disponible pour les réunions. Pour plus d’informations, voir [le manifeste de l’application.](#update-your-app-manifest)

* Pour que votre application fonctionne dans le cycle de vie de la réunion sous la mesure d’un onglet, elle doit prendre en charge les onglets configurables dans l’étendue groupchat. Pour plus d’informations, voir [étendue groupchat](../resources/schema/manifest-schema.md#configurabletabs) et [créer un onglet de groupe.](../build-your-first-app/build-channel-tab.md)

* Vous devez respecter les instructions générales de conception de l’onglet Teams pour les scénarios préalables et post-réunion. Pour les expériences pendant les réunions, reportez-vous aux recommandations en matière de conception de l’onglet réunion et de la boîte de dialogue en réunion. Pour plus d’informations, consultez les recommandations en matière de conception d’onglets [Teams,](../tabs/design/tabs.md)de conception d’onglets en réunion et de conception de boîte de dialogue [en réunion.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)

* Vous devez prendre en charge l’étendue pour activer votre application dans les conversations `groupchat` préalables à la réunion et post-réunion. Avec l’expérience d’application de pré-réunion, vous pouvez rechercher et ajouter des applications de réunion et effectuer des tâches préalables à la réunion. Avec l’expérience d’application post-réunion, vous pouvez afficher les résultats de la réunion, tels que les résultats des sondages ou les commentaires.

* Les paramètres d’URL de l’API de réunion doivent avoir `meetingId` `userId` , et `tenantId` . Ils sont disponibles dans le cadre de l’activité du bot et du SDK client Teams. En outre, des informations fiables pour l’ID d’utilisateur et l’ID de locataire peuvent être récupérées à l’aide de l’authentification [sso tabulation.](../tabs/how-to/authentication/auth-aad-sso.md)

* `GetParticipant`L’API doit avoir un ID et une inscription de bot pour générer des jetons d’th. Pour plus d’informations, voir [l’inscription et l’ID du bot.](../build-your-first-app/build-bot.md)

* Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités d’événements de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue de réunion et dans d’autres étapes du cycle de vie de la réunion. Pour la boîte de dialogue de réunion, voir paramètre `bot Id` d’achèvement dans `Notification Signal API` .

## <a name="meeting-apps-api-reference"></a>Référence de l’API des applications de réunion

|API|Description|Demande|Source|
|---|---|----|---|
|**GetUserContext**| Cette API vous permet d’obtenir des informations contextuelles pour afficher du contenu pertinent dans un onglet Teams. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|Microsoft Teams client SDK|
|**GetParticipant**| Cette API permet à un bot de récupérer les informations des participants par ID de réunion et ID de participant. |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Cette API vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot. Il vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

Pour identifier et récupérer des informations contextuelles pour le contenu de votre onglet, voir [obtenir le contexte de votre onglet Teams.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) est utilisé par un onglet lors de l’exécution dans le contexte de réunion et est `meetingId` ajouté pour la charge utile de réponse.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * Ne pas mettre en cache les rôles des participants, car l’organisateur de la réunion peut modifier un rôle à tout moment.
> * Teams ne prend actuellement pas en charge les grandes listes de distribution ou les tailles de liste de plus de 350 participants pour `GetParticipant` l’API.

#### <a name="query-parameters"></a>Paramètres de requête

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| string | Oui | L’identificateur de réunion est disponible via Bot Invoke et le SDK client Teams.|
|**participantId**| string | Oui | L’ID de participant est l’ID utilisateur. Il est disponible dans le SSO Onglet, l’appel de bot et le SDK client Teams. Il est recommandé d’obtenir un ID de participant à partir de l' sso tabulation. |
|**tenantId**| string | Oui | L’ID de client est requis pour les utilisateurs du client. Il est disponible dans le SSO Onglet, l’appel de bot et le SDK client Teams. Il est recommandé d’obtenir un ID de client à partir de l' sso onglet. |

#### <a name="example"></a>Exemple

# <a name="c"></a>[C#](#tab/dotnet)

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

* * *

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

|Code de réponse|Description|
|---|---|
| **403** | L’application n’est pas autorisée à obtenir des informations sur les participants. Il s’agit de la réponse d’erreur la plus courante et est déclenchée si l’application n’est pas installée dans la réunion. Par exemple, si l’application est désactivée par l’administrateur client ou bloquée lors de la migration de site en direct.|
| **200** | Les informations sur les participants sont récupérées avec succès.|
| **401** | L’application répond avec un jeton non valide.|
| **404** | La réunion a expiré ou le participant est in peut-être trouvé.|
| **500** | La réunion a expiré plus de 60 jours depuis la fin de la réunion ou le participant ne dispose pas d’autorisations en fonction de son rôle.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Tous les utilisateurs d’une réunion reçoivent les notifications envoyées via `NotificationSignal` l’API.

> [!NOTE]
> * Lorsqu’une boîte de dialogue de réunion est invoquée, le contenu est présenté comme un message de conversation.
> * Actuellement, l’envoi de notifications ciblées n’est pas pris en charge.

#### <a name="query-parameters"></a>Paramètres de requête

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**conversationId**| string | Oui | L’identificateur de conversation est disponible dans le cadre de l’appel de bot |

#### <a name="example"></a>Exemple

`Bot ID`L’objet est déclaré dans le manifeste et le bot reçoit un objet de résultat.

> [!NOTE]
> * Le `completionBotId` paramètre est facultatif dans `externalResourceUrl` l’exemple de charge utile demandé. `Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.
> * Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels. Pour vous assurer que les dimensions sont dans les limites autorisées, consultez les [instructions de conception.](design/designing-apps-in-meetings.md)
> * L’URL est la page chargée en tant que dans la boîte de `<iframe>` dialogue de la réunion. Le domaine doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.

# <a name="c"></a>[C#](#tab/dotnet)

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

|Code de réponse|Description|
|---|---|
| **201** | L’activité avec signal est correctement envoyée |
| **401** | L’application répond avec un jeton non valide. |
| **403** | L’application ne peut pas envoyer le signal. Cela peut se produire pour diverses raisons, telles que la désactivation de l’application par l’administrateur client, le blocage de l’application pendant la migration du site en direct, etc. Dans ce cas, la charge utile contient un message d’erreur détaillé. |
| **404** | La conversation de réunion n’existe pas. |

## <a name="enable-your-app-for-teams-meetings"></a>Activer votre application pour les réunions Teams

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Les fonctionnalités de l’application réunions sont déclarées dans le manifeste de votre application à l’aide `configurableTabs` des `scopes` tableaux et des `context` tableaux. L’étendue définit à qui et le contexte définit l’endroit où votre application est disponible.

> [!NOTE]
> Essayez de mettre à jour le manifeste de votre application avec [le schéma de manifeste.](../resources/schema/manifest-schema-dev-preview.md)
> Les applications dans les réunions ont besoin *d’une étendue groupchat.* *L’étendue de* l’équipe fonctionne pour les onglets dans les canaux uniquement.

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
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> `meetingStage` est actuellement disponible en prévisualisation pour les développeurs uniquement.

### <a name="context-property"></a>Propriété Context

`context`L’onglet et `scopes` les propriétés vous permettent de déterminer où votre application doit apparaître. Les onglets de la `team` ou `groupchat` de l’étendue peuvent avoir plusieurs contextes. Voici les valeurs de la propriété à partir de laquelle vous pouvez utiliser l’ensemble ou `context` certaines des valeurs :

|Valeur|Description|
|---|---|
| **channelTab** | Onglet dans l’en-tête d’un canal d’équipe. |
| **privateChatTab** | Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs non dans le contexte d’une équipe ou d’une réunion. |
| **meetingChatTab** | Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le cadre d’une réunion programmée. |
| **meetingDetailsTab** | Onglet dans l’en-tête de l’affichage Détails de la réunion du calendrier. |
| **meetingSidePanel** | Panneau en réunion ouvert via la barre unifiée (barre U). |
| **meetingStage** | Une application à partir du sidepanel peut être partagée à l’étape de la réunion. |

> [!NOTE]
> `Context` n’est actuellement pas prise en charge sur les clients mobiles.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurer votre application pour les scénarios de réunion

> [!NOTE]
> * Pour que votre application soit visible dans la galerie d’onglets, elle doit prendre en charge les onglets configurables et l’étendue de conversation de groupe.
> * Les clients mobiles ne supportent les onglets qu’aux étapes préalables et post-réunion.
> * Les expériences en réunion qui sont des boîtes de dialogue et des onglets en réunion ne sont actuellement pas pris en charge sur les clients mobiles. Pour plus d’informations, [consultez des conseils pour les onglets mobiles](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour appareils mobiles.

### <a name="before-a-meeting"></a>Avant une réunion

Avant une réunion, les utilisateurs peuvent ajouter des onglets, des bots et des extensions de messagerie à une réunion. Les utilisateurs ayant des rôles d’organisateur et de présentateur peuvent ajouter des onglets à une réunion.

**Pour ajouter un onglet à une réunion**

1. Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.
1. Sélectionnez **l’onglet Détails** et sélectionnez plus <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. La galerie d’onglets s’affiche.

    ![Expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

1. Dans la galerie d’onglets, sélectionnez l’application à ajouter et suivez les étapes nécessaires. L’application est installée en tant qu’onglet.
    > [!NOTE] 
    > Actuellement, dans l’onglet Réunions, l’obtention des détails de la réunion et des informations sur les participants n’est pas prise en charge.

**Pour ajouter une extension de messagerie à une réunion**

1. Sélectionnez les ellipses ou le menu de dépassement &#x25CF;&#x25CF;&#x25CF; dans la zone composer un message de la conversation.
1. Sélectionnez l’application à ajouter et suivez les étapes nécessaires. L’application est installée en tant qu’extension de messagerie.

**Pour ajouter un bot à une réunion**

Dans une conversation de réunion, entrez **@** la clé et **sélectionnez Obtenir des bots.**

> [!NOTE]
> * L’identité de l’utilisateur doit être confirmée à l’aide de [l' ssO Onglets.](../tabs/how-to/authentication/auth-aad-sso.md) Après l’authentification, l’application peut récupérer le rôle d’utilisateur à l’aide de `GetParticipant` l’API.
> * En fonction du rôle utilisateur, l’application a la possibilité de fournir des expériences spécifiques au rôle. Par exemple, une application de sondage permet uniquement aux organisateurs et aux présentateurs de créer un sondage.
> * Les attributions de rôle peuvent être modifiées pendant une réunion. Pour plus d’informations, voir [les rôles dans une réunion Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

### <a name="during-a-meeting"></a>Pendant une réunion

#### <a name="sidepanel"></a>sidePanel

Avec sidePanel, vous pouvez personnaliser les expériences d’une réunion qui permettent aux organisateurs et aux présentateurs d’avoir différents ensembles d’affichages et d’actions. Dans le manifeste de votre application, vous devez ajouter sidePanel au tableau de contexte. Dans la réunion et dans tous les scénarios, l’application est restituer dans un onglet de réunion de 320 pixels de largeur. Pour plus d’informations, [voir l’interface FrameContext.](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

Pour utiliser `userContext` l’API pour router les demandes en conséquence, consultez [le SDK Teams.](../tabs/how-to/access-teams-context.md#user-context) Voir [flux d’authentification Teams pour les onglets.](../tabs/how-to/authentication/auth-flow-tab.md) Le flux d’authentification pour les onglets est très similaire au flux d’authentification pour les sites web. Par conséquent, les onglets peuvent utiliser OAuth 2.0 directement. Voir la plateforme d’identité Microsoft et le flux de [code d’autorisation OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)

L’extension de messagerie fonctionne comme prévu lorsqu’un utilisateur est dans un affichage en réunion et qu’il peut publier des cartes d’extension de message de composition. AppName en réunion est une boîte à outils qui indique le nom de l’application dans la barre U de la réunion.

#### <a name="in-meeting-dialog"></a>Boîtes de dialogue en réunion

La boîte de dialogue de réunion peut être utilisée pour impliquer les participants au cours de la réunion et collecter des informations ou des commentaires pendant la réunion. Utilisez [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) l’API pour signaler qu’une notification de bulle doit être déclenchée. Dans le cadre de la charge utile de demande de notification, incluez l’URL où le contenu à afficher est hébergé.

La boîte de dialogue en réunion ne doit pas utiliser le module de tâche. Le module de tâche n’est pas appelé dans une conversation de réunion. Une URL de ressource externe est utilisée pour afficher une bulle de contenu dans une réunion. Vous pouvez utiliser la `submitTask` méthode pour envoyer des données dans une conversation de réunion.

> [!NOTE]
> * Vous devez appeler la [fonction submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour ignorer automatiquement une fois qu’un utilisateur a pris une action dans l’affichage web. Il s’agit d’une condition requise pour la soumission d’application. Pour plus d’informations, voir le module de [tâche du SDK Teams.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)
> * Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, votre charge utile de demande d’appel initiale doit reposer sur les métadonnées de la demande dans l’objet, et non sur `from.id` `from` les `from.aadObjectId` métadonnées de la demande. `from.id` est l’ID utilisateur et `from.aadObjectId` l’ID Azure Active Directory (AAD) de l’utilisateur. Pour plus d’informations, voir [l’utilisation de modules de tâche](../task-modules-and-cards/task-modules/task-modules-tabs.md) dans les onglets [et créer et envoyer le module de tâche.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

#### <a name="share-to-stage"></a>Partager pour mettre en scène 

> [!NOTE]
> Cette fonctionnalité est disponible uniquement dans la prévisualisation du développement insider


Cette fonctionnalité permet aux développeurs de partager une application au stade de la réunion. En activant le partage à l’étape de la réunion, les participants à la réunion peuvent collaborer en temps réel. 

Le contexte requis est meetingStage dans le manifeste de l’application. Une condition préalable pour cela consiste à avoir le contexte meetingSidePanel. Cela active le bouton « Partager » dans le sidepanel comme spécifié ci-dessous



### <a name="after-a-meeting"></a>Après une réunion

Les configurations post-réunion et préalable à la réunion sont équivalentes.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| Extensibilité des réunions | Exemple d’extensibilité de réunion Microsoft Teams pour transmettre des jetons. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | |
| Bot de bulles de contenu de réunion | Exemple d’extensibilité de réunion Microsoft Teams pour l’interaction avec le bot de bulles de contenu dans une réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Recommandations en matière de conception de boîte de dialogue en réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
> [!div class="nextstepaction"]
> [Flux d’authentification Teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
