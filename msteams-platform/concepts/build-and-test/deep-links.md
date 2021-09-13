---
title: Créer des liens plus étroits
description: Décrit les liens profonds et leur utilisation dans vos applications
ms.topic: how-to
ms.localizationpriority: medium
keywords: lien profond teams
ms.openlocfilehash: e61f926e36d379cb6a69816922cca7a8f3a3d17f
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156707"
---
# <a name="create-deep-links"></a>Créer des liens plus étroits 

Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Les scénarios dans lequel la création de liens profonds sont utiles sont les suivants :

* Navigation de l’utilisateur vers le contenu dans l’un des onglets de votre application. Par exemple, votre application peut avoir un bot qui envoie des messages pour avertir l’utilisateur d’une activité importante. Lorsque l’utilisateur tape sur la notification, le lien profond navigue vers l’onglet afin que l’utilisateur puisse afficher plus de détails sur l’activité.
* Votre application automatise ou simplifie certaines tâches utilisateur, telles que la création d’une conversation ou la planification d’une réunion, en pré-remplissant les liens profonds avec les paramètres requis. Cela évite aux utilisateurs d’entrer manuellement des informations.

> [!NOTE]
>
> Un lien profond lance d’abord le navigateur avant de naviguer vers le contenu. Le comportement des liens profonds sur Teams entités sont les suivants :
>
> **Tab**:  
> ✔ permet d’accéder directement à l’URL du lien profond.
>
> **Bot**:  
> ✔ deeplink dans le corps de la carte : s’ouvre en premier dans le navigateur.  
> ✔ deeplink ajouté à l’action OpenURL dans la carte adaptative : permet d’accéder directement à l’URL du lien profond.  
> ✔ texte du markdown lien hypertexte dans la carte : s’ouvre d’abord dans le navigateur.  
>
> **Conversation**:  
> ✔ de lien hypertexte de message texte : permet d’accéder directement à l’URL du lien profond.  
> ✔ de conversation générale : accédez directement à l’URL du lien profond.

## <a name="deep-linking-to-your-tab"></a>Liaison profonde à votre onglet

Vous pouvez créer des liens profonds vers des entités dans Teams. Il est utilisé pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Par exemple, si votre onglet contient une liste de tâches, les membres de l’équipe peuvent créer et partager des liens vers des tâches individuelles. Lorsque vous sélectionnez le lien, il navigue vers votre onglet qui se concentre sur l’élément spécifique. Pour implémenter cela, vous ajoutez une action **de** lien de copie à chaque élément, de la manière la mieux adaptée à votre interface utilisateur. Lorsque l’utilisateur prend cette action, vous appelez pour afficher une boîte de dialogue contenant un lien que l’utilisateur `shareDeepLink()` peut copier dans le Presse-papiers. Lorsque vous passez cet appel, vous passez également un ID pour [](~/tabs/how-to/access-teams-context.md) votre élément, que vous obtenez dans le contexte lorsque le lien est suivi et que votre onglet est rechargé.

Vous pouvez également générer des liens profonds par programme, en utilisant le format spécifié plus loin dans cette rubrique. Vous pouvez utiliser des liens profonds dans les [messages](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) [de bot](~/bots/what-are-bots.md) et de connecteur qui informent les utilisateurs des modifications apportées à votre onglet ou aux éléments qu’il insérez.

> [!NOTE]
> Ce lien profond est différent des liens fournis par le lien Copier vers l’élément de menu **Onglet,** qui génère simplement un lien profond qui pointe vers cet onglet.

>[!NOTE]
> Actuellement, shareDeepLink ne fonctionne pas sur les plateformes mobiles.

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a>Afficher un lien profond vers un élément dans votre onglet

Pour afficher une boîte de dialogue qui contient un lien profond vers un élément dans votre onglet, appelez `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` .

Fournissez les champs suivants :

* `subEntityId`: identificateur unique de l’élément dans votre onglet auquel vous êtes en liaison approfondie.
* `subEntityLabel`: étiquette de l’élément à utiliser pour afficher le lien profond.
* `subEntityWebUrl`: champ facultatif avec une URL de base à utiliser si le client ne prend pas en charge le rendu de l’onglet.

### <a name="generate-a-deep-link-to-your-tab"></a>Générer un lien profond vers votre onglet

> [!NOTE]
> Les onglets personnels ont une étendue, tandis que les onglets de canal et `personal` de groupe utilisent `team` ou `group` utilisent des étendues. Les deux types d’onglets ont une syntaxe légèrement différente, car seul l’onglet configurable possède une `channel` propriété associée à son objet de contexte. Pour plus [d’informations](~/resources/schema/manifest-schema.md) sur les étendues d’onglet, voir la référence de manifeste.

