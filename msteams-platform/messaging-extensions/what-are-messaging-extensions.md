---
title: Extensions de messages
author: surbhigupta
description: Découvrez comment les extensions de message sont utilisées, leurs types et les scénarios où elles sont utilisées sur la plateforme Microsoft Teams. Exemples sur l’action et l’extension de message basée sur la recherche.
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6b486e732542cbd6fdfeaecbef74b9724a024e67
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819974"
---
# <a name="message-extensions"></a>Extensions de messages

Les extensions de messagerie permettent aux utilisateurs du client Microsoft Teams d’interagir avec votre service web par le biais de boutons et de formulaires. Elles peuvent effectuer des recherches, ou lancer des actions, dans un système externe à partir de la zone de rédaction de message, de la zone de commande ou d’un message. Vous pouvez renvoyer les résultats de cette interaction au client Teams sous la forme d’une carte richement mise en forme.

> [!IMPORTANT]
> Les extensions de message sont disponibles dans les environnements Cloud de la communauté du secteur public (GCC) et GCC-High, mais pas dans l’environnement department of Defense (DoD).

Ce document fournit une vue d’ensemble de l’extension de message, des tâches effectuées dans différents scénarios, du fonctionnement de l’extension de message, des commandes d’action et de recherche, et du déploiement de liens.

L’image suivante affiche les emplacements à partir desquels les extensions de message sont appelées :

:::image type="content" source="~/assets/images/messaging-extension-invoke-locations.png" alt-text="emplacement de l'extension du message":::

> [!NOTE]
> L'@mention des extensions de message n'est plus prise en charge dans la boîte de composition.

## <a name="scenarios-where-message-extensions-are-used"></a>Scénarios dans lesquels les extensions de message sont utilisées

| Scénario | Exemple |
|:-----------------|:-----------------|
|Vous souhaitez qu’un système externe effectue une action et que le résultat de l’action soit renvoyé à votre conversation.|Réservez une ressource et autorisez le canal à connaître l’intervalle de temps réservé.|
|Vous souhaitez trouver quelque chose dans un système externe et partager les résultats avec la conversation.|Recherchez un élément de travail dans Azure DevOps, et partagez-le avec le groupe sous forme de carte adaptative.|
|Vous souhaitez effectuer une tâche complexe impliquant plusieurs étapes ou un grand nombre d’informations dans un système externe, et partager les résultats avec une conversation.|Créez un bogue dans votre système de suivi en fonction d’un message Teams, attribuez ce bogue à Bob et envoyez une carte au thread de conversation avec les détails du bogue.|

## <a name="understand-how-message-extensions-work"></a>Comprendre le fonctionnement des extensions de message

Une extension de message se compose d’un service web que vous hébergez et d’un manifeste d’application, qui définit l’emplacement à partir duquel votre service web est appelé dans le client Teams. Le service web tire parti du schéma de messagerie et du protocole de communication sécurisé du Bot Framework. Vous devez donc enregistrer votre service web en tant que bot dans le Bot Framework.

> [!NOTE]
> Bien que vous puissiez créer le service web manuellement, utilisez le [Kit de développement logiciel (SDK) Bot Framework](https://github.com/microsoft/botframework-sdk) pour utiliser le protocole.

Dans le manifeste d’application pour l’application Teams, une seule extension de message est définie avec jusqu’à 10 commandes différentes. Chaque commande définit un type, tel que l’action ou la recherche et les emplacements dans le client à partir desquels il est appelé. Les emplacements d’appel sont la zone de message de composition, la barre de commandes et le message. Lors de l’appel, le service web reçoit un message HTTPS avec une charge utile JSON incluant toutes les informations pertinentes. Répondez avec une charge utile JSON, ce qui permet au client Teams de connaître l’interaction suivante à activer.

## <a name="types-of-message-extension-commands"></a>Types de commandes d’extension de message

Il existe deux types de commandes d’extension de message, la commande d’action et la commande de recherche. Le type de commande d’extension de message définit les éléments d’interface utilisateur et les flux d’interaction disponibles pour votre service web. Certaines interactions, telles que l’authentification et la configuration, sont disponibles pour les deux types de commandes.

### <a name="action-commands"></a>Commandes d'action

Les commandes d’action sont utilisées pour présenter aux utilisateurs une fenêtre contextuelle modale afin de collecter ou d’afficher des informations. Lorsque l'utilisateur soumet le formulaire, votre service web répond en insérant un message dans la conversation directement ou en insérant un message dans la zone de composition de messages. Après cela, l’utilisateur peut envoyer le message. Vous pouvez chaîner plusieurs formulaires ensemble pour des flux de travail plus complexes.

Les commandes d’action sont déclenchées à partir de la zone de composition de message, de la zone de commande ou d’un message. Lorsque la commande est invoquée à partir d'un message, la charge utile JSON initiale envoyée à votre robot comprend l'intégralité du message à partir duquel elle a été invoquée. L'image suivante affiche le module de tâches de la commande d’action de l'extension de message :

:::image type="content" source="~/assets/images/task-module.png" alt-text="Module de tâches de la commande d’action de l’extension de message":::

### <a name="search-commands"></a>Commandes de recherche

Les commandes de recherche permettent aux utilisateurs de rechercher des informations dans un système externe, soit manuellement par le biais d'une boîte de recherche, soit en collant un lien vers un domaine surveillé dans la zone de composition du message, et d'insérer les résultats de la recherche dans un message. Dans le flux de commandes de recherche le plus élémentaire, le message d'appel initial comprend la chaîne de recherche soumise par l'utilisateur. Vous répondez avec une liste de cartes et d’aperçus de cartes. Le client Teams affiche une liste d’aperçus de carte pour l’utilisateur. Lorsque l'utilisateur sélectionne une carte dans la liste, la carte en taille réelle est insérée dans la zone de composition du message.

Les cartes sont déclenchées à partir de la zone de composition des messages ou de la boîte de commande et non à partir d'un message. Ils ne peuvent pas être déclenchés à partir d’un message.
L'image suivante affiche le module de tâches de la commande de recherche d'extension de message :

:::image type="content" source="~/assets/images/search-extension.png" alt-text="Commande de recherche d’extension de message":::

> [!NOTE]
> Pour plus d’informations sur les cartes, voir [ce que sont les cartes](../task-modules-and-cards/what-are-cards.md).

## <a name="link-unfurling"></a>Déploiement de lien

Un service web est appelé lorsqu’une URL est collée dans la zone de composition du message. Cette fonctionnalité est appelée déploiement de liens. Avec de déploiement de lien, votre application peut s’inscrire pour recevoir une activité lorsque les URL avec un domaine particulier sont collées dans la zone rédaction d’un message. Votre service web peut « déployer » l’URL dans une carte détaillée, en fournissant plus d’informations que la carte d’aperçu du site web standard. Vous pouvez ajouter des boutons pour permettre aux utilisateurs d’agir immédiatement sans quitter le client Teams.
Les images suivantes affichent la fonctionnalité de déploiement de lien lorsqu’un lien est collé dans l’extension de message :

:::image type="content" source="../assets/images/messaging-extension/unfurl-link.png" alt-text="déployer le lien":::

![Déploiement de lien](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>Extraits de code

Le code suivant fournit un exemple d’action basée sur les extensions de message :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

 protected override Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
        {
            // Handle different actions using switch
            switch (action.CommandId)
            {
                case "HTML":
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Height = 200,
                                Width = 400,
                                Title = "Task Module HTML Page",
                                Url = baseUrl + "/htmlpage.html",
                            },
                        },
                    };
                // return TaskModuleHTMLPage(turnContext, action);
                default:
                    string memberName = "";
                    var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
                    memberName = member.Name;
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Card = <<AdaptiveAction card json>>,
                                Height = 200,
                                Width = 400,
                                Title = $"Welcome {memberName}",
                            },
                        },
                    };
            }
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

    async handleTeamsMessagingExtensionFetchTask(context, action) {
        switch (action.commandId) {
            case 'Static HTML':
                return staticHtmlPage();
        }
    }

    staticHtmlPage(){
        return {
            task: {
                type: 'continue',
                value: {
                    width: 450,
                    height: 125,
                    title: 'Task module Static HTML',
                    url: `${baseurl}/StaticPage.html`
                }
            }
        };
    }

