---
title: Conception de votre application personnalisée
author: heath-hamilton
description: Découvrez comment concevoir des Microsoft Teams applications. Les ressources incluent le kit Microsoft Teams’interface utilisateur, les meilleures pratiques, les exemples et bien plus encore.
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 2f21872bd8c37026528ff6fde282e8c433d5e052
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565115"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="fc746-104">Conception de votre application Microsoft Teams web</span><span class="sxs-lookup"><span data-stu-id="fc746-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Image conceptuelle présentant les recommandations Microsoft Teams conception.":::

<span data-ttu-id="fc746-106">Que vous êtes concepteur, chef de produit, développeur ou fabricant à l’aide d’outils à code faible, ces instructions peuvent vous aider à prendre rapidement les bonnes décisions en matière de conception pour Microsoft Teams application.</span><span class="sxs-lookup"><span data-stu-id="fc746-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="fc746-107">Teams de conception d’application</span><span class="sxs-lookup"><span data-stu-id="fc746-107">Teams app design principles</span></span>

<span data-ttu-id="fc746-108">Teams applications permettent aux gens d’atteindre des objectifs plus réussis.</span><span class="sxs-lookup"><span data-stu-id="fc746-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="fc746-109">Utilisez ces principes pour guider votre conception.</span><span class="sxs-lookup"><span data-stu-id="fc746-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="fc746-110">Collaboration</span><span class="sxs-lookup"><span data-stu-id="fc746-110">Collaborative</span></span>

<span data-ttu-id="fc746-111">Teams applications permettent aux gens d’atteindre des objectifs plus réussis.</span><span class="sxs-lookup"><span data-stu-id="fc746-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="fc746-112">Utilisez ces principes pour guider votre conception.</span><span class="sxs-lookup"><span data-stu-id="fc746-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="fc746-113">Fiable</span><span class="sxs-lookup"><span data-stu-id="fc746-113">Trustworthy</span></span>

<span data-ttu-id="fc746-114">L’application est sécurisée et conforme.</span><span class="sxs-lookup"><span data-stu-id="fc746-114">The app is secure and compliant.</span></span> <span data-ttu-id="fc746-115">Les utilisateurs peuvent facilement trouver des informations sur la confidentialité.</span><span class="sxs-lookup"><span data-stu-id="fc746-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="fc746-116">Globalement inclusive</span><span class="sxs-lookup"><span data-stu-id="fc746-116">Globally inclusive</span></span>

<span data-ttu-id="fc746-117">Les personnes de tous horizons, de tous les compétences et de toutes les disciplines peuvent utiliser l’application.</span><span class="sxs-lookup"><span data-stu-id="fc746-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="fc746-118">Il s’agit d’une approche culturelle, culturelle et sociale.</span><span class="sxs-lookup"><span data-stu-id="fc746-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="fc746-119">Light</span><span class="sxs-lookup"><span data-stu-id="fc746-119">Light</span></span>

<span data-ttu-id="fc746-120">L’application se concentre sur les scénarios de base qui se fondent avec Teams flux de travail.</span><span class="sxs-lookup"><span data-stu-id="fc746-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="fc746-121">Natif ou distinct</span><span class="sxs-lookup"><span data-stu-id="fc746-121">Native or distinct</span></span>

<span data-ttu-id="fc746-122">L’application utilise des composants Teams de conception natifs ou les vôtres.</span><span class="sxs-lookup"><span data-stu-id="fc746-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="fc746-123">Il n’existe aucun mélange de modèles de couleurs, de contrôles, etc.</span><span class="sxs-lookup"><span data-stu-id="fc746-123">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="fc746-124">Utile</span><span class="sxs-lookup"><span data-stu-id="fc746-124">Useful</span></span>

<span data-ttu-id="fc746-125">L’application est basée sur un scénario que les personnes doivent faire dans Teams.</span><span class="sxs-lookup"><span data-stu-id="fc746-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="fc746-126">Facile à utiliser</span><span class="sxs-lookup"><span data-stu-id="fc746-126">Easy to use</span></span>

<span data-ttu-id="fc746-127">L’interface utilisateur est facile à comprendre, agréable en apparence et en ton, et rend les utilisateurs plus productifs.</span><span class="sxs-lookup"><span data-stu-id="fc746-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="fc746-128">Réactive</span><span class="sxs-lookup"><span data-stu-id="fc746-128">Responsive</span></span>

