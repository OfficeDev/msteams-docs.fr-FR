---
title: Conception de votre application avec des modèles d’interface utilisateur
author: heath-hamilton
description: Concevez votre application plus rapidement avec des composants d’interface utilisateur, des dispositions et des modèles standardisés fréquemment visibles dans Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 0cd5c6c4525e340f9aa53a78749211783880225a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566018"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="15f13-103">Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="15f13-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="15f13-104">Concevez votre application Microsoft Teams plus rapidement avec des modèles d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15f13-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="15f13-105">Les modèles sont une collection de composants fluent basés sur l’interface utilisateur qui fonctionnent dans les cas d’utilisation courants Teams, ce qui vous donne plus de temps pour déterminer la meilleure expérience pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="15f13-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="15f13-106">Mise en place d’outils et d’exemples</span><span class="sxs-lookup"><span data-stu-id="15f13-106">Getting started with tools and samples</span></span>

<span data-ttu-id="15f13-107">Les ressources suivantes peuvent vous aider à concevoir et développer votre application à l’aide de modèles d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15f13-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="15f13-108">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="15f13-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="15f13-109">Récupérer des modèles d’interface utilisateur pour la conception de votre application à partir du kit d’interface utilisateur Microsoft Teams, qui inclut également des informations complètes sur l’utilisation, l’anatomie, l’accessibilité et les meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="15f13-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="15f13-110">Obtenir le kit d’interface utilisateur (Figma)</span><span class="sxs-lookup"><span data-stu-id="15f13-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="15f13-111">Microsoft Teams Bibliothèque d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="15f13-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="15f13-112">Affichez et testez les Teams d’interface utilisateur et les composants associés dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="15f13-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="15f13-113">Essayer la bibliothèque d’interface utilisateur (aire de jeu)</span><span class="sxs-lookup"><span data-stu-id="15f13-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="15f13-114">Importez ces modèles et composants associés directement dans Teams projet d’application.</span><span class="sxs-lookup"><span data-stu-id="15f13-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="15f13-115">Obtenir la bibliothèque d’interface utilisateur (GitHub)</span><span class="sxs-lookup"><span data-stu-id="15f13-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="15f13-116">Exemple d’application</span><span class="sxs-lookup"><span data-stu-id="15f13-116">Sample app</span></span>

<span data-ttu-id="15f13-117">Installez un exemple d’application pour voir l’apparence et le comportement des modèles d’interface utilisateur Teams contextes.</span><span class="sxs-lookup"><span data-stu-id="15f13-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="15f13-118">Obtenir l’exemple d’application (GitHub)</span><span class="sxs-lookup"><span data-stu-id="15f13-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="15f13-119">Répertorier</span><span class="sxs-lookup"><span data-stu-id="15f13-119">List</span></span>

<span data-ttu-id="15f13-120">Vous pouvez utiliser une liste pour afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="15f13-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="Exemple de modèle d’interface utilisateur de liste." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-122">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-122">Top use cases</span></span>

* <span data-ttu-id="15f13-123">Afficher les données</span><span class="sxs-lookup"><span data-stu-id="15f13-123">Display data</span></span>
* <span data-ttu-id="15f13-124">Actions contextuelles sur le contenu de l’application</span><span class="sxs-lookup"><span data-stu-id="15f13-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="15f13-125">Tableau de bord</span><span class="sxs-lookup"><span data-stu-id="15f13-125">Dashboard</span></span>

<span data-ttu-id="15f13-126">Un tableau de bord affiche différents types de contenu dans un emplacement central (Teams application ou onglet personnel).</span><span class="sxs-lookup"><span data-stu-id="15f13-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="15f13-127">Les utilisateurs doivent pouvoir personnaliser au moins une partie de ce qu’ils voient sur un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="15f13-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="Exemple de modèle d’interface utilisateur de tableau de bord." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-129">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-129">Top use cases</span></span>