```

---

Le code suivant fournit un exemple de recherche basée sur les extensions de message :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
        {
            var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

            var packages = new[] {
            new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
            new { title = "Fluent UI Library", value = "FluentUI" }};

            // We take every row of the results and wrap them in cards wrapped in MessagingExtensionAttachment objects.
            // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
            var attachments = packages.Select(package =>
            {
                var previewCard = new ThumbnailCard { Title = package.title, Tap = new CardAction { Type = "invoke", Value = package } };
                if (!string.IsNullOrEmpty(package.title))
                {
                    previewCard.Images = new List<CardImage>() { new CardImage(package.title, "Icon") };
                }

                var attachment = new MessagingExtensionAttachment
                {
                    ContentType = HeroCard.ContentType,
                    Content = new HeroCard { Title = package.title },
                    Preview = previewCard.ToAttachment()
                };

                return attachment;
            }).ToList();

            // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
            return new MessagingExtensionResponse
            {
                ComposeExtension = new MessagingExtensionResult
                {
                    Type = "result",
                    AttachmentLayout = "list",
                    Attachments = attachments
                }
            };
        }
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;     
        const attachments = [];
                const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);
                
                response.data.objects.forEach(obj => {
                        const heroCard = CardFactory.heroCard(obj.package.name);
                        const preview = CardFactory.heroCard(obj.package.name);
                        preview.content.tap = { type: 'invoke', value: { description: obj.package.description } };
                        const attachment = { ...heroCard, preview };
                        attachments.push(attachment);
                });
    
                return {
                    composeExtension:  {
                           type: 'result',
                           attachmentLayout: 'list',
                           attachments: attachments
                    }
                };
            }       
        }
```

---

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|------------|-------------|----------------|------------|------------|
| Extension de message avec des commandes basées sur des actions | Cet exemple montre comment créer une extension de message basée sur des actions. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extension de message avec des commandes basées sur la recherche | Cet exemple montre comment créer une extension de message basée sur la recherche. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|Action d’extension de message pour la planification des tâches|Cet exemple montre comment planifier une tâche à partir de la commande d’action d’extension de message et obtenir une carte de rappel à une date et une heure planifiées.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)| N/A |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Définir la commande d’extension de message d’action](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>Voir aussi

* [Fonctionnalités d’application mappées aux fonctionnalités](../concepts/design/map-use-cases.md#app-capabilities-mapped-to-features)
* [Créer votre première application d’extension de message à l’aide de JavaScript](../sbs-gs-msgext.yml)
* [Conception de votre extension de message Microsoft Teams](design/messaging-extension-design.md)
* [Définir des commandes d’action d’extension de message](how-to/action-commands/define-action-command.md)
* [Définir des commandes de recherche d’extension de message](how-to/search-commands/define-search-command.md)
* [Ajouter un déploiement de lien](how-to/link-unfurling.md)
* [Schéma du manifeste d’application pour Teams](../resources/schema/manifest-schema.md)
* [Documentation pour les développeurs](../concepts/build-and-test/teams-developer-portal.md)
