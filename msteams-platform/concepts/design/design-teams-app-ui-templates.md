---
title: Conception de votre application avec des modèles d’interface utilisateur
author: heath-hamilton
description: Concevez votre application plus rapidement avec des composants d’interface utilisateur, des dispositions et des modèles standardisés fréquemment visibles dans Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 5026554070396dcc55390496b6754961e8e037bc
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644815"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="7c18a-103">Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7c18a-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="7c18a-104">Concevez votre application Microsoft Teams plus rapidement avec des modèles d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7c18a-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="7c18a-105">Les modèles sont une collection de composants fluent basés sur l’interface utilisateur qui fonctionnent dans les cas d’utilisation courants Teams, ce qui vous donne plus de temps pour déterminer la meilleure expérience pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7c18a-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="7c18a-106">Mise en place des outils et des exemples</span><span class="sxs-lookup"><span data-stu-id="7c18a-106">Getting started with tools and samples</span></span>

<span data-ttu-id="7c18a-107">Les ressources suivantes peuvent vous aider à concevoir et développer votre application à l’aide de modèles d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7c18a-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="7c18a-108">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7c18a-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="7c18a-109">Récupérer des modèles d’interface utilisateur pour la conception de votre application à partir du kit d’interface utilisateur Microsoft Teams, qui inclut également des informations complètes sur l’utilisation, l’anatomie, l’accessibilité et les meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="7c18a-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c18a-110">Obtenir le kit d’interface utilisateur (Figma)</span><span class="sxs-lookup"><span data-stu-id="7c18a-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="7c18a-111">Microsoft Teams Bibliothèque d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7c18a-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="7c18a-112">Affichez et testez les Teams d’interface utilisateur et les composants associés dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="7c18a-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c18a-113">Essayer la bibliothèque d’interface utilisateur (aire de jeu)</span><span class="sxs-lookup"><span data-stu-id="7c18a-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="7c18a-114">Importez ces modèles et composants associés directement dans Teams projet d’application.</span><span class="sxs-lookup"><span data-stu-id="7c18a-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c18a-115">Obtenir la bibliothèque d’interface utilisateur (GitHub)</span><span class="sxs-lookup"><span data-stu-id="7c18a-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="7c18a-116">Exemple d’application</span><span class="sxs-lookup"><span data-stu-id="7c18a-116">Sample app</span></span>

<span data-ttu-id="7c18a-117">Installez un exemple d’application pour voir l’apparence et le comportement des modèles d’interface utilisateur Teams contextes.</span><span class="sxs-lookup"><span data-stu-id="7c18a-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c18a-118">Obtenir l’exemple d’application (GitHub)</span><span class="sxs-lookup"><span data-stu-id="7c18a-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a><span data-ttu-id="7c18a-119">Tableau de bord</span><span class="sxs-lookup"><span data-stu-id="7c18a-119">Dashboard</span></span>

<span data-ttu-id="7c18a-120">Un tableau de bord affiche différents types de contenu dans un emplacement central (Teams application ou onglet personnel).</span><span class="sxs-lookup"><span data-stu-id="7c18a-120">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="7c18a-121">Les utilisateurs doivent pouvoir personnaliser au moins une partie de ce qu’ils voient sur un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="7c18a-121">Users should be able to customize at least some of what they see on a dashboard.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7c18a-122">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7c18a-122">Top use cases</span></span>

* <span data-ttu-id="7c18a-123">Analyser les données</span><span class="sxs-lookup"><span data-stu-id="7c18a-123">Analyze data</span></span>
* <span data-ttu-id="7c18a-124">Mesures du rapport</span><span class="sxs-lookup"><span data-stu-id="7c18a-124">Report metrics</span></span>
* <span data-ttu-id="7c18a-125">Organiser différentes informations au même endroit</span><span class="sxs-lookup"><span data-stu-id="7c18a-125">Organize different information in one place</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7c18a-126">Desktop</span><span class="sxs-lookup"><span data-stu-id="7c18a-126">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="L’exemple montre un modèle d’interface utilisateur de tableau de bord sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7c18a-128">Mobile</span><span class="sxs-lookup"><span data-stu-id="7c18a-128">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="L’exemple montre un modèle d’interface utilisateur de tableau de bord sur mobile." border="false":::

