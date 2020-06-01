---
title: Référence des instructions de conception
description: Décrit les instructions pour la conception d’une application personnelle
keywords: instructions de conception teams structure de référence des applications personnelles
ms.openlocfilehash: f66691234149afa56a6753dd51379c9f2355318e
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455498"
---
# <a name="personal-apps"></a><span data-ttu-id="515f2-104">Applications personnelles</span><span class="sxs-lookup"><span data-stu-id="515f2-104">Personal apps</span></span>

> [!NOTE]
> <span data-ttu-id="515f2-105">La prise en charge complète des onglets sur les clients mobiles est prise en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="515f2-105">Full support for tabs on mobile clients is supported in Teams.</span></span> <span data-ttu-id="515f2-106">Vous devez suivre les [instructions pour les onglets sur mobile](../../tabs/design/tabs-mobile.md) lors de la création d’onglets pour les plateformes mobiles.</span><span class="sxs-lookup"><span data-stu-id="515f2-106">You should follow the [guidance for tabs on mobile](../../tabs/design/tabs-mobile.md) when creating tabs for mobile platforms.</span></span>

<span data-ttu-id="515f2-107">Une application personnelle est une application de teams avec une portée personnelle.</span><span class="sxs-lookup"><span data-stu-id="515f2-107">A personal app is a Teams application with a personal scope.</span></span>  <span data-ttu-id="515f2-108">En tant que développeur d’applications, vous avez la possibilité de fournir une version de votre application qui se concentre sur les interactions avec un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="515f2-108">As an app developer, you have the option to provide a version of your app that focuses on interactions with a single user.</span></span> <span data-ttu-id="515f2-109">Il peut s’agir d’un [bot de conversation](../../bots/what-are-bots.md) pour engager des conversations un-à-un avec un utilisateur ou un [onglet personnel](../../tabs/what-are-tabs.md) qui fournit une expérience Web intégrée.</span><span class="sxs-lookup"><span data-stu-id="515f2-109">It can be a [conversational bot](../../bots/what-are-bots.md) to engage in one-to-one conversations with a user or a [personal tab](../../tabs/what-are-tabs.md) providing an embedded web experience.</span></span> <span data-ttu-id="515f2-110">Les applications personnelles permettent aux utilisateurs d’afficher leur contenu sélectionné à un seul endroit.</span><span class="sxs-lookup"><span data-stu-id="515f2-110">Personal apps enable users to view their select content in one place.</span></span> <span data-ttu-id="515f2-111">Dans la capture d’écran suivante, contoso est une application personnelle dans le lanceur d’applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="515f2-111">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![image du menu de dépassement de l’application](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="515f2-113">Conseils</span><span class="sxs-lookup"><span data-stu-id="515f2-113">Guidelines</span></span>

<span data-ttu-id="515f2-114">Une application personnelle contient généralement les onglets suivants :</span><span class="sxs-lookup"><span data-stu-id="515f2-114">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="515f2-115">Votre onglet</span><span class="sxs-lookup"><span data-stu-id="515f2-115">Your tab</span></span>

<span data-ttu-id="515f2-116">C’est ici que vos utilisateurs verront toutes leurs choses.</span><span class="sxs-lookup"><span data-stu-id="515f2-116">This is where your users will see all their stuff.</span></span> <span data-ttu-id="515f2-117">Il s’agit de son espace personnel.</span><span class="sxs-lookup"><span data-stu-id="515f2-117">It's their personal space.</span></span> <span data-ttu-id="515f2-118">L’onglet peut être organisé sous la forme d’une liste, d’une grille, de colonnes ou d’une seule toile... tout ce qui convient le mieux à votre application.</span><span class="sxs-lookup"><span data-stu-id="515f2-118">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="515f2-119">Pour plus d’informations sur la conception d’onglets effectifs, consultez la rubrique : [Tabs Design](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="515f2-119">For additional information on designing effective tabs see: [Tabs design](../../tabs/design/tabs.md).</span></span>

<span data-ttu-id="515f2-120">Dans la mesure où cet onglet permet d’afficher des éléments provenant de plusieurs canaux, chaque élément doit afficher sa propre équipe, le canal et l’onglet de sorte que l’utilisateur puisse voir facilement où il provient.</span><span class="sxs-lookup"><span data-stu-id="515f2-120">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

![Onglet tâches personnelles](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="515f2-122">Récents</span><span class="sxs-lookup"><span data-stu-id="515f2-122">Recent</span></span>

<span data-ttu-id="515f2-123">L’onglet **récent** permet à quelqu’un de parcourir tous les utilisateurs qu’il a consultés récemment dans votre application.</span><span class="sxs-lookup"><span data-stu-id="515f2-123">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="515f2-124">Elle est classée par ordre chronologique (de la plus récente à la moins récente).</span><span class="sxs-lookup"><span data-stu-id="515f2-124">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="515f2-125">Si vous cliquez sur un élément de cette liste, l’utilisateur accède à son canal et à son onglet.</span><span class="sxs-lookup"><span data-stu-id="515f2-125">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![Onglet récent](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="515f2-127">Tous</span><span class="sxs-lookup"><span data-stu-id="515f2-127">All</span></span>

<span data-ttu-id="515f2-128">Il s’agit d’une liste de tous les onglets de l’organisation de la personne (ceux auxquels ils ont accès, quand même).</span><span class="sxs-lookup"><span data-stu-id="515f2-128">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="515f2-129">En d’autres termes, il les affiche partout où l’application est utilisée.</span><span class="sxs-lookup"><span data-stu-id="515f2-129">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="515f2-130">Comme avec l’onglet **récent** , si vous sélectionnez un article dans la liste, l’utilisateur est directement associé à l’onglet et au canal appropriés.</span><span class="sxs-lookup"><span data-stu-id="515f2-130">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="515f2-131">Bot</span><span class="sxs-lookup"><span data-stu-id="515f2-131">Bot</span></span>

<span data-ttu-id="515f2-132">Un bot n’est pas obligatoire, mais il s’agit d’un excellent moyen de communiquer directement et en privé avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="515f2-132">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="515f2-133">La notification est l’une des fonctions les plus importantes d’une application personnelle et quelle est la meilleure façon de les avertir qu’avec la communication directe ?</span><span class="sxs-lookup"><span data-stu-id="515f2-133">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="515f2-134">Les robots fournissent des messages sous la forme de cartes, qui peuvent fournir des informations spécifiques (par exemple, une alerte indiquant que le nouveau contenu est disponible) ou des mises à jour étendues (par exemple, une liste de tâches quotidiennes).</span><span class="sxs-lookup"><span data-stu-id="515f2-134">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="515f2-135">Pour plus d’informations sur la conception de robots efficaces, consultez la rubrique : [Design bot](../../bots/design/bots.md).</span><span class="sxs-lookup"><span data-stu-id="515f2-135">For additional information on designing effective bots see: [Bot design](../../bots/design/bots.md).</span></span>

![Message d’accueil bot](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="515f2-137">Aide et paramètres</span><span class="sxs-lookup"><span data-stu-id="515f2-137">Help and Settings</span></span>

<span data-ttu-id="515f2-138">Le contenu de l’aide permet aux utilisateurs de découvrir les nuances de votre application.</span><span class="sxs-lookup"><span data-stu-id="515f2-138">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="515f2-139">Ajoutez un onglet **paramètres** pour leur donner la possibilité de le personnaliser.</span><span class="sxs-lookup"><span data-stu-id="515f2-139">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="515f2-140">À propos</span><span class="sxs-lookup"><span data-stu-id="515f2-140">About</span></span>

<span data-ttu-id="515f2-141">Incluez un onglet à **propos** de pour fournir des informations telles que le numéro de version, les fonctionnalités, la confidentialité et les liens d’autorisations.</span><span class="sxs-lookup"><span data-stu-id="515f2-141">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="515f2-142">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="515f2-142">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="515f2-143">Communiquer directement avec vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="515f2-143">Communicate directly with your users</span></span>

<span data-ttu-id="515f2-144">Utilisez un bot pour informer les utilisateurs des modifications et des nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="515f2-144">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="515f2-145">Personnaliser vos onglets...</span><span class="sxs-lookup"><span data-stu-id="515f2-145">Customize your tabs...</span></span>

<span data-ttu-id="515f2-146">N’hésitez pas à ajouter d’autres onglets qui aideront vos utilisateurs à accomplir des tâches spécifiques.</span><span class="sxs-lookup"><span data-stu-id="515f2-146">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="515f2-147">... et les rendre pertinentes pour chaque utilisateur</span><span class="sxs-lookup"><span data-stu-id="515f2-147">...and make them relevant to every user</span></span>

<span data-ttu-id="515f2-148">Chaque onglet que vous déclarez dans le manifeste de votre application est visible par tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="515f2-148">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="515f2-149">Par exemple, si votre application personnelle est un outil de création de notes de frais qui est utilisé par les responsables et les employés, un onglet **approbation** doit fournir un contenu significatif pour les deux rôles.</span><span class="sxs-lookup"><span data-stu-id="515f2-149">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
