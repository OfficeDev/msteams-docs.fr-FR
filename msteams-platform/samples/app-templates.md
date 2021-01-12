---
title: Modèles d’application Microsoft Teams
description: Liens et descriptions des modèles d’application pour la plateforme Microsoft Teams
ms.topic: reference
keywords: Démonstration des exemples de modèles Microsoft Teams
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 4a9b2ee9a5fadfa86dead4a15f49a6cea67d4963
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795487"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="cd520-104">Modèles d’application pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cd520-104">App Templates for Microsoft Teams</span></span>

<span data-ttu-id="cd520-105">Les modèles d’application sont des applications prêtes pour la production pour Microsoft Teams qui sont pilotées par la communauté, open source et disponibles sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="cd520-105">App templates are production-ready apps for Microsoft Teams that are community driven, open-source, and available on GitHub.</span></span> <span data-ttu-id="cd520-106">Chacune contient des instructions détaillées sur le déploiement et l’installation de cette application pour votre organisation, en fournissant une application prête à l’emploi que vous pouvez installer et commencer à utiliser immédiatement.</span><span class="sxs-lookup"><span data-stu-id="cd520-106">Each contains detailed instructions for deploying and installing that app for your organization, providing a ready-to-use app that you can install and begin using immediately.</span></span> <span data-ttu-id="cd520-107">Le code source complet est également disponible. Vous pouvez donc l’explorer en détail ou le modifier pour répondre à vos besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="cd520-107">The complete source code is available as well, so you can explore it in detail, or fork the code and alter it to meet your specific needs.</span></span>

<span data-ttu-id="cd520-108">**&#9734; indique les modèles d’application nouvellement publiés.**</span><span class="sxs-lookup"><span data-stu-id="cd520-108">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="cd520-109">Principaux avantages</span><span class="sxs-lookup"><span data-stu-id="cd520-109">Key benefits</span></span>

* <span data-ttu-id="cd520-110">**Expérience de plug-and-play :** Tous les modèles d’application incluent des scripts de déploiement qui vous permettent d’héberger tous les services nécessaires dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cd520-110">**Plug and play experience:** All app templates include deployments scripts that will allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="cd520-111">Aucun codage n’est requis pour déployer les applications.</span><span class="sxs-lookup"><span data-stu-id="cd520-111">No coding is required to deploy the apps.</span></span>
* <span data-ttu-id="cd520-112">**Code prêt pour la production :** Les modèles d’application respectent les meilleures pratiques recommandées en matière de sécurité et d’infrastructure, et toutes les modifications que la communauté leur a soumises sont examinées afin de garantir une conformité continue.</span><span class="sxs-lookup"><span data-stu-id="cd520-112">**Production-ready code:** The app templates conform to recommended best practices around security and infrastructure, and all community submitted changes to them are reviewed to ensure continued conformance.</span></span>
* <span data-ttu-id="cd520-113">**Personnalisables et extensibles :** Bien que tous les modèles d’application soient prêts à être déployés tels qu’ils sont, nous fournissons l’ensemble des scripts de base de code et de déploiement afin que vous pouvez facilement les personnaliser ou les étendre pour répondre à vos besoins uniques.</span><span class="sxs-lookup"><span data-stu-id="cd520-113">**Customizable and extensible:** While all app templates are ready to deploy as they are, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="cd520-114">**Documentation détaillée & prise en charge :** Tous les modèles d’application sont accompagnés d’une documentation de bout en bout sur l’architecture de la solution, le déploiement et les étapes de configuration.</span><span class="sxs-lookup"><span data-stu-id="cd520-114">**Detailed documentation & support:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="cd520-115">Les référentiels sont également surveillés. Veuillez donc signaler les problèmes que vous rencontrez en signalant un problème sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="cd520-115">The repositories are monitored as well, so please report any issues you encounter by raising an Issue on GitHub.</span></span>

## <a name="appointment-manager-9734"></a><span data-ttu-id="cd520-116">Gestionnaire de rendez-vous &#9734;</span><span class="sxs-lookup"><span data-stu-id="cd520-116">Appointment Manager &#9734;</span></span>

