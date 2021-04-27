---
title: Intégrer les applications Web
author: Rajeshwari-v
description: Vue d'ensemble de l'intégration des applications web et des fonctionnalités d'appareil à l'application Microsoft Teams.
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 6493f493b2bfc67a23aebfb5142aff60cf0afe93
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020239"
---
# <a name="integrate-web-apps"></a><span data-ttu-id="c7e38-103">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="c7e38-103">Integrate web apps</span></span>

<span data-ttu-id="c7e38-104">Vous pouvez fournir une expérience utilisateur enrichie en intégrant les fonctionnalités d'une application web existante à la plateforme Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-104">You can provide an enriched user experience by integrating the features of an existing web application into Microsoft Teams platform.</span></span> <span data-ttu-id="c7e38-105">Veillez à suivre [les instructions de conception teams](~/concepts/design/understand-use-cases.md) pour rendre votre application native de Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-105">Ensure to follow [Teams design guidelines](~/concepts/design/understand-use-cases.md) to make your app native to Teams.</span></span>
<span data-ttu-id="c7e38-106">Ce document fournit une vue d'ensemble des conditions préalables à l'intégration d'applications web à Teams, à la plateforme Power pour créer des applications Power, des agents virtuels Power, un Assistant virtuel, des modèles d'application, des connecteurs Shift, Le LMS En forme d'enfant, la création d'un bouton Partager avec Teams pour votre site web, l'ajout d'un onglet Microsoft Teams dans SharePoint, la création de liens profonds et l'intégration de fonctionnalités d'appareil.</span><span class="sxs-lookup"><span data-stu-id="c7e38-106">This document gives an overview of prerequisites to integrate web applications with Teams, Power platform to create Power apps, Power Virtual Agents, Virtual Assistant, app templates, Shift connectors, Moodle LMS, creating a Share-to-Teams button for your website, adding a Microsoft Teams tab in SharePoint, creating deep links, and integrating device capabilities.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7e38-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7e38-107">Prerequisites</span></span>   

<span data-ttu-id="c7e38-108">Pour une intégration efficace, veillez à mieux comprendre les conditions préalables suivantes :</span><span class="sxs-lookup"><span data-stu-id="c7e38-108">For effective integration, ensure to have a better understanding of the following prerequisites:</span></span>
* <span data-ttu-id="c7e38-109">Fonctionnalités teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-109">Teams capabilities.</span></span> 
* <span data-ttu-id="c7e38-110">Conditions requises par SharePoint pour le stockage de fichiers et de données.</span><span class="sxs-lookup"><span data-stu-id="c7e38-110">SharePoint requirements for file and data storage.</span></span>
* <span data-ttu-id="c7e38-111">Conditions requises pour les API.</span><span class="sxs-lookup"><span data-stu-id="c7e38-111">API requirements.</span></span>
* <span data-ttu-id="c7e38-112">Authentification.</span><span class="sxs-lookup"><span data-stu-id="c7e38-112">Authentication.</span></span>
* <span data-ttu-id="c7e38-113">Liaison approfondie de votre application avec Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-113">Deep linking of your app with Teams.</span></span>
* <span data-ttu-id="c7e38-114">Maposez les cas d'utilisation de votre application sur les fonctionnalités de la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-114">Map your app's use cases to Teams platform capabilities.</span></span>
* <span data-ttu-id="c7e38-115">Déterminez les points d'entrée de votre application, tels que l'utilisation personnelle, la collaboration ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c7e38-115">Determine your app's entry points, such as personal use, collaboration, or both.</span></span>

## <a name="low-code-platforms"></a><span data-ttu-id="c7e38-116">Plateformes de code faible</span><span class="sxs-lookup"><span data-stu-id="c7e38-116">Low code platforms</span></span>

