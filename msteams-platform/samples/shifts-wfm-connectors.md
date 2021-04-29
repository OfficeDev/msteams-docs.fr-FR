---
title: Connecteurs Shifts prêts pour la production
description: Connecteurs shifts de gestion du personnel pour Teams
ms.topic: reference
author: laujan
ms.date: 03/09/2020
localization_priority: Normal
keywords: Connecteurs Microsoft Teams kronos
ms.author: lajanuar
ms.openlocfilehash: 459797dd3f8425223c0dcbedc335955bf106ae37
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075737"
---
# <a name="production-ready-shifts-connectors"></a><span data-ttu-id="bec6b-104">Connecteurs Shifts prêts pour la production</span><span class="sxs-lookup"><span data-stu-id="bec6b-104">Production-ready Shifts Connectors</span></span>  

<span data-ttu-id="bec6b-105">Les connecteurs WFM (Teams Shifts Workforce Management) sont des intégrations prêtes pour la production, open source et communautaires, utiles pour les employés de première ligne.</span><span class="sxs-lookup"><span data-stu-id="bec6b-105">Teams Shifts Workforce management (WFM) connectors are production-ready, open-source, and community-driven integrations, useful for firstline workers.</span></span> <span data-ttu-id="bec6b-106">Ils offrent une expérience transparente et un processus rapide pour la transformation numérique des employés de première ligne avec Teams Shifts.</span><span class="sxs-lookup"><span data-stu-id="bec6b-106">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="bec6b-107">Chaque connecteur fournit des instructions détaillées pour le déploiement et l'intégration à votre organisation.</span><span class="sxs-lookup"><span data-stu-id="bec6b-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="bec6b-108">Le code source complet est disponible dans le référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="bec6b-108">The complete source code is available in GitHub repository.</span></span> <span data-ttu-id="bec6b-109">Vous pouvez explorer en détail ou bifurcation et personnaliser pour répondre à vos besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="bec6b-109">You can explore in detail or fork, and customize to meet your specific needs.</span></span>   

<span data-ttu-id="bec6b-110">Ce document offre une vue d'ensemble des principaux avantages des connecteurs WFM Teams Shifts, de Kronos-to-Teams Shifts et du connecteur JDA vers Teams Shifts.</span><span class="sxs-lookup"><span data-stu-id="bec6b-110">This document gives an overview of key benefits of Teams Shifts WFM connectors, Kronos-to-Teams Shifts connector, and JDA-to-Teams Shifts connector.</span></span>

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a><span data-ttu-id="bec6b-111">Principaux avantages des connecteurs WFM Teams Shifts</span><span class="sxs-lookup"><span data-stu-id="bec6b-111">Key benefits of Teams Shifts WFM connectors</span></span>

<span data-ttu-id="bec6b-112">Voici les principaux avantages des connecteurs WFM Teams Shifts :</span><span class="sxs-lookup"><span data-stu-id="bec6b-112">Following are the key benefits of Teams Shifts WFM connectors:</span></span>

* <span data-ttu-id="bec6b-113">**Expérience de plug-and-play :** Tous les connecteurs WFM Shifts incluent ARM scripts de déploiement Azure qui vous permettent d'héberger tous les services nécessaires dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bec6b-113">**Plug and play experience:** All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="bec6b-114">Aucun codage n'est requis pour déployer les applications.</span><span class="sxs-lookup"><span data-stu-id="bec6b-114">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="bec6b-115">**Code prêt pour la production :** Tous les connecteurs Shifts sont conformes aux meilleures pratiques recommandées en matière de sécurité et d'infrastructure, et toutes les modifications envoyées par la communauté sont examinées pour garantir une conformité continue.</span><span class="sxs-lookup"><span data-stu-id="bec6b-115">**Production-ready code:** All  Shifts connectors conform to the recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="bec6b-116">**Personnalisables et extensibles :**   Alors que tous les connecteurs WFM Shifts sont prêts à être déployés pour une utilisation immédiate, avec l'ensemble de la base de code et des scripts de déploiement facilement disponibles.</span><span class="sxs-lookup"><span data-stu-id="bec6b-116">**Customizable and extensible:**  While all Shifts WFM connectors are ready to deploy for immediate use, with the entire code base and deployment scripts readily available.</span></span> <span data-ttu-id="bec6b-117">Vous pouvez facilement les personnaliser ou les étendre pour répondre à vos besoins uniques.</span><span class="sxs-lookup"><span data-stu-id="bec6b-117">You can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="bec6b-118">**Documentation détaillée & prise en charge :**   Tous les connecteurs WFM Shifts sont accompagnés d'une documentation de bout en bout pour les étapes d'architecture, de déploiement et de configuration de la solution.</span><span class="sxs-lookup"><span data-stu-id="bec6b-118">**Detailed documentation & support:**  All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="bec6b-119">Les référentiels de connecteurs sont surveillés, afin que vous pouvez signaler les problèmes, défis ou difficultés que vous rencontrez via le suivi des problèmes GitHub du référentiel.</span><span class="sxs-lookup"><span data-stu-id="bec6b-119">The connector repositories are monitored, so that you can report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="bec6b-120">**Intégration transparente :** L'intégration entre les solutions WFM et teams Shifts permet aux employés de première ligne d'utiliser l'application Teams Shifts pour afficher ou gérer leurs plannings et les heures d'équipe, et d'utiliser toutes les autres fonctionnalités de collaboration enrichies fournies dans Teams directement à partir de leur appareil mobile ou de leur bureau sans avoir à basculer le contexte vers une autre application.</span><span class="sxs-lookup"><span data-stu-id="bec6b-120">**Seamless integration:** The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view or manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>  