<span data-ttu-id="fc746-129">L’application est sans appareil et sans écran.</span><span class="sxs-lookup"><span data-stu-id="fc746-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="fc746-130">Accessible</span><span class="sxs-lookup"><span data-stu-id="fc746-130">Accessible</span></span>

<span data-ttu-id="fc746-131">L’application répond Teams exigences d’accessibilité en termes de contraste de couleur, d’alternatives de navigation et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="fc746-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="fc746-132">Bien décrit</span><span class="sxs-lookup"><span data-stu-id="fc746-132">Well described</span></span>

<span data-ttu-id="fc746-133">Le texte, les icônes et les images montrent clairement à quoi l’application s’utilise et comment l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="fc746-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="fc746-134">Création d’une expérience cohérente</span><span class="sxs-lookup"><span data-stu-id="fc746-134">Creating a cohesive experience</span></span>

<span data-ttu-id="fc746-135">Concevoir une application Teams s’approche de la conception d’une application web conventionnelle, mais également un peu différente.</span><span class="sxs-lookup"><span data-stu-id="fc746-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="fc746-136">Une conception efficace met en évidence les attributs uniques de votre application tout en s’ajustant naturellement Teams fonctionnalités et contextes.</span><span class="sxs-lookup"><span data-stu-id="fc746-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="fc746-137">Ces recommandations et ressources peuvent vous aider à trouver cet équilibre.</span><span class="sxs-lookup"><span data-stu-id="fc746-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="fc746-138">Vous savez ce qu’il faut faire et ce qu’il faut éviter lors de la conception de votre application Teams (par exemple, navigation à plusieurs niveaux dans un onglet).</span><span class="sxs-lookup"><span data-stu-id="fc746-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="fc746-139">Planification de votre application</span><span class="sxs-lookup"><span data-stu-id="fc746-139">Planning your app</span></span>

<span data-ttu-id="fc746-140">Pour concevoir une application Teams de qualité supérieure, vous devez d’abord comprendre ce que vous voulez que votre application fait et comment vous pensez que les personnes l’utiliseront.</span><span class="sxs-lookup"><span data-stu-id="fc746-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="fc746-141">Si ce n’est pas déjà fait, prenez le temps de [planifier correctement votre application.](../../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="fc746-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="fc746-142">Fondements de la conception</span><span class="sxs-lookup"><span data-stu-id="fc746-142">Design fundamentals</span></span>

<span data-ttu-id="fc746-143">Découvrez les [principes de base de Teams conception d’application,](design-teams-app-fundamentals.md)notamment la disposition, les modèles de couleurs, etc.</span><span class="sxs-lookup"><span data-stu-id="fc746-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="fc746-144">Composants d’interface utilisateur Fluent de base pour Teams</span><span class="sxs-lookup"><span data-stu-id="fc746-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="fc746-145">Basés sur l’interface utilisateur Fluent, ce sont les principaux éléments pour créer des [interfaces Teams familières.](design-teams-app-basic-ui-components.md)</span><span class="sxs-lookup"><span data-stu-id="fc746-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="fc746-146">Modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="fc746-146">UI templates</span></span>

<span data-ttu-id="fc746-147">Créez rapidement des conceptions complexes et haute fidélité avec des modèles pour les Teams et les flux [de travail.](design-teams-app-ui-templates.md)</span><span class="sxs-lookup"><span data-stu-id="fc746-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="fc746-148">Fonctionnalités de l’application</span><span class="sxs-lookup"><span data-stu-id="fc746-148">App capabilities</span></span>

<span data-ttu-id="fc746-149">Comprendre comment les personnes ajoutent, utilisent et gèrent Teams applications pour utiliser au mieux chaque fonctionnalité de votre conception.</span><span class="sxs-lookup"><span data-stu-id="fc746-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="fc746-150">Applications personnelles</span><span class="sxs-lookup"><span data-stu-id="fc746-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="fc746-151">Onglets</span><span class="sxs-lookup"><span data-stu-id="fc746-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="fc746-152">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc746-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="fc746-153">Bots</span><span class="sxs-lookup"><span data-stu-id="fc746-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="fc746-154">Extensions de réunion</span><span class="sxs-lookup"><span data-stu-id="fc746-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="fc746-155">Modules de tâche</span><span class="sxs-lookup"><span data-stu-id="fc746-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="fc746-156">Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fc746-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="fc746-157">Personnalisation de l’application</span><span class="sxs-lookup"><span data-stu-id="fc746-157">App customization</span></span>