---

## <a name="data-visualization"></a><span data-ttu-id="7c18a-130">Visualisation de données</span><span class="sxs-lookup"><span data-stu-id="7c18a-130">Data visualization</span></span>

<span data-ttu-id="7c18a-131">Vous pouvez utiliser différentes tailles de carte (unique, double et complète) pour empiler et organiser les visualisations de données sur la même page.</span><span class="sxs-lookup"><span data-stu-id="7c18a-131">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="7c18a-132">Les cartes s’adaptent à la disposition des colonnes et remplissent des espaces vides.</span><span class="sxs-lookup"><span data-stu-id="7c18a-132">The cards scale to fit the column layout and fill in blank spaces.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7c18a-133">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7c18a-133">Top use cases</span></span>

* <span data-ttu-id="7c18a-134">Afficher des informations complexes</span><span class="sxs-lookup"><span data-stu-id="7c18a-134">Display complex information</span></span>
* <span data-ttu-id="7c18a-135">Créer un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="7c18a-135">Create a dashboard</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7c18a-136">Desktop</span><span class="sxs-lookup"><span data-stu-id="7c18a-136">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="L’exemple illustre un modèle d’interface utilisateur de visualisation de données sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7c18a-138">Mobile</span><span class="sxs-lookup"><span data-stu-id="7c18a-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="L’exemple montre un modèle d’interface utilisateur de visualisation de données sur un appareil mobile." border="false":::

---

## <a name="empty-state"></a><span data-ttu-id="7c18a-140">État vide</span><span class="sxs-lookup"><span data-stu-id="7c18a-140">Empty state</span></span>

<span data-ttu-id="7c18a-141">Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="7c18a-141">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="7c18a-142">Il est très flexible : adaptez-le pour utiliser un, quelques-uns ou tous les composants de la conception suivante.</span><span class="sxs-lookup"><span data-stu-id="7c18a-142">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7c18a-143">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7c18a-143">Top use cases</span></span>

* <span data-ttu-id="7c18a-144">Se connecter</span><span class="sxs-lookup"><span data-stu-id="7c18a-144">Sign in</span></span>
* <span data-ttu-id="7c18a-145">Messages de bienvenue et expériences de première expérience</span><span class="sxs-lookup"><span data-stu-id="7c18a-145">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="7c18a-146">Messages de réussite</span><span class="sxs-lookup"><span data-stu-id="7c18a-146">Success messages</span></span>
* <span data-ttu-id="7c18a-147">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="7c18a-147">Error messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7c18a-148">Desktop</span><span class="sxs-lookup"><span data-stu-id="7c18a-148">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7c18a-150">Mobile</span><span class="sxs-lookup"><span data-stu-id="7c18a-150">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide sur mobile." border="false":::

---

## <a name="filter"></a><span data-ttu-id="7c18a-152">Filtre</span><span class="sxs-lookup"><span data-stu-id="7c18a-152">Filter</span></span>

<span data-ttu-id="7c18a-153">Un filtre vous permet de réduire les informations que vous voyez en fonction des critères sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="7c18a-153">A filter allows you to reduce the information you see based on the criteria selected.</span></span> <span data-ttu-id="7c18a-154">Vous pouvez inclure des filtres avec des tableaux, des listes, des cartes et d’autres composants qui organisent le contenu.</span><span class="sxs-lookup"><span data-stu-id="7c18a-154">You can include filters with tables, lists, cards, and other components that organize content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7c18a-155">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7c18a-155">Top use cases</span></span>

<span data-ttu-id="7c18a-156">Organisation du contenu dans :</span><span class="sxs-lookup"><span data-stu-id="7c18a-156">Organizing content in:</span></span>

* <span data-ttu-id="7c18a-157">Listes</span><span class="sxs-lookup"><span data-stu-id="7c18a-157">Lists</span></span>
* <span data-ttu-id="7c18a-158">Tables</span><span class="sxs-lookup"><span data-stu-id="7c18a-158">Tables</span></span>
* <span data-ttu-id="7c18a-159">Tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="7c18a-159">Dashboards</span></span>
* <span data-ttu-id="7c18a-160">Visualisation de données</span><span class="sxs-lookup"><span data-stu-id="7c18a-160">Data visualization</span></span>

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="Exemple de modèle de filtre." border="false":::

