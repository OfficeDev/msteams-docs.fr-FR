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
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="8f7d4-104">Assistant virtuel pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="8f7d4-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="8f7d4-105">Virtual Assistant est un modèle de source ouverte Microsoft qui vous permet de créer une solution de conversation robuste tout en conservant un contrôle total de l’expérience utilisateur, de la personnalisation de l’organisation et des données nécessaires.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="8f7d4-106">Le [modèle de base de l’assistant virtuel](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) est le bloc de construction de base qui rassemble les technologies Microsoft nécessaires à la création d’un assistant virtuel, notamment le [Kit de développement logiciel (SDK](https://github.com/microsoft/botframework-sdk)) de robot, le mémorandum d’accord de [langue (Luis)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), ainsi que les fonctionnalités essentielles, notamment l’enregistrement des compétences, les comptes liés, l’intention de conversation de base pour offrir aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8f7d4-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="8f7d4-107">En outre, les fonctionnalités de modèle incluent des exemples enrichis de [compétences](https://microsoft.github.io/botframework-solutions/overview/skills)de conversation réutilisables.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="8f7d4-108">Les compétences individuelles peuvent être intégrées dans une solution assistant virtuel pour permettre plusieurs scénarios.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="8f7d4-109">À l’aide du kit de développement logiciel (SDK) de robot, les compétences sont présentées sous forme de code source, ce qui vous permet de personnaliser et d’étendre les besoins.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="8f7d4-110">Voir [What is a bot Framework Skills](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![Diagramme de vue d’ensemble de l’assistant virtuel](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="8f7d4-112">Les activités de message texte sont acheminées vers les compétences associées par le noyau de l’assistant virtuel à l’aide d’un modèle de [répartition](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="8f7d4-113">Considérations relatives à l’implémentation</span><span class="sxs-lookup"><span data-stu-id="8f7d4-113">Implementation considerations</span></span>

