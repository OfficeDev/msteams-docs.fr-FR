---
title: Créer des onglets pour la réunion
author: surbhigupta
description: Découvrez comment créer des onglets pour une conversation de réunion, un panneau côté réunion et une étape de réunion dans une réunion Microsoft Teams.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: d86f0931cb6338ef331f2afe3a4a5fdb217bb316
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615395"
---
# <a name="build-tabs-for-meeting"></a>Créer des onglets pour la réunion

Chaque équipe a une façon différente de communiquer et de collaborer des tâches. Pour effectuer ces différentes tâches, personnalisez Teams avec des applications pour les réunions. Activez vos applications pour les réunions Teams et configurez les applications pour qu’elles soient disponibles dans l’étendue de la réunion dans leur manifeste d’application.

## <a name="tabs-in-teams-meetings"></a>Onglets dans les réunions Teams

Les onglets permettent aux participants à la réunion d’accéder aux services et au contenu dans un espace spécifique au sein d’une réunion. Si vous débutez avec le développement d’onglets Microsoft Teams, consultez [les onglets Générer pour Teams](/microsoftteams/platform/tabs/what-are-tabs).

Avant de créer un onglet de réunion, il est important d’en savoir plus sur les surfaces disponibles pour cibler l’affichage de conversation de réunion, l’affichage des détails de la réunion, l’affichage du panneau côté réunion et l’affichage de la phase de réunion.

### <a name="meeting-details-view"></a>Vue détails de la réunion

1. Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.
1. Sélectionnez l’onglet **Détails** , puis sélectionnez :::image type="icon" source="../assets/icons/add-icon.png" Border = "false":::. La galerie d’applications s’affiche.

   :::image type="content" source="~/assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="Cette capture d’écran montre l’expérience d’application de pré-réunion dans la réunion Teams.":::

1. Dans la galerie d’applications, sélectionnez l’application que vous souhaitez ajouter et suivez les étapes nécessaires. L’onglet est ajouté à la page des détails de la réunion.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

L’image suivante montre un onglet ajouté à la page de détails de la réunion dans le client de bureau Teams :

   :::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="La capture d’écran montre les onglets Teams de bureau dans la vue détails de la réunion Teams.":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

L’image suivante montre un onglet ajouté à la page de détails de la réunion dans le client mobile Teams :

   :::image type="content" source="../assets/images/mobile-tab.png" alt-text="La capture d’écran montre les onglets Teams mobiles dans la vue détails de la réunion Teams.":::

---

### <a name="meeting-chat-view"></a>Vue de conversation de réunion

1. Dans le panneau de conversation Teams, sélectionnez l’affichage de conversation de réunion.

1. Sélectionnez :::image type="icon" source="../assets/icons/add-icon.png" Border = "false"::: et la galerie d’applications s’affiche.

1. Dans la galerie d’applications, sélectionnez l’application que vous souhaitez ajouter et suivez les étapes nécessaires. L’onglet est ajouté à la conversation de réunion.

   :::image type="content" source="../assets/images/apps-in-meetings/meeting-chat-view.png" alt-text="La capture d’écran montre l’affichage de conversation de réunion dans la réunion Teams.":::

### <a name="meeting-side-panel-view"></a>Vue du panneau côté réunion

1. Pendant une réunion, vous pouvez sélectionner :::image type="icon" source="../assets/icons/add-icon.png" Border = "false"::: **Applications** dans la fenêtre de réunion Teams pour ajouter des applications à la réunion.

   :::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="Cette capture d’écran montre comment ajouter une application dans la fenêtre de réunion Teams.":::

1. Dans la galerie d’applications, sélectionnez l’application que vous souhaitez ajouter et suivez les étapes nécessaires. L’application est ajoutée au panneau côté réunion.

   :::image type="content" source="../assets/images/side-panel-view.png" alt-text="Cette capture d’écran montre l’affichage du panneau latéral avec la liste des applications.":::

### <a name="meeting-stage-view"></a>Vue de la phase de réunion

1. Une fois qu’un onglet est ajouté au panneau côté réunion, vous pouvez choisir d’opter pour le partage d’application global.