* <span data-ttu-id="15f13-130">Analyser les données</span><span class="sxs-lookup"><span data-stu-id="15f13-130">Analyze data</span></span>
* <span data-ttu-id="15f13-131">Mesures du rapport</span><span class="sxs-lookup"><span data-stu-id="15f13-131">Report metrics</span></span>
* <span data-ttu-id="15f13-132">Organiser différentes informations au même endroit</span><span class="sxs-lookup"><span data-stu-id="15f13-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="15f13-133">Formulaire</span><span class="sxs-lookup"><span data-stu-id="15f13-133">Form</span></span>

<span data-ttu-id="15f13-134">Les formulaires sont utilisés pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="15f13-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="15f13-135">Effacer l’étiquetage et les regroupements logiques de champs d’entrée sont essentiels pour une bonne expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15f13-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="Exemple de modèle d’interface utilisateur de formulaire." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-137">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-137">Top use cases</span></span>

* <span data-ttu-id="15f13-138">Se connecter</span><span class="sxs-lookup"><span data-stu-id="15f13-138">Sign in</span></span>
* <span data-ttu-id="15f13-139">Profils utilisateur</span><span class="sxs-lookup"><span data-stu-id="15f13-139">User profiles</span></span>
* <span data-ttu-id="15f13-140">Paramètres</span><span class="sxs-lookup"><span data-stu-id="15f13-140">Settings</span></span>
* <span data-ttu-id="15f13-141">Collection d’entrées utilisateur</span><span class="sxs-lookup"><span data-stu-id="15f13-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="15f13-142">Se connecter</span><span class="sxs-lookup"><span data-stu-id="15f13-142">Sign in</span></span>

<span data-ttu-id="15f13-143">Vous pouvez concevoir des flux de Teams d’application pour différents contextes et fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="15f13-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="15f13-144">L’exemple suivant inclut l’authentification unique (SSO), que nous vous recommandons pour l’expérience d’authentification la plus simple.</span><span class="sxs-lookup"><span data-stu-id="15f13-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de la signature." border="false":::

### <a name="top-use-case"></a><span data-ttu-id="15f13-146">Cas d’utilisation principaux</span><span class="sxs-lookup"><span data-stu-id="15f13-146">Top use case</span></span>

* <span data-ttu-id="15f13-147">Authentifier les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="15f13-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="15f13-148">Tableau des tâches</span><span class="sxs-lookup"><span data-stu-id="15f13-148">Task board</span></span>

<span data-ttu-id="15f13-149">Un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="15f13-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="15f13-150">Il peut également être utilisé pour trier n’importe quel type de contenu en catégories.</span><span class="sxs-lookup"><span data-stu-id="15f13-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="15f13-151">Vous pouvez modifier et déplacer les cartes entre les colonnes.</span><span class="sxs-lookup"><span data-stu-id="15f13-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="Exemple de modèle d’interface utilisateur du tableau des tâches." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-153">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-153">Top use cases</span></span>

* <span data-ttu-id="15f13-154">Project gestion : affectation des tâches et état de suivi.</span><span class="sxs-lookup"><span data-stu-id="15f13-154">Project management: Assigning tasks and tracking status.</span></span>
* <span data-ttu-id="15f13-155">Brainstorming : ajout d’idées dans différentes catégories.</span><span class="sxs-lookup"><span data-stu-id="15f13-155">Brainstorming: Adding ideas in different categories.</span></span>
* <span data-ttu-id="15f13-156">Exercices de tri : organisation de n’importe quel type d’informations en compartiments.</span><span class="sxs-lookup"><span data-stu-id="15f13-156">Sorting exercises: Organizing any kind of information into buckets.</span></span>

## <a name="data-visualization"></a><span data-ttu-id="15f13-157">Visualisation de données</span><span class="sxs-lookup"><span data-stu-id="15f13-157">Data visualization</span></span>

