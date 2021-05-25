---
title: Conception de votre application personnalisée
author: heath-hamilton
description: Découvrez comment concevoir des Microsoft Teams applications. Les ressources incluent le kit Microsoft Teams’interface utilisateur, les meilleures pratiques, les exemples et bien plus encore.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 19b8f8cbcbc52aa02ccd5d94f5bc4c088f2ae28a
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644874"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="29ed7-104">Conception de votre application Microsoft Teams web</span><span class="sxs-lookup"><span data-stu-id="29ed7-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Image conceptuelle présentant les recommandations Microsoft Teams conception.":::

<span data-ttu-id="29ed7-106">Que vous êtes concepteur, chef de produit, développeur ou fabricant à l’aide d’outils à code faible, ces instructions peuvent vous aider à prendre rapidement les bonnes décisions en matière de conception pour Microsoft Teams application.</span><span class="sxs-lookup"><span data-stu-id="29ed7-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="29ed7-107">Création d’une expérience cohérente</span><span class="sxs-lookup"><span data-stu-id="29ed7-107">Creating a cohesive experience</span></span>

<span data-ttu-id="29ed7-108">Concevoir une application Teams s’approche de la conception d’une application web conventionnelle, mais également un peu différente.</span><span class="sxs-lookup"><span data-stu-id="29ed7-108">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="29ed7-109">Une conception efficace met en évidence les attributs uniques de votre application tout en s’ajustant naturellement Teams fonctionnalités et contextes.</span><span class="sxs-lookup"><span data-stu-id="29ed7-109">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="29ed7-110">Ces recommandations et ressources peuvent vous aider à trouver cet équilibre.</span><span class="sxs-lookup"><span data-stu-id="29ed7-110">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="29ed7-111">Vous savez ce qu’il faut faire et ce qu’il faut éviter lors de la conception de votre application Teams (par exemple, navigation à plusieurs niveaux dans un onglet).</span><span class="sxs-lookup"><span data-stu-id="29ed7-111">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="29ed7-112">Teams de conception d’application</span><span class="sxs-lookup"><span data-stu-id="29ed7-112">Teams app design principles</span></span>

<span data-ttu-id="29ed7-113">Teams applications permettent aux gens de s’améliorer ensemble.</span><span class="sxs-lookup"><span data-stu-id="29ed7-113">Teams apps help people achieve more together.</span></span> <span data-ttu-id="29ed7-114">Utilisez ces principes pour guider votre conception.</span><span class="sxs-lookup"><span data-stu-id="29ed7-114">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="29ed7-115">Collaboration</span><span class="sxs-lookup"><span data-stu-id="29ed7-115">Collaborative</span></span>

<span data-ttu-id="29ed7-116">Teams applications permettent aux gens de s’améliorer ensemble.</span><span class="sxs-lookup"><span data-stu-id="29ed7-116">Teams apps help people achieve more together.</span></span> <span data-ttu-id="29ed7-117">Utilisez ces principes pour guider votre conception.</span><span class="sxs-lookup"><span data-stu-id="29ed7-117">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="29ed7-118">Fiable</span><span class="sxs-lookup"><span data-stu-id="29ed7-118">Trustworthy</span></span>

<span data-ttu-id="29ed7-119">L’application est sécurisée et conforme.</span><span class="sxs-lookup"><span data-stu-id="29ed7-119">The app is secure and compliant.</span></span> <span data-ttu-id="29ed7-120">Les utilisateurs peuvent facilement trouver des informations sur la confidentialité.</span><span class="sxs-lookup"><span data-stu-id="29ed7-120">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="29ed7-121">Globalement inclusive</span><span class="sxs-lookup"><span data-stu-id="29ed7-121">Globally inclusive</span></span>

<span data-ttu-id="29ed7-122">Les personnes de tous horizons, de tous les compétences et de toutes les disciplines peuvent utiliser l’application.</span><span class="sxs-lookup"><span data-stu-id="29ed7-122">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="29ed7-123">Il s’agit d’une approche culturelle, culturelle et sociale.</span><span class="sxs-lookup"><span data-stu-id="29ed7-123">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="29ed7-124">Light</span><span class="sxs-lookup"><span data-stu-id="29ed7-124">Light</span></span>

