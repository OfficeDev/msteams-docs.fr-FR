---
title: Informations de base sur les bots
author: clearab
description: Comprendre les principes de base des bots dans Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3c4e707fa4677c2441f348e8d09ecf4428ef1296
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014501"
---
# <a name="bot-basics"></a>Informations de base sur les bots

Ce document fournit une introduction aux bots dans Microsoft Teams qui s’appuie sur l’article Sur le fonctionnement des [bots](https://aka.ms/how-bots-work) dans la documentation principale [de Bot Framework.](https://aka.ms/azure-bot-service-docs) La principale différence entre les bots développés pour Microsoft Teams et l’infrastructure de bot principale est dans les fonctionnalités fournies dans Teams.

## <a name="teams-activity-handlers"></a>Gérés d’activité Teams

Le handler d’activité Teams est dérivé du programme de gestion d’activité de Microsoft Bot Framework. Il a pour but d’approvisionnement toutes les activités Teams avant d’autoriser le traitement des activités non spécifiques à Teams.

Lorsqu’un bot pour Teams reçoit une activité, il est dirigé vers les *responsables de l’activité.* Toutes les activités sont acheminées via un seul handler de base appelé *« turn handler*». Le *handler turn appelle* le handler d’activité requis pour gérer les activités reçues. Le bot Teams est dérivé de la classe, qui est dérivée de la classe `TeamsActivityHandler` bot `ActivityHandler` Framework.

# <a name="c"></a>[C#](#tab/csharp)

Les bots sont créés à l’aide de Bot Framework. Si les bots reçoivent une activité de message, le turn handler reçoit une notification de cette activité entrante. Le handler turn envoie ensuite l’activité entrante au `OnMessageActivityAsync` handler d’activité. Dans Teams, cette fonctionnalité reste la même. Si le bot reçoit une activité de mise à jour de conversation, le turn handler reçoit une notification de cette activité entrante et envoie l’activité entrante à `OnConversationUpdateActivityAsync` . Le responsable de l’activité Teams vérifie d’abord s’il s’agit d’événements spécifiques à Teams. Si aucun événement n’est trouvé, il les transmet ensuite au programme de gestion d’activité de Bot Framework.

Dans la classe du handler d’activité Teams, il existe deux principaux de ces derniers, `OnConversationUpdateActivityAsync` et `OnInvokeActivityAsync` . `OnConversationUpdateActivityAsync` route toutes les activités de mise à jour de conversation et `OnInvokeActivityAsync` route toutes les activités d’appel teams.

Pour implémenter votre logique pour des responsables d’activité spécifiques à Teams, vous devez remplacer les méthodes dans votre bot, comme indiqué dans la section [logique du](#bot-logic) bot. Il n’existe aucune implémentation de base pour ces handlers, par conséquent, vous devez ajouter la logique que vous souhaitez dans votre substitution.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Les bots sont créés à l’aide de Bot Framework. Si les bots reçoivent une activité de message, le turn handler reçoit une notification de cette activité entrante. Le handler turn envoie ensuite l’activité entrante au `onMessage` handler d’activité. Dans Teams, cette fonctionnalité reste la même. Si le bot reçoit une activité de mise à jour de conversation, le turn handler reçoit une notification de cette activité entrante et envoie l’activité entrante à `dispatchConversationUpdateActivity` . Le responsable de l’activité Teams vérifie d’abord s’il y a des événements spécifiques à Teams. Si aucun événement n’est trouvé, il les transmet ensuite au programme de gestion d’activité de Bot Framework.

Dans la classe du handler d’activité Teams, il existe deux principaux de ces derniers, `dispatchConversationUpdateActivity` et `onInvokeActivity` . `dispatchConversationUpdateActivity` route toutes les activités de mise à jour de conversation et `onInvokeActivity` route toutes les activités d’appel teams.

Pour implémenter votre logique pour des responsables d’activité spécifiques à Teams, vous devez remplacer les méthodes dans votre bot, comme indiqué dans la section [logique du](#bot-logic) bot. Définissez votre logique de bot pour ces handlers, puis **assurez-vous d’appeler `next()` à la fin.** En `next()` appelant, vous vous assurez que le prochain handler s’exécute.

# <a name="python"></a>[Python](#tab/python)

Les bots sont créés à l’aide de Bot Framework. Si les bots reçoivent une activité de message, le turn handler reçoit une notification de cette activité entrante. Le handler turn envoie ensuite l’activité entrante au `on_message_activity` handler d’activité. Dans Teams, cette fonctionnalité reste la même. Si le bot reçoit une activité de mise à jour de conversation, le turn handler reçoit une notification de cette activité entrante et envoie l’activité entrante à `on_conversation_update_activity` . Le responsable de l’activité Teams vérifie d’abord s’il y a des événements spécifiques à Teams. Si aucun événement n’est trouvé, il les transmet ensuite au programme de gestion d’activité de Bot Framework.

Dans la classe du handler d’activité Teams, il existe deux principaux de ces derniers, `on_conversation_update_activity` et `on_invoke_activity` . `on_conversation_update_activity` route toutes les activités de mise à jour de conversation et `on_invoke_activity` route toutes les activités d’appel teams.

Pour implémenter votre logique pour des responsables d’activité spécifiques à Teams, vous devez remplacer les méthodes dans votre bot, comme indiqué dans la section [logique du](#bot-logic) bot. Il n’existe aucune implémentation de base pour ces handlers, par conséquent, vous devez ajouter la logique que vous souhaitez dans votre substitution.

---

## <a name="bot-logic"></a>Logique du bot

La logique du bot traite les activités entrantes à partir d’un ou plusieurs de vos canaux de bot et génère en réponse des activités sortantes. Cela est toujours vrai pour les bots dérivés de la classe de responsable d’activité Teams, qui vérifie d’abord les activités teams. Après avoir vérifié les activités teams, il transmet toutes les autres activités au programme de gestion d’activité de Bot Framework.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Principaux handlers Bot Framework

>[!NOTE]
> À *l’exception*  des activités des membres ajoutés et supprimés, tous les responsables d’activité décrits dans cette section continuent de fonctionner comme ils le font avec un bot autre que Teams.

Les responsables d’activité sont différents dans le contexte d’une équipe, où un nouveau membre est ajouté à l’équipe au lieu d’un thread de message.

La liste des handlers définis dans `ActivityHandler` inclut les suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| Tout type d’activité reçu | `OnTurnAsync` | Cette méthode appelle l’un des autres handlers, en fonction du type d’activité reçu. |
| Activité de message reçue | `OnMessageActivityAsync` | Cette méthode peut être overridden pour gérer une `Message` activité. |
| Activité de mise à jour de conversation reçue | `OnConversationUpdateActivityAsync` | Cette méthode appelle un handler si des membres autres que le bot ont rejoint ou quitté la conversation, lors d’une `ConversationUpdate` activité. |
| Les membres non-bot ont rejoint la conversation | `OnMembersAddedAsync` | Cette méthode peut être overridée pour gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `OnMembersRemovedAsync` | Cette méthode peut être utilisée pour gérer les membres quittant une conversation. |
| Activité d’événement reçue | `OnEventActivityAsync` | Cette méthode appelle un handler spécifique au type d’événement, sur une `Event` activité. |
| Activité d’événement de réponse de jeton reçue | `OnTokenResponseEventAsync` | Cette méthode peut être overridée pour gérer les événements de réponse de jeton. |
| Activité d’événement de réponse sans jeton reçue | `OnEventAsync` | Cette méthode peut être overridée pour gérer d’autres types d’événements. |
| Autre type d’activité reçu | `OnUnrecognizedActivityTypeAsync` | Cette méthode peut être overridée pour gérer tout type d’activité autrement non géré. |

#### <a name="teams-specific-activity-handlers"></a>Les personnes qui gèrent des activités spécifiques à Teams

Il étend la liste des handlers dans la `TeamsActivityHandler` section Core Bot Framework handlers pour inclure les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Cette méthode peut être overridée pour gérer un canal Teams en cours de création. Pour plus d’informations, [voir Canal créé dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Cette méthode peut être supprimée pour gérer un canal Teams en cours de suppression. Pour plus d’informations, [voir Canal supprimé dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) les événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Cette méthode peut être changée pour gérer un canal Teams renommé. Pour plus d’informations, [voir Canal renommé dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) les événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Cette méthode peut être changée pour gérer une équipe Teams renommée. Pour plus d’informations, voir [l’équipe renommée dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) les événements de [mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersAdded | `OnTeamsMembersAddedAsync` | Cette méthode appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler` . La méthode peut être overridée pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, voir les membres [de l’équipe ajoutés aux](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [événements de mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Cette méthode appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler` . La méthode peut être overridée pour gérer les membres quittant une équipe. Pour plus d’informations, voir [Membres d’équipe supprimés dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) les événements de [mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Les équipes appellent des activités

La liste des handlers d’activité Teams appelés à partir du `OnInvokeActivityAsync` handler d’activité Teams est la suivante :

| Types d’appel                    | Handler                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Cette méthode est invoquée lorsqu’une activité d’appel d’action de carte est reçue du connecteur. |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Cette méthode est invoquée lorsqu’une carte de consentement de fichier est acceptée par l’utilisateur. |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Cette méthode est invoquée lorsqu’une activité de carte de consentement de fichier est reçue du connecteur. |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Cette méthode est invoquée lorsqu’une carte de consentement de fichier est refusée par l’utilisateur. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Cette méthode est invoquée lorsqu’une activité d’action de carte de connecteur O365 est reçue du connecteur. |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Cette méthode est invoquée lorsqu’une activité de vérification de l’état signIn est reçue du connecteur. |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Cette méthode peut être override dans une classe dérivée pour fournir une logique lorsqu’un module de tâche est extrait. |
| tâche/soumission                     | `OnTeamsTaskModuleSubmitAsync`       | Cette méthode peut être overridée dans une classe dérivée pour fournir une logique lorsqu’un module de tâche est envoyé. |

Les activités d’appel répertoriées dans cette section sont pour les bots de conversation dans Teams. Le SDK Bot Framework prend également en charge les activités d’appel spécifiques aux extensions de messagerie. Pour plus d’informations, [voir Quelles sont les extensions de messagerie](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Principaux handlers Bot Framework

>[!NOTE]
> À *l’exception*  des activités des membres ajoutés et supprimés, tous les responsables d’activité décrits dans cette section continuent de fonctionner comme ils le font avec un bot autre que Teams.

Les responsables d’activité sont différents dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe au lieu d’un thread de message.

La liste des handlers définis dans `ActivityHandler` inclut les suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| Tout type d’activité reçu | `onTurn` | Cette méthode appelle l’un des autres handlers, en fonction du type d’activité reçu. |
| Activité de message reçue | `onMessage` | Cette méthode permet de gérer une `Message` activité. |
| Activité de mise à jour de conversation reçue | `onConversationUpdate` | Cette méthode appelle un handler si des membres autres que le bot ont rejoint ou quitté la conversation, lors d’une `ConversationUpdate` activité. |
| Les membres non-bot ont rejoint la conversation | `onMembersAdded` | Cette méthode permet de gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `onMembersRemoved` | Cette méthode permet de gérer les membres quittant une conversation. |
| Activité d’événement reçue | `onEvent` | Cette méthode appelle un handler spécifique au type d’événement, sur une `Event` activité. |
| Activité d’événement de réponse de jeton reçue | `onTokenResponseEvent` | Cette méthode permet de gérer les événements de réponse de jeton. |
| Autre type d’activité reçu | `onUnrecognizedActivityType` | Cette méthode permet de gérer tout type d’activité autrement non géré. |

#### <a name="teams-specific-activity-handlers"></a>Les personnes qui gèrent des activités spécifiques à Teams

Il étend la liste des handlers dans la `TeamsActivityHandler` section Core Bot Framework handlers pour inclure les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Cette méthode peut être overridée pour gérer un canal Teams en cours de création. Pour plus d’informations, [voir Canal créé dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Cette méthode peut être supprimée pour gérer un canal Teams en cours de suppression. Pour plus d’informations, [voir Canal supprimé dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) les événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Cette méthode peut être changée pour gérer un canal Teams renommé. Pour plus d’informations, [voir Canal renommé dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) les événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Cette méthode peut être changée pour gérer une équipe Teams renommée. Pour plus d’informations, voir [l’équipe renommée dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) les événements de [mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersAdded | `OnTeamsMembersAddedAsync` | Cette méthode appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler` . La méthode peut être overridée pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, voir les membres [de l’équipe ajoutés aux](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [événements de mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Cette méthode appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler` . La méthode peut être overridée pour gérer les membres quittant une équipe. Pour plus d’informations, voir [Membres d’équipe supprimés dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) les événements de [mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |

#### <a name="teams-invoke-activities"></a>Les équipes appellent des activités

La liste des sous-traites d’activité Teams appelées à partir du handler d’activité `onInvokeActivity` Teams est la suivante :

| Types d’appel                    | Handler                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Cette méthode est invoquée lorsqu’une activité d’appel d’action de carte est reçue du connecteur. |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Cette méthode est invoquée lorsqu’une carte de consentement de fichier est acceptée par l’utilisateur. |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Cette méthode est invoquée lorsqu’une activité de carte de consentement de fichier est reçue du connecteur. |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Cette méthode est invoquée lorsqu’une carte de consentement de fichier est refusée par l’utilisateur. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Cette méthode est invoquée lorsqu’une activité d’action de carte de connecteur O365 est reçue du connecteur. |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Cette méthode est invoquée lorsqu’une activité de vérification de l’état signIn est reçue du connecteur. |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Cette méthode peut être overridée dans une classe dérivée pour fournir une logique lorsqu’un module de tâche est extrait. |
| tâche/soumission                     | `handleTeamsTaskModuleSubmit`       | Cette méthode peut être overridée dans une classe dérivée pour fournir une logique lorsqu’un module de tâche est envoyé. |

Les activités d’appel répertoriées dans cette section sont pour les bots de conversation dans Teams. Le SDK Bot Framework prend également en charge les activités d’appel spécifiques aux extensions de messagerie. Pour plus d’informations, [voir Quelles sont les extensions de messagerie](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Principaux handlers Bot Framework

>[!NOTE]
> À *l’exception*  des activités des membres ajoutés et supprimés, tous les responsables d’activité décrits dans cette section continuent de fonctionner comme ils le font avec un bot autre que Teams.

Les responsables d’activité sont différents dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe au lieu d’un thread de message.

La liste des handlers définis dans `ActivityHandler` inclut les suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| Tout type d’activité reçu | `on_turn` | Cette méthode appelle l’un des autres handlers, en fonction du type d’activité reçue. |
| Activité de message reçue | `on_message_activity` | Cette méthode peut être overridden pour gérer une `Message` activité. |
| Activité de mise à jour de conversation reçue | `on_conversation_update_activity` | Cette méthode appelle un handler si des membres autres que le bot rejoignent ou quittent la conversation. |
| Les membres non-bot ont rejoint la conversation | `on_members_added_activity` | Cette méthode peut être override pour gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `on_members_removed_activity` | Cette méthode peut être overridée pour gérer les membres quittant une conversation. |
| Activité d’événement reçue | `on_event_activity` | Cette méthode appelle un handler spécifique au type d’événement. |
| Activité d’événement de réponse de jeton reçue | `on_token_response_event` | Cette méthode peut être overridée pour gérer les événements de réponse de jeton. |
| Activité d’événement de réponse sans jeton reçue | `on_event` | Cette méthode peut être overridée pour gérer d’autres types d’événements. |
| Autres types d’activité reçus | `on_unrecognized_activity_type` | Cette méthode peut être overridée pour gérer tout type d’activité qui n’est pas géré. |

#### <a name="teams-specific-activity-handlers"></a>Les personnes qui gèrent des activités spécifiques à Teams

La liste des handlers de la section Core Bot Framework handlers s’étend pour `TeamsActivityHandler` inclure les éléments suivants :

| Événement | Handler | Description |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Cette méthode peut être overridée pour gérer un canal Teams en cours de création. Pour plus d’informations, [voir Canal créé dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events) |
| channelDeleted | `on_teams_channel_deleted` | Cette méthode peut être supprimée pour gérer un canal Teams en cours de suppression. Pour plus d’informations, [voir Canal supprimé dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) les événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| channelRenamed | `on_teams_channel_renamed` | Cette méthode peut être changée pour gérer un canal Teams renommé. Pour plus d’informations, [voir Canal renommé dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) les événements de mise à jour de [conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` Cette méthode peut être changée pour gérer une équipe Teams renommée. Pour plus d’informations, voir [l’équipe renommée dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) les événements de [mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersAdded | `on_teams_members_added` | Cette méthode appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler` . La méthode peut être overridée pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, voir les membres [de l’équipe ajoutés aux](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [événements de mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|
| MembersRemoved | `on_teams_members_removed` | Cette méthode appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler` . La méthode peut être overridée pour gérer les membres quittant une équipe. Pour plus d’informations, voir [Membres d’équipe supprimés dans](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) les événements de [mise à jour de conversation.](https://aka.ms/azure-bot-subscribe-to-conversation-events)|

#### <a name="teams-invoke-activities"></a>Les équipes appellent des activités

La liste des sous-traites d’activité Teams appelées à partir du handler d’activité `on_invoke_activity` Teams est la suivante :

| Types d’appel                    | Handler                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Cette méthode est invoquée lorsqu’une activité d’appel d’action de carte est reçue du connecteur. |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Cette méthode est invoquée lorsqu’une carte de consentement de fichier est acceptée par l’utilisateur. |
| fileConsent/invoke              | `on_teams_file_consent`            | Cette méthode est invoquée lorsqu’une activité de carte de consentement de fichier est reçue du connecteur. |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Cette méthode est invoquée lorsqu’une carte de consentement de fichier est refusée par l’utilisateur. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Cette méthode est invoquée lorsqu’une activité d’action de carte de connecteur O365 est reçue du connecteur. |
| signin/verifyState              | `on_teams_signin_verify_state`      | Cette méthode est invoquée lorsqu’une activité de vérification de l’état signIn est reçue du connecteur. |
| task/fetch                      | `on_teams_task_module_fetch`        | Cette méthode peut être overridée dans une classe dérivée pour fournir une logique lorsqu’un module de tâche est extrait. |
| tâche/envoyer                     | `on_teams_task_module_submit`       | Cette méthode peut être overridée dans une classe dérivée pour fournir une logique lorsqu’un module de tâche est envoyé. |

Les activités d’appel répertoriées dans cette section sont pour les bots de conversation dans Teams. Le SDK Bot Framework prend également en charge les activités d’appel spécifiques aux extensions de messagerie. Pour plus d’informations, [voir Quelles sont les extensions de messagerie](https://aka.ms/azure-bot-what-are-messaging-extensions).

---
