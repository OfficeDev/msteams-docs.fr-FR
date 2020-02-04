---
title: Créer des liens détaillés
description: Décrit les liens détaillés et leur utilisation dans vos applications
keywords: teams de liens deeplink
ms.openlocfilehash: 03580c4d15c82da70402d68d85b0d28f8afa670e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673903"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>Créer des liens détaillés vers du contenu et des fonctionnalités dans Microsoft teams

Vous pouvez créer des liens vers des informations et des fonctionnalités dans le client Teams. Exemples d’emplacements pouvant être utiles :

* Navigation entre l’utilisateur et le contenu dans l’un des onglets de votre application. Par exemple, votre application peut disposer d’un bot qui envoie des messages avertissant l’utilisateur d’une activité importante. Lorsque l’utilisateur clique sur la notification, le lien profond navigue vers l’onglet pour permettre à l’utilisateur d’afficher plus de détails sur l’activité.
* Votre application automatise ou simplifie certaines tâches utilisateur, telles que la création d’une conversation ou la planification d’une réunion, en préremplissant les liens détaillés avec les paramètres requis. Cela évite que les utilisateurs aient besoin d’entrer manuellement les informations.

## <a name="deep-linking-to-your-tab"></a>Liens détaillés vers votre onglet

Vous pouvez créer des liens approfondis vers des entités dans Teams. En règle générale, cette opération permet de créer des liens pour accéder au contenu et aux informations au sein de votre onglet. Par exemple, si votre onglet contient une liste de tâches, les membres de l’équipe peuvent créer et partager des liens vers des tâches individuelles. Lorsque l’utilisateur clique dessus, le lien accède à votre onglet qui se concentre sur l’élément spécifique. Pour ce faire, vous ajoutez une action « copier le lien » à chaque élément, de la manière la mieux adaptée à votre interface utilisateur. Lorsque l’utilisateur effectue cette action, vous appelez `shareDeepLink()` pour afficher une boîte de dialogue contenant un lien que l’utilisateur peut copier dans le presse-papiers. Lorsque vous effectuez cet appel, vous transmettez également un ID pour votre élément, que vous obtenez dans le [contexte](~/tabs/how-to/access-teams-context.md) lorsque le lien est suivi et que votre onglet est rechargé.

Vous pouvez également générer des liens détaillés par programme, en utilisant le format indiqué plus loin dans cette rubrique. Vous pouvez utiliser ces éléments dans les messages de [robot](~/bots/what-are-bots.md) et de [connecteur](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) qui informent les utilisateurs des modifications apportées à votre onglet, ou à des éléments qu’il contient.

> [!NOTE]
> Cela est différent des liens fournis par l’élément de menu **copier le lien dans l’onglet** , qui génère uniquement un lien profond pointant vers cet onglet.

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>Affichage d’un lien profond vers un élément au sein de votre onglet

