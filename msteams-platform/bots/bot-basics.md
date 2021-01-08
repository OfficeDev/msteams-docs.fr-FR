---
title: Notions de base sur les robots
author: clearab
description: Maîtrisez les notions de base des robots dans Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 43dd351b30fdba3435d39aca43aae0f2de00ed24
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731957"
---
# <a name="bot-basics"></a>Notions de base sur les robots

Il s’agit d’une introduction qui s’appuie sur l’article [How bots Work](https://aka.ms/how-bots-work) in the Core [bot Framework documentation](https://aka.ms/azure-bot-service-docs). Vous trouverez peut-être cet article, ainsi que les autres Articles de la section *concepts* , utiles.

La principale différence dans les robots développés pour Microsoft teams réside dans la façon dont les activités sont gérées. Le gestionnaire d’activité Microsoft teams dérive du gestionnaire d’activité de l’infrastructure bot pour acheminer toutes les activités de teams avant d’autoriser le traitement de toutes les activités spécifiques non liées à l’équipe.

## <a name="teams-activity-handlers"></a>Gestionnaires d’activités de teams

Lorsqu’un bot pour Microsoft Teams reçoit une activité, il la transmet à ses *gestionnaires d’activités*. En coulisses, un gestionnaire de base (*gestionnaire de tours*) assure l’acheminement de toutes les activités. Le *Gestionnaire Turn* appelle le gestionnaire d’activités requis pour gérer le type d’activité reçu. Lorsqu’un bot conçu pour Microsoft teams diffère, il est dérivé de `TeamsActivityHandler` la classe qui est dérivée de la classe de l’infrastructure bot `ActivityHandler` .

# <a name="c"></a>[C#](#tab/csharp)

Comme avec tout robot créé à l’aide de Microsoft bot Framework, si le bot reçoit une activité de message, le gestionnaire de tournage voit cette activité entrante et l’envoie au `OnMessageActivityAsync` Gestionnaire d’activité. Dans Teams, cette fonctionnalité reste identique. Si le bot reçoit une activité de mise à jour de conversation, le gestionnaire de tournage voit cette activité entrante et l’envoie au `OnConversationUpdateActivityAsync` . Gestionnaire d’activités de *teams* qui vérifieront d’abord les événements spécifiques des équipes et les transmettra au gestionnaire d’activités de l’infrastructure bot si aucun n’est trouvé.

Dans la classe de gestionnaire d’activités de teams, il existe deux gestionnaires d’activité de teams principaux, `OnConversationUpdateActivityAsync` qui acheminent toutes les activités de mise à jour de conversation et `OnInvokeActivityAsync` qui achemine toutes les équipes.

Pour implémenter votre logique pour les gestionnaires d’activités spécifiques à Teams, vous devez remplacer ces méthodes dans votre bot, comme illustré dans la section [logique bot](#bot-logic) ci-dessous. Pour chacun de ces gestionnaires, il n’existe pas d’implémentation de base, il vous suffit d’ajouter la logique de votre choix dans votre substitution.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Comme avec tout robot créé à l’aide de Microsoft bot Framework, si le bot reçoit une activité de message, le gestionnaire de tournage voit cette activité entrante et l’envoie au `onMessage` Gestionnaire d’activité. Dans Teams, cette fonctionnalité reste identique. Si le bot reçoit une activité de mise à jour de conversation, le gestionnaire de tournage voit cette activité entrante et l’envoie au `dispatchConversationUpdateActivity` . Gestionnaire d’activités de *teams* qui vérifieront d’abord les événements spécifiques des équipes et les transmettra au gestionnaire d’activités de l’infrastructure bot si aucun n’est trouvé.

Dans la classe de gestionnaire d’activités de teams, il existe deux gestionnaires d’activité de teams principaux, `dispatchConversationUpdateActivity` qui acheminent toutes les activités de mise à jour de conversation et `onInvokeActivity` qui achemine toutes les équipes.

Pour implémenter votre logique pour les gestionnaires d’activités spécifiques à Teams, vous devez remplacer ces méthodes dans votre bot comme indiqué dans la section de [logique bot](#bot-logic) . Pour chacun de ces gestionnaires, définissez votre logique de robot, puis **Veillez à appeler `next()` à la fin**. En vous appelant, `next()` Assurez-vous que le gestionnaire suivant s’exécute.

# <a name="python"></a>[Python](#tab/python)

Les robots sont créés à l’aide de Microsoft bot Framework, si ces derniers reçoivent une activité de message, puis le gestionnaire Turn reçoit une notification de cette activité entrante. Le gestionnaire de tournage envoie ensuite l’activité entrante au `on_message_activity` Gestionnaire d’activité. Dans Teams, cette fonctionnalité reste identique. Si le bot reçoit une activité de mise à jour de conversation, le gestionnaire Turn reçoit une notification de cette activité entrante et envoie l’activité entrante à `on_conversation_update_activity` . Le gestionnaire d’activités teams vérifiera d’abord les événements spécifiques de teams. Si aucun événement n’est trouvé, il les transmet ensuite au gestionnaire d’activité de l’infrastructure bot.

Dans la classe de gestionnaire d’activités de teams, il existe deux gestionnaires d’activité de teams principaux, `on_conversation_update_activity` et `on_invoke_activity` . `on_conversation_update_activity` achemine toutes les activités de mise à jour de conversation et `on_invoke_activity` achemine toutes les activités appel à des équipes.

Pour implémenter votre logique pour les gestionnaires d’activités spécifiques à Teams, vous devez remplacer ces méthodes dans votre bot, comme illustré dans la section de [logique bot](#bot-logic) . Il n’existe pas d’implémentation de base pour ces gestionnaires, par conséquent, vous devez ajouter la logique souhaitée dans votre remplacement.

---

## <a name="bot-logic"></a>Logique de robot

La logique du robot traite les activités entrantes à partir d’un ou de plusieurs de vos canaux de robots et génère des activités sortantes en réponse.  Cela est toujours vrai pour les robots dérivés de la classe de gestionnaire d’activités Teams, qui vérifie d’abord les activités Teams, puis passe toutes les autres activités au gestionnaire d’activité de l’infrastructure de robot.

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Gestionnaires d’infrastructure de robot principal

Tous les gestionnaires d’activité décrits ci-dessous continueront de fonctionner comme avec un robot non Teams, à l’exception de la gestion des membres *ajoutés* et des activités *supprimées* , celles-ci seront différentes dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe par opposition à un thread de message.

Les gestionnaires définis dans `ActivityHandler` sont présentés ci-dessous :

| Événement | D | Description |
| :-- | :-- | :-- |
| N’importe quel type d’activité reçu | `OnTurnAsync` | Appelle l’un des autres gestionnaires, en fonction du type d’activité reçu. |
| Activité de message reçue | `OnMessageActivityAsync` | Remplacez ceci pour gérer une `Message` activité. |
| Activité de mise à jour de conversation reçue | `OnConversationUpdateActivityAsync` | Sur une `ConversationUpdate` activité, appelle un gestionnaire si les membres autres que le bot ont rejoint ou quitté la conversation. |
| Les membres autres que les robots joignent la conversation | `OnMembersAddedAsync` | Remplacez ceci pour gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `OnMembersRemovedAsync` | Remplacez ceci pour gérer les membres qui quittent une conversation. |
| Activité d’événement reçue | `OnEventActivityAsync` | Sur une `Event` activité, appelle un gestionnaire spécifique au type d’événement. |
| Activité d’événement de réponse de jeton reçue | `OnTokenResponseEventAsync` | Substituez cette option pour gérer les événements de réponse de jeton. |
| Activité d’événement sans réponse de jeton reçue | `OnEventAsync` | Substituez ceci pour gérer les autres types d’événements. |
| Autre type d’activité reçu | `OnUnrecognizedActivityTypeAsync` | Remplacez ceci pour gérer n’importe quel type d’activité non géré. |

#### <a name="teams-specific-handlers"></a>Gestionnaires spécifiques à teams

L' `TeamsActivityHandler` étend la liste des gestionnaires ci-dessus pour inclure les éléments suivants :

| Événement | D | Description |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Remplacez ceci pour gérer la création d’un canal Teams. Pour plus d’informations, consultez la rubrique [canal créé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Remplacez ceci pour gérer la suppression d’un canal Teams. Pour plus d’informations, consultez la rubrique [canal supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Remplacez ceci pour gérer un canal teams renommé. Pour plus d’informations, voir [canal renommé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Remplacez ceci pour gérer une équipe teams renommée. Pour plus d’informations, consultez la rubrique [Equipe renommée](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler` . Remplacez ceci pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, consultez la rubrique membres de l' [équipe ajoutés dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler` . Remplacez ceci pour gérer les membres qui quittent une équipe. Pour plus d’informations, consultez la rubrique membres de l' [équipe supprimés dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Les équipes appellent des activités

Voici une liste de tous les gestionnaires d’activités de teams appelés à partir du gestionnaire d’activités de `OnInvokeActivityAsync` _teams_ :

| Types d’appel                    | D                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction. Invoke               | `OnTeamsCardActionInvokeAsync`       | Appel d’action de la carte Teams. |
| fileConsent/Invoke              | `OnTeamsFileConsentAcceptAsync`      | Acceptation du consentement de fichier Teams. |
| fileConsent/Invoke              | `OnTeamsFileConsentAsync`            | Consentement du fichier Teams. |
| fileConsent/Invoke              | `OnTeamsFileConsentDeclineAsync`     | Consentement du fichier Teams. |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Action de la carte de connecteur O365 Teams. |
| connexion/verifyState              | `OnTeamsSigninVerifyStateAsync`      | L’état de vérification de la connexion Teams. |
| tâche/extraction                      | `OnTeamsTaskModuleFetchAsync`        | Extraction du module de tâche Teams. |
| tâche/Envoyer                     | `OnTeamsTaskModuleSubmitAsync`       | Soumission du module de tâche équipes. |

Les activités d’appel répertoriées ci-dessus concernent les robots de conversation dans Teams. Le kit de développement logiciel (SDK) de robot prend également en charge les appels spécifiques aux extensions de messagerie. Pour plus d’informations, consultez [qu’est-ce que les extensions de messagerie](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Tous les gestionnaires d’activité décrits ci-dessous continuent de fonctionner comme ils le font avec un robot non Teams, à l’exception de la gestion des membres *ajoutés* et des membres des activités *supprimées* , celles-ci seront différentes dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe par opposition à un thread de message.

#### <a name="core-bot-framework-handlers"></a>Gestionnaires d’infrastructure de robot principal

Les gestionnaires définis dans `ActivityHandler` sont présentés ci-dessous.

| Événement | D | Description |
| :-- | :-- | :-- |
| N’importe quel type d’activité reçu | `onTurn` | Appelle l’un des autres gestionnaires, en fonction du type d’activité reçu. |
| Activité de message reçue | `onMessage` | Fournissez une fonction pour qu’elle gère une `Message` activité. |
| Activité de mise à jour de conversation reçue | `onConversationUpdate` | Sur une `ConversationUpdate` activité, appelle un gestionnaire si les membres autres que le bot ont rejoint ou quitté la conversation. |
| Les membres autres que les robots joignent la conversation | `onMembersAdded` | Fournissez une fonction permettant de gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `onMembersRemoved` | Fournir une fonction pour ce qui permet de gérer les membres qui quittent une conversation. |
| Activité d’événement reçue | `onEvent` | Sur une `Event` activité, appelle un gestionnaire spécifique au type d’événement. |
| Activité d’événement de réponse de jeton reçue | `onTokenResponseEvent` | Fournissez une fonction permettant de gérer les événements de réponse de jeton. |
| Autre type d’activité reçu | `onUnrecognizedActivityType` | Fournissez une fonction pour qu’elle gère n’importe quel type d’activité non géré. |
| Gestionnaires d’activité terminés | `onDialog` | Fournissez une fonction permettant de gérer le traitement qui doit être effectué à la fin d’un tour une fois que le reste de vos gestionnaires d’activité est terminé. |

#### <a name="teams-specific-handlers"></a>Gestionnaires spécifiques à teams

L' `TeamsActivityHandler` étend la liste des gestionnaires dans la section des gestionnaires de l’infrastructure de robot pour inclure les éléments suivants :

| Événement | D | Description |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Remplacez ceci pour gérer la création d’un canal Teams. Pour plus d’informations, consultez la rubrique [canal créé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Remplacez ceci pour gérer la suppression d’un canal Teams. Pour plus d’informations, consultez la rubrique [canal supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Remplacez ceci pour gérer un canal teams renommé. Pour plus d’informations, voir [canal renommé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` Remplacez ceci pour gérer une équipe teams renommée. Pour plus d’informations, consultez la rubrique [Equipe renommée](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler` . Remplacez ceci pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, consultez la rubrique membres de l' [équipe ajoutés dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler` . Remplacez ceci pour gérer les membres qui quittent une équipe. Pour plus d’informations, consultez la rubrique membres de l' [équipe supprimés dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |

#### <a name="teams-invoke-activities"></a>Les équipes appellent des activités

Voici une liste de tous les gestionnaires d’activités de teams appelés à partir du `onInvokeActivity` Gestionnaire d’activités de teams :

| Types d’appel                    | D                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction. Invoke               | `handleTeamsCardActionInvoke`       | Appel d’action de la carte Teams. |
| fileConsent/Invoke              | `handleTeamsFileConsentAccept`      | Acceptation du consentement de fichier Teams. |
| fileConsent/Invoke              | `handleTeamsFileConsent`            | Consentement du fichier Teams. |
| fileConsent/Invoke              | `handleTeamsFileConsentDecline`     | Consentement du fichier Teams. |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Action de la carte de connecteur O365 Teams. |
| connexion/verifyState              | `handleTeamsSigninVerifyState`      | L’état de vérification de la connexion Teams. |
| tâche/extraction                      | `handleTeamsTaskModuleFetch`        | Extraction du module de tâche Teams. |
| tâche/Envoyer                     | `handleTeamsTaskModuleSubmit`       | Soumission du module de tâche équipes. |

Les activités d’appel répertoriées dans la section activités appel à teams sont destinées aux robots de conversation dans Teams. Le kit de développement logiciel (SDK) de robot prend également en charge les activités d’appel spécifiques aux extensions de messagerie. Pour plus d’informations, consultez la rubrique [What is Messaging extensions](https://aka.ms/azure-bot-what-are-messaging-extensions).

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Gestionnaires d’infrastructure de robot principal

>[!NOTE]
> À l’exception des activités des membres ajoutées et supprimées, tous les gestionnaires d’activité décrits dans cette section continuent de fonctionner comme ils le font avec un bot non Teams.

Les gestionnaires d’activité sont différents dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe au lieu d’un thread de message.

La liste des gestionnaires définis dans `ActivityHandler` inclut les éléments suivants :

| Événement | D | Description |
| :-- | :-- | :-- |
| N’importe quel type d’activité reçu | `on_turn` | Appelle l’un des autres gestionnaires, en fonction du type d’activité reçu. |
| Activité de message reçue | `on_message_activity` | Remplace ceci pour gérer une `Message` activité. |
| Activité de mise à jour de conversation reçue | `on_conversation_update_activity` | Appelle un gestionnaire si les membres autres que le bot rejoignent ou quittent la conversation. |
| Les membres autres que les robots joignent la conversation | `on_members_added_activity` | Remplace ceci pour gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `on_members_removed_activity` | Remplace ceci pour gérer les membres qui quittent une conversation. |
| Activité d’événement reçue | `on_event_activity` | Appelle un gestionnaire spécifique au type d’événement. |
| Activité d’événement de réponse de jeton reçue | `on_token_response_event` | Remplace ceci pour gérer les événements de réponse de jeton. |
| Activité d’événement sans réponse de jeton reçue | `on_event` | Substitue ceci pour gérer d’autres types d’événements. |
| Autres types d’activité reçus | `on_unrecognized_activity_type` | Remplace ceci pour gérer tout type d’activité qui n’est pas géré. |

#### <a name="teams-specific-handlers"></a>Gestionnaires spécifiques à teams

L' `TeamsActivityHandler` étend la liste des gestionnaires à partir de la section gestionnaires de l’infrastructure de robot principale pour inclure les éléments suivants :

| Événement | D | Description |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | Remplace ceci pour gérer un canal teams en cours de création. Pour plus d’informations, consultez la rubrique [canal créé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `on_teams_channel_deleted` | Remplace ceci pour gérer la suppression d’un canal Teams. Pour plus d’informations, consultez la rubrique [Channel Deleted](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) in [conversation Update Events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `on_teams_channel_renamed` | Remplace ceci pour gérer le changement de nom d’un canal Teams. Pour plus d’informations, reportez-vous à la rubrique [canal renommé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) dans [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` Remplace ceci pour gérer une équipe teams renommée. Pour plus d’informations, voir [Team Renamed](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) in [conversation Update Events](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `on_teams_members_added` | Appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler` . Remplace ceci pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, consultez la rubrique membres de l' [équipe ajoutés dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `on_teams_members_removed` | Appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler` . Remplace ceci pour gérer les membres qui quittent une équipe. Pour plus d’informations, consultez la rubrique membres de l' [équipe supprimés dans les](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke-activities"></a>Les équipes appellent des activités

La liste des gestionnaires d’activités teams appelés à partir du `on_invoke_activity` Gestionnaire d’activités de teams comprend les éléments suivants :

| Types d’appel                    | D                              | Description                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction. Invoke               | `on_teams_card_action_invoke`       | Appel d’action de la carte Teams. |
| fileConsent/Invoke              | `on_teams_file_consent_accept`      | Acceptation du consentement de fichier Teams. |
| fileConsent/Invoke              | `on_teams_file_consent`            | Consentement du fichier Teams. |
| fileConsent/Invoke              | `on_teams_file_consent_decline`     | Refus de consentement de fichier Teams. |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Action de la carte de connecteur O365 Teams. |
| connexion/verifyState              | `on_teams_signin_verify_state`      | L’état de vérification de la connexion Teams. |
| tâche/extraction                      | `on_teams_task_module_fetch`        | Extraction du module de tâche Teams. |
| tâche/Envoyer                     | `on_teams_task_module_submit`       | Soumission du module de tâche équipes. |

Les activités d’appel répertoriées dans la section activités appel à teams sont destinées aux robots de conversation dans Teams. Le kit de développement logiciel (SDK) de robot prend également en charge les activités d’appel spécifiques aux extensions de messagerie. Pour plus d’informations, consultez la rubrique [What is Messaging extensions](https://aka.ms/azure-bot-what-are-messaging-extensions).

---
