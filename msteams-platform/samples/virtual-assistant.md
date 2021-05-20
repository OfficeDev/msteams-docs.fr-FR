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
# <a name="create-virtual-assistant"></a><span data-ttu-id="512a6-104">Créer un assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="512a6-104">Create Virtual Assistant</span></span> 

<span data-ttu-id="512a6-105">Virtual Assistant est un modèle open-source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant le plein contrôle de l’expérience utilisateur, de l’image de marque organisationnelle et des données nécessaires.</span><span class="sxs-lookup"><span data-stu-id="512a6-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="512a6-106">Le [modèle de base Virtual Assistant](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) est le bloc de base qui rassemble les technologies Microsoft nécessaires pour construire un assistant virtuel, y compris le Bot Framework [SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), et [QnA Maker](https://www.qnamaker.ai/).</span><span class="sxs-lookup"><span data-stu-id="512a6-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), and [QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="512a6-107">Il réunit également les capacités essentielles, y compris l’enregistrement des compétences, les comptes liés, l’intention conversationnelle de base d’offrir une gamme d’interactions et d’expériences transparentes aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="512a6-107">It also brings together the essential capabilities including  skills registration, linked accounts, basic conversational intent to offer a range of seamless interactions and experiences to users.</span></span> <span data-ttu-id="512a6-108">En outre, les capacités de modèle incluent de riches exemples de compétences conversationnelles [réutilisables.](https://microsoft.github.io/botframework-solutions/overview/skills)</span><span class="sxs-lookup"><span data-stu-id="512a6-108">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="512a6-109">Les compétences individuelles sont intégrées dans une solution d’assistant virtuel pour activer plusieurs scénarios.</span><span class="sxs-lookup"><span data-stu-id="512a6-109">Individual skills are integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="512a6-110">À l’aide du Bot Framework SDK, les compétences sont présentées sous forme de code source, ce qui vous permet de personnaliser et d’étendre au besoin.</span><span class="sxs-lookup"><span data-stu-id="512a6-110">Using the Bot Framework SDK, skills are presented in source code form, enabling you to customize and extend as required.</span></span> <span data-ttu-id="512a6-111">Pour plus d’informations sur les compétences de Bot Framework, voir [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="512a6-111">For more information on skills of Bot Framework, see [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="512a6-112">Ce document vous guide sur les considérations de mise en œuvre d’Assistant virtuel pour les organisations, comment créer un assistant virtuel axé sur la Teams, exemple connexe, exemple de code et limitations de Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="512a6-112">This document guides you on Virtual Assistant implementation considerations for organizations, how to create a Teams focused Virtual Assistant, related example, code sample, and limitations of Virtual Assistant.</span></span>
<span data-ttu-id="512a6-113">L’image suivante affiche la vue d’ensemble de l’assistant virtuel :</span><span class="sxs-lookup"><span data-stu-id="512a6-113">The following image displays the overview of virtual assistant:</span></span>

![Diagramme d’aperçu d’assistant virtuel](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="512a6-115">Les activités de messagerie texte sont acheminées vers les compétences associées par le noyau assistant virtuel à l’aide d’un [modèle](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) de répartition.</span><span class="sxs-lookup"><span data-stu-id="512a6-115">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="512a6-116">Considérations de mise en œuvre</span><span class="sxs-lookup"><span data-stu-id="512a6-116">Implementation considerations</span></span>

<span data-ttu-id="512a6-117">La décision d’ajouter un assistant virtuel comprend de nombreux déterminants et diffère pour chaque organisation.</span><span class="sxs-lookup"><span data-stu-id="512a6-117">The decision to add a Virtual Assistant includes many determinants and differs for each organization.</span></span> <span data-ttu-id="512a6-118">Les facteurs de soutien d’une implémentation d’assistant virtuel pour votre organisation sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="512a6-118">The supporting factors of a Virtual Assistant implementation for your organization are as follows:</span></span>

* <span data-ttu-id="512a6-119">Une équipe centrale gère toutes les expériences des employés.</span><span class="sxs-lookup"><span data-stu-id="512a6-119">A central team manages all employee experiences.</span></span> <span data-ttu-id="512a6-120">Il a la capacité de construire une expérience d’assistant virtuel et de gérer les mises à jour de l’expérience de base, y compris l’ajout de nouvelles compétences.</span><span class="sxs-lookup"><span data-stu-id="512a6-120">It has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
* <span data-ttu-id="512a6-121">Il existe de multiples applications dans toutes les fonctions de l’entreprise et le nombre devrait augmenter à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="512a6-121">Multiple applications exist across business functions and the number is expected to grow in the future.</span></span>
* <span data-ttu-id="512a6-122">Les applications existantes sont personnalisables, appartenant à l’organisation, et sont converties en compétences pour un assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="512a6-122">Existing applications are customizable, owned by the organization, and are converted into skills for a Virtual Assistant.</span></span>
* <span data-ttu-id="512a6-123">L’équipe d’expériences des employés centraux est en mesure d’influencer les personnalisations sur les applications existantes.</span><span class="sxs-lookup"><span data-stu-id="512a6-123">The central employee experiences team is able to influence customizations to existing apps.</span></span> <span data-ttu-id="512a6-124">Il fournit également les conseils nécessaires pour intégrer les applications existantes en tant que compétences dans l’expérience assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="512a6-124">It also provides necessary guidance for integrating existing applications as skills in Virtual Assistant experience.</span></span>

<span data-ttu-id="512a6-125">L’image suivante affiche les fonctions métier de Virtual Assistant :</span><span class="sxs-lookup"><span data-stu-id="512a6-125">The following image displays the business functions of Virtual Assistant:</span></span> 

![L’équipe centrale maintient l’assistant, et les équipes de fonction d’affaires apportent des qualifications](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="512a6-127">Créer un assistant virtuel Teams axé sur les Teams</span><span class="sxs-lookup"><span data-stu-id="512a6-127">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="512a6-128">Microsoft a publié un modèle [Visual Studio pour la construction](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) d’assistants virtuels et de compétences.</span><span class="sxs-lookup"><span data-stu-id="512a6-128">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="512a6-129">Avec le Visual Studio, vous pouvez créer un assistant virtuel, alimenté par une expérience basée sur le texte avec le soutien de cartes riches limitées avec des actions.</span><span class="sxs-lookup"><span data-stu-id="512a6-129">With the Visual Studio template, you can create a Virtual Assistant, powered by a text based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="512a6-130">Nous avons amélioré le modèle de base Visual Studio pour inclure les capacités de Microsoft Teams et alimenter les expériences d’Teams’applications.</span><span class="sxs-lookup"><span data-stu-id="512a6-130">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="512a6-131">Quelques-unes des fonctionnalités incluent la prise en charge de cartes adaptatives riches, modules de tâches, équipes ou chats de groupe, et des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="512a6-131">A few of the capabilities include support for rich Adaptive Cards, task modules, teams or group chats, and messaging extensions.</span></span> <span data-ttu-id="512a6-132">Pour plus d’informations sur l’extension de Virtual Assistant Microsoft Teams, [voir Tutoriel: Étendre votre assistant virtuel à Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span><span class="sxs-lookup"><span data-stu-id="512a6-132">For more information on extending Virtual Assistant to Microsoft Teams, see [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>    
<span data-ttu-id="512a6-133">L’image suivante affiche le diagramme de haut niveau d’une solution assistant virtuel :</span><span class="sxs-lookup"><span data-stu-id="512a6-133">The following image displays the high level diagram of a Virtual Assistant solution:</span></span>

![Diagramme de haut niveau d’une solution d’assistant virtuel](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="512a6-135">Ajoutez des cartes adaptatives à votre assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="512a6-135">Add Adaptive Cards to your Virtual Assistant</span></span>

<span data-ttu-id="512a6-136">Pour envoyer correctement les demandes, votre assistant virtuel doit identifier le modèle LUIS correct et les compétences correspondantes qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="512a6-136">To dispatch requests properly, your Virtual Assistant must identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="512a6-137">Toutefois, le mécanisme de répartition ne peut pas être utilisé pour les activités d’action par carte car le modèle LUIS associé à une compétence, est formé pour les textes d’action par carte.</span><span class="sxs-lookup"><span data-stu-id="512a6-137">However, the dispatching mechanism cannot be used for card action activities as the LUIS model associated with a skill, is trained for card action texts.</span></span> <span data-ttu-id="512a6-138">Les textes d’action de la carte sont fixes, prédéfins mots clés, et non commentés à partir d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="512a6-138">The card action texts are fixed, pre-defined keywords, and not commented from a user.</span></span>

<span data-ttu-id="512a6-139">Cet inconvénient est résolu en intégrant des informations de compétence dans la charge utile d’action de la carte.</span><span class="sxs-lookup"><span data-stu-id="512a6-139">This drawback is resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="512a6-140">Chaque compétence doit s’intégrer `skillId` dans le domaine des actions de  `value` carte.</span><span class="sxs-lookup"><span data-stu-id="512a6-140">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="512a6-141">Vous devez vous assurer que chaque activité d’action de carte contient les informations de compétences pertinentes, et Virtual Assistant peut utiliser ces informations pour l’expédition.</span><span class="sxs-lookup"><span data-stu-id="512a6-141">You must ensure that each card action activity carries the relevant skill information, and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="512a6-142">Vous devez fournir dans `skillId` le constructeur pour s’assurer que les informations de compétence sont toujours présentes dans les actions de carte.</span><span class="sxs-lookup"><span data-stu-id="512a6-142">You must provide `skillId` in the constructor to ensure that the skill information is always present in card actions.</span></span>
<span data-ttu-id="512a6-143">Un exemple de code d’échantillon de données d’action de carte est affiché dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="512a6-143">A card action data sample code is shown in the following section:</span></span>
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

<span data-ttu-id="512a6-144">Ensuite, `SkillCardActionData` la classe dans le modèle assistant virtuel est introduit pour extraire de la charge utile `skillId` d’action de la carte.</span><span class="sxs-lookup"><span data-stu-id="512a6-144">Next, `SkillCardActionData` class in the Virtual Assistant template is introduces to extract `skillId` from the card action payload.</span></span>
<span data-ttu-id="512a6-145">Un extrait de code à extraire de la  `skillId` charge utile d’action de la carte est affiché dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="512a6-145">A code snippet to extract  `skillId` from card action payload is shown in the following section:</span></span>

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

<span data-ttu-id="512a6-146">La mise en œuvre se fait par une méthode d’extension dans la [classe](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) Activité.</span><span class="sxs-lookup"><span data-stu-id="512a6-146">The implementation is done by an extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>
<span data-ttu-id="512a6-147">Un extrait de code à extraire des données  `skillId` d’action de la carte est affiché dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="512a6-147">A code snippet to extract  `skillId` from card action data is shown in the following section:</span></span>

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

### <a name="handle-interruptions"></a><span data-ttu-id="512a6-148">Gérer les interruptions</span><span class="sxs-lookup"><span data-stu-id="512a6-148">Handle interruptions</span></span>

<span data-ttu-id="512a6-149">Virtual Assistant peut gérer les interruptions dans les cas où un utilisateur tente d’invoquer une compétence alors qu’une autre compétence est actuellement active.</span><span class="sxs-lookup"><span data-stu-id="512a6-149">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="512a6-150">`TeamsSkillDialog`, et `TeamsSwitchSkillDialog` sont introduits sur la base de [SkillDialog de](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) Bot Framework [et SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span><span class="sxs-lookup"><span data-stu-id="512a6-150">`TeamsSkillDialog`, and `TeamsSwitchSkillDialog`are introduced based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span></span> <span data-ttu-id="512a6-151">Ils permettent aux utilisateurs de passer d’une expérience de compétence à des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="512a6-151">They enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="512a6-152">Pour traiter cette demande, l’assistant virtuel invite l’utilisateur avec un message de confirmation à changer de compétences :</span><span class="sxs-lookup"><span data-stu-id="512a6-152">To handle this request, the Virtual Assistant prompts the user with a confirmation message to switch skills:</span></span>

![Invite de confirmation lors du passage à une nouvelle compétence](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a><span data-ttu-id="512a6-154">Gérer les demandes de module de tâches</span><span class="sxs-lookup"><span data-stu-id="512a6-154">Handle task module requests</span></span>

<span data-ttu-id="512a6-155">Pour ajouter des fonctionnalités de module de tâche à un assistant virtuel, deux méthodes supplémentaires sont incluses dans le gestionnaire d’activité Assistant virtuel : `OnTeamsTaskModuleFetchAsync` et `OnTeamsTaskModuleSubmitAsync` .</span><span class="sxs-lookup"><span data-stu-id="512a6-155">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="512a6-156">Ces méthodes écoutent les activités liées au module de tâches de Virtual Assistant, identifient les compétences associées à la demande et transmettre la demande à la compétence identifiée.</span><span class="sxs-lookup"><span data-stu-id="512a6-156">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="512a6-157">Le transfert de demande se fait par le [biais de la méthode SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) `PostActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="512a6-157">Request forwarding is done through the [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="512a6-158">Il renvoie la `InvokeResponse` réponse comme qui est parsed et converti en `TaskModuleResponse` .</span><span class="sxs-lookup"><span data-stu-id="512a6-158">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>


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

<span data-ttu-id="512a6-159">Une approche similaire est suivie pour l’expédition de l’action par carte et les réponses au module de tâches.</span><span class="sxs-lookup"><span data-stu-id="512a6-159">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="512a6-160">Module de tâche aller chercher et soumettre des données d’action est mis à jour pour inclure `skillId` .</span><span class="sxs-lookup"><span data-stu-id="512a6-160">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="512a6-161">La méthode `GetSkillId` d’extension `skillId` d’activité extrait de la charge utile qui fournit des détails sur la compétence qui doit être invoquée.</span><span class="sxs-lookup"><span data-stu-id="512a6-161">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="512a6-162">L’extrait de code et `OnTeamsTaskModuleFetchAsync` les `OnTeamsTaskModuleSubmitAsync` méthodes sont donnés dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="512a6-162">The code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods are given in the following section:</span></span>

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

<span data-ttu-id="512a6-163">En outre, vous devez inclure tous les domaines de compétence dans `validDomains` la section dans le fichier manifeste de Virtual Assistant afin que les modules de tâches invoqués par un rendu de compétence correctement.</span><span class="sxs-lookup"><span data-stu-id="512a6-163">Additionally, you must include all skill domains in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked through a skill render properly.</span></span>

### <a name="handle-collaborative-app-scopes"></a><span data-ttu-id="512a6-164">Gérer les étendues d’applications collaboratives</span><span class="sxs-lookup"><span data-stu-id="512a6-164">Handle collaborative app scopes</span></span>

<span data-ttu-id="512a6-165">Teams applications peuvent exister dans plusieurs étendues, y compris le chat 1:1, le chat de groupe et les canaux.</span><span class="sxs-lookup"><span data-stu-id="512a6-165">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="512a6-166">Le modèle d’assistant virtuel de base est conçu pour les chats 1:1.</span><span class="sxs-lookup"><span data-stu-id="512a6-166">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="512a6-167">Dans le cadre de l’expérience d’onboarding Virtual Assistant invite les utilisateurs à nommer et maintient l’état de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="512a6-167">As part of the onboarding experience Virtual Assistant prompts users for name and maintains user state.</span></span> <span data-ttu-id="512a6-168">Étant donné que cette expérience d’onboarding n’est pas adaptée aux étendues de chat de groupe ou de canal, elle a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="512a6-168">Since that onboarding experience is not suited for group chat or channel scopes it has been removed.</span></span>

<span data-ttu-id="512a6-169">Les compétences doivent gérer les activités dans de multiples étendues, telles que le chat 1:1, le chat de groupe et la conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="512a6-169">Skills should handle activities in multiple scopes, such as 1:1 chat, group chat, and channel conversation.</span></span> <span data-ttu-id="512a6-170">Si l’une ou l’autre de ces portées n’est pas prise en charge, les compétences doivent répondre par un message approprié.</span><span class="sxs-lookup"><span data-stu-id="512a6-170">If any of these scopes are not supported, skills must respond with an appropriate message.</span></span>

<span data-ttu-id="512a6-171">Les fonctions de traitement suivantes ont été ajoutées au noyau Assistant virtuel :</span><span class="sxs-lookup"><span data-stu-id="512a6-171">The following  processing functions have been added to Virtual Assistant core:</span></span>

* <span data-ttu-id="512a6-172">Assistant virtuel peut être invoqué sans aucun message texte d’un chat de groupe ou d’un canal.</span><span class="sxs-lookup"><span data-stu-id="512a6-172">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
* <span data-ttu-id="512a6-173">Les articulations sont nettoyées avant d’envoyer le message au module de répartition.</span><span class="sxs-lookup"><span data-stu-id="512a6-173">Articulations are cleaned before sending the message to the dispatch module.</span></span> <span data-ttu-id="512a6-174">Par exemple, retirez les @mention du bot.</span><span class="sxs-lookup"><span data-stu-id="512a6-174">For example, remove the necessary @mention of the bot.</span></span>

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

### <a name="handle-messaging-extensions"></a><span data-ttu-id="512a6-175">Gérer les extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="512a6-175">Handle messaging extensions</span></span>

<span data-ttu-id="512a6-176">Les commandes d’une extension de messagerie sont déclarées dans votre fichier manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="512a6-176">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="512a6-177">L’interface utilisateur de l’extension de messagerie est alimentée par ces commandes.</span><span class="sxs-lookup"><span data-stu-id="512a6-177">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="512a6-178">Pour qu’un assistant virtuel rallonge une commande d’extension de messagerie en tant que compétence jointe, le manifeste d’un assistant virtuel doit contenir ces commandes.</span><span class="sxs-lookup"><span data-stu-id="512a6-178">For a Virtual Assistant to power a messaging extension command as an attached skill, a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="512a6-179">Vous devez ajouter les commandes du manifeste d’une compétence individuelle au manifeste de l’assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="512a6-179">You must add the commands from an individual skill's manifest to the Virtual Assistant's manifest.</span></span> <span data-ttu-id="512a6-180">L’ID de commande fournit des informations sur une compétence associée en appending id de l’application de la compétence par le biais d’un séparateur `:` .</span><span class="sxs-lookup"><span data-stu-id="512a6-180">The command ID provides information about an associated skill by appending the skill's app ID through a separator `:`.</span></span>

<span data-ttu-id="512a6-181">L’extrait du fichier manifeste d’une compétence est affiché dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="512a6-181">The snippet from a skill's manifest file is shown in the following section:</span></span>

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

<span data-ttu-id="512a6-182">L’extrait de code manifeste de fichier virtual assistant correspondant est affiché dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="512a6-182">The corresponding Virtual Assistant manifest file code snippet is shown in the following section:</span></span>

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

<span data-ttu-id="512a6-183">Une fois que les commandes sont invoquées par un utilisateur, l’assistant virtuel peut identifier une compétence associée en parsing l’ID de commande, mettre à jour l’activité en supprimant le suffixe supplémentaire de `:<skill_id>` l’ID de commande, et le transmettre à la compétence correspondante.</span><span class="sxs-lookup"><span data-stu-id="512a6-183">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix `:<skill_id>` from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="512a6-184">Le code d’une compétence n’a pas besoin de gérer le suffixe supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="512a6-184">The code for a skill doesnot need to handle the extra suffix.</span></span> <span data-ttu-id="512a6-185">Ainsi, les conflits entre les iD de commande entre les compétences sont évités.</span><span class="sxs-lookup"><span data-stu-id="512a6-185">Thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="512a6-186">Avec cette approche, toutes les commandes de recherche et d’action d’une compétence dans tous les contextes, **tels que composer,** **commanderbox,** **et le message** sont alimentés par un assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="512a6-186">With this approach, all the search and action commands of a skill within all contexts, such as **compose**, **commandBox**, and **message** are powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="512a6-187">Certaines activités d’extension de messagerie n’incluent pas l’id de commande.</span><span class="sxs-lookup"><span data-stu-id="512a6-187">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="512a6-188">Par exemple, ne `composeExtension/selectItem` contient que la valeur de l’action d’appel d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="512a6-188">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="512a6-189">Pour identifier la compétence associée, est `skillId`  attaché à chaque carte d’élément tout en formant une réponse pour `OnTeamsMessagingExtensionQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="512a6-189">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="512a6-190">Ceci est similaire à l’approche pour ajouter [des cartes adaptatives à votre assistant virtuel](#add-adaptive-cards-to-your-virtual-assistant).</span><span class="sxs-lookup"><span data-stu-id="512a6-190">This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example"></a><span data-ttu-id="512a6-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="512a6-191">Example</span></span>

<span data-ttu-id="512a6-192">L’exemple suivant montre comment convertir le modèle d’application Book-a-room en une compétence assistant virtuel : Book-a-room est un Microsoft Teams qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pendant 30, 60 ou 90 minutes à partir de l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="512a6-192">The following example shows how to convert the Book-a-room app template to a Virtual Assistant skill: Book-a-room is a Microsoft Teams that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="512a6-193">Le temps par défaut est de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="512a6-193">The default time is 30 minutes.</span></span> <span data-ttu-id="512a6-194">Le livre-une-chambre bot portées à des conversations personnelles ou 1:1.</span><span class="sxs-lookup"><span data-stu-id="512a6-194">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="512a6-195">L’image suivante affiche un assistant virtuel avec un **livre une compétence de** chambre:</span><span class="sxs-lookup"><span data-stu-id="512a6-195">The following image displays a Virtual Assistant with a **book a room** skill:</span></span>

![Assistant virtuel avec une compétence « réserver une chambre »](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="512a6-197">Voici les modifications delta introduites pour la convertir en une compétence qui est attachée à un assistant virtuel.</span><span class="sxs-lookup"><span data-stu-id="512a6-197">Followings are the delta changes introduced to convert it to a skill which is attached to a Virtual Assistant.</span></span> <span data-ttu-id="512a6-198">Des lignes directrices similaires sont suivies pour convertir tout bot v4 existant en une compétence.</span><span class="sxs-lookup"><span data-stu-id="512a6-198">Similar guidelines are followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="512a6-199">Manifeste de compétence</span><span class="sxs-lookup"><span data-stu-id="512a6-199">Skill manifest</span></span>

<span data-ttu-id="512a6-200">Un manifeste de compétences est un fichier JSON qui expose le point de terminaison de messagerie, l’ID, le nom et d’autres métadonnées pertinentes d’une compétence.</span><span class="sxs-lookup"><span data-stu-id="512a6-200">A skill manifest is a JSON file that exposes a skill's messaging endpoint, ID, name, and other relevant metadata.</span></span> <span data-ttu-id="512a6-201">Ce manifeste est différent du manifeste utilisé pour le chargement latéral d’une application dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="512a6-201">This manifest is different than the manifest used for sideloading an app in Microsoft Teams.</span></span> <span data-ttu-id="512a6-202">Un assistant virtuel nécessite un chemin vers ce fichier comme une entrée pour joindre une compétence.</span><span class="sxs-lookup"><span data-stu-id="512a6-202">A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="512a6-203">Nous avons ajouté le manifeste suivant au dossier wwwroot du bot.</span><span class="sxs-lookup"><span data-stu-id="512a6-203">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="512a6-204">INTÉGRATION LUIS</span><span class="sxs-lookup"><span data-stu-id="512a6-204">LUIS Integration</span></span>

<span data-ttu-id="512a6-205">Le modèle de répartition de Virtual Assistant est construit en fonction des modèles LUIS des compétences attachées.</span><span class="sxs-lookup"><span data-stu-id="512a6-205">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="512a6-206">Le modèle d’expédition identifie l’intention de chaque activité de texte et découvre les compétences qui y sont associées.</span><span class="sxs-lookup"><span data-stu-id="512a6-206">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="512a6-207">Virtual Assistant nécessite le modèle LUIS de compétence en `.lu` format comme entrée tout en attachant une compétence.</span><span class="sxs-lookup"><span data-stu-id="512a6-207">Virtual Assistant requires skill's LUIS model in `.lu` format as an input while attaching a skill.</span></span> <span data-ttu-id="512a6-208">LUIS json est converti en format à `.lu` l’aide de l’outil botframework-cli.</span><span class="sxs-lookup"><span data-stu-id="512a6-208">LUIS json is converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="512a6-209">Book-a-room bot a deux commandes principales pour les utilisateurs:</span><span class="sxs-lookup"><span data-stu-id="512a6-209">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="512a6-210">Nous avons construit un modèle LUIS en comprenant ces deux commandes.</span><span class="sxs-lookup"><span data-stu-id="512a6-210">We have built a LUIS model by understanding these two commands.</span></span> <span data-ttu-id="512a6-211">Les secrets correspondants doivent être peuplés dans `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="512a6-211">Corresponding secrets must be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="512a6-212">Le fichier LUIS JSON correspondant se trouve [ici](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).</span><span class="sxs-lookup"><span data-stu-id="512a6-212">The corresponding LUIS JSON file is found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).</span></span>
<span data-ttu-id="512a6-213">Le fichier `.lu` correspondant est affiché dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="512a6-213">The corresponding `.lu` file is shown in the following section:</span></span>

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

<span data-ttu-id="512a6-214">Avec cette approche, toute commande émise par un utilisateur à Virtual Assistant liée `book room` ou sont identifiées comme une commande associée au bot et est transmise à cette `manage favorites` `Book-a-room` compétence.</span><span class="sxs-lookup"><span data-stu-id="512a6-214">With this approach, any command issued by a user to Virtual Assistant related to `book room` or `manage favorites` are identified as a command associated with `Book-a-room` bot and is forwarded to this skill.</span></span>
<span data-ttu-id="512a6-215">D’autre part, `Book-a-room room` bot doit utiliser le modèle LUIS pour comprendre ces commandes si elles ne sont pas tapées à plein.</span><span class="sxs-lookup"><span data-stu-id="512a6-215">On the other hand, `Book-a-room room` bot needs to use LUIS model to understand these commands if they are not typed full.</span></span> <span data-ttu-id="512a6-216">Par exemple : `I want to manage my favorite rooms`.</span><span class="sxs-lookup"><span data-stu-id="512a6-216">For example: `I want to manage my favorite rooms`.</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="512a6-217">Support multi-langues</span><span class="sxs-lookup"><span data-stu-id="512a6-217">Multi-Language support</span></span>

<span data-ttu-id="512a6-218">À titre d’exemple, un modèle LUIS avec seulement la culture anglaise est créé.</span><span class="sxs-lookup"><span data-stu-id="512a6-218">As an example, a LUIS model with only English culture is created.</span></span> <span data-ttu-id="512a6-219">Vous pouvez créer des modèles LUIS correspondant à d’autres langues et ajouter l’entrée à `cognitivemodels.json` .</span><span class="sxs-lookup"><span data-stu-id="512a6-219">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="512a6-220">En parallèle, ajoutez le fichier `.lu` correspondant dans le chemin luisFolder.</span><span class="sxs-lookup"><span data-stu-id="512a6-220">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="512a6-221">La structure du dossier doit être la suivante :</span><span class="sxs-lookup"><span data-stu-id="512a6-221">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="512a6-222">Pour modifier le `languages` paramètre, mettez à jour la commande botskills comme suit :</span><span class="sxs-lookup"><span data-stu-id="512a6-222">To modify `languages` parameter, update botskills command as follows:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="512a6-223">Virtual Assistant utilise pour `SetLocaleMiddleware` identifier le lieu actuel et invoquer le modèle de répartition correspondant.</span><span class="sxs-lookup"><span data-stu-id="512a6-223">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="512a6-224">L’activité de framework bot a le champ local qui est employé par ce middleware.</span><span class="sxs-lookup"><span data-stu-id="512a6-224">Bot framework activity has locale field which is used by this middleware.</span></span> <span data-ttu-id="512a6-225">Vous pouvez utiliser la même chose pour vos compétences ainsi.</span><span class="sxs-lookup"><span data-stu-id="512a6-225">You can use the same for your skill as well.</span></span> <span data-ttu-id="512a6-226">Book-a-room bot n’utilise pas ce middleware et obtient plutôt local de Bot framework activity [clientInfo entité](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span><span class="sxs-lookup"><span data-stu-id="512a6-226">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="512a6-227">Validation des réclamations</span><span class="sxs-lookup"><span data-stu-id="512a6-227">Claim validation</span></span>

<span data-ttu-id="512a6-228">Nous avons ajouté [claimsValidator pour](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) limiter les appelants à la compétence.</span><span class="sxs-lookup"><span data-stu-id="512a6-228">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="512a6-229">Pour permettre à un assistant virtuel d’appeler cette compétence, remplissez `AllowedCallers` le tableau à partir de `appsettings` l’iD d’application de cet assistant virtuel particulier.</span><span class="sxs-lookup"><span data-stu-id="512a6-229">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="512a6-230">Le tableau des appelants autorisé peut restreindre les compétences auxquelles les consommateurs peuvent accéder.</span><span class="sxs-lookup"><span data-stu-id="512a6-230">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="512a6-231">Ajoutez une seule entrée `*` à ce tableau, pour accepter les appels de n’importe quel consommateur de compétences.</span><span class="sxs-lookup"><span data-stu-id="512a6-231">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```

<span data-ttu-id="512a6-232">Pour plus d’informations sur l’ajout de validation des revendications à une compétence, voir [ajouter la validation des revendications à la compétence](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="512a6-232">For more information on adding claims validation to a skill, see [add claims validation to skill](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="limitation-of-card-refresh"></a><span data-ttu-id="512a6-233">Limitation de la actualisation de la carte</span><span class="sxs-lookup"><span data-stu-id="512a6-233">Limitation of card refresh</span></span> 

<span data-ttu-id="512a6-234">La mise à jour de l’activité, telle que la mise à jour de la carte, n’est pas encore prise en charge par Virtual Assistant[(github issue).](https://github.com/microsoft/botbuilder-dotnet/issues/3686)</span><span class="sxs-lookup"><span data-stu-id="512a6-234">Updating activity, such as card refresh is not supported yet through Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="512a6-235">Par conséquent, nous avons remplacé tous les appels de rafraîchissement de carte `UpdateActivityAsync` par l’affichage de nouveaux appels de carte `SendActivityAsync` .</span><span class="sxs-lookup"><span data-stu-id="512a6-235">Hence, we have replaced all card refresh calls `UpdateActivityAsync` with posting new card calls `SendActivityAsync`.</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="512a6-236">Actions de carte et flux de modules de tâches</span><span class="sxs-lookup"><span data-stu-id="512a6-236">Card actions and task module flows</span></span>

<span data-ttu-id="512a6-237">Pour transmettre l’action de la carte ou les activités du module de tâche à une compétence associée, la compétence doit `skillId` s’y intégrer.</span><span class="sxs-lookup"><span data-stu-id="512a6-237">To forward card action or task module activities to an associated skill, the skill must embed `skillId` to it.</span></span>
<span data-ttu-id="512a6-238">`Book-a-room` l’action de la carte bot, le module de tâche aller chercher et soumettre des charges utiles d’action sont modifiés pour `skillId` contenir comme un paramètre.</span><span class="sxs-lookup"><span data-stu-id="512a6-238">`Book-a-room` bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="512a6-239">Pour plus [d’informations, consultez](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) cette section à partir de cette documentation.</span><span class="sxs-lookup"><span data-stu-id="512a6-239">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="512a6-240">Gérer les activités à partir d’un chat de groupe ou d’une portée de canal</span><span class="sxs-lookup"><span data-stu-id="512a6-240">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="512a6-241">`Book-a-room bot` est conçu pour les conversations privées, telles que la portée personnelle ou 1:1 seulement.</span><span class="sxs-lookup"><span data-stu-id="512a6-241">`Book-a-room bot` is designed for private chats, such as personal or 1:1 scope only.</span></span> <span data-ttu-id="512a6-242">Puisque nous avons personnalisé Virtual Assistant pour prendre en charge le chat de groupe et les étendues de canaux, l’assistant virtuel doit être invoqué à partir des étendues de canaux et donc, `Book-a-room` bot doit obtenir des activités pour la même portée.</span><span class="sxs-lookup"><span data-stu-id="512a6-242">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant must be invoked from the channel scopes and thus, `Book-a-room` bot must get activities for the same scope.</span></span> <span data-ttu-id="512a6-243">Par `Book-a-room` conséquent bot est personnalisé pour gérer ces activités.</span><span class="sxs-lookup"><span data-stu-id="512a6-243">Hence `Book-a-room`bot is customized to handle those activities.</span></span> <span data-ttu-id="512a6-244">Vous pouvez trouver les méthodes `OnMessageActivityAsync` `Book-a-room` d’enregistrement du gestionnaire d’activité du bot.</span><span class="sxs-lookup"><span data-stu-id="512a6-244">You can find the check in `OnMessageActivityAsync` methods of `Book-a-room` bot's activity handler.</span></span>

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

<span data-ttu-id="512a6-245">Vous pouvez également tirer parti des compétences existantes à partir [du référentiel Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) ou créer une nouvelle compétence à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="512a6-245">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="512a6-246">Pour créer une nouvelle compétence, consultez des [tutoriels pour créer une nouvelle compétence.](https://microsoft.github.io/botframework-solutions/overview/skills/)</span><span class="sxs-lookup"><span data-stu-id="512a6-246">For creating a new skill, see [tutorials to create a new skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="512a6-247">Pour la documentation sur l’architecture des assistants virtuels et des compétences,[consultez Virtual Assistant et skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="512a6-247">For Virtual Assistant and skills architecture documentation, see[Virtual Assistant and skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span></span>  

## <a name="limitations-of-virtual-assistant"></a><span data-ttu-id="512a6-248">Limitations de l’assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="512a6-248">Limitations of Virtual Assistant</span></span> 

* <span data-ttu-id="512a6-249">**EndOfConversation**: Une compétence doit envoyer une activité `endOfConversation` lorsqu’elle termine une conversation.</span><span class="sxs-lookup"><span data-stu-id="512a6-249">**EndOfConversation**: A skill must send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="512a6-250">Basé sur l’activité, un assistant virtuel termine le contexte avec cette compétence particulière et revient dans le contexte racine de Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="512a6-250">Based on the activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's root context.</span></span> <span data-ttu-id="512a6-251">Pour book-a-room bot, il n’y a pas d’état clair où la conversation est terminée.</span><span class="sxs-lookup"><span data-stu-id="512a6-251">For Book-a-room bot, there is no clear state where conversation is ended.</span></span> <span data-ttu-id="512a6-252">Par conséquent, nous `endOfConversation` n’avons pas envoyé de bot et quand `Book-a-room` l’utilisateur veut revenir au contexte racine, ils peuvent simplement le faire par `start over` commande.</span><span class="sxs-lookup"><span data-stu-id="512a6-252">Hence we have not sent `endOfConversation` from `Book-a-room` bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>  
* <span data-ttu-id="512a6-253">**Actualisation de la** carte : La mise à jour de la carte n’est pas encore prise en charge par Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="512a6-253">**Card refresh**: Card refresh is not yet supported through Virtual Assistant.</span></span>  
* <span data-ttu-id="512a6-254">**Extensions de messagerie**:</span><span class="sxs-lookup"><span data-stu-id="512a6-254">**Messaging extensions**:</span></span>
  * <span data-ttu-id="512a6-255">Actuellement, un assistant virtuel peut prendre en charge un maximum de dix commandes pour les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="512a6-255">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  * <span data-ttu-id="512a6-256">La configuration des extensions de messagerie n’est pas étendue aux commandes individuelles, mais à l’ensemble de l’extension elle-même.</span><span class="sxs-lookup"><span data-stu-id="512a6-256">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="512a6-257">Cela limite la configuration de chaque compétence individuelle par l’intermédiaire de Virtual Assistant.</span><span class="sxs-lookup"><span data-stu-id="512a6-257">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  * <span data-ttu-id="512a6-258">Les iD de commande d’extensions de messagerie ont une longueur maximale [de 64 caractères](../resources/schema/manifest-schema.md#composeextensions) et 37 caractères sont utilisés pour intégrer des informations de compétence.</span><span class="sxs-lookup"><span data-stu-id="512a6-258">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters are used for embedding skill information.</span></span> <span data-ttu-id="512a6-259">Ainsi, les contraintes mises à jour pour l’id de commande sont limitées à 27 caractères.</span><span class="sxs-lookup"><span data-stu-id="512a6-259">Thus, updated constraints for command ID are limited to 27 characters.</span></span>

<span data-ttu-id="512a6-260">Vous pouvez également tirer parti des compétences existantes à partir [du référentiel Bot Framework Solutions](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) ou créer une nouvelle compétence à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="512a6-260">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="512a6-261">Tutoriels pour le plus tard peuvent être trouvés [ici](https://microsoft.github.io/botframework-solutions/overview/skills/).</span><span class="sxs-lookup"><span data-stu-id="512a6-261">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="512a6-262">Veuillez consulter la [documentation pour l’assistant](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) virtuel et l’architecture des compétences.</span><span class="sxs-lookup"><span data-stu-id="512a6-262">Please refer to [documentation](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="512a6-263">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="512a6-263">Code sample</span></span>

| <span data-ttu-id="512a6-264">**Nom de l’échantillon**</span><span class="sxs-lookup"><span data-stu-id="512a6-264">**Sample name**</span></span> | <span data-ttu-id="512a6-265">**Description**</span><span class="sxs-lookup"><span data-stu-id="512a6-265">**Description**</span></span> | <span data-ttu-id="512a6-266">**C#**</span><span class="sxs-lookup"><span data-stu-id="512a6-266">**C#**</span></span> | <span data-ttu-id="512a6-267">**.NET (en)**</span><span class="sxs-lookup"><span data-stu-id="512a6-267">**.NET**</span></span> |
|----------|-----------------|----------|------------------|
| <span data-ttu-id="512a6-268">Modèle de studio visuel mis à jour</span><span class="sxs-lookup"><span data-stu-id="512a6-268">Updated visual studio template</span></span> | <span data-ttu-id="512a6-269">Modèle personnalisé pour prendre en charge les capacités des équipes.</span><span class="sxs-lookup"><span data-stu-id="512a6-269">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="512a6-270">View</span><span class="sxs-lookup"><span data-stu-id="512a6-270">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| <span data-ttu-id="512a6-271">Code de compétence de bot de livre-une-chambre</span><span class="sxs-lookup"><span data-stu-id="512a6-271">Book-a-room bot skill code</span></span> | <span data-ttu-id="512a6-272">Vous permet de trouver rapidement et réserver une salle de réunion sur la aller.</span><span class="sxs-lookup"><span data-stu-id="512a6-272">Lets you quickly find and book a meeting room on the go.</span></span> |  | [<span data-ttu-id="512a6-273">View</span><span class="sxs-lookup"><span data-stu-id="512a6-273">View</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a><span data-ttu-id="512a6-274">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="512a6-274">See also</span></span>

- [<span data-ttu-id="512a6-275">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="512a6-275">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

- [<span data-ttu-id="512a6-276">Réservez une chambre</span><span class="sxs-lookup"><span data-stu-id="512a6-276">Book-a-room</span></span>](app-templates.md#book-a-room)

- [<span data-ttu-id="512a6-277">bot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="512a6-277">Microsoft Teams bot</span></span>](../bots/what-are-bots.md)