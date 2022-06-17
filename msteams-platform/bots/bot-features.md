---
title: Bots et kits de développement
author: surbhigupta
description: Dans cet article, découvrez les outils et les kits de développement logiciel (SDK) pour créer Microsoft Teams bots et bots avec le Microsoft Bot Framework.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 0b344b6a2db0abc4d1769c47aca6f496f69b98d7
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142464"
---
# <a name="bots-and-sdks"></a>Bots et kits de développement

Vous pouvez créer un bot qui fonctionne dans Microsoft Teams avec l’un des outils ou fonctionnalités suivants :

* [Kit de développement logiciel (SDK) Microsoft Bot Framework](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [Virtual Assistant](~/samples/virtual-assistant.md)
* [Webhooks et connecteurs](#bots-with-webhooks-and-connectors)
* [Service de bot Azure](#azure-bot-service)

## <a name="bots-with-the-microsoft-bot-framework"></a>Bots avec le Microsoft Bot Framework

Votre bot Teams se compose des éléments suivants :

* Service web accessible publiquement hébergé par vous.
* Une inscription Bot Framework pour votre service web.
* Votre package d’application Teams, qui connecte le client Teams à votre service web.

> [!TIP]
> Utilisez le Developer Portal pour inscrire votre service web auprès du Bot Framework et spécifier les configurations de votre application. Pour plus d’informations, consultez [gérer vos applications avec le portail des développeurs pour Teams](~/concepts/build-and-test/teams-developer-portal.md).

Le [Bot Framework](https://dev.botframework.com/) est un kit de développement logiciel (SDK) riche utilisé pour créer des bots à l’aide de C#, Java, Python et JavaScript. Si vous disposez déjà d’un bot basé sur le Bot Framework, vous pouvez facilement le modifier pour qu’il fonctionne dans Teams. Utilisez C# ou Node.js pour tirer parti de nos [Kits de développement logiciel](/microsoftteams/platform/#pivot=sdk-tools). Ces packages étendent les classes et méthodes de kit de développement logiciel (SDK) de base de Bot Builder :

* Utilisez des types de cartes spécialisés comme la carte de connecteur Office 365.
* Définissez des données de canal spécifiques à Teams sur les activités.
* Traiter les demandes d’extension de message.

> [!IMPORTANT]
> Vous pouvez développer des applications Teams dans n’importe quelle technologie de programmation web et appeler directement les [API REST Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) . Toutefois, vous devez gérer les jetons dans tous les cas.

## <a name="bots-with-power-virtual-agents"></a>Bots avec Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) est un service chatbot basé sur la plateforme Microsoft Power et Bot Framework. Le processus de développement de Power Virtual Agent utilise une approche guidée, sans code et d’interface graphique qui permet aux membres de votre équipe de créer et de gérer facilement un agent virtuel intelligent. Après avoir créé votre chatbot dans le portail [Power Virtual Agents](https://powervirtualagents.microsoft.com), vous pouvez facilement [l’intégrer à Teams](how-to/add-power-virtual-agents-bot-to-teams.md). Pour plus d’informations sur la prise en main, consultez [Documentation Power Virtual Agents](/power-virtual-agents).

>[!NOTE]
>Vous ne devez pas utiliser Microsoft Power Platform pour créer des applications qui doivent être publiées dans l’App Store Teams. Microsoft Power Platform applications peuvent être publiées uniquement dans l’App Store d’une organisation.

## <a name="bots-with-webhooks-and-connectors"></a>Bots avec webhooks et connecteurs

Les webhooks et les connecteurs connectent votre bot à vos services web. À l’aide de webhooks et de connecteurs, vous pouvez créer un bot pour une interaction de base, comme la création d’un workflow ou d’autres commandes simples. Elles sont disponibles uniquement dans l’équipe où vous les créez et sont destinées à des processus simples spécifiques au flux de travail de votre entreprise. Pour plus d’informations, consultez [ce que sont les webhooks et les connecteurs](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="azure-bot-service"></a>Service de bot Azure

Le service de bot Azure, ainsi que Bot Framework, fournit des outils pour créer, tester, déployer et gérer des bots intelligents, le tout au même endroit. Vous pouvez également créer votre bot dans azure bot service.

> [!IMPORTANT]
> Les applications Bot dans Microsoft Teams sont disponibles dans GCC-High par le biais d’[Azure Bot Service](/azure/bot-service/channel-connect-teams).

> [!NOTE]
> * Les bots dans GCCH prennent uniquement en charge jusqu’à la version manifeste v1.10.
> * Les URL d’image dans les cartes adaptatives ne sont pas prises en charge dans l’environnement GCCH. Vous pouvez remplacer une URL d’image par un DataUri encodé en Base64.
> * L’inscription de canal de bot dans Azure Government approvisionnera le bot d’application web, app service (plan App Service) et Application Insights, mais il ne prend pas en charge l’approvisionnement d’Azure Bot Service uniquement (aucun service d’application).
>   <details>
>   <summary><b>Si vous souhaitez effectuer l’inscription du bot uniquement</b></summary>
>
>   * Accédez au groupe de ressources et supprimez manuellement les ressources inutilisées. Par exemple, le service d’application, le plan App Service (si vous avez créé lors de l’inscription du bot) et les insights d’application (si vous choisissez de l’activer lors de l’inscription du bot).
>   * Vous pouvez également utiliser az-cli pour effectuer l’inscription du bot :
>
>     1. Connectez-vous à Azure et définissez l’abonnement <br> 
>           &nbsp; az cloud set –name « AzureUSGovernment » <br> 
>           &nbsp; az account set –name « `subscriptionname/id` ».<br>
>     1. Créer l’inscription d’application  
>           &nbsp; az ad app create --display-name « `name` » <br> 
>           &nbsp; --password « `password` » --available-to-other-tenants.<br> 
>           Votre ID d’application est créé ici.<br>
>     1. Créer une ressource de bot <br>
>           &nbsp; az bot create –resource-group « `resource-group` »<br>
>           &nbsp; --appid « `appid` »<br>
>           &nbsp; --name « `botid` »<br>
>           &nbsp; --kind « registration ».<br>
>
> </details>

Pour l’environnement GCCH, vous devez inscrire un bot à l’aide [du portail Azure Government](https://portal.azure.us).

:::image type="content" source="../assets/videos/abs-bot.gif" alt-text="portail Azure Government":::
<br>
<br>
Les modifications suivantes sont nécessaires dans le bot pour GCC-High environnement :
<br>
<br>
<details>
<summary><b>Modifications de configuration</b></summary>

À mesure que l’inscription du bot se produit dans Azure Government portail, veillez à mettre à jour les configurations du bot pour se connecter aux instances de govermnet Azure. Voici les détails de configuration :

| Nom de la configuration | Valeur |
|----|----|
| ChannelService | `https://botframework.azure.us` |
| OAuthUrl | `https://tokengcch.botframework.azure.us` |
| ToChannelFromBotLoginUrl | `https://login.microsoftonline.us/MicrosoftServices.onmicrosoft.us` |
| ToChannelFromBotOAuthScope | `https://api.botframework.us` |
| ToBotFromChannelTokenIssuer | `https://api.botframework.us`  |
| BotOpenIdMetadata | `https://login.botframework.azure.us/v1/.well-known/openidconfiguration` |

</details>
<br>
<details>
<summary><b>Mise à jour vers appsettings.json & startup.cs</b></summary>

1. **Mettre à jour appsettings.json :**

    * Définissez `ConnectionName` le nom du paramètre de connexion OAuth que vous avez ajouté à votre bot.

    * Définissez et `MicrosoftAppPassword` définissez `MicrosoftAppId` l’ID d’application et le secret d’application de votre bot.
    
    Selon les caractères de votre secret de bot, vous devrez peut-être placer le mot de passe dans un échappement XML. Par exemple, tous les ampersands (&) doivent être encodés en tant que `&amp;`.

    ```json
    {
      "MicrosoftAppType": "",
      "MicrosoftAppId": "",
      "MicrosoftAppPassword": "",
      "MicrosoftAppTenantId": "",
      "ConnectionName": ""
    }
    ```
2. **Mettre à jour Startup.cs :**

    Pour utiliser OAuth dans des *clouds Azure non publics*, comme le cloud public, ou dans des bots avec résidence des données, vous devez ajouter le code suivant dans le fichier **Startup.cs** .
    
    ```csharp
    string uri = "<uri-to-use>";
    MicrosoftAppCredentials.TrustServiceUrl(uri);
    OAuthClientConfig.OAuthEndpoint = uri;
    ```
    
    Où \<uri-to-use\> se trouve l’un des URI suivants :

    |**URI**|**Description**|
    |---|---|
    |`https://europe.api.botframework.com`|Pour les bots de cloud public avec résidence des données en Europe.|
    |`https://unitedstates.api.botframework.com`|Pour les bots de cloud public avec résidence des données dans le États-Unis.|
    |`https://apiGCCH.botframework.azure.us`|Pour États-Unis bots cloud gouvernementaux sans résidence des données.|
    |`https://api.botframework.com`|Pour les bots de cloud public sans résidence des données. Il s’agit de l’URI par défaut et ne nécessite pas de modification de **Startup.cs**.|

3. L’URL de redirection pour l’inscription d’application à partir d’Azure doit être mise à jour vers `https://tokengcch.botframework.azure.us/.auth/web/redirect`.

</details>

## <a name="advantages-of-bots"></a>Avantages de la CCR

Les bots dans Microsoft Teams peuvent être intégrés dans une conversation à deux, une conversation de groupe ou un canal dans une équipe. Chaque étendue fournit des opportunités et des défis uniques pour votre bot conversationnel.

| Dans un canal | Dans une conversation de groupe | Dans une conversation privée |
| :-- | :-- | :-- |
| Portée massive | Moins de membres | Mode traditionnel |
| Interactions individuelles concises | @mention au bot  | Questions et réponses Un bot |
| @mention au bot | Similaire au canal | Bots qui décrivent les rires et prennent des notes |

### <a name="in-a-channel"></a>Dans un canal

Les canaux contiennent des conversations thématiques entre plusieurs personnes, même jusqu’à deux milliers. Cela donne potentiellement une portée massive à votre bot, mais les interactions individuelles doivent être concises. Les interactions multitours traditionnelles ne fonctionnent pas. Au lieu de cela, vous devez chercher à utiliser des cartes interactives ou des modules de tâches, ou déplacer la conversation vers une conversation un-à-un pour collecter un grand nombre d’informations. Votre bot a uniquement accès aux messages où il se trouve `@mentioned`. Vous pouvez récupérer des messages supplémentaires à partir de la conversation à l’aide d’autorisations Microsoft Graph et au niveau de l’organisation.

Les bots fonctionnent mieux dans un canal dans les cas suivants :

* Notifications, où vous fournissez une carte interactive permettant aux utilisateurs de prendre des informations supplémentaires.
* Scénarios de commentaires, tels que les sondages et les enquêtes.
* Un cycle de requête ou de réponse unique résout les interactions et les résultats sont utiles pour plusieurs membres de la conversation.
* Les bots sociaux ou amusants, où vous obtenez une image de chat exceptionnelle, choisissez aléatoirement un gagnant, etc.

### <a name="in-a-group-chat"></a>Dans une conversation de groupe

Les conversations de groupe sont des conversations non thématiques entre trois personnes au minimum. Elles impliquent généralement moins de membres qu’un canal et sont plus éphémères. À l’instar d’un canal, votre bot n’a accès qu’aux messages où il est `@mentioned` directement.

Dans les cas où les bots fonctionnent mieux dans un canal, ils fonctionnent également mieux dans une conversation de groupe.

### <a name="in-a-one-to-one-chat"></a>Dans une conversation privée

Les bots de conversation interagissent traditionnellement de cette façon avec les utilisateurs. Voici quelques exemples de bots conversationnels un-à-un :

* Questions et réponses Un bot
* bots qui lancent des workflows dans d’autres systèmes
* bots qui décrivent des rires
* bots qui prennent des notes Avant de créer des chatbots un-à-un, déterminez si une interface basée sur une conversation est la meilleure façon de présenter vos fonctionnalités.

## <a name="disadvantages-of-bots"></a>Inconvénients des bots

Une boîte de dialogue étendue entre votre bot et l’utilisateur est un moyen lent et complexe d’accomplir une tâche. Un bot qui prend en charge des commandes excessives, en particulier un large éventail de commandes, ne réussit pas ou n’est pas considéré positivement par les utilisateurs.

### <a name="have-multi-turn-experiences-in-chat"></a>Avoir des expériences multitours dans la conversation

Une boîte de dialogue étendue nécessite que le développeur conserve l’état. Pour quitter cet état, un utilisateur doit délai d’expiration ou sélectionner **Annuler**. En outre, le processus est fastidieux. Par exemple, consultez le scénario de conversation suivant :

UTILISATEUR : planifier une réunion avec Megan.

BOT : j’ai trouvé 200 résultats. Veuillez inclure un prénom et un nom.

UTILISATEUR : Planifiez une réunion avec Megan Bowen.

BOT : OK, à quelle heure voulez-vous rencontrer Megan Bowen ?

UTILISATEUR : 13:00.

BOT : quel jour ?

### <a name="support-too-many-commands"></a>Prendre en charge un trop grand nombre de commandes

Étant donné qu’il n’y a que six commandes visibles dans le menu du bot actuel, il est peu probable que d’autres commandes soient utilisées avec n’importe quelle fréquence. Les bots qui s’inscrivent dans un domaine spécifique plutôt que d’essayer d’être un grand assistant fonctionnent mieux.

### <a name="maintain-a-large-knowledge-base"></a>Gérer une grande base de connaissances

L’un des inconvénients des bots est qu’il est difficile de maintenir une grande base de connaissances de récupération avec des réponses non classées. Les bots sont particulièrement adaptés aux interactions courtes et rapides, sans passer en revue les longues listes à la recherche d’une réponse.

## <a name="code-snippets"></a>Extraits de code

Le code suivant fournit un exemple d’activité de bot pour une étendue d’équipe de canal :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});

```

---

Le code suivant fournit un exemple d’activité de bot pour une conversation un-à-un :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle message activity
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    turnContext.Activity.RemoveRecipientMention();
    var text = turnContext.Activity.Text.Trim().ToLower();
  await turnContext.SendActivityAsync(MessageFactory.Text($"Your message is {text}."), cancellationToken);
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
this.onMessage(async (context, next) => {
    await context.sendActivity(MessageFactory.text("Your message is:" + context.activity.text));
    await next();
});
```

---

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore | Node.js | Python|
|----------------|-----------------|--------------|----------------|-------|
| Bot de conversation Teams | Gestion des événements de messagerie et de conversation. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
| Échantillons de bottes | Ensemble d’exemples de bots | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Gestionnaire d'activité du robot](~/bots/bot-basics.md)

## <a name="see-also"></a>Voir aussi

* [Bots d’appels et réunions](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [Conversations de robots](~/bots/how-to/conversations/conversation-basics.md)
* [Menus de commandes Bot](~/bots/how-to/create-a-bot-commands-menu.md)
* [Flux d’authentification pour les bots dans Microsoft Teams](~/bots/how-to/authentication/auth-flow-bot.md)
* [Utiliser des modules de tâches à partir de bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)
