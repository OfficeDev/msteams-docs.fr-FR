---
title: Utiliser Microsoft Graph pour activer l’installation et la messagerie de robots proactifs dans teams
description: Décrit la messagerie proactive dans teams et la mise en œuvre.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Graphique d’installation de conversation de messagerie proactive teams
ms.openlocfilehash: 735dbfa39222f312b4f3714b5c009dfd1bf28b05
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434495"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Activation de l’installation proactive du bot et de la messagerie proactive dans teams avec Microsoft Graph (préversion publique)

>[!IMPORTANT]
> Les aperçus publics de Microsoft Graph sont disponibles pour l’accès anticipé et les commentaires. Bien que cette version ait subi des tests approfondis, elle n’est pas destinée à être utilisée en production.

## <a name="proactive-messaging-in-teams"></a>Messagerie proactive dans teams

Les messages proactifs sont initiés par les robots pour démarrer des conversations avec des utilisateurs. Elles répondent à de nombreux objectifs, notamment en envoyant des messages de bienvenue, en effectuant des enquêtes ou des sondages et en diffusant des notifications à l’échelle de l’organisation.  Les messages proactifs dans teams peuvent être fournis sous la forme de conversations **ad hoc** ou **basées sur des boîtes de dialogue** :

|Type de message | Description |
|----------------|-------------- |
|Message proactif ad hoc| Le bot prorompre un message sans interrompre le flux de conversation.|
|Message proactif basé sur des boîtes de dialogue | Le bot crée un nouveau thread, prend le contrôle d’une conversation, remet le message proactif, se ferme et renvoie le contrôle à la boîte de dialogue précédente.|

*Voir*, [Envoyer des notifications proactives au kit de développement logiciel (SDK) v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)

## <a name="proactive-app-installation-in-teams"></a>Installation de l’application proactive dans teams

Pour que votre robot puisse messageer de manière proactive un utilisateur, il doit être installé en tant qu’application personnelle ou dans une équipe où l’utilisateur est membre. Parfois, vous devrez peut-être communiquer de manière proactive les utilisateurs qui _n’ont pas_ installé ou précédemment interagi avec votre application. Par exemple, la nécessité de messageer des informations vitales à tous les membres de votre organisation. Pour ces scénarios, vous pouvez utiliser l’API Microsoft Graph pour installer votre robot de manière proactive pour vos utilisateurs.

## <a name="permissions"></a>Autorisations

Les autorisations de [type de ressource](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) Microsoft Graph teamsAppInstallation vous permettent de gérer le cycle de vie de l’installation de votre application pour toutes les étendues utilisateur (personnelles) ou d’équipe (canal) au sein de la plateforme Microsoft teams :

|Autorisation de l’application | Description|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Permet à une application de teams de lire, d’installer, de mettre à niveau et de désinstaller lui-même pour tout **utilisateur**, sans connexion ni utilisation préalable.|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Permet à une application de teams de lire, d’installer, de mettre à niveau et de désinstaller elle-même dans n’importe quelle **équipe**, sans connexion ni utilisation préalable.|

Pour utiliser ces autorisations, vous devez ajouter une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **ID** : votre ID d’application Azure ad.
> * **ressource** — l’URL de la ressource pour l’application.
>

