---
title: Assistant virtuel pour Microsoft Teams
description: Comment créer un bot assistant virtuel et des compétences à utiliser dans Microsoft Teams
ms.topic: how-to
keywords: bots d'assistant virtuel Teams
ms.openlocfilehash: 52591435c5a7e1c65a8f86a7c41fe4a3a4fa5c83
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996022"
---
# <a name="virtual-assistant-for-microsoft-teams"></a>Assistant virtuel pour Microsoft Teams

Assistant virtuel est un modèle Microsoft open source qui vous permet de créer une solution conversationnelle robuste tout en conservant un contrôle total de l'expérience utilisateur, de la marque organisationnelle et des données nécessaires. Le [](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) modèle de base assistant virtuel est le bloc de construction de base qui regroupe les technologies Microsoft requises pour créer un Assistant virtuel, y compris le [SDK Bot Framework,](https://github.com/microsoft/botframework-sdk)language [understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), ainsi que les fonctionnalités essentielles, y compris l'inscription des compétences, les comptes liés, l'intention de conversation de base pour offrir aux utilisateurs finaux une gamme d'interactions et d'expériences transparentes. En outre, les fonctionnalités de modèle incluent de riches exemples de compétences de conversation [réutilisables.](https://microsoft.github.io/botframework-solutions/overview/skills)  Les compétences individuelles peuvent être intégrées dans une solution d'Assistant virtuel pour permettre plusieurs scénarios. À l'aide du SDK Bot Framework, les compétences sont présentées sous forme de code source, ce qui vous permet de personnaliser et d'étendre selon vos besoins. Découvrez [ce qu'est une compétence Bot Framework.](https://microsoft.github.io/botframework-solutions/overview/skills/)

![Diagramme de vue d'ensemble de l'Assistant virtuel](../assets/images/bots/virtual-assistant/overview.png)

Les activités de message texte sont acheminées vers les compétences associées par le cœur de l'Assistant virtuel à l'aide [d'un modèle de](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) distribution. 

## <a name="implementation-considerations"></a>Considérations sur l'implémentation

La décision d'ajouter un Assistant virtuel peut inclure de nombreux déterminants et différer pour chaque organisation. Voici les facteurs qui contribuent à l'implémentation d'un Assistant virtuel pour votre organisation :

- Une équipe centrale gère toutes les expériences des employés et a la possibilité de créer une expérience d'Assistant virtuel et de gérer les mises à jour de l'expérience de base, y compris l'ajout de nouvelles compétences.
- Plusieurs applications existent dans les fonctions métiers et/ou le nombre est censé augmenter à l'avenir.
- Les applications existantes sont personnalisables, elles sont la propriété de l'organisation et peuvent être converties en compétences pour un Assistant virtuel.
- L'équipe centrale d'expériences des employés est en mesure d'influencer les personnalisations des applications existantes et de fournir les instructions nécessaires pour intégrer des applications existantes en tant que compétences dans l'expérience de l'Assistant virtuel

![L'équipe centrale maintient l'assistant, et les équipes de fonction professionnelle contribuent aux compétences](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Créer un Assistant virtuel axé sur Teams

Microsoft a publié un modèle [Visual Studio pour](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) créer des assistants virtuels et des compétences. Avec le Visual Studio, vous pouvez créer un Assistant virtuel, optimisé par une expérience textuelle avec prise en charge de cartes enrichies limitées avec des actions. Nous avons amélioré le modèle Visual Studio de base pour inclure les fonctionnalités de la plateforme Microsoft Teams et améliorer les expériences d'application Teams. Quelques-unes des fonctionnalités incluent la prise en charge de cartes adaptatives enrichies, de modules de tâche, de conversations d'équipes/groupes et d'extensions de messagerie. *Voir aussi*, [Didacticiel : Étendre votre Assistant virtuel à Microsoft Teams.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)

![Diagramme de haut niveau d'une solution d'Assistant virtuel](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Ajouter des cartes adaptatives à votre Assistant virtuel

Pour envoyer correctement les demandes, votre Assistant virtuel doit identifier le modèle LUIS approprié et les compétences correspondantes qui lui sont associées. Toutefois, le mécanisme de distribution ne peut pas être utilisé pour les activités d'action de carte, car le modèle LUIS associé à une compétence peut ne pas être formé pour les textes d'action de carte, car il s'agit de mots clés fixes prédéfinis, et non de énoncés d'un utilisateur.

Nous avons résolu ce problème en inséraient des informations de compétences dans la charge utile de l'action de carte. Chaque compétence doit être incorporer `skillId` dans le champ des actions de  `value` carte. Il s'agit de la meilleure façon de s'assurer que chaque activité d'action de carte porte les informations de compétence pertinentes et que l'Assistant virtuel peut utiliser ces informations pour la distribution.

Vous trouverez ci-dessous un exemple de données d'action de carte. En fournissant dans le constructeur, nous nous assurons que les informations de compétences `skillId` sont toujours présentes dans les actions de carte.

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

Ensuite, nous introduisons la classe dans le modèle Assistant virtuel à `SkillCardActionData` extraire `skillId` de la charge utile d'action de carte.

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

Voici un extrait de code à extraire des  `skillId` données d'action de carte. Nous l'avons implémentée en tant que méthode d'extension dans la [classe Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)

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

### <a name="handle-interruptions-gracefully"></a>Gérer les interruptions de manière normale

L'Assistant virtuel peut gérer les interruptions lorsqu'un utilisateur tente d'invoquer une compétence alors qu'une autre compétence est active. nous avons introduit et, sur la base de `TeamsSkillDialog` `TeamsSwitchSkillDialog` [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) et [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de Bot Framework, pour permettre aux utilisateurs de basculer une expérience de compétence à partir d'actions de carte. Pour gérer cette demande, l'Assistant virtuel invite l'utilisateur à transmettre un message de confirmation pour changer de compétences.

![Invite de confirmation lors du passage à une nouvelle compétence](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>Gestion des demandes de module de tâche

Pour ajouter des fonctionnalités de module de tâche à un Assistant virtuel, deux méthodes supplémentaires sont incluses dans le handler d'activité de l'Assistant virtuel : `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync` . Ces méthodes écoutent les activités liées au module de tâche à partir de l'Assistant virtuel, identifient les compétences associées à la demande et la forwardent à la compétence identifiée. 

Le forwarding de demande est effectué via  [la méthode SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync` . Elle renvoie la réponse telle `InvokeResponse` qu'elle est l'une des deux. `TaskModuleResponse`

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

Une approche similaire est suivie pour la distribution des actions de carte et les réponses de module de tâche. Les données d'action d'extraction et d'soumission du module de tâche sont mises à jour pour inclure `skillId` . La méthode d'extension d'activité extrait de la charge utile qui fournit des détails sur les compétences qui `GetSkillId` `skillId` doivent être invoquées.

Vous trouverez ci-dessous un extrait de code pour `OnTeamsTaskModuleFetchAsync` les `OnTeamsTaskModuleSubmitAsync` méthodes.

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

            return invokeResponse.GetTaskModuleRespose();
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

En outre, tous les domaines de compétence doivent être inclus dans la section du fichier manifeste de l'Assistant virtuel afin que les modules de tâche appelés via une compétence `validDomains` s'effectuent correctement.

### <a name="handling-collaborative-app-scopes"></a>Gestion des étendues d'application collaborative

Les applications Teams peuvent exister dans plusieurs étendues, y compris la conversation 1:1, la conversation de groupe et les canaux. Le modèle d'Assistant virtuel principal est conçu pour les conversations 1:1. Dans le cadre de l'expérience d'intégration, l'Assistant virtuel invite les utilisateurs à nommer et maintient l'état de l'utilisateur. Étant donné que cette expérience d'intégration n'est pas adaptée aux étendues de conversation de groupe/canal, elle a été supprimée.

Les compétences doivent gérer les activités dans plusieurs étendues (conversation 1:1, conversation de groupe et conversation de canal). Si l'une de ces étendues n'est pas prise en charge, les compétences doivent répondre par un message approprié.

Les fonctions de traitement suivantes ont été ajoutées au cœur de l'Assistant virtuel :

- L'Assistant virtuel peut être appelé sans message texte d'une conversation de groupe ou d'un canal.
- Les robots sont nettoyés (c'est-à-dire, suppriment les @mention nécessaires du bot) avant d'envoyer le message au module de distribution.

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

### <a name="handling-messaging-extensions"></a>Gestion des extensions de messagerie

Les commandes d'une extension de messagerie sont déclarées dans le fichier manifeste de votre application. L'interface utilisateur de l'extension de messagerie est optimisée par ces commandes. Pour qu'un Assistant virtuel soit en mesure d'alimenter une commande d'extension de messagerie (en tant que compétence jointe), le manifeste d'un Assistant virtuel doit contenir ces commandes. Les commandes du manifeste d'une compétence individuelle doivent également être ajoutées au manifeste de l'Assistant virtuel. L'ID de commande fournit des informations sur une compétence associée en axant l'ID d'application de la compétence via un séparateur ( `:` ).

Vous trouverez ci-dessous un extrait du fichier manifeste d'une compétence.

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

Vous trouverez ci-dessous l'extrait de code du fichier manifeste de l'Assistant virtuel correspondant.

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

Une fois que les commandes sont invoquées par un utilisateur, l'Assistant virtuel peut identifier une compétence associée en parant l'ID de commande, mettre à jour l'activité en supprimant le suffixe supplémentaire ( ) de l'ID de commande et le faire suivre à la compétence `:<skill_id>` correspondante. Le code d'une compétence n'a pas besoin de gérer le suffixe supplémentaire. Par conséquent, les conflits entre les ID de commande entre les compétences sont évités. Avec cette approche, toutes les commandes de recherche et d'action d'une compétence dans tous les contextes (« compose », « commandBox » et « message ») peuvent être optimisées par un Assistant virtuel.

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

Certaines activités d'extension de messagerie n'incluent pas l'ID de commande. Par exemple, `composeExtension/selectItem` contient uniquement la valeur de l'action d'appel d'appel. Pour identifier les compétences associées, est attaché à chaque carte `skillId`  d'élément lors de la formation d'une réponse pour `OnTeamsMessagingExtensionQueryAsync` . (Cette approche est similaire à l'ajout de cartes [adaptatives à votre Assistant virtuel.](#add-adaptive-cards-to-your-virtual-assistant)

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>Exemple : Convertir le modèle d'application De salle à salle en compétence Assistant virtuel

[Book-a-room](app-templates.md#book-a-room) est un [bot Microsoft Teams](../bots/what-are-bots.md) qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pendant 30 (par défaut), 60 ou 90 minutes à partir de l'heure actuelle. Le bot Book-a-room s'étendue à des conversations personnelles ou 1:1.

![Assistant virtuel avec compétence « Réserver une salle »](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Voici les modifications delta introduites pour la convertir en une compétence qui peut être jointe à un Assistant virtuel. Des instructions similaires peuvent être suivies pour convertir n'importe quel bot v4 existant en une compétence.

### <a name="skill-manifest"></a>Manifeste de compétences

Un manifeste de compétences est un fichier JSON qui expose le point de terminaison de messagerie, l'ID, le nom et d'autres métadonnées pertinentes d'une compétence (ce manifeste est différent du manifeste utilisé pour le chargement d'une application dans Microsoft Teams) Un Assistant virtuel requiert un chemin d'accès à ce fichier comme entrée pour joindre une compétence. Nous avons ajouté le manifeste suivant au dossier wwwroot du bot.

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

Le modèle de distribution de l'Assistant virtuel est construit sur les modèles LUIS des compétences jointes. Le modèle de distribution identifie l'intention de chaque activité de texte et détecte les compétences qui lui sont associées.

L'Assistant virtuel nécessite le modèle LUIS des compétences (dans le format) en tant qu'entrée lors de `.lu` l'attachement d'une compétence. Le json LUIS peut être converti au format à l'aide de `.lu` l'outil botframework-cli.

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

Nous avons créé un modèle LUIS comprenant ces deux commandes. Les secrets correspondants doivent être remplies dans `cognitivemodels.json` . Le fichier LUIS JSON [](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) correspondant se trouve ici et voici à quoi ressemble `.lu` le fichier correspondant.

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

Avec cette approche, tous les problèmes de commande d'un utilisateur vers l'Assistant virtuel liés à un bot de salle ou qui peuvent être identifiés comme une commande associée au bot De réservation de salle sont transmis à `book room` `manage favorites` cette compétence.
En revanche, le bot de salle de réservation doit utiliser le modèle LUIS pour comprendre ces commandes s'ils ne sont pas tapés tels quel (par exemple : `I want to manage my favorite rooms` ).

### <a name="multi-language-support"></a>Prise en charge multi-langue

Pour cet exemple, nous avons uniquement créé un modèle LUIS avec culture anglaise. Vous pouvez créer des modèles LUIS correspondant à d'autres langues et ajouter une entrée à `cognitivemodels.json` .

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

Mettez à jour la commande botskills comme suit pour modifier le `languages` paramètre :

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

L'Assistant virtuel `SetLocaleMiddleware` utilise pour identifier les paramètres régionaux actuels et appeler le modèle de distribution correspondant. (L'activité bot framework possède un champ de paramètres régionaux qui est utilisé par cet intermédiaire.) Nous vous recommandons également d'utiliser la même technique pour vos compétences. Le bot book-a-room n'utilise pas cet middleware et obtient à la place les paramètres régionaux de l'entité [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de l'activité Bot Framework.

### <a name="claim-validation"></a>Validation des revendications

Nous avons ajouté [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) pour limiter les appelants à la compétence. Pour permettre à un Assistant virtuel d'appeler cette compétence, remplir le tableau à partir de `AllowedCallers` `appsettings` l'ID d'application de cet Assistant virtuel particulier.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Le tableau des appelants autorisés peut restreindre les compétences que les consommateurs peuvent utiliser. Ajoutez une entrée `*` unique à ce tableau, pour accepter les appels de n'importe quel consommateur de compétences.

```
"AllowedCallers": [ "*" ],
```
Vous pouvez trouver ici une documentation détaillée sur l'ajout de la validation des revendications à une [compétence.](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)

### <a name="card-refresh-limitation"></a>Limitation de l'actualisation de la carte

La mise à jour de l'activité (actualisation de la carte) n'est pas encore prise en charge via l'Assistant[virtuel (problème github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686) Par conséquent, nous avons remplacé tous les appels d'actualisation de carte ( `UpdateActivityAsync` ) par la publication de nouveaux appels de carte( `SendActivityAsync` ).

### <a name="card-actions-and-task-module-flows"></a>Actions de carte et flux de module de tâche

Pour qu'une action de carte ou des activités de module de tâche soit transmis à une compétence associée, cette compétence doit `skillId` y être incorporer.
Les charges utiles d'action d'extraction et d'soumission de module de tâche sont modifiées pour contenir `skillId` en tant que paramètres. 

Pour plus d'informations, [reportez-vous](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) à cette section de cette documentation.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Gérer les activités à partir d'une conversation de groupe ou d'une étendue de canal

Le bot book-a-room est conçu pour les conversations privées (étendue personnelle/1:1) uniquement. Étant donné que nous avons personnalisé l'Assistant virtuel pour prendre en charge les étendues de conversation de groupe et de canal, l'Assistant virtuel peut être appelé à partir de ces étendues et par conséquent, le bot de réservation de salle peut obtenir des activités pour la même. Par conséquent, le bot « Book-a-room » est personnalisé pour gérer ces activités. La vérification a été mise en place dans des méthodes de traitement des activités du `OnMessageActivityAsync` bot Book-a-room.

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

Vous pouvez également tirer parti des compétences existantes du référentiel [de solutions Bot Framework](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) ou créer une compétence entièrement à partir de zéro. Vous pouvez trouver des didacticiels pour la suite [ici.](https://microsoft.github.io/botframework-solutions/overview/skills/) Reportez-vous à [la documentation relative](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) à l'Assistant virtuel et à l'architecture des compétences.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **C#** | **.NET** |
|----------|-----------------|----------|------------------|
| Modèle Visual Studio mis à jour | Modèle personnalisé pour prendre en charge les fonctionnalités teams. | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| Code de compétences pour un bot dans une salle | Vous permet de rechercher et de réserver rapidement une salle de réunion en cours de réunion. |  | [View](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |



## <a name="virtual-assistant-known-limitations"></a>Limitations connues de l'Assistant virtuel

- **EndOfConversation**. Une compétence doit envoyer une `endOfConversation` activité à la fin d'une conversation. sur la base de cette activité, un Assistant virtuel met fin au contexte avec cette compétence particulière et revient dans le contexte (racine) de l'Assistant virtuel. Pour le bot Book-a-room, il n'existe aucun état clair dans lequel la conversation peut être terminée. Par conséquent, nous n'avons pas envoyé à partir du `endOfConversation` bot Book-a-room et lorsque l'utilisateur souhaite revenir au contexte racine, il peut simplement le faire par `start over` commande.
- **Actualisation de la carte.** Les actualisations de carte ne sont pas encore pris en charge via l'Assistant virtuel.
- **Extensions de messagerie**::
  - Actuellement, un Assistant virtuel peut prendre en charge un maximum de dix commandes pour les extensions de messagerie.
  - La configuration des extensions de messagerie n'est pas limitée aux commandes individuelles, mais à l'ensemble de l'extension elle-même. Cela limite la configuration de chaque compétence individuelle par le biais de l'Assistant virtuel.
  - Les ID de commande des extensions de messagerie ont une longueur maximale de [64](../resources/schema/manifest-schema.md#composeextensions) caractères et 37 caractères sont utilisés pour incorporer des informations de compétences. Par conséquent, les contraintes mises à jour pour l'ID de commande sont limitées à 27 caractères.
>
>
