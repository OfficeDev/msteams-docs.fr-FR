---
title: Assistant virtuel pour Microsoft teams
description: Comment créer des compétences et des robots d’assistant virtuel pour une utilisation dans Microsoft teams
keywords: robots de l’assistant virtuel teams
ms.openlocfilehash: 0bb1ad832fd33675e607874fcc50f20ffbb96943
ms.sourcegitcommit: 26b7404142706290810064f8216abaa1c262d1e5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/16/2020
ms.locfileid: "45146008"
---
# <a name="virtual-assistant-for-microsoft-teams"></a>Assistant virtuel pour Microsoft teams

Virtual Assistant est un modèle de source ouverte Microsoft qui vous permet de créer une solution de conversation robuste tout en conservant un contrôle total de l’expérience utilisateur, de la personnalisation de l’organisation et des données nécessaires. Le [modèle de base de l’assistant virtuel](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) est le bloc de construction de base qui rassemble les technologies Microsoft nécessaires à la création d’un assistant virtuel, notamment le [Kit de développement logiciel (SDK](https://github.com/microsoft/botframework-sdk)) de robot, le mémorandum d’accord de [langue (Luis)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), ainsi que les fonctionnalités essentielles, notamment l’enregistrement des compétences, les comptes liés, l’intention de conversation de base pour offrir aux utilisateurs En outre, les fonctionnalités de modèle incluent des exemples enrichis de [compétences](https://microsoft.github.io/botframework-solutions/overview/skills)de conversation réutilisables.  Les compétences individuelles peuvent être intégrées dans une solution assistant virtuel pour permettre plusieurs scénarios. À l’aide du kit de développement logiciel (SDK) de robot, les compétences sont présentées sous forme de code source, ce qui vous permet de personnaliser et d’étendre les besoins. Voir [What is a bot Framework Skills](https://microsoft.github.io/botframework-solutions/overview/skills/).

![Diagramme de vue d’ensemble de l’assistant virtuel](../assets/images/bots/virtual-assistant/overview.png)

Les activités de message texte sont acheminées vers les compétences associées par le noyau de l’assistant virtuel à l’aide d’un modèle de [répartition](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) . 

## <a name="implementation-considerations"></a>Considérations relatives à l’implémentation

La décision d’ajouter un assistant virtuel peut inclure de nombreux déterminants et diffère pour chaque organisation. Voici les facteurs qui prennent en charge l’implémentation d’un assistant virtuel pour votre organisation :

- Une équipe centrale gère toutes les expériences des employés et offre la possibilité de créer une expérience de l’assistant virtuel et de gérer les mises à jour de l’expérience principale, y compris l’ajout de nouvelles compétences.
- Il existe plusieurs applications pour les fonctions professionnelles et/ou le nombre devrait augmenter à l’avenir.
- Les applications existantes sont personnalisables, détenues par l’organisation et peuvent être converties en compétences pour un assistant virtuel.
- L’équipe centrale employés-expériences peut influencer les personnalisations apportées aux applications existantes et fournir les instructions nécessaires pour intégrer les applications existantes en tant que compétences dans l’expérience de l’assistant virtuel

![L’équipe centrale gère l’Assistant et les compétences de Team Function Teams.](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Créer un assistant virtuel centré sur teams

Microsoft a publié un [modèle Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) pour créer des assistants virtuels et des compétences. Avec le modèle Visual Studio, vous pouvez créer un assistant virtuel, alimenté par une expérience basée sur le texte avec prise en charge de cartes riches limitées avec des actions. Nous avons amélioré le modèle de base Visual Studio pour inclure les fonctionnalités de la plateforme Microsoft teams et les expériences de l’application Power Great Teams. Quelques-unes des fonctionnalités incluent la prise en charge de cartes adaptatives riches, de modules de tâches, d’équipes/de conversations de groupes et d’extensions de messagerie. *Voir aussi* [Tutorial : étendre votre assistant virtuel à Microsoft teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).

![Diagramme de haut niveau d’une solution d’assistant virtuel](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Ajouter des cartes adaptatives à votre assistant virtuel

Pour distribuer les demandes correctement, votre assistant virtuel doit identifier le modèle LUIS correct et les compétences correspondantes associées. Toutefois, le mécanisme de répartition ne peut pas être utilisé pour les activités d’action de carte étant donné que le modèle LUIS associé à une compétence ne peut pas être formé pour les textes d’action de carte, car il s’agit de mots clés prédéfinis et non d’énoncés d’un utilisateur.

Nous avons résolu cela en incorporant des informations sur les compétences dans la charge utile d’action de la carte. Toutes les compétences doivent être incorporées `skillId` dans le `value` champ des actions de carte. Il s’agit de la meilleure façon de vous assurer que chaque activité d’action de carte véhicule les informations de compétences pertinentes et que l’assistant virtuel peut utiliser ces informations pour la distribution.

Vous trouverez ci-dessous un exemple de données d’action de carte. En fournissant `skillId` dans le constructeur, nous nous assurons que les informations sur les compétences sont toujours présentes dans les actions de carte.

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

Ensuite, nous introduisons `SkillCardActionData` la classe dans le modèle de l’assistant virtuel pour extraire `skillId` de la charge utile de la carte.

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

Vous trouverez ci-dessous un extrait de code pour extraire `skillId` des données d’action de carte. Nous l’avons implémentée en tant que méthode d’extension dans la classe [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .

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

### <a name="handle-interruptions-gracefully"></a>Gérer les interruptions de manière appropriée

L’assistant virtuel peut gérer les interruptions lorsqu’un utilisateur tente d’appeler une compétence alors qu’une autre compétence est actuellement active. Nous avons introduit `TeamsSkillDialog` et `TeamsSwitchSkillDialog` , en se basant sur les [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) et [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de l’infrastructure bot, pour permettre aux utilisateurs de changer une expérience de compétences à partir d’actions de carte. Pour gérer cette demande, l’assistant virtuel invite l’utilisateur à indiquer un message de confirmation pour faire basculer les compétences.

![Invite de confirmation lors du basculement vers une nouvelle qualification](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>Gestion des demandes de module de tâche

Pour ajouter des fonctionnalités de module de tâches à un assistant virtuel, deux méthodes supplémentaires sont incluses dans le gestionnaire d’activités de l’Assistant Virtual : `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync` . Ces méthodes écoutent les activités liées au module de tâche à partir de l’assistant virtuel, identifient les compétences associées à la demande et transfèrent la demande à la compétence identifiée. 

Le transfert des demandes est réalisé via la méthode [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable) `PostActivityAsync` . Elle renvoie la réponse telle qu’elle `InvokeResponse` est analysée et convertie en `TaskModuleResponse` .

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

Une approche similaire est suivie pour les réponses de module de tâche et de distribution d’action de carte. Les données d’action d’extraction et d’envoi du module tâches sont mises à jour pour inclure `skillId` . `GetSkillId`La méthode d’extension d’activité extrait `skillId` de la charge utile, qui fournit des détails sur les compétences qui doivent être appelées.

Vous trouverez ci-dessous un extrait de code pour `OnTeamsTaskModuleFetchAsync` et des `OnTeamsTaskModuleSubmitAsync` méthodes.

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

De plus, tous les domaines de compétences doivent être inclus dans la `validDomains` section du fichier manifeste de l’assistant virtuel afin que les modules de tâches appelés via un rendu de compétences soient correctement affichés.

### <a name="handling-collaborative-app-scopes"></a>Gestion des étendues d’applications collaboratives

Les applications teams peuvent exister dans plusieurs étendues, y compris la conversation de 1:1, la conversation de groupe et les canaux. Le modèle de l’assistant virtuel principal est conçu pour les conversations de 1:1. Dans le cadre de l’Assistant Virtual expérience d’intégration, l’assistant virtuel invite les utilisateurs à fournir un nom et gère l’état de l’utilisateur. Étant donné que cette expérience d’intégration n’est pas adaptée aux étendues de conversation de groupe/canal, elle a été supprimée.

Les compétences doivent gérer les activités dans plusieurs étendues (1:1 chat, conversation de groupe et conversation de canal). Si l’une de ces étendues n’est pas prise en charge, les compétences doivent répondre avec un message approprié.

Les fonctions de traitement suivantes ont été ajoutées à Virtual Assistant Core :

- L’assistant virtuel peut être appelé sans aucun message texte provenant d’une conversation ou d’un canal de groupe.
- Les articulations sont nettoyées (autrement dit, supprimez les @mention nécessaires du bot) avant d’envoyer le message au module de répartition.

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

Les commandes pour une extension de messagerie sont déclarées dans le fichier manifeste de votre application. L’interface utilisateur de l’extension de messagerie est gérée par ces commandes. Pour qu’un assistant virtuel alimente une commande d’extension de messagerie (en tant que compétence attachée), le propre manifeste d’un assistant virtuel doit contenir ces commandes. Les commandes du manifeste d’une compétence individuelle doivent également être ajoutées au manifeste de l’assistant virtuel. L’ID de commande fournit des informations sur une compétence associée en ajoutant l’ID de l’application de la compétence via un séparateur ( `:` ).

Vous trouverez ci-dessous un extrait du fichier manifeste d’une compétence.

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

Et, ci-dessous, l’extrait de code du fichier de manifeste de l’assistant virtuel correspondant.

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

Une fois que les commandes sont appelées par un utilisateur, l’assistant virtuel peut identifier une compétence associée en analysant l’ID de commande, mettre à jour l’activité en supprimant le suffixe supplémentaire ( `:<skill_id>` ) de l’ID de commande et le transférer à la compétence correspondante. Le code d’une compétence n’a pas besoin de gérer le suffixe supplémentaire, de sorte que les conflits entre les ID de commande entre les compétences sont évités. Avec cette approche, toutes les commandes de recherche et d’action d’une compétence dans tous les contextes (« composition », « commandBox » et « message ») peuvent être gérées par un assistant virtuel.

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

Certaines activités d’extension de messagerie n’incluent pas l’ID de commande. Par exemple, `composeExtension/selectItem` contient uniquement la valeur de l’action appeler le TAP. Pour identifier la compétence associée, `skillId` est joint à chaque fiche d’article tout en formant une réponse à `OnTeamsMessagingExtensionQueryAsync` . (Cette méthode est similaire à celle permettant d' [Ajouter des cartes adaptatives à votre assistant virtuel](#add-adaptive-cards-to-your-virtual-assistant).

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>Exemple : convertir le modèle d’application livre-a-Room en habiletés de l’assistant virtuel

[Book-a-room](app-templates.md#book-a-room) est un [robot Microsoft teams](../bots/what-are-bots.md) qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pour 30 (par défaut), 60 ou 90 minutes à compter de l’heure actuelle. Les étendues de bot livre-a-room aux conversations personnelles ou 1:1.

![Assistant virtuel avec une compétence « réserver une salle »](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Les éléments suivants sont les modifications Delta introduites pour les convertir en une compétence qui peut être associée à un assistant virtuel. Des instructions similaires peuvent être suivies pour convertir tout robot v4 existant en compétences.

### <a name="skill-manifest"></a>Manifeste de compétences

Un manifeste de compétences est un fichier JSON qui expose un point de terminaison de messagerie, un ID, un nom et d’autres métadonnées pertinentes (ce manifeste est différent du manifeste utilisé pour chargement une application dans Microsoft Teams) un assistant virtuel requiert un chemin d’accès à ce fichier comme entrée pour joindre une compétence. Nous avons ajouté le manifeste suivant au dossier Wwwroot du bot.

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

### <a name="luis-integration"></a>Intégration de LUIS

Le modèle de répartition de l’assistant virtuel est basé sur les modèles LUIS des compétences attachées. Le modèle de répartition identifie l’intention pour chaque activité de texte et Découvre les compétences associées.

L’assistant virtuel nécessite le modèle LUIS de compétences (au `.lu` format) en tant qu’entrée lors de l’attachement d’une compétence. Le format JSON LUIS peut être converti en `.lu` format à l’aide de l’outil botframework-CLI.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Book-a-room bot dispose de deux commandes principales pour les utilisateurs :

- `Book room`
- `Manage Favorites`

Nous avons créé un modèle LUIS qui comprenne ces deux commandes. Les secrets correspondants doivent être renseignés `cognitivemodels.json` . Vous trouverez [ici](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) le fichier JSON Luis correspondant, ainsi que l' `.lu` apparence du fichier correspondant.

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

Dans le cadre de cette approche, les commandes émises par un utilisateur vers un assistant virtuel lié à `book room` ou `manage favorites` peuvent être identifiées en tant que commandes associées à un bot livre-a-room et sont transmises à cette compétence.
En revanche, livre-a-room main bot doit utiliser le modèle LUIS pour comprendre ces commandes s’ils ne sont pas tapés tels quels (par exemple : `I want to manage my favorite rooms` ).

### <a name="multi-language-support"></a>Prise en charge de plusieurs langues

Pour cet exemple, nous avons créé uniquement un modèle LUIS avec une culture en anglais. Vous pouvez créer des modèles LUIS correspondant à d’autres langages et ajouter une entrée à `cognitivemodels.json` .

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

En parallèle, ajoutez le `.lu` fichier correspondant dans le chemin d’accès luisFolder. La structure de dossiers doit être la suivante :

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Mettez à jour la commande botskills comme suit pour modifier le `languages` paramètre :

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

L’assistant virtuel utilise `SetLocaleMiddleware` pour identifier les paramètres régionaux en cours et appeler le modèle de répartition correspondant. (L’activité de l’infrastructure bot a un champ de paramètres régionaux utilisé par ce middleware.) Nous vous recommandons également d’utiliser le même pour vos compétences. Book-a-room bot n’utilise pas ce middleware et obtient à la place des paramètres régionaux de l' [entité clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de l’activité de l’infrastructure bot.

### <a name="claim-validation"></a>Validation de revendication

Nous avons ajouté [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) pour restreindre les appelants à la compétence. Pour permettre à un assistant virtuel d’appeler cette qualification, renseignez le `AllowedCallers` tableau à `appsettings` l’aide de l’ID d’application de cet assistant virtuel particulier.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Le tableau des appelants autorisés peut restreindre les compétences auxquelles les consommateurs peuvent accéder. Ajoutez une entrée unique `*` à ce tableau pour accepter les appels de tous les consommateurs de compétences.

```
"AllowedCallers": [ "*" ],
```
Vous trouverez [ici](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)une documentation détaillée sur l’ajout de la validation des revendications à une compétence.

### <a name="card-refresh-limitation"></a>Limitation de l’actualisation de la carte

L’activité de mise à jour (actualisation de carte) n’est pas encore prise en charge via l’assistant virtuel ([problème GitHub](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Par conséquent, nous avons remplacé tous les appels d’actualisation de carte ( `UpdateActivityAsync` ) par la publication de nouveaux appels de carte ( `SendActivityAsync` ).

### <a name="card-actions-and-task-module-flows"></a>Actions de carte et flux de module de tâches

Pour transférer les activités d’une action de carte ou d’un module de tâche à une compétence associée, la compétence doit être incorporée `skillId` .
Action de la carte de robot de livre-a-room, le module de tâche FETCH and Submit action Payloads est modifié pour contenir `skillId` comme paramètre. 

Pour plus d’informations, reportez-vous à [cette](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section à partir de cette documentation.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Gérer les activités à partir de la conversation de groupe ou de l’étendue de canal

Book-a-room bot est conçu pour les conversations privées (personnelles/1:1 étendue) uniquement. Étant donné que l’assistant virtuel personnalisé prend en charge la conversation de groupe et les étendues de canal, l’assistant virtuel peut être appelé à partir de ces étendues et, par conséquent, le bot livre-a-Room peut obtenir des activités pour le même. Par conséquent, le bot de livre-a-Room est personnalisé pour gérer ces activités. La vérification a été placée dans les `OnMessageActivityAsync` méthodes du gestionnaire d’activité livre-a-room.

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

Vous pouvez également tirer parti des compétences existantes du [référentiel de solutions de robots](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) ou créer une nouvelle compétence entièrement complète. Vous trouverez des didacticiels pour les versions ultérieures [ici](https://microsoft.github.io/botframework-solutions/overview/skills/). Reportez-vous à [la documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0) pour l’assistant virtuel et l’architecture des compétences.

## <a name="sample-code-to-get-started"></a>Exemple de code pour commencer

- [Modèle Visual Studio mis à jour](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [Livre-code de compétences de robot a-room](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a>Limitations connues de l’assistant virtuel

- **EndOfConversation**. Une compétence doit envoyer une `endOfConversation` activité lorsqu’elle termine une conversation. Cette activité est basée sur cette activité, un assistant virtuel met fin au contexte avec cette compétence particulière et revient dans le contexte de l’assistant virtuel (racine). Pour un bot livre-a-room, il n’existe pas d’État clair où la conversation peut être terminée. Par conséquent, nous n’avons pas envoyé `endOfConversation` de livre-a-room bot et lorsque l’utilisateur souhaite revenir au contexte racine, il peut simplement le faire par `start over` Command.
- **Actualisation**de la carte. L’actualisation de la carte n’est pas encore prise en charge par l’assistant virtuel.
- **Extensions de messagerie**:
  - À l’heure actuelle, un assistant virtuel peut prendre en charge un maximum de dix commandes pour les extensions de messagerie.
  - La configuration des extensions de messagerie n’est pas limitée aux commandes individuelles, mais pour l’intégralité de l’extension. Cela limite la configuration de chaque compétence par le biais de l’assistant virtuel.
  - Les ID de commande des extensions de messagerie ont une longueur maximale de [64 caractères](../resources/schema/manifest-schema.md#composeextensions) et 37 caractères seront utilisés pour incorporer des informations sur les compétences. Par conséquent, les contraintes mises à jour pour l’ID de commande sont limitées à 27 caractères.
>
>
