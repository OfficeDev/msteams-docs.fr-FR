---
title: Créer des liens profonds vers le contenu
description: Décrit les liens profonds et leur utilisation dans vos applications
keywords: lien profond teams
ms.openlocfilehash: 35aceba4b569baac9283a3355ee5719273145652
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797784"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a>Créer des liens profonds vers du contenu et des fonctionnalités dans Microsoft Teams

Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Exemples d’exemples où cela peut être utile :

* Navigation de l’utilisateur vers le contenu dans l’un des onglets de votre application. Par exemple, votre application peut avoir un bot qui envoie des messages pour avertir l’utilisateur d’une activité importante. Lorsque l’utilisateur tape sur la notification, le lien profond navigue jusqu’à l’onglet afin que l’utilisateur puisse afficher plus de détails sur l’activité.
* Votre application automatise ou simplifie certaines tâches utilisateur, telles que la création d’une conversation ou la planification d’une réunion, en pré-remplissant les liens profonds avec les paramètres requis. Cela évite aux utilisateurs d’entrer manuellement des informations.

> [!NOTE]
>
> Un lien profond lance d’abord le navigateur avant de naviguer vers le contenu et les informations comme suit :
>
> **Tab**:  
> ✔ permet d’accéder directement à l’URL du lien profond.
>
> **Bot**:  
> ✔ deeplink dans le corps de la carte : s’ouvre dans le navigateur en premier.  
> ✔ deeplink ajouté à l’action OuvrirURL dans la carte adaptative : permet d’accéder directement à l’URL du lien profond.  
> ✔ texte du markdown lien hypertexte dans la carte : s’ouvre d’abord dans le navigateur.  
>
> **Conversation**:  
> ✔ de lien hypertexte de message texte : permet d’accéder directement à l’URL du lien profond.  
> ✔ de conversation générale - Navigue directement vers l’URL du lien profond.

## <a name="deep-linking-to-your-tab"></a>Liaison profonde à votre onglet

Vous pouvez créer des liens profonds vers des entités dans Teams. En règle générale, il est utilisé pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Par exemple, si votre onglet contient une liste de tâches, les membres de l’équipe peuvent créer et partager des liens vers des tâches individuelles. Lorsque vous cliquez dessus, le lien permet d’accéder à votre onglet qui se concentre sur l’élément spécifique. Pour implémenter cela, vous ajoutez une action « copier le lien » à chaque élément, de la manière la mieux adaptée à votre interface utilisateur. Lorsque l’utilisateur prend cette action, vous appelez pour afficher une boîte de dialogue contenant un lien que l’utilisateur `shareDeepLink()` peut copier dans le Presse-papiers. Lorsque vous passez cet appel, vous passez également un ID pour [](~/tabs/how-to/access-teams-context.md) votre élément, que vous obtenez dans le contexte lorsque le lien est suivi et que votre onglet est rechargé.

Vous pouvez également générer des liens profonds par programme, en utilisant le format spécifié plus loin dans cette rubrique. Vous pouvez les utiliser dans les [messages](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) [de bot](~/bots/what-are-bots.md) et de connecteur qui informent les utilisateurs des modifications apportées à votre onglet ou aux éléments qu’il int ment.

> [!NOTE]
> Ceci est différent des liens fournis par le lien Copier vers l’élément de menu **Onglet,** qui génère simplement un lien profond qui pointe vers cet onglet.

>[!NOTE]
> Actuellement, shareDeepLink ne fonctionne pas sur les plateformes mobiles.

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a>Affichage d’un lien profond vers un élément dans votre onglet

Pour afficher une boîte de dialogue qui contient un lien profond vers un élément dans votre onglet, appelez `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`

Fournissez les champs ci-après :

* `subEntityId`&emsp;Identificateur unique de l’élément dans votre onglet avec lequel vous êtes en lien profond
* `subEntityLabel`&emsp;Étiquette de l’élément à utiliser pour afficher le lien profond
* `subEntityWebUrl`&emsp;Champ facultatif avec une URL de base à utiliser si le client ne prend pas en charge le rendu de l’onglet

