---
title: Gérer vos applications avec le Portail du développeur
description: Découvrez comment gérer vos applications à l’aide du portail de développement pour Microsoft Teams.
keywords: mise en place des équipes du portail de développement
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 5f3335470a442fc8a3c94e9563e21fea75c4ef4b
ms.sourcegitcommit: c55b0d2a4c1f8945e49b0b7c0b08c0eb3da3d2be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646332"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a><span data-ttu-id="751a3-104">Gérer vos applications avec le Portail des développeurs pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="751a3-104">Manage your apps with the Developer Portal for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="751a3-105">Le Portail des développeurs pour Teams est actuellement en prévisualisation [pour les développeurs publics.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="751a3-105">The Developer Portal for Teams is currently in [public developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

<span data-ttu-id="751a3-106">Le Portail des développeurs pour Teams est le principal outil de configuration, de distribution et de gestion de vos applications Microsoft Teams client.</span><span class="sxs-lookup"><span data-stu-id="751a3-106">The Developer Portal for Teams is the primary tool for configuring, distributing, and managing your Microsoft Teams apps.</span></span> <span data-ttu-id="751a3-107">Avec le Portail des développeurs, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’runtime, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="751a3-107">With the Developer Portal, you can collaborate with colleagues on your app, set up runtime environments, and much more.</span></span>

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Capture d’écran montrant la page d’accueil du portail de développement pour Teams.":::

## <a name="register-an-app"></a><span data-ttu-id="751a3-109">Inscrire une application</span><span class="sxs-lookup"><span data-stu-id="751a3-109">Register an app</span></span>

<span data-ttu-id="751a3-110">Le Portail des développeurs propose deux façons d’inscrire une Teams application :</span><span class="sxs-lookup"><span data-stu-id="751a3-110">The Developer Portal provides a couple ways to register a Teams app:</span></span>

* <span data-ttu-id="751a3-111">Inscrire une toute nouvelle application</span><span class="sxs-lookup"><span data-stu-id="751a3-111">Register a brand new app</span></span>
* <span data-ttu-id="751a3-112">Importer un package d’application existant</span><span class="sxs-lookup"><span data-stu-id="751a3-112">Import an existing app package</span></span>

> [!NOTE]
> <span data-ttu-id="751a3-113">Si vous créez une application à [l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), vous pouvez gérer cette application dans le Portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="751a3-113">If you create an app using the [Microsoft Teams Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), you can manage that app in the Developer Portal.</span></span>

## <a name="set-up-an-environment"></a><span data-ttu-id="751a3-114">Configurer un environnement</span><span class="sxs-lookup"><span data-stu-id="751a3-114">Set up an environment</span></span>

<span data-ttu-id="751a3-115">Vous pouvez configurer des environnements et des variables globales pour faciliter la transition de votre application de votre runtime local vers la production.</span><span class="sxs-lookup"><span data-stu-id="751a3-115">You can configure environments and global variables to help transition your app from your local runtime to production.</span></span> <span data-ttu-id="751a3-116">Les variables globales sont utilisées dans tous les environnements.</span><span class="sxs-lookup"><span data-stu-id="751a3-116">Global variables are used across all environments.</span></span>

<span data-ttu-id="751a3-117">**Pour configurer un environnement**</span><span class="sxs-lookup"><span data-stu-id="751a3-117">**To set up an environment**</span></span>

1. <span data-ttu-id="751a3-118">Dans le portail du développeur, sélectionnez l’application sur qui vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="751a3-118">In the Developer Portal, select the app you're working on.</span></span>
2. <span data-ttu-id="751a3-119">Go to the **Environments** page and select **+ Add an environment**.</span><span class="sxs-lookup"><span data-stu-id="751a3-119">Go to the **Environments** page and select **+ Add an environment**.</span></span>
3. <span data-ttu-id="751a3-120">Sélectionnez **+ Ajoutez une variable** pour créer des variables de configuration pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="751a3-120">Select **+ Add a variable** to create configuration variables for your environment.</span></span>

<span data-ttu-id="751a3-121">**Pour utiliser des variables**</span><span class="sxs-lookup"><span data-stu-id="751a3-121">**To use variables**</span></span>

<span data-ttu-id="751a3-122">Utilisez les noms de variables au lieu de valeurs codées en dur pour définir les configurations de votre application.</span><span class="sxs-lookup"><span data-stu-id="751a3-122">Use the variable names instead of hard-coded values to set your app configurations.</span></span>

1. <span data-ttu-id="751a3-123">Entrez `{{` n’importe quel champ dans le portail du développeur.</span><span class="sxs-lookup"><span data-stu-id="751a3-123">Enter `{{` in any field in the Developer Portal.</span></span> <span data-ttu-id="751a3-124">Une dropdown avec toutes les variables que vous avez créées pour l’environnement choisi ainsi que les variables globales s’affiche.</span><span class="sxs-lookup"><span data-stu-id="751a3-124">A dropdown with all the variables you've created for the chosen environment along with the global variables appears.</span></span>  
1. <span data-ttu-id="751a3-125">Avant de télécharger votre package d’application (par exemple, lorsque vous êtes prêt à publier sur le Teams Store), sélectionnez l’environnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="751a3-125">Before downloading your app package (for example, when getting ready to publish to the Teams store), select the environment you want to use.</span></span> <span data-ttu-id="751a3-126">Les configurations de votre application sont automatiquement mises à jour en fonction de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="751a3-126">Your app configurations update automatically based on the environment.</span></span> 