> [!NOTE]
> Les liens profonds fonctionnent correctement uniquement si l’onglet a été configuré à l’aide de la bibliothèque v0.4 ou ultérieure et en raison de cet ID d’entité. Les liens profonds vers les onglets sans ID d’entité naviguent toujours vers l’onglet, mais ne peuvent pas fournir l’ID de sous-entité à l’onglet.

Utilisez le format suivant pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie :

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si le bot envoie un message contenant un lien profond, un nouvel onglet de navigateur s’ouvre lorsque l’utilisateur `TextBlock` sélectionne le lien. Cela se produit dans Chrome et dans l Microsoft Teams de bureau, les deux s’exécutant sur Linux.
> Si le bot envoie la même URL de lien profond dans un , l’onglet Teams est ouvert dans l’onglet du navigateur actuel lorsque l’utilisateur sélectionne `Action.OpenUrl` le lien. Un nouvel onglet de navigateur n’est pas ouvert.

Les paramètres de requête sont les suivants :

| Nom du paramètre | Description | Exemple |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | ID de votre manifeste. |fe4a8eba-2a31-4737-8e33-e5fae6fee194|
| `entityId`&emsp; | ID de l’élément dans l’onglet, que vous avez fourni lors de [la configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).|Tasklist123|
| `entityWebUrl` ou `subEntityWebUrl`&emsp; | Champ facultatif avec une URL de base à utiliser si le client ne prend pas en charge le rendu de l’onglet. | `https://tasklist.example.com/123` ou `https://tasklist.example.com/list123/task456` |
| `entityLabel` ou `subEntityLabel`&emsp; | Étiquette de l’élément dans votre onglet, à utiliser lors de l’affichage du lien profond. | Liste des tâches 123 ou « Tâche 456 » |
| `context`&emsp; </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| Objet JSON contenant les champs suivants :</br></br> * ID de l’élément dans l’onglet. </br></br> * ID Microsoft Teams canal disponible à partir du contexte de [l’onglet.](~/tabs/how-to/access-teams-context.md) | 
| `subEntityId`&emsp; | ID de l’élément dans l’onglet. |Task456 |
| `channelId`&emsp; | ID Microsoft Teams canal disponible à partir du contexte de [l’onglet.](~/tabs/how-to/access-teams-context.md) Cette propriété est disponible uniquement dans les onglets configurables avec une étendue **d’équipe.** Il n’est pas disponible dans les onglets statiques, qui ont une étendue **personnelle.**| 19:cbe3683f25094106b826c9cada3afbe0@thread.skype |

Exemples :

* Lien vers un onglet configurable lui-même : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Lien vers un élément de tâche dans l’onglet configurable : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Lien vers un onglet statique lui-même : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Lien vers un élément de tâche dans l’onglet statique : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Assurez-vous que tous les paramètres de requête sont correctement codés en URI. Vous devez suivre les exemples de précédation à l’aide du dernier exemple :

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a>Utiliser un lien profond à partir d’un onglet

Lorsque vous naviguez vers un lien profond, Microsoft Teams navigue simplement vers l’onglet et fournit un mécanisme via la bibliothèque JavaScript Microsoft Teams pour récupérer l’ID de sous-entité s’il existe.

[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-)L’appel renvoie un contexte qui inclut le champ si l’onglet est inclus dans un lien `subEntityId` profond.

## <a name="deep-linking-from-your-tab"></a>Liaison profonde à partir de votre onglet

Vous pouvez resserrez un lien profond vers le contenu Teams partir de votre onglet. Cela est utile si votre onglet doit établir un lien vers d’autres contenus dans Teams, tels qu’un canal, un message, un autre onglet ou même pour ouvrir une boîte de dialogue de planification. Pour déclencher un lien profond à partir de votre onglet, vous devez appeler :

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Cet appel vous permet d’accéder à l’URL correcte ou de déclencher une action du client, telle que l’ouverture d’une boîte de dialogue de planification ou d’installation d’application. Prenons l’exemple suivant :

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Lien profond vers une conversation

Vous pouvez créer des liens profonds vers des conversations privées entre les utilisateurs en spécifiant l’ensemble des participants. Si une conversation n’existe pas avec les participants spécifiés, le lien permet à l’utilisateur d’accéder à une nouvelle conversation vide. Les nouvelles conversations sont créées en état brouillon jusqu’à ce que l’utilisateur envoie le premier message. Sinon, vous pouvez spécifier le nom de la conversation si elle n’existe pas déjà, ainsi que le texte à insérer dans la zone de composition de l’utilisateur. Vous pouvez voir cette fonctionnalité comme un raccourci pour l’utilisateur qui fait l’action manuelle de naviguer vers ou créer la conversation, puis de taper le message.

