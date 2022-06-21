---
title: Utilisez Microsoft Graph pour autoriser l'installation de robots proactifs et l'envoi de messages dans Teams.
description: Cet article décrit la messagerie proactive dans Teams et comment l’implémenter. Découvrez comment activer l’installation proactive des applications et la conversation à l’aide d’un exemple de code.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
ms.openlocfilehash: 832dfe6ddce7710d506c480fc1195c426b8da0df
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189582"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Installation proactive d’applications à l’aide de l’API Graph pour envoyer des messages

## <a name="proactive-messaging-in-teams"></a>Messagerie proactive dans Teams

Les messages proactifs sont lancés par les bots pour démarrer des conversations avec un utilisateur. Ils servent de nombreux objectifs, notamment l’envoi de messages d’accueil, la réalisation d’enquêtes ou de sondages et la diffusion de notifications à l’échelle de l’organisation. Les messages proactifs dans Teams peuvent être remis en tant que conversations **ad hoc** ou **basées sur** des dialogues :

|Type de message | Description |
|----------------|-------------- |
|Message proactif ad hoc| Le robot interjecte un message sans interrompre le flux de la conversation.|
|Message proactif basé sur une boîte de dialogue | Le bot crée un thread de dialogue, prend le contrôle d’une conversation, remet le message proactif, ferme et retourne le contrôle à la boîte de dialogue précédente.|

## <a name="proactive-app-installation-in-teams"></a>Installation proactive d’applications dans Teams

Pour que votre bot puisse faire passer un message proactif à un utilisateur, il doit être installé en tant qu’application personnelle ou dans une équipe où l’utilisateur est membre. Parfois, vous devez envoyer des messages proactifs aux utilisateurs qui n’ont pas installé ou qui ont déjà interagi avec votre application. Par exemple, si vous devez envoyer des informations importantes à tous les membres de votre organisation, vous pouvez utiliser microsoft API Graph pour installer votre bot de manière proactive pour vos utilisateurs.

## <a name="permissions"></a>Autorisations

Les autorisations de [type de ressource Microsoft Graph teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) vous aident à gérer le cycle de vie d’installation de votre application pour toutes les étendues d’utilisateur (personnel) ou d’équipe (canal) au sein de la plateforme Microsoft Teams :

|Autorisation d’application | Description|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permet à une application Teams de lire, d’installer, de mettre à niveau et de désinstaller elle-même pour *n’importe quel utilisateur*, sans connexion ni utilisation préalable.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permet à Teams de lire, d’installer, de mettre à jour et de se désinstaller elle-même dans une *équipe*, sans utilisateur connecté.|

Pour utiliser ces autorisations, vous devez ajouter une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

* **id** : ID de votre application Azure Active Directory
* **ressource** : URL de ressource pour l’application

