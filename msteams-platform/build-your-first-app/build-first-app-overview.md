---
title: Get started - Build your first app overview and prerequisites
author: girliemac
description: Découvrez comment commencer à développer des applications Microsoft Teams et configurer votre environnement.
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: 3bc99c535ea659f046b65dc26d9a60de0dd49cab
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068565"
---
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="eaf9c-103">Mise en place du développement d’applications Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="eaf9c-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="eaf9c-104">Créez une application simple pour découvrir les principes de base du développement d’applications Teams.</span><span class="sxs-lookup"><span data-stu-id="eaf9c-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="eaf9c-105">Une fois que vous avez vu « Hello, World! », essayez l’un des autres articles de mise en ligne pour plus d’informations sur les outils courants, les concepts fondamentaux et les fonctionnalités avancées.</span><span class="sxs-lookup"><span data-stu-id="eaf9c-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="eaf9c-106">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="eaf9c-106">What you'll learn</span></span>

* <span data-ttu-id="eaf9c-107">Rapidement opérationnel avec la Shared Computer Toolkit Teams, une extension Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="eaf9c-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension</span></span> 
* <span data-ttu-id="eaf9c-108">Configurer votre application avec App Studio</span><span class="sxs-lookup"><span data-stu-id="eaf9c-108">Configure your app with App Studio</span></span> 
* <span data-ttu-id="eaf9c-109">Familiarisez-vous avec les outils de développement et les SDK Teams</span><span class="sxs-lookup"><span data-stu-id="eaf9c-109">Get familiar with Teams developer tools and SDKs</span></span>
* <span data-ttu-id="eaf9c-110">Prenez en compte les concepts importants de l’application Teams, tels que l’authentification et les meilleures pratiques en matière de conception</span><span class="sxs-lookup"><span data-stu-id="eaf9c-110">Consider important Teams app concepts, such as authentication and design best practices</span></span>

<span data-ttu-id="eaf9c-111">Vous pouvez créer une application Teams à l’aide de n’importe quelle technologie de votre choix, par exemple, l’interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="eaf9c-111">You can build Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="eaf9c-112">Toutefois, ces articles vous aident à commencer avec les outils et technologies recommandés suivants :</span><span class="sxs-lookup"><span data-stu-id="eaf9c-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="eaf9c-113">Teams Shared Computer Toolkit, une extension Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="eaf9c-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="eaf9c-114">React.js pour les onglets</span><span class="sxs-lookup"><span data-stu-id="eaf9c-114">React.js for tabs</span></span>
* <span data-ttu-id="eaf9c-115">Node.js pour les bots et les extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="eaf9c-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="eaf9c-116">Principes de base de l’application Teams</span><span class="sxs-lookup"><span data-stu-id="eaf9c-116">Teams app fundamentals</span></span>

<span data-ttu-id="eaf9c-117">Vous pouvez créer des applications Teams personnalisées pour vous-même, les personnes de votre organisation ou les personnes du monde entier.</span><span class="sxs-lookup"><span data-stu-id="eaf9c-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="eaf9c-118">Avant de commencer, vous devez comprendre les concepts fondamentaux suivants concernant le développement d’applications Teams :</span><span class="sxs-lookup"><span data-stu-id="eaf9c-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="eaf9c-119">Cas d’utilisation d’applications courants</span><span class="sxs-lookup"><span data-stu-id="eaf9c-119">Common app use cases</span></span>

<span data-ttu-id="eaf9c-120">Voici quelques scénarios classiques qu’une application Teams personnalisée peut vous aider :</span><span class="sxs-lookup"><span data-stu-id="eaf9c-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="eaf9c-121">Incorporer du contenu web, tel qu'une application web ou une partie d'un site web, dans le client Teams</span><span class="sxs-lookup"><span data-stu-id="eaf9c-121">Embed web-based content, such as a web app or part of a website, in the Teams client</span></span>
* <span data-ttu-id="eaf9c-122">Rechercher rapidement des informations dans un autre système et les ajouter à une conversation Teams</span><span class="sxs-lookup"><span data-stu-id="eaf9c-122">Look up information quickly in another system and adding it to a Teams conversation</span></span> 
* <span data-ttu-id="eaf9c-123">Déclencher des flux de travail et des processus directement à partir de ce qui est dit dans une conversation</span><span class="sxs-lookup"><span data-stu-id="eaf9c-123">Trigger workflows and processes directly from what's said in a conversation</span></span> 

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="eaf9c-124">Fonctionnalités et outils de l'application</span><span class="sxs-lookup"><span data-stu-id="eaf9c-124">App capabilities and tools</span></span>