Par exemple, si vous renvoyez un profil utilisateur Office 365 à partir de votre bot en tant que carte, ce lien profond peut permettre à l’utilisateur de discuter facilement avec cette personne.

### <a name="generate-a-deep-link-to-a-chat"></a>Générer un lien profond vers une conversation

Utilisez ce format pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie :

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Exemple : `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Les paramètres de requête sont les suivants :

* `users`: Liste des ID d’utilisateurs séparés par des virgules représentant les participants à la conversation. L’utilisateur qui effectue l’action est toujours inclus en tant que participant. Actuellement, le champ ID utilisateur prend en charge Azure AD UserPrincipalName, par exemple une adresse de messagerie uniquement.
* `topicName`: champ facultatif pour le nom complet de la conversation, dans le cas d’une conversation avec 3 utilisateurs ou plus. Si ce champ n’est pas spécifié, le nom complet de la conversation est basé sur les noms des participants.
* `message`: champ facultatif pour le texte du message que vous souhaitez insérer dans la zone de composition de l’utilisateur actuel lorsque la conversation est en état brouillon.

Pour utiliser ce lien profond avec votre bot, spécifiez-le comme cible d’URL dans le bouton de votre carte ou appuyez sur l’action par le biais du `openUrl` type d’action.

## <a name="generate-deep-links-to-file-in-channel"></a>Générer des liens profonds vers un fichier dans le canal

Le format de lien profond suivant peut être utilisé dans un bot, un connecteur ou une carte d’extension de messagerie :

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

Les paramètres de requête sont les suivants :

* `tenantId`: Exemple d’ID de client, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb
* `fileType`: Type de fichier pris en charge, tel que docx, pptx, xlsx et pdf
* `objectUrl`: URL d’objet du fichier. Le format est `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext`. Par exemple, `https://microsoft.sharepoint.com/teams/(filepath)`
* `baseUrl`: URL de base du fichier. Le format est `https://{tenantName}.sharepoint.com/sites/{TeamName}`. Par exemple, `https://microsoft.sharepoint.com/teams`
* `serviceName`: Nom du service, ID d’application. Par exemple, teams.
* `threadId`: ThreadId est l’ID d’équipe de l’équipe dans laquelle le fichier est stocké. Elle est facultative et ne peut pas être définie pour les fichiers stockés dans le dossier d’OneDrive’un utilisateur. threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype
* `groupId`: ID de groupe du fichier, ae063b79-5315-4ddb-ba70-27328ba6c31e 

> [!NOTE]
> Vous pouvez voir `threadId` et `groupId` dans l’URL à partir du canal.  

Le format de lien profond suivant est utilisé dans un bot, un connecteur ou une carte d’extension de messagerie : `https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

L’exemple de format suivant montre le lien profond vers les fichiers :

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

## <a name="deep-linking-to-an-app"></a>Lien profond vers une application

Créez des liens profonds pour l’application une fois l’application répertoriée dans le Teams store. Pour créer un lien pour lancer Teams, vous pouvez également l’associer à l’URL suivante à votre ID d’application `https://teams.microsoft.com/l/app/<your-app-id>` : Une boîte de dialogue s’affiche pour installer l’application. 
  
## <a name="deep-linking-for-sharepoint-framework-tabs"></a>Liaisons profondes pour SharePoint Framework onglets

Le format de lien profond suivant peut être utilisé dans un bot, un connecteur ou une carte d’extension de messagerie : `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`

> [!NOTE]
> Lorsqu’un bot envoie un message TextBlock avec un lien profond, un nouvel onglet de navigateur s’ouvre lorsque les utilisateurs sélectionnent le lien. Cela se produit dans Chrome et Microsoft Teams application de bureau s’exécutant sur Linux.
> Si le bot envoie la même URL de lien profond dans un , l’onglet Teams s’ouvre dans le navigateur actuel lorsque l’utilisateur `Action.OpenUrl` sélectionne le lien. Aucun nouvel onglet de navigateur n’est ouvert.

Les paramètres de requête sont les suivants :

* `appID`: Votre ID manifeste **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.

* `entityID`: ID d’élément que vous avez fourni lors de [la configuration de l’onglet.](~/tabs/how-to/create-tab-pages/configuration-page.md) Par exemple, **tasklist123**.
* `entityWebUrl`: champ facultatif avec une URL de base à utiliser si le client ne prend pas en charge le rendu de l’onglet - `https://tasklist.example.com/123` ou `https://tasklist.example.com/list123/task456` .
* `entityName`: une étiquette pour l’élément dans votre onglet, à utiliser lors de l’affichage du lien profond, Liste des tâches 123 ou Tâche 456.

