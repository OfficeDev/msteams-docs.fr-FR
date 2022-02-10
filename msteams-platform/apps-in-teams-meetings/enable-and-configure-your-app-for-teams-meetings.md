---
title: Activer et configurer vos applications pour Teams réunions
author: surbhigupta
description: Activer et configurer vos applications pour les réunions Teams et différents scénarios de réunion, mettre à jour le manifeste de l’application, configurer des fonctionnalités, telles que la boîte de dialogue de réunion, la phase de réunion partagée, le sidepanel de réunion, et bien plus encore
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 7eacd4c406dc81a2f6704a05d678eb6b70912856
ms.sourcegitcommit: 60e4bbb013f0bb17a87a2e558abfcc311c73af75
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62523779"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>Activer et configurer vos applications pour Teams réunions

Chaque équipe dispose d’une façon différente de communiquer et de collaborer sur des tâches. Pour effectuer ces différentes tâches, personnalisez Teams avec des applications pour les réunions. Activez vos applications pour Teams réunions et configurez les applications pour qu’elles soient disponibles dans l’étendue de la réunion dans leur manifeste d’application.

## <a name="enable-your-app-for-teams-meetings"></a>Activer votre application pour Teams réunions

Pour activer votre application pour les Teams, mettez à jour le manifeste de votre application et utilisez les propriétés de contexte pour déterminer où votre application doit apparaître.

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Les fonctionnalités de l’application réunions sont déclarées dans le manifeste de votre application à l’aide `configurableTabs`des tableaux et des `scopes`tableaux `context` . L’étendue définit qui peut accéder et le contexte définit l’endroit où votre application est disponible.

> [!NOTE]
> * Vous devez mettre à jour le manifeste de votre application avec [le schéma de manifeste](../resources/schema/manifest-schema-dev-preview.md).
> * Les applications dans les réunions nécessitent une `groupchat` étendue. L’étendue `team` fonctionne pour les onglets dans les canaux uniquement.

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

### <a name="context-property"></a>Propriété Context

La `context` propriété détermine ce qui doit être affiché lorsqu’un utilisateur appelle une application dans une réunion en fonction de l’endroit où il appelle l’application. L’onglet `context` et `scopes` les propriétés vous permettent de déterminer où votre application doit apparaître. Les onglets de la ou `team` de l’étendue `groupchat` peuvent avoir plusieurs contextes. Voici les valeurs de la `context` propriété à partir de laquelle vous pouvez utiliser l’ensemble ou certaines des valeurs :

|Valeur|Description|
|---|---|
| **channelTab** | Onglet dans l’en-tête d’un canal d’équipe. |
| **privateChatTab** | Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs, et non dans le contexte d’une équipe ou d’une réunion. |
| **meetingChatTab** | Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs pour une réunion programmée. Vous pouvez spécifier **meetingChatTab** ou **meetingDetailsTab** pour vous assurer que les applications fonctionnent sur mobile. |
| **meetingDetailsTab** | Onglet dans l’en-tête de l’affichage Détails de la réunion du calendrier. Vous pouvez spécifier **meetingChatTab** ou **meetingDetailsTab** pour vous assurer que les applications fonctionnent sur mobile. |
| **meetingSidePanel** | Panneau en réunion ouvert via la barre unifiée (barre U). |
| **meetingStage** | Une application de l’étape `meetingSidePanel` de réunion peut être partagée. Vous ne pouvez pas utiliser cette application sur les clients mobiles ou de salle Teams. |

Après avoir activé votre application pour Teams réunions, vous devez configurer votre application avant une réunion, pendant une réunion et après une réunion.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurer votre application pour les scénarios de réunion

Teams réunions fournissent une expérience de collaboration pour votre organisation. Configurez votre application pour différents scénarios de réunion et pour améliorer l’expérience de réunion. Vous pouvez maintenant identifier les actions qui peuvent être prises dans les scénarios de réunion suivants :

