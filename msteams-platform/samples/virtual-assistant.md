---
title: Créer un assistant virtuel
description: Comment créer virtual assistant bot et les compétences pour une utilisation dans Microsoft Teams
localization_priority: Normal
ms.topic: how-to
keywords: équipes robots assistant virtuel
ms.openlocfilehash: 072d9cb5742cd39101587cad32e3048bd36cc1d8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566872"
---
# <a name="create-virtual-assistant"></a>Créer un assistant virtuel 

Virtual Assistant est un modèle open-source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant le plein contrôle de l’expérience utilisateur, de l’image de marque organisationnelle et des données nécessaires. Le [modèle de base Virtual Assistant](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) est le bloc de base qui rassemble les technologies Microsoft nécessaires pour construire un assistant virtuel, y compris le Bot Framework [SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), et [QnA Maker](https://www.qnamaker.ai/). Il réunit également les capacités essentielles, y compris l’enregistrement des compétences, les comptes liés, l’intention conversationnelle de base d’offrir une gamme d’interactions et d’expériences transparentes aux utilisateurs. En outre, les capacités de modèle incluent de riches exemples de compétences conversationnelles [réutilisables.](https://microsoft.github.io/botframework-solutions/overview/skills)  Les compétences individuelles sont intégrées dans une solution d’assistant virtuel pour activer plusieurs scénarios. À l’aide du Bot Framework SDK, les compétences sont présentées sous forme de code source, ce qui vous permet de personnaliser et d’étendre au besoin. Pour plus d’informations sur les compétences de Bot Framework, voir [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/). Ce document vous guide sur les considérations de mise en œuvre d’Assistant virtuel pour les organisations, comment créer un assistant virtuel axé sur la Teams, exemple connexe, exemple de code et limitations de Virtual Assistant.
L’image suivante affiche la vue d’ensemble de l’assistant virtuel :

![Diagramme d’aperçu d’assistant virtuel](../assets/images/bots/virtual-assistant/overview.png)

Les activités de messagerie texte sont acheminées vers les compétences associées par le noyau assistant virtuel à l’aide d’un [modèle](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) de répartition. 

## <a name="implementation-considerations"></a>Considérations de mise en œuvre

La décision d’ajouter un assistant virtuel comprend de nombreux déterminants et diffère pour chaque organisation. Les facteurs de soutien d’une implémentation d’assistant virtuel pour votre organisation sont les suivants :

* Une équipe centrale gère toutes les expériences des employés. Il a la capacité de construire une expérience d’assistant virtuel et de gérer les mises à jour de l’expérience de base, y compris l’ajout de nouvelles compétences.
* Il existe de multiples applications dans toutes les fonctions de l’entreprise et le nombre devrait augmenter à l’avenir.
* Les applications existantes sont personnalisables, appartenant à l’organisation, et sont converties en compétences pour un assistant virtuel.
* L’équipe d’expériences des employés centraux est en mesure d’influencer les personnalisations sur les applications existantes. Il fournit également les conseils nécessaires pour intégrer les applications existantes en tant que compétences dans l’expérience assistant virtuel.

L’image suivante affiche les fonctions métier de Virtual Assistant : 

![L’équipe centrale maintient l’assistant, et les équipes de fonction d’affaires apportent des qualifications](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Créer un assistant virtuel Teams axé sur les Teams

Microsoft a publié un modèle [Visual Studio pour la construction](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) d’assistants virtuels et de compétences. Avec le Visual Studio, vous pouvez créer un assistant virtuel, alimenté par une expérience basée sur le texte avec le soutien de cartes riches limitées avec des actions. Nous avons amélioré le modèle de base Visual Studio pour inclure les capacités de Microsoft Teams et alimenter les expériences d’Teams’applications. Quelques-unes des fonctionnalités incluent la prise en charge de cartes adaptatives riches, modules de tâches, équipes ou chats de groupe, et des extensions de messagerie. Pour plus d’informations sur l’extension de Virtual Assistant Microsoft Teams, [voir Tutoriel: Étendre votre assistant virtuel à Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).    
L’image suivante affiche le diagramme de haut niveau d’une solution assistant virtuel :

![Diagramme de haut niveau d’une solution d’assistant virtuel](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Ajoutez des cartes adaptatives à votre assistant virtuel

Pour envoyer correctement les demandes, votre assistant virtuel doit identifier le modèle LUIS correct et les compétences correspondantes qui lui sont associées. Toutefois, le mécanisme de répartition ne peut pas être utilisé pour les activités d’action par carte car le modèle LUIS associé à une compétence, est formé pour les textes d’action par carte. Les textes d’action de la carte sont fixes, prédéfins mots clés, et non commentés à partir d’un utilisateur.

Cet inconvénient est résolu en intégrant des informations de compétence dans la charge utile d’action de la carte. Chaque compétence doit s’intégrer `skillId` dans le domaine des actions de  `value` carte. Vous devez vous assurer que chaque activité d’action de carte contient les informations de compétences pertinentes, et Virtual Assistant peut utiliser ces informations pour l’expédition.

Vous devez fournir dans `skillId` le constructeur pour s’assurer que les informations de compétence sont toujours présentes dans les actions de carte.
Un exemple de code d’échantillon de données d’action de carte est affiché dans la section suivante :
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

Ensuite, `SkillCardActionData` la classe dans le modèle assistant virtuel est introduit pour extraire de la charge utile `skillId` d’action de la carte.
Un extrait de code à extraire de la  `skillId` charge utile d’action de la carte est affiché dans la section suivante :

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

La mise en œuvre se fait par une méthode d’extension dans la [classe](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) Activité.
Un extrait de code à extraire des données  `skillId` d’action de la carte est affiché dans la section suivante :

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

Virtual Assistant peut gérer les interruptions dans les cas où un utilisateur tente d’invoquer une compétence alors qu’une autre compétence est actuellement active. `TeamsSkillDialog`, et `TeamsSwitchSkillDialog` sont introduits sur la base de [SkillDialog de](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) Bot Framework [et SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs). Ils permettent aux utilisateurs de passer d’une expérience de compétence à des actions de carte. Pour traiter cette demande, l’assistant virtuel invite l’utilisateur avec un message de confirmation à changer de compétences :

![Invite de confirmation lors du passage à une nouvelle compétence](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Gérer les demandes de module de tâches

Pour ajouter des fonctionnalités de module de tâche à un assistant virtuel, deux méthodes supplémentaires sont incluses dans le gestionnaire d’activité Assistant virtuel : `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync` . Ces méthodes écoutent les activités liées au module de tâches de Virtual Assistant, identifient les compétences associées à la demande et transmettre la demande à la compétence identifiée. 

Le transfert de demande se fait par le [biais de la méthode SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync` . Il renvoie la `InvokeResponse` réponse comme qui est parsed et converti en `TaskModuleResponse` .


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

Une approche similaire est suivie pour l’expédition de l’action par carte et les réponses au module de tâches. Module de tâche aller chercher et soumettre des données d’action est mis à jour pour inclure `skillId` . La méthode `GetSkillId` d’extension `skillId` d’activité extrait de la charge utile qui fournit des détails sur la compétence qui doit être invoquée.

L’extrait de code et `OnTeamsTaskModuleFetchAsync` les `OnTeamsTaskModuleSubmitAsync` méthodes sont donnés dans la section suivante :

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

En outre, vous devez inclure tous les domaines de compétence dans `validDomains` la section dans le fichier manifeste de Virtual Assistant afin que les modules de tâches invoqués par un rendu de compétence correctement.

### <a name="handle-collaborative-app-scopes"></a>Gérer les étendues d’applications collaboratives

Teams applications peuvent exister dans plusieurs étendues, y compris le chat 1:1, le chat de groupe et les canaux. Le modèle d’assistant virtuel de base est conçu pour les chats 1:1. Dans le cadre de l’expérience d’onboarding Virtual Assistant invite les utilisateurs à nommer et maintient l’état de l’utilisateur. Étant donné que cette expérience d’onboarding n’est pas adaptée aux étendues de chat de groupe ou de canal, elle a été supprimée.

Les compétences doivent gérer les activités dans de multiples étendues, telles que le chat 1:1, le chat de groupe et la conversation de canal. Si l’une ou l’autre de ces portées n’est pas prise en charge, les compétences doivent répondre par un message approprié.

Les fonctions de traitement suivantes ont été ajoutées au noyau Assistant virtuel :

* Assistant virtuel peut être invoqué sans aucun message texte d’un chat de groupe ou d’un canal.
* Les articulations sont nettoyées avant d’envoyer le message au module de répartition. Par exemple, retirez les @mention du bot.

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

Les commandes d’une extension de messagerie sont déclarées dans votre fichier manifeste d’application. L’interface utilisateur de l’extension de messagerie est alimentée par ces commandes. Pour qu’un assistant virtuel rallonge une commande d’extension de messagerie en tant que compétence jointe, le manifeste d’un assistant virtuel doit contenir ces commandes. Vous devez ajouter les commandes du manifeste d’une compétence individuelle au manifeste de l’assistant virtuel. L’ID de commande fournit des informations sur une compétence associée en appending id de l’application de la compétence par le biais d’un séparateur `:` .

L’extrait du fichier manifeste d’une compétence est affiché dans la section suivante :

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

L’extrait de code manifeste de fichier virtual assistant correspondant est affiché dans la section suivante :

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

Une fois que les commandes sont invoquées par un utilisateur, l’assistant virtuel peut identifier une compétence associée en parsing l’ID de commande, mettre à jour l’activité en supprimant le suffixe supplémentaire de `:<skill_id>` l’ID de commande, et le transmettre à la compétence correspondante. Le code d’une compétence n’a pas besoin de gérer le suffixe supplémentaire. Ainsi, les conflits entre les iD de commande entre les compétences sont évités. Avec cette approche, toutes les commandes de recherche et d’action d’une compétence dans tous les contextes, **tels que composer,** **commanderbox,** **et le message** sont alimentés par un assistant virtuel.

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

Certaines activités d’extension de messagerie n’incluent pas l’id de commande. Par exemple, ne `composeExtension/selectItem` contient que la valeur de l’action d’appel d’enregistrement. Pour identifier la compétence associée, est `skillId`  attaché à chaque carte d’élément tout en formant une réponse pour `OnTeamsMessagingExtensionQueryAsync` . Ceci est similaire à l’approche pour ajouter [des cartes adaptatives à votre assistant virtuel](#add-adaptive-cards-to-your-virtual-assistant).

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

L’exemple suivant montre comment convertir le modèle d’application Book-a-room en une compétence assistant virtuel : Book-a-room est un Microsoft Teams qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pendant 30, 60 ou 90 minutes à partir de l’heure actuelle. Le temps par défaut est de 30 minutes. Le livre-une-chambre bot portées à des conversations personnelles ou 1:1. L’image suivante affiche un assistant virtuel avec un **livre une compétence de** chambre:

![Assistant virtuel avec une compétence « réserver une chambre »](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Voici les modifications delta introduites pour la convertir en une compétence qui est attachée à un assistant virtuel. Des lignes directrices similaires sont suivies pour convertir tout bot v4 existant en une compétence.

### <a name="skill-manifest"></a>Manifeste de compétence

Un manifeste de compétences est un fichier JSON qui expose le point de terminaison de messagerie, l’ID, le nom et d’autres métadonnées pertinentes d’une compétence. Ce manifeste est différent du manifeste utilisé pour le chargement latéral d’une application dans Microsoft Teams. Un assistant virtuel nécessite un chemin vers ce fichier comme une entrée pour joindre une compétence. Nous avons ajouté le manifeste suivant au dossier wwwroot du bot.

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

### <a name="luis-integration"></a>INTÉGRATION LUIS

Le modèle de répartition de Virtual Assistant est construit en fonction des modèles LUIS des compétences attachées. Le modèle d’expédition identifie l’intention de chaque activité de texte et découvre les compétences qui y sont associées.

Virtual Assistant nécessite le modèle LUIS de compétence en `.lu` format comme entrée tout en attachant une compétence. LUIS json est converti en format à `.lu` l’aide de l’outil botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Book-a-room bot a deux commandes principales pour les utilisateurs:

- `Book room`
- `Manage Favorites`

Nous avons construit un modèle LUIS en comprenant ces deux commandes. Les secrets correspondants doivent être peuplés dans `cognitivemodels.json` . Le fichier LUIS JSON correspondant se trouve [ici](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).
Le fichier `.lu` correspondant est affiché dans la section suivante :

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

Avec cette approche, toute commande émise par un utilisateur à Virtual Assistant liée `book room` ou sont identifiées comme une commande associée au bot et est transmise à cette `manage favorites` `Book-a-room` compétence.
D’autre part, `Book-a-room room` bot doit utiliser le modèle LUIS pour comprendre ces commandes si elles ne sont pas tapées à plein. Par exemple : `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Support multi-langues

À titre d’exemple, un modèle LUIS avec seulement la culture anglaise est créé. Vous pouvez créer des modèles LUIS correspondant à d’autres langues et ajouter l’entrée à `cognitivemodels.json` .

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

En parallèle, ajoutez le fichier `.lu` correspondant dans le chemin luisFolder. La structure du dossier doit être la suivante :

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

Virtual Assistant utilise pour `SetLocaleMiddleware` identifier le lieu actuel et invoquer le modèle de répartition correspondant. L’activité de framework bot a le champ local qui est employé par ce middleware. Vous pouvez utiliser la même chose pour vos compétences ainsi. Book-a-room bot n’utilise pas ce middleware et obtient plutôt local de Bot framework activity [clientInfo entité](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).

### <a name="claim-validation"></a>Validation des réclamations

Nous avons ajouté [claimsValidator pour](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) limiter les appelants à la compétence. Pour permettre à un assistant virtuel d’appeler cette compétence, remplissez `AllowedCallers` le tableau à partir de `appsettings` l’iD d’application de cet assistant virtuel particulier.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Le tableau des appelants autorisé peut restreindre les compétences auxquelles les consommateurs peuvent accéder. Ajoutez une seule entrée `*` à ce tableau, pour accepter les appels de n’importe quel consommateur de compétences.

```
"AllowedCallers": [ "*" ],
```

Pour plus d’informations sur l’ajout de validation des revendications à une compétence, voir [ajouter la validation des revendications à la compétence](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).

### <a name="limitation-of-card-refresh"></a>Limitation de la actualisation de la carte 

La mise à jour de l’activité, telle que la mise à jour de la carte, n’est pas encore prise en charge par Virtual Assistant[(github issue).](https://github.com/microsoft/botbuilder-dotnet/issues/3686) Par conséquent, nous avons remplacé tous les appels de rafraîchissement de carte `UpdateActivityAsync` par l’affichage de nouveaux appels de carte `SendActivityAsync` .

### <a name="card-actions-and-task-module-flows"></a>Actions de carte et flux de modules de tâches

Pour transmettre l’action de la carte ou les activités du module de tâche à une compétence associée, la compétence doit `skillId` s’y intégrer.
`Book-a-room` l’action de la carte bot, le module de tâche aller chercher et soumettre des charges utiles d’action sont modifiés pour `skillId` contenir comme un paramètre. 

Pour plus [d’informations, consultez](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) cette section à partir de cette documentation.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Gérer les activités à partir d’un chat de groupe ou d’une portée de canal

`Book-a-room bot` est conçu pour les conversations privées, telles que la portée personnelle ou 1:1 seulement. Puisque nous avons personnalisé Virtual Assistant pour prendre en charge le chat de groupe et les étendues de canaux, l’assistant virtuel doit être invoqué à partir des étendues de canaux et donc, `Book-a-room` bot doit obtenir des activités pour la même portée. Par `Book-a-room` conséquent bot est personnalisé pour gérer ces activités. Vous pouvez trouver les méthodes `OnMessageActivityAsync` `Book-a-room` d’enregistrement du gestionnaire d’activité du bot.

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

Vous pouvez également tirer parti des compétences existantes à partir [du référentiel Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) ou créer une nouvelle compétence à partir de zéro. Pour créer une nouvelle compétence, consultez des [tutoriels pour créer une nouvelle compétence.](https://microsoft.github.io/botframework-solutions/overview/skills/) Pour la documentation sur l’architecture des assistants virtuels et des compétences,[consultez Virtual Assistant et skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).  

## <a name="limitations-of-virtual-assistant"></a>Limitations de l’assistant virtuel 

* **EndOfConversation**: Une compétence doit envoyer une activité `endOfConversation` lorsqu’elle termine une conversation. Basé sur l’activité, un assistant virtuel termine le contexte avec cette compétence particulière et revient dans le contexte racine de Virtual Assistant. Pour book-a-room bot, il n’y a pas d’état clair où la conversation est terminée. Par conséquent, nous `endOfConversation` n’avons pas envoyé de bot et quand `Book-a-room` l’utilisateur veut revenir au contexte racine, ils peuvent simplement le faire par `start over` commande.  
* **Actualisation de la** carte : La mise à jour de la carte n’est pas encore prise en charge par Virtual Assistant.  
* **Extensions de messagerie**:
  * Actuellement, un assistant virtuel peut prendre en charge un maximum de dix commandes pour les extensions de messagerie.
  * La configuration des extensions de messagerie n’est pas étendue aux commandes individuelles, mais à l’ensemble de l’extension elle-même. Cela limite la configuration de chaque compétence individuelle par l’intermédiaire de Virtual Assistant.
  * Les iD de commande d’extensions de messagerie ont une longueur maximale [de 64 caractères](../resources/schema/manifest-schema.md#composeextensions) et 37 caractères sont utilisés pour intégrer des informations de compétence. Ainsi, les contraintes mises à jour pour l’id de commande sont limitées à 27 caractères.

Vous pouvez également tirer parti des compétences existantes à partir [du référentiel Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) ou créer une nouvelle compétence à partir de zéro. Tutoriels pour le plus tard peuvent être trouvés [ici](https://microsoft.github.io/botframework-solutions/overview/skills/). Veuillez consulter la [documentation pour l’assistant](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) virtuel et l’architecture des compétences.

## <a name="code-sample"></a>Exemple de code

| **Nom de l’échantillon** | **Description** | **C#** | **.NET (en)** |
|----------|-----------------|----------|------------------|
| Modèle de studio visuel mis à jour | Modèle personnalisé pour prendre en charge les capacités des équipes. | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| Code de compétence de bot de livre-une-chambre | Vous permet de trouver rapidement et réserver une salle de réunion sur la aller. |  | [View](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a>Voir aussi

- [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)

- [Réservez une chambre](app-templates.md#book-a-room)

- [bot Microsoft Teams](../bots/what-are-bots.md)