Pour afficher une boîte de dialogue qui contient un lien détaillé vers un élément au sein de votre onglet, appelez`microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

Renseignez les champs suivants :

* `subEntityId`&emsp;Identificateur unique de l’élément dans votre onglet vers lequel vous établissez un lien profond.
* `subEntityLabel`&emsp;Étiquette de l’élément à utiliser pour l’affichage du lien profond
* `subEntityWebUrl`&emsp;Un champ facultatif avec une URL de secours à utiliser si le client ne prend pas en charge le rendu de l’onglet

### <a name="generating-a-deep-link-to-your-tab"></a>Génération d’un lien profond vers votre onglet

> [!NOTE]
> Les onglets statiques ont une portée de « personnel » et les onglets configurables ont une portée de « Team ». Les deux types d’onglets ont une syntaxe légèrement différente étant donné que seul l’onglet `channel` configurable a une propriété associée à son objet de contexte. Pour plus d’informations sur les étendues personnelles et d’équipe, voir la référence de [manifeste](~/resources/schema/manifest-schema.md) .
> [!NOTE]
> Les liens détaillés fonctionnent correctement uniquement si l’onglet a été configuré à l’aide de la bibliothèque v 0.4 ou version ultérieure et, en raison de l’ID d’entité. Les liens détaillés vers les onglets sans ID d’entité continuent à accéder à l’onglet mais ne peuvent pas fournir l’ID de sous-entité à l’onglet.

Utilisez ce format pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie :

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

Les paramètres de requête sont les suivants :

* `appId`&emsp;ID de votre manifeste ; par exemple, « fe4a8eba-2a31-4737-8E33-e5fae6fee194 »
* `entityId`&emsp;ID de l’élément dans l’onglet, que vous avez fourni lors de la [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md); par exemple, « tasklist123 »
* `entityWebUrl`ou `subEntityWebUrl` &emsp;un champ facultatif avec une URL de secours à utiliser si le client ne prend pas en charge le rendu de l’onglet ; par exemple, "https://tasklist.example.com/123" ou "https://tasklist.example.com/list123/task456"
* `entityLabel`ou `subEntityLabel` &emsp;une étiquette pour l’élément de votre onglet, à utiliser lors de l’affichage du lien profond ; par exemple, « liste des tâches 123 » ou « tâche 456 »
* `context`&emsp;Objet JSON contenant les champs suivants :
  * `subEntityId`&emsp;ID de l’élément _dans_ l’onglet ; par exemple, « task456 »
  * `channelId`&emsp;ID de canal Microsoft Teams (disponible à partir du [contexte](~/tabs/how-to/access-teams-context.md)d’onglet, par exemple, « 19 : cbe3683f25094106b826c9cada3afbe0@thread. Skype ». Cette propriété est disponible uniquement dans les onglets configurables avec une portée de « Team ». Elle n’est pas disponible dans les onglets statiques, dont l’étendue est « personnel ».

Exemples :

* Lien vers un onglet configurable lui-même :`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Lien vers une tâche dans l’onglet configurable :`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Lien vers un onglet statique lui-même :`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Lien vers un élément de tâche dans l’onglet statique :`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Assurez-vous que tous les paramètres de requête sont correctement codés en URI. Pour des raisons de lisibilité, les exemples ci-dessus ne le sont pas, mais vous devez le faire. À l’aide du dernier exemple :
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>Consommation d’un lien profond à partir d’un onglet

Lorsque vous accédez à un lien profond, Microsoft teams navigue vers l’onglet et fournit un mécanisme via la bibliothèque JavaScript de Microsoft teams pour récupérer l’ID de sous-entité (le cas échéant).

L' [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) appel renvoie un contexte qui inclut le `subEntityId` champ si l’onglet a été accédé via un lien profond.

## <a name="deep-linking-from-your-tab"></a>Liens détaillés à partir de votre onglet

Vous pouvez deeplink au contenu dans teams à partir de votre onglet. Cette fonctionnalité est utile si votre onglet doit établir un lien vers un autre contenu dans Teams, tel qu’un canal, un message, un autre onglet ou même d’ouvrir une boîte de dialogue de planification. Pour déclencher un deeplink à partir de votre onglet, vous devez appeler :

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Cela vous permet d’accéder à l’URL correcte ou de déclencher une action client telle que l’ouverture d’une boîte de dialogue d’installation de planification ou d’application. Exemple :

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Liaison profonde à une conversation

Vous pouvez créer des liens détaillés vers des conversations privées entre les utilisateurs en spécifiant l’ensemble des participants. S’il n’existe pas de conversation avec les participants spécifiés, le lien va diriger l’utilisateur vers une nouvelle conversation vide. Les nouvelles conversations seront créées en état Brouillon jusqu’à ce que l’utilisateur envoie le premier message. Si vous le souhaitez, vous pouvez spécifier le nom de la conversation (si elle n’existe pas déjà), ainsi que le texte à insérer dans la zone de composition de l’utilisateur. Vous pouvez considérer cette fonctionnalité comme un raccourci pour l’utilisateur qui effectue l’action manuelle de navigation vers ou de création de la conversation, puis en tapant le message.

À titre d’exemple d’utilisation, si vous renvoyez un profil utilisateur Office 365 à partir de votre robot sous forme de carte, ce lien profond peut permettre à l’utilisateur de converser facilement avec cette personne.

### <a name="generating-a-deep-link-to-a-chat"></a>Génération d’un lien profond vers une conversation

Utilisez ce format pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie :

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Exemple : `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Les paramètres de requête sont les suivants :

* `users`&emsp;Liste d’ID utilisateur, séparés par des virgules, représentant les participants de la conversation. L’utilisateur qui effectue l’action est toujours inclus en tant que participant. Le champ ID d’utilisateur ne prend actuellement en charge que le UserPrincipalName Azure AD (généralement une adresse de messagerie).
* `topicName`&emsp;Champ facultatif pour le nom d’affichage de la conversation, dans le cas d’une conversation avec 3 utilisateurs ou plus. Si ce champ n’est pas spécifié, le nom d’affichage de la conversation sera basé sur les noms des participants.
* `message`&emsp;Champ facultatif pour le texte du message que vous souhaitez insérer dans la zone de composition de l’utilisateur actuel pendant que la conversation est à l’état Brouillon.

Pour utiliser ce lien profond avec votre robot, vous pouvez le spécifier en tant qu’URL cible dans le bouton de votre carte ou cliquer sur `openUrl` action par le biais du type d’action.

## <a name="linking-to-the-scheduling-dialog"></a>Liaison à la boîte de dialogue planification

> [!Note]
> Cette fonctionnalité est actuellement en version préliminaire pour les développeurs.

Vous pouvez créer des liens détaillés vers la boîte de dialogue de planification intégrée du client Teams. Ceci est particulièrement utile si votre application aide l’utilisateur à effectuer des tâches de calendrier ou de planification.

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>Génération d’un lien profond vers la boîte de dialogue planification

Utilisez ce format pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie :`https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Exemple : `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Les paramètres de requête sont les suivants :

* `attendees`&emsp;Liste facultative d’ID utilisateur, séparés par des virgules, représentant les participants de la réunion. L’utilisateur qui effectue l’action est l’organisateur de la réunion. Le champ ID d’utilisateur ne prend actuellement en charge que le UserPrincipalName Azure AD (généralement une adresse de messagerie).
* `startTime`&emsp;Heure de début facultative de l’événement. Cette valeur doit être au [format ISO 8601](https://en.wikipedia.org/wiki/ISO_8601), par exemple « 2018-03-12T23:55:25 + 02:00 ».
* `endTime`&emsp;Heure de fin facultative de l’événement, également au format ISO 8601.
* `subject`&emsp;Champ facultatif pour l’objet de la réunion.
* `content`&emsp;Champ facultatif pour le champ détails de la réunion.

Actuellement, la spécification de l’emplacement n’est pas prise en charge. Lors de la génération des heures de début et de fin, veillez à spécifier le décalage UTC (fuseaux horaires).

Pour utiliser ce lien profond avec votre robot, vous pouvez le spécifier en tant qu’URL cible dans le bouton de votre carte ou cliquer sur `openUrl` action par le biais du type d’action.
