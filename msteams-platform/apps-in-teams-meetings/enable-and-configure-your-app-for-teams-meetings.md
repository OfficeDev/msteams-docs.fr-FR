---
title: Activer et configurer vos applications pour Teams réunions
author: surbhigupta
description: Activer et configurer vos applications pour Teams réunions
ms.topic: conceptual
ms.openlocfilehash: c123cc5cf15a7d0af64e2de16e96a673a2e4435c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53139969"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>Activer et configurer vos applications pour Teams réunions

Chaque équipe dispose d’une façon différente de communiquer et de collaborer sur des tâches. Vous pouvez effectuer ces différentes tâches en personnalisant Teams avec des applications pour les réunions. Pour personnaliser et effectuer différentes tâches, vous devez activer vos applications pour les réunions Teams et configurer vos applications pour qu’elles soient disponibles dans l’étendue de la réunion dans leur manifeste d’application.

## <a name="enable-your-app-for-teams-meetings"></a>Activer votre application pour les Teams réunion

Pour activer votre application pour Teams réunions, vous devez mettre à jour le manifeste de votre application et utiliser les propriétés de contexte pour déterminer où votre application doit apparaître.

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Les fonctionnalités de l’application réunions sont déclarées dans le manifeste de votre application à l’aide `configurableTabs` des `scopes` tableaux et des `context` tableaux. L’étendue définit à qui et le contexte définit l’endroit où votre application est disponible.

> [!NOTE]
> * Essayez de mettre à jour le manifeste de votre application avec [le schéma de manifeste.](../resources/schema/manifest-schema-dev-preview.md)
> * Les applications dans les réunions nécessitent une étendue groupchat. L’étendue de l’équipe fonctionne pour les onglets dans les canaux uniquement.

Le manifeste de l’application doit inclure l’extrait de code suivant :

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
> `meetingStage` est actuellement disponible en [prévisualisation pour les](../resources/dev-preview/developer-preview-intro.md) développeurs uniquement.

### <a name="context-property"></a>Propriété Context

La propriété détermine ce qui doit être affiché lorsqu’un utilisateur appelle une application dans une réunion en fonction de l’endroit où il `context` appelle l’application. `context`L’onglet et `scopes` les propriétés vous permettent de déterminer où votre application doit apparaître. Les onglets de la `team` ou `groupchat` de l’étendue peuvent avoir plusieurs contextes. Voici les valeurs de la propriété à partir de laquelle vous pouvez utiliser l’ensemble ou `context` certaines des valeurs :

|Valeur|Description|
|---|---|
| **channelTab** | Onglet dans l’en-tête d’un canal d’équipe. |
| **privateChatTab** | Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs, et non dans le contexte d’une équipe ou d’une réunion. |
| **meetingChatTab** | Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le cadre d’une réunion programmée. |
| **meetingDetailsTab** | Onglet dans l’en-tête de l’affichage Détails de la réunion du calendrier. |
| **meetingSidePanel** | Panneau en réunion ouvert via la barre unifiée (barre U). |
| **meetingStage** | Une application de meetingSidePanel peut être partagée à l’étape de la réunion. |

> [!NOTE]
> `Context` n’est actuellement pas prise en charge sur les clients mobiles.

Après avoir activé votre application pour Teams réunions, vous devez configurer votre application avant une réunion, pendant une réunion et après une réunion.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurer votre application pour les scénarios de réunion