>[!NOTE]
>
> * Votre bot requiert des autorisations _déléguées_ de l' _application_ , car l’installation n’est pas pour vous, mais pour d’autres.
>
> * Un administrateur client Azure AD doit [accorder explicitement des autorisations à une application](/graph/security-authorization#grant-permissions-to-an-application). Une fois qu’une application reçoit des autorisations, _tous_ les membres du client Azure ad bénéficient des autorisations accordées.

## <a name="enable-proactive-app-installation-and-messaging"></a>Activation de la messagerie et de l’installation de l’application proactive

 > [!IMPORTANT]
>Microsoft Graph installe uniquement les applications publiées dans le [catalogue d’applications](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) de votre organisation ou dans [AppSource](https://appsource.microsoft.com/).

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Créer et publier votre robot de messagerie proactive pour teams

Pour commencer, vous aurez besoin d’un [bot pour teams](../../bots/how-to/create-a-bot-for-teams.md) avec des fonctionnalités de [messagerie proactive](../../concepts/bots/bot-conversations/bots-conv-proactive.md) et [publié](../../concepts/deploy-and-publish/overview.md) dans le [catalogue d’applications](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) de votre organisation ou dans [AppSource](https://appsource.microsoft.com/).

>[!TIP]
> Le modèle d’application [**Communicator**](../..//samples/app-templates.md#company-communicator) de l’entreprise prête pour la production permet la messagerie de diffusion et constitue une base intéressante pour la création de votre application bot proactive.

### <a name="-get-the-teamsappid-for-your-app"></a>✔ Obtenir le `teamsAppId` pour votre application

**1.** vous en aurez besoin `teamsAppId` pour les étapes suivantes.

Le `teamsAppId` peut être récupéré à partir du catalogue d’applications de votre organisation :

**Référence de la page Microsoft Graph :** [type de ressource teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0)

Requête **Get http** :

```http
GET https://graph.microsoft.com/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

La demande renverra un `teamsApp` objet. L’objet renvoyé `id` est l’ID de l’application générée par le catalogue de l’application et est différent du « ID : » que vous avez fourni dans le manifeste de votre application teams :

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

**2.** si votre application a déjà été téléchargée/versions test chargées pour un utilisateur dans l’étendue personnelle, vous pouvez récupérer les `teamsAppId` éléments suivants :

**Référence de la page Microsoft Graph :** [répertorier les applications installées pour l’utilisateur](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

Requête **Get http** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

**3.** si votre application a déjà été téléchargée/versions test chargées pour un canal dans l’étendue de l’équipe, vous pouvez récupérer les `teamsAppId` éléments suivants :

**Référence de la page Microsoft Graph :** [répertorier les applications dans Team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)

Requête **Get http** :

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> Vous pouvez filtrer les champs de l’objet [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) pour affiner la liste des résultats.

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ Déterminer si votre bot est actuellement installé pour un destinataire de message

**Référence de la page Microsoft Graph :** [répertorier les applications installées pour l’utilisateur](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

Requête **Get http** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

Cette requête renverra un tableau vide si l’application n’est pas installée ou une baie avec un seul objet [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) , si elle a été installée.

### <a name="-install-your-app"></a>✔ Installer votre application

**Référence Microsoft Graph :** [installer l’application pour l’utilisateur](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)

Demande **http post** :

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

Si Microsoft teams est en cours d’exécution pour l’utilisateur, l’installation de l’application peut s’afficher immédiatement. Un redémarrage peut également être nécessaire pour afficher l’application installée.

### <a name="-retrieve-the-conversation-chatid"></a>✔ Récupérer le **chatId** de conversation

Lorsque votre application est installée pour l’utilisateur, le bot reçoit une `conversationUpdate` [notification d’événement](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) qui contiendra les informations nécessaires pour envoyer le message proactif.

Le `chatId` peut également être récupéré comme suit :

**Référence Microsoft Graph :** [obtenir une conversation](/graph/api/chat-get?view=graph-rest-beta&tabs=http)

**1.** vous aurez besoin de votre application `{teamsAppInstallationId}` si vous ne l’avez pas, utilisez les éléments suivants :

Requête **Get http** :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

La propriété **ID** de la réponse est l' `teamsAppInstallationId` .

**2.** effectuez la requête suivante pour extraire les `chatId` éléments suivants :

Requête **http Get** (autorisation `TeamsAppInstallation.ReadWriteSelfForUser.All` ) :  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

La propriété **ID** de la réponse est l' `chatId` .

Vous pouvez également récupérer les `chatId` avec la demande ci-dessous, mais cela nécessite une autorisation plus large `Chat.Read.All` :

Requête **http Get** (autorisation `Chat.Read.All` ) :

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ Envoyer des messages proactifs

Une fois que votre robot a été ajouté pour un utilisateur ou une équipe et qu’il a acquis les informations d’utilisateur nécessaires, il peut commencer à [Envoyer des messages proactifs](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).

# <a name="c--net"></a>[C#/.NET](#tab/csharp)

L’extrait de code suivant provient des [exemples de l’infrastructure Microsoft bot pour C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

```csharp
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Bot.Builder;
using Microsoft.Bot.Schema;

namespace Microsoft.BotBuilderSamples
{
    public class ProactiveBot : ActivityHandler
    {
        // Message to send to users when the bot receives a Conversation Update event
        private const string WelcomeMessage = "Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.";

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

        public ProactiveBot(ConcurrentDictionary<string, ConversationReference> conversationReferences)
        {
            _conversationReferences = conversationReferences;
        }

        private void AddConversationReference(Activity activity)
        {
            var conversationReference = activity.GetConversationReference();
            _conversationReferences.AddOrUpdate(conversationReference.User.Id, conversationReference, (key, newValue) => conversationReference);
        }

        protected override Task OnConversationUpdateActivityAsync(ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            return base.OnConversationUpdateActivityAsync(turnContext, cancellationToken);
        }

        protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            foreach (var member in membersAdded)
            {
                // Greet anyone that was not the target (recipient) of this message.
                if (member.Id != turnContext.Activity.Recipient.Id)
                {
                    await turnContext.SendActivityAsync(MessageFactory.Text(WelcomeMessage), cancellationToken);
                }
            }
        }

        protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            // Echo back what the user said
            await turnContext.SendActivityAsync(MessageFactory.Text($"You sent '{turnContext.Activity.Text}'"), cancellationToken);
        }
    }
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

L’extrait de code suivant provient des [exemples de Microsoft bot Framework pour JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).

```javascript
const { ActivityHandler, TurnContext } = require('botbuilder');

class ProactiveBot extends ActivityHandler {
    constructor(conversationReferences) {
        super();

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        this.conversationReferences = conversationReferences;

        this.onConversationUpdate(async (context, next) => {
            this.addConversationReference(context.activity);

            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (let cnt = 0; cnt < membersAdded.length; cnt++) {
                if (membersAdded[cnt].id !== context.activity.recipient.id) {
                    const welcomeMessage = 'Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.';
                    await context.sendActivity(welcomeMessage);
                }
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });

        this.onMessage(async (context, next) => {
            this.addConversationReference(context.activity);

            // Echo back what the user said
            await context.sendActivity(`You sent '${ context.activity.text }'`);
            await next();
        });
    }

    addConversationReference(activity) {
        const conversationReference = TurnContext.getConversationReference(activity);
        this.conversationReferences[conversationReference.conversation.id] = conversationReference;
    }
}

module.exports.ProactiveBot = ProactiveBot;

```
---

## <a name="related-topic-for-teams-administrators"></a>Rubrique connexe pour les administrateurs teams
>
> [!div class="nextstepaction"]
> [**Gérer les stratégies de configuration d’application dans Microsoft teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>Afficher des exemples de code supplémentaires
>
> [!div class="nextstepaction"]
> [**Exemples de code de messagerie proactive teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>