<span data-ttu-id="15f13-158">Vous pouvez utiliser différentes tailles de carte (unique, double et complète) pour empiler et organiser les visualisations de données sur la même page.</span><span class="sxs-lookup"><span data-stu-id="15f13-158">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="15f13-159">Les cartes s’adaptent à la disposition des colonnes et remplissent des espaces vides.</span><span class="sxs-lookup"><span data-stu-id="15f13-159">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="Exemple de modèle d’interface utilisateur de visualisation de données." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-161">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-161">Top use cases</span></span>

* <span data-ttu-id="15f13-162">Afficher des informations complexes</span><span class="sxs-lookup"><span data-stu-id="15f13-162">Display complex information</span></span>
* <span data-ttu-id="15f13-163">Créer un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="15f13-163">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="15f13-164">Assistant</span><span class="sxs-lookup"><span data-stu-id="15f13-164">Wizard</span></span>

<span data-ttu-id="15f13-165">Un Assistant guide un utilisateur à travers plusieurs écrans pour effectuer une tâche (par exemple, un processus d’installation).</span><span class="sxs-lookup"><span data-stu-id="15f13-165">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="Exemple de modèle d’interface utilisateur assistant." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-167">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-167">Top use cases</span></span>

* <span data-ttu-id="15f13-168">Configuration</span><span class="sxs-lookup"><span data-stu-id="15f13-168">Setup</span></span>
* <span data-ttu-id="15f13-169">Intégration</span><span class="sxs-lookup"><span data-stu-id="15f13-169">Onboarding</span></span>
* <span data-ttu-id="15f13-170">Expériences de première expérience</span><span class="sxs-lookup"><span data-stu-id="15f13-170">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="15f13-171">État vide</span><span class="sxs-lookup"><span data-stu-id="15f13-171">Empty state</span></span>

<span data-ttu-id="15f13-172">Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="15f13-172">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="15f13-173">Il est très flexible : adaptez-le pour utiliser un, quelques-uns ou tous les composants de la conception suivante.</span><span class="sxs-lookup"><span data-stu-id="15f13-173">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-175">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-175">Top use cases</span></span>

* <span data-ttu-id="15f13-176">Se connecter</span><span class="sxs-lookup"><span data-stu-id="15f13-176">Sign in</span></span>
* <span data-ttu-id="15f13-177">Messages de bienvenue et expériences de première expérience</span><span class="sxs-lookup"><span data-stu-id="15f13-177">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="15f13-178">Messages de réussite</span><span class="sxs-lookup"><span data-stu-id="15f13-178">Success messages</span></span>
* <span data-ttu-id="15f13-179">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="15f13-179">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="15f13-180">Barre de notification</span><span class="sxs-lookup"><span data-stu-id="15f13-180">Notification bar</span></span>