> [!NOTE]
> * Pour que votre application soit visible dans la galerie d’onglets, elle doit prendre en charge les onglets configurables et l’étendue de conversation de groupe.
> * Les clients mobiles ne supportent les onglets qu’aux étapes préalables et post-réunion.
> * Les expériences en réunion qui sont des boîtes de dialogue et des onglets en réunion ne sont actuellement pas pris en charge sur les clients mobiles. Pour plus d’informations, [consultez des conseils pour les onglets mobiles](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour appareils mobiles.

Teams réunions fournit une expérience de collaboration unique pour votre organisation. Il permet de configurer votre application pour différents scénarios de réunion. Vous pouvez configurer vos applications pour améliorer l’expérience de réunion en fonction du rôle de participant ou du type d’utilisateur. Vous pouvez maintenant identifier les actions qui peuvent être prises dans les scénarios de réunion suivants :

* [Avant une réunion](#before-a-meeting)
* [Lors d'une réunion](#during-a-meeting)
* [Après une réunion](#after-a-meeting)

### <a name="before-a-meeting"></a>Avant une réunion

Avant une réunion, les utilisateurs peuvent ajouter des onglets, des bots et des extensions de messagerie. Les utilisateurs ayant des rôles d’organisateur et de présentateur peuvent ajouter des onglets à une réunion.

**Pour ajouter un onglet à une réunion**

1. Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.
1. Sélectionnez **l’onglet Détails** et sélectionnez <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    ![Expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

1. Dans la galerie d’onglets qui s’affiche, sélectionnez l’application à ajouter et suivez les étapes nécessaires. L’application est installée en tant qu’onglet.

    > [!NOTE]
    > Actuellement, dans l’onglet Réunions, l’obtention des détails de la réunion et des informations sur les participants n’est pas prise en charge.

**Pour ajouter une extension de messagerie à une réunion**

1. Sélectionnez les &#x25CF;&#x25CF;&#x25CF; situées dans la zone composer un message de la conversation.
1. Sélectionnez l’application à ajouter et suivez les étapes nécessaires. L’application est installée en tant qu’extension de messagerie.

**Pour ajouter un bot à une réunion**

Dans une conversation de réunion, entrez la **@** clé et sélectionnez **Obtenir des bots.**

> [!NOTE]
> * L’identité de l’utilisateur doit être confirmée à [l’aide de l' ssO Onglets.](../tabs/how-to/authentication/auth-aad-sso.md) Après l’authentification, l’application peut récupérer le rôle d’utilisateur à l’aide de `GetParticipant` l’API.
> * En fonction du rôle utilisateur, l’application a la possibilité de fournir des expériences spécifiques au rôle. Par exemple, une application de sondage permet uniquement aux organisateurs et aux présentateurs de créer un sondage.
> * Les attributions de rôle peuvent être modifiées pendant une réunion. Pour plus d’informations, [voir les rôles dans une Teams réunion.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

### <a name="during-a-meeting"></a>Lors d'une réunion

Au cours d’une réunion, vous pouvez utiliser meetingSidePanel ou la boîte de dialogue en réunion pour créer des expériences uniques pour vos applications.

#### <a name="meetingsidepanel"></a>meetingSidePanel

Avec meetingSidePanel, vous pouvez personnaliser les expériences d’une réunion qui permettent aux organisateurs et aux présentateurs d’avoir différents ensembles d’affichages et d’actions. Dans le manifeste de votre application, vous devez ajouter meetingSidePanel au tableau de contexte. Dans la réunion et dans tous les scénarios, l’application est rendue dans un onglet de réunion de 320 pixels de largeur. Pour plus d’informations, [voir l’interface FrameContext.](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)

Pour utiliser l’API pour router les demandes en `userContext` conséquence, voir Teams [SDK](../tabs/how-to/access-teams-context.md#user-context). Pour plus d’informations, [Teams flux d’authentification pour les onglets.](../tabs/how-to/authentication/auth-flow-tab.md) Le flux d’authentification pour les onglets est très similaire au flux d’authentification pour les sites web. Par conséquent, les onglets peuvent utiliser OAuth 2.0 directement. Pour plus d’informations, voir Plateforme d’identités Microsoft flux de code d’autorisation [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)

L’extension de messagerie fonctionne comme prévu lorsqu’un utilisateur est dans un affichage en réunion et qu’il peut publier des cartes d’extension de message de composition. AppName en réunion est une boîte à outils qui indique le nom de l’application dans la barre U de la réunion.

> [!NOTE]
> Utilisez la version 1.7.0 ou une version ultérieure du [SDK Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)car les versions antérieures ne peuvent pas prendre en charge le panneau latéral.

#### <a name="in-meeting-dialog-box"></a>Boîte de dialogue En réunion

La boîte de dialogue de réunion peut être utilisée pour impliquer les participants au cours de la réunion et collecter des informations ou des commentaires pendant la réunion. Utilisez [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) l’API pour signaler qu’une notification de bulle doit être déclenchée. Dans le cadre de la charge utile de demande de notification, incluez l’URL où le contenu à afficher est hébergé.

La boîte de dialogue en réunion ne doit pas utiliser le module de tâche. Le module de tâche n’est pas appelé dans une conversation de réunion. Une URL de ressource externe est utilisée pour afficher une bulle de contenu dans une réunion. Vous pouvez utiliser la `submitTask` méthode pour envoyer des données dans une conversation de réunion.

> [!NOTE]
> * Vous devez appeler la [fonction submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) pour ignorer automatiquement une fois qu’un utilisateur effectue une action dans l’affichage web. Il s’agit d’une condition requise pour la soumission d’application. Pour plus d’informations, voir Teams module de [tâche du SDK.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)
> * Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, votre charge utile de demande d’appel initiale doit reposer sur les métadonnées de la demande dans l’objet, et non sur `from.id` `from` les `from.aadObjectId` métadonnées de la demande. `from.id`est l’ID d’utilisateur `from.aadObjectId` Azure Active Directory (AAD) de l’utilisateur. Pour plus d’informations, voir [l’utilisation de modules de tâche](../task-modules-and-cards/task-modules/task-modules-tabs.md) dans les onglets [et créer et envoyer le module de tâche.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

#### <a name="shared-meeting-stage"></a>Étape de réunion partagée

> [!NOTE]
> * Cette fonctionnalité est actuellement disponible en [prévisualisation pour les](../resources/dev-preview/developer-preview-intro.md) développeurs uniquement.

La phase de réunion partagée permet aux participants à la réunion d’interagir et de collaborer sur le contenu de l’application en temps réel.

Le contexte requis se trouve `meetingStage` dans le manifeste de l’application. Une condition préalable consiste à avoir le `meetingSidePanel` contexte. Cela active le **partage** dans meetingSidePanel.

![Partager des étapes pendant l’expérience de réunion](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

Pour activer la phase de réunion partagée, configurez votre manifeste d’application comme ceci :

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

Découvrez comment [concevoir une expérience de réunion partagée.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)

### <a name="after-a-meeting"></a>Après une réunion

Les configurations après et [avant les réunions](#before-a-meeting) sont les mêmes.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | Échantillon |
|----------------|-----------------|--------------|----------------|-----------|
| Application de réunion | Montre comment utiliser l’application Générateur de jetons de réunion pour demander un jeton, qui est généré séquentiellement afin que chaque participant ait une opportunité de participer à une réunion. Cela peut être utile dans des situations telles que les réunions scrum et les sessions Q&A. | [View](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a>Voir aussi

* [Recommandations en matière de conception de boîte de dialogue en réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams d’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
