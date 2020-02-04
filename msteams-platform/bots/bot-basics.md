---
title: Notions de base sur les robots
author: clearab
description: Maîtrisez les notions de base des robots dans Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e1b0c79b73ae89c8ab76ba0a1ff045603ab0b932
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673704"
---
# <a name="bot-basics"></a>Notions de base sur les robots

Il s’agit d’une introduction qui s’appuie sur l’article [How bots Work](https://aka.ms/how-bots-work) in the Core [bot Framework documentation](https://aka.ms/azure-bot-service-docs). Vous trouverez peut-être cet article, ainsi que les autres Articles de la section *concepts* , utiles.

La principale différence dans les robots développés pour Microsoft teams réside dans la façon dont les activités sont gérées. Le gestionnaire d’activité Microsoft teams dérive du gestionnaire d’activité de l’infrastructure bot pour acheminer toutes les activités de teams avant d’autoriser le traitement de toutes les activités spécifiques non liées à l’équipe.

## <a name="teams-activity-handlers"></a>Gestionnaires d’activités de teams

Lorsqu’un bot pour Microsoft teams reçoit une activité, il le transmet à ses *gestionnaires d’activité*. En coulisses, il existe un gestionnaire de base appelé *Gestionnaire de tournage*, que toutes les activités sont acheminées par le biais de. Le *Gestionnaire Turn* appelle le gestionnaire d’activités requis pour gérer le type d’activité reçu. Lorsqu’un bot conçu pour Microsoft teams diffère, il est dérivé de `TeamsActivityHandler` la classe qui est dérivée de la classe `ActivityHandler` de l’infrastructure bot.

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

Comme avec tout robot créé à l’aide de Microsoft bot Framework, si le bot reçoit une activité de message, le gestionnaire de tournage voit cette activité entrante `OnMessageActivityAsync` et l’envoie au gestionnaire d’activité. Dans Teams, cette fonctionnalité reste identique. Si le bot reçoit une activité de mise à jour de conversation, le gestionnaire de tournage voit cette activité entrante et l’envoie au `OnConversationUpdateActivityAsync` gestionnaire d’activités *teams* qui vérifie d’abord les événements spécifiques des équipes et les transmet au gestionnaire d’activité de l’infrastructure de robots si aucun n’est trouvé.

Dans la classe de gestionnaire d’activités de teams, il existe deux gestionnaires d' `OnConversationUpdateActivityAsync` activité de teams principaux, qui acheminent toutes les activités de mise à jour de conversation et `OnInvokeActivityAsync` qui achemine toutes les équipes.

Pour implémenter votre logique pour les gestionnaires d’activités spécifiques à Teams, vous devez remplacer ces méthodes dans votre bot, comme illustré dans la section [logique bot](#bot-logic) ci-dessous. Pour chacun de ces gestionnaires, il n’existe pas d’implémentation de base, il vous suffit d’ajouter la logique de votre choix dans votre substitution.

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

Comme avec tout robot créé à l’aide de Microsoft bot Framework, si le bot reçoit une activité de message, le gestionnaire de tournage voit cette activité entrante `onMessage` et l’envoie au gestionnaire d’activité. Dans Teams, cette fonctionnalité reste identique. Si le bot reçoit une activité de mise à jour de conversation, le gestionnaire de tournage voit cette activité entrante et l’envoie au `dispatchConversationUpdateActivity` gestionnaire d’activités *teams* qui vérifiera d’abord les événements spécifiques des équipes et les transmettra au gestionnaire d’activités de robots Framework si aucun n’est trouvé.

Dans la classe de gestionnaire d’activités de teams, il existe deux gestionnaires d' `dispatchConversationUpdateActivity` activité de teams principaux, qui acheminent toutes les activités de mise à jour de conversation et `onInvokeActivity` qui achemine toutes les équipes.

Pour implémenter votre logique pour les gestionnaires d’activités spécifiques à Teams, vous devez remplacer ces méthodes dans votre bot, comme indiqué dans la section de la [logique bot](#bot-logic) ci-dessous. Pour chacun de ces gestionnaires, définissez votre logique de robot, puis **Veillez à appeler `next()` à la fin**. En vous `next()` appelant, assurez-vous que le gestionnaire suivant s’exécute.

---

## <a name="bot-logic"></a>Logique de robot

La logique du robot traite les activités entrantes à partir d’un ou de plusieurs de vos canaux de robots et génère des activités sortantes en réponse.  Cela est toujours vrai pour les robots dérivés de la classe de gestionnaire d’activités Teams, qui vérifie d’abord les activités Teams, puis passe toutes les autres activités au gestionnaire d’activité de l’infrastructure de robot.

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Gestionnaires d’infrastructure de robot principal

Tous les gestionnaires d’activité décrits ci-dessous continueront de fonctionner comme avec un robot non Teams, à l’exception de la gestion des membres *ajoutés* et des activités *supprimées* , celles-ci seront différentes dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe par opposition à un thread de message.

Les gestionnaires définis dans `ActivityHandler` sont présentés ci-dessous.

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

L `TeamsActivityHandler` 'étend la liste des gestionnaires ci-dessus pour inclure les éléments suivants :

| Événement | D | Description |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Remplacez ceci pour gérer la création d’un canal Teams. Pour plus d’informations, consultez la rubrique [canal créé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Remplacez ceci pour gérer la suppression d’un canal Teams. Pour plus d’informations, consultez la rubrique [canal supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Remplacez ceci pour gérer un canal teams renommé. Pour plus d’informations, voir [canal renommé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Remplacez ceci pour gérer une équipe teams renommée. Pour plus d’informations, consultez la rubrique [Equipe renommée](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersAdded | `OnTeamsMembersAddedAsync` | Appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler`. Remplacez ceci pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, consultez la rubrique [membre d’équipe ajouté](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Added) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler`. Remplacez ceci pour gérer les membres qui quittent une équipe. Pour plus d’informations, consultez la rubrique [membre d’équipe supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Removed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|

#### <a name="teams-invoke--activities"></a>Les équipes appellent des activités

Voici une liste de tous les gestionnaires d’activités de teams appelés à partir `OnInvokeActivityAsync` du gestionnaire d’activités de _teams_ :

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

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

Tous les gestionnaires d’activité décrits ci-dessous continuent de fonctionner comme ils le font avec un robot non Teams, à l’exception de la gestion des membres *ajoutés* et des membres des activités *supprimées* , celles-ci seront différentes dans le contexte d’une équipe, où le nouveau membre est ajouté à l’équipe par opposition à un thread de message.

#### <a name="core-bot-framework-handlers"></a>Gestionnaires d’infrastructure de robot principal

Les gestionnaires définis dans `ActivityHandler` sont présentés ci-dessous.

| Événement | D | Description |
| :-- | :-- | :-- |
| N’importe quel type d’activité reçu | `onTurn` | Appelle l’un des autres gestionnaires, en fonction du type d’activité reçu. |
| Activité de message reçue | `onMessage` | Fournissez une fonction pour qu’elle gère `Message` une activité. |
| Activité de mise à jour de conversation reçue | `onConversationUpdate` | Sur une `ConversationUpdate` activité, appelle un gestionnaire si les membres autres que le bot ont rejoint ou quitté la conversation. |
| Les membres autres que les robots joignent la conversation | `onMembersAdded` | Fournissez une fonction permettant de gérer les membres qui rejoignent une conversation. |
| Les membres non-bot ont quitté la conversation | `onMembersRemoved` | Fournir une fonction pour ce qui permet de gérer les membres qui quittent une conversation. |
| Activité d’événement reçue | `onEvent` | Sur une `Event` activité, appelle un gestionnaire spécifique au type d’événement. |
| Activité d’événement de réponse de jeton reçue | `onTokenResponseEvent` | Fournissez une fonction permettant de gérer les événements de réponse de jeton. |
| Autre type d’activité reçu | `onUnrecognizedActivityType` | Fournissez une fonction pour qu’elle gère n’importe quel type d’activité non géré. |
| Gestionnaires d’activité terminés | `onDialog` | Fournissez une fonction permettant de gérer le traitement qui doit être effectué à la fin d’un tour, une fois que le reste de vos gestionnaires d’activité est terminé. |

#### <a name="teams-specific-handlers"></a>Gestionnaires spécifiques à teams

L `TeamsActivityHandler` 'étend la liste des gestionnaires ci-dessus pour inclure les éléments suivants :

| Événement | D | Description |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | Remplacez ceci pour gérer la création d’un canal Teams. Pour plus d’informations, consultez la rubrique [canal créé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| channelDeleted | `OnTeamsChannelDeletedAsync` | Remplacez ceci pour gérer la suppression d’un canal Teams. Pour plus d’informations, consultez la rubrique [canal supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events).|
| channelRenamed | `OnTeamsChannelRenamedAsync` | Remplacez ceci pour gérer un canal teams renommé. Pour plus d’informations, voir [canal renommé](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`Remplacez ceci pour gérer une équipe teams renommée. Pour plus d’informations, consultez la rubrique [Equipe renommée](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) en [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersAdded | `OnTeamsMembersAddedAsync` | Appelle la `OnMembersAddedAsync` méthode dans `ActivityHandler`. Remplacez ceci pour gérer les membres qui rejoignent une équipe. Pour plus d’informations, consultez la rubrique [membre d’équipe ajouté](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Added) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | Appelle la `OnMembersRemovedAsync` méthode dans `ActivityHandler`. Remplacez ceci pour gérer les membres qui quittent une équipe. Pour plus d’informations, consultez la rubrique [membre d’équipe supprimé](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Removed) dans les [événements de mise à jour de conversation](https://aka.ms/azure-bot-subscribe-to-conversation-events). |

#### <a name="teams-invoke-activities"></a>Les équipes appellent des activités

Voici une liste de tous les gestionnaires d’activités de teams appelés à partir `onInvokeActivity` du gestionnaire d’activités de _teams_ :

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

Les activités d’appel répertoriées ci-dessus concernent les robots de conversation dans Teams. Le kit de développement logiciel (SDK) de robot prend également en charge les appels spécifiques aux extensions de messagerie. Pour plus d’informations, consultez [qu’est-ce que les extensions de messagerie](https://aka.ms/azure-bot-what-are-messaging-extensions)

---
