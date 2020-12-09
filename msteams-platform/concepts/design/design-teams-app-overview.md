---
title: Conception de votre application personnalisée
author: heath-hamilton
description: Découvrez comment concevoir des applications Microsoft Teams. Les ressources incluent le kit d’interface utilisateur Microsoft Teams, les meilleures pratiques, des exemples et plus encore.
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0160a59ed4ebc51e900acbb5d74735ccae0b6083
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605872"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="7e3ce-104">Conception de votre application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="7e3ce-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Image conceptuelle présentant les instructions de conception de Microsoft Teams.":::

<span data-ttu-id="7e3ce-106">Que vous soyez un concepteur, un responsable de produit, un développeur ou un fabricant utilisant des outils à faible code, ces instructions peuvent vous aider à prendre les bonnes décisions de conception pour votre application Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="7e3ce-107">Principes de conception des applications teams</span><span class="sxs-lookup"><span data-stu-id="7e3ce-107">Teams app design principles</span></span>

<span data-ttu-id="7e3ce-108">Les applications teams aident les utilisateurs à travailler ensemble.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="7e3ce-109">Utilisez ces principes pour vous aider dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="7e3ce-110">Partagée</span><span class="sxs-lookup"><span data-stu-id="7e3ce-110">Collaborative</span></span>

<span data-ttu-id="7e3ce-111">Les applications teams aident les utilisateurs à travailler ensemble.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="7e3ce-112">Utilisez ces principes pour vous aider dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="7e3ce-113">Sûre</span><span class="sxs-lookup"><span data-stu-id="7e3ce-113">Trustworthy</span></span>

<span data-ttu-id="7e3ce-114">L’application est sécurisée et conforme.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-114">The app is secure and compliant.</span></span> <span data-ttu-id="7e3ce-115">Les utilisateurs peuvent facilement trouver des informations sur la confidentialité.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="7e3ce-116">Globalement inclusif</span><span class="sxs-lookup"><span data-stu-id="7e3ce-116">Globally inclusive</span></span>

<span data-ttu-id="7e3ce-117">Les personnes de tous les arrière-plans, skillsets et disciplines peuvent utiliser l’application.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="7e3ce-118">Il s’agit d’un service culturel, racial ou social.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="7e3ce-119">Light</span><span class="sxs-lookup"><span data-stu-id="7e3ce-119">Light</span></span>

<span data-ttu-id="7e3ce-120">L’application se concentre sur les scénarios principaux qui fusionnent avec les flux de travail Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="7e3ce-121">Natif ou distinct</span><span class="sxs-lookup"><span data-stu-id="7e3ce-121">Native or distinct</span></span>

<span data-ttu-id="7e3ce-122">L’application utilise les composants de conception teams natifs ou vous-même.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="7e3ce-123">Il n’y a pas de mélange de jeux de couleurs, de contrôles, etc.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="7e3ce-124">Utile</span><span class="sxs-lookup"><span data-stu-id="7e3ce-124">Useful</span></span>

<span data-ttu-id="7e3ce-125">L’application est basée sur un scénario que les utilisateurs doivent faire dans Teams.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="7e3ce-126">Facile à utiliser</span><span class="sxs-lookup"><span data-stu-id="7e3ce-126">Easy to use</span></span>

<span data-ttu-id="7e3ce-127">L’interface utilisateur est facile à comprendre, agréable en apparence et ton et rend les personnes plus productives.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="7e3ce-128">Réactive</span><span class="sxs-lookup"><span data-stu-id="7e3ce-128">Responsive</span></span>

<span data-ttu-id="7e3ce-129">L’application est indépendante de l’écran et de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="7e3ce-130">Accessible</span><span class="sxs-lookup"><span data-stu-id="7e3ce-130">Accessible</span></span>

<span data-ttu-id="7e3ce-131">L’application répond aux exigences en matière d’accessibilité de teams en termes de contraste de couleur, alternatives de navigation et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="7e3ce-132">Bien décrit</span><span class="sxs-lookup"><span data-stu-id="7e3ce-132">Well described</span></span>

<span data-ttu-id="7e3ce-133">Le texte, les icônes et les images permettent de clarifier l’objet de l’application et son utilisation.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="7e3ce-134">Création d’une expérience cohésive</span><span class="sxs-lookup"><span data-stu-id="7e3ce-134">Creating a cohesive experience</span></span>