## <a name="identify-app-owners"></a><span data-ttu-id="751a3-127">Identifier les propriétaires d’applications</span><span class="sxs-lookup"><span data-stu-id="751a3-127">Identify app owners</span></span>

<span data-ttu-id="751a3-128">Chaque application inclut une page **Propriétaires,** dans laquelle vous pouvez partager l’inscription de votre application avec des collègues de votre organisation. Le **rôle Collaborateur** dispose des mêmes autorisations que le rôle **Propriétaire,** à l’exception de la possibilité de supprimer une application.</span><span class="sxs-lookup"><span data-stu-id="751a3-128">Each app includes an **Owners** page, where you can share your app registration with colleagues in your org. The **Contributor** role has the same permissions as the **Owner** role except the ability to delete an app.</span></span>

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a><span data-ttu-id="751a3-129">Configurer les fonctionnalités de votre application et d’autres métadonnées importantes</span><span class="sxs-lookup"><span data-stu-id="751a3-129">Configure your app's capabilities and other important metadata</span></span>

<span data-ttu-id="751a3-130">Une Teams est une application web.</span><span class="sxs-lookup"><span data-stu-id="751a3-130">A Teams app is a web app.</span></span> <span data-ttu-id="751a3-131">Comme toutes les applications web, son code source est généralement développé dans un éditeur de code ou IDE et hébergé quelque part dans le cloud (comme Azure).</span><span class="sxs-lookup"><span data-stu-id="751a3-131">Like all web apps, its source code is typically developed in an IDE or code editor and hosted somewhere in the cloud (like Azure).</span></span>

<span data-ttu-id="751a3-132">Pour installer et restituer votre application dans Teams, vous devez inclure un ensemble de configurations Teams reconnu.</span><span class="sxs-lookup"><span data-stu-id="751a3-132">To install and render your app in Teams, you must include a set of configurations that Teams recognizes.</span></span> <span data-ttu-id="751a3-133">Pour ce faire, il s’agit généralement d’un manifeste d’application, un fichier JSON qui contient toutes les métadonnées dont Teams a besoin pour afficher le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="751a3-133">This has traditionally been done by crafting an app manifest, a JSON file that contains all the metadata Teams needs to display your app content.</span></span> <span data-ttu-id="751a3-134">Le Portail des développeurs fait abstraction de ce processus et inclut de nouvelles fonctionnalités et outils pour vous aider à réussir.</span><span class="sxs-lookup"><span data-stu-id="751a3-134">The Developer Portal abstracts this process and includes new features and tooling to help you be more successful.</span></span>

## <a name="test-your-app-directly-in-teams"></a><span data-ttu-id="751a3-135">Testez votre application directement dans Teams</span><span class="sxs-lookup"><span data-stu-id="751a3-135">Test your app directly in Teams</span></span>

<span data-ttu-id="751a3-136">Le Portail des développeurs fournit des options pour tester et déboguer votre application :</span><span class="sxs-lookup"><span data-stu-id="751a3-136">The Developer Portal provides options for testing and debugging your app:</span></span>

* <span data-ttu-id="751a3-137">Dans la page **Vue d’ensemble,** vous pouvez voir un instantané de la validation des configurations de votre application par rapport Teams cas de test du Store.</span><span class="sxs-lookup"><span data-stu-id="751a3-137">On the **Overview** page, you can see a snapshot of whether your app's configurations validate against Teams store test cases.</span></span>
* <span data-ttu-id="751a3-138">**L’aperçu Teams** bouton vous permet de lancer rapidement votre application dans le client Teams pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="751a3-138">The **Preview in Teams** button lets you launch your app quickly in the Teams client for debugging.</span></span>

## <a name="distribute-your-app"></a><span data-ttu-id="751a3-139">Distribuer votre application.</span><span class="sxs-lookup"><span data-stu-id="751a3-139">Distribute your app</span></span>

<span data-ttu-id="751a3-140">À partir du portail  du développeur, utilisez le bouton Distribuer pour télécharger un package d’application, publier dans votre organisation ou publier sur le Teams store.</span><span class="sxs-lookup"><span data-stu-id="751a3-140">From the Developer Portal, use the **Distribute** button to download an app package, publish to your org, or publish to the Teams store.</span></span>

<span data-ttu-id="751a3-141">Pour plus d’informations, [voir distribuer votre Teams application.](~/concepts/deploy-and-publish/apps-publish-overview.md)</span><span class="sxs-lookup"><span data-stu-id="751a3-141">For more information, see [distribute your Teams app](~/concepts/deploy-and-publish/apps-publish-overview.md).</span></span>

