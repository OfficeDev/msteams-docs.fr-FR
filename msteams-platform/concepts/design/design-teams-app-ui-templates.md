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
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="7ed40-103">Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7ed40-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="7ed40-104">Concevez votre application Microsoft Teams plus rapidement avec des modèles d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7ed40-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="7ed40-105">Les modèles sont une collection de composants fluent basés sur l’interface utilisateur qui fonctionnent dans les cas d’utilisation courants Teams, ce qui vous donne plus de temps pour déterminer la meilleure expérience pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7ed40-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="7ed40-106">Mise en place d’outils et d’exemples</span><span class="sxs-lookup"><span data-stu-id="7ed40-106">Getting started with tools and samples</span></span>

<span data-ttu-id="7ed40-107">Les ressources suivantes peuvent vous aider à concevoir et développer votre application à l’aide de modèles d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7ed40-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="7ed40-108">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7ed40-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="7ed40-109">Récupérer des modèles d’interface utilisateur pour la conception de votre application à partir du kit d’interface utilisateur Microsoft Teams, qui inclut également des informations complètes sur l’utilisation, l’anatomie, l’accessibilité et les meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="7ed40-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ed40-110">Obtenir le kit d’interface utilisateur (Figma)</span><span class="sxs-lookup"><span data-stu-id="7ed40-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="7ed40-111">Microsoft Teams Bibliothèque d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7ed40-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="7ed40-112">Affichez et testez les Teams d’interface utilisateur et les composants associés dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="7ed40-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ed40-113">Essayer la bibliothèque d’interface utilisateur (aire de jeu)</span><span class="sxs-lookup"><span data-stu-id="7ed40-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="7ed40-114">Importez ces modèles et composants associés directement dans Teams projet d’application.</span><span class="sxs-lookup"><span data-stu-id="7ed40-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ed40-115">Obtenir la bibliothèque d’interface utilisateur (GitHub)</span><span class="sxs-lookup"><span data-stu-id="7ed40-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="7ed40-116">Exemple d’application</span><span class="sxs-lookup"><span data-stu-id="7ed40-116">Sample app</span></span>

<span data-ttu-id="7ed40-117">Installez un exemple d’application pour voir l’apparence et le comportement des modèles d’interface utilisateur Teams contextes.</span><span class="sxs-lookup"><span data-stu-id="7ed40-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ed40-118">Obtenir l’exemple d’application (GitHub)</span><span class="sxs-lookup"><span data-stu-id="7ed40-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a><span data-ttu-id="7ed40-119">Tableau de bord</span><span class="sxs-lookup"><span data-stu-id="7ed40-119">Dashboard</span></span>

<span data-ttu-id="7ed40-120">Un tableau de bord affiche différents types de contenu dans un emplacement central (Teams application ou onglet personnel).</span><span class="sxs-lookup"><span data-stu-id="7ed40-120">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="7ed40-121">Les utilisateurs doivent pouvoir personnaliser au moins une partie de ce qu’ils voient sur un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="7ed40-121">Users should be able to customize at least some of what they see on a dashboard.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7ed40-122">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7ed40-122">Top use cases</span></span>

* <span data-ttu-id="7ed40-123">Analyser les données</span><span class="sxs-lookup"><span data-stu-id="7ed40-123">Analyze data</span></span>
* <span data-ttu-id="7ed40-124">Mesures du rapport</span><span class="sxs-lookup"><span data-stu-id="7ed40-124">Report metrics</span></span>
* <span data-ttu-id="7ed40-125">Organiser différentes informations au même endroit</span><span class="sxs-lookup"><span data-stu-id="7ed40-125">Organize different information in one place</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7ed40-126">Desktop</span><span class="sxs-lookup"><span data-stu-id="7ed40-126">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="L’exemple montre un modèle d’interface utilisateur de tableau de bord sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7ed40-128">Mobile</span><span class="sxs-lookup"><span data-stu-id="7ed40-128">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="L’exemple montre un modèle d’interface utilisateur de tableau de bord sur mobile." border="false":::

---