<span data-ttu-id="c7e38-117">Les plateformes à code faible offrent une approche intuitive du développement de logiciels et nécessitent peu ou pas de codage pour créer des applications et des processus.</span><span class="sxs-lookup"><span data-stu-id="c7e38-117">Low code platforms provide an intuitive approach to software development and require little or no coding to build applications and processes.</span></span> <span data-ttu-id="c7e38-118">Vous pouvez créer facilement des applications personnalisées avec des plateformes à code faible.</span><span class="sxs-lookup"><span data-stu-id="c7e38-118">You can create custom apps easily with low code platforms.</span></span> <span data-ttu-id="c7e38-119">Ces plateformes se composent d'une interface visuelle, de connecteurs vers des services back end et d'un système de gestion du cycle de vie des applications intégré pour créer, déboguer, déployer et gérer des applications.</span><span class="sxs-lookup"><span data-stu-id="c7e38-119">These platforms consist of a visual interface, connectors to back end services, and a built-in app lifecycle management system to build, debug, deploy, and maintain applications.</span></span> <span data-ttu-id="c7e38-120">Microsoft fournit les passerelles innovantes suivantes pour créer rapidement des applications compatibles avec Teams à l'aide d'attributs de code faible :</span><span class="sxs-lookup"><span data-stu-id="c7e38-120">Microsoft provides the following innovative gateways to rapidly build Teams-compatible apps using low code attributes:</span></span>
* <span data-ttu-id="c7e38-121">Plateforme Microsoft Power</span><span class="sxs-lookup"><span data-stu-id="c7e38-121">Microsoft Power platform</span></span>
* <span data-ttu-id="c7e38-122">Modèles d'application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c7e38-122">Microsoft Teams app templates</span></span>

## <a name="microsoft-power-platform"></a><span data-ttu-id="c7e38-123">Plateforme Microsoft Power</span><span class="sxs-lookup"><span data-stu-id="c7e38-123">Microsoft Power platform</span></span>

<span data-ttu-id="c7e38-124">La plateforme Microsoft Power combine quatre technologies Microsoft robustes, telles que Power BI, Power Apps, Power Automate et Power Virtual Agents dans une plateforme d’application puissante.</span><span class="sxs-lookup"><span data-stu-id="c7e38-124">Microsoft Power platform combines four robust Microsoft technologies, such as Power BI, Power Apps, Power Automate, and Power Virtual Agents in one powerful application platform.</span></span> <span data-ttu-id="c7e38-125">Ces technologies vous permettent de créer des solutions, d’automatiser des processus, d’analyser des données et de créer des agents virtuels dans un environnement unifié et intégré.</span><span class="sxs-lookup"><span data-stu-id="c7e38-125">These technologies empower you to build solutions, automate processes, analyze data, and create virtual agents within a unified and integrated environment.</span></span>

### <a name="power-apps"></a><span data-ttu-id="c7e38-126">Power Apps</span><span class="sxs-lookup"><span data-stu-id="c7e38-126">Power Apps</span></span>

<span data-ttu-id="c7e38-127">Avec Power Apps, vous pouvez créer des applications d’entreprise qui se connectent à vos données métiers et sont adaptées aux besoins de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c7e38-127">With Power Apps, you can build business apps that connect to your business data and are tailored to your organization's needs.</span></span> <span data-ttu-id="c7e38-128">Power Apps permet de mettre en place un large éventail de scénarios d’application pour relever les défis de l’entreprise par le biais d’applications de canevas.</span><span class="sxs-lookup"><span data-stu-id="c7e38-128">Power Apps enable a wide range of app scenarios to solve business challenges through canvas apps.</span></span> <span data-ttu-id="c7e38-129">Après avoir construit l’application, vous pouvez l’exporter à partir du portail Fabricant de Power Apps et l’incorporer dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-129">After building the app, you can export it from the Power Apps maker portal and embed in Microsoft Teams.</span></span>

### <a name="power-virtual-agents"></a><span data-ttu-id="c7e38-130">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="c7e38-130">Power Virtual Agents</span></span>

<span data-ttu-id="c7e38-131">Power Virtual Agent est une solution d’interface graphique guidée sans code.</span><span class="sxs-lookup"><span data-stu-id="c7e38-131">Power Virtual Agent is a no code, guided graphical interface solution.</span></span> <span data-ttu-id="c7e38-132">Il repose sur microsoft Power Platform et Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c7e38-132">It is built on the Microsoft Power Platform and the Bot Framework.</span></span> <span data-ttu-id="c7e38-133">Il permet à chaque membre de votre équipe de créer et de gérer des chatbots de conversation enrichis qui s’intègrent facilement à la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-133">It empowers every member of your team to create and maintain rich conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="c7e38-134">Vous pouvez concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement, à créer un service web ou à vous inscrire directement à Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c7e38-134">You can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment, create a web service, or directly register with the Bot Framework.</span></span>

### <a name="create-virtual-assistant"></a><span data-ttu-id="c7e38-135">Créer un Assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="c7e38-135">Create Virtual Assistant</span></span>

