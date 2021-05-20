---
title: Utilisez Microsoft Graph autoriser l’installation proactive de bots et la messagerie dans Teams
description: Décrit les messages proactifs dans les Teams la façon de mettre en œuvre.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: équipes proactives d’installation de chat de messagerie Graph
ms.openlocfilehash: 06b50e5ab8594c257959430383bab5e355af4e06
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566151"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>Installation proactive d’applications à l’aide de l’API Graph et envoi de messages

>[!IMPORTANT]
> Microsoft Graph et Microsoft Teams aperçus publics sont disponibles pour un accès précoce et des commentaires. Bien que cette version ait fait l’objet d’essais approfondis, elle n’est pas destinée à être utilisé en production.

## <a name="proactive-messaging-in-teams"></a>Messagerie proactive en Teams

Les messages proactifs sont initiés par des bots pour démarrer des conversations avec un utilisateur. Ils servent à de nombreuses fins, y compris l’envoi de messages de bienvenue, la réalisation de sondages ou de sondages, et la diffusion de notifications à l’échelle de l’organisation. Les messages proactifs Teams peuvent être transmis sous forme de conversations **ad hoc** **ou dialoguées** :

|Type de message | Description |
|----------------|-------------- |
|Message proactif ad hoc| Le bot interjecte un message sans interrompre le flux de conversation.|
|Message proactif basé sur le dialogue | Le bot crée un nouveau thread de dialogue, prend le contrôle d’une conversation, délivre le message proactif, ferme et renvoie le contrôle au dialogue précédent.|

## <a name="proactive-app-installation-in-teams"></a>Installation proactive d’applications dans Teams

Avant que votre bot puisse envoyer un message proactif à un utilisateur, il doit être installé soit comme une application personnelle, soit dans une équipe où l’utilisateur est membre. Parfois, vous devez envoyer un message proactif aux utilisateurs qui n’ont pas installé ou interagi auparavant avec votre application. Par exemple, la nécessité de transmettre des informations vitales à tous les membres de votre organisation. Pour de tels scénarios, vous pouvez utiliser l’API Graph Microsoft pour installer proactivement votre bot pour vos utilisateurs.

## <a name="permissions"></a>Autorisations

Microsoft Graph les autorisations de [type ressources d’installation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) d’Applications vous aident à gérer le cycle de vie d’installation de votre application pour toutes les étendues utilisateur (personnel) ou d’équipe (canal) dans la plate-forme Microsoft Teams :

|Autorisation de l’application | Description|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permet à une Teams de lire, installer, mettre à niveau et désinstaller pour tout **utilisateur,** sans se connecter ou utiliser préalablement.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permet à une Teams de lire, installer, mettre à niveau et se désinstaller dans n’importe **quelle** équipe, sans se connecter ou utiliser préalablement.|

Pour utiliser ces autorisations, vous devez ajouter une [clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id** — votre identifiant d’application Azure AD.
> * **ressource** — l’URL de ressources de l’application.
>
>[!NOTE]
>
> * Votre bot nécessite une application et non des autorisations déléguées par l’utilisateur parce que l’installation est pour d’autres.
>
> * Un administrateur locataire Azure AD doit [explicitement accorder des autorisations à une application](/graph/security-authorization#grant-permissions-to-an-application). Une fois qu’une demande est accordée, tous les membres du locataire Azure AD obtiennent les autorisations accordées.

## <a name="enable-proactive-app-installation-and-messaging"></a>Activer l’installation proactive d’applications et la messagerie

> [!IMPORTANT]
>Microsoft Graph pouvez installer uniquement des applications publiées sur l’App Store de votre organisation ou sur le Teams store.

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ créer et publier votre bot de messagerie proactif pour Teams

Pour commencer, vous avez besoin [d’un bot pour Teams](../../bots/how-to/create-a-bot-for-teams.md) avec des capacités de messagerie [proactives](../../concepts/bots/bot-conversations/bots-conv-proactive.md) qui est dans [l’App Store de votre organisation](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) ou le magasin [Teams.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)

>[!TIP]
> Le modèle d’application [**Communicator de l’entreprise**](../..//samples/app-templates.md#company-communicator) prêt à la production permet la diffusion de messages et est une bonne base pour la construction de votre application proactive bot.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ Obtenez le `teamsAppId` pour votre application

**1. Vous** avez besoin `teamsAppId` de la pour les prochaines étapes.

Le `teamsAppId` peut être récupéré à partir du catalogue d’applications de votre organisation :

**Référence de Graph page Microsoft :** type de ressource [teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**HTTP GET** demande:

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

La demande doit retourner un `teamsApp` objet. L’objet retourné `id` est l’iD d’application généré par le catalogue de l’application et est différent de l’ID que vous avez fourni dans votre Teams manifeste de l’application :

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

**2.**  Si votre application a déjà été téléchargée ou déchargée latéralement pour un utilisateur dans le champ d’application personnel, vous pouvez récupérer les `teamsAppId` informations suivantes :

**Référence de Graph page Microsoft : Liste des** applications [installées pour les utilisateurs](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** demande:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** Si votre application a été téléchargée ou déchargée latéralement pour un canal dans la portée de l’équipe, vous pouvez récupérer les `teamsAppId` informations suivantes :

**Référence de Graph page microsoft : Liste des** applications en [équipe](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** demande:

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> Pour affiner la liste des résultats, vous pouvez filtrer sur n’importe quel domaine de [**l’objet teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ déterminer si votre bot est actuellement installé pour un destinataire de message

**Référence de Graph page Microsoft : Liste des** applications [installées pour les utilisateurs](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** demande:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Cette demande renvoie un tableau vide si l’application n’est pas installée et un tableau avec un [seul objet teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si l’application est installée.

### <a name="-install-your-app"></a>✔ installez votre application

**Référence de Graph page Microsoft : Installer une** application pour [l’utilisateur](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**DEMANDE HTTP POST:**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si l’utilisateur a été Microsoft Teams, l’installation de l’application est vue immédiatement. Un redémarrage peut être nécessaire pour afficher l’application installée.

### <a name="-retrieve-the-conversation-chatid"></a>✔ récupérer la conversation **chatId**

Lorsque votre application est installée pour l’utilisateur, le bot reçoit une `conversationUpdate` [notification d’événement](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) qui contient les informations nécessaires pour envoyer le message proactif.

Le `chatId` peut également être récupéré comme suit:

**Référence de la page Graph Microsoft : Obtenez** le [chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** Vous devez avoir besoin de votre application `{teamsAppInstallationId}` . Si vous ne l’avez pas, utilisez les éléments suivants :

**HTTP GET** demande:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La **propriété id** de la réponse est le `teamsAppInstallationId` .

**2.** Faites la demande suivante pour aller chercher les `chatId` :

**HTTP GET** demande (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All` :  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

La **propriété id** de la réponse est le `chatId` .

Vous pouvez également récupérer le avec `chatId` la demande suivante, mais il nécessite l’autorisation plus `Chat.Read.All` large:

**HTTP GET** demande (permission — `Chat.Read.All` :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ envoyer des messages proactifs

Votre bot peut [envoyer des messages proactifs](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) après l’ajout du bot pour un utilisateur ou une équipe et a reçu toutes les informations utilisateur.

## <a name="see-also"></a>Voir aussi

* [**Gérer les stratégies de mise en application dans Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Envoyer des notifications proactives aux utilisateurs SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a>Afficher des échantillons de code supplémentaires
>
> [!div class="nextstepaction"]
> [**Teams échantillons de code de messagerie proactifs**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)