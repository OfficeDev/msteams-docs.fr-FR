---
title: Référence des instructions de conception
description: Décrit les instructions pour la conception d’une application personnelle
keywords: instructions de conception teams structure de référence des applications personnelles
ms.openlocfilehash: 6a07b618d78a3ad79850713052c88ef178c1ecc1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673611"
---
# <a name="personal-apps"></a><span data-ttu-id="d9e49-104">Applications personnelles</span><span class="sxs-lookup"><span data-stu-id="d9e49-104">Personal apps</span></span>

> [!Important]
> <span data-ttu-id="d9e49-105">La prise en charge complète des onglets sur les clients mobiles bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="d9e49-105">Full support for tabs on mobile clients is coming soon.</span></span> <span data-ttu-id="d9e49-106">Pour vous préparer à ce changement, suivez les [instructions pour les onglets sur mobile](~/tabs/design/tabs-mobile.md) lors de la création des onglets.</span><span class="sxs-lookup"><span data-stu-id="d9e49-106">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="d9e49-107">Les applications personnelles (onglets statiques) sont actuellement disponibles dans l’Aperçu pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="d9e49-107">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="d9e49-108">Lorsque la prise en charge complète des onglets est publiée :</span><span class="sxs-lookup"><span data-stu-id="d9e49-108">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="d9e49-109">Tous les onglets seront toujours disponibles sur mobile</span><span class="sxs-lookup"><span data-stu-id="d9e49-109">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="d9e49-110">Votre `contentUrl` **sera chargé dans le client teams mobile**.</span><span class="sxs-lookup"><span data-stu-id="d9e49-110">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="d9e49-111">Pour les onglets canal/groupe, les utilisateurs peuvent toujours ouvrir l’onglet dans un navigateur `websiteUrl`distinct via votre `contentUrl` , mais votre sera chargé en premier.</span><span class="sxs-lookup"><span data-stu-id="d9e49-111">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>