<span data-ttu-id="29ed7-125">L’application se concentre sur les scénarios principaux qui se fondent avec Teams flux de travail.</span><span class="sxs-lookup"><span data-stu-id="29ed7-125">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="29ed7-126">Natif ou distinct</span><span class="sxs-lookup"><span data-stu-id="29ed7-126">Native or distinct</span></span>

<span data-ttu-id="29ed7-127">L’application utilise des composants Teams de conception natifs ou les vôtres.</span><span class="sxs-lookup"><span data-stu-id="29ed7-127">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="29ed7-128">Il n’existe aucun mélange de modèles de couleurs, de contrôles, etc.</span><span class="sxs-lookup"><span data-stu-id="29ed7-128">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="29ed7-129">Utile</span><span class="sxs-lookup"><span data-stu-id="29ed7-129">Useful</span></span>

<span data-ttu-id="29ed7-130">L’application est basée sur un scénario que les personnes doivent faire dans Teams.</span><span class="sxs-lookup"><span data-stu-id="29ed7-130">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="29ed7-131">Facile à utiliser</span><span class="sxs-lookup"><span data-stu-id="29ed7-131">Easy to use</span></span>

<span data-ttu-id="29ed7-132">L’interface utilisateur est facile à comprendre, agréable dans l’apparence et le ton et rend les utilisateurs plus productifs.</span><span class="sxs-lookup"><span data-stu-id="29ed7-132">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="29ed7-133">Réactive</span><span class="sxs-lookup"><span data-stu-id="29ed7-133">Responsive</span></span>

<span data-ttu-id="29ed7-134">L’application est sans appareil et sans écran.</span><span class="sxs-lookup"><span data-stu-id="29ed7-134">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="29ed7-135">Accessible</span><span class="sxs-lookup"><span data-stu-id="29ed7-135">Accessible</span></span>

<span data-ttu-id="29ed7-136">L’application répond Teams exigences d’accessibilité en termes de contraste de couleur, d’alternatives de navigation et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="29ed7-136">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="29ed7-137">Bien décrit</span><span class="sxs-lookup"><span data-stu-id="29ed7-137">Well described</span></span>

<span data-ttu-id="29ed7-138">Le texte, les icônes et les images montrent clairement à quoi l’application s’utilise et comment l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="29ed7-138">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a><span data-ttu-id="29ed7-139">Teams de conception</span><span class="sxs-lookup"><span data-stu-id="29ed7-139">Teams design system</span></span>

<span data-ttu-id="29ed7-140">Découvrez les [principes de base de Teams conception d’application,](design-teams-app-fundamentals.md)notamment la disposition, les modèles de couleurs, etc.</span><span class="sxs-lookup"><span data-stu-id="29ed7-140">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="29ed7-141">Fonctionnalités de l’application</span><span class="sxs-lookup"><span data-stu-id="29ed7-141">App capabilities</span></span>

<span data-ttu-id="29ed7-142">Comprendre comment les personnes ajoutent, utilisent et gèrent Teams applications pour utiliser au mieux chaque fonctionnalité de votre conception.</span><span class="sxs-lookup"><span data-stu-id="29ed7-142">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="29ed7-143">Applications personnelles</span><span class="sxs-lookup"><span data-stu-id="29ed7-143">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="29ed7-144">Onglets</span><span class="sxs-lookup"><span data-stu-id="29ed7-144">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="29ed7-145">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="29ed7-145">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="29ed7-146">Bots</span><span class="sxs-lookup"><span data-stu-id="29ed7-146">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="29ed7-147">Extensions de réunion</span><span class="sxs-lookup"><span data-stu-id="29ed7-147">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a><span data-ttu-id="29ed7-148">Modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="29ed7-148">UI templates</span></span>

