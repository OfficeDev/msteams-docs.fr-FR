---
title: Get started - Build your first app overview and prerequisites
author: heath-hamilton
description: Découvrez comment commencer à développer des applications Microsoft Teams et configurer votre environnement.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 4288efdbfada5f1a51fa1d4aeccdd6cdf9c64382
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797896"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="c5f04-103">Créer votre première vue d’ensemble de l’application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c5f04-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="c5f04-104">Dans les **leçons de début,** vous allez apprendre à créer des applications Teams de base.</span><span class="sxs-lookup"><span data-stu-id="c5f04-104">In the **get started** lessons, you learn how to create basic Teams apps.</span></span> <span data-ttu-id="c5f04-105">Chaque didacticiel vous montre comment créer une application Teams simple et réelle tout en vous présentant des outils courants, des concepts fondamentaux et des fonctionnalités plus avancées.</span><span class="sxs-lookup"><span data-stu-id="c5f04-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c5f04-106">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="c5f04-106">What you'll learn</span></span>

<span data-ttu-id="c5f04-107">Voici une idée de ce que vous allez savoir après avoir tiré les leçons.</span><span class="sxs-lookup"><span data-stu-id="c5f04-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="c5f04-108">Mise en route rapide avec le **Shared Computer Toolkit Teams**: le Shared Computer Toolkit Microsoft Teams pour Visual Studio Code s’occupe de la création de votre projet d’application et de la création d’une application en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c5f04-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="c5f04-109">**Configurez votre application avec App Studio :** spécifiez les fonctionnalités et les services que votre application Teams utilise.</span><span class="sxs-lookup"><span data-stu-id="c5f04-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="c5f04-110">**Étendue de l’audience de votre application**: créez une application Teams pour un usage personnel, la collaboration ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c5f04-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
> * <span data-ttu-id="c5f04-111">**Obtenez de l’expérience avec les outils et les SDK Teams**: personnalisez votre application avec l’aide du SDK client JavaScript teams.</span><span class="sxs-lookup"><span data-stu-id="c5f04-111">**Get experience with Teams tools and SDKs**: Customize your app with help from the Teams JavaScript client SDK.</span></span> <span data-ttu-id="c5f04-112">Par exemple, modifiez le jeu de couleurs de votre application pour qu’il corresponde au thème Teams.</span><span class="sxs-lookup"><span data-stu-id="c5f04-112">For example, change your app's color scheme to match the Teams theme.</span></span> <span data-ttu-id="c5f04-113">Découvrez également les outils courants pour créer et gérer des bots.</span><span class="sxs-lookup"><span data-stu-id="c5f04-113">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="c5f04-114">**Développez votre application**: tout au long des leçons, vous trouverez des rubriques connexes qui vous intéressent probablement (telles que les instructions d’authentification et de conception).</span><span class="sxs-lookup"><span data-stu-id="c5f04-114">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="c5f04-115">Principes de base de l’application Teams</span><span class="sxs-lookup"><span data-stu-id="c5f04-115">Teams app fundamentals</span></span>

<span data-ttu-id="c5f04-116">Avant de commencer les didacticiels, vous devez connaître les informations suivantes sur la création d’applications pour Teams.</span><span class="sxs-lookup"><span data-stu-id="c5f04-116">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="c5f04-117">Les applications peuvent avoir plusieurs fonctionnalités et points d’entrée</span><span class="sxs-lookup"><span data-stu-id="c5f04-117">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="c5f04-118">Une application Teams est composé d’une ou de plusieurs fonctionnalités de plateforme [(comment](../concepts/capabilities-overview.md) les personnes utilisent l’application) et [de points](../concepts/extensibility-points.md) d’entrée (où les personnes utilisent l’application).</span><span class="sxs-lookup"><span data-stu-id="c5f04-118">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people use the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="c5f04-119">Teams n’héberge pas votre application</span><span class="sxs-lookup"><span data-stu-id="c5f04-119">Teams doesn't host your app</span></span>

<span data-ttu-id="c5f04-120">Une application Teams comprend les éléments importants suivants :</span><span class="sxs-lookup"><span data-stu-id="c5f04-120">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="c5f04-121">La logique, le stockage des données et les appels d’API qui sont à l’alimentation de votre application.</span><span class="sxs-lookup"><span data-stu-id="c5f04-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="c5f04-122">Ces services ne sont pas hébergés par Teams et doivent être accessibles via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c5f04-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="c5f04-123">Client Teams (web, de bureau ou mobile) où les utilisateurs utilisent votre application.</span><span class="sxs-lookup"><span data-stu-id="c5f04-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="c5f04-124">Votre ID d’application, qui vous permet de configurer votre application avec App Studio.</span><span class="sxs-lookup"><span data-stu-id="c5f04-124">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="c5f04-125">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="c5f04-125">Get prerequisites</span></span>

<span data-ttu-id="c5f04-126">Vérifiez que vous avez le bon compte pour créer des applications Teams et installez certains outils de développement recommandés.</span><span class="sxs-lookup"><span data-stu-id="c5f04-126">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="c5f04-127">Configurer votre compte de développement</span><span class="sxs-lookup"><span data-stu-id="c5f04-127">Set up your development account</span></span>