<span data-ttu-id="eaf9c-125">Une application est composé d'une ou de plusieurs fonctionnalités Teams et de points d'interaction utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eaf9c-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="eaf9c-126">Votre groupe d'outils de développement varie en fonction des fonctionnalités que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="eaf9c-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="eaf9c-127">**Fonctionnalités de l’application**</span><span class="sxs-lookup"><span data-stu-id="eaf9c-127">**App capabilities**</span></span>| <span data-ttu-id="eaf9c-128">**Points d'interaction**</span><span class="sxs-lookup"><span data-stu-id="eaf9c-128">**Interaction points**</span></span> | <span data-ttu-id="eaf9c-129">**Outils recommandés**</span><span class="sxs-lookup"><span data-stu-id="eaf9c-129">**Recommended tools**</span></span> | <span data-ttu-id="eaf9c-130">**Kits de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="eaf9c-130">**SDKs**</span></span> | <span data-ttu-id="eaf9c-131">**Piles technologiques**</span><span class="sxs-lookup"><span data-stu-id="eaf9c-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="eaf9c-132">Onglets</span><span class="sxs-lookup"><span data-stu-id="eaf9c-132">Tabs</span></span> | <span data-ttu-id="eaf9c-133">Espaces dans lequel les utilisateurs peuvent interagir avec du contenu web incorporé dans des contextes personnels et partagés</span><span class="sxs-lookup"><span data-stu-id="eaf9c-133">Spaces where users can interact with embedded web content in personal and shared contexts</span></span> | <span data-ttu-id="eaf9c-134">Vs Code avec l'extension Shared Computer Toolkit Teams ou le générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="eaf9c-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="eaf9c-135">Kit de développement logiciel client JavaScript Teams</span><span class="sxs-lookup"><span data-stu-id="eaf9c-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="eaf9c-136">Technologies web générales (HTML, CSS et JavaScript) ou React.js</span><span class="sxs-lookup"><span data-stu-id="eaf9c-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="eaf9c-137">Bots</span><span class="sxs-lookup"><span data-stu-id="eaf9c-137">Bots</span></span> | <span data-ttu-id="eaf9c-138">Chatbots qui interagissent avec les utilisateurs dans des contextes personnels et partagés</span><span class="sxs-lookup"><span data-stu-id="eaf9c-138">Chatbots that interact with users in personal and shared contexts</span></span> | <span data-ttu-id="eaf9c-139">Vs Code avec l'extension Shared Computer Toolkit Teams ou le générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="eaf9c-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="eaf9c-140">SDK Bot Botework SDK</span><span class="sxs-lookup"><span data-stu-id="eaf9c-140">Bot Franework SDK</span></span> | <span data-ttu-id="eaf9c-141">Node.js, C# ou Python</span><span class="sxs-lookup"><span data-stu-id="eaf9c-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="eaf9c-142">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="eaf9c-142">Messaging extensions</span></span> | <span data-ttu-id="eaf9c-143">Raccourcis pour insérer du contenu d'application ou agir sur un message sans sortir de la conversation</span><span class="sxs-lookup"><span data-stu-id="eaf9c-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation</span></span> | <span data-ttu-id="eaf9c-144">Vs Code avec l'extension Shared Computer Toolkit Teams ou le générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="eaf9c-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="eaf9c-145">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="eaf9c-145">Bot Framework SDK</span></span> | <span data-ttu-id="eaf9c-146">Node.js, C# ou Python</span><span class="sxs-lookup"><span data-stu-id="eaf9c-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="eaf9c-147">Teams n'héberge pas votre application</span><span class="sxs-lookup"><span data-stu-id="eaf9c-147">Teams doesn't host your app</span></span>

<span data-ttu-id="eaf9c-148">Lorsqu'un utilisateur installe votre application dans Teams, il installe uniquement un package d'application qui contient un fichier de configuration (également appelé manifeste d'application) et les icônes de votre application.</span><span class="sxs-lookup"><span data-stu-id="eaf9c-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="eaf9c-149">La logique et le stockage de données de votre application sont hébergés ailleurs, tels que les services web Azure ou l'hôte local pendant le développement.</span><span class="sxs-lookup"><span data-stu-id="eaf9c-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="eaf9c-150">Teams accède à ces ressources via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eaf9c-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Illustration showing your app on Teams is pointing to your app logic in the cloud server.":::

## <a name="next-step"></a><span data-ttu-id="eaf9c-152">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="eaf9c-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eaf9c-153">Créer et exécuter votre première application Teams</span><span class="sxs-lookup"><span data-stu-id="eaf9c-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