### <a name="generating-a-deep-link-to-your-tab"></a>Génération d’un lien profond vers votre onglet

> [!NOTE]
> Les onglets personnels ont une étendue, tandis que les onglets de canal et `personal` de groupe utilisent `team` ou `group` utilisent des étendues. Les deux types d’onglets ont une syntaxe légèrement différente, car seul l’onglet configurable possède une `channel` propriété associée à son objet de contexte. Pour plus [d’informations](~/resources/schema/manifest-schema.md) sur les étendues d’onglet, voir la référence de manifeste.

> [!NOTE]
> Les liens profonds fonctionnent correctement uniquement si l’onglet a été configuré à l’aide de la bibliothèque v0.4 ou ultérieure et en raison de cet ID d’entité. Les liens profonds vers les onglets sans ID d’entité naviguent toujours vers l’onglet, mais ne peuvent pas fournir l’ID de sous-entité à l’onglet.

Utilisez ce format pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie :

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si le bot envoie un message contenant un lien profond, un nouvel onglet de navigateur s’ouvre lorsque l’utilisateur `TextBlock` sélectionne le lien. Cela se produit dans Chrome et dans l’application de bureau Microsoft Teams, les deux s’exécutant sur Linux.
> Si le bot envoie la même URL de lien profond dans un , l’onglet Teams est ouvert dans l’onglet du navigateur actuel lorsque l’utilisateur clique `Action.OpenUrl` sur le lien. Aucun nouvel onglet de navigateur n’est ouvert.

Les paramètres de requête sont les suivants :