<span data-ttu-id="c5f04-128">Vous avez besoin d’un compte Teams qui autorise le chargement de version de version d’application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c5f04-128">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="c5f04-129">(Votre compte peut déjà le fournir.)</span><span class="sxs-lookup"><span data-stu-id="c5f04-129">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="c5f04-130">Si vous avez un compte Teams, vérifiez si vous pouvez télécharger une version de version de chargement d’applications dans Teams :</span><span class="sxs-lookup"><span data-stu-id="c5f04-130">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="c5f04-131">Dans le client Teams, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5f04-131">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="c5f04-132">Recherchez une option pour **télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="c5f04-132">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="c5f04-134"><b>Sélectionnez ici</b> si vous ne pouvez pas voir l’option de chargement de version de version ou si vous n’avez pas de compte Teams.</span><span class="sxs-lookup"><span data-stu-id="c5f04-134"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="c5f04-135">Vous pouvez obtenir un compte de test Teams gratuit qui permet le chargement de version test d’application en rejoignant le programme microsoft 365 développeur.</span><span class="sxs-lookup"><span data-stu-id="c5f04-135">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="c5f04-136">(Le processus d’inscription prend environ deux minutes.)</span><span class="sxs-lookup"><span data-stu-id="c5f04-136">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="c5f04-137">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="c5f04-137">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="c5f04-138">Sélectionnez **Rejoindre maintenant** et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="c5f04-138">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="c5f04-139">Lorsque vous arrivez à l’écran d’accueil, **sélectionnez Configurer l’abonnement E5.**</span><span class="sxs-lookup"><span data-stu-id="c5f04-139">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="c5f04-140">Configurer votre compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c5f04-140">Set up your administrator account.</span></span> <span data-ttu-id="c5f04-141">Une fois que vous avez terminé, vous devriez voir un écran comme celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c5f04-141">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrire au programme pour les développeurs Microsoft 365.":::
1. <span data-ttu-id="c5f04-143">Connectez-vous à Teams à l’aide du compte d’administrateur que vous viennent de configurer.</span><span class="sxs-lookup"><span data-stu-id="c5f04-143">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="c5f04-144">Vérifiez si vous avez désormais l’option **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="c5f04-144">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="c5f04-145">Si vous ne pouvez toujours pas charger une version de version de chargement d’applications, voir activer les applications Teams personnalisées et activer le chargement [d’applications personnalisées.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)</span><span class="sxs-lookup"><span data-stu-id="c5f04-145">If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="c5f04-146">Installer vos outils de développement</span><span class="sxs-lookup"><span data-stu-id="c5f04-146">Install your development tools</span></span>

<span data-ttu-id="c5f04-147">Vous pouvez créer des applications Teams avec vos outils préférés, mais ces leçons montrent comment vous pouvez commencer rapidement avec microsoft Teams Shared Computer Toolkit for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c5f04-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="c5f04-148">Teams affiche le contenu de l’application uniquement par le biais de connexions HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c5f04-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="c5f04-149">Pour déboguer certains types d’applications localement, comme un bot, vous allez apprendre à utiliser [ngrok](../concepts/build-and-test/debug.md#locally-hosted) pour configurer un tunnel sécurisé entre Teams et votre application.</span><span class="sxs-lookup"><span data-stu-id="c5f04-149">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="c5f04-150">(Les applications De Production Teams sont hébergées dans le cloud.)</span><span class="sxs-lookup"><span data-stu-id="c5f04-150">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="c5f04-151">Installez [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="c5f04-151">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="c5f04-152">Installez [ngrok](https://ngrok.com/download) si vous prévoyez de créer un bot ou une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="c5f04-152">Install [ngrok](https://ngrok.com/download) if you plan to build a bot or messaging extension.</span></span>
1. <span data-ttu-id="c5f04-153">Installez la dernière version de [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="c5f04-153">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="c5f04-154">(Les versions antérieures peuvent ne pas fonctionner avec le kit de ressources.)</span><span class="sxs-lookup"><span data-stu-id="c5f04-154">(Earlier versions might not work with the toolkit.)</span></span>
1. In Visual Studio Code, select **Extensions** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: on the left Activity Bar and install the Microsoft Teams **Shared Computer Toolkit**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Illustration montrant où, dans Visual Studio Code, vous pouvez installer l’extension Shared Computer Toolkit Microsoft Teams.":::

## <a name="about-the-tutorials"></a><span data-ttu-id="c5f04-157">À propos des didacticiels</span><span class="sxs-lookup"><span data-stu-id="c5f04-157">About the tutorials</span></span>

<span data-ttu-id="c5f04-158">Vous pouvez commencer par les leçons de **démarrage de** Teams.</span><span class="sxs-lookup"><span data-stu-id="c5f04-158">You can start with any of the Teams **get started** lessons.</span></span> <span data-ttu-id="c5f04-159">Si vous ne savez pas où aller en premier, suivez notre chemin d’accès convivial débutant et créez un « Hello, World! »</span><span class="sxs-lookup"><span data-stu-id="c5f04-159">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="c5f04-160">application.</span><span class="sxs-lookup"><span data-stu-id="c5f04-160">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Arborescence de compétences montrant les parcours d’apprentissage pour les leçons de « mise en route » de Teams." border="false":::

## <a name="next-step"></a><span data-ttu-id="c5f04-162">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="c5f04-162">Next step</span></span>

<span data-ttu-id="c5f04-163">Une fois que vous avez installé votre compte et votre environnement, vous pouvez commencer la création.</span><span class="sxs-lookup"><span data-stu-id="c5f04-163">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="c5f04-164">Didacticiel convivial pour débutant</span><span class="sxs-lookup"><span data-stu-id="c5f04-164">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c5f04-165">Créer une application « Hello, World! »</span><span class="sxs-lookup"><span data-stu-id="c5f04-165">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="c5f04-166">Autres didacticiels</span><span class="sxs-lookup"><span data-stu-id="c5f04-166">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c5f04-167">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="c5f04-167">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="c5f04-168">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="c5f04-168">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