<span data-ttu-id="bec6b-121">**Affichage Des équipes ouvertes dans Teams**</span><span class="sxs-lookup"><span data-stu-id="bec6b-121">**Open shifts view in Teams**</span></span> 

<span data-ttu-id="bec6b-122">L'affichage shifts dans Teams est illustré dans l'image suivante :</span><span class="sxs-lookup"><span data-stu-id="bec6b-122">The shifts view in Teams is shown in the following image:</span></span> 

![Équipes ouvertes dans Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="bec6b-124">Connecteur Kronos-Teams Shifts</span><span class="sxs-lookup"><span data-stu-id="bec6b-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="bec6b-125">Avec du code open source, vous pouvez intégrer Kronos Workforce Central Version 8.1 et versions supérieures, avec des équipes teams telles que, application de bureau ou mobile Teams pour les scénarios de travail et de responsable de première ligne suivants :</span><span class="sxs-lookup"><span data-stu-id="bec6b-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="bec6b-126">Afficher la planification.</span><span class="sxs-lookup"><span data-stu-id="bec6b-126">View schedule.</span></span>

* <span data-ttu-id="bec6b-127">Publier et demander des équipes d'ouverture.</span><span class="sxs-lookup"><span data-stu-id="bec6b-127">Publish and request open shifts.</span></span>

* <span data-ttu-id="bec6b-128">Permutation.</span><span class="sxs-lookup"><span data-stu-id="bec6b-128">Swap shifts.</span></span>

* <span data-ttu-id="bec6b-129">Demander des congés.</span><span class="sxs-lookup"><span data-stu-id="bec6b-129">Request time off.</span></span>

* <span data-ttu-id="bec6b-130">Changements d'offre.</span><span class="sxs-lookup"><span data-stu-id="bec6b-130">Offer shifts.</span></span>

<span data-ttu-id="bec6b-131">Pour plus d'informations sur le déploiement du connecteur Kronos-to-Teams Shifts, voir Obtenir sur [GitHub.](https://aka.ms/KronosShiftsConnector)</span><span class="sxs-lookup"><span data-stu-id="bec6b-131">For more information on deployment of Kronos-to-Teams Shifts connector, see [Get it on GitHub](https://aka.ms/KronosShiftsConnector).</span></span>

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="bec6b-132">Connecteur Shifts JDA-Teams</span><span class="sxs-lookup"><span data-stu-id="bec6b-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="bec6b-133">Avec le code open source, vous pouvez intégrer JDA, tel que BlueYonder Version 17.2 et versions supérieures, avec teams Shifts tels que, application de bureau ou mobile Teams pour les scénarios de travail et de responsable de première ligne suivants :</span><span class="sxs-lookup"><span data-stu-id="bec6b-133">With open-source code, you can integrate JDA, such as BlueYonder Version 17.2 and above, with Teams Shifts  such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="bec6b-134">Publiez des équipes et des groupes de planification dans JDA et affichez-les dans Teams.</span><span class="sxs-lookup"><span data-stu-id="bec6b-134">Publish shifts and schedule groups in JDA and view them in Teams.</span></span>

* <span data-ttu-id="bec6b-135">Activez des scénarios de planification enrichis, y compris la demande de permutations d'équipe et de congés.</span><span class="sxs-lookup"><span data-stu-id="bec6b-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

* <span data-ttu-id="bec6b-136">Définir la disponibilité des utilisateurs à [l'aide de l'API Microsoft Graph pour Shifts.](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="bec6b-136">Set user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).</span></span>

<span data-ttu-id="bec6b-137">Pour plus d'informations sur la contribution et la suggestion, voir [Obtenir sur GitHub.](https://aka.ms/JDAShiftsConnector)</span><span class="sxs-lookup"><span data-stu-id="bec6b-137">For more information on contribution and suggestion, see [Get it on GitHub](https://aka.ms/JDAShiftsConnector).</span></span></br></br>

## <a name="see-also"></a><span data-ttu-id="bec6b-138">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="bec6b-138">See also</span></span>

[<span data-ttu-id="bec6b-139">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="bec6b-139">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