<span data-ttu-id="cd520-117">Le Gestionnaire de rendez-vous est un modèle d’application Teams pour aider les entreprises à créer, gérer et mener des rendez-vous virtuels avec des clients via Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-117">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="cd520-118">Les nouvelles demandes de rendez-vous des consommateurs sont visibles dans les canaux Teams, où ils peuvent rapidement être affectés et réassignés au personnel d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="cd520-118">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="cd520-119">Les demandes de rendez-vous peuvent être vues à des niveaux d’équipe ou personnels via des onglets personnalisés.</span><span class="sxs-lookup"><span data-stu-id="cd520-119">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="cd520-120">Chaque rendez-vous est associé à une réunion en ligne Teams, de ce fait, le personnel et les consommateurs peuvent facilement participer à la réunion à l’heure prévue.</span><span class="sxs-lookup"><span data-stu-id="cd520-120">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="cd520-121">Le modèle d’application s’intègre à Microsoft Bookings pour faciliter la gestion des rendez-vous.</span><span class="sxs-lookup"><span data-stu-id="cd520-121">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="cd520-122">Les rendez-vous programmés apparaissent automatiquement sur les calendriers des membres du personnel affectés, et les consommateurs reçoivent des notifications et rappels par courrier électronique personnalisables avec des liens de réunion incorporés.</span><span class="sxs-lookup"><span data-stu-id="cd520-122">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="cd520-123">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-123">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="cd520-124">![Vue d’ensemble du ](../assets/images/appointment-manager-overview.png)
 ![ gestionnaire de rendez-vous dans Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="cd520-124">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="cd520-125">Demander l’absence</span><span class="sxs-lookup"><span data-stu-id="cd520-125">Ask Away</span></span>

<span data-ttu-id="cd520-126">Ask Away est un [bot Microsoft Teams](../bots/what-are-bots.md) qui permet aux utilisateurs d’effectuer des sessions Q&(questions et réponses) au sein de Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-126">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="cd520-127">À l’aide du bot Ask Away, les membres de l’équipe peuvent soumettre et voter des questions partagées par des collègues, ce qui permet aux hôtes Q&A de collecter facilement des questions les plus importantes au sein d’un canal ou d’une conversation.</span><span class="sxs-lookup"><span data-stu-id="cd520-127">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="cd520-128">Le bot peut être utilisé pour mener une session de questions-réponses en temps réel&une réunion Teams et permet aux participants de soumettre des questions en direct via la conversation.</span><span class="sxs-lookup"><span data-stu-id="cd520-128">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="cd520-129">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-129">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Affichage de la boîte de dialogue de la fenêtre d’affichage du classement pour que les utilisateurs votent sur des questions](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="cd520-131">Informations du collaborateur</span><span class="sxs-lookup"><span data-stu-id="cd520-131">Associate Insights</span></span>

<span data-ttu-id="cd520-132">Associate Insights est un modèle [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) qui permet aux employés de première ligne de capturer et d’envoyer directement l’opinion, l’opinion et la perception des clients.</span><span class="sxs-lookup"><span data-stu-id="cd520-132">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="cd520-133">Les employés de première ligne sont souvent le premier représentant de l’entreprise à contacter des clients dans un point de contact un-à-un.</span><span class="sxs-lookup"><span data-stu-id="cd520-133">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="cd520-134">Les données collectées peuvent être partagées et utilisées en collaboration par les équipes professionnelles, par exemple, via un onglet Power BI Teams, pour améliorer le produit et améliorer l’expérience client.</span><span class="sxs-lookup"><span data-stu-id="cd520-134">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="cd520-135">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-135">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Affichage des commentaires sur les informations générées par l’application](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vue Power BI des informations générées par l’application](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="cd520-138">Présence</span><span class="sxs-lookup"><span data-stu-id="cd520-138">Attendance</span></span>

<span data-ttu-id="cd520-139">L’application De présence est un [onglet Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) qui peut être épinglé dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="cd520-139">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="cd520-140">Il est conçu pour enregistrer la présence, généralement dans des paramètres tels que des environnements d’apprentissage et de formation.</span><span class="sxs-lookup"><span data-stu-id="cd520-140">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="cd520-141">Les utilisateurs peuvent marquer ou modifier l’assistance jusqu’à 30 jours dans le passé et afficher des rapports de présence récapitulés pour un groupe entier ou des participants individuels.</span><span class="sxs-lookup"><span data-stu-id="cd520-141">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="cd520-142">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-142">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Démonstration de l’application de participation](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="cd520-144">Réserver une salle</span><span class="sxs-lookup"><span data-stu-id="cd520-144">Book-a-room</span></span>

<span data-ttu-id="cd520-145">Book-a-room est un [bot Microsoft Teams](../bots/what-are-bots.md) qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pendant 30 (par défaut), 60 ou 90 minutes à partir de l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="cd520-145">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="cd520-146">Le bot Book-a-room s’étendue à des conversations personnelles ou 1:1.</span><span class="sxs-lookup"><span data-stu-id="cd520-146">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="cd520-147">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-147">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Démonstration du livre dans une salle](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="cd520-149">Création d’un accès</span><span class="sxs-lookup"><span data-stu-id="cd520-149">Building Access</span></span>

<span data-ttu-id="cd520-150">Building Access est une application basée sur microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)qui prend en charge l’administration de seuils d’occupation et de normes de d’éloignement social en permettant aux directeurs des installations de gérer, de suivre et de signaler la présence des employés sur site.</span><span class="sxs-lookup"><span data-stu-id="cd520-150">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="cd520-151">L’application, conçue à l’aide de Microsoft [Power Apps](/powerapps/powerapps-overview)et [Power Automate,](/power-automate/getting-started)s’intègre de façon profonde à Microsoft Teams et permet aux organisations de déterminer la préparation, d’établir des critères d’éligibilité pour l’accès sur site et de recueillir des informations pour la planification future.</span><span class="sxs-lookup"><span data-stu-id="cd520-151">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="cd520-152">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-152">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Création d’une carte de réservation Access](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Création d’une vue de touche d’accès rapide](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="cd520-155">Célébrations</span><span class="sxs-lookup"><span data-stu-id="cd520-155">Celebrations</span></span>

<span data-ttu-id="cd520-156">La fête est une application Teams qui permet aux membres de l’équipe de se faire une fête d’anniversaire, d’anniversaires et d’autres événements périodiques.</span><span class="sxs-lookup"><span data-stu-id="cd520-156">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="cd520-157">Il se souvenir des événements spéciaux de tous les membres de l’équipe et envoie un message convivial dans toutes les équipes sélectionnées au moment de la création de l’événement, pour que les membres de l’équipe se sentent spéciaux lors de leur journée.</span><span class="sxs-lookup"><span data-stu-id="cd520-157">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="cd520-158">L’application fournit une interface simple permettant à tous les membres de l’équipe d’ajouter et d’afficher leurs événements, et permet également à l’utilisateur de sélectionner les équipes dans lesquelles les événements sont partagés.</span><span class="sxs-lookup"><span data-stu-id="cd520-158">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="cd520-159">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-159">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="cd520-160">Liste de vérification</span><span class="sxs-lookup"><span data-stu-id="cd520-160">Checklist</span></span>

<span data-ttu-id="cd520-161">La liste de contrôle est une application [d’extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Microsoft Teams personnalisée qui vous permet de collaborer avec votre équipe en créant une liste de contrôle partagée dans une conversation ou un canal.</span><span class="sxs-lookup"><span data-stu-id="cd520-161">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="cd520-162">L’application est prise en charge sur tous les clients de la plateforme Teams (bureau, navigateur, iOS et Android) et est prête pour le déploiement dans le cadre de votre abonnement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="cd520-162">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="cd520-163">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-163">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Créer une liste de contrôle en affichage Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a><span data-ttu-id="cd520-165">Classe &#9734;</span><span class="sxs-lookup"><span data-stu-id="cd520-165">Classroom Drop-in &#9734;</span></span>

<span data-ttu-id="cd520-166">Classroom Drop-in est une application basée sur la plateforme Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)qui permet aux responsables système de rechercher des équipes de classe (salles de classe virtuelles) et de s’ajouter eux-mêmes ou d’autres à ces équipes de cours pour une période de présentation spécifiée, selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="cd520-166">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="cd520-167">L’application conçue à l’aide de Microsoft [Power Apps](/powerapps/powerapps-overview) et [Power Automate](/power-automate/getting-started), s’intègre en profondeur à Microsoft Teams pour garantir que les établissements d’enseignement peuvent optimiser leurs opérations dans un environnement d’apprentissage hybride en fournissant l’accès aux parties prenantes pertinentes pour les équipes de classe par besoins de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="cd520-167">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="cd520-168">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-168">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Demande de salle de classe](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="cd520-170">Communicateur d’entreprise</span><span class="sxs-lookup"><span data-stu-id="cd520-170">Company Communicator</span></span>

