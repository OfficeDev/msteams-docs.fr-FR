---
title: Créer un assistant virtuel
description: Comment créer des bots Virtual Assistant et des compétences à utiliser dans Microsoft Teams
ms.localizationpriority: medium
ms.topic: how-to
keywords: bots d’assistant virtuel Teams
ms.openlocfilehash: 1231520278f97fc48ad53937af80c127021bd9c2
ms.sourcegitcommit: 25a88715d9b06b2afeac14de86177bb34161b0cf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2021
ms.locfileid: "60266633"
---
# <a name="create-virtual-assistant"></a>Créer un assistant virtuel 

Virtual Assistant est un modèle open source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant un contrôle total de l’expérience utilisateur, de la marque organisationnelle et des données nécessaires. Le [Virtual Assistant](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) principal est le bloc de construction de base qui regroupe les technologies Microsoft requises pour créer un Virtual Assistant, y compris le [SDK Bot Framework,](https://github.com/microsoft/botframework-sdk)language [understanding (LUIS)](https://www.luis.ai/)et [QnA Maker](https://www.qnamaker.ai/). Il regroupe également les fonctionnalités essentielles, notamment l’inscription des compétences, les comptes liés, l’intention de conversation de base de proposer aux utilisateurs un large éventail d’interactions et d’expériences transparentes. En outre, les fonctionnalités de modèle incluent de riches exemples de compétences de conversation [réutilisables.](https://microsoft.github.io/botframework-solutions/overview/skills)  Les compétences individuelles sont intégrées dans une solution Virtual Assistant pour permettre plusieurs scénarios. À l’aide du SDK Bot Framework, les compétences sont présentées sous forme de code source, ce qui vous permet de personnaliser et d’étendre selon vos besoins. Pour plus d’informations sur les compétences de Bot Framework, voir [Qu’est-ce qu’une compétence Bot Framework](https://microsoft.github.io/botframework-solutions/overview/skills/). Ce document vous guide sur les Virtual Assistant d’implémentation pour les organisations, la création d’une Virtual Assistant axée sur Teams, l’exemple associé, l’exemple de code et les limitations des Virtual Assistant.
L’image suivante affiche la vue d’ensemble de l’Assistant virtuel :

![Virtual Assistant de vue d’ensemble](../assets/images/bots/virtual-assistant/overview.png)

Les activités de message texte sont acheminées vers les compétences associées par le Virtual Assistant à l’aide [d’un modèle de](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) distribution. 

## <a name="implementation-considerations"></a>Considérations sur l’implémentation

La décision d’ajouter un Virtual Assistant de nombreux déterminants et diffère pour chaque organisation. Les facteurs de prise en charge d’une implémentation Virtual Assistant pour votre organisation sont les suivants :

* Une équipe centrale gère toutes les expériences des employés. Il a la possibilité de créer une expérience Virtual Assistant et de gérer les mises à jour de l’expérience de base, y compris l’ajout de nouvelles compétences.
* Plusieurs applications existent dans les fonctions métiers et le nombre devrait augmenter à l’avenir.
* Les applications existantes sont personnalisables, elles sont la propriété de l’organisation et sont converties en compétences pour un Virtual Assistant.
* L’équipe centrale des expériences des employés est en mesure d’influencer les personnalisations des applications existantes. Il fournit également des instructions nécessaires pour intégrer des applications existantes en tant que compétences dans Virtual Assistant expérience utilisateur.

L’image suivante affiche les fonctions métiers des Virtual Assistant : 

![L’équipe centrale maintient l’assistant, et les équipes de fonction professionnelle contribuent aux compétences](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Créer un Teams centré sur Virtual Assistant

Microsoft a publié un modèle [Visual Studio pour](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) créer des assistants virtuels et des compétences. Avec le Visual Studio, vous pouvez créer une Virtual Assistant, optimisée par une expérience textuelle avec prise en charge de cartes enrichies limitées avec des actions. Nous avons amélioré le modèle de base Visual Studio pour inclure Microsoft Teams fonctionnalités de plateforme et de Teams expériences d’application. Quelques-unes des fonctionnalités incluent la prise en charge des cartes adaptatives enrichies, des modules de tâche, des conversations d’équipe ou de groupe et des extensions de messagerie. Pour plus d’informations sur l’extension Virtual Assistant la Microsoft Teams, voir didacticiel : Étendre [votre Virtual Assistant à Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).    
L’image suivante affiche le diagramme de haut niveau d’une solution Virtual Assistant suivante :

![Diagramme de haut niveau d’une solution Virtual Assistant de données](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Ajouter des cartes adaptatives à votre Virtual Assistant

Pour envoyer correctement les demandes, Virtual Assistant devez identifier le modèle LUIS approprié et les compétences correspondantes qui lui sont associées. Toutefois, le mécanisme de distribution ne peut pas être utilisé pour les activités d’action de carte, car le modèle LUIS associé à une compétence est formé aux textes d’action de carte. Les textes d’action de carte sont des mots clés fixes, prédéfin définis et ne sont pas commentés par un utilisateur.

Cet inconvénient est résolu par l’incorporation d’informations de compétences dans la charge utile de l’action de carte. Chaque compétence doit être incorporer `skillId` dans le champ des actions de  `value` carte. Vous devez vous assurer que chaque activité d’action de carte porte les informations pertinentes sur les compétences et Virtual Assistant pouvez utiliser ces informations pour la distribution.

Vous devez fournir dans le constructeur pour vous assurer que les informations de compétences sont `skillId` toujours présentes dans les actions de carte.
Un exemple de code de données d’action de carte est illustré dans la section suivante :
```csharp
    public class CardActionData
    {
        public CardActionData(string skillId)
        {
            this.SkillId = skillId;
        }

        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }

    ...
    var button = new CardAction
    {
        Type = ActionTypes.MessageBack,
        Title = "Card action button",
        Text = "card action button text",
        Value = new CardActionData(<SkillId>),
    };
```

Ensuite, `SkillCardActionData` la classe dans le modèle Virtual Assistant est introduit pour extraire de la charge utile `skillId` d’action de carte.
Un extrait de code à extraire de la charge utile d’action de carte est  `skillId` illustré dans la section suivante :

```csharp
    // Skill Card action data should contain skillId parameter
    // This class is used to deserialize it and get skillId 
    public class SkillCardActionData
    {
        /// <summary>
        /// Gets the ID of the skil that should handle this card
        /// </summary>
        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }
```

L’implémentation est effectuée par une méthode d’extension dans la [classe Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)
Un extrait de code à extraire des données d’action de carte est  `skillId` illustré dans la section suivante :

```csharp
    public static class ActivityExtensions
    {
        // Fetches skillId from CardAction data if present
        public static string GetSkillId(this Activity activity)
        {
            string skillId = string.Empty;

            try
            {
                if (activity.Type.Equals(ActivityTypes.Message) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(activity.Value.ToString());
                    skillId = data.SkillId;
                }
                else if (activity.Type.Equals(ActivityTypes.Invoke) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(JObject.Parse(activity.Value.ToString()).SelectToken("data").ToString());
                    skillId = data.SkillId;
                }
            }
            catch
            {
                // If not able to retrive skillId, empty skillId should be returned
            }

            return skillId;
        }
    }
```

### <a name="handle-interruptions"></a>Gérer les interruptions

Virtual Assistant gérer les interruptions lorsqu’un utilisateur tente d’invoquer une compétence alors qu’une autre compétence est active. `TeamsSkillDialog`, `TeamsSwitchSkillDialog` et sont introduits en fonction de [l’infrastructure de Bot SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) et [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs). Ils permettent aux utilisateurs de basculer une expérience de compétence à partir d’actions de carte. Pour gérer cette demande, le Virtual Assistant demande à l’utilisateur d’envoyer un message de confirmation pour changer de compétences :

![Invite de confirmation lors du passage à une nouvelle compétence](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Gérer les demandes de module de tâche

Pour ajouter des fonctionnalités de module de tâche à un Virtual Assistant, deux méthodes supplémentaires sont incluses dans le Virtual Assistant d’activité : `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync` . Ces méthodes écoutent les activités liées au module de tâche de Virtual Assistant, identifient les compétences associées à la demande et la placent à la compétence identifiée. 

Le forwarding de demande est effectué par le biais de [la méthode SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` . Elle renvoie la réponse telle `InvokeResponse` qu’elle est l’une des deux. `TaskModuleResponse`


```csharp
    public static TaskModuleResponse GetTaskModuleRespose(this InvokeResponse invokeResponse)
    {
        if (invokeResponse.Body != null)
        {
            return new TaskModuleResponse()
            {
                Task = GetTask(invokeResponse.Body),
            };
        }

        return null;
    }

    private static TaskModuleResponseBase GetTask(object invokeResponseBody)
        {
            JObject resposeBody = (JObject)JToken.FromObject(invokeResponseBody);
            var task = resposeBody.GetValue("task");
            var taskType = task.SelectToken("type").ToString();

            return taskType switch
            {
                "continue" => new TaskModuleContinueResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToObject<TaskModuleTaskInfo>(),
                },
                "message" => new TaskModuleMessageResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToString(),
                },
                _ => null,
            };
        }
```

Une approche similaire est suivie pour la distribution des actions de carte et les réponses de module de tâche. Les données d’action d’extraction et d’soumission du module de tâche sont mises à jour pour inclure `skillId` . La méthode d’extension d’activité extrait de la charge utile qui fournit des détails sur les compétences qui `GetSkillId` `skillId` doivent être invoquées.

L’extrait de code et les méthodes sont `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` donnés dans la section suivante :

```csharp
    // Invoked when a "task/fetch" event is received to invoke task module.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken);

            return invokeResponse.GetTaskModuleResponse();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }

    // Invoked when a 'task/submit' invoke activity is received for task module submit actions.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

            return invokeResponse.GetTaskModuleRespose();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }
```

En outre, vous devez inclure tous les domaines de compétence dans la section du fichier manifeste de Virtual Assistant afin que les modules de tâche soient appelés par le biais d’un rendu de `validDomains` compétence correctement.

### <a name="handle-collaborative-app-scopes"></a>Gérer les étendues d’application collaborative

Teams applications peuvent exister dans plusieurs étendues, y compris la conversation 1:1, la conversation de groupe et les canaux. Le modèle Virtual Assistant est conçu pour les conversations 1:1. Dans le cadre de l’expérience d’Virtual Assistant invite les utilisateurs à nommer et maintient l’état de l’utilisateur. Étant donné que cette expérience d’intégration n’est pas adaptée aux étendues de conversation de groupe ou de canal, elle a été supprimée.

Les compétences doivent gérer les activités dans plusieurs étendues, telles que la conversation 1:1, la conversation de groupe et la conversation de canal. Si l’une de ces étendues n’est pas prise en charge, les compétences doivent répondre par un message approprié.

Les fonctions de traitement suivantes ont été ajoutées au Virtual Assistant principal :

* Virtual Assistant peut être appelé sans message texte provenant d’une conversation de groupe ou d’un canal.
* Les entrées sont nettoyées avant d’envoyer le message au module de distribution. Par exemple, supprimez les @mention du bot.

```csharp
    if (innerDc.Context.Activity.Conversation?.IsGroup == true)
    {
        // Remove bot atmentions for teams/groupchat scope
        innerDc.Context.Activity.RemoveRecipientMention();

        // If bot is invoked without any text, reply with FirstPromptMessage
        if (string.IsNullOrWhiteSpace(innerDc.Context.Activity.Text))
        {
            await innerDc.Context.SendActivityAsync(_templateEngine.GenerateActivityForLocale("FirstPromptMessage"));
            return EndOfTurn;
        }
    }
```

### <a name="handle-messaging-extensions"></a>Gérer les extensions de messagerie

Les commandes d’une extension de messagerie sont déclarées dans le fichier manifeste de votre application. L’interface utilisateur de l’extension de messagerie est optimisée par ces commandes. Pour qu Virtual Assistant commande d’extension de messagerie soit une compétence jointe, le manifeste d’un Virtual Assistant doit contenir ces commandes. Vous devez ajouter les commandes du manifeste d’une compétence individuelle au Virtual Assistant manifeste de l’équipe. L’ID de commande fournit des informations sur une compétence associée en axant l’ID d’application de la compétence par le biais d’un `:` séparateur.

L’extrait de code du fichier manifeste d’une compétence est illustré dans la section suivante :

```json
 "composeExtensions": [
    {
        "botId": "<Skil_App_Id>",
        "commands": [
            {
                "id": "searchQuery",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

L’extrait Virtual Assistant code de fichier manifeste correspondant est illustré dans la section suivante :

```json
 "composeExtensions": [
    {
        "botId": "<VA_App_Id>",
        "commands": [
            {
                "id": "searchQuery:<skill_id>",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

Une fois que les commandes sont invoquées par un utilisateur, le Virtual Assistant peut identifier une compétence associée en parant l’ID de commande, mettre à jour l’activité en supprimant le suffixe supplémentaire de l’ID de commande et le faire suivre à la compétence `:<skill_id>` correspondante. Le code d’une compétence n’a pas besoin de gérer le suffixe supplémentaire. Ainsi, les conflits entre les ID de commande entre les compétences sont évités. Avec cette approche, toutes les commandes de recherche et d’action d’une compétence dans tous les contextes, tels que **composer,** **commandBox** et **message** sont optimisées par un Virtual Assistant.

```csharp
    const string MessagingExtensionCommandIdSeparator = ":";

    // Invoked when a 'composeExtension/submitAction' invoke activity is received for a messaging extension action command
    protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        return await ForwardMessagingExtensionActionCommandActivityToSkill(turnContext, action, cancellationToken);
    }

    // Forwards invoke activity to right skill for messaging extension action commands.
    private async Task<MessagingExtensionActionResponse> ForwardMessagingExtensionActionCommandActivityToSkill(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        var skillId = ExtractSkillIdFromMessagingExtensionActionCommand(turnContext, action);
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionActionResponse();
    }

    // Extracts skill Id from messaging extension command and updates activity value
    private string ExtractSkillIdFromMessagingExtensionActionCommand(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action)
    {
        var commandArray = action.CommandId.Split(MessagingExtensionCommandIdSeparator);
        var skillId = commandArray.Last();

        // Update activity value by removing skill id before forwarding to the skill.
        var activityValue = JsonConvert.DeserializeObject<MessagingExtensionAction>(turnContext.Activity.Value.ToString());
        activityValue.CommandId = string.Join(MessagingExtensionCommandIdSeparator, commandArray, 0 commandArray.Length - 1);
        turnContext.Activity.Value = activityValue;

        return skillId;
    }
```

Certaines activités d’extension de messagerie n’incluent pas l’ID de commande. Par exemple, `composeExtension/selectItem` contient uniquement la valeur de l’action d’appel d’appel. Pour identifier les compétences associées, est attaché à chaque carte `skillId`  d’élément lors de la formation d’une réponse pour `OnTeamsMessagingExtensionQueryAsync` . Cela est similaire à l’approche d’ajout [de cartes adaptatives à votre Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).

```csharp
    // Invoked when a 'composeExtension/selectItem' invoke activity is received for compose extension query command.
    protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
    {
        var data = JsonConvert.DeserializeObject<SkillCardActionData>(query.ToString());
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == data.SkillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionResponse();
    }
```

---

## <a name="example"></a>Exemple

L’exemple suivant montre comment convertir le modèle d’application Livrer une salle en une compétence Virtual Assistant : « Réserver une salle » est un Microsoft Teams qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pendant 30, 60 ou 90 minutes à partir de l’heure actuelle. La durée par défaut est 30 minutes. Le bot Book-a-room s’étendue à des conversations personnelles ou 1:1. L’image suivante affiche une Virtual Assistant avec un **livre avec une compétence de** salle :

![Virtual Assistant compétence « réserver une salle »](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Voici les modifications delta introduites pour la convertir en une compétence attachée à une Virtual Assistant. Des instructions similaires sont suivies pour convertir tout bot v4 existant en une compétence.

### <a name="skill-manifest"></a>Manifeste de compétences

Un manifeste de compétences est un fichier JSON qui expose le point de terminaison de messagerie, l’ID, le nom et d’autres métadonnées pertinentes d’une compétence. Ce manifeste est différent du manifeste utilisé pour le chargement d’une application dans Microsoft Teams. Une Virtual Assistant nécessite un chemin d’accès à ce fichier comme entrée pour joindre une compétence. Nous avons ajouté le manifeste suivant au dossier wwwroot du bot.

```bash
botskills connect --remoteManifest "<url to skill's manifest>" ..
```

```json
{
  "$schema": "https://schemas.botframework.com/schemas/skills/skill-manifest-2.1.preview-0.json",
  "$id": "microsoft_teams_apps_bookaroom",
  "name": "microsoft-teams-apps-bookaroom",
  "description": "microsoft-teams-apps-bookaroom description",
  "publisherName": "Your Company",
  "version": "1.1",
  "iconUrl": "<icon url>",
  "copyright": "Copyright (c) Microsoft Corporation. All rights reserved.",
  "license": "",
  "privacyUrl": "<privacy url>",
  "endpoints": [
    {
      "name": "production",
      "protocol": "BotFrameworkV3",
      "description": "Production endpoint for the skill",
      "endpointUrl": "<endpoint url>",
      "msAppId": "skill app id"
    }
  ],
  "dispatchModels": {
    "languages": {
      "en-us": [
        {
          "id": "microsoft-teams-apps-bookaroom-en",
          "name": "microsoft-teams-apps-bookaroom LU (English)",
          "contentType": "application/lu",
          "url": "file://book-a-meeting.lu",
          "description": "English language model for the skill"
        }
      ]
    }
  },
  "activities": {
    "message": {
      "type": "message",
      "description": "Receives the users utterance and attempts to resolve it using the skill's LU models"
    }
  }
}
```

### <a name="luis-integration"></a>Intégration LUIS

Virtual Assistant de distribution est construit sur les modèles LUIS des compétences jointes. Le modèle de distribution identifie l’intention de chaque activité de texte et détecte les compétences qui lui sont associées.

Virtual Assistant nécessite le modèle LUIS de compétences au format comme entrée tout en `.lu` attachant une compétence. Le json LUIS est converti en format à l’aide de `.lu` l’outil botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Le bot book-a-room dispose de deux commandes principales pour les utilisateurs :

- `Book room`
- `Manage Favorites`

Nous avons créé un modèle LUIS en comprenant ces deux commandes. Les secrets correspondants doivent être remplies dans `cognitivemodels.json` . Le fichier LUIS JSON correspondant se trouve [ici.](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json)
Le fichier `.lu` correspondant est indiqué dans la section suivante :

```
> ! Automatically generated by [LUDown CLI](https://github.com/Microsoft/botbuilder-tools/tree/master/Ludown), Tue Mar 31 2020 17:30:32 GMT+0530 (India Standard Time)

> ! Source LUIS JSON file: book-a-meeting.json

> ! Source QnA TSV file: Not Specified

> ! Source QnA Alterations file: Not Specified


> # Intent definitions

## BOOK ROOM
- book a room
- book room
- please book a room
- reserve a room
- i want to book a room
- i want to book a room please
- get me a room please
- get me a room


## MANAGE FAVORITES
- manage favorites
- manage favorite
- please manage my favorite rooms
- manage my favorite rooms please
- manage my favorite rooms
- i want to manage my favorite rooms

## None


> # Entity definitions


> # PREBUILT Entity definitions


> # Phrase list definitions


> # List entities

> # RegEx entities
```

Avec cette approche, toute commande émise par un utilisateur pour Virtual Assistant associée ou identifiée comme une commande associée au bot est transmis à `book room` `manage favorites` cette `Book-a-room` compétence.
En revanche, le bot doit utiliser le modèle LUIS pour comprendre ces commandes si elles ne sont `Book-a-room room` pas tapés complètes. Par exemple : `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Prise en charge multi-langue

Par exemple, un modèle LUIS avec uniquement une culture anglaise est créé. Vous pouvez créer des modèles LUIS correspondant à d’autres langues et ajouter une entrée à `cognitivemodels.json` .

```json
{
  "defaultLocale": "en-us",
  "languageModels": {
    "en-us": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    },
    "<your_language_culture>": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    }
  }
}
```

En parallèle, ajoutez le `.lu` fichier correspondant dans le chemin luisFolder. La structure des dossiers doit être la suivante :

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Pour modifier le `languages` paramètre, mettez à jour la commande botskills comme suit :

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Virtual Assistant pour `SetLocaleMiddleware` identifier les paramètres régionaux actuels et appeler le modèle de distribution correspondant. L’activité bot framework possède un champ de paramètres régionaux qui est utilisé par cet intermédiaire. Vous pouvez également utiliser la même technique pour vos compétences. Le bot book-a-room n’utilise pas cet middleware et obtient à la place les paramètres régionaux de l’entité [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de l’activité Bot Framework.

### <a name="claim-validation"></a>Validation des revendications

Nous avons ajouté [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) pour limiter les appelants à la compétence. Pour permettre à un Virtual Assistant d’appeler cette compétence, remplir le tableau à partir de cet `AllowedCallers` `appsettings` ID Virtual Assistant’application.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Le tableau des appelants autorisés peut restreindre les compétences que les consommateurs peuvent utiliser. Ajoutez une entrée `*` unique à ce tableau, pour accepter les appels de n’importe quel consommateur de compétences.

```
"AllowedCallers": [ "*" ],
```

Pour plus d’informations sur l’ajout de la validation des revendications à une compétence, voir ajouter la validation des revendications [aux compétences.](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)

### <a name="limitation-of-card-refresh"></a>Limitation de l’actualisation de la carte 

La mise à jour de l’activité, telle que l’actualisation de carte n’est pas encore prise en charge par Virtual Assistant ([problème github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Par conséquent, nous avons remplacé tous les appels d’actualisation de `UpdateActivityAsync` carte par la publication de nouveaux appels de `SendActivityAsync` carte.

### <a name="card-actions-and-task-module-flows"></a>Actions de carte et flux de module de tâche

Pour qu’une action de carte ou des activités de module de tâche soit transmis à une compétence associée, cette compétence doit `skillId` y être incorporer.
`Book-a-room` Les charges utiles d’action de la carte de robot, d’extraction et d’soumission du module de tâche sont modifiées pour contenir `skillId` en tant que paramètre. 

Pour plus d’informations, [reportez-vous](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) à cette section de cette documentation.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Gérer les activités à partir d’une conversation de groupe ou d’une étendue de canal

`Book-a-room bot` est conçu pour les conversations privées, telles que l’étendue personnelle ou 1:1 uniquement. Étant donné que nous avons personnalisé des Virtual Assistant pour prendre en charge les étendues de conversation de groupe et de canal, le Virtual Assistant doit être appelé à partir des étendues de canal et par conséquent, le bot doit obtenir des activités pour la même `Book-a-room` étendue. Par `Book-a-room` conséquent, le bot est personnalisé pour gérer ces activités. Vous pouvez trouver les méthodes `OnMessageActivityAsync` `Book-a-room` d’enregistrement du handler d’activité du bot.

```csharp
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        // Check if activities are from groupchat/ teams scope. This might happen when the bot is consumed by Virtual Assistant.
        if (turnContext.Activity.Conversation.IsGroup == true)
        {
            await ShowNotSupportedInGroupChatCardAsync(turnContext).ConfigureAwait(false);
        }
        else
        {
            ...
        }
    }
```

Vous pouvez également tirer parti des compétences existantes à partir du référentiel [de solutions Bot Framework](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) ou créer une compétence entièrement à partir de zéro. Pour créer une compétence, consultez des [didacticiels pour créer une compétence.](https://microsoft.github.io/botframework-solutions/overview/skills/) Pour obtenir Virtual Assistant documentation sur l’architecture des compétences et des compétences,[voir Virtual Assistant et l’architecture des compétences.](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)  

## <a name="limitations-of-virtual-assistant"></a>Limitations des Virtual Assistant 

* **EndOfConversation**: une compétence doit envoyer une activité à la `endOfConversation` fin d’une conversation. En fonction de l’activité, un Virtual Assistant contexte avec cette compétence particulière et revient dans le contexte racine Virtual Assistant’entreprise. Pour le bot Book-a-room, il n’existe aucun état clair où la conversation est terminée. Par conséquent, nous n’avons pas envoyé à partir du bot et lorsque l’utilisateur souhaite revenir au contexte racine, il peut simplement le faire `endOfConversation` `Book-a-room` par `start over` commande.  
* **Actualisation de la** carte : l’actualisation de la carte n’est pas encore prise en charge Virtual Assistant.  
* **Extensions de messagerie**:
  * Actuellement, un Virtual Assistant peut prendre en charge un maximum de dix commandes pour les extensions de messagerie.
  * La configuration des extensions de messagerie n’est pas limitée aux commandes individuelles, mais à l’ensemble de l’extension elle-même. Cela limite la configuration de chaque compétence individuelle par le biais de Virtual Assistant.
  * Les ID de commande des extensions de messagerie ont une longueur maximale de [64](../resources/schema/manifest-schema.md#composeextensions) caractères et 37 caractères sont utilisés pour incorporer des informations de compétences. Par conséquent, les contraintes mises à jour pour l’ID de commande sont limitées à 27 caractères.

Vous pouvez également tirer parti des compétences existantes à partir du référentiel [de solutions Bot Framework](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) ou créer une compétence entièrement à partir de zéro. Vous pouvez trouver des didacticiels pour la suite [ici.](https://microsoft.github.io/botframework-solutions/overview/skills/) Reportez-vous [à la documentation relative](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) à l Virtual Assistant et à l’architecture des compétences.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| Modèle Visual Studio mis à jour | Modèle personnalisé pour prendre en charge les fonctionnalités teams. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| Code de compétences pour un bot dans une salle | Vous permet de rechercher et de réserver rapidement une salle de réunion en cours de réunion. | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |


## <a name="see-also"></a>Voir aussi

* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
* [Réserver une salle](app-templates.md#app-template-code-samples)
* [Microsoft Teams bot](../bots/what-are-bots.md)