<span data-ttu-id="8f7d4-114">La décision d’ajouter un assistant virtuel peut inclure de nombreux déterminants et diffère pour chaque organisation.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="8f7d4-115">Voici les facteurs qui prennent en charge l’implémentation d’un assistant virtuel pour votre organisation :</span><span class="sxs-lookup"><span data-stu-id="8f7d4-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="8f7d4-116">Une équipe centrale gère toutes les expériences des employés et offre la possibilité de créer une expérience de l’assistant virtuel et de gérer les mises à jour de l’expérience principale, y compris l’ajout de nouvelles compétences.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="8f7d4-117">Il existe plusieurs applications pour les fonctions professionnelles et/ou le nombre devrait augmenter à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="8f7d4-118">Les applications existantes sont personnalisables, détenues par l’organisation et peuvent être converties en compétences pour un assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="8f7d4-119">L’équipe centrale employés-expériences peut influencer les personnalisations apportées aux applications existantes et fournir les instructions nécessaires pour intégrer les applications existantes en tant que compétences dans l’expérience de l’assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="8f7d4-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![L’équipe centrale gère l’Assistant et les compétences de Team Function Teams.](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="8f7d4-121">Créer un assistant virtuel centré sur teams</span><span class="sxs-lookup"><span data-stu-id="8f7d4-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="8f7d4-122">Microsoft a publié un [modèle Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) pour créer des assistants virtuels et des compétences.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="8f7d4-123">Avec le modèle Visual Studio, vous pouvez créer un assistant virtuel, alimenté par une expérience basée sur le texte avec prise en charge de cartes riches limitées avec des actions.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="8f7d4-124">Nous avons amélioré le modèle de base Visual Studio pour inclure les fonctionnalités de la plateforme Microsoft teams et les expériences de l’application Power Great Teams.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="8f7d4-125">Quelques-unes des fonctionnalités incluent la prise en charge de cartes adaptatives riches, de modules de tâches, d’équipes/de conversations de groupes et d’extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="8f7d4-126">*Voir aussi* [Tutorial : étendre votre assistant virtuel à Microsoft teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![Diagramme de haut niveau d’une solution d’assistant virtuel](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="8f7d4-128">Ajouter des cartes adaptatives à votre assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="8f7d4-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="8f7d4-129">Pour distribuer les demandes correctement, votre assistant virtuel doit identifier le modèle LUIS correct et les compétences correspondantes associées.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="8f7d4-130">Toutefois, le mécanisme de répartition ne peut pas être utilisé pour les activités d’action de carte étant donné que le modèle LUIS associé à une compétence ne peut pas être formé pour les textes d’action de carte, car il s’agit de mots clés prédéfinis et non d’énoncés d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="8f7d4-131">Nous avons résolu cela en incorporant des informations sur les compétences dans la charge utile d’action de la carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="8f7d4-132">Toutes les compétences doivent être incorporées `skillId` dans le `value` champ des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="8f7d4-133">Il s’agit de la meilleure façon de vous assurer que chaque activité d’action de carte véhicule les informations de compétences pertinentes et que l’assistant virtuel peut utiliser ces informations pour la distribution.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="8f7d4-134">Vous trouverez ci-dessous un exemple de données d’action de carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-134">Below is a card action data sample.</span></span> <span data-ttu-id="8f7d4-135">En fournissant `skillId` dans le constructeur, nous nous assurons que les informations sur les compétences sont toujours présentes dans les actions de carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="8f7d4-136">Ensuite, nous introduisons `SkillCardActionData` la classe dans le modèle de l’assistant virtuel pour extraire `skillId` de la charge utile de la carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="8f7d4-137">Vous trouverez ci-dessous un extrait de code pour extraire `skillId` des données d’action de carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="8f7d4-138">Nous l’avons implémentée en tant que méthode d’extension dans la classe [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="8f7d4-139">Gérer les interruptions de manière appropriée</span><span class="sxs-lookup"><span data-stu-id="8f7d4-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="8f7d4-140">L’assistant virtuel peut gérer les interruptions lorsqu’un utilisateur tente d’appeler une compétence alors qu’une autre compétence est actuellement active.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="8f7d4-141">Nous avons introduit `TeamsSkillDialog` et `TeamsSwitchSkillDialog` , en se basant sur les [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) et [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)de l’infrastructure bot, pour permettre aux utilisateurs de changer une expérience de compétences à partir d’actions de carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="8f7d4-142">Pour gérer cette demande, l’assistant virtuel invite l’utilisateur à indiquer un message de confirmation pour faire basculer les compétences.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![Invite de confirmation lors du basculement vers une nouvelle qualification](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="8f7d4-144">Gestion des demandes de module de tâche</span><span class="sxs-lookup"><span data-stu-id="8f7d4-144">Handling task module requests</span></span>

<span data-ttu-id="8f7d4-145">Pour ajouter des fonctionnalités de module de tâches à un assistant virtuel, deux méthodes supplémentaires sont incluses dans le gestionnaire d’activités de l’Assistant Virtual : `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="8f7d4-146">Ces méthodes écoutent les activités liées au module de tâche à partir de l’assistant virtuel, identifient les compétences associées à la demande et transfèrent la demande à la compétence identifiée.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="8f7d4-147">Le transfert des demandes est réalisé via la méthode [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable) `PostActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable), `PostActivityAsync` method.</span></span> <span data-ttu-id="8f7d4-148">Elle renvoie la réponse telle qu’elle `InvokeResponse` est analysée et convertie en `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="8f7d4-149">Une approche similaire est suivie pour les réponses de module de tâche et de distribution d’action de carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="8f7d4-150">Les données d’action d’extraction et d’envoi du module tâches sont mises à jour pour inclure `skillId` .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="8f7d4-151">`GetSkillId`La méthode d’extension d’activité extrait `skillId` de la charge utile, qui fournit des détails sur les compétences qui doivent être appelées.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="8f7d4-152">Vous trouverez ci-dessous un extrait de code pour `OnTeamsTaskModuleFetchAsync` et des `OnTeamsTaskModuleSubmitAsync` méthodes.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="8f7d4-153">De plus, tous les domaines de compétences doivent être inclus dans la `validDomains` section du fichier manifeste de l’assistant virtuel afin que les modules de tâches appelés via un rendu de compétences soient correctement affichés.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="8f7d4-154">Gestion des étendues d’applications collaboratives</span><span class="sxs-lookup"><span data-stu-id="8f7d4-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="8f7d4-155">Les applications teams peuvent exister dans plusieurs étendues, y compris la conversation de 1:1, la conversation de groupe et les canaux.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="8f7d4-156">Le modèle de l’assistant virtuel principal est conçu pour les conversations de 1:1.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="8f7d4-157">Dans le cadre de l’Assistant Virtual expérience d’intégration, l’assistant virtuel invite les utilisateurs à fournir un nom et gère l’état de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="8f7d4-158">Étant donné que cette expérience d’intégration n’est pas adaptée aux étendues de conversation de groupe/canal, elle a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="8f7d4-159">Les compétences doivent gérer les activités dans plusieurs étendues (1:1 chat, conversation de groupe et conversation de canal).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="8f7d4-160">Si l’une de ces étendues n’est pas prise en charge, les compétences doivent répondre avec un message approprié.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="8f7d4-161">Les fonctions de traitement suivantes ont été ajoutées à Virtual Assistant Core :</span><span class="sxs-lookup"><span data-stu-id="8f7d4-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="8f7d4-162">L’assistant virtuel peut être appelé sans aucun message texte provenant d’une conversation ou d’un canal de groupe.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="8f7d4-163">Les articulations sont nettoyées (autrement dit, supprimez les @mention nécessaires du bot) avant d’envoyer le message au module de répartition.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="8f7d4-164">Gestion des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="8f7d4-164">Handling messaging extensions</span></span>

<span data-ttu-id="8f7d4-165">Les commandes pour une extension de messagerie sont déclarées dans le fichier manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="8f7d4-166">L’interface utilisateur de l’extension de messagerie est gérée par ces commandes.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="8f7d4-167">Pour qu’un assistant virtuel alimente une commande d’extension de messagerie (en tant que compétence attachée), le propre manifeste d’un assistant virtuel doit contenir ces commandes.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="8f7d4-168">Les commandes du manifeste d’une compétence individuelle doivent également être ajoutées au manifeste de l’assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="8f7d4-169">L’ID de commande fournit des informations sur une compétence associée en ajoutant l’ID de l’application de la compétence via un séparateur ( `:` ).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="8f7d4-170">Vous trouverez ci-dessous un extrait du fichier manifeste d’une compétence.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="8f7d4-171">Et, ci-dessous, l’extrait de code du fichier de manifeste de l’assistant virtuel correspondant.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="8f7d4-172">Une fois que les commandes sont appelées par un utilisateur, l’assistant virtuel peut identifier une compétence associée en analysant l’ID de commande, mettre à jour l’activité en supprimant le suffixe supplémentaire ( `:<skill_id>` ) de l’ID de commande et le transférer à la compétence correspondante.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="8f7d4-173">Le code d’une compétence n’a pas besoin de gérer le suffixe supplémentaire, de sorte que les conflits entre les ID de commande entre les compétences sont évités.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="8f7d4-174">Avec cette approche, toutes les commandes de recherche et d’action d’une compétence dans tous les contextes (« composition », « commandBox » et « message ») peuvent être gérées par un assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="8f7d4-175">Certaines activités d’extension de messagerie n’incluent pas l’ID de commande.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="8f7d4-176">Par exemple, `composeExtension/selectItem` contient uniquement la valeur de l’action appeler le TAP.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="8f7d4-177">Pour identifier la compétence associée, `skillId` est joint à chaque fiche d’article tout en formant une réponse à `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="8f7d4-178">(Cette méthode est similaire à celle permettant d' [Ajouter des cartes adaptatives à votre assistant virtuel](#add-adaptive-cards-to-your-virtual-assistant).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="8f7d4-179">Exemple : convertir le modèle d’application livre-a-Room en habiletés de l’assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="8f7d4-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="8f7d4-180">[Book-a-room](app-templates.md#book-a-room) est un [robot Microsoft teams](../bots/what-are-bots.md) qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pour 30 (par défaut), 60 ou 90 minutes à compter de l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="8f7d4-181">Les étendues de bot livre-a-room aux conversations personnelles ou 1:1.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![Assistant virtuel avec une compétence « réserver une salle »](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="8f7d4-183">Les éléments suivants sont les modifications Delta introduites pour les convertir en une compétence qui peut être associée à un assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="8f7d4-184">Des instructions similaires peuvent être suivies pour convertir tout robot v4 existant en compétences.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="8f7d4-185">Manifeste de compétences</span><span class="sxs-lookup"><span data-stu-id="8f7d4-185">Skill manifest</span></span>

<span data-ttu-id="8f7d4-186">Un manifeste de compétences est un fichier JSON qui expose un point de terminaison de messagerie, un ID, un nom et d’autres métadonnées pertinentes (ce manifeste est différent du manifeste utilisé pour chargement une application dans Microsoft Teams) un assistant virtuel requiert un chemin d’accès à ce fichier comme entrée pour joindre une compétence.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="8f7d4-187">Nous avons ajouté le manifeste suivant au dossier Wwwroot du bot.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="8f7d4-188">Intégration de LUIS</span><span class="sxs-lookup"><span data-stu-id="8f7d4-188">LUIS Integration</span></span>

<span data-ttu-id="8f7d4-189">Le modèle de répartition de l’assistant virtuel est basé sur les modèles LUIS des compétences attachées.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="8f7d4-190">Le modèle de répartition identifie l’intention pour chaque activité de texte et Découvre les compétences associées.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="8f7d4-191">L’assistant virtuel nécessite le modèle LUIS de compétences (au `.lu` format) en tant qu’entrée lors de l’attachement d’une compétence.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="8f7d4-192">Le format JSON LUIS peut être converti en `.lu` format à l’aide de l’outil botframework-CLI.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="8f7d4-193">Book-a-room bot dispose de deux commandes principales pour les utilisateurs :</span><span class="sxs-lookup"><span data-stu-id="8f7d4-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="8f7d4-194">Nous avons créé un modèle LUIS qui comprenne ces deux commandes.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="8f7d4-195">Les secrets correspondants doivent être renseignés `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="8f7d4-196">Vous trouverez [ici](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) le fichier JSON Luis correspondant, ainsi que l' `.lu` apparence du fichier correspondant.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="8f7d4-197">Dans le cadre de cette approche, les commandes émises par un utilisateur vers un assistant virtuel lié à `book room` ou `manage favorites` peuvent être identifiées en tant que commandes associées à un bot livre-a-room et sont transmises à cette compétence.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="8f7d4-198">En revanche, livre-a-room main bot doit utiliser le modèle LUIS pour comprendre ces commandes s’ils ne sont pas tapés tels quels (par exemple : `I want to manage my favorite rooms` ).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="8f7d4-199">Prise en charge de plusieurs langues</span><span class="sxs-lookup"><span data-stu-id="8f7d4-199">Multi-Language support</span></span>

<span data-ttu-id="8f7d4-200">Pour cet exemple, nous avons créé uniquement un modèle LUIS avec une culture en anglais.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="8f7d4-201">Vous pouvez créer des modèles LUIS correspondant à d’autres langages et ajouter une entrée à `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="8f7d4-202">En parallèle, ajoutez le `.lu` fichier correspondant dans le chemin d’accès luisFolder.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="8f7d4-203">La structure de dossiers doit être la suivante :</span><span class="sxs-lookup"><span data-stu-id="8f7d4-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="8f7d4-204">Mettez à jour la commande botskills comme suit pour modifier le `languages` paramètre :</span><span class="sxs-lookup"><span data-stu-id="8f7d4-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="8f7d4-205">L’assistant virtuel utilise `SetLocaleMiddleware` pour identifier les paramètres régionaux en cours et appeler le modèle de répartition correspondant.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="8f7d4-206">(L’activité de l’infrastructure bot a un champ de paramètres régionaux utilisé par ce middleware.) Nous vous recommandons également d’utiliser le même pour vos compétences.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="8f7d4-207">Book-a-room bot n’utilise pas ce middleware et obtient à la place des paramètres régionaux de l' [entité clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)de l’activité de l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="8f7d4-208">Validation de revendication</span><span class="sxs-lookup"><span data-stu-id="8f7d4-208">Claim validation</span></span>

<span data-ttu-id="8f7d4-209">Nous avons ajouté [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) pour restreindre les appelants à la compétence.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="8f7d4-210">Pour permettre à un assistant virtuel d’appeler cette qualification, renseignez le `AllowedCallers` tableau à `appsettings` l’aide de l’ID d’application de cet assistant virtuel particulier.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="8f7d4-211">Le tableau des appelants autorisés peut restreindre les compétences auxquelles les consommateurs peuvent accéder.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="8f7d4-212">Ajoutez une entrée unique `*` à ce tableau pour accepter les appels de tous les consommateurs de compétences.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="8f7d4-213">Vous trouverez [ici](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)une documentation détaillée sur l’ajout de la validation des revendications à une compétence.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="8f7d4-214">Limitation de l’actualisation de la carte</span><span class="sxs-lookup"><span data-stu-id="8f7d4-214">Card refresh limitation</span></span>

<span data-ttu-id="8f7d4-215">L’activité de mise à jour (actualisation de carte) n’est pas encore prise en charge via l’assistant virtuel ([problème GitHub](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="8f7d4-216">Par conséquent, nous avons remplacé tous les appels d’actualisation de carte ( `UpdateActivityAsync` ) par la publication de nouveaux appels de carte ( `SendActivityAsync` ).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="8f7d4-217">Actions de carte et flux de module de tâches</span><span class="sxs-lookup"><span data-stu-id="8f7d4-217">Card actions and task module flows</span></span>

<span data-ttu-id="8f7d4-218">Pour transférer les activités d’une action de carte ou d’un module de tâche à une compétence associée, la compétence doit être incorporée `skillId` .</span><span class="sxs-lookup"><span data-stu-id="8f7d4-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="8f7d4-219">Action de la carte de robot de livre-a-room, le module de tâche FETCH and Submit action Payloads est modifié pour contenir `skillId` comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="8f7d4-220">Pour plus d’informations, reportez-vous à [cette](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section à partir de cette documentation.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="8f7d4-221">Gérer les activités à partir de la conversation de groupe ou de l’étendue de canal</span><span class="sxs-lookup"><span data-stu-id="8f7d4-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="8f7d4-222">Book-a-room bot est conçu pour les conversations privées (personnelles/1:1 étendue) uniquement.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="8f7d4-223">Étant donné que l’assistant virtuel personnalisé prend en charge la conversation de groupe et les étendues de canal, l’assistant virtuel peut être appelé à partir de ces étendues et, par conséquent, le bot livre-a-Room peut obtenir des activités pour le même.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="8f7d4-224">Par conséquent, le bot de livre-a-Room est personnalisé pour gérer ces activités.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="8f7d4-225">La vérification a été placée dans les `OnMessageActivityAsync` méthodes du gestionnaire d’activité livre-a-room.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="8f7d4-226">Vous pouvez également tirer parti des compétences existantes du [référentiel de solutions de robots](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) ou créer une nouvelle compétence entièrement complète.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="8f7d4-227">Vous trouverez des didacticiels pour les versions ultérieures [ici](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="8f7d4-228">Reportez-vous à [la documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0) pour l’assistant virtuel et l’architecture des compétences.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   for Virtual Assistant and skills architecture.</span></span>

## <a name="sample-code-to-get-started"></a><span data-ttu-id="8f7d4-229">Exemple de code pour commencer</span><span class="sxs-lookup"><span data-stu-id="8f7d4-229">Sample code to get started</span></span>

- [<span data-ttu-id="8f7d4-230">Modèle Visual Studio mis à jour</span><span class="sxs-lookup"><span data-stu-id="8f7d4-230">Updated visual studio template</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [<span data-ttu-id="8f7d4-231">Livre-code de compétences de robot a-room</span><span class="sxs-lookup"><span data-stu-id="8f7d4-231">Book-a-room bot skill code</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="8f7d4-232">Limitations connues de l’assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="8f7d4-232">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="8f7d4-233">**EndOfConversation**.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-233">**EndOfConversation**.</span></span> <span data-ttu-id="8f7d4-234">Une compétence doit envoyer une `endOfConversation` activité lorsqu’elle termine une conversation.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-234">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="8f7d4-235">Cette activité est basée sur cette activité, un assistant virtuel met fin au contexte avec cette compétence particulière et revient dans le contexte de l’assistant virtuel (racine).</span><span class="sxs-lookup"><span data-stu-id="8f7d4-235">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="8f7d4-236">Pour un bot livre-a-room, il n’existe pas d’État clair où la conversation peut être terminée.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-236">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="8f7d4-237">Par conséquent, nous n’avons pas envoyé `endOfConversation` de livre-a-room bot et lorsque l’utilisateur souhaite revenir au contexte racine, il peut simplement le faire par `start over` Command.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-237">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="8f7d4-238">**Actualisation**de la carte.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-238">**Card refresh**.</span></span> <span data-ttu-id="8f7d4-239">L’actualisation de la carte n’est pas encore prise en charge par l’assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-239">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="8f7d4-240">**Extensions de messagerie**:</span><span class="sxs-lookup"><span data-stu-id="8f7d4-240">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="8f7d4-241">À l’heure actuelle, un assistant virtuel peut prendre en charge un maximum de dix commandes pour les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-241">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="8f7d4-242">La configuration des extensions de messagerie n’est pas limitée aux commandes individuelles, mais pour l’intégralité de l’extension.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-242">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="8f7d4-243">Cela limite la configuration de chaque compétence par le biais de l’assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-243">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="8f7d4-244">Les ID de commande des extensions de messagerie ont une longueur maximale de [64 caractères](../resources/schema/manifest-schema.md#composeextensions) et 37 caractères seront utilisés pour incorporer des informations sur les compétences.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-244">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="8f7d4-245">Par conséquent, les contraintes mises à jour pour l’ID de commande sont limitées à 27 caractères.</span><span class="sxs-lookup"><span data-stu-id="8f7d4-245">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