<span data-ttu-id="29ed7-149">Créez rapidement des conceptions complexes et haute fidélité avec des modèles pour les Teams et les flux [de travail.](design-teams-app-ui-templates.md)</span><span class="sxs-lookup"><span data-stu-id="29ed7-149">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="basic-ui-components"></a><span data-ttu-id="29ed7-150">Composants d’interface utilisateur de base</span><span class="sxs-lookup"><span data-stu-id="29ed7-150">Basic UI components</span></span>

<span data-ttu-id="29ed7-151">Basés sur l’interface utilisateur [](design-teams-app-basic-ui-components.md) Fluent, voici les principaux éléments que vous pouvez utiliser pour créer Teams expériences à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="29ed7-151">Based on Fluent UI, these are the [core elements](design-teams-app-basic-ui-components.md) you can use to create Teams experiences from scratch.</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="29ed7-152">Outils et exemples</span><span class="sxs-lookup"><span data-stu-id="29ed7-152">Tools and samples</span></span>

<span data-ttu-id="29ed7-153">Les outils suivants peuvent aider les concepteurs et les développeurs à démarrer :</span><span class="sxs-lookup"><span data-stu-id="29ed7-153">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="29ed7-154">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="29ed7-154">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="29ed7-155">Concevez une Teams avec des composants d’interface utilisateur, des modèles et des exemples que vous pouvez faire glisser, déposer et modifier selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="29ed7-155">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="29ed7-156">Le kit d’interface utilisateur inclut également des informations complètes sur l’apparence et le comportement des applications dans différents Teams scénarios.</span><span class="sxs-lookup"><span data-stu-id="29ed7-156">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29ed7-157">Obtenir le kit d’interface utilisateur (Figma)</span><span class="sxs-lookup"><span data-stu-id="29ed7-157">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="29ed7-158">Microsoft Teams Bibliothèque d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="29ed7-158">Microsoft Teams UI Library</span></span>

<span data-ttu-id="29ed7-159">Affichez et testez les Teams d’interface utilisateur et les composants associés dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="29ed7-159">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29ed7-160">Essayer la bibliothèque d’interface utilisateur (aire de jeu)</span><span class="sxs-lookup"><span data-stu-id="29ed7-160">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="29ed7-161">Importez ces modèles et composants associés directement dans Teams projet d’application.</span><span class="sxs-lookup"><span data-stu-id="29ed7-161">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29ed7-162">Obtenir la bibliothèque d’interface utilisateur (GitHub)</span><span class="sxs-lookup"><span data-stu-id="29ed7-162">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="29ed7-163">Exemple d’application</span><span class="sxs-lookup"><span data-stu-id="29ed7-163">Sample app</span></span>

<span data-ttu-id="29ed7-164">Vous pouvez télécharger un exemple d’application pour voir l’apparence et le comportement des applications dans Teams client.</span><span class="sxs-lookup"><span data-stu-id="29ed7-164">You can upload a sample app to see how apps should look and behave in the Teams client.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29ed7-165">Obtenir l’exemple d’application (GitHub)</span><span class="sxs-lookup"><span data-stu-id="29ed7-165">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="29ed7-166">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="29ed7-166">Other resources</span></span>

<span data-ttu-id="29ed7-167">Pour en savoir plus, essayez l’une des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="29ed7-167">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="29ed7-168">Documentation de l’interface utilisateur Fluent</span><span class="sxs-lookup"><span data-stu-id="29ed7-168">Fluent UI documentation</span></span>

<span data-ttu-id="29ed7-169">Obtenez des exemples de code et des détails d’implémentation pour les composants d’interface utilisateur Fluent de base utilisés pour créer Teams expériences utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29ed7-169">Get code samples and implementation details for the basic Fluent UI components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29ed7-170">Essayer Teams composants d’interface utilisateur (interface utilisateur Fluent)</span><span class="sxs-lookup"><span data-stu-id="29ed7-170">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="29ed7-171">Concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="29ed7-171">Adaptive Cards designer</span></span>

<span data-ttu-id="29ed7-172">Concevez des cartes adaptatives dans notre outil web.</span><span class="sxs-lookup"><span data-stu-id="29ed7-172">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29ed7-173">Essayer le concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="29ed7-173">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