<span data-ttu-id="cd520-171">L’application Communicator entreprise permet aux équipes d’entreprise de créer et d’envoyer des messages destinés à plusieurs équipes ou à un grand nombre d’employés par conversation, ce qui permet à l’organisation d’atteindre les employés là où elles collaborent.</span><span class="sxs-lookup"><span data-stu-id="cd520-171">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="cd520-172">Utilisez ce modèle pour plusieurs scénarios tels que les annonces de nouvelles initiatives, l’intégration des employés, l’apprentissage et le développement modernes ou les diffusions à l’échelle de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="cd520-172">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="cd520-173">L’application fournit une interface simple pour que les utilisateurs désignés créent, prévisualiser, collaborent et envoient des messages.</span><span class="sxs-lookup"><span data-stu-id="cd520-173">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="cd520-174">Il fournit une base pour créer des fonctionnalités de communication ciblées personnalisées telles que la télémétrie personnalisée sur le nombre d’utilisateurs reconnus ou ayant interagi avec un message.</span><span class="sxs-lookup"><span data-stu-id="cd520-174">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="cd520-175">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-175">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![Affichage de la zone Communicator composition jCompany](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="cd520-177">Recherche de groupe de contacts</span><span class="sxs-lookup"><span data-stu-id="cd520-177">Contact Group Lookup</span></span>

