---
title: Utiliser Microsoft Graph pour autoriser l’installation proactive d’un bot et la messagerie dans Teams
description: Décrit la messagerie proactive dans Teams et comment implémenter.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: équipes d’installation de conversation de messagerie proactive Graph
ms.openlocfilehash: 0ece7d3ec3a9e00774ff2f529f7c38bc1932469d
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069086"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Installation proactive d’applications utilisant Graph API pour envoyer des messages

>[!IMPORTANT]
> Microsoft Graph et Microsoft Teams prévisualisations publiques sont disponibles pour un accès et des commentaires en avant-première. Bien que cette version ait fait l’objet de tests approfondis, elle n’est pas destinée à être mise en production.

## <a name="proactive-messaging-in-teams"></a>Messagerie proactive dans Teams

Les messages proactifs sont initiés par des bots pour démarrer des conversations avec un utilisateur. Ils servent de nombreuses fonctions, notamment l’envoi de messages de bienvenue, la conduite d’enquêtes ou d’enquêtes et la diffusion de notifications à l’échelle de l’organisation. Les messages proactifs Teams peuvent être remis en tant que conversations **ad hoc** ou basées **sur des** boîtes de dialogue :

|Type de message | Description |
|----------------|-------------- |
|Message proactif ad hoc| Le bot interjecte un message sans interrompre le flux de conversation.|
|Message proactif basé sur la boîte de dialogue | Le bot crée un thread de boîte de dialogue, prend le contrôle d’une conversation, remet le message proactif, ferme et renvoie le contrôle à la boîte de dialogue précédente.|

## <a name="proactive-app-installation-in-teams"></a>Installation proactive de l’application dans Teams

Pour que votre bot puisse envoyer un message de manière proactive à un utilisateur, il doit être installé en tant qu’application personnelle ou dans une équipe dont l’utilisateur est membre. Parfois, vous devez envoyer un message de manière proactive aux utilisateurs qui n’ont pas installé votre application ou qui ont déjà interagi avec celle-là. Par exemple, la nécessité de transmettre des informations vitales à tous les membres de votre organisation. Pour de tels scénarios, vous pouvez utiliser l’API Microsoft Graph pour installer votre bot de manière proactive pour vos utilisateurs.

## <a name="permissions"></a>Autorisations

Les autorisations de type de ressource Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) vous aident à gérer le cycle de vie d’installation de votre application pour toutes les étendues utilisateur (personnelle) ou d’équipe (canal) au sein de la plateforme Microsoft Teams :

|Autorisation de l’application | Description|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permet à une application Teams de lire, d’installer, de mettre à niveau et de se désinstaller elle-même pour n’importe quel **utilisateur,** sans se connecter ou utiliser préalablement.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permet à une Teams de lire, d’installer, de mettre à niveau et de se désinstaller elle-même dans n’importe quelle **équipe,** sans se connecter ou utiliser préalablement.|