<span data-ttu-id="c7e38-136">Assistant virtuel est un modèle open source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant un contrôle total de l’expérience utilisateur, de la marque organisationnelle et des données nécessaires.</span><span class="sxs-lookup"><span data-stu-id="c7e38-136">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> 

## <a name="app-templates"></a><span data-ttu-id="c7e38-137">Modèles d’application</span><span class="sxs-lookup"><span data-stu-id="c7e38-137">App templates</span></span>

<span data-ttu-id="c7e38-138">Vous pouvez utiliser un modèle d’application pour créer des applications personnalisées en fonction des besoins de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c7e38-138">You can use app template to create custom made apps to suit your organizational needs.</span></span> <span data-ttu-id="c7e38-139">Ce sont des applications prêtes pour la production pour Microsoft Teams qui sont pilotées par la communauté, open source et disponibles sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="c7e38-139">These are production-ready apps for Microsoft Teams that are community driven, open-source, and available on GitHub.</span></span> <span data-ttu-id="c7e38-140">Chaque modèle contient des instructions détaillées pour déployer et installer l’application pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c7e38-140">Each template contains detailed instructions to deploy and install the app for your organization.</span></span> <span data-ttu-id="c7e38-141">Il fournit une application prête à l’emploi que vous pouvez installer et commencer à utiliser immédiatement.</span><span class="sxs-lookup"><span data-stu-id="c7e38-141">It provides a ready-to-use application that you can install and start using immediately.</span></span> 

## <a name="teams-shifts-work-force-management-connectors"></a><span data-ttu-id="c7e38-142">Teams shifts Work Force Management connectors</span><span class="sxs-lookup"><span data-stu-id="c7e38-142">Teams Shifts Work Force Management connectors</span></span>

<span data-ttu-id="c7e38-143">Teams Shifts Work Force Management connectors are production-ready, open-source, and community-driven integrations.</span><span class="sxs-lookup"><span data-stu-id="c7e38-143">Teams Shifts Work Force Management connectors are production-ready, open-source, and community-driven integrations.</span></span> <span data-ttu-id="c7e38-144">Ils offrent une expérience transparente et un processus rapide pour la transformation numérique des employés de première ligne avec Teams Shifts.</span><span class="sxs-lookup"><span data-stu-id="c7e38-144">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span>

## <a name="install-moodle-lms"></a><span data-ttu-id="c7e38-145">Installer Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="c7e38-145">Install Moodle LMS</span></span>

<span data-ttu-id="c7e38-146">Il s'agit d'un système LMS (Learning Management System) open source populaire.</span><span class="sxs-lookup"><span data-stu-id="c7e38-146">Moodle is a popular open-source Learning Management System (LMS).</span></span> <span data-ttu-id="c7e38-147">Il est désormais intégré à Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-147">It is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="c7e38-148">Cette intégration permet aux enseignants et aux enseignants de collaborer autour des cours De céseurs, de poser des questions sur les notes et les devoirs, et de rester à jour avec des notifications directement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-148">This integration helps educators and teachers to collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

## <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="c7e38-149">Créer un bouton Partager vers Teams sur votre site web</span><span class="sxs-lookup"><span data-stu-id="c7e38-149">Create a Share-to-Teams button for your website</span></span>

<span data-ttu-id="c7e38-150">Les sites web tiers peuvent utiliser le script de lancement pour incorporer des boutons Partager dans Teams sur leurs pages web.</span><span class="sxs-lookup"><span data-stu-id="c7e38-150">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages.</span></span> <span data-ttu-id="c7e38-151">Lorsque vous sélectionnez le bouton, il lance l'expérience Partager avec Teams dans une fenêtre fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c7e38-151">When you select the button, it launches the Share to Teams experience in a pop-up window.</span></span> <span data-ttu-id="c7e38-152">Cela vous permet de partager un lien directement avec une personne ou un canal Microsoft Teams sans changer de contexte.</span><span class="sxs-lookup"><span data-stu-id="c7e38-152">This allows you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a><span data-ttu-id="c7e38-153">Ajouter un onglet Microsoft Teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="c7e38-153">Add a Microsoft Teams tab in SharePoint</span></span>