## <a name="analyze-your-apps-usage"></a><span data-ttu-id="751a3-142">Analyser l’utilisation de votre application</span><span class="sxs-lookup"><span data-stu-id="751a3-142">Analyze your app's usage</span></span>

<span data-ttu-id="751a3-143">Dans **la** page Vue d’ensemble, vous pouvez voir le nombre total d’utilisateurs actifs pour votre application.</span><span class="sxs-lookup"><span data-stu-id="751a3-143">On the **Overview** page, you can see the total number of active users for your app.</span></span> <span data-ttu-id="751a3-144">Ces mesures sont disponibles pour les applications publiées dans le Teams store ou le catalogue d’applications d’une organisation via le Portail du développeur et limitées à l’ID de l’application.</span><span class="sxs-lookup"><span data-stu-id="751a3-144">These metrics are available for apps published to the Teams store or an org's app catalog through Developer Portal and scoped to the app ID.</span></span>

| <span data-ttu-id="751a3-145">Métrique</span><span class="sxs-lookup"><span data-stu-id="751a3-145">Metric</span></span> | <span data-ttu-id="751a3-146">Définition</span><span class="sxs-lookup"><span data-stu-id="751a3-146">Definition</span></span> |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="751a3-147">*R30 mensuel*</span><span class="sxs-lookup"><span data-stu-id="751a3-147">*Monthly R30*</span></span> | <span data-ttu-id="751a3-148">Mesure d’utilisation par défaut.</span><span class="sxs-lookup"><span data-stu-id="751a3-148">The default usage metric.</span></span> <span data-ttu-id="751a3-149">Il indique le nombre d’utilisateurs actifs uniques qui ont utilisé votre application dans cette fenêtre de 30 jours en temps UTC.</span><span class="sxs-lookup"><span data-stu-id="751a3-149">It shows you the count of unique active users that used your app within that rolling 30-day window in UTC.</span></span> |
| <span data-ttu-id="751a3-150">*Tous les jours*</span><span class="sxs-lookup"><span data-stu-id="751a3-150">*Daily*</span></span> | <span data-ttu-id="751a3-151">Indique le nombre d’utilisateurs actifs uniques qui ont utilisé votre application au cours d’un jour donné au cours de l’UTC.</span><span class="sxs-lookup"><span data-stu-id="751a3-151">Shows you the count of unique active users that used your app in a given day in UTC.</span></span> |

<span data-ttu-id="751a3-152">L’utilisation mensuelle et quotidienne est indiquée pour les sept, 30 et 60 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="751a3-152">Monthly and daily usage is shown for the past seven, 30 days, and 60 days.</span></span> <span data-ttu-id="751a3-153">L’utilisation doit être reflétée pour un jour donné dans les 24 à 48 heures.</span><span class="sxs-lookup"><span data-stu-id="751a3-153">You should see usage reflected for a given day within 24-48 hours.</span></span> <span data-ttu-id="751a3-154">L’affichage des nouvelles applications peut prendre jusqu’à 3 à 5 jours.</span><span class="sxs-lookup"><span data-stu-id="751a3-154">Usage for new apps can take up to 3-5 days to display.</span></span>

## <a name="use-tools-to-create-app-features"></a><span data-ttu-id="751a3-155">Utiliser des outils pour créer des fonctionnalités d’application</span><span class="sxs-lookup"><span data-stu-id="751a3-155">Use tools to create app features</span></span>

<span data-ttu-id="751a3-156">Le Portail des développeurs inclut également des outils pour vous aider à créer certaines fonctionnalités clés de Teams applications.</span><span class="sxs-lookup"><span data-stu-id="751a3-156">The Developer Portal also includes tools to help you build some key features of Teams apps.</span></span> <span data-ttu-id="751a3-157">Voici quelques-uns de ces outils :</span><span class="sxs-lookup"><span data-stu-id="751a3-157">Some of these tools include:</span></span>

* <span data-ttu-id="751a3-158">**Scene studio :** concevoir des scènes personnalisées en mode Ensemble pour Teams réunions.</span><span class="sxs-lookup"><span data-stu-id="751a3-158">**Scene studio**: Design custom Together mode scenes for Teams meetings.</span></span>
* <span data-ttu-id="751a3-159">**Éditeur de cartes adaptatives**: créez et prévisualiser des cartes adaptatives à inclure avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="751a3-159">**Adaptive Cards editor**: Create and preview Adaptive Cards to include with your apps.</span></span>
* <span data-ttu-id="751a3-160">**Plateforme d’identités Microsoft gestion des** applications : inscrivez vos applications avec Azure Active Directory (Azure AD) pour aider les utilisateurs à se connecter et à fournir l’accès aux API.</span><span class="sxs-lookup"><span data-stu-id="751a3-160">**Microsoft identity platform management**: Register your apps with Azure Active Directory (Azure AD) to help users sign in and provide access to APIs.</span></span>