Pour utiliser ces autorisations, vous devez ajouter une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id** : votre ID d’application Azure AD.
> * **ressource** : URL de ressource pour l’application.
>
>[!NOTE]
>
> * Votre bot nécessite des autorisations d’application et non des autorisations déléguées par l’utilisateur, car l’installation est pour d’autres utilisateurs.
>
> * Un administrateur client Azure AD doit explicitement [accorder des autorisations à une application.](/graph/security-authorization#grant-permissions-to-an-application) Une fois qu’une application a reçu des autorisations, tous les membres du client Azure AD ont les autorisations accordées.

## <a name="enable-proactive-app-installation-and-messaging"></a>Activer l’installation proactive de l’application et la messagerie

> [!IMPORTANT]
>Microsoft Graph installer uniquement les applications publiées dans le magasin d’applications de votre organisation ou le Teams store.

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ créer et publier votre bot de messagerie proactive pour Teams

To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with proactive [messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that’s in your [organization’s app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the Teams [store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).

>[!TIP]
> Le modèle d’application [**Communicator**](../..//samples/app-templates.md#company-communicator) entreprise prêt pour la production autorise la diffusion de messagerie et constitue une bonne base pour la création de votre application de bot proactive.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ obtenir `teamsAppId` l’application

**1. Vous** en avez besoin `teamsAppId` pour les étapes suivantes.

Les `teamsAppId` données peuvent être récupérées à partir du catalogue d’applications de votre organisation :

**Référence de la page Graph Microsoft :** type de ressource [teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**Requête HTTP GET** :

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

La demande doit renvoyer un `teamsApp` objet. L’objet renvoyé est l’ID d’application généré par le catalogue de l’application et est différent de l’ID que vous avez fourni dans `id` votre manifeste Teams’application :

```json
{
  "value": [
    {
      "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
      "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
      "name": "Test App",
      "version": "1.0.1",
      "distributionMethod": "Organization"
    }
  ]
}
```

**2.**  Si votre application a déjà été téléchargée ou téléchargée de manière secondaire pour un utilisateur dans l’étendue personnelle, vous pouvez récupérer les données `teamsAppId` suivantes :

**Référence Graph page** microsoft : [liste des applications installées pour l’utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Requête HTTP GET** :

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Si votre application a été téléchargée ou téléchargée de manière secondaire pour un canal dans l’étendue de l’équipe, vous pouvez récupérer les données `teamsAppId` suivantes :

**Référence de page Graph Microsoft : lister** [les applications en équipe](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Requête HTTP GET** :

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Pour affiner la liste des résultats, vous pouvez filtrer sur n’importe quel champ de [**l’objet teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ déterminer si votre bot est actuellement installé pour un destinataire de message

**Référence Graph page** microsoft : [liste des applications installées pour l’utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Requête HTTP GET** :

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Cette demande renvoie un tableau vide si l’application n’est pas installée et un tableau avec un seul objet [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si l’application est installée.

### <a name="-install-your-app"></a>✔ installer votre application

**Référence de page Graph Microsoft : installer** [l’application pour l’utilisateur](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**Requête HTTP POST** :

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si l’utilisateur a Microsoft Teams en cours d’exécution, l’installation de l’application s’exécute immédiatement. Un redémarrage peut être nécessaire pour afficher l’application installée.

### <a name="-retrieve-the-conversation-chatid"></a>✔ récupérer la conversation **chatId**

Lorsque votre application est installée pour l’utilisateur, le bot reçoit une notification d’événement qui contient les informations nécessaires `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) pour envoyer le message proactif.

Les `chatId` données peuvent également être récupérées comme suit :

**Référence de la page Graph Microsoft : obtenir** une [conversation](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** Vous devez avoir besoin de votre `{teamsAppInstallationId}` application. Si vous ne l’avez pas, utilisez ce qui suit :

**Requête HTTP GET** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La **propriété id** de la réponse est le `teamsAppInstallationId` .

**2. Faites** la demande suivante pour récupérer le `chatId` :

**Requête HTTP GET** (autorisation — `TeamsAppInstallation.ReadWriteSelfForUser.All` ) :  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

La **propriété id** de la réponse est le `chatId` .

Vous pouvez également récupérer la `chatId` requête avec la requête suivante, mais elle requiert l’autorisation plus large `Chat.Read.All` :

**Requête HTTP GET** (autorisation — `Chat.Read.All` ) :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ messages proactifs

Votre bot peut [envoyer des messages proactifs](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) une fois qu’il a été ajouté pour un utilisateur ou une équipe et qu’il a reçu toutes les informations utilisateur.

## <a name="see-also"></a>Voir aussi

* [**Gérer les stratégies de configuration d’application dans Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Envoyer des notifications proactives aux utilisateurs SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a>Afficher des exemples de code supplémentaires
>
> [!div class="nextstepaction"]
> [**Teams exemples de code de messagerie proactifs**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
