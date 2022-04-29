---
title: Gestionnaire d'activité du robot
author: surbhigupta
description: Comprendre les gestionnaires d’activité de bot dans Teams.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: anclear
keywords: événement de canal de consentement de la carte de bot du gestionnaire d’activités
ms.openlocfilehash: e975279276e8b8d4f3b934144b6cb1c3a7850424
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65112003"
---
# <a name="bot-activity-handlers"></a>Gestionnaire d'activité du robot

Ce document s’appuie sur l’article sur le [fonctionnement des bots](https://aka.ms/how-bots-work) dans la [documentation principale de Bot Framework](https://aka.ms/azure-bot-service-docs). La principale différence entre les bots développés pour Microsoft Teams et le framework bot principal réside dans les fonctionnalités fournies dans Teams.

Pour organiser la logique conversationnelle de votre bot, un gestionnaire d’activités est utilisé. Les activités sont gérées de deux manières à l’aide de gestionnaires d’activités Teams et de logique de bot. Le gestionnaire d’activités Teams ajoute la prise en charge des événements et interactions spécifiques à Microsoft Teams. L’objet bot contient le raisonnement conversationnel ou la logique d’un tour et expose un gestionnaire de tours, qui est la méthode qui peut accepter les activités entrantes de l’adaptateur de bot.

## <a name="teams-activity-handlers"></a>Gestionnaires d’activités Microsoft Teams

Teams gestionnaire d’activités est dérivé du gestionnaire d’activités de Microsoft Bot Framework. Il achemine toutes les activités Teams avant d’autoriser la gestion des activités non Teams spécifiques.

Lorsqu’un bot pour Microsoft Teams reçoit une activité, il la transmet à ses gestionnaires d’activités. Toutes les activités sont routées via un gestionnaire de base appelé gestionnaire de tour. Le gestionnaire de tours appelle le gestionnaire d’activités requis pour gérer le type d’activité reçu. Le bot Teams est dérivé de la `TeamsActivityHandler` classe, qui est dérivée de la classe bot `ActivityHandler` framework.

# <a name="c"></a>[C#](#tab/csharp)

Les bots sont créés à l’aide de Bot Framework. Si les bots reçoivent une activité de message, le gestionnaire de tours reçoit une notification de cette activité entrante. Le gestionnaire de tours envoie ensuite l’activité entrante au gestionnaire d’activités `OnMessageActivityAsync`. Dans Teams, cette fonctionnalité reste la même. Si le bot reçoit une activité de mise à jour de conversation, le gestionnaire de tours reçoit une notification de cette activité entrante et envoie l’activité entrante à `OnConversationUpdateActivityAsync`. Le gestionnaire d’activités Teams vérifie d’abord les événements spécifiques Teams. Si aucun événement n’est trouvé, il les transmet ensuite au gestionnaire d’activités de Bot Framework.

Dans la classe de gestionnaire d’activités Teams, il existe deux principaux gestionnaires d’activités Teams, `OnConversationUpdateActivityAsync` et `OnInvokeActivityAsync`. `OnConversationUpdateActivityAsync` achemine toutes les activités de mise à jour de conversation et `OnInvokeActivityAsync` achemine toutes les activités d’appel Teams.

Pour implémenter votre logique pour Teams gestionnaires d’activités spécifiques, vous devez remplacer les méthodes de votre bot, comme indiqué dans la section [logique du bot](#bot-logic). Il n’existe aucune implémentation de base pour ces gestionnaires. Par conséquent, vous devez ajouter la logique souhaitée dans votre remplacement.

Extraits de code pour les gestionnaires d’activités Teams :

`OnTeamsChannelCreatedAsync`

```csharp

protected override Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelDeletedAsync`

```csharp

protected override Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelRenamedAsync`

```csharp

protected override Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsTeamRenamedAsync`

```csharp

protected override Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsMembersAddedAsync`

```csharp

protected override Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsMembersRemovedAsync`

```csharp

protected override Task OnTeamsMembersRemovedAsync(IList<TeamsChannelAccount> teamsMembersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken);
  {
   // Code logic here
  }
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Les bots sont créés à l’aide de Bot Framework. Si les bots reçoivent une activité de message, le gestionnaire de tours reçoit une notification de cette activité entrante. Le gestionnaire de tours envoie ensuite l’activité entrante au gestionnaire d’activités `onMessage`. Dans Teams, cette fonctionnalité reste la même. Si le bot reçoit une activité de mise à jour de conversation, le gestionnaire de tours reçoit une notification de cette activité entrante et envoie l’activité entrante à `dispatchConversationUpdateActivity`. Le gestionnaire d’activités Teams vérifie d’abord les événements spécifiques Teams. Si aucun événement n’est trouvé, il les transmet ensuite au gestionnaire d’activités de Bot Framework.

Dans la classe de gestionnaire d’activités Teams, il existe deux principaux gestionnaires d’activités Teams, `dispatchConversationUpdateActivity` et `onInvokeActivity`. `dispatchConversationUpdateActivity` achemine toutes les activités de mise à jour de conversation et `onInvokeActivity` achemine toutes les activités d’appel Teams.

Pour implémenter votre logique pour Teams gestionnaires d’activités spécifiques, vous devez remplacer les méthodes de votre bot, comme indiqué dans la section [logique du bot](#bot-logic). Définissez votre logique de bot pour ces gestionnaires, puis veillez à appeler `next()` à la fin. En appelant `next()` vous assurez que le gestionnaire suivant s’exécute.

Extraits de code pour les gestionnaires d’activités Teams :

`OnTeamsChannelCreatedAsync`

```javascript

onTeamsChannelCreated(async (channelInfo, teamInfo, context, next) => {
       // code for handling
        await next()
    });
```

`OnTeamsChannelDeletedAsync`

```javascript

onTeamsChannelDeleted(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsChannelRenamedAsync`

```javascript

onTeamsChannelRenamed(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsTeamRenamedAsync`

```javascript

onTeamsTeamRenamedAsync(async (teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsMembersAddedAsync`

```javascript

onTeamsMembersAdded(async (membersAdded, teamInfo, context, next) => {
       // code for handling
    await next();
    });
```

`OnTeamsMembersRemovedAsync`

```javascript

onTeamsMembersRemoved(async (membersRemoved, teamInfo, context, next) => {
       // code for handling
    await next();
    });
```

# <a name="python"></a>[Python](#tab/python)

Les bots sont créés à l’aide de Bot Framework. Si les bots reçoivent une activité de message, le gestionnaire de tours reçoit une notification de cette activité entrante. Le gestionnaire de tours envoie ensuite l’activité entrante au gestionnaire d’activités `on_message_activity`. Dans Teams, cette fonctionnalité reste la même. Si le bot reçoit une activité de mise à jour de conversation, le gestionnaire de tours reçoit une notification de cette activité entrante et envoie l’activité entrante à `on_conversation_update_activity`. Le gestionnaire d’activités Teams vérifie d’abord les événements spécifiques Teams. Si aucun événement n’est trouvé, il les transmet ensuite au gestionnaire d’activités de Bot Framework.

Dans la classe de gestionnaire d’activités Teams, il existe deux principaux gestionnaires d’activités Teams, `on_conversation_update_activity` et `on_invoke_activity`. `on_conversation_update_activity`route toutes les activités de mise à jour de conversation et `on_invoke_activity` route toutes les activités Teams appeler.

Pour implémenter votre logique pour Teams gestionnaires d’activités spécifiques, vous devez remplacer les méthodes de votre bot, comme indiqué dans la section [logique du bot](#bot-logic). Il n’existe aucune implémentation de base pour ces gestionnaires. Par conséquent, vous devez ajouter la logique souhaitée dans votre remplacement.

---

## <a name="bot-logic"></a>Logique de bot

La logique du bot traite les activités entrantes à partir d’un ou plusieurs de vos canaux de bot et génère en réponse des activités sortantes. Cela est toujours vrai pour les bots dérivés de la classe de gestionnaire d’activités Teams, qui vérifie d’abord les activités Teams. Après avoir vérifié Teams activités, elle transmet toutes les autres activités au gestionnaire d’activités de Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Principaux gestionnaires Bot Framework

>[!NOTE]
>
>* À l’exception des activités des membres **ajoutés** et **supprimés**, tous les gestionnaires d’activités décrits dans cette section continuent de fonctionner comme ils le font avec un bot non Teams.
>* La méthode `onInstallationUpdateActivityAsync()` est utilisée pour obtenir les paramètres régionaux de Microsoft Teams lors de l’ajout du bot à Microsoft Teams.

Les gestionnaires d’activités sont différents dans le contexte d’une équipe, où un nouveau membre est ajouté à l’équipe au lieu d’un thread de message.

La liste des gestionnaires définis dans `ActivityHandler` inclut les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| Tout type d’activité reçu | `OnTurnAsync` | Cette méthode appelle l’un des autres gestionnaires, en fonction du type d’activité reçue. |
| Activité de message reçue | `OnMessageActivityAsync` | Cette méthode peut être remplacée pour gérer une `Message` activité. |
| Activité de mise à jour de conversation reçue | `OnConversationUpdateActivityAsync` | Cette méthode appelle un gestionnaire si des membres autres que le bot ont rejoint ou quitté la conversation, sur une `ConversationUpdate` activité. |
| Les membres non-bot ont rejoint la conversation | `OnMembersAddedAsync` | Cette méthode peut être remplacée pour gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `OnMembersRemovedAsync` | Cette méthode peut être substituée pour gérer les membres quittant une conversation. |
| Activité d’événement reçue | `OnEventActivityAsync` | Cette méthode appelle un gestionnaire spécifique au type d’événement, sur une `Event` activité. |
| Activité d’événement de réponse de jeton reçue | `OnTokenResponseEventAsync` | Cette méthode peut être remplacée pour gérer les événements de réponse de jeton. |
| Activité d’événement sans réponse de jeton reçue | `OnEventAsync` | Cette méthode peut être remplacée pour gérer d’autres types d’événements. |
| Autre type d’activité reçu | `OnUnrecognizedActivityTypeAsync` | Cette méthode peut être substituée pour gérer n’importe quel type d’activité autrement non géré. |

#### <a name="teams-specific-activity-handlers"></a>Gestionnaires d’activités Microsoft Teams

L’extension `TeamsActivityHandler` de la liste des gestionnaires dans la section principale des gestionnaires Bot Framework inclut les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Cette méthode peut être substituée pour gérer un canal Teams en cours de création. Pour plus d’informations, consultez [le canal créé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| ChannelDeleted | `OnTeamsChannelDeletedAsync` | Cette méthode peut être remplacée pour gérer un canal Teams en cours de suppression. Pour plus d’informations, consultez [le canal supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Cette méthode peut être remplacée pour gérer un canal Teams renommé. Pour plus d’informations, consultez [le canal renommé dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Cette méthode peut être remplacée pour gérer une équipe Teams renommée. Pour plus d’informations, consultez [l’équipe renommée dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Cette méthode appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler`. La méthode peut être remplacée pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, consultez [les membres de l’équipe ajoutés](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) aux [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Cette méthode appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler`. La méthode peut être remplacée pour gérer les membres quittant une équipe. Pour plus d’informations, consultez [les membres de l’équipe supprimés](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Teams appeler des activités

La liste des gestionnaires d’activités Teams appelés à partir du `OnInvokeActivityAsync` gestionnaire d’activités Teams inclut les éléments suivants :

| Appeler des types                    | Handler                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Cette méthode est appelée lorsqu’une activité d’appel d’action de carte est reçue du connecteur. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Cette méthode est appelée lorsqu’une carte de consentement de fichier est acceptée par l’utilisateur. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Cette méthode est appelée lorsqu’une activité de carte de consentement de fichier est reçue du connecteur. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Cette méthode est appelée lorsqu’une carte de consentement de fichier est refusée par l’utilisateur. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Cette méthode est appelée lorsqu’une activité d’action de carte de connecteur Office 365 est reçue du connecteur. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Cette méthode est appelée lorsqu’une activité d’état de vérification signIn est reçue du connecteur. |
| tâche/extraction                      | `OnTeamsTaskModuleFetchAsync`        | Cette méthode peut être substituée dans une classe dérivée pour fournir une logique lors de l’extraction d’un module de tâche. |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Cette méthode peut être substituée dans une classe dérivée pour fournir une logique lors de l’envoi d’un module de tâche. |

Les activités d’appel répertoriées dans cette section concernent les bots conversationnels dans Teams. Le Kit de développement logiciel (SDK) Bot Framework prend également en charge les activités d’appel spécifiques aux extensions de message. Pour plus d’informations, consultez [les extensions de message](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Principaux gestionnaires Bot Framework

>[!NOTE]
> À l’exception des activités des membres **ajoutés** et **supprimés**, tous les gestionnaires d’activités décrits dans cette section continuent de fonctionner comme ils le font avec un bot non Teams.

Les gestionnaires d’activités sont différents dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe au lieu d’un thread de message.

La liste des gestionnaires définis dans `ActivityHandler` inclut les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| Tout type d’activité reçu | `onTurn` | Cette méthode appelle l’un des autres gestionnaires, en fonction du type d’activité reçue. |
| Activité de message reçue | `onMessage` | Cette méthode permet de gérer une `Message` activité. |
| Activité de mise à jour de conversation reçue | `onConversationUpdate` | Cette méthode appelle un gestionnaire si des membres autres que le bot ont rejoint ou quitté la conversation, sur une `ConversationUpdate` activité. |
| Les membres non-bot ont rejoint la conversation | `onMembersAdded` | Cette méthode permet de gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `onMembersRemoved` | Cette méthode permet de gérer les membres quittant une conversation. |
| Activité d’événement reçue | `onEvent` | Cette méthode appelle un gestionnaire spécifique au type d’événement, sur une `Event` activité. |
| Activité d’événement de réponse de jeton reçue | `onTokenResponseEvent` | Cette méthode permet de gérer les événements de réponse de jeton. |
| Autre type d’activité reçu | `onUnrecognizedActivityType` | Cette méthode permet de gérer n’importe quel type d’activité autrement non géré. |

#### <a name="teams-specific-activity-handlers"></a>Gestionnaires d’activités Microsoft Teams

L’extension `TeamsActivityHandler` de la liste des gestionnaires dans la section principale des gestionnaires Bot Framework inclut les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Cette méthode peut être substituée pour gérer un canal Teams en cours de création. Pour plus d’informations, consultez [le canal créé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| ChannelDeleted | `OnTeamsChannelDeletedAsync` | Cette méthode peut être remplacée pour gérer un canal Teams en cours de suppression. Pour plus d’informations, consultez [le canal supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Cette méthode peut être remplacée pour gérer un canal Teams renommé. Pour plus d’informations, consultez [le canal renommé dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Cette méthode peut être remplacée pour gérer une équipe Teams renommée. Pour plus d’informations, consultez [l’équipe renommée dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Cette méthode appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler`. La méthode peut être remplacée pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, consultez [les membres de l’équipe ajoutés](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) aux [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Cette méthode appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler`. La méthode peut être remplacée pour gérer les membres quittant une équipe. Pour plus d’informations, consultez [les membres de l’équipe supprimés](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |

#### <a name="teams-invoke-activities"></a>Teams appeler des activités

La liste des gestionnaires d’activités Teams appelés à partir du `onInvokeActivity` gestionnaire d’activités Teams inclut les éléments suivants :

| Appeler des types                    | Handler                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Cette méthode est appelée lorsqu’une activité d’appel d’action de carte est reçue du connecteur. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Cette méthode est appelée lorsqu’une carte de consentement de fichier est acceptée par l’utilisateur. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Cette méthode est appelée lorsqu’une activité de carte de consentement de fichier est reçue du connecteur. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Cette méthode est appelée lorsqu’une carte de consentement de fichier est refusée par l’utilisateur. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Cette méthode est appelée lorsqu’une activité d’action de carte de connecteur Office 365 est reçue du connecteur. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Cette méthode est appelée lorsqu’une activité d’état de vérification signIn est reçue du connecteur. |
| tâche/extraction                      | `handleTeamsTaskModuleFetch`        | Cette méthode peut être substituée dans une classe dérivée pour fournir une logique lors de l’extraction d’un module de tâche. |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Cette méthode peut être substituée dans une classe dérivée pour fournir une logique lors de l’envoi d’un module de tâche. |

Les activités d’appel répertoriées dans cette section concernent les bots conversationnels dans Teams. Le Kit de développement logiciel (SDK) Bot Framework prend également en charge les activités d’appel spécifiques aux extensions de message. Pour plus d’informations, consultez [les extensions de message](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Principaux gestionnaires Bot Framework

>[!NOTE]
> À l’exception des activités des membres **ajoutés** et **supprimés**, tous les gestionnaires d’activités décrits dans cette section continuent de fonctionner comme ils le font avec un bot non Teams.

Les gestionnaires d’activités sont différents dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe au lieu d’un thread de message.

La liste des gestionnaires définis dans `ActivityHandler` inclut les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| Tout type d’activité reçu | `on_turn` | Cette méthode appelle l’un des autres gestionnaires, en fonction du type d’activité reçue. |
| Activité de message reçue | `on_message_activity` | Cette méthode peut être remplacée pour gérer une `Message` activité. |
| Activité de mise à jour de conversation reçue | `on_conversation_update_activity` | Cette méthode appelle un gestionnaire si des membres autres que le bot rejoignent ou quittent la conversation. |
| Les membres non-bot ont rejoint la conversation | `on_members_added_activity` | Cette méthode peut être remplacée pour gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `on_members_removed_activity` | Cette méthode peut être substituée pour gérer les membres quittant une conversation. |
| Activité d’événement reçue | `on_event_activity` | Cette méthode appelle un gestionnaire spécifique au type d’événement. |
| Activité d’événement de réponse de jeton reçue | `on_token_response_event` | Cette méthode peut être remplacée pour gérer les événements de réponse de jeton. |
| Activité d’événement sans réponse de jeton reçue | `on_event` | Cette méthode peut être remplacée pour gérer d’autres types d’événements. |
| Autres types d’activités reçus | `on_unrecognized_activity_type` | Cette méthode peut être substituée pour gérer n’importe quel type d’activité qui n’est pas géré. |

#### <a name="teams-specific-activity-handlers"></a>Gestionnaires d’activités Microsoft Teams

La `TeamsActivityHandler` liste des gestionnaires s’étend à partir de la section principale des gestionnaires Bot Framework pour inclure les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Cette méthode peut être substituée pour gérer un canal Teams en cours de création. Pour plus d’informations, consultez [le canal créé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| ChannelDeleted | `on_teams_channel_deleted` | Cette méthode peut être remplacée pour gérer un canal Teams en cours de suppression. Pour plus d’informations, consultez [le canal supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `on_teams_channel_renamed` | Cette méthode peut être remplacée pour gérer un canal Teams renommé. Pour plus d’informations, consultez [le canal renommé dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;`Cette méthode peut être remplacée pour gérer une équipe Teams renommée. Pour plus d’informations, consultez [l’équipe renommée dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `on_teams_members_added` | Cette méthode appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler`. La méthode peut être remplacée pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, consultez [les membres de l’équipe ajoutés](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) aux [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `on_teams_members_removed` | Cette méthode appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler`. La méthode peut être remplacée pour gérer les membres quittant une équipe. Pour plus d’informations, consultez [les membres de l’équipe supprimés](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Teams appeler des activités

La liste des gestionnaires d’activités Teams appelés à partir du `on_invoke_activity` gestionnaire d’activités Teams inclut les éléments suivants :

| Appeler des types                    | Handler                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Cette méthode est appelée lorsqu’une activité d’appel d’action de carte est reçue du connecteur. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Cette méthode est appelée lorsqu’une carte de consentement de fichier est acceptée par l’utilisateur. |
| fileConsent/invoke              | `on_teams_file_consent`            | Cette méthode est appelée lorsqu’une activité de carte de consentement de fichier est reçue du connecteur. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Cette méthode est appelée lorsqu’une carte de consentement de fichier est refusée par l’utilisateur. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Cette méthode est appelée lorsqu’une activité d’action de carte de connecteur Office 365 est reçue du connecteur. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Cette méthode est appelée lorsqu’une activité d’état de vérification signIn est reçue du connecteur. |
| tâche/extraction                      | `on_teams_task_module_fetch`        | Cette méthode peut être substituée dans une classe dérivée pour fournir une logique lors de l’extraction d’un module de tâche. |
| task/submit                     | `on_teams_task_module_submit`       | Cette méthode peut être substituée dans une classe dérivée pour fournir une logique lors de l’envoi d’un module de tâche. |

Les activités d’appel répertoriées dans cette section concernent les bots conversationnels dans Teams. Le Kit de développement logiciel (SDK) Bot Framework prend également en charge les activités d’appel spécifiques aux extensions de message. Pour plus d’informations, consultez [les extensions de message](https://aka.ms/azure-bot-what-are-messaging-extensions).

---

---

Maintenant que vous vous êtes familiarisé avec les gestionnaires d’activités de bot, voyons comment les bots se comportent différemment en fonction de la conversation et des messages qu’il reçoit ou envoie.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Concepts de base d’une conversation](~/bots/how-to/conversations/conversation-basics.md)
