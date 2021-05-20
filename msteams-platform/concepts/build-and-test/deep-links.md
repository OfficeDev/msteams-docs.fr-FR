---
title: Créer des liens plus étroits
description: Décrit les liens profonds et la façon de les utiliser dans vos applications
ms.topic: how-to
localization_priority: Normal
keywords: équipes lien profond deeplink
ms.openlocfilehash: 837d180b06f69b9be49d898c62b9ab8ee64d51d0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566053"
---
# <a name="create-deep-links"></a>Créer des liens plus étroits 

Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Les scénarios où la création de liens profonds sont utiles sont les suivants :

* Naviguer l’utilisateur vers le contenu dans l’un des onglets de votre application. Par exemple, votre application peut avoir un bot qui envoie des messages informant l’utilisateur d’une activité importante. Lorsque l’utilisateur tape sur la notification, le lien profond navigue vers l’onglet afin que l’utilisateur puisse afficher plus de détails sur l’activité.
* Votre application automatise ou simplifie certaines tâches de l’utilisateur, telles que la création d’un chat ou la planification d’une réunion, en prépulant les liens profonds avec les paramètres requis. Cela évite aux utilisateurs d’entrer manuellement des informations.

> [!NOTE]
>
> Un deeplink lance le navigateur d’abord avant de naviguer vers le contenu. Le comportement des liens profonds sur Teams entités sont les suivants :
>
> **Onglet**:  
> ✔ navigue directement vers l’url deeplink.
>
> **Bot**:  
> ✔ Deeplink dans le corps de la carte: S’ouvre dans le navigateur d’abord.  
> ✔ Deeplink ajouté à l’action OpenURL dans Adaptive Card : navigue directement vers l’url deeplink.  
> ✔ texte de balisage Hyperlink dans la carte : s’ouvre d’abord dans le navigateur.  
>
> **Chat**:  
> ✔ message texte hyperlien markdown: Navigue directement vers l’url deeplink.  
> ✔ lien passé dans la conversation de chat en général: Navigue directement vers l’url deeplink.

## <a name="deep-linking-to-your-tab"></a>Lien profond vers votre onglet

Vous pouvez créer des liens profonds avec des entités en Teams. Ceci est utilisé pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Par exemple, si votre onglet contient une liste de tâches, les membres de l’équipe peuvent créer et partager des liens vers des tâches individuelles. Lorsque vous sélectionnez le lien, il navigue vers votre onglet qui se concentre sur l’élément spécifique. Pour implémenter cela, vous ajoutez une action **de lien** de copie à chaque élément, de quelque manière que ce soit convient le mieux à votre interface utilisateur. Lorsque l’utilisateur prend cette mesure, vous appelez `shareDeepLink()` pour afficher une boîte de dialogue contenant un lien que l’utilisateur peut copier sur le presse-papiers. Lorsque vous passez cet appel, vous passez également un ID pour votre élément, que vous obtenez dans [le contexte lorsque](~/tabs/how-to/access-teams-context.md) le lien est suivi et que votre onglet est rechargé.

Alternativement, vous pouvez également générer des liens profonds programmatiquement, en utilisant le format spécifié plus tard dans ce sujet. Vous pouvez utiliser des liens profonds dans [les](~/bots/what-are-bots.md) messages [bot et connecteur](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) qui informent les utilisateurs sur les modifications apportées à votre onglet, ou aux éléments qui s’y trouvent.

> [!NOTE]
> Ce lien profond est différent des liens fournis par le lien **Copie à l’élément** de menu onglet, qui génère juste un lien profond qui pointe vers cet onglet.

>[!NOTE]
> Actuellement, shareDeepLink ne fonctionne pas sur les plateformes mobiles.

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>Afficher un lien profond vers un élément de votre onglet

Pour afficher une boîte de dialogue qui contient un lien profond vers un élément de votre onglet, appelez `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` .

Fournir les champs suivants :

* `subEntityId`: Un identificateur unique pour l’élément dans votre onglet auquel vous êtes en lien profond.
* `subEntityLabel`: Une étiquette pour l’élément à utiliser pour afficher le lien profond.
* `subEntityWebUrl`: Un champ optionnel avec une URL de repli à utiliser si le client ne prend pas en charge le rendu de l’onglet.

### <a name="generate-a-deep-link-to-your-tab"></a>Générer un lien profond vers votre onglet

