---
title: Créer des liens plus étroits
description: Découvrez comment décrire les liens profonds Teams et comment les utiliser dans vos applications.
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 750fc8f6153cf64fa585e3d74d73afba483aafb0
ms.sourcegitcommit: f7d0e330c96e00b2031efe6f91a0c67ab0976455
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/20/2022
ms.locfileid: "65611456"
---
# <a name="create-deep-links"></a>Créer des liens plus étroits

Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Les scénarios dans lesquels la création de liens profonds est utile sont les suivants :

* Navigation de l’utilisateur vers le contenu dans l’un des onglets de votre application. Par exemple, votre application peut avoir un bot qui envoie des messages informant l’utilisateur d’une activité importante. Lorsque l’utilisateur appuie sur la notification, le lien profond accède à l’onglet afin que l’utilisateur puisse afficher plus de détails sur l’activité.
* Votre application automatise ou simplifie certaines tâches utilisateur, telles que la création d’une conversation ou la planification d’une réunion, en préremplissant les liens profonds avec les paramètres requis. Cela évite aux utilisateurs d’entrer manuellement des informations.

> [!NOTE]
>
> Un lien profond lance d’abord le navigateur avant d’accéder au contenu. Le comportement des liens profonds sur les entités Teams est le suivant :
>
> **Onglet** :   
> ✔ accède directement à l’URL de lien profond.
>
> **Bot** :   
> ✔ Deeplink dans le corps de la carte : s’ouvre d’abord dans le navigateur.  
> ✔ Deeplink ajouté à l’action OpenURL dans la carte adaptative : accède directement à l’URL de lien profond.  
> ✔ texte Markdown de lien hypertexte dans la carte : s’ouvre dans le navigateur en premier.  
>
> **Conversation** :   
> ✔ le markdown du lien hypertexte du message texte : accède directement à l’URL de lien profond.  
> ✔ Lien collé dans la conversation générale : accède directement à l’URL de lien profond.

## <a name="deep-linking-to-your-tab"></a>Liaison approfondie à votre onglet

Vous pouvez créer des liens profonds vers des entités dans Teams. Cela permet de créer des liens qui accèdent au contenu et aux informations dans votre onglet. Par exemple, si votre onglet contient une liste de tâches, les membres de l’équipe peuvent créer et partager des liens vers des tâches individuelles. Lorsque vous sélectionnez le lien, il accède à votre onglet qui se concentre sur l’élément spécifique. Pour implémenter cela, vous ajoutez une action **copier le lien** à chaque élément, de la manière la mieux adaptée à votre interface utilisateur. Lorsque l’utilisateur effectue cette action, vous appelez `shareDeepLink()` pour afficher une boîte de dialogue contenant un lien que l’utilisateur peut copier dans le Presse-papiers. Lorsque vous effectuez cet appel, vous transmettez également un ID pour votre élément, que vous revenez dans le [contexte](~/tabs/how-to/access-teams-context.md) lorsque le lien est suivi et que votre onglet est rechargé.

