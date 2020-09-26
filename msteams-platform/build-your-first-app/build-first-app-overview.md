---
title: Commencer à créer une application de première équipe
author: heath-hamilton
description: Vue d’ensemble et conditions préalables à la création d’une application Microsoft teams
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 7431230487f1644de8b17b0b9e143819395b7527
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279708"
---
# <a name="build-your-first-teams-app-overview"></a><span data-ttu-id="a20a4-103">Vue d’ensemble de la création de votre première application teams</span><span class="sxs-lookup"><span data-stu-id="a20a4-103">Build your first Teams app overview</span></span>

<span data-ttu-id="a20a4-104">Dans les leçons créer **votre première application** , vous créez des applications teams de base.</span><span class="sxs-lookup"><span data-stu-id="a20a4-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="a20a4-105">Chaque Didacticiel explique comment créer une application de teams simple et réelle de teams tout en vous présentant des outils courants, des concepts fondamentaux et des fonctionnalités plus avancées.</span><span class="sxs-lookup"><span data-stu-id="a20a4-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="a20a4-106">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="a20a4-106">What you'll learn</span></span>

<span data-ttu-id="a20a4-107">Voici une idée de ce que vous saurez après les leçons.</span><span class="sxs-lookup"><span data-stu-id="a20a4-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="a20a4-108">**Soyez rapidement opérationnel avec Team Toolkit**: Microsoft teams Toolkit for Visual Studio code s’occupe de la création de votre projet d’application et de votre génération de modèles automatique afin que vous puissiez utiliser une application en cours d’exécution en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a20a4-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="a20a4-109">**Définissez votre application avec le manifeste**: le manifeste de l’application est l’endroit où vous spécifiez les capacités et les services utilisés par votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="a20a4-109">**Define your app with the manifest**: The app manifest is where you specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="a20a4-110">**Portée de l’audience de votre application**: créez une application de teams pour l’utilisation personnelle, la collaboration ou les deux.</span><span class="sxs-lookup"><span data-stu-id="a20a4-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="a20a4-111">**Obtenez de l’expérience avec Team frameworks**: Personnalisez votre application (par exemple, modifiez son jeu de couleurs pour qu’elle corresponde au thème Teams) avec l’aide du kit de développement logiciel JavaScript de teams.</span><span class="sxs-lookup"><span data-stu-id="a20a4-111">**Get experience with Teams frameworks**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="a20a4-112">En savoir plus sur les outils courants de création et de gestion des robots.</span><span class="sxs-lookup"><span data-stu-id="a20a4-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="a20a4-113">**Développez votre application**: tout au long des leçons, vous trouverez des rubriques connexes qui vous intéresseront probablement (telles que les instructions de conception et d’authentification).</span><span class="sxs-lookup"><span data-stu-id="a20a4-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="a20a4-114">Principes fondamentaux des applications teams</span><span class="sxs-lookup"><span data-stu-id="a20a4-114">Teams app fundamentals</span></span>

<span data-ttu-id="a20a4-115">Avant de commencer les didacticiels, vous devez connaître les points suivants relatifs à la création d’applications pour Teams.</span><span class="sxs-lookup"><span data-stu-id="a20a4-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="a20a4-116">Les applications peuvent avoir plusieurs fonctionnalités et points d’entrée</span><span class="sxs-lookup"><span data-stu-id="a20a4-116">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="a20a4-117">Les applications teams se composent d’une ou de plusieurs [fonctionnalités de plateforme](../concepts/capabilities-overview.md) et de [points d’entrée](../concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="a20a4-117">Teams apps are made up of one or more [platform capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="a20a4-118">Vous pouvez présenter votre application à l’aide d’un certain nombre de [composants et de conventions d’interface utilisateur](../concepts/extensibility-points.md#ui-components)propres à Teams, tels que des cartes et des modules de tâches.</span><span class="sxs-lookup"><span data-stu-id="a20a4-118">You can present your app using a number of Teams-specific [UI components and conventions](../concepts/extensibility-points.md#ui-components), such as cards and task modules.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="a20a4-119">Teams n’héberge pas votre application</span><span class="sxs-lookup"><span data-stu-id="a20a4-119">Teams doesn't host your app</span></span>

<span data-ttu-id="a20a4-120">Une application teams comprend trois parties importantes :</span><span class="sxs-lookup"><span data-stu-id="a20a4-120">A Teams app includes three important pieces:</span></span>

* <span data-ttu-id="a20a4-121">La logique, le stockage de données et les appels d’API qui alimentent votre application.</span><span class="sxs-lookup"><span data-stu-id="a20a4-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="a20a4-122">Ces services ne sont pas hébergés par teams et doivent être accessibles via HTTPs.</span><span class="sxs-lookup"><span data-stu-id="a20a4-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="a20a4-123">Le client Teams (Web, de bureau ou mobile) où les utilisateurs utilisent votre application.</span><span class="sxs-lookup"><span data-stu-id="a20a4-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="a20a4-124">Votre package d’application, que vous utilisez pour installer l’application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="a20a4-124">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="a20a4-125">Il contient des métadonnées d’application et des pointeurs vers vos services hébergés.</span><span class="sxs-lookup"><span data-stu-id="a20a4-125">It contains app metadata and pointers to your hosted services.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="a20a4-126">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="a20a4-126">Get prerequisites</span></span>

<span data-ttu-id="a20a4-127">Vérifiez que vous disposez du compte approprié pour créer des applications teams et installer des outils de développement recommandés.</span><span class="sxs-lookup"><span data-stu-id="a20a4-127">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="a20a4-128">Configurer votre compte de développement</span><span class="sxs-lookup"><span data-stu-id="a20a4-128">Set up your development account</span></span>