> [!NOTE]
> Les onglets personnels ont une `personal` portée, tandis que les onglets de canal et de groupe utilisent `team` ou des `group` étendues. Les deux types d’onglets ont une syntaxe légèrement différente puisque seul l’onglet configurable a `channel` une propriété associée à son objet contexteur. Consultez la référence [manifeste pour](~/resources/schema/manifest-schema.md) plus d’informations sur les étendues d’onglets.

> [!NOTE]
> Les liens profonds ne fonctionnent correctement que si l’onglet a été configuré à l’aide de la bibliothèque v0.4 ou plus tard et à cause de cela a un ID d’entité. Les liens profonds vers les onglets sans identifiants d’entité naviguent toujours vers l’onglet, mais ne peuvent pas fournir l’ID de la sous-entité à l’onglet.

Utilisez le format suivant pour un lien profond que vous pouvez utiliser dans une carte d’extension de bot, connecteur ou messagerie :

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si le bot envoie un message contenant un lien `TextBlock` profond, alors un nouvel onglet de navigateur est ouvert lorsque l’utilisateur sélectionne le lien. Cela se produit dans Chrome et dans l’application Microsoft Teams bureau, toutes deux fonctionnant sous Linux.
> Si le bot envoie la même URL de lien profond dans un `Action.OpenUrl` , alors l’onglet Teams est ouvert dans l’onglet du navigateur actuel lorsque l’utilisateur sélectionne le lien. Un nouvel onglet navigateur n’est pas ouvert.

Les paramètres de requête sont les :

| Nom du paramètre | Description | Exemple |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | L’identité de votre manifeste. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | L’ID pour l’élément dans l’onglet, que vous avez fourni lors [de la configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).|Tasklist123 (en)|
| `entityWebUrl` ou `subEntityWebUrl`&emsp; | Un champ optionnel avec une URL de repli à utiliser si le client ne prend pas en charge le rendu de l’onglet. | https://tasklist.example.com/123 ou https://tasklist.example.com/list123/task456 |
| `entityLabel` ou `subEntityLabel`&emsp; | Une étiquette pour l’élément dans votre onglet, à utiliser lors de l’affichage du lien profond. | Liste de tâches 123 ou « Tâche 456 |
| `context`&emsp; </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| Un objet JSON contenant les champs suivants :</br></br> * Un ID pour l’élément dans l’onglet. </br></br> * L’Microsoft Teams canal qui est disponible à partir du contexte de [l’onglet](~/tabs/how-to/access-teams-context.md). | 
| `subEntityId`&emsp; | Un ID pour l’élément dans l’onglet. |Tâche456 |
| `channelId`&emsp; | L’Microsoft Teams canal qui est disponible à partir du contexte de [l’onglet](~/tabs/how-to/access-teams-context.md). Cette propriété n’est disponible que dans des onglets configurables avec une portée **d’équipe.** Il n’est pas disponible dans les onglets statiques, qui ont une portée de **personnel**.| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |

Exemples :

* Lien vers un onglet configurable lui-même: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Lien vers un élément de tâche dans l’onglet configurable : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Lien vers un onglet statique lui-même: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Lien vers un élément de tâche dans l’onglet statique : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Assurez-vous que tous les paramètres de requête sont correctement codés URI. Vous devez suivre les exemples précédents en utilisant le dernier exemple :

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a>Consommer un lien profond à partir d’un onglet

Lorsque vous naviguez vers un lien profond, Microsoft Teams navigue simplement vers l’onglet et fournit un mécanisme à travers la bibliothèque JavaScript Microsoft Teams pour récupérer l’ID de la sous-entité s’il existe.

[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-)L’appel renvoie un contexte qui inclut `subEntityId` le champ si l’onglet est navigué à travers un lien profond.

## <a name="deep-linking-from-your-tab"></a>Lien profond à partir de votre onglet

Vous pouvez créer un lien profond vers le contenu Teams à partir de votre onglet. Ceci est utile si votre onglet doit se lier à d’autres contenus en Teams, comme à un canal, un message, un autre onglet ou même pour ouvrir un dialogue de planification. Pour déclencher un lien profond à partir de votre onglet, vous devez appeler :

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Cet appel vous navigue vers l’URL correcte, ou déclenche une action client, comme l’ouverture d’une planification ou d’une application installer le dialogue. Prenons l’exemple suivant :

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Lien profond vers un chat