## <a name="form"></a><span data-ttu-id="7c18a-162">Formulaire</span><span class="sxs-lookup"><span data-stu-id="7c18a-162">Form</span></span>

<span data-ttu-id="7c18a-163">Les formulaires sont utilisés pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="7c18a-163">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="7c18a-164">Effacer l’étiquetage et les regroupements logiques de champs d’entrée sont essentiels pour une bonne expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7c18a-164">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7c18a-165">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7c18a-165">Top use cases</span></span>

* <span data-ttu-id="7c18a-166">Se connecter</span><span class="sxs-lookup"><span data-stu-id="7c18a-166">Sign in</span></span>
* <span data-ttu-id="7c18a-167">Profils utilisateur</span><span class="sxs-lookup"><span data-stu-id="7c18a-167">User profiles</span></span>
* <span data-ttu-id="7c18a-168">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7c18a-168">Settings</span></span>
* <span data-ttu-id="7c18a-169">Collection d’entrées utilisateur</span><span class="sxs-lookup"><span data-stu-id="7c18a-169">User input collection</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7c18a-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="7c18a-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="L’exemple montre un modèle d’interface utilisateur de formulaire sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7c18a-172">Mobile</span><span class="sxs-lookup"><span data-stu-id="7c18a-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="L’exemple montre un modèle d’interface utilisateur de formulaire sur mobile." border="false":::

---

## <a name="list"></a><span data-ttu-id="7c18a-174">Répertorier</span><span class="sxs-lookup"><span data-stu-id="7c18a-174">List</span></span>

<span data-ttu-id="7c18a-175">Vous pouvez utiliser une liste pour afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="7c18a-175">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7c18a-176">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7c18a-176">Top use cases</span></span>

* <span data-ttu-id="7c18a-177">Afficher les données</span><span class="sxs-lookup"><span data-stu-id="7c18a-177">Display data</span></span>
* <span data-ttu-id="7c18a-178">Actions contextuelles sur le contenu de l’application</span><span class="sxs-lookup"><span data-stu-id="7c18a-178">Contextual actions on app content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7c18a-179">Desktop</span><span class="sxs-lookup"><span data-stu-id="7c18a-179">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="L’exemple montre un modèle d’interface utilisateur de liste sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7c18a-181">Mobile</span><span class="sxs-lookup"><span data-stu-id="7c18a-181">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="L’exemple montre un modèle d’interface utilisateur de liste sur mobile." border="false":::

---

## <a name="sign-in"></a><span data-ttu-id="7c18a-183">Se connecter</span><span class="sxs-lookup"><span data-stu-id="7c18a-183">Sign in</span></span>

<span data-ttu-id="7c18a-184">Vous pouvez concevoir des flux de Teams d’application pour différents contextes et fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="7c18a-184">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="7c18a-185">L’exemple suivant inclut l’authentification unique (SSO), que nous recommandons pour l’expérience d’authentification la plus simple.</span><span class="sxs-lookup"><span data-stu-id="7c18a-185">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

### <a name="top-use-case"></a><span data-ttu-id="7c18a-186">Cas d’utilisation principaux</span><span class="sxs-lookup"><span data-stu-id="7c18a-186">Top use case</span></span>

* <span data-ttu-id="7c18a-187">Authentifier les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="7c18a-187">Authenticate users</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7c18a-188">Desktop</span><span class="sxs-lookup"><span data-stu-id="7c18a-188">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de la signature sur le bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7c18a-190">Mobile</span><span class="sxs-lookup"><span data-stu-id="7c18a-190">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de la signature sur un appareil mobile." border="false":::

---

## <a name="settings"></a><span data-ttu-id="7c18a-192">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7c18a-192">Settings</span></span>

<span data-ttu-id="7c18a-193">Paramètres sont les écrans où les utilisateurs peuvent configurer leurs préférences avec votre application.</span><span class="sxs-lookup"><span data-stu-id="7c18a-193">Settings screens are where users can configure their preferences with your app.</span></span> <span data-ttu-id="7c18a-194">(Remarque : Paramètres est un conteneur pour les [composants d’interface utilisateur de base.)](~/concepts/design/design-teams-app-basic-ui-components.md)</span><span class="sxs-lookup"><span data-stu-id="7c18a-194">(Note: Settings is a container for [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md).)</span></span>

