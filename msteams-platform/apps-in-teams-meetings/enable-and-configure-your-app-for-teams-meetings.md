---
title: Créer des applications pour les réunions Teams > Activer et configurer vos applications pour les réunions Teams
author: surbhigupta
description: Découvrez comment activer et configurer vos applications pour les réunions Teams et différents scénarios de réunion, mettre à jour le manifeste de l’application, configurer les fonctionnalités, etc.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: b551513d61e7bb9ab2b9c118f756b3ce5232dde4
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537583"
---
# <a name="enable-and-configure-apps-for-meetings"></a>Activer et configurer les applications pour les meetings

Chaque équipe a une façon différente de communiquer et de collaborer des tâches. Pour effectuer ces différentes tâches, personnalisez Teams avec des applications pour les réunions. Activez vos applications pour Teams réunions et configurez-les pour qu’elles soient disponibles dans l’étendue de la réunion dans leur manifeste d’application.

## <a name="prerequisites"></a>Configuration requise

Avec les applications pour Teams réunions, vous pouvez étendre les fonctionnalités de vos applications tout au long du cycle de vie des réunions. Avant de travailler avec des applications pour Teams réunions, vous devez remplir les conditions préalables suivantes :

* Savoir comment développer des applications Teams Pour plus d’informations sur le développement de l’application Teams, consultez [développement de l’application Teams](../overview.md).