## <a name="data-visualization"></a><span data-ttu-id="7ed40-130">Visualisation de données</span><span class="sxs-lookup"><span data-stu-id="7ed40-130">Data visualization</span></span>

<span data-ttu-id="7ed40-131">Vous pouvez utiliser différentes tailles de carte (unique, double et complète) pour empiler et organiser les visualisations de données sur la même page.</span><span class="sxs-lookup"><span data-stu-id="7ed40-131">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="7ed40-132">Les cartes s’adaptent à la disposition des colonnes et remplissent des espaces vides.</span><span class="sxs-lookup"><span data-stu-id="7ed40-132">The cards scale to fit the column layout and fill in blank spaces.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7ed40-133">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7ed40-133">Top use cases</span></span>

* <span data-ttu-id="7ed40-134">Afficher des informations complexes</span><span class="sxs-lookup"><span data-stu-id="7ed40-134">Display complex information</span></span>
* <span data-ttu-id="7ed40-135">Créer un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="7ed40-135">Create a dashboard</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7ed40-136">Desktop</span><span class="sxs-lookup"><span data-stu-id="7ed40-136">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="L’exemple illustre un modèle d’interface utilisateur de visualisation de données sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7ed40-138">Mobile</span><span class="sxs-lookup"><span data-stu-id="7ed40-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="L’exemple montre un modèle d’interface utilisateur de visualisation de données sur un appareil mobile." border="false":::

---

## <a name="empty-state"></a><span data-ttu-id="7ed40-140">État vide</span><span class="sxs-lookup"><span data-stu-id="7ed40-140">Empty state</span></span>

<span data-ttu-id="7ed40-141">Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="7ed40-141">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="7ed40-142">Il est très flexible : adaptez-le pour utiliser un, quelques-uns ou tous les composants de la conception suivante.</span><span class="sxs-lookup"><span data-stu-id="7ed40-142">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7ed40-143">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7ed40-143">Top use cases</span></span>

* <span data-ttu-id="7ed40-144">Se connecter</span><span class="sxs-lookup"><span data-stu-id="7ed40-144">Sign in</span></span>
* <span data-ttu-id="7ed40-145">Messages de bienvenue et expériences de première expérience</span><span class="sxs-lookup"><span data-stu-id="7ed40-145">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="7ed40-146">Messages de réussite</span><span class="sxs-lookup"><span data-stu-id="7ed40-146">Success messages</span></span>
* <span data-ttu-id="7ed40-147">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="7ed40-147">Error messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7ed40-148">Desktop</span><span class="sxs-lookup"><span data-stu-id="7ed40-148">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7ed40-150">Mobile</span><span class="sxs-lookup"><span data-stu-id="7ed40-150">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide sur mobile." border="false":::

---

## <a name="filter"></a><span data-ttu-id="7ed40-152">Filtre</span><span class="sxs-lookup"><span data-stu-id="7ed40-152">Filter</span></span>

<span data-ttu-id="7ed40-153">Un filtre vous permet de réduire les informations que vous voyez en fonction des critères sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="7ed40-153">A filter allows you to reduce the information you see based on the criteria selected.</span></span> <span data-ttu-id="7ed40-154">Vous pouvez inclure des filtres avec des tableaux, des listes, des cartes et d’autres composants qui organisent le contenu.</span><span class="sxs-lookup"><span data-stu-id="7ed40-154">You can include filters with tables, lists, cards, and other components that organize content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7ed40-155">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7ed40-155">Top use cases</span></span>

<span data-ttu-id="7ed40-156">Organisation du contenu dans :</span><span class="sxs-lookup"><span data-stu-id="7ed40-156">Organizing content in:</span></span>

* <span data-ttu-id="7ed40-157">Listes</span><span class="sxs-lookup"><span data-stu-id="7ed40-157">Lists</span></span>
* <span data-ttu-id="7ed40-158">Tables</span><span class="sxs-lookup"><span data-stu-id="7ed40-158">Tables</span></span>
* <span data-ttu-id="7ed40-159">Tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="7ed40-159">Dashboards</span></span>
* <span data-ttu-id="7ed40-160">Visualisation de données</span><span class="sxs-lookup"><span data-stu-id="7ed40-160">Data visualization</span></span>

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="Exemple de modèle de filtre." border="false":::