> [!NOTE]
>
> * Votre bot nécessite des autorisations d’application et non des autorisations déléguées par l’utilisateur, car l’installation est destinée à d’autres utilisateurs.
>
> * Un administrateur de locataire Microsoft Azure Active Directory doit [explicitement accorder des autorisations à une application](/graph/security-authorization#grant-permissions-to-an-application). Une fois les autorisations accordées à l’application, tous les membres du client Microsoft Azure Active Directory obtiennent les autorisations accordées.

## <a name="enable-proactive-app-installation-and-messaging"></a>Activer l’installation proactive du bot et de la messagerie proactive

> [!IMPORTANT]
> Microsoft Graph ne peut installer que les applications publiées sur l’App Store de votre organisation ou le magasin Teams.

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>Créer et publier votre bot de messagerie proactive pour Teams

Pour commencer, vous avez besoin d’un [bot pour Teams](../../bots/how-to/create-a-bot-for-teams.md) avec des fonctionnalités de [messagerie proactive](../../concepts/bots/bot-conversations/bots-conv-proactive.md) qui se trouve dans [l’App Store de votre organisation](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) ou dans le [magasin Teams](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).

> [!TIP]
> Le modèle d’application [*Company Communicator*](../..//samples/app-templates.md#company-communicator) prêt pour la production autorise la messagerie de diffusion et constitue un bon point de départ pour créer votre application de bot proactive.

### <a name="get-the-teamsappid-for-your-app"></a>Obtenir `teamsAppId` pour votre application

Vous pouvez effectuer ce `teamsAppId` des façons suivantes :

* À partir du catalogue d’applications de votre organisation :

    **Informations de référence sur la page Microsoft Graph :** [type de ressource teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    Demande **HTTP GET** :

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    La demande doit retourner un `teamsApp` objet `id`, qui est l’ID d’application généré par le catalogue de l’application. Cela diffère de l’ID que vous avez fourni dans votre manifeste d’application Teams :

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

* Si votre application a déjà été chargée ou chargée de manière indépendante pour un utilisateur dans une étendue personnelle :

    **Informations de référence sur la page Microsoft Graph :** [Répertorier les applications installées pour l’utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    Demande **HTTP GET** :

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* Si votre application a déjà été chargée ou chargée de manière test pour un canal dans l’étendue de l’équipe :

    **Informations de référence sur la page Microsoft Graph :** [Répertorier les applications en équipe](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    Demande **HTTP GET** :

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > Pour affiner la liste des résultats, vous pouvez filtrer n’importe quel champ de l’objet [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true).

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>Déterminer si votre bot est actuellement installé pour un destinataire de message

Vous pouvez déterminer si votre bot est actuellement installé pour un destinataire de message comme suit :

**Informations de référence sur la page Microsoft Graph :** [Répertorier les applications installées pour l’utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

Demande **HTTP GET** :

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La requête renvoie aux :

* Tableau vide si l’application n’est pas installée.
* Tableau avec un objet [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) unique si l’application est installée.

### <a name="install-your-app"></a>Installez votre application.

Vous pouvez installer votre application comme suit :

**Informations de référence sur la page Microsoft Graph :** [Installer l’application pour l’utilisateur](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

Demande **HTTP POST**

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si l’utilisateur a Microsoft Teams en cours d’exécution, l’installation de l’application se produit immédiatement. Un redémarrage peut être nécessaire pour afficher l’application installée.

### <a name="retrieve-the-conversation-chatid"></a>Récupérer la conversation `chatId`

Lorsque votre application est installée pour l’utilisateur, le bot reçoit une `conversationUpdate`[notification d’événement](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)v qui contient les informations nécessaires pour envoyer le message proactif.

Informations de référence sur la **page Microsoft Graph :** [Obtenir une conversation](/graph/api/chat-get?view=graph-rest-v1.0&tabs=http&preserve-view=true)

1. Vous devez disposer de `{teamsAppInstallationId}`votre application . Si vous ne l’avez pas, utilisez les éléments suivants :

    Demande **HTTP GET** :

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    La propriété **id** de la réponse est le `teamsAppInstallationId`.

1. Effectuez la requête suivante pour récupérer les `chatId`éléments suivants :

    **Requête HTTP GET** (autorisation) :`TeamsAppInstallation.ReadWriteSelfForUser.All`  

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    La propriété **id** de la réponse est le `chatId`.

    Vous pouvez également récupérer la `chatId` requête avec la suivante, mais elle nécessite l’autorisation plus large `Chat.Read.All` :

    **Requête HTTP GET** (autorisation) :`Chat.Read.All`

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a>Envoyer des messages proactifs

Votre bot peut [envoyer des messages proactifs](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) une fois le bot ajouté pour un utilisateur ou une équipe et avoir reçu toutes les informations utilisateur.

## <a name="code-snippets"></a>Extraits de code

Le code suivant fournit un exemple d’envoi de messages proactifs :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public async Task<int> SendNotificationToAllUsersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
   int msgSentCount = 0;

   // Send notification to all the members
   foreach (var conversationReference in _conversationReferences.Values)
   {
       await turnContext.Adapter.ContinueConversationAsync(_configuration["MicrosoftAppId"], conversationReference, BotCallback, cancellationToken);
       msgSentCount++;
   }

   return msgSentCount;
}

private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
{
   await turnContext.SendActivityAsync("Proactive hello.");
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
server.get('/api/notify', async (req, res) => {
    for (const conversationReference of Object.values(conversationReferences)) {
        await adapter.continueConversationAsync(process.env.MicrosoftAppId, conversationReference, async context => {
            await context.sendActivity('proactive hello');
        });
    }

    res.setHeader('Content-Type', 'text/html');
    res.writeHead(200);
    res.write('<html><body><h1>Proactive messages have been sent.</h1></body></html>');
    res.end();
});
```

---

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|
| Installation proactive de l’application et envoi de notifications proactives | Cet exemple indique comment utiliser l’installation proactive de l’application pour les utilisateurs et envoyer des notifications proactives en appelant les API Microsoft Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="additional-code-samples"></a>Exemples de code d’application de messagerie supplémentaires
>
> [!div class="nextstepaction"]
> [**Exemples de code Teams de messagerie proactive**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>Voir aussi

* [Gérer les stratégies de mise en application dans Teams](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [Envoyer des notifications proactives aux utilisateurs SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)