* Utilisez votre application qui prend en charge les onglets configurables dans l’étendue groupchat et/ou d’équipe. Pour plus d’informations, consultez [les étendues](../resources/schema/manifest-schema.md#configurabletabs) et [générez votre première application onglet](../build-your-first-app/build-channel-tab.md).

* Respectez [les instructions générales de conception des onglets Teams pour les scénarios](../tabs/design/tabs.md) de pré-réunion et de post-réunion. Pour obtenir des expériences pendant les réunions, [reportez-vous aux instructions de conception de l’onglet en réunion](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) et [aux instructions de conception des dialogues en réunion](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).

* Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités événementielles de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue en réunion et d’autres étapes au cours du cycle de vie de la réunion. Pour la boîte de dialogue en réunion, consultez `completionBotId` le paramètre dans la [charge utile de notification dans la réunion](API-references.md#send-an-in-meeting-notification).

## <a name="enable-your-app-for-teams-meetings"></a>Activer votre application pour Teams réunions

Pour activer votre application pour Teams réunions, mettez à jour le manifeste de votre application et utilisez les propriétés de contexte pour déterminer où votre application doit apparaître.

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de l’application

Les fonctionnalités de l’application de réunions sont déclarées dans le manifeste de votre application à l’aide des `configurableTabs`tableaux , `scopes`et `context` des tableaux. L’étendue définit qui peut accéder et le contexte définit l’emplacement où votre application est disponible.

> [!NOTE]
>
> * Les applications dans les réunions nécessitent ou `team` s’appliquent `groupchat` à l’étendue. L’étendue `team` fonctionne pour les onglets dans les canaux ou les réunions de canal.
> * Pour prendre en charge l’ajout d’onglets dans des réunions de canal planifiées, spécifiez l’étendue de **l’équipe** dans **la section Étendues** dans le manifeste de votre application. Sans étendue **d’équipe** , l’application n’apparaîtrait pas dans le menu volant pour les réunions de canal.
> * Les applications dans les réunions peuvent utiliser les contextes suivants : `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` et `meetingStage`.
> * Les autorisations `MeetingStage.Write.Chat` RSC déléguées et `ChannelMeetingStage.Write.Group` sont requises dans le manifeste pour activer le partage de la phase de réunion.

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

### <a name="context-property"></a>Propriété du contexte

La propriété`context` détermine ce qui doit être affiché lorsqu'un utilisateur appelle une application dans une réunion en fonction de l'endroit où l'utilisateur appelle l'application. L’onglet `context` et `scopes` les propriétés vous permettent de déterminer où votre application doit apparaître. Les onglets de l’étendue ou `groupchat` de l’étendue `team` peuvent avoir plusieurs contextes.

Prenez en charge l’étendue `groupchat` pour activer votre application dans les conversations de pré-réunion et de post-réunion. Grâce à l'expérience des applications de pré-réunion, vous pouvez trouver et ajouter des applications de réunion et effectuer les tâches de pré-réunion. L'expérience de l'application post-réunion vous permet d'afficher les résultats de la réunion, tels que les résultats des sondages ou les honoraires.

 Voici les valeurs de la `context` propriété à partir de laquelle vous pouvez utiliser la totalité ou une partie des valeurs :

|Valeur|Description|
|---|---|
| **channelTab** | Onglet dans l’en-tête d’un canal d’équipe |
| **privateChatTab** | Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs, et non dans le contexte d’une équipe ou d’une réunion. |
| **meetingChatTab** | Un onglet dans l'en-tête d'une conversation de groupe entre un ensemble d'utilisateurs pour une réunion planifiée. Vous pouvez spécifier soit **meetingChatTab** ou **meetingDetailsTab** pour vous assurer que les applications fonctionnent sur mobile. |
| **meetingDetailsTab** | Un onglet dans l'en-tête de la vue des détails de la réunion du calendrier. Vous pouvez spécifier soit **meetingChatTab** ou **meetingDetailsTab** pour vous assurer que les applications fonctionnent sur mobile. |
| **meetingSidePanel** | Un panneau en réunion s'est ouvert à travers le bar unifié (U-bar). |
| **meetingStage** | Une application de `meetingSidePanel` peut être partagée à l'étape de la réunion. Vous ne pouvez pas utiliser cette application sur les clients mobiles ou de salle Teams. |

Une fois que vous avez activé votre application pour Teams réunions, vous devez configurer votre application avant une réunion, pendant une réunion et après une réunion.

## <a name="configure-your-app-for-meeting-scenarios"></a>Configurer votre application pour les scénarios de réunion

Teams réunions offre une expérience collaborative à votre organisation. Configurez votre application pour différents scénarios de réunion et pour améliorer l’expérience de réunion. Vous pouvez maintenant identifier les actions qui peuvent être effectuées dans les scénarios de réunion suivants :

* [Avant une réunion](#before-a-meeting)
* [Lors d'une réunion](#during-a-meeting)
* [Après une réunion](#after-a-meeting)

### <a name="before-a-meeting"></a>Avant une réunion

Avant une réunion, les utilisateurs peuvent ajouter des onglets, des bots et des extensions de message. Les utilisateurs disposant de rôles d’organisateur et de présentateur peuvent ajouter des onglets à une réunion.

Pour ajouter un onglet à une réunion :

1. Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.
1. Sélectionnez l’onglet **Détails** , puis sélectionnez <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting1.png" alt="Pre-meeting experience" width="900"/>

1. Dans la galerie d’onglets qui s’affiche, sélectionnez l’application que vous souhaitez ajouter et suivez les étapes nécessaires. L’application est installée sous forme d’onglet.

Pour ajouter une extension de message à une réunion :

1. Sélectionnez les points de suspension &#x25CF;&#x25CF;&#x25CF; situés dans la zone de composition du message dans la conversation.
1. Sélectionnez l’application que vous souhaitez ajouter et suivez les étapes nécessaires. L’application est installée en tant qu’extension de message.

Pour ajouter un bot à une réunion :

Dans une conversation de réunion, entrez la **@** clé et sélectionnez **Obtenir des bots**.

> [!NOTE]
>
> * La boîte de dialogue en réunion affiche une boîte de dialogue dans une réunion et publie simultanément une carte adaptative dans la conversation de réunion auxquelles les utilisateurs peuvent accéder. La carte adaptative dans la conversation de réunion aide les utilisateurs lors de la participation à la réunion ou si l’application Teams est réduite.
> * L’identité de l’utilisateur doit être confirmée à l’aide de [l’authentification unique des onglets](../tabs/how-to/authentication/tab-sso-overview.md). Après l’authentification, l’application peut récupérer le rôle d’utilisateur à l’aide de l’API `GetParticipant` .
> * En fonction du rôle d’utilisateur, l’application peut fournir des expériences spécifiques au rôle. Par exemple, une application d’interrogation autorise uniquement les organisateurs et les présentateurs à créer un sondage.
> * Les attributions de rôles peuvent être modifiées pendant qu’une réunion est en cours. Pour plus d’informations, consultez [Partager du contenu dans une réunion Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### <a name="during-a-meeting"></a>Lors d'une réunion

Pendant une réunion, vous pouvez utiliser la notification ou la `meetingSidePanel` notification en réunion pour créer des expériences uniques pour vos applications.

#### <a name="meeting-sidepanel"></a>SidePanel de réunion

Le `meetingSidePanel` vous permet de personnaliser les expériences d’une réunion qui permettent aux organisateurs et aux présentateurs d’avoir différents ensembles de vues et d’actions. Dans le manifeste de votre application, vous devez l’ajouter `meetingSidePanel` au tableau de contextes. Dans la réunion et dans tous les scénarios, l’application est affichée dans un onglet de la réunion de 320 pixels de largeur. Pour plus d'informations, consultez l'[interface FrameInfo](/javascript/api/@microsoft/teams-js/frameinfo) (connue sous le nom de `FrameContext` avant TeamsJS v.2.0.0).

Vous pouvez [utiliser le contexte de l'utilisateur pour acheminer les requêtes](../tabs/how-to/access-teams-context.md#user-context). Pour plus d’informations, consultez [Flux d’authentification Teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md). Le flux d’authentification pour les onglets est similaire au flux d’authentification pour les sites web. Les onglets peuvent utiliser OAuth 2.0 directement. Pour plus d'informations, consultez[Plateforme d'identité Microsoft et flux de code d'autorisation OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

L’extension de message fonctionne comme prévu lorsqu’un utilisateur est en mode réunion. L’utilisateur peut publier des cartes d’extension de message de composition. AppNameen réunion est une info-bulle qui indique le nom de l’application dans la barre U de la réunion.

> [!NOTE]
> Utilisez la version 1.7.0 ou ultérieure de [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), car les versions antérieures ne prennent pas en charge le panneau latéral.

#### <a name="in-meeting-notification"></a>Notification en réunion

La notification en réunion est utilisée pour impliquer les participants pendant la réunion et collecter des informations ou des commentaires pendant la réunion. Utilisez une [charge utile de notification en réunion](API-references.md#send-an-in-meeting-notification) pour déclencher une notification en réunion. Dans le cadre de la charge utile de la demande de notification, incluez l’URL où le contenu à afficher est hébergé.

La notification en réunion ne doit pas utiliser le module de tâche. Le module de tâche n’est pas appelé dans la conversation de la réunion. Une URL de ressource externe est utilisée pour afficher la notification en réunion. Vous pouvez utiliser la `submitTask` méthode pour envoyer des données dans une conversation de réunion.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="Exemple montrant comment utiliser une boîte de dialogue en réunion.":::

Vous pouvez également ajouter l’image d’affichage Teams et la carte de contacts de l’utilisateur à la notification en réunion en fonction du jeton `onBehalfOf` avec l’utilisateur NULL et le nom d’affichage transmis dans la charge utile. Voici un exemple de charge utile :

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="Exemple montrant comment l’image d’affichage Teams et la carte de contacts sont utilisées avec la boîte de dialogue en réunion." border="true":::

#### <a name="shared-meeting-stage"></a>Étape de réunion partagée

La phase de réunion partagée permet aux participants à la réunion d’interagir et de collaborer sur le contenu de l’application en temps réel. Vous pouvez partager vos applications à l’étape de la réunion collaborative des manières suivantes :

* [Partagez l’intégralité de l’application pour effectuer une étape à](#share-entire-app-to-stage) l’aide du bouton Partager pour mettre en scène dans le panneau côté réunion du client Teams ou via [[liens profonds](#generate-a-deep-link-to-share-content-to-stage-in-meetings).
* [Partagez des parties spécifiques de l’application pour effectuer des étapes à](#share-specific-parts-of-the-app-to-stage) l’aide d’API dans le SDK client Teams.

##### <a name="share-entire-app-to-stage"></a>Partager l’intégralité de l’application en plusieurs étapes

Les participants peuvent partager l'ensemble de l'application avec la scène de la réunion collaborative en utilisant le bouton Partager la scène du panneau latéral de l'application.

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

Pour partager l’ensemble de l’application à mettre en scène, dans le manifeste de l’application, vous devez configurer `meetingStage` et `meetingSidePanel` en tant que contextes d’image. Par exemple :

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

Pour plus d'informations, voir [app manifest](../resources/schema/manifest-schema-dev-preview.md#configurabletabs)

##### <a name="share-specific-parts-of-the-app-to-stage"></a>Partager des parties spécifiques de l’application à mettre en scène

Les participants peuvent partager des parties spécifiques de l'application vers la fenêtre de partage collaborative en utilisant les API de partage vers la scène. Les API sont disponibles dans le SDK du client Teams et sont invoquées à partir du panneau latéral de l'application.

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

Pour partager des parties spécifiques de l'application sur scène, vous devez invoquer les API correspondantes dans la bibliothèque SDK du client Teams. Pour plus d'informations, consultez la [référence de l’API](API-references.md).

> [!NOTE]
>
> * Pour partager des parties spécifiques de l’application à mettre en scène, utilisez Teams manifeste version 1.12 ou ultérieure.
> * Vous pouvez partager des parties spécifiques de l’application pour la phase de réunion uniquement sur les clients de bureau Teams. Les utilisateurs mobiles peuvent partager des parties spécifiques de l’application à mettre en scène à l’aide de [l’API share to stage](API-references.md#share-app-content-to-stage-api).

### <a name="after-a-meeting"></a>Après une réunion

Les configurations d’après et [d’avant les réunions sont les mêmes](#before-a-meeting) .

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Générer un lien profond pour partager du contenu à mettre en scène dans les réunions

Vous pouvez également générer un lien profond pour [partager l’application afin de](#share-entire-app-to-stage) mettre en scène et de démarrer ou de participer à une réunion.

> [!NOTE]
>
> * Actuellement, le lien profond vers le partage de contenu pour effectuer des étapes dans les réunions fait l’objet d’améliorations de l’expérience utilisateur et n’est disponible qu’en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).
> * Le lien profond permettant de partager du contenu vers une phase de réunion est pris en charge uniquement dans le client de bureau Teams.

Lorsqu’un lien profond est sélectionné dans une application par un utilisateur qui fait partie d’une réunion en cours, l’application est partagée à l’étape et une fenêtre contextuelle d’autorisation s’affiche. Les utilisateurs peuvent accorder l’accès aux participants pour collaborer avec une application.

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="La capture d’écran est un exemple montrant une fenêtre contextuelle d’autorisation.":::

Lorsqu’un utilisateur ne participe pas à une réunion, il est redirigé vers le calendrier Teams où il peut participer à une réunion ou lancer une réunion instantanée (Réunion maintenant).

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="La capture d’écran est un exemple montrant une fenêtre contextuelle lorsqu’il n’y a pas de réunion en cours.":::

Une fois que l’utilisateur a lancé une réunion instantanée (Réunion maintenant), il peut ajouter des participants et interagir avec l’application.

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="La capture d’écran est un exemple qui montre une option pour ajouter des participants et comment interagir avec l’application.":::

Pour ajouter un lien profond pour partager du contenu sur scène, vous devez disposer d’un contexte d’application. Le contexte d’application permet au client Teams d’extraire le manifeste de l’application et de vérifier si le partage sur scène est possible. Voici un exemple de contexte d’application.

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

Les paramètres de requête pour le contexte d’application sont les suivants :

* `appID`: il s’agit de l’ID qui peut être obtenu à partir du manifeste de l’application.
* `appSharingUrl`: l’URL qui doit être partagée sur scène doit être un domaine valide défini dans le manifeste de l’application. Si l’URL n’est pas un domaine valide, une boîte de dialogue d’erreur s’affiche pour fournir à l’utilisateur une description de l’erreur.
* `useMeetNow`: cela inclut un paramètre booléen qui peut être vrai ou faux.
  * **True** : lorsque la `UseMeetNow` valeur est true et s’il n’y a pas de réunion en cours, une nouvelle réunion De réunion maintenant est lancée. Quand une réunion est en cours, cette valeur est ignorée.

  * **False** : la valeur `UseMeetNow` par défaut est false, ce qui signifie que lorsqu’un lien profond est partagé vers une phase et qu’il n’y a pas de réunion en cours, une fenêtre contextuelle de calendrier s’affiche. Toutefois, vous pouvez partager directement pendant une réunion.

Vérifiez que tous les paramètres de requête sont correctement encodés en URI et que le contexte de l’application doit être encodé deux fois dans l’URL finale. Voici un exemple :

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

Un lien profond peut être lancé à partir du web Teams ou du client de bureau Teams.

* **Web Teams** : utilisez le format suivant pour lancer un lien profond à partir du site web Teams pour partager du contenu sur scène.

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    Exemple : `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Lien profond|Format|Exemple|
    |---------|---------|---------|
    |Pour partager l’application et ouvrir le calendrier Teams, lorsque UseMeeetNow a la **valeur false**, par défaut.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Pour partager l’application et lancer une réunion instantanée, lorsque UseMeeetNow a **la valeur true**.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Client de bureau d’équipe** : utilisez le format suivant pour lancer un lien profond à partir du client de bureau Teams pour partager du contenu sur scène.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Exemple : `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Lien profond|Format|Exemple|
    |---------|---------|---------|
    |Pour partager l’application et ouvrir le calendrier Teams, lorsque UseMeeetNow a la **valeur false**, par défaut.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Pour partager l’application et lancer une réunion instantanée, lorsque UseMeeetNow a **la valeur true**.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

Les paramètres de requête sont les suivants :

* `deepLinkId`: tout identificateur utilisé pour la corrélation de télémétrie.
* `fqdn`: `fqdn` est un paramètre facultatif, qui peut être utilisé pour basculer vers un environnement approprié d’une réunion pour partager une application sur scène. Il prend en charge les scénarios dans lesquels un partage d’application spécifique se produit dans un environnement particulier. La valeur par défaut est l’URL d’entreprise `fqdn` et les valeurs possibles sont `Teams.live.com` pour Teams for Life, `teams.microsoft.com`ou `teams.microsoft.us`.

Pour partager l’intégralité de l’application à l’étape, dans le manifeste de l’application, vous devez configurer `meetingStage` et `meetingSidePanel` , en tant que contextes d’image, voir [le manifeste de l’application](../resources/schema/manifest-schema.md). Dans le cas contraire, les participants à la réunion peuvent ne pas être en mesure de voir le contenu sur scène.

> [!NOTE]
> Pour que votre application réussisse la validation, lorsque vous créez un lien profond à partir de votre site web, de votre application web ou de votre carte adaptative, utilisez **Share in meeting** comme chaîne ou copie.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Application de réunion | Démontre comment utiliser l'application Meeting Token Generator pour demander un jeton. Le jeton est généré de manière séquentielle afin que chaque participant ait une occasion équitable de contribuer à une réunion. Ce jeton est utile dans des situations telles que les réunions de mêlée et les séances de questions-réponses. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|Exemple de phase de réunion | Exemple d’application pour afficher un onglet dans la phase de réunion pour la collaboration | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|Panneau latéral de la réunion | Exemple d’application pour montrer comment ajouter un ordre du jour dans un panneau latéral de la réunion | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>Guides détaillés

* Suivez le [guide pas à pas](../sbs-meeting-token-generator.yml) pour générer un jeton de réunion dans votre réunion Teams.
* Suivez le [guide pas à pas](../sbs-meetings-sidepanel.yml) pour générer un panneau latéral de réunion dans votre réunion Teams.
* Suivez le [guide pas à pas](../sbs-meetings-stage-view.yml) pour partager l’affichage de la vue des étapes dans votre réunion Teams.
* Suivez le [guide pas à pas](../sbs-meeting-content-bubble.yml) pour générer une bulle de contenu de réunion dans votre réunion Teams.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Références API des applications de réunion](API-references.md)

## <a name="see-also"></a>Voir aussi

* [Instructions de conception de boîte de dialogue en réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Flux d’authentification Microsoft Teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Instructions de conception de l’expérience de la fenêtre de partage partagée](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Ajouter des applications aux réunions via Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