<span data-ttu-id="a20a4-129">Vous avez besoin d’un compte teams qui autorise les chargement d’applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="a20a4-129">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="a20a4-130">(Il est possible que votre compte vous fournisse déjà.)</span><span class="sxs-lookup"><span data-stu-id="a20a4-130">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="a20a4-131">Si vous disposez d’un compte Teams, vérifiez si vous pouvez chargement des applications dans teams :</span><span class="sxs-lookup"><span data-stu-id="a20a4-131">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="a20a4-132">Dans le client Teams, sélectionnez **applications**.</span><span class="sxs-lookup"><span data-stu-id="a20a4-132">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="a20a4-133">Recherchez une option permettant de **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="a20a4-133">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où, dans Teams, vous pouvez télécharger une application personnalisée.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="a20a4-135"><b>Sélectionnez ici</b> si vous ne voyez pas l’option chargement ou si vous ne disposez pas d’un compte Teams.</span><span class="sxs-lookup"><span data-stu-id="a20a4-135"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="a20a4-136">Vous pouvez obtenir un compte de test gratuit teams qui autorise l’application chargement en rejoignant le programme de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="a20a4-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="a20a4-137">(Le processus d’inscription prend environ deux minutes.)</span><span class="sxs-lookup"><span data-stu-id="a20a4-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="a20a4-138">Accédez au [programme de développement Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="a20a4-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="a20a4-139">Sélectionnez **rejoindre** et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="a20a4-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="a20a4-140">Lorsque vous accédez à l’écran d’accueil, sélectionnez **configurer l’abonnement E5**.</span><span class="sxs-lookup"><span data-stu-id="a20a4-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="a20a4-141">Configurez votre compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a20a4-141">Set up your administrator account.</span></span> <span data-ttu-id="a20a4-142">Une fois que vous avez terminé, un écran semblable à celui-ci s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a20a4-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrit au programme pour les développeurs Microsoft 365.":::
1. <span data-ttu-id="a20a4-144">Connectez-vous à teams à l’aide du compte d’administrateur que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="a20a4-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="a20a4-145">Vérifiez si vous disposez maintenant de l’option **Télécharger une application personnalisée** .</span><span class="sxs-lookup"><span data-stu-id="a20a4-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

### <a name="install-your-development-tools"></a><span data-ttu-id="a20a4-146">Installer vos outils de développement</span><span class="sxs-lookup"><span data-stu-id="a20a4-146">Install your development tools</span></span>

<span data-ttu-id="a20a4-147">Vous pouvez créer des applications teams avec vos outils préférés, mais ces leçons montrent comment vous pouvez commencer rapidement avec Microsoft teams Toolkit pour Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="a20a4-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="a20a4-148">Teams affiche le contenu de l’application uniquement via les connexions HTTPs.</span><span class="sxs-lookup"><span data-stu-id="a20a4-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="a20a4-149">Étant donné que vous hébergerez votre première application localement pour gagner du temps, vous apprendrez à utiliser [ngrok pour configurer un tunnel sécurisé](../concepts/build-and-test/debug.md#locally-hosted) entre teams et votre application.</span><span class="sxs-lookup"><span data-stu-id="a20a4-149">Since you'll host your first app locally to save time, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="a20a4-150">(Les applications teams de niveau production sont hébergées dans le Cloud.)</span><span class="sxs-lookup"><span data-stu-id="a20a4-150">(Production-level Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="a20a4-151">Installez [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="a20a4-151">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="a20a4-152">Installez [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="a20a4-152">Install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="a20a4-153">Installez la dernière version de [Visual Studio code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="a20a4-153">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="a20a4-154">(Les versions antérieures peuvent ne pas fonctionner avec la boîte à outils.)</span><span class="sxs-lookup"><span data-stu-id="a20a4-154">(Earlier versions might not work with the toolkit.)</span></span>
1. Dans Visual Studio code, sélectionnez **Extensions** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: sur la barre d’activité de gauche et installez le kit de développement **Microsoft teams**.
    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Illustration montrant où dans Visual Studio code vous pouvez installer l’extension Microsoft teams Toolkit.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="a20a4-157">À propos des didacticiels</span><span class="sxs-lookup"><span data-stu-id="a20a4-157">About the tutorials</span></span>

<span data-ttu-id="a20a4-158">Vous pouvez commencer avec n’importe quelle équipe de **création de votre première** expérience d’application.</span><span class="sxs-lookup"><span data-stu-id="a20a4-158">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="a20a4-159">Si vous ne savez pas où commencer, suivez notre chemin convivial et créez un « Hello, World ! ».</span><span class="sxs-lookup"><span data-stu-id="a20a4-159">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="a20a4-160">Phone.</span><span class="sxs-lookup"><span data-stu-id="a20a4-160">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Arborescence des compétences montrant des cursus pour les didacticiels « créer vos premières applications » Teams." border="false":::

## <a name="next-step"></a><span data-ttu-id="a20a4-162">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a20a4-162">Next step</span></span>

<span data-ttu-id="a20a4-163">Une fois que vous avez configuré votre compte et votre environnement, vous pouvez commencer à créer.</span><span class="sxs-lookup"><span data-stu-id="a20a4-163">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="a20a4-164">Didacticiel convivial</span><span class="sxs-lookup"><span data-stu-id="a20a4-164">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a20a4-165">Créer une application « Hello, World ! »</span><span class="sxs-lookup"><span data-stu-id="a20a4-165">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="a20a4-166">Autres didacticiels</span><span class="sxs-lookup"><span data-stu-id="a20a4-166">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a20a4-167">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="a20a4-167">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="a20a4-168">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="a20a4-168">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)