Vous pouvez également générer des liens profonds par programmation, en utilisant le format spécifié plus loin dans cet article. Vous pouvez utiliser des liens profonds dans [bot](~/bots/what-are-bots.md) et [connecteur](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages qui informent les utilisateurs des modifications apportées à votre onglet ou aux éléments qu’il contient.

> [!NOTE]
> Ce lien profond est différent des liens fournis par l’élément de menu **Copier vers l’onglet**, qui génère simplement un lien profond qui pointe vers cet onglet.

>[!IMPORTANT]
> Actuellement, shareDeepLink ne fonctionne pas sur les plateformes mobiles.

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>Afficher un lien ciblé vers un élément dans votre onglet

Pour afficher une boîte de dialogue qui contient un lien profond vers un élément dans votre onglet, appelez `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`.

Renseignez les champs suivants : 

* `subEntityId` : identificateur unique de l’élément dans votre onglet auquel vous effectuez une liaison approfondie.
* `subEntityLabel` : étiquette de l’élément à utiliser pour afficher le lien profond.
* `subEntityWebUrl` : champ facultatif avec une URL de secours à utiliser si le client ne prend pas en charge le rendu de l’onglet.

### <a name="generate-a-deep-link-to-your-tab"></a>Générer un lien ciblé vers votre onglet

> [!NOTE]
>
> * Les onglets personnels ont un `personal`scope, tandis que les onglets canal et groupe utilisent `team`or `group`scopes. Les deux types d’onglets ont une syntaxe légèrement différente, car seul l’onglet configurable a un `channel`propriété associé à son objet de contexte. Pour plus d’informations sur les étendues d’onglets, consultez la référence du [manifeste](~/resources/schema/manifest-schema.md).
> * Les liens profonds fonctionnent correctement uniquement si l’onglet a été configuré à l’aide de la bibliothèque v0.4 ou ultérieure et qu’en raison de cela a un ID d’entité. Les liens profonds vers des onglets sans ID d’entité accèdent toujours à l’onglet, mais ne peuvent pas fournir l’ID de sous-entité à l’onglet.

Utilisez le format suivant pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de message :

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si le bot envoie un message contenant un `TextBlock` avec un lien profond, un nouvel onglet de navigateur est ouvert lorsque l’utilisateur sélectionne le lien. Cela se produit dans Chrome et dans l’application de bureau Microsoft Teams, tous deux exécutés sur Linux.
> Si le bot envoie la même URL de lien profond dans un `Action.OpenUrl`, l’onglet Teams est ouvert dans l’onglet du navigateur actuel lorsque l’utilisateur sélectionne le lien. Aucun nouvel onglet de navigateur n’est ouvert.

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused. 
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* List items in the table are not formatted well in output.
* Some headings use -ing verbs.
* Example values and some URLs should be in backticks and not emphasized.
* Codeblock are missing language.
* Check for markdownlint errors.
* Table with just a row isn't really needed. Provide the content without tabulating it.
--->

Les paramètres de requête sont les suivants :

| Nom du paramètre | Description | Exemple |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | ID du Centre d’administration Teams. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | ID de l’élément dans l’onglet, que vous avez fourni lors de la [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).|Liste des tâches123|
| `entityWebUrl` ou `subEntityWebUrl`&emsp; | Champ facultatif avec une URL de secours à utiliser si le client ne prend pas en charge le rendu de l’onglet. | `https://tasklist.example.com/123` ou `https://tasklist.example.com/list123/task456` |
| `entityLabel` ou `subEntityLabel`&emsp; | Étiquette de l’élément dans votre onglet, à utiliser lors de l’affichage du lien profond. | Liste des tâches 123 ou » Tâche 456 |
| `context.subEntityId`&emsp; | ID de l’élément dans l’onglet. |Tâche456 |
| `context.channelId`&emsp; | ID de canal Microsoft Teams disponible à partir de l’onglet [contexte](~/tabs/how-to/access-teams-context.md). Cette propriété est disponible uniquement dans les onglets configurables avec une étendue d’**équipe**. Il n’est pas disponible dans les onglets statiques, qui ont une étendue **personnelle**.| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |
| `chatId`&emsp; | ChatId disponible à partir du [contexte](~/tabs/how-to/access-teams-context.md) d’onglet pour la conversation de groupe et de réunion | 17:b42de192376346a7906a7dd5cb84b673@thread.v2 |
| `contextType`&emsp; |  La conversation est le seul contextType pris en charge pour les réunions | conversation |

**Exemples** :

* Lien vers un onglet statique (personnel) lui-même :

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`

* Lien vers un élément de tâche dans l’onglet statique (personnel) :

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

* Lier à un onglet configurable lui-même : 

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* Lien vers un élément de tâche sous l’onglet configurable : 

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`

* Lien vers une application onglet ajoutée à une réunion ou une conversation de groupe :

    >`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456?context={"chatId": "17:b42de192376346a7906a7dd5cb84b673@thread.v2","contextType":"chat"}`

> [!IMPORTANT]
> Assurez-vous que tous les paramètres de requête sont encodés correctement en URI. Vous devez suivre les exemples précédents à l’aide du dernier exemple :
>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a>Utiliser un lien profond à partir d’un onglet

Lorsque vous accédez à un lien profond, Microsoft Teams accède simplement à l’onglet et fournit un mécanisme via la bibliothèque JavaScript de Microsoft Teams pour récupérer l’ID de sous-entité s’il existe.

L’appel [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-)retourne un contexte qui inclut le champ `subEntityId`si l’onglet est parcouru via un lien profond.

## <a name="deep-linking-from-your-tab"></a>Liaison approfondie à partir de votre onglet

Vous pouvez effectuer un lien profond vers du contenu dans Teams à partir de votre onglet. Cela est utile si votre onglet doit créer un lien vers d’autres contenus dans Teams, tels qu’un canal, un message, un autre onglet ou même pour ouvrir une boîte de dialogue de planification. Pour déclencher un lien profond à partir de votre onglet, appelez :

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Cet appel vous permet d’accéder à l’URL correcte ou de déclencher une action du client, telle que l’ouverture d’une boîte de dialogue de planification ou d’installation d’application. Prenons l’exemple suivant :

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Liaison approfondie à une conversation

Vous pouvez créer des liens profonds vers des conversations privées entre les utilisateurs en spécifiant l’ensemble des participants. Si aucune conversation n’existe avec les participants spécifiés, le lien dirige l’utilisateur vers une nouvelle conversation vide. Les nouvelles conversations sont créées dans un état brouillon jusqu’à ce que l’utilisateur envoie le premier message. Sinon, vous pouvez spécifier le nom de la conversation si elle n’existe pas déjà, ainsi que le texte qui doit être inséré dans la zone de composition de l’utilisateur. Vous pouvez considérer cette fonctionnalité comme un raccourci permettant à l’utilisateur d’effectuer l’action manuelle d’accéder à la conversation ou de la créer, puis de taper le message.

Par exemple, si vous renvoyez un profil utilisateur Office 365 à partir de votre bot sous forme de carte, ce lien profond peut permettre à l’utilisateur de discuter facilement avec cette personne.

### <a name="generate-a-deep-link-to-a-chat"></a>Générer un lien ciblé vers une conversation

Utilisez ce format pour un lien ciblé que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de message :

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Exemple : `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Les paramètres de requête sont les suivants :

* `users` : liste séparée par des virgules des ID d’utilisateur représentant les participants de la conversation. L’utilisateur qui effectue l’action est toujours inclus en tant que participant. Actuellement, le champ ID d’utilisateur prend en charge Microsoft Azure Active Directory Domain Services (Azure AD) UserPrincipalName, telle qu’une adresse e-mail uniquement.
* `topicName` : champ facultatif pour le nom complet de la conversation, dans le cas d’une conversation avec au moins trois utilisateurs. Si ce champ n’est pas spécifié, le nom complet de la conversation est basé sur les noms des participants.
* `message` : champ facultatif pour le texte du message que vous souhaitez insérer dans la zone de composition de l’utilisateur actuel lorsque la conversation est dans un état brouillon.

Pour utiliser ce lien profond avec votre bot, spécifiez-le comme cible d’URL dans le bouton de votre carte ou appuyez sur l’action via le type `openUrl`action.

## <a name="generate-deep-links-to-channel-conversation"></a>Générer des liens profonds vers la conversation du canal

Utilisez ce format de lien profond pour accéder à une conversation particulière dans le thread du canal :

`https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

Exemple : `https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

Les paramètres de requête sont les suivants :

* `channelId` : ID du canal de la conversation. Par exemple `19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2`.
* `tenantId` : ID de client tel que `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `groupId` : ID de groupe du fichier. Par exemple, `3606f714-ec2e-41b3-9ad1-6afb331bd35d`.
* `parentMessageId` : ID de message parent de la conversation.
* `teamName` : nom de l’équipe.
* `channelName` : nom du canal de l’équipe.

> [!NOTE]
> Vous pouvez voir `channelId`and `groupId` dans l’URL du canal.

## <a name="generate-deep-links-to-file-in-channel"></a>Générer des liens profonds vers un fichier dans le canal

Le format de lien profond suivant peut être utilisé dans un bot, un connecteur ou une carte d’extension de message :

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

Les paramètres de requête sont les suivants :

* `fileId` : ID de fichier unique de Sharepoint Online, également appelé `sourcedoc`. Par exemple,`1FA202A5-3762-4F10-B550-C04F81F6ACBD`.
* `tenantId` : ID de client tel que `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `fileType` : type de fichier pris en charge, tel que docx, pptx, xlsx et pdf.
* `objectUrl` : URL de l’objet du fichier. Le format est `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext`. Par exemple : `https://microsoft.sharepoint.com/teams/(filepath)`.
* `baseUrl` : URL de base du fichier. Le format est `https://{tenantName}.sharepoint.com/sites/{TeamName}`. Par exemple : `https://microsoft.sharepoint.com/teams`.
* `serviceName` : nom du service, ID d’application. Par exemple, `teams`.
* `threadId`: threadId est l’ID d’équipe de l’équipe où le fichier est stocké. Elle est facultative et ne peut pas être définie pour les fichiers stockés dans le dossier OneDrive d’un utilisateur. threadId : 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype.
* `groupId` : ID de groupe du fichier. Par exemple, `ae063b79-5315-4ddb-ba70-27328ba6c31e`.

> [!NOTE]
> Vous pouvez voir `threadId`and `groupId` dans l’URL du canal.  

Le format de lien profond suivant est utilisé dans un bot, un connecteur ou une carte d’extension de message :

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

L’exemple de format suivant illustre le lien profond vers les fichiers :

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a>Sérialisation de cet objet

```javascript
{
fileId: "5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80",
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```

## <a name="deep-linking-to-an-app"></a>Liaison profonde à une conversation

Créez des liens profonds pour l’application une fois l’application répertoriée dans le Magasin Teams. Pour créer un lien pour lancer Teams, ajoutez l’ID d’application à l’URL suivante : `https://teams.microsoft.com/l/app/<your-app-id>`. Une boîte de dialogue s’affiche pour installer l’application.
  
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>Liaison approfondie pour les onglets SharePoint Framework

Le format de lien profond suivant peut être utilisé dans un bot, un connecteur ou une carte d’extension de message : `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Lorsqu’un bot envoie un message TextBlock avec un lien ciblé, un nouvel onglet de navigateur s’ouvre lorsque les utilisateurs sélectionnent le lien. Cela se produit dans Chrome et l’application de bureau Microsoft Teams s’exécutant sur Linux.
> Si le bot envoie la même URL de lien profond dans un `Action.OpenUrl`, l’onglet Teams s’ouvre dans le navigateur actuel lorsque l’utilisateur sélectionne le lien. Aucun nouvel onglet de navigateur n’est ouvert.

Les paramètres de requête sont les suivants :

* `appID`: votre ID de manifeste, par exemple `fe4a8eba-2a31-4737-8e33-e5fae6fee194`.

* `entityID`: ID d’élément que vous avez fourni lors de la [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md). Par exemple, `tasklist123`.
* `entityWebUrl` : champ facultatif avec une URL de secours à utiliser si le client ne prend pas en charge le rendu de l’onglet – `https://tasklist.example.com/123` ou `https://tasklist.example.com/list123/task456`.
* `entityName` : étiquette de l’élément dans votre onglet, à utiliser lors de l’affichage du lien profond, Liste des tâches 123 ou la tâche 456.

Exemple : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList`

## <a name="deep-linking-to-the-scheduling-dialog"></a>Liaison approfondie à la boîte de dialogue de planification

> [!NOTE]
> Cette fonctionnalité est actuellement en préversion pour les développeurs.

Vous pouvez créer des liens profonds vers la boîte de dialogue de planification intégrée teams. Cela est particulièrement utile si votre application aide l’utilisateur à effectuer le calendrier ou à planifier les tâches associées.

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Générer un lien ciblé vers la boîte de dialogue de planification

Utilisez le format suivant pour un lien ciblé que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de message : `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Exemple : `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

> [!NOTE]
> Les paramètres de recherche ne prennent pas en charge `+`signal à la place de l’espace blanc (` `). Vérifiez que votre code d’encodage d’URI retourne `%20`for spaces, par exemple, `?subject=test%20subject` est correct, mais `?subject=test+subject` est incorrect.

Les paramètres de requête sont les suivants :

* `attendees` : liste facultative d’ID utilisateur séparés par des virgules représentant les participants de la réunion. L’utilisateur qui effectue l’action est l’organisateur de la réunion. Actuellement, le champ ID d’utilisateur prend uniquement en charge le Azure AD UserPrincipalName, généralement une adresse e-mail.
* `startTime` : heure de début facultative de l’événement. Il doit être au [format ISO 8601 long](https://en.wikipedia.org/wiki/ISO_8601), par exemple *2018-03-12T23:55:25+02:00*.
* `endTime` : heure de fin facultative de l’événement, également au format ISO 8601.
* `subject` : champ facultatif pour l’objet de la réunion.
* `content` : champ facultatif pour le champ détails de la réunion.

> [!NOTE]
> Actuellement, la spécification de l'emplacement n'est pas prise en charge. Vous devez spécifier le décalage UTC, c'est-à-dire les fuseaux horaires lors de la génération de vos heures de début et de fin.

Pour utiliser ce lien profond avec votre bot, vous pouvez le spécifier comme cible d’URL dans le bouton de votre carte ou appuyer sur l’action via le type `openUrl`action.

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>Liaison approfondie à un appel audio ou audio-vidéo

Vous pouvez créer des liens profonds pour appeler des appels audio uniquement ou audio-vidéo à un seul utilisateur ou à un groupe d’utilisateurs, en spécifiant le type d’appel, comme *audio* ou *av* et les participants. Une fois le lien profond appelé et avant de passer l’appel, le client Teams demande une confirmation pour effectuer l’appel. En cas d’appel de groupe, vous pouvez appeler un ensemble d’utilisateurs VoIP et un ensemble d’utilisateurs RTC dans le même appel de lien profond.

En cas d’appel vidéo, le client demande une confirmation et active la vidéo de l’appelant pour l’appel. Le destinataire de l’appel a le choix entre répondre par audio uniquement ou audio et vidéo, via la fenêtre de notification d’appel Teams.

> [!NOTE]
> Ce lien profond ne peut pas être utilisé pour appeler une réunion.

### <a name="generate-a-deep-link-to-a-call"></a>Générer un lien profond vers un appel

| Lien profond | Format | Exemple |
|-----------|--------|---------|
| Passer un appel audio | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com` |
| Effectuer des appels audio et vidéo | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true` |
|Passer un appel audio et vidéo avec une source de paramètre facultative | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true&source=demoApp` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp` |  
| Effectuer un appel audio et vidéo à une combinaison d’utilisateurs VoIP et RTC | `https://teams.microsoft.com/l/call/0/0?users=<user1>,4:<phonenumber>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210` |
  
Voici les paramètres de requête :

* `users` : liste d’identifiants d’utilisateur séparés par des virgules représentant les participants de l’appel. Actuellement, le champ ID utilisateur prend en charge le Azure AD UserPrincipalName, généralement une adresse e-mail, ou en cas d’appel RTC, il prend en charge un pstn url 4 :&lt;numéro de téléphone&gt;.
* `withVideo` : il s’agit d’un paramètre facultatif que vous pouvez utiliser pour effectuer un appel vidéo. La définition de ce paramètre active uniquement la caméra de l’appelant. Le destinataire de l’appel peut répondre par le biais d’un appel audio ou audio et vidéo via la fenêtre de notification d’appel Teams.
* `Source` : il s’agit d’un paramètre facultatif, qui informe sur la source du lien profond.

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|ID de sous-entité consommateur de liens profonds  |Exemple d’application Microsoft Teams pour illustrer le lien profond entre la conversation de bot et l’ID de sous-entité de consommation de tabulation.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Voir aussi

* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
* [Moodle LMS](~/resources/moodleinstructions.md)
