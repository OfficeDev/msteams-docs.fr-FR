---
title: Get started - Build your first app overview and prerequisites
author: girliemac
description: Découvrez comment prendre en Microsoft Teams développement d’applications et configurer votre environnement.
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: dae942be9383ef1e0a931d238e6148651f334ef5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565878"
---
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="140d5-103">Prendre en Microsoft Teams développement d’applications</span><span class="sxs-lookup"><span data-stu-id="140d5-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="140d5-104">Créez une application simple pour découvrir les principes de base du Teams développement d’applications.</span><span class="sxs-lookup"><span data-stu-id="140d5-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="140d5-105">Une fois que vous avez vu « Hello, World! », essayez l’un des autres articles de mise en ligne pour plus d’informations sur les outils courants, les concepts fondamentaux et les fonctionnalités avancées.</span><span class="sxs-lookup"><span data-stu-id="140d5-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="140d5-106">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="140d5-106">What you'll learn</span></span>

* <span data-ttu-id="140d5-107">Préparez-vous rapidement avec l’extension Teams Shared Computer Toolkit, une extension Visual Studio Code’extension.</span><span class="sxs-lookup"><span data-stu-id="140d5-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension.</span></span> 
* <span data-ttu-id="140d5-108">Configurez votre application avec App Studio.</span><span class="sxs-lookup"><span data-stu-id="140d5-108">Configure your app with App Studio.</span></span>
* <span data-ttu-id="140d5-109">Familiarisez-vous Teams des outils de développement et des SDK.</span><span class="sxs-lookup"><span data-stu-id="140d5-109">Get familiar with Teams developer tools and SDKs.</span></span>
* <span data-ttu-id="140d5-110">Prenez en compte Teams concepts d’application, tels que l’authentification et les meilleures pratiques en matière de conception.</span><span class="sxs-lookup"><span data-stu-id="140d5-110">Consider important Teams app concepts, such as authentication and design best practices.</span></span>

<span data-ttu-id="140d5-111">Vous pouvez créer une application Teams à l’aide de n’importe quelle technologie de votre choix, par exemple, l’interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="140d5-111">You can build a Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="140d5-112">Toutefois, ces articles vous aident à commencer avec les outils et technologies recommandés suivants :</span><span class="sxs-lookup"><span data-stu-id="140d5-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="140d5-113">Teams Shared Computer Toolkit, une extension Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="140d5-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="140d5-114">React.js pour les onglets</span><span class="sxs-lookup"><span data-stu-id="140d5-114">React.js for tabs</span></span>
* <span data-ttu-id="140d5-115">Node.js pour les bots et les extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="140d5-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="140d5-116">Teams de base de l’application</span><span class="sxs-lookup"><span data-stu-id="140d5-116">Teams app fundamentals</span></span>

<span data-ttu-id="140d5-117">Vous pouvez créer des applications Teams personnalisées pour vous-même, les personnes de votre organisation ou les personnes du monde entier.</span><span class="sxs-lookup"><span data-stu-id="140d5-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="140d5-118">Avant de commencer, vous devez comprendre les concepts fondamentaux suivants concernant Teams développement d’applications :</span><span class="sxs-lookup"><span data-stu-id="140d5-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="140d5-119">Cas d’utilisation d’applications courants</span><span class="sxs-lookup"><span data-stu-id="140d5-119">Common app use cases</span></span>

<span data-ttu-id="140d5-120">Voici quelques scénarios classiques qu’une application Teams personnalisée peut vous aider :</span><span class="sxs-lookup"><span data-stu-id="140d5-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="140d5-121">Incorporez du contenu web, tel qu’une application web ou une partie d’un site web, dans Teams client.</span><span class="sxs-lookup"><span data-stu-id="140d5-121">Embed web-based content, such as a web app or part of a website, in the Teams client.</span></span>
* <span data-ttu-id="140d5-122">Recherchez rapidement des informations dans un autre système et ajoutez-les à une conversation Teams conversation.</span><span class="sxs-lookup"><span data-stu-id="140d5-122">Look up information quickly in another system and adding it to a Teams conversation.</span></span>
* <span data-ttu-id="140d5-123">Déclencher des flux de travail et des processus directement à partir de ce qui est dit dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="140d5-123">Trigger workflows and processes directly from what's said in a conversation.</span></span>

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="140d5-124">Fonctionnalités et outils de l’application</span><span class="sxs-lookup"><span data-stu-id="140d5-124">App capabilities and tools</span></span>