<span data-ttu-id="c7e38-154">Vous pouvez obtenir une expérience d'intégration enrichie entre Microsoft Teams et SharePoint en ajoutant un onglet Microsoft Teams dans SharePoint en tant que partie Web SPFx.</span><span class="sxs-lookup"><span data-stu-id="c7e38-154">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> 

## <a name="create-deep-link"></a><span data-ttu-id="c7e38-155">Créer un lien profond</span><span class="sxs-lookup"><span data-stu-id="c7e38-155">Create deep link</span></span>

<span data-ttu-id="c7e38-156">Vous pouvez créer des liens profonds vers les entités dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-156">You can create deep links to the entities in Teams.</span></span> <span data-ttu-id="c7e38-157">Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-157">You can create links to information and features within Teams.</span></span> <span data-ttu-id="c7e38-158">Ces liens profonds naviguent vers le contenu et les informations de votre onglet. Vous pouvez utiliser des liens profonds pour lier votre application à Teams, car ils relient plusieurs éléments d'une application pour une expérience Teams plus native.</span><span class="sxs-lookup"><span data-stu-id="c7e38-158">These deep links navigate to content and information within your tab. You can use deep links to link your app with Teams as they tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="integrate-device-capabilities"></a><span data-ttu-id="c7e38-159">Intégrer les fonctionnalités de l'appareil</span><span class="sxs-lookup"><span data-stu-id="c7e38-159">Integrate device capabilities</span></span>

<span data-ttu-id="c7e38-160">La plateforme Microsoft Teams améliore en permanence les capacités des développeurs en s'alignant sur les expériences intégrées de la première partie.</span><span class="sxs-lookup"><span data-stu-id="c7e38-160">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="c7e38-161">La plateforme Teams améliorée permet aux partenaires d'accéder et d'intégrer les fonctionnalités natives de l'appareil, telles que l'appareil photo, le scanneur de QR ou de code-barres, la galerie de photos, le microphone et l'emplacement à l'aide d'API dédiées disponibles dans le SDK client JavaScript microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c7e38-161">The enhanced Teams platform allows partners to access and integrate the native device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location using dedicated APIs available in Microsoft Teams JavaScript client SDK.</span></span> 

## <a name="see-also"></a><span data-ttu-id="c7e38-162">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c7e38-162">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-163">Ma cartographier les cas d'utilisation de votre application sur les fonctionnalités de la plateforme Teams</span><span class="sxs-lookup"><span data-stu-id="c7e38-163">Map your app's use cases to Teams platform capabilities</span></span>](~/concepts/design/map-use-cases.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-164">Déterminer les points d'entrée de votre application</span><span class="sxs-lookup"><span data-stu-id="c7e38-164">Determine your app's entry points</span></span>](~/concepts/extensibility-points.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-165">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="c7e38-165">Integrate web apps</span></span>](~/samples/integrating-web-apps.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-166">Créer des applications personnalisées à code faible pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c7e38-166">Create low-code custom apps for Microsoft Teams</span></span>](~/samples/teams-low-code-solutions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-167">Ajouter un chatbot Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="c7e38-167">Add a Power Virtual Agents chatbot</span></span>](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-168">Créer un assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="c7e38-168">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-169">Modèles d’application pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c7e38-169">App templates for Microsoft Teams</span></span>](~/samples/app-templates.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-170">Connecteurs Shift prêts pour la production</span><span class="sxs-lookup"><span data-stu-id="c7e38-170">Production-ready Shift Connectors</span></span>](~/samples/shifts-wfm-connectors.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-171">Installer Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="c7e38-171">Install Moodle LMS</span></span>](~/resources/moodleinstructions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-172">Créer un bouton de partage Teams</span><span class="sxs-lookup"><span data-stu-id="c7e38-172">Create a Share-to-Teams button</span></span>](~/concepts/build-and-test/share-to-teams.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-173">Ajouter un onglet Teams à SharePoint</span><span class="sxs-lookup"><span data-stu-id="c7e38-173">Add a Teams tab to SharePoint</span></span>](~/tabs/how-to/tabs-in-sharepoint.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-174">Créer des liens plus étroits</span><span class="sxs-lookup"><span data-stu-id="c7e38-174">Create deep links</span></span>](~/concepts/build-and-test/deep-links.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e38-175">Fonctionnalités de l’appareil</span><span class="sxs-lookup"><span data-stu-id="c7e38-175">Device capabilities</span></span>](~/concepts/device-capabilities/device-capabilities-overview.md)