<span data-ttu-id="7e3ce-135">La conception d’une application de teams est similaire à la conception d’une application Web conventionnelle, mais également légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="7e3ce-136">Une conception efficace met en évidence les attributs uniques de votre application tout en raccordant naturellement aux fonctionnalités et contextes de teams.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="7e3ce-137">Ces instructions et ressources peuvent vous aider à suivre ce bilan.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="7e3ce-138">Vous saurez ce que vous devez faire et ce qu’il faut éviter lors de la conception de votre application Teams (par exemple, navigation sur plusieurs niveaux dans un onglet).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="7e3ce-139">Planification de votre application</span><span class="sxs-lookup"><span data-stu-id="7e3ce-139">Planning your app</span></span>

<span data-ttu-id="7e3ce-140">Pour concevoir une application teams de grande qualité, vous devez d’abord comprendre ce que vous souhaitez que votre application effectue et comment vous pensez que les utilisateurs l’utiliseront.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="7e3ce-141">Si ce n’est pas déjà fait, prenez le temps de [planifier correctement votre application](../../concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="7e3ce-142">Principes de base de conception</span><span class="sxs-lookup"><span data-stu-id="7e3ce-142">Design fundamentals</span></span>

<span data-ttu-id="7e3ce-143">Découvrez la [conception d’applications de base](design-teams-app-fundamentals.md), notamment la disposition, les modèles de couleurs et plus encore.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="7e3ce-144">Composants de base de l’interface utilisateur Fluent pour teams</span><span class="sxs-lookup"><span data-stu-id="7e3ce-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="7e3ce-145">En fonction de l’interface utilisateur Fluent, il s’agit des [éléments principaux permettant de créer des interfaces familières teams](design-teams-app-basic-ui-components.md).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="7e3ce-146">Fonctionnalités de l’application</span><span class="sxs-lookup"><span data-stu-id="7e3ce-146">App capabilities</span></span>

<span data-ttu-id="7e3ce-147">Découvrez comment les utilisateurs ajoutent, utilisent et gèrent les applications teams pour tirer le meilleur parti de chaque fonctionnalité de votre conception.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-147">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="7e3ce-148">Applications personnelles</span><span class="sxs-lookup"><span data-stu-id="7e3ce-148">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="7e3ce-149">Onglets</span><span class="sxs-lookup"><span data-stu-id="7e3ce-149">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="7e3ce-150">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e3ce-150">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="7e3ce-151">Bots</span><span class="sxs-lookup"><span data-stu-id="7e3ce-151">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="7e3ce-152">Extensions de la réunion</span><span class="sxs-lookup"><span data-stu-id="7e3ce-152">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="7e3ce-153">Modules de tâche</span><span class="sxs-lookup"><span data-stu-id="7e3ce-153">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="7e3ce-154">Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7e3ce-154">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="ui-templates"></a><span data-ttu-id="7e3ce-155">Modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7e3ce-155">UI templates</span></span>

<span data-ttu-id="7e3ce-156">Créez rapidement des conceptions complexes de haute fidélité avec des [modèles pour les cas d’utilisation et les flux de travail de teams courants](design-teams-app-ui-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-156">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="get-started-with-the-microsoft-teams-ui-kit"></a><span data-ttu-id="7e3ce-157">Prise en main du kit d’interface utilisateur Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="7e3ce-157">Get started with the Microsoft Teams UI Kit</span></span>

<span data-ttu-id="7e3ce-158">Le kit d’interface utilisateur Microsoft teams comporte des composants de l’interface utilisateur, des modèles et des exemples que vous pouvez faire glisser, déplacer et modifier selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-158">The Microsoft Teams UI Kit has UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="7e3ce-159">Le kit d’interface utilisateur comprend également des informations complètes sur l’apparence et le comportement des applications dans différents scénarios de teams.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-159">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7e3ce-160">Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="7e3ce-160">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="other-resources"></a><span data-ttu-id="7e3ce-161">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="7e3ce-161">Other resources</span></span>

<span data-ttu-id="7e3ce-162">Pour en savoir plus, essayez l’une des ressources suivantes.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-162">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui"></a><span data-ttu-id="7e3ce-163">Interface utilisateur Fluent</span><span class="sxs-lookup"><span data-stu-id="7e3ce-163">Fluent UI</span></span>

<span data-ttu-id="7e3ce-164">Obtenez des exemples de code et des détails d’implémentation pour les composants de l’interface utilisateur Fluent utilisés pour créer des expériences de teams.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-164">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7e3ce-165">Essayer les composants de l’interface utilisateur de Teams (interface utilisateur Fluent)</span><span class="sxs-lookup"><span data-stu-id="7e3ce-165">Try out Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="7e3ce-166">Concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7e3ce-166">Adaptive Cards designer</span></span>

<span data-ttu-id="7e3ce-167">Concevoir des cartes adaptatives dans un outil basé sur le Web.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-167">Design Adaptive Cards in a web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7e3ce-168">Essayer le concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7e3ce-168">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