<span data-ttu-id="fc746-158">Comprendre comment l’administrateur Teams peut personnaliser ou renommer l’application en fonction des besoins de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="fc746-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="fc746-159">Cette personnalisation est activée si vous définissez le `configurableProperties` schéma de manifeste.</span><span class="sxs-lookup"><span data-stu-id="fc746-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="fc746-160">Pour plus d’informations, voir [Personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="fc746-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="fc746-161">La personnalisation d’application permet aux administrateurs de modifier l’apparence des applications chargées par le biais de bots, d’extensions de messagerie, d’onglets et de connecteurs.</span><span class="sxs-lookup"><span data-stu-id="fc746-161">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="fc746-162">Par exemple, si l’administrateur Teams personnalise le nom d’une application de *Contoso* à *Agent Contoso,* l’application apparaît sous le nouveau nom *Agent Contoso* pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fc746-162">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="fc746-163">Toutefois, lors de l’ajout d’un connecteur à une conversation, dans la liste, les connecteurs afficheront toujours le nom de l’application en tant *que Contoso*.</span><span class="sxs-lookup"><span data-stu-id="fc746-163">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="fc746-164">En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="fc746-164">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="fc746-165">Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="fc746-165">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="fc746-166">Outils et exemples</span><span class="sxs-lookup"><span data-stu-id="fc746-166">Tools and samples</span></span>

<span data-ttu-id="fc746-167">Les outils suivants peuvent aider les concepteurs et les développeurs à démarrer :</span><span class="sxs-lookup"><span data-stu-id="fc746-167">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="fc746-168">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fc746-168">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="fc746-169">Concevez une Teams avec des composants d’interface utilisateur, des modèles et des exemples que vous pouvez faire glisser, déposer et modifier selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="fc746-169">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="fc746-170">Le kit d’interface utilisateur inclut également des informations complètes sur l’apparence et le comportement des applications dans Teams différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="fc746-170">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc746-171">Obtenir le kit d’interface utilisateur (Figma)</span><span class="sxs-lookup"><span data-stu-id="fc746-171">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="fc746-172">Microsoft Teams Bibliothèque d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="fc746-172">Microsoft Teams UI Library</span></span>

<span data-ttu-id="fc746-173">Affichez et testez les Teams d’interface utilisateur et les composants associés dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="fc746-173">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc746-174">Essayer la bibliothèque d’interface utilisateur (aire de jeu)</span><span class="sxs-lookup"><span data-stu-id="fc746-174">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="fc746-175">Importez ces modèles et composants associés directement dans Teams projet d’application.</span><span class="sxs-lookup"><span data-stu-id="fc746-175">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc746-176">Obtenir la bibliothèque d’interface utilisateur (GitHub)</span><span class="sxs-lookup"><span data-stu-id="fc746-176">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="fc746-177">Exemple d’application</span><span class="sxs-lookup"><span data-stu-id="fc746-177">Sample app</span></span>

<span data-ttu-id="fc746-178">Installez un exemple d’application pour voir l’apparence et le comportement des modèles d’interface utilisateur Teams contextes.</span><span class="sxs-lookup"><span data-stu-id="fc746-178">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc746-179">Obtenir l’exemple d’application (GitHub)</span><span class="sxs-lookup"><span data-stu-id="fc746-179">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="fc746-180">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="fc746-180">Other resources</span></span>

<span data-ttu-id="fc746-181">Pour en savoir plus, essayez l’une des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc746-181">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="fc746-182">Documentation de l’interface utilisateur Fluent</span><span class="sxs-lookup"><span data-stu-id="fc746-182">Fluent UI documentation</span></span>

<span data-ttu-id="fc746-183">Obtenez des exemples de code et des détails d’implémentation pour les composants Fluent UI utilisés pour créer des expériences Teams utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fc746-183">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc746-184">Essayer Teams composants d’interface utilisateur (interface utilisateur Fluent)</span><span class="sxs-lookup"><span data-stu-id="fc746-184">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="fc746-185">Concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fc746-185">Adaptive Cards designer</span></span>

<span data-ttu-id="fc746-186">Concevez des cartes adaptatives dans notre outil web.</span><span class="sxs-lookup"><span data-stu-id="fc746-186">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc746-187">Essayer le concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fc746-187">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