Vous pouvez créer des liens profonds vers des conversations privées entre utilisateurs en spécifier l’ensemble des participants. Si un chat n’existe pas avec les participants spécifiés, le lien navigue vers un nouveau chat vide. De nouveaux chats sont créés dans l’état de brouillon jusqu’à ce que l’utilisateur envoie le premier message. Dans le cas contraire, vous pouvez spécifier le nom du chat s’il n’existe pas déjà, ainsi que le texte qui doit être inséré dans la boîte de composition de l’utilisateur. Vous pouvez considérer cette fonctionnalité comme un raccourci pour l’utilisateur prenant l’action manuelle de naviguer ou de créer le chat, puis en tapant le message.

Par exemple, si vous retournez un profil d’utilisateur Office 365 de votre bot sous forme de carte, ce lien profond peut permettre à l’utilisateur de discuter facilement avec cette personne.

### <a name="generate-a-deep-link-to-a-chat"></a>Générer un lien profond vers un chat

Utilisez ce format pour un lien profond que vous pouvez utiliser dans une carte d’extension de bot, connecteur ou messagerie :

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Exemple : `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Les paramètres de requête sont les :

* `users`: La liste des adresses d’impression des utilisateurs séparées par virgule représentant les participants au chat. L’utilisateur qui effectue l’action est toujours inclus en tant que participant. Actuellement, le champ Id utilisateur prend en charge le Nom utilisateur Azure ADPrincipalName, tel qu’une adresse e-mail uniquement.
* `topicName`: Un champ optionnel pour le nom d’affichage du chat, dans le cas d’un chat avec 3 utilisateurs ou plus. Si ce champ n’est pas spécifié, le nom d’affichage du chat est basé sur les noms des participants.
* `message`: Champ optionnel pour le texte de message que vous souhaitez insérer dans la boîte de composition de l’utilisateur actuel pendant que le chat est dans un état de brouillon.

Pour utiliser ce lien profond avec votre bot, spécifiez-le comme cible URL dans le bouton de votre carte ou appuyez sur l’action via le `openUrl` type d’action.

## <a name="generate-deep-links-to-file-in-channel"></a>Générer des liens profonds pour le fichier dans le canal

Le format de lien profond suivant peut être utilisé dans une carte d’extension de bot, connecteur ou messagerie :

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

Les paramètres de requête sont les :

* `tenantId`: Exemple d’identification du locataire, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb
* `fileType`: Type de fichier pris en charge, tel que docx, pptx, xlsx et pdf
* `objectUrl`: URL objet du fichier, https://microsoft.sharepoint.com/teams/(filepath)
* `baseUrl`: URL de base du fichier, https://microsoft.sharepoint.com/teams
* `serviceName`: Nom du service, id d’application
* `threadId`: Le threadId est l’id d’équipe de l’équipe où le fichier est stocké. Il est facultatif et ne peut pas être défini pour les fichiers stockés dans le dossier d’OneDrive utilisateur. threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype
* `groupId`: Id de groupe du fichier, ae063b79-5315-4ddb-ba70-27328ba6c31e

Voici le format d’exemple de deeplink vers les fichiers :

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80 ?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a>Sérialisation de cet objet :
```
{
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>Liaison profonde pour SharePoint Framework onglets

Le format de lien profond suivant peut être utilisé dans une carte d’extension bot, connecteur ou messagerie : `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Lorsqu’un bot envoie un message TextBlock avec un lien profond, un nouvel onglet navigateur s’ouvre lorsque les utilisateurs sélectionnent le lien. Cela se produit dans Chrome et Microsoft Teams de bureau fonctionnant sous Linux.
> Si le bot envoie la même URL de lien profond dans un `Action.OpenUrl` , l’onglet Teams s’ouvre dans le navigateur actuel lorsque l’utilisateur sélectionne le lien. Aucun nouvel onglet navigateur n’est ouvert.

Les paramètres de requête sont les :

* `appID`: Votre manifeste ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.

* `entityID`: L’iD d’élément que vous avez fourni [lors de la configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md). Par exemple, **tasklist123**.
* `entityWebUrl`: Un champ optionnel avec une URL de repli à utiliser si le client ne prend pas en charge le rendu de l’onglet - https://tasklist.example.com/123 ou https://tasklist.example.com/list123/task456 .
* `entityName`: Une étiquette pour l’élément dans votre onglet, à utiliser lors de l’affichage du lien profond, liste de tâches 123 ou tâche 456.

Exemple : https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList

## <a name="deep-linking-to-the-scheduling-dialog"></a>Lien profond vers le dialogue de planification

> [!NOTE]
> Cette fonctionnalité est actuellement en aperçu développeur.

Vous pouvez créer des liens profonds vers Teams de planification intégrée. Ceci est particulièrement utile si votre application aide l’utilisateur à remplir le calendrier ou à planifier des tâches connexes.

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Générer un lien profond vers le dialogue de planification

Utilisez le format suivant pour un lien profond que vous pouvez utiliser dans une carte d’extension de bot, connecteur ou messagerie : `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Exemple : `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Les paramètres de requête sont les :

* `attendees`: La liste facultative des iD utilisateur s’élisant par virgule représentant les participants à la réunion. L’utilisateur effectuant l’action est l’organisateur de la réunion. Le champ Id utilisateur prend actuellement en charge uniquement le Nom de l’utilisateur Azure ADPrincipalName, généralement une adresse e-mail.
* `startTime`: L’heure de début optionnelle de l’événement. Cela devrait être dans [le format LONG ISO 8601](https://en.wikipedia.org/wiki/ISO_8601), par *exemple 2018-03-12T23:55:25+02:00*.
* `endTime`: L’heure de fin optionnelle de l’événement, également au format ISO 8601.
* `subject`: Un champ optionnel pour le sujet de la réunion.
* `content`: Un champ optionnel pour le champ de détails de la réunion.

> [!NOTE]
> À l’heure actuelle, il n’est pas pris en charge de spécifier l’emplacement. Vous devez spécifier le décalage UTC, cela signifie fuseaux horaires lors de la génération de vos heures de début et de fin.

Pour utiliser ce lien profond avec votre bot, vous pouvez spécifier cela comme cible URL dans le bouton de votre carte ou appuyez sur l’action à travers le `openUrl` type d’action.

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>Lien profond vers un appel audio ou audio-vidéo

Vous pouvez créer des liens profonds pour invoquer des appels audio uniquement ou audio-vidéo à un seul utilisateur ou à un groupe d’utilisateurs, en spécifiez le type *d’appel, comme audio* *ou av,* et les participants. Une fois le lien profond invoqué et avant de placer l’appel, Teams client de bureau invite une confirmation pour effectuer l’appel. En cas d’appel de groupe, vous pouvez appeler un ensemble d’utilisateurs VoIP et un ensemble d’utilisateurs PSTN dans la même invocation deeplink. 

En cas d’appel vidéo, le client demandera confirmation et allumera la vidéo de l’appelant pour l’appel. Le récepteur de l’appel a le choix de répondre par audio seulement ou audio et vidéo, par le biais de la fenêtre Teams notification d’appel.

> [!NOTE]
> Ce lien profond ne peut pas être utilisé pour invoquer une réunion.

### <a name="generate-a-deep-link-to-a-call"></a>Générer un lien profond vers un appel

| Lien profond | Format | Exemple |
|-----------|--------|---------|
| Passer un appel audio | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; utilisateur2&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| Passer un appel audio et vidéo | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; withvideo=true | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true |
|Passer un appel audio et vidéo avec une source de paramètres optionnelle | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; withvideo=true&source=demoApp | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true&source=demoApp |  
| Faites un appel audio et vidéo à une combinaison d’utilisateurs voIP et PSTN | https://teams.microsoft.com/l/call/0/0?users=&lt&gt;;user1,4: &lt; nombre de téléphones&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210 |
  
Voici les paramètres de requête :
* `users`: La liste des adresses d’impression des utilisateurs séparées par virgule représentant les participants à l’appel. Actuellement, le champ Id utilisateur prend en charge l’Azure AD UserPrincipalName, généralement une adresse e-mail, ou en cas d’appel PSTN, il prend en charge un mri pstn 4: &lt; phonenumber &gt; .
* `Withvideo`: Il s’agit d’un paramètre optionnel, que vous pouvez utiliser pour faire un appel vidéo. La configuration de ce paramètre n’allumera que la caméra de l’appelant. Le destinataire de l’appel a le choix de répondre par appel audio ou audio et vidéo par l’intermédiaire de la fenêtre Teams notification d’appel. 
* `Source`: Il s’agit d’un paramètre optionnel, qui informe sur la source du deeplink.

## <a name="code-sample"></a>Exemple de code

| Nom de l’échantillon | Description | C# |Node.js|
|-------------|-------------|------|----|
|Deep Link consommant subentity ID  |Microsoft Teams’application pour démontrer deeplink du chat bot à l’onglet consommant Subentity ID.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Voir aussi

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)