<span data-ttu-id="cd520-178">L’application de recherche de groupe de contacts offre une approche pratique et utile pour la création, l’accès et la gestion des groupes de contacts de votre organisation (anciennement appelés listes de distribution ou groupes de communication).</span><span class="sxs-lookup"><span data-stu-id="cd520-178">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="cd520-179">Les utilisateurs peuvent rapidement afficher et discuter avec les membres du groupe, afficher l’état des membres et créer une conversation de groupe avec des membres sélectionnés dans le groupe de contacts, le tout dans l’environnement Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-179">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="cd520-180">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-180">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Vue favoris épinglés de la recherche de groupe de contacts](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Démonstration de démarrage de conversation de recherche de groupe de contacts](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation-9734"></a><span data-ttu-id="cd520-183">Co-worker &#9734;</span><span class="sxs-lookup"><span data-stu-id="cd520-183">Co-worker Appreciation &#9734;</span></span>

<span data-ttu-id="cd520-184">À l’aide du modèle de collaboration de Microsoft Teams, les utilisateurs peuvent reconnaître les succès de leurs collègues dans le contexte de Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-184">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="cd520-185">Lorsque des collègues choisissent de récompenser un collègue, les destinataires et les autres membres de l’équipe sont marqués dans une conversation de canal et reçoivent une notification concernant les détails de l’attribution du canal.</span><span class="sxs-lookup"><span data-stu-id="cd520-185">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="cd520-186">Les prix sont enregistrés dans l’application Teams, qui est sécurisée, portable et facilement partageable.</span><span class="sxs-lookup"><span data-stu-id="cd520-186">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="cd520-187">Cela peut être considéré comme la version powerApps du modèle d’application Open Badges, avec un classement.</span><span class="sxs-lookup"><span data-stu-id="cd520-187">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="cd520-188">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-188">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![Globalement](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="cd520-190">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="cd520-190">CrowdSourcer</span></span>

<span data-ttu-id="cd520-191">CrowdSourcer est un [bot Microsoft Teams](../bots/what-are-bots.md) qui fournit aux équipes des informations interrogés provenant de façon collaborative à partir des membres du groupe.</span><span class="sxs-lookup"><span data-stu-id="cd520-191">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="cd520-192">Il s’agit d’un excellent moyen de répondre aux questions fréquemment posées tout en permettant aux participants de s’impliquer activement et de contribuer à une ressource d’informations agréable et utile.</span><span class="sxs-lookup"><span data-stu-id="cd520-192">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="cd520-193">L’obtenir sur Github</span><span class="sxs-lookup"><span data-stu-id="cd520-193">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interaction de l’utilisateur final de la source de contenu](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="cd520-195">Autocollants personnalisés</span><span class="sxs-lookup"><span data-stu-id="cd520-195">Custom Stickers</span></span>

<span data-ttu-id="cd520-196">L’expression autonome est essentielle à une culture d’équipe saine.</span><span class="sxs-lookup"><span data-stu-id="cd520-196">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="cd520-197">Ce modèle d’application est une [extension](~/messaging-extensions/what-are-messaging-extensions.md) de messagerie qui permet à vos utilisateurs d’utiliser des autocollants personnalisés et des GIF dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-197">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="cd520-198">Ce modèle offre une expérience de configuration web simple dans laquelle toute personne ayant un accès à la configuration peut télécharger les gif/autocollants/images qu’elle souhaite que ses utilisateurs finaux disposent, ce qui permet à toute votre équipe d’utiliser n’importe quel ensemble d’autocollants que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="cd520-198">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="cd520-199">Cette application permet également de partager facilement des images/GIF/autocollants entre les équipes sans avoir besoin d’accéder aux sites SharePoint ou aux canaux individuels en tant que mécanismes de stockage et de partage.</span><span class="sxs-lookup"><span data-stu-id="cd520-199">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="cd520-200">Par exemple, les équipes produit peuvent facilement partager des images de produit et des GIF sur les réseaux sociaux, le marketing et les équipes commerciales par programme.</span><span class="sxs-lookup"><span data-stu-id="cd520-200">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="cd520-201">Vous pouvez également étendre cette application en déclenchant un flux de notification à des équipes/individus spécifiques lorsque de nouvelles images/GIF sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="cd520-201">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="cd520-202">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-202">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Application Autocollants](../assets/images/stickers.png)

## <a name="employee-ideas-9734"></a><span data-ttu-id="cd520-204">Idées d’employés &#9734;</span><span class="sxs-lookup"><span data-stu-id="cd520-204">Employee Ideas &#9734;</span></span>

<span data-ttu-id="cd520-205">L’application Idées d’employés est la version PowerApps du modèle d’application Bonnes idées basé sur Azure.</span><span class="sxs-lookup"><span data-stu-id="cd520-205">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="cd520-206">L’application permet aux utilisateurs de Teams de configurer et de configurer une campagne d’idées.</span><span class="sxs-lookup"><span data-stu-id="cd520-206">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="cd520-207">Une campagne d’idées est une catégorie de regroupement d’idées autour de thèmes courants.</span><span class="sxs-lookup"><span data-stu-id="cd520-207">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="cd520-208">Les utilisateurs de Teams peuvent également effectuer les activités suivantes :</span><span class="sxs-lookup"><span data-stu-id="cd520-208">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="cd520-209">Configurez un formulaire d’envoi standard que les employés doivent envoyer pour chaque idée.</span><span class="sxs-lookup"><span data-stu-id="cd520-209">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="cd520-210">Examiner et gérer les idées et la liste des campagnes.</span><span class="sxs-lookup"><span data-stu-id="cd520-210">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="cd520-211">Modifier et supprimer des campagnes.</span><span class="sxs-lookup"><span data-stu-id="cd520-211">Modify and delete campaigns.</span></span>
* <span data-ttu-id="cd520-212">Passer en revue les conseils d’idées.</span><span class="sxs-lookup"><span data-stu-id="cd520-212">Review leader boards of ideas.</span></span>
* <span data-ttu-id="cd520-213">Votez pour et partagez des idées prioritaires.</span><span class="sxs-lookup"><span data-stu-id="cd520-213">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="cd520-214">Soumettre des idées pour une campagne.</span><span class="sxs-lookup"><span data-stu-id="cd520-214">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="cd520-215">Afficher l’idée d’un autre membre de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="cd520-215">View other team member's idea.</span></span>
* <span data-ttu-id="cd520-216">Votez sur la plupart des idées aimées.</span><span class="sxs-lookup"><span data-stu-id="cd520-216">Vote on most liked ideas.</span></span>
* <span data-ttu-id="cd520-217">Examinez les performances de leurs idées par rapport aux autres au sein d’une campagne.</span><span class="sxs-lookup"><span data-stu-id="cd520-217">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="cd520-218">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-218">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Gérer l’affichage campagne](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="cd520-220">E-Ent</span><span class="sxs-lookup"><span data-stu-id="cd520-220">E-Prescriptions</span></span> 

<span data-ttu-id="cd520-221">E-Titre est une application [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)qui améliore la télémédique et les soins virtuels en automatisant le processus d’émission de courrier électronique aux patients.</span><span class="sxs-lookup"><span data-stu-id="cd520-221">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="cd520-222">Les professionnels de la santé peuvent rapidement passer en revue les rendez-vous, générer des courriers électroniques et envoyer des courriers électroniques avec des pièces jointes électroniques aux patients directement dans la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-222">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="cd520-223">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-223">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![Capture d’écran de l’application E-Nouvelle.](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Capture d’écran de l’application E-Nouvelle.](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a><span data-ttu-id="cd520-228">Formation des employés</span><span class="sxs-lookup"><span data-stu-id="cd520-228">Employee Training</span></span> 

<span data-ttu-id="cd520-229">La formation des employés est une application Microsoft Teams qui permet aux organisateurs de publier, de suivre et de promouvoir facilement des événements d’apprentissage et de formation pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="cd520-229">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="cd520-230">Avec l’application, les planificateurs d’événements peuvent envoyer des rappels et des notifications aux personnes inscrites aux événements et les employés peuvent indiquer leur intérêt pour les événements à venir, rester informés des événements en cours et partager les détails des événements avec leurs collègues via l’extension de messagerie Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-230">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="cd520-231">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-231">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="cd520-232">**Afficher les événements de formation des employés** ![ Image de l’onglet Formation des employés](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="cd520-232">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="cd520-233">**Créer un événement de formation pour les employés** ![ Formulaire de création d’événements pour la formation des employés](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="cd520-233">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="cd520-234">Expert Finder</span><span class="sxs-lookup"><span data-stu-id="cd520-234">Expert Finder</span></span>

<span data-ttu-id="cd520-235">Expert Finder est un [bot Microsoft Teams](../bots/what-are-bots.md) qui identifie des membres spécifiques de l’organisation en fonction de leurs compétences, de leurs intérêts et de leurs attributs d’éducation.</span><span class="sxs-lookup"><span data-stu-id="cd520-235">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="cd520-236">Les membres trouvent des experts au sein d’une organisation qui correspondent à une recherche par mot clé des profils utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd520-236">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="cd520-237">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-237">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Démonstration des résultats de la recherche du finder expert](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="cd520-239">Forum aux questions</span><span class="sxs-lookup"><span data-stu-id="cd520-239">FAQ Plus</span></span>

<span data-ttu-id="cd520-240">Les réponses aux questions fréquemment posées par les utilisateurs&bots sont un moyen simple de fournir des réponses aux questions fréquemment posées par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cd520-240">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="cd520-241">Toutefois, la plupart des bots ne parviennent pas à interagir avec les utilisateurs de manière significative, car il n’y a aucun humain dans la boucle lorsque le bot échoue.</span><span class="sxs-lookup"><span data-stu-id="cd520-241">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="cd520-242">Le bot FAQ est une question-&un bot qui met un humain dans la boucle lorsqu’il n’est pas en mesure de vous aider.</span><span class="sxs-lookup"><span data-stu-id="cd520-242">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="cd520-243">Vous pouvez poser une question au bot et le bot répond par une réponse s’il est contenu dans la base de connaissances.</span><span class="sxs-lookup"><span data-stu-id="cd520-243">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="cd520-244">Si ce n’est pas le cas, le bot permet à l’utilisateur d’envoyer une requête qui est ensuite publiée à une équipe pré-configurée d’experts qui aident à fournir un support en agissant sur les notifications à partir de l’équipe elle-même.</span><span class="sxs-lookup"><span data-stu-id="cd520-244">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="cd520-245">La dernière version de **FAQ Plus** prend en charge les résolutions&A améliorées en permettant à une équipe d’experts d’effectuer les choses suivantes :</span><span class="sxs-lookup"><span data-stu-id="cd520-245">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="cd520-246">&#x2714; ajoutez de nouvelles Q&directement à la base de connaissances à l’aide des extensions de message.</span><span class="sxs-lookup"><span data-stu-id="cd520-246">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="cd520-247">&#x2714; modifier et supprimer des&paires A ajoutées par un bot.</span><span class="sxs-lookup"><span data-stu-id="cd520-247">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="cd520-248">&#x2714; l’historique des révisions de Q&As.</span><span class="sxs-lookup"><span data-stu-id="cd520-248">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="cd520-249">&#x2714; configurer une réponse avec des détails supplémentaires à afficher en tant que [carte adaptative.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="cd520-249">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="cd520-250">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-250">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ Plus gif](../assets/images/FAQPlusEndUser.gif)

## <a name="goal-tracker"></a><span data-ttu-id="cd520-252">Suivi des objectifs</span><span class="sxs-lookup"><span data-stu-id="cd520-252">Goal Tracker</span></span>

<span data-ttu-id="cd520-253">L’application De suivi des objectifs est une solution complète pour votre organisation qui permet de prendre en charge l’établissement d’objectifs, l’observation de la progression et l’accusé de succès dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-253">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="cd520-254">L’application permet aux utilisateurs de définir, de suivre et de mettre à jour des objectifs au niveau professionnel, personnel et d’équipe.</span><span class="sxs-lookup"><span data-stu-id="cd520-254">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="cd520-255">Les membres de l’équipe reçoivent également des rappels et des mises à jour d’état à temps pour rester concentrés et suivre.</span><span class="sxs-lookup"><span data-stu-id="cd520-255">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="cd520-256">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-256">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![Définir des objectifs](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Afficher les objectifs fixés](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="cd520-259">Bonnes idées</span><span class="sxs-lookup"><span data-stu-id="cd520-259">Great Ideas</span></span>

<span data-ttu-id="cd520-260">L’application Bonnes idées prend en charge et favorise l’innovation et la créativité au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="cd520-260">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="cd520-261">L’application permet à vos employés de partager des idées avec des collègues et des responsables, de découvrir de nouvelles soumissions, de faire la une pour la considération des pairs et de voter pour les meilleures propositions au sein de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-261">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="cd520-262">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-262">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

:::row:::
  :::column span="2":::
    ![Afficher les idées envoyées](../assets/images/great-ideas-all-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Afficher des idées](../assets/images/great-ideas-digest-view.png)
:::column-end:::
:::row-end:::

## <a name="group-activities"></a><span data-ttu-id="cd520-265">Activités de groupe</span><span class="sxs-lookup"><span data-stu-id="cd520-265">Group Activities</span></span>

<span data-ttu-id="cd520-266">Activités de groupe est une application Microsoft Teams qui permet aux propriétaires d’équipes de créer rapidement des groupes d’activités et de gérer les flux de travail de collaboration dans le contexte de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-266">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="cd520-267">Les auteurs d’activités sont activés pour créer des activités, distribuer de manière aléatoire les membres de l’équipe dans des groupes et éventuellement faire envoyer des rappels au bot jusqu’à ce que les activités soient terminées.</span><span class="sxs-lookup"><span data-stu-id="cd520-267">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="cd520-268">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-268">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Liste des activités de groupe dans Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Message de notification d’activité de groupe dans un canal](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a><span data-ttu-id="cd520-271">Développer vos compétences</span><span class="sxs-lookup"><span data-stu-id="cd520-271">Grow Your Skills</span></span>

<span data-ttu-id="cd520-272">L’application Développer vos compétences prend en charge la croissance et le développement professionnels en permettant aux employés de contribuer à des projets supplémentaires pour votre organisation tout en apprendant simultanément de nouvelles compétences.</span><span class="sxs-lookup"><span data-stu-id="cd520-272">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="cd520-273">Les employés peuvent utiliser l’application pour rechercher des opportunités qui répondent à leurs intérêts, profiter d’une collaboration significative avec leurs homologues et acquérir de nouveaux niveaux d’expertise et de fonctionnalités, le tout dans l’environnement Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-273">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="cd520-274">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Affichage des projets disponibles](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Affichage des compétences acquises de la visionneuse](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="cd520-277">Prise en charge RH</span><span class="sxs-lookup"><span data-stu-id="cd520-277">HR Support</span></span>

<span data-ttu-id="cd520-278">Le bot de support rh est une question-&un bot qui apporte un support professionnel/expert de l’équipe RH en boucle lorsqu’il n’est pas en mesure de vous aider.</span><span class="sxs-lookup"><span data-stu-id="cd520-278">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="cd520-279">Vous pouvez poser une question au bot et le bot répond par une réponse s’il est contenu dans la base de connaissances.</span><span class="sxs-lookup"><span data-stu-id="cd520-279">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="cd520-280">Si ce n’est pas le cas, le bot permet à l’utilisateur d’envoyer une requête qui est ensuite publiée dans une équipe pré-configurée d’experts qui aident à fournir un support en agissant sur les notifications à partir de leur équipe elle-même.</span><span class="sxs-lookup"><span data-stu-id="cd520-280">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="cd520-281">En outre, le bot suggère des liens vers des stratégies/questions RH recommandées en recherchant des balises pré-configurées dans la question.</span><span class="sxs-lookup"><span data-stu-id="cd520-281">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="cd520-282">Ces vignettes sont également trouvées dans l’onglet associé en tant que référence rapide.</span><span class="sxs-lookup"><span data-stu-id="cd520-282">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="cd520-283">Le support RH fonctionne bien pour la QnA légère et pour fournir un support rapide lors du lancement de nouveaux projets/initiatives dans l’organisation.</span><span class="sxs-lookup"><span data-stu-id="cd520-283">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="cd520-284">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-284">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Prise en charge RH](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="cd520-286">Brise-glace</span><span class="sxs-lookup"><span data-stu-id="cd520-286">Icebreaker</span></span>

<span data-ttu-id="cd520-287">Icebreaker est un [bot Microsoft Teams](../bots/what-are-bots.md) qui permet à votre équipe de se rapprocher en couplant deux membres d’équipe aléatoires par semaine pour se réunir.</span><span class="sxs-lookup"><span data-stu-id="cd520-287">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="cd520-288">Le bot facilite la planification en suggérant automatiquement des heures libres qui fonctionnent pour les deux membres.</span><span class="sxs-lookup"><span data-stu-id="cd520-288">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="cd520-289">Renforcer les connexions personnelles et créer une communauté étroite avec cette application.</span><span class="sxs-lookup"><span data-stu-id="cd520-289">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="cd520-290">En plus d’encourager les connexions personnelles au sein de l’ensemble de votre équipe, l’application Icebreaker peut contribuer à promouvoir les communautés basées sur l’intérêt au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="cd520-290">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="cd520-291">Par exemple, vous pouvez utiliser cette application pour un groupe d’intérêt DevOps afin d’aider les idées et les meilleures pratiques à se propager de façon organique au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="cd520-291">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="cd520-292">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-292">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Application icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="cd520-294">Primes incitatives</span><span class="sxs-lookup"><span data-stu-id="cd520-294">Incentives</span></span>

<span data-ttu-id="cd520-295">Les primes incitatives sont un [modèle Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) qui gère et suit la participation des employés incentivisés aux activités désignées, telles que les formations et les initiatives de gestion des changements.</span><span class="sxs-lookup"><span data-stu-id="cd520-295">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="cd520-296">Les administrateurs utilisent l’application pour établir des activités désignées, affecter des points pour l’achèvement et spécifier les niveaux de points d’éligibilité requis pour les primes.</span><span class="sxs-lookup"><span data-stu-id="cd520-296">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="cd520-297">Les employés utilisent l’application pour afficher leurs points cumulés et, lorsqu’ils atteignent l’éligibilité, ils demandent et demandent des avantages.</span><span class="sxs-lookup"><span data-stu-id="cd520-297">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="cd520-298">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-298">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Démonstration d’application de primes incitatives](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="cd520-300">Reporter d’incident</span><span class="sxs-lookup"><span data-stu-id="cd520-300">Incident Reporter</span></span>

<span data-ttu-id="cd520-301">Le reporter d’incidents [est un bot Microsoft Teams](../bots/what-are-bots.md)  qui optimise la gestion des incidents dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="cd520-301">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="cd520-302">Le bot facilite la collecte automatisée des données d’incident, les rapports d’incident personnalisés, les notifications des parties prenantes pertinentes et le suivi des incidents de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="cd520-302">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="cd520-303">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-303">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Affichage de l’étendue du groupe de reporter d’incidents](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vue d’étendue personnelle du reporter d’incident](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection-9734"></a><span data-ttu-id="cd520-306">Inspection &#9734;</span><span class="sxs-lookup"><span data-stu-id="cd520-306">Inspection &#9734;</span></span>

 <span data-ttu-id="cd520-307">L’inspection est une application Microsoft Teams qui permet aux employés de première ligne d’inspecter n’importe quoi, des emplacements aux ressources et équipements.</span><span class="sxs-lookup"><span data-stu-id="cd520-307">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="cd520-308">Par exemple, un magasin de vente au détail, une usine de fabrication ou des véhicules et des ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="cd520-308">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="cd520-309">Il existe deux applications dans cette solution, chacune destinée à différents types d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cd520-309">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="cd520-310">L’application permet aux employés de première ligne d’inspecter un bien ou une zone, de gérer la qualité des produits et services ou de maintenir la sécurité sur l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="cd520-310">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="cd520-311">Il facilite la communication entre les membres de l’équipe pour résoudre les problèmes trouvés lors de l’inspection.</span><span class="sxs-lookup"><span data-stu-id="cd520-311">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="cd520-312">L’application fournit des rapports simples aux responsables pour accélérer la résolution des problèmes et mettre en évidence les tendances.</span><span class="sxs-lookup"><span data-stu-id="cd520-312">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="cd520-313">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-313">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Vue d’ensemble de l’inspection](../assets/images/inspection-app.png)  


## <a name="issue-reporting-9734"></a><span data-ttu-id="cd520-315">Issue Reporting &#9734;</span><span class="sxs-lookup"><span data-stu-id="cd520-315">Issue Reporting &#9734;</span></span>

<span data-ttu-id="cd520-316">L’application Rapports de problèmes permet aux employés et aux responsables de lever et de gérer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="cd520-316">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="cd520-317">Il se compose de deux applications, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span><span class="sxs-lookup"><span data-stu-id="cd520-317">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="cd520-318">Les responsables d’équipe utilisent l’application Gérer les problèmes pour configurer l’expérience de l’application, y compris le canal dans lequel les messages Microsoft Teams et les tâches du Planificateur sont créés par l’application.</span><span class="sxs-lookup"><span data-stu-id="cd520-318">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="cd520-319">Les responsables utilisent également l’application pour créer des formulaires de modèle afin de collecter des détails lorsqu’un utilisateur signale un problème.</span><span class="sxs-lookup"><span data-stu-id="cd520-319">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="cd520-320">Par exemple, examinez, modifiez ou supprimez des formulaires de modèle d’émission.</span><span class="sxs-lookup"><span data-stu-id="cd520-320">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="cd520-321">L’application peut également être utilisée pour passer en revue les problèmes de l’équipe, signaler l’historique des problèmes et gérer efficacement la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="cd520-321">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="cd520-322">Les employés utilisent l’application De rapport de problèmes pour enregistrer les problèmes et les détails nécessaires pour les résoudre.</span><span class="sxs-lookup"><span data-stu-id="cd520-322">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="cd520-323">L’application est également utilisée pour modifier et résoudre les problèmes existants et obtenir une vue d’avant-plan des problèmes individuels ou d’équipe.</span><span class="sxs-lookup"><span data-stu-id="cd520-323">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="cd520-324">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-324">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Affichage de l’équipe de rapports de problèmes](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="cd520-326">Intégration de nouveaux employés</span><span class="sxs-lookup"><span data-stu-id="cd520-326">New Employee Onboarding</span></span> 

<span data-ttu-id="cd520-327">L’intégration de nouveaux employés est une solution intégrée d’intégration de Microsoft Teams et de [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) Nouveaux employés qui permet à votre organisation de fournir une expérience d’intégration cohérente et de haute qualité aux employés lors de leur parcours d’embauche.</span><span class="sxs-lookup"><span data-stu-id="cd520-327">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="cd520-328">L’application peut être utilisée par les équipes de ressources humaines et les responsables de l’embauche pour fournir des informations pertinentes tout au long du processus d’orientation et de création, ainsi que par les nouveaux employés pour partager des commentaires, fournir des introductions et effectuer des tâches d’intégration.</span><span class="sxs-lookup"><span data-stu-id="cd520-328">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="cd520-329">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-329">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="cd520-330">**Carte de bienvenue des nouveaux employés** ![ Image de la carte de bienvenue des nouveaux employés](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="cd520-330">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="cd520-331">**Liste de vérification des nouveaux employés** ![ Image de la liste de contrôle des nouveaux employés](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="cd520-331">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="cd520-332">Ouvrir des badges</span><span class="sxs-lookup"><span data-stu-id="cd520-332">Open Badges</span></span>

<span data-ttu-id="cd520-333">Open Badges est une application Microsoft Teams qui permet aux utilisateurs de gagner des badges d’identification d’apprentissage numérique dans le contexte Teams et de les partager partout.</span><span class="sxs-lookup"><span data-stu-id="cd520-333">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="cd520-334">L’utilisation des fonctionnalités de l’autorité d’émission de badge numérique tiers, [Badgr](https://badgr.org/), badges attribués sont enregistrées dans le profil Badgr d’un destinataire et disponibles pour créer et partager une image complète des parcours d’apprentissage de la durée de vie.</span><span class="sxs-lookup"><span data-stu-id="cd520-334">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="cd520-335">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-335">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![Image des badges disponibles](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Affichage des badges attribués](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="cd520-338">Sondage</span><span class="sxs-lookup"><span data-stu-id="cd520-338">Poll</span></span> 

<span data-ttu-id="cd520-339">Poll est une application [d’extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Microsoft Teams personnalisée qui vous permet de créer et d’envoyer rapidement des sondages dans une conversation ou un canal pour recueillir les opinions et les préférences de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="cd520-339">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="cd520-340">L’application est prise en charge sur tous les clients de la plateforme Teams (bureau, navigateur, iOS et Android) et est prête pour le déploiement dans le cadre de votre abonnement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="cd520-340">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="cd520-341">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-341">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Créer un sondage en affichage Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="cd520-343">Réponses rapides</span><span class="sxs-lookup"><span data-stu-id="cd520-343">Quick Responses</span></span>

<span data-ttu-id="cd520-344">Réponses rapides est une application Microsoft Teams qui fournit une solution robuste pour répondre efficacement aux questions fréquemment posées par les utilisateurs (FAQ).</span><span class="sxs-lookup"><span data-stu-id="cd520-344">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="cd520-345">Au lieu de répondre à chaque requête manuellement et en continu, l’application crée une bibliothèque de réponses pour une expérience utilisateur interactive via les [extensions](../messaging-extensions/what-are-messaging-extensions.md)de messagerie Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-345">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="cd520-346">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-346">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Exemple d’affichage des réponses](../assets/images/quick-responses.png)

## <a name="rapid-assist-9734"></a><span data-ttu-id="cd520-348">Aide rapide &#9734;</span><span class="sxs-lookup"><span data-stu-id="cd520-348">Rapid Assist &#9734;</span></span>

<span data-ttu-id="cd520-349">Quick Assist est une application basée sur microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) qui permet aux associés de se connecter rapidement aux experts pour obtenir des réponses rapides, rechercher des informations, suivre des demandes ouvertes et permettre aux experts de recevoir des notifications pour passer rapidement à un appel pour répondre aux questions.</span><span class="sxs-lookup"><span data-stu-id="cd520-349">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="cd520-350">L’application conçue à l’aide de Microsoft [Power Apps](/powerapps/powerapps-overview) et [Power Automate](/power-automate/getting-started), s’intègre en profondeur à Microsoft Teams pour permettre aux organisations de connecter facilement des travailleurs de l’entreprise aux liaisons d’entreprise pour résoudre les requêtes des clients et offrir une expérience client excellente.</span><span class="sxs-lookup"><span data-stu-id="cd520-350">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="cd520-351">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-351">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Interface de demande de l’utilisateur final](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Affichage des demandes d’expert](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="cd520-354">Reflect</span><span class="sxs-lookup"><span data-stu-id="cd520-354">Reflect</span></span> 

<span data-ttu-id="cd520-355">Reflect est une application [d’extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Microsoft Teams personnalisée qui fournit une ressource sûre et inclusive pour que les membres de votre équipe partagent l’état de leur bien-être émotionnel avec leurs collègues et/ou responsables de groupe directement au sein de Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-355">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="cd520-356">L’application est disponible dans les conversations de canal, de groupe, de réunion et 1:1. La réponse d’enregistrement peut être définie sur public, privé à expéditeur ou entièrement anonyme.</span><span class="sxs-lookup"><span data-stu-id="cd520-356">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="cd520-357">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-357">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="cd520-358">**Sondage de bien-être**</span><span class="sxs-lookup"><span data-stu-id="cd520-358">**Well-being poll**</span></span>
    
    ![Refléter le sondage de l’utilisateur de l’application](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="cd520-360">Prise en charge à distance</span><span class="sxs-lookup"><span data-stu-id="cd520-360">Remote Support</span></span>

<span data-ttu-id="cd520-361">Le support à distance est [un bot Microsoft Teams](../bots/what-are-bots.md) qui fournit une interface axée entre les demandeurs de support dans toute votre organisation et l’équipe de support interne.</span><span class="sxs-lookup"><span data-stu-id="cd520-361">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="cd520-362">Les utilisateurs finaux peuvent soumettre, modifier ou retirer des demandes de support, et l’équipe de support peut répondre, gérer et mettre à jour les demandes dans la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-362">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="cd520-363">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-363">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![Formulaire de demande de support](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Demander des détails sur le support](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="cd520-366">Demander une équipe</span><span class="sxs-lookup"><span data-stu-id="cd520-366">Request-a-team</span></span>

<span data-ttu-id="cd520-367">Demander une équipe est une application Microsoft Teams qui optimise la création d’équipes pour votre organisation d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="cd520-367">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="cd520-368">L’application prend en charge la normalisation et les meilleures pratiques lors de la création de nouvelles instances d’équipe par le biais de l’intégration d’un formulaire de demande guidé par l’Assistant, d’un processus d’approbation incorporé, d’un tableau de bord d’état des demandes et de builds d’équipe automatisées.</span><span class="sxs-lookup"><span data-stu-id="cd520-368">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="cd520-369">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Affichage de la page de démarrage demande-à-équipe](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Affichage de la page de l’Assistant Demande-à-équipe](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="cd520-372">Scrums pour les canaux</span><span class="sxs-lookup"><span data-stu-id="cd520-372">Scrums for Channels</span></span>

<span data-ttu-id="cd520-373">Scrums for Channels est une application d’assistant scrum qui permet aux utilisateurs de planifier et d’exécuter des scrums dans les canaux de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-373">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="cd520-374">L’application est excellente pour les équipes distantes et les équipes composées de membres de différents emplacements géographiques et fuseaux horaires pour partager des mises à jour quotidiennes et garantir la participation à des réunions de secours.</span><span class="sxs-lookup"><span data-stu-id="cd520-374">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="cd520-375">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="cd520-376">Pour effectuer des réunions scrum dans une conversation de groupe, consultez notre modèle d’application [Scrums for Group Chat.](#scrums-for-group-chat)</span><span class="sxs-lookup"><span data-stu-id="cd520-376">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![Scrums pour l’affichage des paramètres des canaux](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrums pour l’affichage d’état des membres de l’équipe des canaux](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="cd520-379">Scrums pour la conversation de groupe</span><span class="sxs-lookup"><span data-stu-id="cd520-379">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="cd520-380">Le modèle d’application État de Scrums a été mis à jour et est désormais Scrums pour la conversation de groupe.</span><span class="sxs-lookup"><span data-stu-id="cd520-380">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="cd520-381">Scrums pour la conversation de groupe est un assistant scrum positif qui permet aux membres de conversation de groupe d’exécuter des réunions asynchrones et de partager facilement leurs mises à jour quotidiennes.</span><span class="sxs-lookup"><span data-stu-id="cd520-381">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="cd520-382">Elle permet à tous les membres de la conversation de groupe de contribuer à la scrum et d’afficher les mises à jour réalisées par d’autres personnes dans la scrum en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="cd520-382">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="cd520-383">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-383">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Démonstration Scrums for Group Chat](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="cd520-385">Partager maintenant</span><span class="sxs-lookup"><span data-stu-id="cd520-385">Share Now</span></span> 

<span data-ttu-id="cd520-386">L’application Partager maintenant favorise l’échange positif d’informations entre collègues en permettant à vos utilisateurs de partager facilement du contenu dans l’environnement Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-386">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="cd520-387">Les utilisateurs engagent l’application pour partager des éléments d’intérêt avec les membres de l’équipe, découvrir de nouveaux contenus partagés, définir des préférences et des favoris de signet pour une lecture ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cd520-387">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="cd520-388">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-388">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Sélectionner un affichage de contenu](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="cd520-390">Recherche de liste SharePoint</span><span class="sxs-lookup"><span data-stu-id="cd520-390">SharePoint List Search</span></span>

<span data-ttu-id="cd520-391">La collaboration dans Microsoft Teams fait assez souvent référence aux informations contenues dans les éléments d’une liste SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cd520-391">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="cd520-392">Le simple fait de le cingner un lien vers l’élément en question force tout le monde à basculer le contexte de la conversation, à trouver les informations nécessaires, puis à revenir à Teams pour poursuivre la conversation.</span><span class="sxs-lookup"><span data-stu-id="cd520-392">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="cd520-393">À mesure que la conversation se poursuit, les utilisateurs doivent revenir à l’élément de référence plusieurs fois pour vérifier les nouveaux commentaires et actualiser leurs informations contenues dans l’élément.</span><span class="sxs-lookup"><span data-stu-id="cd520-393">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="cd520-394">Ce basculement de contexte crée un obstacle à la collaboration en douceur et est une recette pour les choses qui tombent entre les fêlures.</span><span class="sxs-lookup"><span data-stu-id="cd520-394">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="cd520-395">Pour vous aider à remédier à cette situation, nous sommes heureux de vous apporter le modèle d’application De recherche de liste.</span><span class="sxs-lookup"><span data-stu-id="cd520-395">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="cd520-396">Des millions d’utilisateurs utilisent SharePoint pour alimenter certains des flux de travail principaux de leur organisation.</span><span class="sxs-lookup"><span data-stu-id="cd520-396">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="cd520-397">Toutefois, la collaboration autour de listes peut être particulièrement fastidieuse.</span><span class="sxs-lookup"><span data-stu-id="cd520-397">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="cd520-398">À l’aide du modèle d’application recherche de liste dans Microsoft Teams, les utilisateurs peuvent insérer des informations à partir d’éléments de liste SharePoint directement dans une conversation pour réduire le basculement de contexte provoqué lors de l’insertion d’un lien dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="cd520-398">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="cd520-399">Les informations sont insérées sous la forme d’une carte mise en forme automatique facile à lire, ce qui permet à vos utilisateurs de rester impliqués dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="cd520-399">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="cd520-400">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-400">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Application de recherche de liste](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="cd520-402">Vérifications du personnel</span><span class="sxs-lookup"><span data-stu-id="cd520-402">Staff Check-ins</span></span>

<span data-ttu-id="cd520-403">Les vérifications du personnel sont une application basée sur [Power Apps](/powerapps/powerapps-overview)qui permet de contrôler la communication entre votre entreprise et le personnel sur le terrain.</span><span class="sxs-lookup"><span data-stu-id="cd520-403">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="cd520-404">Le personnel peut facilement fournir des informations critiques et des mises à jour d’état sur une base programmée ou ad hoc directement à partir de Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-404">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="cd520-405">L’application prend en charge l’emplacement en temps réel, les photos et les notes, ainsi que les notifications de rappel et les flux de travail automatisés.</span><span class="sxs-lookup"><span data-stu-id="cd520-405">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="cd520-406">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-406">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Créer un affichage d’enregistrement](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="cd520-408">Enquête</span><span class="sxs-lookup"><span data-stu-id="cd520-408">Survey</span></span>

<span data-ttu-id="cd520-409">L’enquête est une application [d’extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Microsoft Teams personnalisée qui vous permet de créer une enquête dans une conversation ou un canal pour collecter des données et obtenir des informations actionnables.</span><span class="sxs-lookup"><span data-stu-id="cd520-409">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="cd520-410">L’application est prise en charge sur tous les clients de la plateforme Teams (bureau, navigateur, iOS et Android) et est prête pour le déploiement dans le cadre de votre abonnement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="cd520-410">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="cd520-411">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-411">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Créer une enquête en affichage Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="virtual-rounding-9734"></a><span data-ttu-id="cd520-413">Arrondi virtuel &#9734;</span><span class="sxs-lookup"><span data-stu-id="cd520-413">Virtual Rounding &#9734;</span></span>

<span data-ttu-id="cd520-414">Les fournisseurs d’urgence et d’hôpital font des dizaines et souvent des centaines de « séries » par jour.</span><span class="sxs-lookup"><span data-stu-id="cd520-414">Hospital and emergency room providers make dozens, and often hundreds of “rounds” per day.</span></span> <span data-ttu-id="cd520-415">Ces vérifications rapides sur les patients sont destinées à fournir une vérification de l’état du patient et à s’assurer que ses préoccupations sont traitées.</span><span class="sxs-lookup"><span data-stu-id="cd520-415">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="cd520-416">Bien que l’arrondi soit une pratique essentielle pour s’assurer que les patients sont surveillés par plusieurs types de fournisseurs, ils représentent un drainage considérable de l’PPE, car pour chaque visite, à partir de chaque fournisseur, un nouveau masque et un nouvel ensemble de gants doivent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="cd520-416">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="cd520-417">Grâce à ces modèles d’application, les travailleurs médicaux peuvent facilement mener des séries de cycles virtuellement, par le biais d’une réunion Microsoft Teams entre le fournisseur et le patient.</span><span class="sxs-lookup"><span data-stu-id="cd520-417">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="cd520-418">La solution d’arrondi virtuel est également référencé dans le billet de [blog](https://aka.ms/teamsvirtualrounding)Microsoft Health and Life Sciences .</span><span class="sxs-lookup"><span data-stu-id="cd520-418">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="cd520-419">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-419">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Arrondi virtuel](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="cd520-421">Gestion des visiteurs</span><span class="sxs-lookup"><span data-stu-id="cd520-421">Visitor Management</span></span>

<span data-ttu-id="cd520-422">L’application Gestion des visiteurs permet à votre organisation et à vos employés de gérer facilement et efficacement le processus des visiteurs sur site, directement à partir de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cd520-422">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="cd520-423">L’application permet aux employés de créer des demandes de visiteurs, de suivre de manière centralisée l’état d’une demande via le tableau de bord du visiteur et de recevoir des notifications en temps réel lorsqu’un visiteur arrive.</span><span class="sxs-lookup"><span data-stu-id="cd520-423">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="cd520-424">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-424">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![Créer un affichage de requête](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Notification d’arrivée des visiteurs](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards"></a><span data-ttu-id="cd520-427">Workplace Lieu de travail</span><span class="sxs-lookup"><span data-stu-id="cd520-427">Workplace Awards</span></span>

<span data-ttu-id="cd520-428">Workplace Lieu de travail est un modèle d’application Teams qui fournit une infrastructure positive pour favoriser la reconnaissance et encourager la culture de reconnaissance des employés dans l’espace de travail moderne.</span><span class="sxs-lookup"><span data-stu-id="cd520-428">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="cd520-429">L’application vous permet de configurer et de gérer un programme de reconnaissance et de reconnaissance des employés (R&R) dans lequel les employés peuvent facilement nommer et approuver des collègues, et votre responsable R&R peut afficher les documents soumis, accorder des prix et annoncer des destinataires.</span><span class="sxs-lookup"><span data-stu-id="cd520-429">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="cd520-430">L’obtenir sur GitHub</span><span class="sxs-lookup"><span data-stu-id="cd520-430">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="cd520-431">Carte de poste de travail</span><span class="sxs-lookup"><span data-stu-id="cd520-431">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Onglet liste des listes de classements de l’espace de travail](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="cd520-433">Vous avez une idée pour un modèle d’application que vous souhaitez voir ?</span><span class="sxs-lookup"><span data-stu-id="cd520-433">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="cd520-434">[N’hésitez pas à nous le faire savoir.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)</span><span class="sxs-lookup"><span data-stu-id="cd520-434">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