## <a name="form"></a><span data-ttu-id="7ed40-162">Formulaire</span><span class="sxs-lookup"><span data-stu-id="7ed40-162">Form</span></span>

<span data-ttu-id="7ed40-163">Les formulaires sont utilisés pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="7ed40-163">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="7ed40-164">Effacer l’étiquetage et les regroupements logiques de champs d’entrée sont essentiels pour une bonne expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7ed40-164">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7ed40-165">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7ed40-165">Top use cases</span></span>

* <span data-ttu-id="7ed40-166">Se connecter</span><span class="sxs-lookup"><span data-stu-id="7ed40-166">Sign in</span></span>
* <span data-ttu-id="7ed40-167">Profils utilisateur</span><span class="sxs-lookup"><span data-stu-id="7ed40-167">User profiles</span></span>
* <span data-ttu-id="7ed40-168">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7ed40-168">Settings</span></span>
* <span data-ttu-id="7ed40-169">Collection d’entrées utilisateur</span><span class="sxs-lookup"><span data-stu-id="7ed40-169">User input collection</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7ed40-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="7ed40-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="L’exemple montre un modèle d’interface utilisateur de formulaire sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7ed40-172">Mobile</span><span class="sxs-lookup"><span data-stu-id="7ed40-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="L’exemple montre un modèle d’interface utilisateur de formulaire sur mobile." border="false":::

---

## <a name="list"></a><span data-ttu-id="7ed40-174">Répertorier</span><span class="sxs-lookup"><span data-stu-id="7ed40-174">List</span></span>

<span data-ttu-id="7ed40-175">Vous pouvez utiliser une liste pour afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="7ed40-175">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7ed40-176">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7ed40-176">Top use cases</span></span>

* <span data-ttu-id="7ed40-177">Afficher les données</span><span class="sxs-lookup"><span data-stu-id="7ed40-177">Display data</span></span>
* <span data-ttu-id="7ed40-178">Actions contextuelles sur le contenu de l’application</span><span class="sxs-lookup"><span data-stu-id="7ed40-178">Contextual actions on app content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7ed40-179">Desktop</span><span class="sxs-lookup"><span data-stu-id="7ed40-179">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="L’exemple montre un modèle d’interface utilisateur de liste sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7ed40-181">Mobile</span><span class="sxs-lookup"><span data-stu-id="7ed40-181">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="L’exemple montre un modèle d’interface utilisateur de liste sur mobile." border="false":::

---

## <a name="sign-in"></a><span data-ttu-id="7ed40-183">Se connecter</span><span class="sxs-lookup"><span data-stu-id="7ed40-183">Sign in</span></span>

<span data-ttu-id="7ed40-184">Vous pouvez concevoir des flux de Teams d’application pour différents contextes et fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="7ed40-184">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="7ed40-185">L’exemple suivant inclut l’authentification unique (SSO), que nous vous recommandons pour l’expérience d’authentification la plus simple.</span><span class="sxs-lookup"><span data-stu-id="7ed40-185">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

### <a name="top-use-case"></a><span data-ttu-id="7ed40-186">Cas d’utilisation principaux</span><span class="sxs-lookup"><span data-stu-id="7ed40-186">Top use case</span></span>

* <span data-ttu-id="7ed40-187">Authentifier les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="7ed40-187">Authenticate users</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7ed40-188">Desktop</span><span class="sxs-lookup"><span data-stu-id="7ed40-188">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de la signature sur le bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7ed40-190">Mobile</span><span class="sxs-lookup"><span data-stu-id="7ed40-190">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de la signature sur un appareil mobile." border="false":::

---

## <a name="settings"></a><span data-ttu-id="7ed40-192">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7ed40-192">Settings</span></span>

<span data-ttu-id="7ed40-193">Paramètres’écran sont les écrans où les utilisateurs peuvent configurer leurs préférences avec votre application.</span><span class="sxs-lookup"><span data-stu-id="7ed40-193">Settings screens are where users can configure their preferences with your app.</span></span> <span data-ttu-id="7ed40-194">(Remarque : Paramètres est un conteneur pour les [composants d’interface utilisateur de base.)](~/concepts/design/design-teams-app-basic-ui-components.md)</span><span class="sxs-lookup"><span data-stu-id="7ed40-194">(Note: Settings is a container for [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md).)</span></span>