<span data-ttu-id="15f13-181">Une barre de notification est une zone dédiée à l’affichage de messages brefs et importants qui ne nécessitent pas que l’utilisateur prenne des mesures immédiates.</span><span class="sxs-lookup"><span data-stu-id="15f13-181">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="15f13-182">Des icônes et des couleurs d’arrière-plan spécifiques sont associées à des types de messages spécifiques (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="15f13-182">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="Exemple de modèles de barre de notification." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-184">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-184">Top use cases</span></span>

* <span data-ttu-id="15f13-185">Messages critiques, erreurs et avertissements</span><span class="sxs-lookup"><span data-stu-id="15f13-185">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="15f13-186">Messages de réussite</span><span class="sxs-lookup"><span data-stu-id="15f13-186">Success messages</span></span>
* <span data-ttu-id="15f13-187">Messages d’information ou promotionnels</span><span class="sxs-lookup"><span data-stu-id="15f13-187">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="15f13-188">Navigation gauche</span><span class="sxs-lookup"><span data-stu-id="15f13-188">Left nav</span></span>

<span data-ttu-id="15f13-189">Utilisez le navigation de gauche pour parcourir plusieurs pages dans votre onglet Teams gauche. Dans l’exemple suivant, le navigation gauche se trouve entre la liste de canaux et le contenu de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="15f13-189">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="Exemple de modèle de navigation gauche." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-191">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-191">Top use cases</span></span>

* <span data-ttu-id="15f13-192">Parcourez plusieurs pages dans un Teams onglet.</span><span class="sxs-lookup"><span data-stu-id="15f13-192">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="15f13-193">Décomposez les applications complexes en plusieurs pages.</span><span class="sxs-lookup"><span data-stu-id="15f13-193">Break down complex apps into multiple pages.</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="15f13-194">Barre de navigation</span><span class="sxs-lookup"><span data-stu-id="15f13-194">Breadcrumb</span></span>

<span data-ttu-id="15f13-195">Les barre de navigation sont une aide à la navigation qui véhicule la hiérarchie de votre application.</span><span class="sxs-lookup"><span data-stu-id="15f13-195">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="15f13-196">Ils aident les utilisateurs à comprendre comment la page qu’ils affichent s’intègre à l’expérience globale et offrent un accès en un clic aux niveaux supérieurs de cette hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="15f13-196">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="Exemple de modèle de lacrumb." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-198">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-198">Top use cases</span></span>

* <span data-ttu-id="15f13-199">Hiérarchie de communication</span><span class="sxs-lookup"><span data-stu-id="15f13-199">Communicate hierarchy</span></span>
* <span data-ttu-id="15f13-200">Navigation</span><span class="sxs-lookup"><span data-stu-id="15f13-200">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="15f13-201">Barre d'outils</span><span class="sxs-lookup"><span data-stu-id="15f13-201">Toolbar</span></span>

<span data-ttu-id="15f13-202">Une barre d’outils est un conteneur permettant de grouper un ensemble de contrôles.</span><span class="sxs-lookup"><span data-stu-id="15f13-202">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="Exemple de modèle de barre d’outils." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-204">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-204">Top use cases</span></span>

* <span data-ttu-id="15f13-205">Actions contextuelles sur le contenu de l’application</span><span class="sxs-lookup"><span data-stu-id="15f13-205">Contextual actions on app content</span></span>
* <span data-ttu-id="15f13-206">Filtre contextuel et recherche</span><span class="sxs-lookup"><span data-stu-id="15f13-206">Contextual filter and find</span></span>
* <span data-ttu-id="15f13-207">Navigation et barre de navigation</span><span class="sxs-lookup"><span data-stu-id="15f13-207">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="15f13-208">Phase</span><span class="sxs-lookup"><span data-stu-id="15f13-208">Stage</span></span>

<span data-ttu-id="15f13-209">L’étape permet aux utilisateurs d’ouvrir une entité (par exemple, une image, un fichier ou un site web) dans Teams au lieu de l’ouvrir dans une autre application ou navigateur.</span><span class="sxs-lookup"><span data-stu-id="15f13-209">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="15f13-210">Le cas d’utilisation principal de l’étape est l’affichage ; la surface ne doit pas être utilisée pour des interactions complexes.</span><span class="sxs-lookup"><span data-stu-id="15f13-210">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="15f13-211">(Remarque d’implémentation : créez votre étape à l’aide d’un [module de tâche de grande taille.)](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="15f13-211">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="L’exemple montre un modèle d’étape." border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="15f13-213">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="15f13-213">Top use cases</span></span>

* <span data-ttu-id="15f13-214">Ouvrez une entité dans Teams au lieu d’une autre application ou navigateur.</span><span class="sxs-lookup"><span data-stu-id="15f13-214">Open an entity in Teams instead of another app or browser.</span></span>
* <span data-ttu-id="15f13-215">Média à la une ou autre contenu.</span><span class="sxs-lookup"><span data-stu-id="15f13-215">Spotlight media or other content.</span></span>