<span data-ttu-id="d9e49-112">Une application personnelle est une application avec une portée personnelle.</span><span class="sxs-lookup"><span data-stu-id="d9e49-112">A personal app is an app with a personal scope.</span></span> <span data-ttu-id="d9e49-113">En tant que développeur d’applications, vous avez la possibilité de fournir une version de votre application conçue pour l’utilisateur individuel.</span><span class="sxs-lookup"><span data-stu-id="d9e49-113">As an app developer, you have the option to provide a version of your app that is built for the individual user.</span></span> <span data-ttu-id="d9e49-114">Dans cette version, la collection d’onglets (et le bot, si vous en avez inclus un), est conçue pour la personne.</span><span class="sxs-lookup"><span data-stu-id="d9e49-114">In this version, the collection of tabs (and the bot, if you've included one), are designed for the person.</span></span> <span data-ttu-id="d9e49-115">De cette manière, vous pouvez créer une interaction un-à-un avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d9e49-115">This way, you're able to create a one-on-one interaction with your users.</span></span>

<span data-ttu-id="d9e49-116">Une application personnelle est l’endroit où quelqu’un peut voir tout ce qu’il y a et tous les éléments qu’il a consultés récemment dans l’application.</span><span class="sxs-lookup"><span data-stu-id="d9e49-116">A personal app is where someone can see everything that's theirs, and all the items they've recently viewed in the app.</span></span> <span data-ttu-id="d9e49-117">Il met tout le tout en même lieu.</span><span class="sxs-lookup"><span data-stu-id="d9e49-117">It puts everything in one place.</span></span> <span data-ttu-id="d9e49-118">Dans la capture d’écran suivante, contoso est une application personnelle dans le lanceur d’applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="d9e49-118">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![image du menu de dépassement de l’application](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="d9e49-120">Conseils</span><span class="sxs-lookup"><span data-stu-id="d9e49-120">Guidelines</span></span>

<span data-ttu-id="d9e49-121">Une application personnelle contient généralement les onglets suivants :</span><span class="sxs-lookup"><span data-stu-id="d9e49-121">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="d9e49-122">Votre onglet</span><span class="sxs-lookup"><span data-stu-id="d9e49-122">Your tab</span></span>

<span data-ttu-id="d9e49-123">C’est ici que vos utilisateurs verront toutes leurs choses.</span><span class="sxs-lookup"><span data-stu-id="d9e49-123">This is where your users will see all their stuff.</span></span> <span data-ttu-id="d9e49-124">Il s’agit de son espace personnel.</span><span class="sxs-lookup"><span data-stu-id="d9e49-124">It's their personal space.</span></span> <span data-ttu-id="d9e49-125">L’onglet peut être organisé sous la forme d’une liste, d’une grille, de colonnes ou d’une seule toile... tout ce qui convient le mieux à votre application.</span><span class="sxs-lookup"><span data-stu-id="d9e49-125">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="d9e49-126">Pour plus d’informations sur la conception d’onglets effectifs, voir : [Tabs Design (~/Tabs/Design/Tabs.MD).</span><span class="sxs-lookup"><span data-stu-id="d9e49-126">For additional information on designing effective tabs see: [Tabs design(~/tabs/design/tabs.md).</span></span>

<span data-ttu-id="d9e49-127">Dans la mesure où cet onglet permet d’afficher des éléments provenant de plusieurs canaux, chaque élément doit afficher sa propre équipe, le canal et l’onglet de sorte que l’utilisateur puisse voir facilement où il provient.</span><span class="sxs-lookup"><span data-stu-id="d9e49-127">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

![Onglet tâches personnelles](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="d9e49-129">Récents</span><span class="sxs-lookup"><span data-stu-id="d9e49-129">Recent</span></span>

<span data-ttu-id="d9e49-130">L’onglet **récent** permet à quelqu’un de parcourir tous les utilisateurs qu’il a consultés récemment dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d9e49-130">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="d9e49-131">Elle est classée par ordre chronologique (de la plus récente à la moins récente).</span><span class="sxs-lookup"><span data-stu-id="d9e49-131">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="d9e49-132">Si vous cliquez sur un élément de cette liste, l’utilisateur accède à son canal et à son onglet.</span><span class="sxs-lookup"><span data-stu-id="d9e49-132">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![Onglet récent](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="d9e49-134">Tous</span><span class="sxs-lookup"><span data-stu-id="d9e49-134">All</span></span>

<span data-ttu-id="d9e49-135">Il s’agit d’une liste de tous les onglets de l’organisation de la personne (ceux auxquels ils ont accès, quand même).</span><span class="sxs-lookup"><span data-stu-id="d9e49-135">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="d9e49-136">En d’autres termes, il les affiche partout où l’application est utilisée.</span><span class="sxs-lookup"><span data-stu-id="d9e49-136">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="d9e49-137">Comme avec l’onglet **récent** , si vous sélectionnez un article dans la liste, l’utilisateur est directement associé à l’onglet et au canal appropriés.</span><span class="sxs-lookup"><span data-stu-id="d9e49-137">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="d9e49-138">Bot</span><span class="sxs-lookup"><span data-stu-id="d9e49-138">Bot</span></span>

<span data-ttu-id="d9e49-139">Un bot n’est pas obligatoire, mais il s’agit d’un excellent moyen de communiquer directement et en privé avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d9e49-139">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="d9e49-140">La notification est l’une des fonctions les plus importantes d’une application personnelle et quelle est la meilleure façon de les avertir qu’avec la communication directe ?</span><span class="sxs-lookup"><span data-stu-id="d9e49-140">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="d9e49-141">Les robots fournissent des messages sous la forme de cartes, qui peuvent fournir des informations spécifiques (par exemple, une alerte indiquant que le nouveau contenu est disponible) ou des mises à jour étendues (par exemple, une liste de tâches quotidiennes).</span><span class="sxs-lookup"><span data-stu-id="d9e49-141">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="d9e49-142">Pour plus d’informations sur la conception de robots efficaces, voir : [Bot Design (~/bots/Design/bots.MD).</span><span class="sxs-lookup"><span data-stu-id="d9e49-142">For additional information on designing effective bots see: [Bot design(~/bots/design/bots.md).</span></span>

![Message d’accueil bot](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="d9e49-144">Aide et paramètres</span><span class="sxs-lookup"><span data-stu-id="d9e49-144">Help and Settings</span></span>

<span data-ttu-id="d9e49-145">Le contenu de l’aide permet aux utilisateurs de découvrir les nuances de votre application.</span><span class="sxs-lookup"><span data-stu-id="d9e49-145">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="d9e49-146">Ajoutez un onglet **paramètres** pour leur donner la possibilité de le personnaliser.</span><span class="sxs-lookup"><span data-stu-id="d9e49-146">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="d9e49-147">À propos</span><span class="sxs-lookup"><span data-stu-id="d9e49-147">About</span></span>

<span data-ttu-id="d9e49-148">Incluez un onglet à **propos** de pour fournir des informations telles que le numéro de version, les fonctionnalités, la confidentialité et les liens d’autorisations.</span><span class="sxs-lookup"><span data-stu-id="d9e49-148">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="d9e49-149">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="d9e49-149">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="d9e49-150">Communiquer directement avec vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d9e49-150">Communicate directly with your users</span></span>

<span data-ttu-id="d9e49-151">Utilisez un bot pour informer les utilisateurs des modifications et des nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="d9e49-151">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="d9e49-152">Personnaliser vos onglets...</span><span class="sxs-lookup"><span data-stu-id="d9e49-152">Customize your tabs...</span></span>

<span data-ttu-id="d9e49-153">N’hésitez pas à ajouter d’autres onglets qui aideront vos utilisateurs à accomplir des tâches spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d9e49-153">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="d9e49-154">... et les rendre pertinentes pour chaque utilisateur</span><span class="sxs-lookup"><span data-stu-id="d9e49-154">...and make them relevant to every user</span></span>

<span data-ttu-id="d9e49-155">Chaque onglet que vous déclarez dans le manifeste de votre application est visible par tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d9e49-155">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="d9e49-156">Par exemple, si votre application personnelle est un outil de création de notes de frais qui est utilisé par les responsables et les employés, un onglet **approbation** doit fournir un contenu significatif pour les deux rôles.</span><span class="sxs-lookup"><span data-stu-id="d9e49-156">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