### <a name="top-use-case"></a><span data-ttu-id="7ed40-195">Cas d’utilisation principaux</span><span class="sxs-lookup"><span data-stu-id="7ed40-195">Top use case</span></span>

* <span data-ttu-id="7ed40-196">Gérer les fonctionnalités de l’application</span><span class="sxs-lookup"><span data-stu-id="7ed40-196">Manage app features</span></span>

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="L’exemple montre un modèle de paramètres." border="false":::

## <a name="task-board"></a><span data-ttu-id="7ed40-198">Tableau des tâches</span><span class="sxs-lookup"><span data-stu-id="7ed40-198">Task board</span></span>

<span data-ttu-id="7ed40-199">Un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="7ed40-199">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="7ed40-200">Il peut également être utilisé pour trier n’importe quel type de contenu en catégories.</span><span class="sxs-lookup"><span data-stu-id="7ed40-200">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="7ed40-201">Vous pouvez modifier et déplacer les cartes entre les colonnes.</span><span class="sxs-lookup"><span data-stu-id="7ed40-201">You can edit and move the cards between columns.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7ed40-202">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7ed40-202">Top use cases</span></span>

* <span data-ttu-id="7ed40-203">Gestion de projet.</span><span class="sxs-lookup"><span data-stu-id="7ed40-203">Project management.</span></span> <span data-ttu-id="7ed40-204">Affectation de tâches et état de suivi</span><span class="sxs-lookup"><span data-stu-id="7ed40-204">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="7ed40-205">Brainstorming.</span><span class="sxs-lookup"><span data-stu-id="7ed40-205">Brainstorming.</span></span> <span data-ttu-id="7ed40-206">Ajout d’idées dans différentes catégories</span><span class="sxs-lookup"><span data-stu-id="7ed40-206">Adding ideas in different categories</span></span>
* <span data-ttu-id="7ed40-207">Exercices de tri.</span><span class="sxs-lookup"><span data-stu-id="7ed40-207">Sorting exercises.</span></span> <span data-ttu-id="7ed40-208">Organisation de n’importe quel type d’informations dans des compartiments</span><span class="sxs-lookup"><span data-stu-id="7ed40-208">Organizing any kind of information into buckets</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7ed40-209">Desktop</span><span class="sxs-lookup"><span data-stu-id="7ed40-209">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="L’exemple montre un modèle d’interface utilisateur du tableau des tâches sur le bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7ed40-211">Mobile</span><span class="sxs-lookup"><span data-stu-id="7ed40-211">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="L’exemple montre un modèle d’interface utilisateur du tableau des tâches sur mobile." border="false":::

---

## <a name="wizard"></a><span data-ttu-id="7ed40-213">Assistant</span><span class="sxs-lookup"><span data-stu-id="7ed40-213">Wizard</span></span>

<span data-ttu-id="7ed40-214">Un Assistant guide un utilisateur à travers plusieurs écrans pour effectuer une tâche (par exemple, un processus d’installation).</span><span class="sxs-lookup"><span data-stu-id="7ed40-214">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="7ed40-215">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7ed40-215">Top use cases</span></span>

* <span data-ttu-id="7ed40-216">Configuration</span><span class="sxs-lookup"><span data-stu-id="7ed40-216">Setup</span></span>
* <span data-ttu-id="7ed40-217">Intégration</span><span class="sxs-lookup"><span data-stu-id="7ed40-217">Onboarding</span></span>
* <span data-ttu-id="7ed40-218">Expériences de première expérience</span><span class="sxs-lookup"><span data-stu-id="7ed40-218">First-run experiences</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7ed40-219">Desktop</span><span class="sxs-lookup"><span data-stu-id="7ed40-219">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’Assistant sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7ed40-221">Mobile</span><span class="sxs-lookup"><span data-stu-id="7ed40-221">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’Assistant sur mobile." border="false":::

---
