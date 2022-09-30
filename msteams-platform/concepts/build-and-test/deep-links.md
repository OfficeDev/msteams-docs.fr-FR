---
title: Créer des liens plus étroits
description: Dans cet article, vous allez apprendre à créer des liens profonds et à les parcourir dans vos applications Microsoft Teams avec des onglets.
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 7a9af415a6fdc4f2cb1f9fd04ba79e8b197a40fc
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243219"
---
# <a name="create-deep-links"></a>Créer des liens plus étroits

Les liens profonds sont un mécanisme de navigation que vous pouvez utiliser pour connecter les utilisateurs à des informations et des fonctionnalités dans Teams et les applications Teams. Voici quelques scénarios où la création de liens profonds peut être utile :

* Navigation de l’utilisateur vers le contenu dans l’un des onglets de votre application. Par exemple, votre application peut avoir un bot qui envoie des messages informant l’utilisateur d’une activité importante. Lorsque l’utilisateur appuie sur la notification, le lien profond accède à l’onglet afin que l’utilisateur puisse afficher plus de détails sur l’activité.
* Votre application automatise ou simplifie certaines tâches utilisateur. Vous pouvez créer une conversation ou planifier une réunion en préremplis les liens profonds avec les paramètres requis. Cela évite aux utilisateurs d’entrer manuellement des informations.

Le SDK client JavaScript de Microsoft Teams (TeamsJS) simplifie le processus de navigation. Pour de nombreux scénarios, tels que la navigation vers du contenu et des informations dans votre onglet ou le lancement d’une boîte de dialogue de conversation. Le Kit de développement logiciel (SDK) fournit des API typées qui offrent une expérience améliorée et peuvent remplacer l’utilisation de liens profonds. Ces API sont recommandées pour les applications Teams susceptibles d'être exécutées dans d'autres hôtes (Outlook, Office), car elles permettent également de vérifier que la fonctionnalité utilisée est prise en charge par cet hôte. Les sections suivantes présentent des informations sur les liens profonds, mais soulignent également comment les scénarios qui les nécessitaient ont changé avec la version v2 de TeamsJS.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

> [!NOTE]
> Le comportement des liens profonds dépend d'un certain nombre de facteurs. La liste suivante décrit le comportement des liens profonds sur les entités Teams.
>
> **Onglet** :   
> ✔ Accède directement à l’URL de lien profond.
>
> **Bot** :   
> ✔ Lien profond dans le corps de la carte : S'ouvre d'abord dans le navigateur.  
> ✔ Lien profond ajouté à l'action OpenURL dans la carte adaptative : Permet de naviguer directement vers l'url du lien profond.  
> ✔ texte Markdown de lien hypertexte dans la carte : s’ouvre dans le navigateur en premier.  
>
> **Conversation** :   
> ✔ Message texte hyperlien markdown : Permet de naviguer directement vers l'url du lien profond.  
> ✔ Lien collé dans une conversation générale de conversation : Permet de naviguer directement vers l'url du lien profond.
>
>
>Le comportement de navigation d'une application Teams étendue à Microsoft 365 (Outlook/Office) dépend de deux facteurs :
>
> * Cible vers laquelle pointe le lien profond.
> * Hôte sur lequel l’application Teams s’exécute.
>
> Si l'application Teams est exécutée dans l'hôte où le lien profond est ciblé, votre application s'ouvrira directement dans l'hôte. Toutefois, si l'application Teams est exécutée sur un hôte différent de celui où le lien profond est ciblé, l'application s'ouvrira d'abord dans le navigateur.

## <a name="deep-link-to-your-tab"></a>Lien profond à votre onglet

Vous pouvez créer des liens profonds vers des entités dans Teams. Cette méthode permet de créer des liens qui accèdent au contenu et aux informations dans votre onglet. Par exemple, si votre onglet contient une liste de tâches, les membres de l’équipe peuvent créer et partager des liens vers des tâches individuelles. Lorsque vous sélectionnez le lien, il accède à votre onglet qui se concentre sur l’élément spécifique.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

Pour implémenter, ajoutez une action **copier le lien** à chaque élément, de la manière qui convient le mieux à votre interface utilisateur. Lorsque l'utilisateur effectue cette action, appelez [pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true) pour afficher une boîte de dialogue contenant un lien que l'utilisateur peut copier dans le presse-papiers. Lorsque vous effectuez cet appel, transmettez un ID pour votre élément. Vous le récupérez en [contexte](~/tabs/how-to/access-teams-context.md) lorsque le lien est suivi et que votre onglet est rechargé.