<span data-ttu-id="140d5-125">Une application est composé d’un ou de plusieurs Teams et de points d’interaction utilisateur.</span><span class="sxs-lookup"><span data-stu-id="140d5-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="140d5-126">Votre groupe d’outils de développement varie en fonction des fonctionnalités que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="140d5-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="140d5-127">**Fonctionnalités de l’application**</span><span class="sxs-lookup"><span data-stu-id="140d5-127">**App capabilities**</span></span>| <span data-ttu-id="140d5-128">**Points d’interaction**</span><span class="sxs-lookup"><span data-stu-id="140d5-128">**Interaction points**</span></span> | <span data-ttu-id="140d5-129">**Outils recommandés**</span><span class="sxs-lookup"><span data-stu-id="140d5-129">**Recommended tools**</span></span> | <span data-ttu-id="140d5-130">**Kits de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="140d5-130">**SDKs**</span></span> | <span data-ttu-id="140d5-131">**Piles technologiques**</span><span class="sxs-lookup"><span data-stu-id="140d5-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="140d5-132">Onglets</span><span class="sxs-lookup"><span data-stu-id="140d5-132">Tabs</span></span> | <span data-ttu-id="140d5-133">Espaces dans lequel les utilisateurs peuvent interagir avec du contenu web incorporé dans des contextes personnels et partagés.</span><span class="sxs-lookup"><span data-stu-id="140d5-133">Spaces where users can interact with embedded web content in personal and shared contexts.</span></span> | <span data-ttu-id="140d5-134">VS Code avec une extension Teams Shared Computer Toolkit ou le générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="140d5-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="140d5-135">Kit de développement logiciel client JavaScript Teams</span><span class="sxs-lookup"><span data-stu-id="140d5-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="140d5-136">Technologies web générales (HTML, CSS et JavaScript) ou React.js</span><span class="sxs-lookup"><span data-stu-id="140d5-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="140d5-137">Bots</span><span class="sxs-lookup"><span data-stu-id="140d5-137">Bots</span></span> | <span data-ttu-id="140d5-138">Chatbots qui interagissent avec les utilisateurs dans des contextes personnels et partagés.</span><span class="sxs-lookup"><span data-stu-id="140d5-138">Chatbots that interact with users in personal and shared contexts.</span></span> | <span data-ttu-id="140d5-139">VS Code avec une extension Teams Shared Computer Toolkit ou le générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="140d5-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="140d5-140">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="140d5-140">Bot Framework SDK</span></span> | <span data-ttu-id="140d5-141">Node.js, C# ou Python</span><span class="sxs-lookup"><span data-stu-id="140d5-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="140d5-142">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="140d5-142">Messaging extensions</span></span> | <span data-ttu-id="140d5-143">Raccourcis pour insérer du contenu d’application ou agir sur un message sans sortir de la conversation.</span><span class="sxs-lookup"><span data-stu-id="140d5-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> | <span data-ttu-id="140d5-144">VS Code avec une extension Teams Shared Computer Toolkit ou le générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="140d5-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="140d5-145">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="140d5-145">Bot Framework SDK</span></span> | <span data-ttu-id="140d5-146">Node.js, C# ou Python</span><span class="sxs-lookup"><span data-stu-id="140d5-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="140d5-147">Teams n’héberge pas votre application</span><span class="sxs-lookup"><span data-stu-id="140d5-147">Teams doesn't host your app</span></span>

<span data-ttu-id="140d5-148">Lorsqu’un utilisateur installe votre application dans Teams, il installe uniquement un package d’application qui contient un fichier de configuration (également appelé manifeste d’application) et les icônes de votre application.</span><span class="sxs-lookup"><span data-stu-id="140d5-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="140d5-149">La logique et le stockage de données de votre application sont hébergés ailleurs, tels que les services web Azure ou l’hôte local pendant le développement.</span><span class="sxs-lookup"><span data-stu-id="140d5-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="140d5-150">Teams accède à ces ressources via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="140d5-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Illustration showing your app on Teams is pointing to your app logic in the cloud server.":::

## <a name="next-step"></a><span data-ttu-id="140d5-152">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="140d5-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="140d5-153">Créer et exécuter votre première application Teams de messagerie</span><span class="sxs-lookup"><span data-stu-id="140d5-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
