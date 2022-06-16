---
title: Créer un assistant virtuel
description: Découvrez comment créer Virtual Assistant bot pour Teams à l’aide d’exemples de code et d’extraits de code avec des fonctionnalités telles que les cartes adaptatives, la gestion des interruptions, etc.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 4b1dc7168cc67cd455182dddd4dd2d14a0cf9c3d
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123061"
---
# <a name="create-virtual-assistant"></a>Créer un assistant virtuel

Virtual Assistant est un modèle Microsoft open-source qui vous permet de créer une solution conversationnelle robuste tout en gardant le contrôle total de l'expérience utilisateur, de la marque de l'organisation et des données nécessaires. Le [modèle de base de l’assistant virtuel](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) est le bloc de construction de base qui rassemble les technologies Microsoft nécessaires à la création d’une Virtual Assistant, notamment le Kit de développement logiciel [(SDK) Bot Framework](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/) et [QnA Maker](https://www.qnamaker.ai/). Il réunit également les fonctionnalités essentielles, notamment l’inscription des compétences, les comptes liés, l’intention conversationnelle de base pour offrir aux utilisateurs une gamme d’interactions et d’expériences transparentes. En outre, les fonctionnalités de modèle incluent de riches exemples de [compétences](https://microsoft.github.io/botframework-solutions/overview/skills) conversationnelles réutilisables.  Les compétences individuelles sont intégrées dans une solution de l’assistant virtuel pour permettre plusieurs scénarios. À l’aide du Kit de développement logiciel (SDK) Bot Framework, les compétences sont présentées sous forme de code source, ce qui vous permet de personnaliser et d’étendre selon vos besoins. Pour plus d’informations sur les compétences de Bot Framework, consultez [Qu’est-ce qu’une compétence Bot Framework](https://microsoft.github.io/botframework-solutions/overview/skills/) ? Ce document vous guide sur les considérations relatives à l’implémentation pour les organisations de l’assistant virtuel, la création d’un assistant virtuel Teams ciblé, l’exemple associé, l’exemple de code et les limitations de l’assistant virtuel.
L’image suivante affiche la vue d’ensemble de l’assistant virtuel :

![Diagramme de l'assistant virtuel](../assets/images/bots/virtual-assistant/overview.png)

Les activités de sms sont routées vers les compétences associées par l’assistant virtuel principal à l’aide d’un modèle de [répartition](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true).

## <a name="implementation-considerations"></a>Considérations relatives à l’implémentation

La décision d’ajouter un assistant virtuel comprend de nombreux déterminants et diffère pour chaque organisation. Les facteurs de prise en charge d’une implémentation d’un assistant virtuel pour votre organisation sont les suivants :

* Une équipe centrale gère toutes les expériences des employés. Il a la possibilité de créer une expérience d’un assistant virtuel et de gérer les mises à jour de l’expérience de base, y compris l’ajout de nouvelles compétences.
* Plusieurs applications existent entre les fonctions métier et le nombre devrait augmenter à l’avenir.
* Les applications existantes sont personnalisables, appartiennent à l’organisation et sont converties en compétences pour un assistant virtuel.
* L’équipe des expériences des employés centraux est en mesure d’influencer les personnalisations des applications existantes. Il fournit également les conseils nécessaires pour intégrer des applications existantes en tant que compétences dans l’expérience de l’assistant virtuel.

L'image suivante présente les fonctions commerciales de l'assistant virtuel :

![L’équipe centrale gère l’assistant et les équipes de fonction métier apportent des compétences.](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Créer un assistant virtuel pour Teams

Microsoft a publié un [modèle Microsoft Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) pour la création d’assistants virtuels et de compétences. Avec le modèle Visual Studio, vous pouvez créer un assistant virtuel, optimisé par une expérience textuelle prenant en charge des cartes enrichies limitées avec des actions. Nous avons amélioré le modèle de base de Visual Studio afin d'inclure les fonctionnalités de la plateforme Microsoft Teams et d'optimiser les expériences des applications Teams. Parmi ces fonctionnalités, citons la prise en charge des cartes adaptatives riches, des modules de tâches, des équipes ou des chats de groupe et des extensions de messages. Pour plus d’informations sur l’extension de l’assistant virtuel à Microsoft Teams, consultez [tutoriel : Étendre votre assistant virtuel à Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).
L’image suivante affiche le diagramme de haut niveau d’une solution de l’assistant virtuel :

![Diagramme de haut niveau d’une solution d’assistant virtuel](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Ajouter des cartes adaptatives à votre assistant virtuel

Pour distribuer correctement les demandes, votre assistant virtuel doit identifier le modèle LUIS correct et la compétence correspondante qui lui sont associées. Toutefois, le mécanisme de répartition ne peut pas être utilisé pour les activités d’action de carte, car le modèle LUIS associé à une compétence est formé pour les textes d’action de carte. Les textes d’action de carte sont des mots clés prédéfinis fixes et non commentés par un utilisateur.

Cet inconvénient est résolu par l’incorporation d’informations de compétence dans la charge utile de l’action de carte. Chaque compétence doit être incorporée `skillId` dans le  `value` champ des actions de carte. Vous devez vous assurer que chaque activité d’action de carte contient les informations de compétence pertinentes, et l’assistant virtuel peut utiliser ces informations pour la répartition.

Vous devez fournir `skillId` dans le constructeur pour vous assurer que les informations de compétence sont toujours présentes dans les actions de carte.
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

Ensuite, la classe `SkillCardActionData` du modèle de l’assistant virtuel est introduite pour extraire `skillId` de la charge utile de l’action de carte.
Un extrait de code à extraire  `skillId` de la charge utile de l’action de carte est illustré dans la section suivante :

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

L’implémentation est effectuée par une méthode d’extension dans la classe [Activité](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .
Un extrait de code à extraire  `skillId` des données d’action de carte est illustré dans la section suivante :

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

L’assistant virtuel peut gérer les interruptions lorsqu’un utilisateur tente d’appeler une compétence alors qu’une autre compétence est actuellement active. `TeamsSkillDialog`, et `TeamsSwitchSkillDialog`sont introduits en fonction de [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) et [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs) de Bot Framework. Ils permettent aux utilisateurs de passer d’une expérience de compétence à des actions de carte. Pour gérer cette demande, l’assistant virtuel invite l’utilisateur avec un message de confirmation à changer de compétences :

![Invite de confirmation lors du passage à une nouvelle compétence](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>Gérer les demandes de module de tâche

Pour ajouter des fonctionnalités de module de tâche à un assistant virtuel, deux méthodes supplémentaires sont incluses dans le gestionnaire d’activités de l’assistant virtuel : `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync`. Ces méthodes écoutent les activités liées aux modules de tâches à partir de l’assistant virtuel, identifient la compétence associée à la demande et transfèrent la demande à la compétence identifiée.

Le transfert de demande est effectué via la [méthode](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) SkillHttpClient`PostActivityAsync`. Elle retourne la réponse comme `InvokeResponse` étant analysée et convertie en `TaskModuleResponse`.

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

Une approche similaire est suivie pour la répartition des actions de carte et les réponses aux modules de tâches. Les données d’action d’extraction et d’envoi du module de tâche sont mises à jour pour inclure `skillId`.
La méthode `GetSkillId` d’extension d’activité extrait `skillId` de la charge utile qui fournit des détails sur la compétence à appeler.

L’extrait de code pour `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync` les méthodes sont donnés dans la section suivante :

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

En outre, vous devez inclure tous les domaines de compétence dans la section dans le `validDomains` fichier manifeste de l’assistant virtuel afin que les modules de tâche appelés via une compétence s’affichent correctement.

### <a name="handle-collaborative-app-scopes"></a>Gérer les étendues d’application collaborative

Les applications Teams peuvent exister dans plusieurs étendues, notamment la conversation 1:1, la conversation de groupe et les canaux. Le modèle de l’assistant virtuel de base est conçu pour les conversations 1:1. Dans le cadre de l’expérience d’intégration, l’assistant virtuel invite les utilisateurs à entrer un nom et conserve l’état de l’utilisateur. Étant donné que l’expérience d’intégration n’est pas adaptée aux étendues de conversation de groupe ou de canal, elle a été supprimée.

Les compétences doivent gérer les activités dans plusieurs étendues, telles que la conversation 1:1, la conversation de groupe et la conversation de canal. Si l’une de ces étendues n’est pas prise en charge, les compétences doivent répondre avec un message approprié.

Les fonctions de traitement suivantes ont été ajoutées à l’assistant virtuel principal :

* L’assistant virtuel peut être appelée sans message texte provenant d’une conversation de groupe ou d’un canal.
* Les articulations sont nettoyées avant d’envoyer le message au module de répartition. Par exemple, supprimez le @mention nécessaire du bot.

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

### <a name="handle-message-extensions"></a>Gérer les extensions de message

Les commandes d’une extension de message sont déclarées dans le fichier manifeste de votre application. L’interface utilisateur de l’extension de message est optimisée par ces commandes. Pour qu’un assistant virtuel alimente une commande d’extension de message en tant que compétence jointe, le propre manifeste d’un assistant virtuel doit contenir ces commandes. Vous devez ajouter les commandes du manifeste d’une compétence individuelle au manifeste de l’assistant virtuel. L’ID de commande fournit des informations sur une compétence associée en ajoutant l’ID d’application de la compétence via un séparateur `:`.

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

L’extrait de code de fichier manifeste de l’assistant virtuel correspondant est illustré dans la section suivante :

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

Une fois les commandes appelées par un utilisateur, l’assistant virtuel peut identifier une compétence associée en analysant l’ID de commande, en mettant à jour l’activité en supprimant le suffixe `:<skill_id>` supplémentaire de l’ID de commande et en le transférant à la compétence correspondante. Le code d’une compétence n’a pas besoin de gérer le suffixe supplémentaire. Ainsi, les conflits entre les ID de commande entre les compétences sont évités. Avec cette approche, toutes les commandes de recherche et d’action d’une compétence dans tous les contextes, telles que **la composition**, **la boîte de commandes** et le **message**, sont optimisées par un assistant virtuel.

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

Certaines activités d’extension de message n’incluent pas l’ID de commande. Par exemple, `composeExtension/selectItem` contient uniquement la valeur de l’action d’appui d’appel. Pour identifier la compétence associée, `skillId`  est attachée à chaque carte d’élément lors de la formation d’une réponse pour `OnTeamsMessagingExtensionQueryAsync`. Cela est similaire à l’approche [d’ajout de cartes adaptatives à votre assistant virtuel](#add-adaptive-cards-to-your-virtual-assistant).

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

L'exemple suivant montre comment convertir le modèle d'application Book-a-room en une compétence d'assistant virtuel : Book-a-room est une application Microsoft Teams qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pour 30, 60 ou 90 minutes à partir de l'heure actuelle. La durée par défaut est de 30 minutes. Le bot Book-a-room s’applique aux conversations personnelles ou 1:1.
L’image suivante affiche un assistant virtuel avec un **livre une compétence de salle** :

![L’assistant virtuel avec une compétence « réserver une salle »](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Voici les modifications delta introduites pour la convertir en compétence attachée à un assistant virtuel. Des instructions similaires sont suivies pour convertir un bot v4 existant en compétence.

### <a name="skill-manifest"></a>Manifeste de compétence

Un manifeste de compétence est un fichier JSON qui expose le point de terminaison de messagerie, l’ID, le nom et d’autres métadonnées pertinentes d’une compétence. Ce manifeste est différent du manifeste utilisé pour charger de manière indépendante une application dans Microsoft Teams. Une assistant virtuel nécessite un chemin d’accès à ce fichier comme entrée pour attacher une compétence. Nous avons ajouté le manifeste suivant au dossier wwwroot du bot.

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

Le modèle de répartition de l’assistant virtuel repose sur les modèles LUIS des compétences jointes. Le modèle de répartition identifie l’intention de chaque activité de texte et découvre la compétence qui lui est associée.

L’assistant virtuel nécessite le modèle LUIS de la compétence au `.lu` format en tant qu’entrée lors de l’attachement d’une compétence. LuiS json est converti au format à l’aide `.lu` de l’outil botframework-cli.

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Le bot Book-a-room a deux commandes principales pour les utilisateurs :

* `Book room`
* `Manage Favorites`

Nous avons créé un modèle LUIS en comprenant ces deux commandes. Les secrets correspondants doivent être renseignés dans `cognitivemodels.json`. Le fichier JSON LUIS correspondant se trouve [ici](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).
Le fichier correspondant `.lu` s’affiche dans la section suivante :

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

Avec cette approche, toute commande émise par un utilisateur pour Virtual Assistant liée `book room` ou `manage favorites` identifiée en tant que commande associée `Book-a-room` au bot est transférée à cette compétence.
En revanche, `Book-a-room room` le bot doit utiliser le modèle LUIS pour comprendre ces commandes si elles ne sont pas typées complètes. Par exemple : `I want to manage my favorite rooms`.

### <a name="multi-language-support"></a>Prise en charge de plusieurs langues

Par exemple, un modèle LUIS avec uniquement la culture anglaise est créé. Vous pouvez créer des modèles LUIS correspondant à d’autres langues et ajouter une entrée à `cognitivemodels.json`.

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

En parallèle, ajoutez le fichier correspondant `.lu` dans le chemin luisFolder. La structure des dossiers doit être la suivante :

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Pour modifier un `languages` paramètre, mettez à jour la commande botskills comme suit :

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

L’assistant virtuel permet d’identifier les paramètres régionaux actuels `SetLocaleMiddleware` et d’appeler le modèle de répartition correspondant. L’activité bot framework a un champ de paramètres régionaux qui est utilisé par cet intergiciel. Vous pouvez également utiliser la même chose pour votre compétence. Le bot Book-a-room n’utilise pas cet intergiciel et obtient à la place les paramètres régionaux de [l’entité clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo) de l’activité Bot Framework.

### <a name="claim-validation"></a>Validation des revendications

Nous avons ajouté [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) pour restreindre les appelants à la compétence. Pour permettre à un assistant virtuel d’appeler cette compétence, renseignez `AllowedCallers` le tableau à partir de l’ID d’application `appsettings` de cet assistant virtuel particulier.

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

Le tableau d’appelants autorisés peut restreindre les consommateurs de compétences qui peuvent accéder à la compétence. Ajoutez une entrée `*` unique à ce tableau pour accepter les appels de n’importe quel consommateur de compétences.

```
"AllowedCallers": [ "*" ],
```

Pour plus d’informations sur l’ajout de la validation des revendications à une compétence, consultez [ajouter la validation des revendications à la compétence](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).

### <a name="limitation-of-card-refresh"></a>Limitation de l’actualisation de la carte

L’activité de mise à jour, telle que l’actualisation de carte, n’est pas encore prise en charge via l’assistant virtuel ([problème github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)). Par conséquent, nous avons remplacé tous les appels `UpdateActivityAsync` d’actualisation de carte par la publication de nouveaux appels `SendActivityAsync`de carte .

### <a name="card-actions-and-task-module-flows"></a>Actions de carte et flux de modules de tâches

Pour transférer des activités d’action de carte ou de module de tâche à une compétence associée, la compétence doit y être incorporée `skillId` .
`Book-a-room` l’action de carte de bot, les charges utiles d’action d’extraction et d’envoi du module de tâches sont modifiées pour qu’elles soient contenues `skillId` en tant que paramètre.

Pour plus d’informations, consultez [cette](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) section de cette documentation.

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>Gérer les activités à partir d’une conversation de groupe ou d’une étendue de canal

`Book-a-room bot` est conçu pour les conversations privées, telles que l’étendue personnelle ou 1:1 uniquement. Étant donné que nous avons personnalisé l’assistant virtuel pour prendre en charge les étendues de conversation de groupe et de canal, l’assistant virtuel doit être appelé à partir des étendues de canal et, par conséquent, `Book-a-room` le bot doit obtenir des activités pour la même étendue. Par conséquent, `Book-a-room`le bot est personnalisé pour gérer ces activités. Vous trouverez les méthodes d’archivage `OnMessageActivityAsync` du gestionnaire d’activités `Book-a-room` du bot.

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

Vous pouvez également tirer parti des compétences existantes à partir du [référentiel Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) ou créer une compétence entièrement à partir de zéro. Pour créer une compétence, consultez [les didacticiels pour créer une compétence](https://microsoft.github.io/botframework-solutions/overview/skills/). Pour obtenir l’assistant virtuel et la documentation sur l’architecture des compétences, consultez [l’assistant virtuel et l’architecture des compétences](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).  

## <a name="limitations-of-virtual-assistant"></a>Limitations de l’assistant virtuel

* **EndOfConversation** : une compétence doit envoyer une `endOfConversation` activité à la fin d’une conversation. En fonction de l’activité, un assistant virtuel termine le contexte avec cette compétence particulière et revient dans le contexte racine de l’assistant virtuel. Pour le bot Book-a-room, il n’existe aucun état clair où la conversation est terminée. Par conséquent, nous n’avons pas envoyé `endOfConversation` de `Book-a-room` bot et quand l’utilisateur souhaite revenir au contexte racine, il peut simplement le faire par `start over` commande.  
* **Actualisation de la carte** : l’actualisation de la carte n’est pas encore prise en charge par le biais de l’assistant virtuel.  
* **Extensions de messages** :
  * Actuellement, un assistant virtuel peut gérer un maximum de dix commandes pour les extensions de message.
  * La configuration des extensions de message n’est pas limitée à des commandes individuelles, mais à l’ensemble de l’extension elle-même. Cela limite la configuration de chaque compétence individuelle via l’assistant virtuel.
  * Les ID de commande des extensions de message ont une longueur maximale de [64 caractères](../resources/schema/manifest-schema.md#composeextensions) et 37 caractères sont utilisés pour incorporer des informations de compétence. Ainsi, les contraintes mises à jour pour l’ID de commande sont limitées à 27 caractères.

Vous pouvez également tirer parti des compétences existantes à partir du [référentiel Bot Framework Solutions](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) ou créer une compétence entièrement à partir de zéro. Vous trouverez des didacticiels pour les versions ultérieures [ici](https://microsoft.github.io/botframework-solutions/overview/skills/). Reportez-vous à la [documentation](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) relative à l’assistant virtuel et à l’architecture des compétences.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| Modèle Visual Studio mis à jour | Modèle personnalisé pour prendre en charge les fonctionnalités des équipes | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| Code de compétence du bot Book-a-room | Vous permet de trouver et de réserver rapidement une salle de réunion en déplacement. | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |

## <a name="see-also"></a>Voir aussi

* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
* [Robot location de salle](app-templates.md#app-template-code-samples)
* [Bot Microsoft Teams](../bots/what-are-bots.md)
