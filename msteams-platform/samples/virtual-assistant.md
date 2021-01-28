---
title: Assistant virtuel pour Microsoft Teams
description: Comment créer un bot assistant virtuel et des compétences à utiliser dans Microsoft Teams
ms.topic: how-to
keywords: bots d’assistant virtuel Teams
ms.openlocfilehash: d72b1afbf975707d694d4aaef31263a3ce467629
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014613"
---
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="c256d-104">Assistant virtuel pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c256d-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="c256d-105">Assistant virtuel est un modèle open source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant un contrôle total de l’expérience utilisateur, de la marque organisationnelle et des données nécessaires.</span><span class="sxs-lookup"><span data-stu-id="c256d-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="c256d-106">Le [](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) modèle de base assistant virtuel est le bloc de construction de base qui regroupe les technologies Microsoft requises pour créer un Assistant virtuel, y compris le [SDK Bot Framework,](https://github.com/microsoft/botframework-sdk)language [understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), ainsi que les fonctionnalités essentielles, y compris l’inscription des compétences, les comptes liés, l’intention de conversation de base pour offrir aux utilisateurs finaux une gamme d’interactions et d’expériences transparentes.</span><span class="sxs-lookup"><span data-stu-id="c256d-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="c256d-107">En outre, les fonctionnalités de modèle incluent de riches exemples de compétences de conversation [réutilisables.](https://microsoft.github.io/botframework-solutions/overview/skills)</span><span class="sxs-lookup"><span data-stu-id="c256d-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="c256d-108">Les compétences individuelles peuvent être intégrées dans une solution d’Assistant virtuel pour permettre plusieurs scénarios.</span><span class="sxs-lookup"><span data-stu-id="c256d-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="c256d-109">À l’aide du SDK Bot Framework, les compétences sont présentées sous forme de code source, ce qui vous permet de personnaliser et d’étendre selon les besoins.</span><span class="sxs-lookup"><span data-stu-id="c256d-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="c256d-110">Découvrez [ce qu’est une compétence Bot Framework.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="c256d-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![Diagramme de vue d’ensemble de l’Assistant virtuel](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="c256d-112">Les activités de message texte sont acheminées vers les compétences associées par le cœur de l’Assistant virtuel à l’aide [d’un modèle de](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) distribution.</span><span class="sxs-lookup"><span data-stu-id="c256d-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="c256d-113">Considérations sur l’implémentation</span><span class="sxs-lookup"><span data-stu-id="c256d-113">Implementation considerations</span></span>

<span data-ttu-id="c256d-114">La décision d’ajouter un Assistant virtuel peut inclure de nombreux déterminants et différer pour chaque organisation.</span><span class="sxs-lookup"><span data-stu-id="c256d-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="c256d-115">Voici les facteurs qui contribuent à l’implémentation d’un Assistant virtuel pour votre organisation :</span><span class="sxs-lookup"><span data-stu-id="c256d-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="c256d-116">Une équipe centrale gère toutes les expériences des employés et a la possibilité de créer une expérience d’Assistant virtuel et de gérer les mises à jour de l’expérience de base, y compris l’ajout de nouvelles compétences.</span><span class="sxs-lookup"><span data-stu-id="c256d-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="c256d-117">Plusieurs applications existent dans les fonctions métiers et/ou le nombre est censé augmenter à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="c256d-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="c256d-118">Les applications existantes sont personnalisables, elles sont la propriété de l’organisation et peuvent être converties en compétences pour un Assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="c256d-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="c256d-119">L’équipe centrale d’expériences des employés est en mesure d’influencer les personnalisations des applications existantes et de fournir les instructions nécessaires pour intégrer des applications existantes en tant que compétences dans l’expérience de l’Assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="c256d-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![L’équipe centrale maintient l’assistant, et les équipes de fonction professionnelle contribuent aux compétences](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="c256d-121">Créer un Assistant virtuel axé sur Teams</span><span class="sxs-lookup"><span data-stu-id="c256d-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="c256d-122">Microsoft a publié un modèle [Visual Studio pour](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) créer des assistants virtuels et des compétences.</span><span class="sxs-lookup"><span data-stu-id="c256d-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="c256d-123">Avec le Visual Studio, vous pouvez créer un Assistant virtuel, optimisé par une expérience textuelle avec prise en charge de cartes enrichies limitées avec des actions.</span><span class="sxs-lookup"><span data-stu-id="c256d-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="c256d-124">Nous avons amélioré le modèle Visual Studio de base pour inclure les fonctionnalités de la plateforme Microsoft Teams et améliorer les expériences d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="c256d-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="c256d-125">Quelques-unes des fonctionnalités incluent la prise en charge de cartes adaptatives enrichies, de modules de tâche, de conversations d’équipes/groupes et d’extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="c256d-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="c256d-126">*Voir aussi*, [Didacticiel : Étendre votre Assistant virtuel à Microsoft Teams.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)</span><span class="sxs-lookup"><span data-stu-id="c256d-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![Diagramme de haut niveau d’une solution d’Assistant virtuel](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="c256d-128">Ajouter des cartes adaptatives à votre Assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="c256d-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="c256d-129">Pour envoyer correctement les demandes, votre Assistant virtuel doit identifier le modèle LUIS approprié et les compétences correspondantes qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="c256d-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="c256d-130">Toutefois, le mécanisme de distribution ne peut pas être utilisé pour les activités d’action de carte, car le modèle LUIS associé à une compétence peut ne pas être formé pour les textes d’action de carte, car il s’agit de mots clés fixes prédéfinis, et non de énoncés d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c256d-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="c256d-131">Nous avons résolu ce problème en inséraient des informations de compétences dans la charge utile de l’action de carte.</span><span class="sxs-lookup"><span data-stu-id="c256d-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="c256d-132">Chaque compétence doit être incorporer `skillId` dans le champ des actions de  `value` carte.</span><span class="sxs-lookup"><span data-stu-id="c256d-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="c256d-133">Il s’agit de la meilleure façon de s’assurer que chaque activité d’action de carte porte les informations de compétence pertinentes et que l’Assistant virtuel peut utiliser ces informations pour la distribution.</span><span class="sxs-lookup"><span data-stu-id="c256d-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="c256d-134">Vous trouverez ci-dessous un exemple de données d’action de carte.</span><span class="sxs-lookup"><span data-stu-id="c256d-134">Below is a card action data sample.</span></span> <span data-ttu-id="c256d-135">En fournissant dans le constructeur, nous nous assurons que les informations de compétences `skillId` sont toujours présentes dans les actions de carte.</span><span class="sxs-lookup"><span data-stu-id="c256d-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="c256d-136">Ensuite, nous introduisons la classe dans le modèle Assistant virtuel à `SkillCardActionData` extraire `skillId` de la charge utile d’action de carte.</span><span class="sxs-lookup"><span data-stu-id="c256d-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="c256d-137">Voici un extrait de code à extraire des  `skillId` données d’action de carte.</span><span class="sxs-lookup"><span data-stu-id="c256d-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="c256d-138">Nous l’avons implémentée en tant que méthode d’extension dans la [classe Activity.](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)</span><span class="sxs-lookup"><span data-stu-id="c256d-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="c256d-139">Gérer les interruptions de manière normale</span><span class="sxs-lookup"><span data-stu-id="c256d-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="c256d-140">L’Assistant virtuel peut gérer les interruptions lorsqu’un utilisateur tente d’invoquer une compétence alors qu’une autre compétence est active.</span><span class="sxs-lookup"><span data-stu-id="c256d-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="c256d-141">nous avons introduit et, sur la base de `TeamsSkillDialog` `TeamsSwitchSkillDialog` [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) et [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de Bot Framework, pour permettre aux utilisateurs de basculer une expérience de compétence à partir d’actions de carte.</span><span class="sxs-lookup"><span data-stu-id="c256d-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="c256d-142">Pour gérer cette demande, l’Assistant virtuel invite l’utilisateur à transmettre un message de confirmation pour changer de compétences.</span><span class="sxs-lookup"><span data-stu-id="c256d-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![Invite de confirmation lors du passage à une nouvelle compétence](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="c256d-144">Gestion des demandes de module de tâche</span><span class="sxs-lookup"><span data-stu-id="c256d-144">Handling task module requests</span></span>

<span data-ttu-id="c256d-145">Pour ajouter des fonctionnalités de module de tâche à un Assistant virtuel, deux méthodes supplémentaires sont incluses dans le handler d’activité de l’Assistant virtuel : `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="c256d-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="c256d-146">Ces méthodes écoutent les activités liées au module de tâche à partir de l’Assistant virtuel, identifient les compétences associées à la demande et la forwardent à la compétence identifiée.</span><span class="sxs-lookup"><span data-stu-id="c256d-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="c256d-147">Le forwarding de demande est effectué via  [la méthode SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable) `PostActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="c256d-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable), `PostActivityAsync` method.</span></span> <span data-ttu-id="c256d-148">Elle renvoie la réponse telle `InvokeResponse` qu’elle est l’une des deux. `TaskModuleResponse`</span><span class="sxs-lookup"><span data-stu-id="c256d-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="c256d-149">Une approche similaire est suivie pour la distribution des actions de carte et les réponses de module de tâche.</span><span class="sxs-lookup"><span data-stu-id="c256d-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="c256d-150">Les données d’action d’extraction et d’soumission du module de tâche sont mises à jour pour inclure `skillId` .</span><span class="sxs-lookup"><span data-stu-id="c256d-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="c256d-151">La méthode d’extension d’activité extrait de la charge utile qui fournit des détails sur les compétences qui `GetSkillId` `skillId` doivent être invoquées.</span><span class="sxs-lookup"><span data-stu-id="c256d-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="c256d-152">Vous trouverez ci-dessous un extrait de code pour `OnTeamsTaskModuleFetchAsync` les `OnTeamsTaskModuleSubmitAsync` méthodes.</span><span class="sxs-lookup"><span data-stu-id="c256d-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="c256d-153">En outre, tous les domaines de compétence doivent être inclus dans la section du fichier manifeste de l’Assistant virtuel afin que les modules de tâche appelés via une compétence `validDomains` s’effectuent correctement.</span><span class="sxs-lookup"><span data-stu-id="c256d-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="c256d-154">Gestion des étendues d’application collaborative</span><span class="sxs-lookup"><span data-stu-id="c256d-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="c256d-155">Les applications Teams peuvent exister dans plusieurs étendues, y compris la conversation 1:1, la conversation de groupe et les canaux.</span><span class="sxs-lookup"><span data-stu-id="c256d-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="c256d-156">Le modèle d’Assistant virtuel principal est conçu pour les conversations 1:1.</span><span class="sxs-lookup"><span data-stu-id="c256d-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="c256d-157">Dans le cadre de l’expérience d’intégration, l’Assistant virtuel invite les utilisateurs à nommer et maintient l’état de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c256d-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="c256d-158">Étant donné que cette expérience d’intégration n’est pas adaptée aux étendues de conversation de groupe/canal, elle a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="c256d-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="c256d-159">Les compétences doivent gérer les activités dans plusieurs étendues (conversation 1:1, conversation de groupe et conversation de canal).</span><span class="sxs-lookup"><span data-stu-id="c256d-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="c256d-160">Si l’une de ces étendues n’est pas prise en charge, les compétences doivent répondre par un message approprié.</span><span class="sxs-lookup"><span data-stu-id="c256d-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="c256d-161">Les fonctions de traitement suivantes ont été ajoutées au cœur de l’Assistant virtuel :</span><span class="sxs-lookup"><span data-stu-id="c256d-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="c256d-162">L’Assistant virtuel peut être appelé sans message texte d’une conversation de groupe ou d’un canal.</span><span class="sxs-lookup"><span data-stu-id="c256d-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="c256d-163">Les robots sont nettoyés (c’est-à-dire, suppriment les @mention nécessaires du bot) avant d’envoyer le message au module de distribution.</span><span class="sxs-lookup"><span data-stu-id="c256d-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="c256d-164">Gestion des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="c256d-164">Handling messaging extensions</span></span>

<span data-ttu-id="c256d-165">Les commandes d’une extension de messagerie sont déclarées dans le fichier manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="c256d-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="c256d-166">L’interface utilisateur de l’extension de messagerie est optimisée par ces commandes.</span><span class="sxs-lookup"><span data-stu-id="c256d-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="c256d-167">Pour qu’un Assistant virtuel soit en mesure d’alimenter une commande d’extension de messagerie (en tant que compétence jointe), le manifeste d’un Assistant virtuel doit contenir ces commandes.</span><span class="sxs-lookup"><span data-stu-id="c256d-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="c256d-168">Les commandes du manifeste d’une compétence individuelle doivent également être ajoutées au manifeste de l’Assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="c256d-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="c256d-169">L’ID de commande fournit des informations sur une compétence associée en axant l’ID d’application de la compétence via un séparateur ( `:` ).</span><span class="sxs-lookup"><span data-stu-id="c256d-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="c256d-170">Vous trouverez ci-dessous un extrait du fichier manifeste d’une compétence.</span><span class="sxs-lookup"><span data-stu-id="c256d-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="c256d-171">Vous trouverez ci-dessous l’extrait de code du fichier manifeste de l’Assistant virtuel correspondant.</span><span class="sxs-lookup"><span data-stu-id="c256d-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="c256d-172">Une fois que les commandes sont invoquées par un utilisateur, l’Assistant virtuel peut identifier une compétence associée en parant l’ID de commande, mettre à jour l’activité en supprimant le suffixe supplémentaire ( ) de l’ID de commande et le faire suivre à la compétence `:<skill_id>` correspondante.</span><span class="sxs-lookup"><span data-stu-id="c256d-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="c256d-173">Le code d’une compétence n’a pas besoin de gérer le suffixe supplémentaire. Par conséquent, les conflits entre les ID de commande entre les compétences sont évités.</span><span class="sxs-lookup"><span data-stu-id="c256d-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="c256d-174">Avec cette approche, toutes les commandes de recherche et d’action d’une compétence dans tous les contextes (« compose », « commandBox » et « message ») peuvent être optimisées par un Assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="c256d-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="c256d-175">Certaines activités d’extension de messagerie n’incluent pas l’ID de commande.</span><span class="sxs-lookup"><span data-stu-id="c256d-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="c256d-176">Par exemple, `composeExtension/selectItem` contient uniquement la valeur de l’action d’appel d’appel.</span><span class="sxs-lookup"><span data-stu-id="c256d-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="c256d-177">Pour identifier les compétences associées, est attaché à chaque carte `skillId`  d’élément lors de la formation d’une réponse pour `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="c256d-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="c256d-178">(Cette approche est similaire à l’ajout de cartes [adaptatives à votre Assistant virtuel.](#add-adaptive-cards-to-your-virtual-assistant)</span><span class="sxs-lookup"><span data-stu-id="c256d-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="c256d-179">Exemple : convertir le modèle d’application « Livrer une salle » en compétence Assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="c256d-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="c256d-180">[Book-a-room](app-templates.md#book-a-room) est un [bot Microsoft Teams](../bots/what-are-bots.md) qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pendant 30 (par défaut), 60 ou 90 minutes à partir de l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="c256d-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="c256d-181">Le bot Book-a-room s’étendue à des conversations personnelles ou 1:1.</span><span class="sxs-lookup"><span data-stu-id="c256d-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![Assistant virtuel avec compétence « Réserver une salle »](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="c256d-183">Voici les modifications delta introduites pour la convertir en une compétence qui peut être jointe à un Assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="c256d-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="c256d-184">Des instructions similaires peuvent être suivies pour convertir n’importe quel bot v4 existant en une compétence.</span><span class="sxs-lookup"><span data-stu-id="c256d-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="c256d-185">Manifeste de compétences</span><span class="sxs-lookup"><span data-stu-id="c256d-185">Skill manifest</span></span>

<span data-ttu-id="c256d-186">Un manifeste de compétences est un fichier JSON qui expose le point de terminaison de messagerie, l’ID, le nom et d’autres métadonnées pertinentes d’une compétence (ce manifeste est différent du manifeste utilisé pour le chargement d’une application dans Microsoft Teams) Un Assistant virtuel requiert un chemin d’accès à ce fichier comme entrée pour joindre une compétence.</span><span class="sxs-lookup"><span data-stu-id="c256d-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="c256d-187">Nous avons ajouté le manifeste suivant au dossier wwwroot du bot.</span><span class="sxs-lookup"><span data-stu-id="c256d-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="c256d-188">Intégration LUIS</span><span class="sxs-lookup"><span data-stu-id="c256d-188">LUIS Integration</span></span>

<span data-ttu-id="c256d-189">Le modèle de distribution de l’Assistant virtuel est construit sur les modèles LUIS des compétences jointes.</span><span class="sxs-lookup"><span data-stu-id="c256d-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="c256d-190">Le modèle de distribution identifie l’intention de chaque activité de texte et détecte les compétences qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="c256d-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="c256d-191">L’Assistant virtuel nécessite le modèle LUIS des compétences (dans le format) en tant qu’entrée lors de `.lu` l’attachement d’une compétence.</span><span class="sxs-lookup"><span data-stu-id="c256d-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="c256d-192">Le json LUIS peut être converti au format à l’aide de `.lu` l’outil botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="c256d-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="c256d-193">Le bot book-a-room dispose de deux commandes principales pour les utilisateurs :</span><span class="sxs-lookup"><span data-stu-id="c256d-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="c256d-194">Nous avons créé un modèle LUIS comprenant ces deux commandes.</span><span class="sxs-lookup"><span data-stu-id="c256d-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="c256d-195">Les secrets correspondants doivent être remplies dans `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="c256d-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="c256d-196">Le fichier LUIS JSON correspondant se trouve [ici](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) et voici à quoi ressemble `.lu` le fichier correspondant.</span><span class="sxs-lookup"><span data-stu-id="c256d-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="c256d-197">Avec cette approche, tous les problèmes de commande d’un utilisateur à l’Assistant virtuel liés à ou peuvent être identifiés comme une commande associée au bot de salle de réservation sont transmis à `book room` `manage favorites` cette compétence.</span><span class="sxs-lookup"><span data-stu-id="c256d-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="c256d-198">En revanche, le bot de salle de réservation doit utiliser le modèle LUIS pour comprendre ces commandes s’ils ne sont pas tapés tels quel (par exemple : `I want to manage my favorite rooms` ).</span><span class="sxs-lookup"><span data-stu-id="c256d-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="c256d-199">Prise en charge multi-langue</span><span class="sxs-lookup"><span data-stu-id="c256d-199">Multi-Language support</span></span>

<span data-ttu-id="c256d-200">Pour cet exemple, nous avons uniquement créé un modèle LUIS avec culture anglaise.</span><span class="sxs-lookup"><span data-stu-id="c256d-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="c256d-201">Vous pouvez créer des modèles LUIS correspondant à d’autres langues et ajouter une entrée à `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="c256d-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="c256d-202">En parallèle, ajoutez le `.lu` fichier correspondant dans le chemin luisFolder.</span><span class="sxs-lookup"><span data-stu-id="c256d-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="c256d-203">La structure des dossiers doit être la suivante :</span><span class="sxs-lookup"><span data-stu-id="c256d-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="c256d-204">Mettez à jour la commande botskills comme suit pour modifier le `languages` paramètre :</span><span class="sxs-lookup"><span data-stu-id="c256d-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="c256d-205">L’Assistant virtuel `SetLocaleMiddleware` utilise pour identifier les paramètres régionaux actuels et appeler le modèle de distribution correspondant.</span><span class="sxs-lookup"><span data-stu-id="c256d-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="c256d-206">(L’activité bot framework possède un champ de paramètres régionaux qui est utilisé par cet intermédiaire.) Nous vous recommandons également d’utiliser la même technique pour vos compétences.</span><span class="sxs-lookup"><span data-stu-id="c256d-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="c256d-207">Le bot book-a-room n’utilise pas cet middleware et obtient à la place les paramètres régionaux de l’entité [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de l’activité Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c256d-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="c256d-208">Validation des revendications</span><span class="sxs-lookup"><span data-stu-id="c256d-208">Claim validation</span></span>

<span data-ttu-id="c256d-209">Nous avons ajouté [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) pour limiter les appelants à la compétence.</span><span class="sxs-lookup"><span data-stu-id="c256d-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="c256d-210">Pour permettre à un Assistant virtuel d’appeler cette compétence, remplir le tableau à partir de `AllowedCallers` `appsettings` l’ID d’application de cet Assistant virtuel particulier.</span><span class="sxs-lookup"><span data-stu-id="c256d-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="c256d-211">Le tableau des appelants autorisés peut restreindre les compétences que les consommateurs peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="c256d-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="c256d-212">Ajoutez une entrée `*` unique à ce tableau, pour accepter les appels de n’importe quel consommateur de compétences.</span><span class="sxs-lookup"><span data-stu-id="c256d-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="c256d-213">Vous pouvez trouver ici une documentation détaillée sur l’ajout de la validation des revendications à une [compétence.](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)</span><span class="sxs-lookup"><span data-stu-id="c256d-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="c256d-214">Limitation de l’actualisation de la carte</span><span class="sxs-lookup"><span data-stu-id="c256d-214">Card refresh limitation</span></span>

<span data-ttu-id="c256d-215">La mise à jour de l’activité (actualisation de la carte) n’est pas encore prise en charge via l’Assistant[virtuel (problème github).](https://github.com/microsoft/botbuilder-dotnet/issues/3686)</span><span class="sxs-lookup"><span data-stu-id="c256d-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="c256d-216">Par conséquent, nous avons remplacé tous les appels d’actualisation de carte ( `UpdateActivityAsync` ) par la publication de nouveaux appels de carte( `SendActivityAsync` ).</span><span class="sxs-lookup"><span data-stu-id="c256d-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="c256d-217">Actions de carte et flux de module de tâche</span><span class="sxs-lookup"><span data-stu-id="c256d-217">Card actions and task module flows</span></span>

<span data-ttu-id="c256d-218">Pour qu’une action de carte ou des activités de module de tâche soit transmis à une compétence associée, cette compétence doit y `skillId` être incorporer.</span><span class="sxs-lookup"><span data-stu-id="c256d-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="c256d-219">Les charges utiles d’action d’extraction et d’soumission de module de tâche sont modifiées pour contenir `skillId` en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="c256d-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="c256d-220">Pour plus d’informations, [reportez-vous](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) à cette section de cette documentation.</span><span class="sxs-lookup"><span data-stu-id="c256d-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="c256d-221">Gérer les activités à partir d’une conversation de groupe ou d’une étendue de canal</span><span class="sxs-lookup"><span data-stu-id="c256d-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="c256d-222">Le bot book-a-room est conçu pour les conversations privées (étendue personnelle/1:1) uniquement.</span><span class="sxs-lookup"><span data-stu-id="c256d-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="c256d-223">Étant donné que nous avons personnalisé l’Assistant virtuel pour prendre en charge les étendues de conversation de groupe et de canal, l’Assistant virtuel peut être appelé à partir de ces étendues et par conséquent, le bot de réservation de salle peut obtenir des activités pour la même.</span><span class="sxs-lookup"><span data-stu-id="c256d-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="c256d-224">Par conséquent, le bot « Book-a-room » est personnalisé pour gérer ces activités.</span><span class="sxs-lookup"><span data-stu-id="c256d-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="c256d-225">La vérification a été mise en place dans des méthodes de traitement des activités du `OnMessageActivityAsync` bot Book-a-room.</span><span class="sxs-lookup"><span data-stu-id="c256d-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="c256d-226">Vous pouvez également tirer parti des compétences existantes du référentiel [de solutions Bot Framework](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) ou créer une compétence entièrement à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="c256d-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="c256d-227">Vous pouvez trouver des didacticiels pour la suite [ici.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="c256d-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="c256d-228">Reportez-vous à [la documentation relative](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   à l’Assistant virtuel et à l’architecture des compétences.</span><span class="sxs-lookup"><span data-stu-id="c256d-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   for Virtual Assistant and skills architecture.</span></span>

## <a name="sample-code-to-get-started"></a><span data-ttu-id="c256d-229">Exemple de code pour commencer</span><span class="sxs-lookup"><span data-stu-id="c256d-229">Sample code to get started</span></span>

- [<span data-ttu-id="c256d-230">Modèle Visual Studio mis à jour</span><span class="sxs-lookup"><span data-stu-id="c256d-230">Updated visual studio template</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [<span data-ttu-id="c256d-231">Code de compétences pour un bot dans une salle</span><span class="sxs-lookup"><span data-stu-id="c256d-231">Book-a-room bot skill code</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="c256d-232">Limitations connues de l’Assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="c256d-232">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="c256d-233">**EndOfConversation**.</span><span class="sxs-lookup"><span data-stu-id="c256d-233">**EndOfConversation**.</span></span> <span data-ttu-id="c256d-234">Une compétence doit envoyer une `endOfConversation` activité à la fin d’une conversation.</span><span class="sxs-lookup"><span data-stu-id="c256d-234">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="c256d-235">sur la base de cette activité, un Assistant virtuel met fin au contexte avec cette compétence particulière et revient dans le contexte (racine) de l’Assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="c256d-235">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="c256d-236">Pour le bot Book-a-room, il n’existe aucun état clair dans lequel la conversation peut être terminée.</span><span class="sxs-lookup"><span data-stu-id="c256d-236">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="c256d-237">Par conséquent, nous n’avons pas envoyé à partir du `endOfConversation` bot Book-a-room et lorsque l’utilisateur souhaite revenir au contexte racine, il peut simplement le faire par `start over` commande.</span><span class="sxs-lookup"><span data-stu-id="c256d-237">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="c256d-238">**Actualisation de la carte.**</span><span class="sxs-lookup"><span data-stu-id="c256d-238">**Card refresh**.</span></span> <span data-ttu-id="c256d-239">Les actualisations de carte ne sont pas encore pris en charge via l’Assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="c256d-239">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="c256d-240">**Extensions de messagerie**::</span><span class="sxs-lookup"><span data-stu-id="c256d-240">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="c256d-241">Actuellement, un Assistant virtuel peut prendre en charge un maximum de dix commandes pour les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="c256d-241">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="c256d-242">La configuration des extensions de messagerie n’est pas limitée aux commandes individuelles, mais à l’ensemble de l’extension elle-même.</span><span class="sxs-lookup"><span data-stu-id="c256d-242">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="c256d-243">Cela limite la configuration de chaque compétence individuelle par le biais de l’Assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="c256d-243">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="c256d-244">Les ID de commande des extensions de messagerie ont une longueur maximale de [64](../resources/schema/manifest-schema.md#composeextensions) caractères et 37 caractères sont utilisés pour incorporer des informations de compétences.</span><span class="sxs-lookup"><span data-stu-id="c256d-244">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="c256d-245">Par conséquent, les contraintes mises à jour pour l’ID de commande sont limitées à 27 caractères.</span><span class="sxs-lookup"><span data-stu-id="c256d-245">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