```javascript
pages.shareDeepLink({ subPageId: <subPageId>, subPageLabel: <subPageLabel>, subPageWebUrl: <subPageWebUrl> })
```

Vous devez remplacer les champs par les informations appropriées :

* `subPageId` : un identificateur unique de l’élément dans votre onglet auquel vous effectuez un lien profond.
* `subPageLabel` : étiquette de l’élément à utiliser pour afficher le lien profond.
* `subPageWebUrl`: une URL de secours à utiliser si le client ne peut pas afficher la page.

Pour plus d’informations, consultez [pages.shareDeepLink()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-sharedeeplink&preserve-view=true).

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

Pour implémenter cela, vous ajoutez une action **copier le lien** à chaque élément, de la manière la mieux adaptée à votre interface utilisateur. Lorsque l’utilisateur effectue cette action, vous appelez `shareDeepLink()` pour afficher une boîte de dialogue contenant un lien que l’utilisateur peut copier dans le Presse-papiers. Lorsque vous effectuez cet appel, vous transmettez également un ID pour votre élément, que vous revenez dans le [contexte](~/tabs/how-to/access-teams-context.md) lorsque le lien est suivi et que votre onglet est rechargé.

```javascript
microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })
```

Vous devez remplacer les champs par les informations appropriées :

* `subEntityId` : identificateur unique de l’élément dans votre onglet auquel vous effectuez une liaison approfondie.
* `subEntityLabel` : étiquette de l’élément à utiliser pour afficher le lien profond.
* `subEntityWebUrl` : champ facultatif avec une URL de secours à utiliser si le client ne prend pas en charge le rendu de l’onglet.

---

