---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions d’équipes
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: équipes apps réunions utilisateur participant rôle api
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565913"
---
# <a name="create-apps-for-teams-meetings"></a>Créer des applications pour les réunions Teams

## <a name="prerequisites-and-considerations"></a>Conditions préalables et considérations

Avant de créer des applications pour Teams réunions, vous devez avoir une compréhension des éléments suivants :

* Vous devez avoir une connaissance de la façon de développer Teams applications. Pour plus d’informations, [consultez Teams développement d’applications](../overview.md).

* Vous devez mettre à jour le Teams’application pour indiquer que l’application est disponible pour les réunions. Pour plus d’informations, voir [manifeste de l’application](#update-your-app-manifest).

* Pour que votre application fonctionne dans le cycle de vie de la réunion sous forme d’onglet, elle doit prendre en charge les onglets configurables dans la portée groupchat. Pour plus d’informations, consultez [la portée groupchat](../resources/schema/manifest-schema.md#configurabletabs) et [créez un onglet groupe](../build-your-first-app/build-channel-tab.md).

* Vous devez respecter les lignes directrices générales Teams conception des onglets pour les scénarios avant et après la réunion. Pour les expériences pendant les réunions, consultez l’onglet en réunion et les lignes directrices de conception de dialogue en réunion. Pour plus d’informations, consultez [les Teams de conception d’onglets,](../tabs/design/tabs.md)les lignes [directrices de conception d’onglets en](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) réunion et les lignes [directrices de conception de dialogue en réunion.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

* Vous devez prendre en charge `groupchat` la portée pour activer votre application dans les conversations de pré-réunion et post-réunion. Grâce à l’expérience de l’application pré-réunion, vous pouvez trouver et ajouter des applications de réunion et effectuer des tâches de pré-réunion. Grâce à l’expérience de l’application après la réunion, vous pouvez consulter les résultats de la réunion, tels que les résultats du sondage ou les commentaires.

* La réunion des paramètres d’URL de l’API `meetingId` doit avoir , et `userId` `tenantId` . Ceux-ci sont disponibles dans le cadre de l Teams client SDK et l’activité bot. En outre, des informations fiables pour l’identification de l’utilisateur et l’ID locataire peuvent être récupérées à l’aide [de l’authentification Tab SSO](../tabs/how-to/authentication/auth-aad-sso.md).

* `GetParticipant`L’API doit avoir un enregistrement de bot et un ID pour générer des jetons auth. Pour plus d’informations, voir [inscription bot et ID](../build-your-first-app/build-bot.md).

* Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités de l’événement lors de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue en réunion et dans d’autres étapes du cycle de vie de la réunion. Pour la boîte de dialogue en réunion, voir le paramètre `bot Id` d’achèvement dans `Notification Signal API` .

## <a name="meeting-apps-api-reference"></a>Référence API des applications de réunion

|API|Description|Demande|Source|
|---|---|----|---|
|**GetUserContexte GetUserContext GetUserContext GetUs**| Cette API vous permet d’obtenir des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams’écran. |_**microsoftTeams.getContext ( ) => { /*...* / } )**_|Microsoft Teams client SDK|
|**GetParticipant**| Cette API permet à un bot d’aller chercher des informations sur les participants en rencontrant l’ID et l’ID du participant. |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK (en)|
|**NotificationSignal (notifications)** | Cette API vous permet de fournir des signaux de réunion qui sont livrés à l’aide de l’API de notification de conversation existante pour le chat utilisateur-bot. Il vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion. |**POST** _**/v3/conversations/{conversationId}/activités**_|Microsoft Bot Framework SDK (en)|

### <a name="getusercontext"></a>GetUserContexte GetUserContext GetUserContext GetUs

Pour identifier et récupérer les informations contextuelles pour le contenu de votre onglet, [consultez le contexte de votre onglet Teams’onglet](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId`est utilisé par un onglet lors de l’exécution dans le contexte de la réunion et est ajouté pour la charge utile de réponse.

### <a name="getparticipant-api"></a>GetPi GetParticipant

> [!NOTE]
> * Ne cachez pas les rôles des participants puisque l’organisateur de la réunion peut changer de rôle à tout moment.
> * Teams’appuie pas actuellement les grandes listes de distribution ou la taille des listes de plus de 350 participants pour `GetParticipant` l’API.

#### <a name="query-parameters"></a>Paramètres de requête

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**meetingId**| string | Oui | L’identificateur de réunion est disponible via Bot Invoke Teams client SDK.|
|**participantId**| string | Oui | L’iD participant est l’identifiant de l’utilisateur. Il est disponible dans Tab SSO, Bot Invoke et Teams Client SDK. Il est recommandé d’obtenir un iD participant de l’onglet SSO. |
|**tenantId**| string | Oui | L’identification du locataire est requise pour les utilisateurs locataires. Il est disponible dans Tab SSO, Bot Invoke et Teams Client SDK. Il est recommandé d’obtenir une pièce d’identité du locataire de l’onglet SSO. |

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

L’organe de réponse JSON pour `GetParticipant` l’API est :

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
| **403** | L’application n’est pas autorisée à obtenir des informations sur les participants. Il s’agit de la réponse d’erreur la plus courante et est déclenchée si l’application n’est pas installée dans la réunion. Par exemple, si l’application est désactivée par l’administrateur locataire ou bloquée pendant la migration du site en direct.|
| **200** | Les informations des participants sont récupérées avec succès.|
| **401** | L’application répond par un jeton invalide.|
| **404** | La réunion est expirée ou le participant ne peut pas être trouvé.|
| **500** | La réunion a expiré plus de 60 jours depuis la fin de la réunion ou le participant n’a pas d’autorisations en fonction de son rôle.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Tous les utilisateurs d’une réunion reçoivent les notifications envoyées via `NotificationSignal` l’API.

> [!NOTE]
> * Lorsqu’une boîte de dialogue en réunion est invoquée, le contenu est présenté comme un message de chat.
> * Actuellement, l’envoi de notifications ciblées n’est pas pris en charge.

#### <a name="query-parameters"></a>Paramètres de requête

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**conversationId**| string | Oui | L’identificateur de conversation est disponible dans le cadre de bot invoquer. |

#### <a name="example"></a>Exemple

Le `Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.

> [!NOTE]
> * Le `completionBotId` paramètre de la `externalResourceUrl` est facultative dans l’exemple de charge utile demandé. `Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.
> * Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels. Pour vous assurer que les dimensions sont dans les limites autorisées, consultez les lignes [directrices de conception.](design/designing-apps-in-meetings.md)
> * L’URL est la page chargée comme `<iframe>` un dans la boîte de dialogue en réunion. Le domaine doit être dans le tableau de `validDomains` l’application dans votre manifeste d’application.

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
| **201** | L’activité avec signal est envoyée avec succès. |
| **401** | L’application répond par un jeton invalide. |
| **403** | L’application n’est pas en mesure d’envoyer le signal. Cela peut se produire pour diverses raisons telles que l’administrateur locataire désactive l’application, l’application est bloquée pendant la migration du site en direct, et ainsi de suite. Dans ce cas, la charge utile contient un message d’erreur détaillé. |
| **404** | Le chat de réunion n’existe pas. |

## <a name="enable-your-app-for-teams-meetings"></a>Activez votre application pour Teams réunions

### <a name="update-your-app-manifest"></a>Mettez à jour le manifeste de votre application

Les fonctionnalités de l’application de réunions sont déclarées dans le manifeste de votre application à `configurableTabs` l’aide de la , et les `scopes` `context` tableaux. Scope définit à qui et le contexte définit l’endroit où votre application est disponible.

> [!NOTE]
> Essayez de mettre à jour votre manifeste d’application [avec le schéma manifeste](../resources/schema/manifest-schema-dev-preview.md).
> Les applications dans les réunions ont besoin *d’une portée groupchat.* La *portée de* l’équipe fonctionne uniquement pour les onglets dans les canaux.

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
> `meetingStage` est actuellement disponible en aperçu développeur seulement.

### <a name="context-property"></a>Propriété context

L’onglet `context` et les propriétés vous permettent de déterminer `scopes` où votre application doit apparaître. Les onglets dans la `team` portée ou la portée peuvent avoir plus `groupchat` d’un contexte. Voici les valeurs de la propriété `context` à partir de laquelle vous pouvez utiliser la plupart ou certaines des valeurs:

|Valeur|Description|
|---|---|
| **channelTab (en)** | Un onglet dans l’en-tête d’un canal d’équipe. |
| **privateChatTab (en)** | Un onglet dans l’en-tête d’un chat de groupe entre un ensemble d’utilisateurs non dans le cadre d’une équipe ou d’une réunion. |
| **réunionChatTab** | Un onglet dans l’en-tête d’un chat de groupe entre un ensemble d’utilisateurs dans le cadre d’une réunion planifiée. |
| **réunionDetailsTab** | Un onglet dans l’en-tête de la réunion détaille la vue du calendrier. |
| **réunionSidePanel** | Un panel en réunion s’est ouvert via la barre unifiée (U-bar). |
| **réunionStage** | Une application du sidepanel peut être partagée jusqu’à l’étape de la réunion. |

> [!NOTE]
> `Context` propriété n’est actuellement pas prise en charge sur les clients mobiles.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurez votre application pour des scénarios de réunion

> [!NOTE]
> * Pour que votre application soit visible dans la galerie d’onglets, elle doit prendre en charge les onglets configurables et la portée de chat de groupe.
> * Les clients mobiles ne supporte les onglets qu’aux étapes avant et après la réunion.
> * Les expériences en réunion qui sont en réunion boîte de dialogue et onglet n’est actuellement pas pris en charge sur les clients mobiles. Pour plus d’informations, consultez [les conseils pour les onglets sur mobile](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour mobile.

### <a name="before-a-meeting"></a>Avant une réunion

Avant une réunion, les utilisateurs peuvent ajouter des onglets, des bots et des extensions de messagerie à une réunion. Les utilisateurs ayant des rôles d’organisateur et de présentateur peuvent ajouter des onglets à une réunion.

**Pour ajouter un onglet à une réunion**

1. Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.
1. Sélectionnez **l’onglet Détails** et sélectionnez plus <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. La galerie d’onglets apparaît.

    ![Expérience de pré-réunion](../assets/images/apps-in-meetings/PreMeeting.png)

1. Dans la galerie d’onglets, sélectionnez l’application que vous souhaitez ajouter et suivez les étapes au besoin. L’application est installée sous forme d’onglet.
    > [!NOTE] 
    > À l’heure actuelle, dans l’onglet réunions, il n’est pas pris en charge l’obtention des détails de la réunion et de l’information sur les participants.

**Pour ajouter une extension de messagerie à une réunion**

1. Sélectionnez les ellipses ou le menu de débordement &#x25CF;&#x25CF;&#x25CF; dans la zone de message de composition dans le chat.
1. Sélectionnez l’application que vous souhaitez ajouter et suivez les étapes au besoin. L’application est installée comme une extension de messagerie.

**Pour ajouter un bot à une réunion**

Dans un chat de réunion entrez **@** la clé et **sélectionnez Get bots**.

> [!NOTE]
> * L’identité de l’utilisateur doit être confirmée à [l’aide de Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md). Après authentification, l’application peut récupérer le rôle de l’utilisateur à l’aide de `GetParticipant` l’API.
> * En fonction du rôle de l’utilisateur, l’application a la capacité de fournir des expériences spécifiques au rôle. Par exemple, une application de sondage permet uniquement aux organisateurs et aux présentateurs de créer un nouveau sondage.
> * Les affectations de rôle peuvent être modifiées pendant qu’une réunion est en cours. Pour plus d’informations, [voir les rôles dans une Teams réunion](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### <a name="during-a-meeting"></a>Au cours d’une réunion

#### <a name="sidepanel"></a>sidePanel (sidePanel)

Avec sidePanel, vous pouvez personnaliser les expériences d’une réunion qui permet aux organisateurs et aux présentateurs d’avoir différents ensembles de points de vue et d’actions. Dans votre manifeste d’application, vous devez ajouter sidePanel au tableau contextnel. Dans la réunion et dans tous les scénarios, l’application est rendue dans un onglet en réunion de 320 pixels de largeur. Pour plus d’informations, [voir interface FrameContext](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).

Pour utiliser `userContext` l’API pour acheminer les demandes en conséquence, [Teams SDK](../tabs/how-to/access-teams-context.md#user-context). Voir [le Teams’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md). Le flux d’authentification pour les onglets est très similaire au flux auth pour les sites Web. Ainsi, les onglets peuvent utiliser OAuth 2.0 directement. Voir, [Plateforme d’identités Microsoft et OAuth 2.0 flux de code d’autorisation](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

L’extension de messagerie fonctionne comme prévu lorsqu’un utilisateur est dans une vue en réunion et que l’utilisateur peut poster des cartes d’extension de message. AppName en réunion est un tooltip qui indique le nom de l’application en réunion U-bar.

> [!NOTE]
> Utilisez la version 1.7.0 ou plus [de Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), car les versions antérieures ne supportent pas le panneau latéral.

#### <a name="in-meeting-dialog"></a>Boîtes de dialogue en réunion

La boîte de dialogue en réunion peut être utilisée pour engager les participants pendant la réunion et recueillir des informations ou des commentaires pendant la réunion. Utilisez [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) l’API pour signaler qu’une notification de bulle doit être déclenchée. Dans le cadre de la charge utile de la demande de notification, inclure l’URL où le contenu à montrer est hébergé.

Le dialogue en réunion ne doit pas utiliser de module de tâches. Le module de tâche n’est pas invoqué dans un chat de réunion. Une URL de ressource externe est utilisée pour afficher la bulle de contenu dans une réunion. Vous pouvez utiliser la méthode `submitTask` pour soumettre des données dans un chat de réunion.

> [!NOTE]
> * Vous devez [invoquer la fonction submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour rejeter automatiquement après qu’un utilisateur prend une action dans la vue Web. Il s’agit d’une exigence pour la soumission de l’application. Pour plus d’informations, [Teams module de tâches SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
> * Si vous souhaitez que votre application prend en charge les utilisateurs anonymes, votre charge utile de demande d’invocateur initial doit s’appuyer `from.id` sur les métadonnées de demande dans `from` l’objet, et non `from.aadObjectId` sur les métadonnées de la demande. `from.id`est l’identifiant de `from.aadObjectId` l’utilisateur et est Azure Active Directory ID (AAD) de l’utilisateur. Pour plus d’informations, voir [l’utilisation de modules de tâches dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) [et créer et envoyer le module de tâches](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

#### <a name="share-to-stage"></a>Partager sur scène 

> [!NOTE]
> * Cette fonctionnalité est actuellement disponible en aperçu développeur uniquement.
> * Pour utiliser cette fonctionnalité, l’application doit prendre en charge un sidepanel en réunion.


Cette fonctionnalité permet aux développeurs de partager une application à l’étape de la réunion. En permettant de partager à l’étape de la réunion, les participants à la réunion peuvent collaborer en temps réel. 

Le contexte requis se trouve `meetingStage` dans le manifeste de l’application. Une condition préalable à cela est d’avoir le `meetingSidePanel` contexte. Cela permet le **bouton Partager** dans le sidepanel tel que spécifié dans l’image suivante :

  ![share_to_stage_during_meeting expérience](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

Le changement manifeste nécessaire pour activer cette capacité est le suivant : 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a>Après une réunion

Les configurations post-réunion et pré-réunion sont équivalentes.

## <a name="code-sample"></a>Exemple de code

|Nom de l’échantillon | Description | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| Extensibilité des réunions | Microsoft Teams’exemple d’extensibilité de réunion pour passer des jetons. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Bot de bulle de contenu de réunion | Microsoft Teams’exemple d’extensibilité de réunion pour interagir avec le bot bulle de contenu dans une réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Réunion SidePanel | Microsoft Teams’exemple d’extensibilité de la réunion pour iteracting avec le panneau latéral en réunion. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a>Voir aussi

* [Lignes directrices en réunion sur la conception du dialogue](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams d’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