1. Cela entraîne le rendu de l’onglet sur la scène pour chaque participant à la réunion.

   :::image type="content" source="../assets/images/meeting-stage-view.png" alt-text="Cette capture d’écran montre l’affichage de la phase de réunion de l’application que vous avez partagée à la réunion.":::

### <a name="apps-in-channel-meeting"></a>Applications dans la réunion de canal

Une réunion de canal public planifiée a la même liste d’applications que son équipe parente. L’installation d’une application dans une réunion de canal la rend également disponible dans l’équipe parente, et vice versa.

Toutefois, les instances d’onglet d’une réunion de canal sont distinctes des onglets du canal lui-même. Par exemple, supposons qu’un canal *de développement* ait un onglet *Polly* . Si vous *créez* une réunion autonome dans ce canal, cette réunion n’a pas d’onglet *Polly* tant que vous n’avez pas ajouté explicitement [l’onglet à la réunion](#meeting-details-view).

Dans les réunions de canal planifiées publiques, après l’ajout d’un onglet de réunion, vous pouvez sélectionner l’objet de réunion dans la page de détails de la réunion pour accéder à l’onglet.

:::image type="content" source="~/assets/images/apps-in-meetings/after-a-meeting1.png" alt-text="Après une réunion":::

> [!NOTE]
> Sur les appareils mobiles, les utilisateurs anonymes ne peuvent pas accéder aux applications dans les réunions de canal public planifiées.

### <a name="app-manifest-settings-for-tabs-in-meeting"></a>Paramètres de manifeste d’application pour les onglets dans la réunion

Mettez à jour le [manifeste de votre application](/microsoftteams/platform/resources/schema/manifest-schema) avec la propriété de contexte appropriée pour configurer les différents affichages d’onglets. Les fonctionnalités de l’application réunions sont déclarées dans le manifeste de votre application à l’aide des étendues et des tableaux de contexte sous la section configurableTabs.

#### <a name="scope"></a>Portée

L’étendue définit qui peut accéder aux applications.

* `groupchat` l’étendue rend votre application disponible dans une étendue de groupe et permet d’ajouter l’application dans un appel ou une réunion (réunion privée planifiée ou réunions instantanées).

* `team` rend votre application disponible dans une étendue d’équipe et permet d’ajouter votre application dans une réunion d’équipe, de canal ou de canal planifiée.

#### <a name="context"></a>Contexte

La `context` propriété détermine si l’application est disponible dans un affichage spécifique après l’installation et la configuration. Voici les valeurs de la `context` propriété à partir de laquelle vous pouvez utiliser la totalité ou une partie des valeurs :

|Valeur|Description|
|---|---|
| **channelTab** | Onglet dans l’en-tête d’un canal d’équipe |
| **privateChatTab** | Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs, et non dans le contexte d’une équipe ou d’une réunion. |
| **meetingChatTab** | Un onglet dans l'en-tête d'une conversation de groupe entre un ensemble d'utilisateurs pour une réunion planifiée. Vous pouvez spécifier soit **meetingChatTab** ou **meetingDetailsTab** pour vous assurer que les applications fonctionnent sur mobile. |
| **meetingDetailsTab** | Un onglet dans l'en-tête de la vue des détails de la réunion du calendrier. Vous pouvez spécifier soit **meetingChatTab** ou **meetingDetailsTab** pour vous assurer que les applications fonctionnent sur mobile. |
| **meetingSidePanel** | Un panneau en réunion s'est ouvert à travers le bar unifié (U-bar). |
| **meetingStage** | Une application de `meetingSidePanel` peut être partagée à l'étape de la réunion. Vous ne pouvez pas utiliser cette application sur les clients mobiles ou de salle Teams. |

#### <a name="configure-tab-app-for-a-meeting"></a>Configurer l’application onglet pour une réunion

Les applications dans les réunions peuvent utiliser les contextes suivants : `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` et `meetingStage`. Une fois qu’un participant à la réunion a installé une application et configuré l’onglet dans la réunion, tous les autres contextes ciblés de l’application pour la réunion donnée commencent à afficher l’onglet.

L’extrait de code suivant est un exemple d’onglet configurable utilisé dans une application pour les réunions Teams :

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

---

#### <a name="other-examples"></a>Autres exemples

Le contexte par défaut des onglets (s’il n’est pas spécifié) est le suivant :  

```json
"context":[ 
  "channelTab", 
  "privateChatTab", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

Pour empêcher l’affichage d’une application dans des conversations de groupe hors réunion, vous devez définir le contexte suivant :

```json
"context":[ 
  "meetingSidePanel", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

Pour une expérience de panneau côté réunion uniquement :  

```json
"context":[ 
  "meetingSidePanel" 
     ] 
```

### <a name="advanced-tab-sdk-apis"></a>API du Kit de développement logiciel (SDK) Onglet avancé

Le Kit de développement logiciel (SDK) client JavaScript De Microsoft Teams est un kit de développement logiciel (SDK) enrichi utilisé pour créer des onglets à l’aide de JavaScript. Utilisez la dernière version de TeamsJS (V.2.0 ou version ultérieure) pour travailler dans Teams, Office et Outlook. Pour plus d’informations, consultez [Kit de développement logiciel (SDK) client JavaScript Teams](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk?tabs=javascript%2Cmanifest-teams-toolkit).

### <a name="frame-context"></a>Contexte d’image

La bibliothèque JavaScript de Microsoft Teams expose le frameContext dans lequel l’URL de l’onglet réunion est chargée dans l’API getContext. Les valeurs possibles de frameContext sont content, task, setting, remove, sidePanel et meetingStage. Cela vous permet de créer des expériences personnalisées en fonction de l’endroit où l’application s’affiche. Par exemple, l’affichage d’une interface utilisateur spécifique axée sur la collaboration dans l’interface `meetingStage` utilisateur de préparation de réunion et une autre dans l’onglet de conversation (`content`). Pour plus d’informations, consultez [l’API getContext](/microsoftteams/platform/tabs/how-to/access-teams-context?tabs=teamsjs-v2).

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Application de réunion | Démontre comment utiliser l'application Meeting Token Generator pour demander un jeton. Le jeton est généré de manière séquentielle afin que chaque participant ait une occasion équitable de contribuer à une réunion. Ce jeton est utile dans des situations telles que les réunions de mêlée et les séances de questions-réponses. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Exemple de phase de réunion | Exemple d’application pour afficher un onglet dans la phase de réunion pour la collaboration | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| Panneau latéral de la réunion | Exemple d’application pour montrer comment ajouter un ordre du jour dans un panneau latéral de la réunion | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|
| Notification en réunion | Montre comment implémenter une notification en réunion à l’aide du bot. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| Signature de document en réunion | Montre comment implémenter une application Teams de signature de document. Inclut le partage de contenu d’application spécifique à l’étape, l’authentification unique Teams et la vue d’étape spécifique à l’utilisateur. | [View](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | N/A |

> [!NOTE]
>
> * Les applications de réunion (panneau latéral et étape de réunion) sont prises en charge dans le client de bureau Teams.
> * Les applications de réunion (panneau latéral et étape de réunion) dans le client web Teams sont prises en charge uniquement lorsque la [préversion du développeur est activée](/microsoftteams/platform/resources/dev-preview/developer-preview-intro#enable-developer-preview).

## <a name="step-by-step-guides"></a>Guides détaillés

* Suivez le [guide pas à pas](../sbs-meeting-token-generator.yml) pour générer un jeton de réunion dans votre réunion Teams.
* Suivez le [guide pas à pas](../sbs-meetings-sidepanel.yml) pour générer le panneau côté réunion dans votre réunion Teams.
* Suivez le [guide pas à pas](../sbs-meetings-stage-view.yml) pour partager l’affichage de la vue des étapes dans votre réunion Teams.
* Suivez le [guide pas à pas](../sbs-meeting-content-bubble.yml) pour générer une notification en réunion dans votre réunion Teams.

## <a name="see-also"></a>Voir aussi

* [Instructions de conception des notifications en réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Flux d’authentification Microsoft Teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Instructions de conception de l’expérience de la fenêtre de partage partagée](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Ajouter des applications aux réunions via Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