Vous pouvez également générer des liens profonds par programmation, en utilisant le format spécifié plus loin dans cet article. Vous pouvez utiliser des liens profonds dans [bot](~/bots/what-are-bots.md) et [connecteur](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages qui informent les utilisateurs des modifications apportées à votre onglet ou aux éléments qu’il contient.

> [!NOTE]
> Ce lien profond est différent des liens fournis par l’élément de menu **Copier vers l’onglet**, qui génère simplement un lien profond qui pointe vers cet onglet.

>[!IMPORTANT]
> Actuellement, shareDeepLink ne fonctionne pas sur les plateformes mobiles.

### <a name="consume-a-deep-link-from-a-tab"></a>Utiliser un lien profond à partir d’un onglet

Lorsque vous accédez à un lien profond, Microsoft Teams accède simplement à l’onglet et fournit un mécanisme via la bibliothèque JavaScript Teams pour récupérer l’ID de sous-page s’il existe.

L’appel [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) (`microsoftTeams.getContext()`) dans TeamsJS v1 retourne une promesse qui sera résolue avec le contexte qui inclut la `subPageId` propriété (subEntityId pour TeamsJS v1) si l’onglet est parcouru via un lien profond. Pour plus d'informations, voir [Interface PageInfo](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true).

### <a name="generate-a-deep-link-to-your-tab"></a>Générer un lien ciblé vers votre onglet

Bien qu’il soit recommandé d’utiliser `shareDeepLink()` pour générer un lien profond vers votre onglet, il est possible d’en créer un manuellement.

> [!NOTE]
>
> * Les onglets personnels ont un `personal`scope, tandis que les onglets canal et groupe utilisent `team`or `group`scopes. Les deux types d’onglets ont une syntaxe légèrement différente, car seul l’onglet configurable a un `channel`propriété associé à son objet de contexte. Pour plus d’informations sur les étendues d’onglet, consultez la référence du [manifeste](~/resources/schema/manifest-schema.md).
> * Les liens profonds fonctionnent correctement uniquement si l’onglet a été configuré à l’aide de la bibliothèque v0.4 ou ultérieure et qu’en raison de cela a un ID d’entité. Les liens profonds vers les onglets sans ID d’entité passent toujours à l’onglet, mais ne peuvent pas fournir l’ID de sous-entité à l’onglet.

Utilisez le format suivant pour un lien profond que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de message :

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> Si le bot envoie un message contenant un `TextBlock` avec un lien profond, un nouvel onglet de navigateur est ouvert lorsque l’utilisateur sélectionne le lien. Cela se produit dans Chrome et dans l’application de bureau Teams, tous deux exécutés sur Linux.
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
| `entityId`&emsp; | ID de l’élément dans l’onglet, que vous avez fourni lors de la [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md). Lors de la génération d’une URL pour la liaison approfondie, continuez à utiliser entityID comme nom de paramètre dans l’URL. Lors de la configuration de l’onglet, l’objet de contexte fait référence à l’entityID en tant que {page.id}. |Liste des tâches123|
| `entityWebUrl` ou `subEntityWebUrl`&emsp; | Champ facultatif avec une URL de secours à utiliser si le client ne prend pas en charge le rendu de l’onglet. | `https://tasklist.example.com/123` ou `https://tasklist.example.com/list123/task456` |
| `entityLabel` ou `subEntityLabel`&emsp; | Étiquette de l’élément dans votre onglet, à utiliser lors de l’affichage du lien profond. | Liste des tâches 123 ou » Tâche 456 |
| `context.subEntityId`&emsp; | ID de l’élément dans l’onglet. Lors de la génération d’une URL pour la liaison approfondie, continuez à utiliser subEntityId comme nom de paramètre dans l’URL. Lors de la configuration de l’onglet, l’objet de contexte fait référence à subEntityID en tant que subPageID. |Tâche456 |
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
> Assurez-vous que tous les paramètres de requête sont encodés correctement en URI. Vous devez suivre les exemples précédents à l’aide du dernier exemple :
>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

## <a name="navigation-from-your-tab"></a>Navigation à partir de votre onglet

Vous pouvez accéder au contenu dans Teams à partir de votre onglet à l’aide de TeamsJS ou de liens profonds. Ceci est utile si votre onglet doit connecter les utilisateurs à d'autres contenus dans Teams, par exemple à un canal, un message, un autre onglet ou même pour ouvrir un dialogue de planification. Auparavant, la navigation pouvait nécessiter un lien profond, mais elle peut désormais être réalisée dans de nombreux cas à l'aide du SDK. Les sections suivantes montrent les deux méthodes, mais l’utilisation possible des fonctionnalités typées du Kit de développement logiciel (SDK) est recommandée.

L'un des avantages de l'utilisation de TeamsJS, en particulier pour les applications Teams susceptibles de fonctionner dans d'autres hôtes (Outlook et Office), est qu'il est possible de vérifier que l'hôte prend en charge la fonctionnalité que vous tentez d'utiliser. Pour vérifier la prise en charge d’une fonctionnalité par un hôte, vous pouvez utiliser la `isSupported()` fonction associée à l’espace de noms de l’API. Le SDK TeamsJS organise les API en capacités au moyen d'espaces de noms. Par exemple, avant l'utilisation d'une API dans `pages`l'espace de noms, vous pouvez vérifier la valeur booléenne renvoyée`pages.isSupported()` et prendre les mesures appropriées dans le contexte de votre application et de son interface utilisateur.  

Pour plus d’informations sur les fonctionnalités et les API dans TeamsJS, consultez [Création d’onglets et d’autres expériences hébergées avec le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](~/tabs/how-to/using-teams-client-sdk.md#apis-organized-into-capabilities).

### <a name="navigate-within-your-app"></a>Navigation dans votre application

Il est possible de naviguer dans une application à l’aide de TeamsJS. Le code suivant montre comment accéder à une entité spécifique dans votre application Teams.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

Vous pouvez déclencher une navigation à partir de votre onglet à l’aide de la fonction [pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true), comme indiqué dans le code suivant :

```javascript
if (pages.isSupported()) {
  const navPromise = pages.navigateToApp({ appId: <appId>, pageId: <pageId>, webUrl: <webUrl>, subPageId: <subPageId>, channelId:<channelId>});
  navPromise.
     then((result) => {/*Successful navigation*/}).
     catch((error) => {/*Failed navigation*/});
}
else { /* handle case where capability isn't supported */ }
```

Pour plus d’informations sur l’utilisation de la fonctionnalité pages, consultez [pages.navigateToApp()](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest#@microsoft-teams-js-pages-navigatetoapp&preserve-view=true) et l’espace de noms [pages](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) pour d’autres options de navigation. Si nécessaire, il est également possible d’ouvrir directement un lien profond à l’aide de la fonction [app.openLink()](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-openlink&preserve-view=true).

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

Pour déclencher un lien profond à partir de votre onglet, appelez :

```javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

---

### <a name="open-a-scheduling-dialog"></a>Ouvrir une boîte de dialogue

> [!NOTE]
> Pour ouvrir la boîte de dialogue de planification dans Teams, les développeurs doivent continuer d’utiliser la méthode basée sur l’URL de lien profond d’origine, car Teams ne prend pas encore en charge la fonctionnalité de calendrier.

Pour plus d'informations sur l'utilisation du calendrier, voir l'espace de noms du [calendrier](/javascript/api/@microsoft/teams-js/calendar?view=msteams-client-js-latest&preserve-view=true) dans la documentation de référence de l'API.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
// Open a scheduling dialog from your tab
if(calendar.isSupported()) {
   const calendarPromise = calendar.composeMeeting({
      attendees: ["joe@contoso.com", "bob@contoso.com"],
      content: "test content",
      endTime: "2018-10-24T10:30:00-07:00",
      startTime: "2018-10-24T10:00:00-07:00",
      subject: "test subject"});
   calendarPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");
```

---

Vous pouvez également créer manuellement des liens profonds vers la boîte de dialogue de planification intégrée de Teams.

#### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a>Générer un lien ciblé vers la boîte de dialogue de planification

Bien qu’il soit recommandé d’utiliser les API typées de TeamsJS, il est possible de créer manuellement des liens profonds vers la boîte de dialogue de planification intégrée Teams. Utilisez le format suivant pour un lien ciblé que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de message : `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`

Exemple : `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`

> [!NOTE]
> Les paramètres de recherche ne prennent pas en charge`+` le signal à la place de l’espace blanc (``). Vérifiez que votre code d’encodage d’URI retourne `%20`for spaces, par exemple, `?subject=test%20subject` est correct, mais `?subject=test+subject` est incorrect.

Les paramètres de requête sont les suivants :

* `attendees` : liste facultative d’ID utilisateur séparés par des virgules représentant les participants de la réunion. L’utilisateur qui effectue l’action est l’organisateur de la réunion. Actuellement, le champ ID utilisateur ne prend en charge que le UserPrincipalName d'Azure AD, généralement une adresse électronique.
* `startTime` : heure de début facultative de l’événement. Il doit être au [format ISO 8601 long](https://en.wikipedia.org/wiki/ISO_8601), par exemple *2018-03-12T23:55:25+02:00*.
* `endTime` : heure de fin facultative de l’événement, également au format ISO 8601.
* `subject` : champ facultatif pour l’objet de la réunion.
* `content` : champ facultatif pour le champ détails de la réunion.

> [!NOTE]
> Currently, specifying the location isn't supported. You must specify the UTC offset, it means time zones when generating your start and end times.

Pour utiliser ce lien profond avec votre bot, vous pouvez le spécifier comme cible d’URL dans le bouton de votre carte ou appuyer sur l’action via le type `openUrl`action.

### <a name="open-an-app-install-dialog"></a>Ouvrir une boîte de dialogue d’installation d’application

Vous pouvez ouvrir une boîte de dialogue d'installation d'application à partir de votre application Teams, comme le montre le code suivant.

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
// Open an app install dialog from your tab
if(appInstallDialog.isSupported()) {
    const dialogPromise = appInstallDialog.openAppInstallDialog({ appId: <appId>});
    dialogPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

Pour plus d’informations sur la boîte de dialogue d’installation, consultez la fonction [appInstallDialog.openAppInstallDialog()](/javascript/api/@microsoft/teams-js/appinstalldialog?view=msteams-client-js-latest#@microsoft-teams-js-appinstalldialog-openappinstalldialog&preserve-view=true) dans la documentation de référence de l’API.

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

---

### <a name="navigate-to-a-chat"></a>Accéder à une conversation

Vous pouvez naviguer ou créer des chats privés entre utilisateurs avec TeamsJS en spécifiant l'ensemble des participants. Si une conversation n'existe pas avec les participants spécifiés, l'utilisateur est dirigé vers une nouvelle conversation vide. Les nouvelles conversations sont créées dans un état brouillon jusqu’à ce que l’utilisateur envoie le premier message. Sinon, vous pouvez spécifier le nom de la conversation si elle n’existe pas déjà, ainsi que le texte qui doit être inséré dans la zone de composition de l’utilisateur. Vous pouvez considérer cette fonctionnalité comme un raccourci permettant à l’utilisateur d’effectuer l’action manuelle d’accéder à la conversation ou de la créer, puis de taper le message.

Par exemple, si vous renvoyez un profil utilisateur Office 365 à partir de votre bot sous forme de carte, ce lien profond peut permettre à l’utilisateur de discuter facilement avec cette personne. L’exemple suivant montre comment ouvrir un message de conversation à un groupe de participants avec un message initial.

```javascript
if(chat.isSupported()) {
    const chatPromise = chat.openGroupChat({ users: ["joe@contoso.com","bob@contoso.com"], topic: "Prep For Meeting Tomorrow", message: "Hi folks kicking off chat about our meeting tomorrow"});
    chatPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

Bien que l’utilisation des API typées soit recommandée, vous pouvez également utiliser le format suivant pour un lien profond créé manuellement que vous pouvez utiliser dans un bot, un connecteur ou une carte d’extension de message :

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Exemple : `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

Les paramètres de requête sont les suivants :

* `users` : liste séparée par des virgules des ID d’utilisateur représentant les participants de la conversation. L’utilisateur qui effectue l’action est toujours inclus en tant que participant. Actuellement, le champ ID d’utilisateur prend en charge Microsoft Azure Active Directory Domain Services (Azure AD) UserPrincipalName, telle qu’une adresse e-mail uniquement.
* `topicName`: champ facultatif pour le nom d’affichage de la conversation, si une conversation a au moins trois utilisateurs. Si ce champ n’est pas spécifié, le nom complet de la conversation est basé sur les noms des participants.
* `message` : champ facultatif pour le texte du message que vous souhaitez insérer dans la zone de composition de l’utilisateur actuel lorsque la conversation est dans un état brouillon.

Pour utiliser ce lien profond avec votre bot, spécifiez-le comme cible d’URL dans le bouton de votre carte ou appuyez sur l’action via le type `openUrl`action.

### <a name="generate-deep-links-to-channel-conversation"></a>Générer des liens profonds vers la conversation du canal

Utilisez ce format de lien profond pour accéder à une conversation particulière dans le thread de canal :

`https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

Exemple : `https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

Les paramètres de requête sont les suivants :

* `channelId` : ID du canal de la conversation. Par exemple : `19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2`.
* `tenantId` : ID de client tel que `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `groupId` : ID de groupe du fichier. Par exemple : `3606f714-ec2e-41b3-9ad1-6afb331bd35d`.
* `parentMessageId`: ID de message parent de la conversation.
* `teamName` : nom de l’équipe.
* `channelName` : nom du canal de l’équipe.

> [!NOTE]
> Vous pouvez voir `channelId`and `groupId` dans l’URL du canal.

### <a name="generate-deep-links-to-file-in-channel"></a>Générer des liens profonds vers un fichier dans le canal

Le format de lien profond suivant peut être utilisé dans un bot, un connecteur ou une carte d’extension de message :

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

Les paramètres de requête sont les suivants :

* `fileId`: Unique file ID from Sharepoint Online, also known as `sourcedoc`. For example,`1FA202A5-3762-4F10-B550-C04F81F6ACBD`.
* `tenantId` : ID de client tel que `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `fileType` : type de fichier pris en charge, tel que docx, pptx, xlsx et pdf.
* `objectUrl` : URL de l’objet du fichier. Le format est `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext`. Par exemple : `https://microsoft.sharepoint.com/teams/(filepath)`.
* `baseUrl` : URL de base du fichier. Le format est `https://{tenantName}.sharepoint.com/sites/{TeamName}`. Par exemple : `https://microsoft.sharepoint.com/teams`.
* `serviceName` : nom du service, ID d’application. Par exemple : `teams`.
* `threadId`: threadId est l’ID d’équipe de l’équipe où le fichier est stocké. Elle est facultative et ne peut pas être définie pour les fichiers stockés dans le dossier OneDrive d’un utilisateur. threadId : 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype.
* `groupId` : ID de groupe du fichier. Par exemple : `ae063b79-5315-4ddb-ba70-27328ba6c31e`.

> [!NOTE]
> Vous pouvez voir `threadId`and `groupId` dans l’URL du canal.  

Le format de lien profond suivant est utilisé dans un bot, un connecteur ou une carte d’extension de message :

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

L’exemple de format suivant illustre le lien profond vers les fichiers :

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

#### <a name="serialization-of-this-object"></a>Sérialisation de cet objet

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

Créez un lien profond pour l'application après son inscription dans le magasin Teams. Pour créer un lien pour lancer Teams, ajoutez l’ID d’application à l’URL suivante : `https://teams.microsoft.com/l/app/<your-app-id>`. Une boîte de dialogue s’affiche pour installer ou ouvrir l’application.

> [!NOTE]
> Si votre application a été approuvée pour la plateforme mobile, vous pouvez établir un lien profond vers une application mobile. L’ID d’équipe Apple App Store Connect est également requis pour que le lien approfondi fonctionne sur Teams-iOS. Pour plus d’informations, consultez [la mise à jour de l’ID d’équipe Apple App Store Connect](../deploy-and-publish/appsource/prepare/update-apple-store-team-connect-id.md).

### <a name="deep-linking-for-sharepoint-framework-tabs"></a>Liaison approfondie pour les onglets SharePoint Framework

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

## <a name="navigate-to-an-audio-or-audio-video-call"></a>Lien profond à un appel audio ou audio-vidéo

Vous pouvez lancer des appels audio uniquement ou audio-vidéo à un seul utilisateur ou à un groupe d'utilisateurs, en spécifiant le type d'appel et les participants. Avant de passer l'appel, le client Teams demande une confirmation pour effectuer l'appel. Dans le cas d’un appel de groupe, vous pouvez appeler un ensemble d’utilisateurs VoIP et un ensemble d’utilisateurs RTC dans le même appel de lien profond.

Dans un appel vidéo, le client demande une confirmation et active la vidéo de l’appelant pour l’appel. Le destinataire de l’appel a le choix entre répondre par audio uniquement ou audio et vidéo, via la fenêtre de notification d’appel Teams.

> [!NOTE]
> Cette méthode ne peut pas être utilisée pour appeler une réunion.

Le code suivant illustre l’utilisation du Kit de développement logiciel (SDK) TeamsJS pour démarrer un appel :

```javascript
if(call.isSupported()) {
    const callPromise = call.startCall({ targets: ["joe@contoso.com","bob@contoso.com","4:9876543210"], requestedModalities: [call.CallModalities.Audio], source: "demoApp"});
    callPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }

```

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Générer un lien profond pour partager du contenu à mettre en scène dans les réunions

Vous pouvez également générer un lien profond pour [partager l’application afin de](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md#share-entire-app-to-stage) mettre en scène et de démarrer ou de participer à une réunion.

> [!Note]
> Le lien profond permettant de partager du contenu vers une phase de réunion est pris en charge uniquement dans le client de bureau Teams.

Lorsqu’un lien profond est sélectionné dans une application par un utilisateur qui fait partie d’une réunion en cours, l’application est partagée à l’étape et une fenêtre contextuelle d’autorisation s’affiche. Les utilisateurs peuvent accorder des autorisations aux participants, telles que la co-édition d’un document ou la collaboration avec une application.

:::image type="content" source="../../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="La capture d’écran est un exemple montrant une fenêtre contextuelle d’autorisation.":::

Lorsque l’utilisateur n’est pas dans une réunion, l’utilisateur est redirigé vers le calendrier Teams où l’utilisateur doit participer à une réunion ou à une réunion instantanée (Réunion maintenant) peut être lancé.

:::image type="content" source="../../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="La capture d’écran est un exemple montrant une fenêtre contextuelle lorsqu’il n’y a pas de réunion en cours.":::

Une fois que l’utilisateur a lancé une réunion instantanée (Réunion maintenant), il peut ajouter des participants et interagir avec l’application.

:::image type="content" source="../../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="La capture d’écran est un exemple qui montre une option pour ajouter des participants et comment interagir avec l’application.":::

Pour ajouter un lien profond pour partager du contenu sur scène, vous devez disposer d’un contexte d’application. Le contexte d’application permet au client Teams d’extraire le manifeste de l’application et de vérifier si le partage sur scène est possible. Voici un exemple de contexte d’application.

* `{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

Les paramètres de requête pour le contexte d’application sont les suivants :

* `appID`: il s’agit de l’ID qui peut être obtenu à partir du manifeste de l’application.
* `appSharingUrl`: l’URL qui doit être partagée sur scène doit être un domaine valide défini dans le manifeste de l’application. Si l’URL n’est pas un domaine valide, une boîte de dialogue d’erreur s’affiche pour fournir à l’utilisateur une description de l’erreur.
* `useMeetNow`: cela inclut un paramètre booléen qui peut être vrai ou faux.
  * **True** : lorsque la `UseMeetNow` valeur est true et s’il n’y a pas de réunion en cours, une nouvelle réunion De réunion maintenant est lancée. Quand une réunion est en cours, cette valeur est ignorée.

  * **False** : la valeur `UseMeetNow` par défaut est false, ce qui signifie que lorsqu’un lien profond est partagé pour être mis en scène et qu’il n’y a pas de réunion en cours, une fenêtre contextuelle de calendrier s’affiche. Quand une réunion est en cours, le partage peut être effectué directement.

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
    |Pour partager l’application et ouvrir le calendrier Teams, lorsque UseMeeetNow a la valeur « false », par défaut.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|
    |Pour partager l’application et lancer une réunion instantanée, lorsque UseMeeetNow est « true ».|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Client de bureau d’équipe** : utilisez le format suivant pour lancer un lien profond à partir du client de bureau Teams pour partager du contenu sur scène.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Exemple : `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Lien profond|Format|Exemple|
    |---------|---------|---------|
    |Pour partager l’application et ouvrir le calendrier Teams, lorsque UseMeeetNow a la valeur « false », par défaut.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|
    |Pour partager l’application et lancer une réunion instantanée, lorsque UseMeeetNow est « true ».|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

Les paramètres de requête sont les suivants :

* `deepLinkId`: tout identificateur utilisé pour la corrélation de télémétrie.
* `fqdn`: `fqdn` est un paramètre facultatif, qui peut être utilisé pour basculer vers un environnement approprié d’une réunion pour partager une application sur scène. Il prend en charge les scénarios dans lesquels un partage d’application spécifique se produit dans un environnement particulier. La valeur par défaut est l’URL d’entreprise `fqdn` et les valeurs possibles sont `Teams.live.com` pour Teams for Life, `teams.microsoft.com`ou `teams.microsoft.us`.

Pour partager l’intégralité de l’application à l’étape, dans le manifeste de l’application, vous devez configurer `meetingStage` et `meetingSidePanel` , en tant que contextes d’image, voir [le manifeste de l’application](../../resources/schema/manifest-schema.md). Dans le cas contraire, les participants à la réunion peuvent ne pas être en mesure de voir le contenu sur scène.

## <a name="generate-a-deep-link-to-a-call"></a>Générer un lien profond vers un appel

Bien que l’utilisation des API typées de TeamsJS soit recommandée, vous pouvez également utiliser un lien profond créé manuellement pour démarrer un appel.

| Lien profond | Format | Exemple |
|-----------|--------|---------|
| Passer un appel audio | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com` |
| Effectuer des appels audio et vidéo | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true` |
|Passer un appel audio et vidéo avec une source de paramètre facultative | `https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>&withVideo=true&source=demoApp` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withVideo=true&source=demoApp` |  
| Effectuer un appel audio et vidéo à une combinaison d’utilisateurs VoIP et RTC | `https://teams.microsoft.com/l/call/0/0?users=<user1>,4:<phonenumber>` | `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210` |
  
Voici les paramètres de requête :

* `users` : liste séparée par des virgules des ID d’utilisateur représentant les participants de l’appel. Actuellement, le champ ID d’utilisateur prend en charge le UserPrincipalName Azure AD, généralement une adresse e-mail, ou lors d’un appel RTC, il prend en charge un RTC mri 4 :&lt;numéro de téléphone&gt;.
* `withVideo` : il s’agit d’un paramètre facultatif que vous pouvez utiliser pour effectuer un appel vidéo. La définition de ce paramètre active uniquement la caméra de l’appelant. Le destinataire de l’appel peut répondre par le biais d’un appel audio ou audio et vidéo via la fenêtre de notification d’appel Teams.
* `Source` : il s’agit d’un paramètre facultatif, qui informe sur la source du lien profond.

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|ID de sous-entité consommateur de liens profonds  | Exemple d'application Teams pour la démonstration d'un lien profond entre une conversation bot et un onglet consommant un ID de sous-entité.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a>Voir aussi

* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
* [Moodle LMS](~/resources/moodleinstructions.md)