Exemple : https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList

## <a name="deep-linking-to-the-scheduling-dialog"></a>Liaison profonde à la boîte de dialogue de planification

> [!NOTE]
> Cette fonctionnalité est actuellement en prévisualisation pour les développeurs.

Vous pouvez créer des liens profonds vers la boîte Teams de planification intégrée. Cela est particulièrement utile si votre application aide l’utilisateur à effectuer le calendrier ou à planifier les tâches associées.

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Générer un lien profond vers la boîte de dialogue de planification

Utilisez le format suivant pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie : `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Exemple : `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Les paramètres de requête sont les suivants :

* `attendees`: Liste facultative d’ID d’utilisateurs séparés par des virgules représentant les participants à la réunion. L’utilisateur qui effectue l’action est l’organisateur de la réunion. Pour l’instant, le champ ID utilisateur prend uniquement en charge Azure AD UserPrincipalName, généralement une adresse de messagerie.
* `startTime`: Heure de début facultative de l’événement. Il doit être au [format ISO 8601 long](https://en.wikipedia.org/wiki/ISO_8601), par exemple *2018-03-12T23:55:25+02:00*.
* `endTime`: Heure de fin facultative de l’événement, également au format ISO 8601.
* `subject`: Champ facultatif pour l’objet de la réunion.
* `content`: champ facultatif pour le champ Détails de la réunion.

> [!NOTE]
> Actuellement, la spécification de l’emplacement n’est pas prise en charge. Vous devez spécifier le décalage UTC, c’est-à-dire les fuseaux horaires lors de la génération de vos heures de début et de fin.

Pour utiliser ce lien profond avec votre bot, vous pouvez le spécifier comme cible d’URL dans le bouton de votre carte ou appuyer sur l’action par le biais du `openUrl` type d’action.

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a>Liaison profonde à un appel audio ou audio-vidéo

Vous pouvez créer des liens profonds pour appeler des appels audio uniquement ou audio-vidéo à un seul utilisateur ou à un groupe d’utilisateurs, en spécifiant le type d’appel, en tant *qu’audio* ou *av,* et les participants. Une fois que le lien profond est appelé et avant de passer l’appel, Teams client de bureau invite une confirmation pour passer l’appel. En cas d’appel de groupe, vous pouvez appeler un ensemble d’utilisateurs VoIP et un ensemble d’utilisateurs PSTN dans le même appel de lien profond. 

En cas d’appel vidéo, le client demande confirmation et allume la vidéo de l’appelant pour l’appel. Le destinataire de l’appel a le choix de répondre uniquement par le biais de l’audio ou de l’audio et de la vidéo, via la fenêtre Teams notification d’appel.

> [!NOTE]
> Ce lien profond ne peut pas être utilisé pour l’facturation d’une réunion.

### <a name="generate-a-deep-link-to-a-call"></a>Générer un lien profond vers un appel

| Lien profond | Format | Exemple |
|-----------|--------|---------|
| Effectuer un appel audio | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| Effectuer un appel audio et vidéo | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; avecVideo=true | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true |
|Effectuer un appel audio et vidéo avec une source de paramètres facultative | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; avecVideo=true&source=demoApp | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp |  
| Effectuer un appel audio et vidéo à une combinaison d’utilisateurs VoIP et PSTN | https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; ,4: &lt; phonenumber&gt; | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210 |
  
Les paramètres de requête suivants sont les suivants :
* `users`: Liste des ID d’utilisateurs séparés par des virgules représentant les participants de l’appel. Actuellement, le champ ID utilisateur prend en charge Azure AD UserPrincipalName, généralement une adresse e-mail, ou en cas d’appel PSTN, il prend en charge un pstn 4: numéro de téléphone &lt; &gt; .
* `withVideo`: il s’agit d’un paramètre facultatif que vous pouvez utiliser pour effectuer un appel vidéo. La définition de ce paramètre n’activera que la caméra de l’appelant. Le destinataire de l’appel peut répondre par le biais d’un appel audio ou audio et vidéo via la Teams de notification d’appel. 
* `Source`: il s’agit d’un paramètre facultatif qui informe sur la source du lien profond.

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C # |Node.js|
|-------------|-------------|------|----|
|ID de sous-entité consommant un lien profond  |Microsoft Teams exemple d’application pour montrer le lien profond entre la conversation de bot et l’ID de sous-entité de consommation d’onglets.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Voir aussi

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)