* [Avant une réunion](#before-a-meeting)
* [Lors d'une réunion](#during-a-meeting)
* [Après une réunion](#after-a-meeting)

### <a name="before-a-meeting"></a>Avant une réunion

Avant une réunion, les utilisateurs peuvent ajouter des onglets, des bots et des extensions de messagerie. Les utilisateurs ayant des rôles d’organisateur et de présentateur peuvent ajouter des onglets à une réunion.

**Pour ajouter un onglet à une réunion**

1. Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.
1. Sélectionnez **l’onglet Détails** et sélectionnez <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting.png" alt="Pre-meeting experience" width="900"/>

1. Dans la galerie d’onglets qui s’affiche, sélectionnez l’application à ajouter et suivez les étapes nécessaires. L’application est installée en tant qu’onglet.

**Pour ajouter une extension de messagerie à une réunion**

1. Sélectionnez les &#x25CF;&#x25CF;&#x25CF; situées dans la zone composer un message de la conversation.
1. Sélectionnez l’application à ajouter et suivez les étapes nécessaires. L’application est installée en tant qu’extension de messagerie.

**Pour ajouter un bot à une réunion**

Dans une conversation de réunion, entrez la **@** clé et sélectionnez **Obtenir des bots**.

> [!NOTE]
> * La bulle de contenu publie une carte adaptative ou une carte simultanément dans la conversation de réunion accessible aux utilisateurs. Cela aide les utilisateurs lorsque la réunion ou l’Teams’application est réduite.
> * L’identité de l’utilisateur doit être confirmée à l’aide de [l’ssO Onglets](../tabs/how-to/authentication/auth-aad-sso.md). Après l’authentification, l’application peut récupérer le rôle d’utilisateur à l’aide de l’API `GetParticipant` .
> * En fonction du rôle utilisateur, l’application a la possibilité de fournir des expériences spécifiques au rôle. Par exemple, une application de sondage permet uniquement aux organisateurs et aux présentateurs de créer un sondage.
> * Les attributions de rôle peuvent être modifiées pendant une réunion. Pour plus d’informations, voir [rôles dans une Teams réunion.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

### <a name="during-a-meeting"></a>Lors d'une réunion

Au cours d’une réunion, vous pouvez utiliser `meetingSidePanel` la boîte de dialogue ou la boîte de dialogue en réunion pour créer des expériences uniques pour vos applications.

#### <a name="meeting-sidepanel"></a>Meeting SidePanel

Cela `meetingSidePanel` vous permet de personnaliser les expériences d’une réunion qui permettent aux organisateurs et aux présentateurs d’avoir différents ensembles d’affichages et d’actions. Dans le manifeste de votre application, vous devez l’ajouter `meetingSidePanel` au tableau de contexte. Dans la réunion et dans tous les scénarios, l’application est restituer dans un onglet de réunion de 320 pixels de largeur. Pour plus d’informations, [voir l’interface FrameContext](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).

Pour utiliser l’API `userContext` pour router les demandes, voir [Teams SDK](../tabs/how-to/access-teams-context.md#user-context). Pour plus d’informations, [Teams flux d’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md). Le flux d’authentification pour les onglets est similaire au flux d’authentification pour les sites web. Par conséquent, les onglets peuvent utiliser OAuth 2.0 directement. Pour plus d’informations, [voir Plateforme d'identités Microsoft flux de code d’autorisation OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

L’extension de messagerie fonctionne comme prévu lorsqu’un utilisateur est en affichage en réunion. L’utilisateur peut publier des cartes d’extension de message de composition. AppName en réunion est une boîte à outils qui indique le nom de l’application dans la barre U de la réunion.

> [!NOTE]
> Utilisez la version 1.7.0 ou une version ultérieure du [SDK Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), car les versions antérieures ne peuvent pas prendre en charge le panneau latéral.

#### <a name="in-meeting-dialog-box"></a>Boîte de dialogue En réunion

La boîte de dialogue de réunion est utilisée pour impliquer les participants pendant la réunion et collecter des informations ou des commentaires pendant la réunion. Utilisez [l’API SendNotificationSignal](API-references.md#send-notification-signal-api) pour déclencher une notification de bulle. Dans le cadre de la charge utile de demande de notification, incluez l’URL où le contenu à afficher est hébergé.

La boîte de dialogue en réunion ne doit pas utiliser le module de tâche. Le module de tâche n’est pas appelé dans une conversation de réunion. Une URL de ressource externe est utilisée pour afficher la bulle de contenu dans une réunion. Vous pouvez utiliser la méthode `submitTask` pour envoyer des données dans une conversation de réunion.

> [!NOTE]
> * Vous devez appeler la [fonction submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) pour ignorer automatiquement une fois qu’un utilisateur effectue une action dans l’affichage web. Il s’agit d’une condition requise pour la soumission d’application. Pour plus d’informations, [voir Teams module de tâche du SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true). 
> * Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, la charge utile de la demande d’appel initial `from.id` doit reposer sur les métadonnées `from` de demande dans l’objet, et non sur les `from.aadObjectId` métadonnées de demande. `from.id`est l’ID d’utilisateur `from.aadObjectId` et Microsoft Azure Active Directory (Azure AD) de l’utilisateur. Pour plus d’informations, voir [l’utilisation de modules de tâche dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) [et créer et envoyer le module de tâche](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

#### <a name="shared-meeting-stage"></a>Étape de réunion partagée

La phase de réunion partagée permet aux participants à la réunion d’interagir et de collaborer sur le contenu de l’application en temps réel. Vous pouvez partager vos applications à l’étape de la réunion collaborative des manières suivantes :

* [Partagez l’intégralité de l’application pour](#share-entire-app-to-stage) l’étape à l’aide du bouton partager pour mettre en Teams client.
* [Partagez des parties spécifiques de l’application pour](#share-specific-parts-of-the-app-to-stage) l’étape à l’aide d’API dans Teams SDK client.

##### <a name="share-entire-app-to-stage"></a>Partager l’intégralité de l’application pour la phase

Les participants peuvent partager l’ensemble de l’application à l’étape de la réunion collaborative à l’aide du bouton partager pour la phase à partir du panneau latéral de l’application.

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

Pour partager l’intégralité de l’application à l’étape, dans le manifeste de l’application, vous devez configurer `meetingStage` `meetingSidePanel` et en tant que contextes de trame. Par exemple :

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

Pour plus d’informations, voir [le manifeste de l’application](../resources/schema/manifest-schema-dev-preview.md#configurabletabs). 

##### <a name="share-specific-parts-of-the-app-to-stage"></a>Partager des parties spécifiques de l’application pour la phase

Les participants peuvent partager des parties spécifiques de l’application à la phase de réunion collaborative en utilisant le partage pour mettre en scène des API. Les API sont disponibles dans le SDK Teams client et sont appelés à partir du panneau latéral de l’application.

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

Pour partager des parties spécifiques de l’application à des étapes, vous devez appeler les API associées dans la bibliothèque Teams SDK client. Pour plus d’informations, voir la [référence d’API](API-references.md).

Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, la charge utile de la demande d’appel initial `from.id` doit reposer sur les métadonnées `from` de demande dans l’objet, et non sur les `from.aadObjectId` métadonnées de demande. `from.id`est l’ID d’utilisateur `from.aadObjectId` et Microsoft Azure Active Directory (Azure AD) de l’utilisateur. Pour plus d’informations, voir [l’utilisation de modules de tâche dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) [et créer et envoyer le module de tâche](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### <a name="after-a-meeting"></a>Après une réunion

Les configurations des réunions après [et avant](#before-a-meeting) sont les mêmes.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Application de réunion | Montre comment utiliser l’application Générateur de jetons de réunion pour demander un jeton. Le jeton est généré de manière séquentielle afin que chaque participant ait une opportunité de participer à une réunion. Le jeton est utile dans les situations telles que les réunions scrum et les sessions Q&A. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|Exemple d’étape de réunion | Exemple d’application pour afficher un onglet lors de la phase de réunion pour la collaboration | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|Panneau latéral de réunion | Exemple d’application pour montrer comment ajouter un ordre du jour dans un panneau latéral de réunion | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>Guides détaillés

* Suivez le [guide pas à pas pour](../sbs-meeting-token-generator.yml) générer un jeton de réunion dans votre Teams réunion.
* Suivez le [guide pas à pas pour](../sbs-meetings-sidepanel.yml) générer un sidepanel de réunion dans votre Teams réunion.
* Suivez le [guide pas à pas pour](../sbs-meetings-stage-view.yml) générer une vue d’étape de la réunion dans Teams réunion.
* Suivez le [guide pas à pas pour](../sbs-meeting-content-bubble.yml) générer une bulle de contenu de réunion dans Teams réunion.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Références API des applications de réunion](API-references.md)

## <a name="see-also"></a>Voir aussi

* [Recommandations en matière de conception de boîte de dialogue en réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams d’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Recommandations en matière de conception de l’expérience de réunion partagée](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Ajouter des applications à des réunions via Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