* `appId`&emsp;L’ID de votre manifeste ; par exemple, « fe4a8eba-2a31-4737-8e33-e5fae6fee194 »
* `entityId`&emsp;ID de l’élément dans l’onglet, que vous avez fourni lors de [la configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md); par exemple, « tasklist123 »
* `entityWebUrl`ou un champ facultatif avec une URL de base à utiliser si le client ne prend pas en charge le rendu de l’onglet ; par `subEntityWebUrl` &emsp; exemple, https://tasklist.example.com/123 " ou https://tasklist.example.com/list123/task456 »
* `entityLabel`ou une étiquette pour l’élément dans votre onglet, à utiliser lors de l’affichage du lien profond ; par exemple, « Liste des tâches 123 » ou « `subEntityLabel` &emsp; Tâche 456 »
* `context`&emsp;Objet JSON contenant les champs suivants :
  * `subEntityId`&emsp;ID de l’élément _dans l’onglet_ ; par exemple, « task456 »
  * `channelId`&emsp;ID de canal Microsoft Teams [](~/tabs/how-to/access-teams-context.md)(disponible dans le contexte de l’onglet ; par exemple, « 19:cbe3683f25094106b826c9cada3afbe0@thread.skype ». Cette propriété est disponible uniquement dans les onglets configurables dont l’étendue est « team ». Il n’est pas disponible dans les onglets statiques, dont l’étendue est « personnel ».

Exemples :

* Lien vers un onglet configurable lui-même : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Lien vers un élément de tâche dans l’onglet configurable : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`
* Lien vers un onglet statique lui-même : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`
* Lien vers un élément de tâche dans l’onglet statique : `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`

> [!IMPORTANT]
> Assurez-vous que tous les paramètres de requête sont correctement codés en URI. Pour des raisons de lisibilité, les exemples ci-dessus ne le sont pas, mais vous devez le faire. En utilisant le dernier exemple :
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a>Consommation d’un lien profond à partir d’un onglet

Lorsque vous accédez à un lien profond, Microsoft Teams navigue simplement vers l’onglet et fournit un mécanisme via la bibliothèque JavaScript Microsoft Teams pour récupérer l’ID de sous-entité (s’il existe).

L’appel renvoie un contexte qui inclut le champ si l’onglet a été accédé [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) via un lien `subEntityId` profond.

## <a name="deep-linking-from-your-tab"></a>Liaison profonde à partir de votre onglet

Vous pouvez resserrez un lien profond vers le contenu dans Teams à partir de votre onglet. Cela est utile si votre onglet doit être en lien avec d’autres contenus dans Teams, tels qu’un canal, un message, un autre onglet ou même pour ouvrir une boîte de dialogue de planification. Pour déclencher un lien profond à partir de votre onglet, vous devez appeler :

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

Cela vous permet d’accéder à l’URL correcte ou de déclencher une action du client telle que l’ouverture d’une boîte de dialogue de planification ou d’installation d’application. Exemple :

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a>Lien profond vers une conversation

Vous pouvez créer des liens profonds vers des conversations privées entre les utilisateurs en spécifiant l’ensemble des participants. Si une conversation n’existe pas avec les participants spécifiés, le lien dirigera l’utilisateur vers une nouvelle conversation vide. Les nouvelles conversations seront créées en état brouillon jusqu’à ce que l’utilisateur envoie le premier message. Si vous le souhaitez, vous pouvez spécifier le nom de la conversation (si elle n’existe pas encore), ainsi que le texte à insérer dans la zone de composition de l’utilisateur. Vous pouvez voir cette fonctionnalité comme un raccourci pour l’utilisateur qui fait l’action manuelle de naviguer vers ou créer la conversation, puis de taper le message.

Par exemple, si vous renvoyez un profil utilisateur Office 365 à partir de votre bot en tant que carte, ce lien profond peut permettre à l’utilisateur de discuter facilement avec cette personne.

### <a name="generating-a-deep-link-to-a-chat"></a>Génération d’un lien profond vers une conversation

Utilisez ce format pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie :

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Exemple : `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Les paramètres de requête sont les suivants :

* `users`: Liste des ID d’utilisateurs séparés par des virgules représentant les participants à la conversation. L’utilisateur qui exécute l’action est toujours inclus en tant que participant. Le champ ID utilisateur prend actuellement uniquement en charge Azure AD UserPrincipalName (généralement une adresse e-mail).
* `topicName`: champ facultatif pour le nom complet de la conversation, dans le cas d’une conversation avec 3 utilisateurs ou plus. Si ce champ n’est pas spécifié, le nom complet de la conversation sera basé sur les noms des participants.
* `message`: champ facultatif pour le texte du message que vous souhaitez insérer dans la zone de composition de l’utilisateur actuel lorsque la conversation est en état brouillon.

Pour utiliser ce lien profond avec votre bot, vous pouvez le spécifier comme cible d’URL dans le bouton de votre carte ou appuyer sur l’action par le biais du `openUrl` type d’action.

## <a name="linking-to-the-scheduling-dialog"></a>Liaison à la boîte de dialogue de planification

> [!Note]
> Cette fonctionnalité est actuellement en prévisualisation pour les développeurs.

Vous pouvez créer des liens profonds vers la boîte de dialogue de planification intégrée teams. Cela est particulièrement utile si votre application aide l’utilisateur à effectuer des tâches liées au calendrier ou à la planification.

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a>Génération d’un lien profond vers la boîte de dialogue de planification

Utilisez ce format pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de messagerie : `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Exemple : `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

Les paramètres de requête sont les suivants :

* `attendees`: Liste facultative d’ID d’utilisateurs séparés par des virgules représentant les participants à la réunion. L’utilisateur qui effectue l’action est l’organisateur de la réunion. Le champ ID utilisateur prend actuellement uniquement en charge Azure AD UserPrincipalName (généralement une adresse e-mail).
* `startTime`: Heure de début facultative de l’événement. Il doit être au [format ISO 8601 long,](https://en.wikipedia.org/wiki/ISO_8601)par exemple « 2018-03-12T23:55:25+02:00 ».
* `endTime`: Heure de fin facultative de l’événement, également au format ISO 8601.
* `subject`: Champ facultatif pour l’objet de la réunion.
* `content`: champ facultatif pour le champ Détails de la réunion.

Actuellement, la spécification de l’emplacement n’est pas prise en charge. Lors de la génération de vos heures de début et de fin, assurez-vous de spécifier le décalage UTC (fuseaux horaires).

Pour utiliser ce lien profond avec votre bot, vous pouvez le spécifier comme cible d’URL dans le bouton de votre carte ou appuyer sur l’action par le biais du `openUrl` type d’action.