### <a name="top-use-case"></a><span data-ttu-id="7c18a-195">Cas d’utilisation principaux</span><span class="sxs-lookup"><span data-stu-id="7c18a-195">Top use case</span></span>

* <span data-ttu-id="7c18a-196">Gérer les fonctionnalités de l’application</span><span class="sxs-lookup"><span data-stu-id="7c18a-196">Manage app features</span></span>

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="L’exemple montre un modèle de paramètres." border="false":::

## <a name="task-board"></a><span data-ttu-id="7c18a-198">Tableau des tâches</span><span class="sxs-lookup"><span data-stu-id="7c18a-198">Task board</span></span>

<span data-ttu-id="7c18a-199">Un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="7c18a-199">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="7c18a-200">Il peut également être utilisé pour trier n’importe quel type de contenu en catégories.</span><span class="sxs-lookup"><span data-stu-id="7c18a-200">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="7c18a-201">Vous pouvez modifier et déplacer les cartes entre les colonnes.</span><span class="sxs-lookup"><span data-stu-id="7c18a-201">You can edit and move the cards between columns.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7c18a-202">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7c18a-202">Top use cases</span></span>

* <span data-ttu-id="7c18a-203">Gestion de projet.</span><span class="sxs-lookup"><span data-stu-id="7c18a-203">Project management.</span></span> <span data-ttu-id="7c18a-204">Affectation de tâches et état de suivi</span><span class="sxs-lookup"><span data-stu-id="7c18a-204">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="7c18a-205">Brainstorming.</span><span class="sxs-lookup"><span data-stu-id="7c18a-205">Brainstorming.</span></span> <span data-ttu-id="7c18a-206">Ajout d’idées dans différentes catégories</span><span class="sxs-lookup"><span data-stu-id="7c18a-206">Adding ideas in different categories</span></span>
* <span data-ttu-id="7c18a-207">Exercices de tri.</span><span class="sxs-lookup"><span data-stu-id="7c18a-207">Sorting exercises.</span></span> <span data-ttu-id="7c18a-208">Organisation de n’importe quel type d’informations dans des compartiments</span><span class="sxs-lookup"><span data-stu-id="7c18a-208">Organizing any kind of information into buckets</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7c18a-209">Desktop</span><span class="sxs-lookup"><span data-stu-id="7c18a-209">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="L’exemple montre un modèle d’interface utilisateur du tableau des tâches sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7c18a-211">Mobile</span><span class="sxs-lookup"><span data-stu-id="7c18a-211">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="L’exemple montre un modèle d’interface utilisateur du tableau des tâches sur mobile." border="false":::

---

## <a name="wizard"></a><span data-ttu-id="7c18a-213">Assistant</span><span class="sxs-lookup"><span data-stu-id="7c18a-213">Wizard</span></span>

<span data-ttu-id="7c18a-214">Un Assistant guide un utilisateur à travers plusieurs écrans pour effectuer une tâche (par exemple, un processus d’installation).</span><span class="sxs-lookup"><span data-stu-id="7c18a-214">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7c18a-215">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7c18a-215">Top use cases</span></span>

* <span data-ttu-id="7c18a-216">Configuration</span><span class="sxs-lookup"><span data-stu-id="7c18a-216">Setup</span></span>
* <span data-ttu-id="7c18a-217">Intégration</span><span class="sxs-lookup"><span data-stu-id="7c18a-217">Onboarding</span></span>
* <span data-ttu-id="7c18a-218">Expériences de première expérience</span><span class="sxs-lookup"><span data-stu-id="7c18a-218">First-run experiences</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7c18a-219">Desktop</span><span class="sxs-lookup"><span data-stu-id="7c18a-219">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="Un exemple illustre un modèle d’interface utilisateur d’Assistant sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7c18a-221">Mobile</span><span class="sxs-lookup"><span data-stu-id="7c18a-221">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’assistant sur mobile." border="false":::

---
