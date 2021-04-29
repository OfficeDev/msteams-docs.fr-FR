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
# <a name="production-ready-shifts-connectors"></a>Connecteurs Shifts prêts pour la production  

Les connecteurs WFM (Teams Shifts Workforce Management) sont des intégrations prêtes pour la production, open source et communautaires, utiles pour les employés de première ligne. Ils offrent une expérience transparente et un processus rapide pour la transformation numérique des employés de première ligne avec Teams Shifts. 

Chaque connecteur fournit des instructions détaillées pour le déploiement et l'intégration à votre organisation. Le code source complet est disponible dans le référentiel GitHub. Vous pouvez explorer en détail ou bifurcation et personnaliser pour répondre à vos besoins spécifiques.   

Ce document offre une vue d'ensemble des principaux avantages des connecteurs WFM Teams Shifts, de Kronos-to-Teams Shifts et du connecteur JDA vers Teams Shifts.

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Principaux avantages des connecteurs WFM Teams Shifts

Voici les principaux avantages des connecteurs WFM Teams Shifts :

* **Expérience de plug-and-play :** Tous les connecteurs WFM Shifts incluent ARM scripts de déploiement Azure qui vous permettent d'héberger tous les services nécessaires dans Microsoft Azure. Aucun codage n'est requis pour déployer les applications.

* **Code prêt pour la production :** Tous les connecteurs Shifts sont conformes aux meilleures pratiques recommandées en matière de sécurité et d'infrastructure, et toutes les modifications envoyées par la communauté sont examinées pour garantir une conformité continue.

* **Personnalisables et extensibles :**   Alors que tous les connecteurs WFM Shifts sont prêts à être déployés pour une utilisation immédiate, avec l'ensemble de la base de code et des scripts de déploiement facilement disponibles. Vous pouvez facilement les personnaliser ou les étendre pour répondre à vos besoins uniques.

* **Documentation détaillée & prise en charge :**   Tous les connecteurs WFM Shifts sont accompagnés d'une documentation de bout en bout pour les étapes d'architecture, de déploiement et de configuration de la solution. Les référentiels de connecteurs sont surveillés, afin que vous pouvez signaler les problèmes, défis ou difficultés que vous rencontrez via le suivi des problèmes GitHub du référentiel.

* **Intégration transparente :** L'intégration entre les solutions WFM et teams Shifts permet aux employés de première ligne d'utiliser l'application Teams Shifts pour afficher ou gérer leurs plannings et les heures d'équipe, et d'utiliser toutes les autres fonctionnalités de collaboration enrichies fournies dans Teams directement à partir de leur appareil mobile ou de leur bureau sans avoir à basculer le contexte vers une autre application.  

**Affichage Des équipes ouvertes dans Teams** 

L'affichage shifts dans Teams est illustré dans l'image suivante : 

![Équipes ouvertes dans Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Connecteur Kronos-Teams Shifts

Avec du code open source, vous pouvez intégrer Kronos Workforce Central Version 8.1 et versions supérieures, avec des équipes teams telles que, application de bureau ou mobile Teams pour les scénarios de travail et de responsable de première ligne suivants :

* Afficher la planification.

* Publier et demander des équipes d'ouverture.

* Permutation.

* Demander des congés.

* Changements d'offre.

Pour plus d'informations sur le déploiement du connecteur Kronos-to-Teams Shifts, voir Obtenir sur [GitHub.](https://aka.ms/KronosShiftsConnector)

## <a name="jda-to-teams-shifts-connector"></a>Connecteur Shifts JDA-Teams

Avec le code open source, vous pouvez intégrer JDA, tel que BlueYonder Version 17.2 et versions supérieures, avec teams Shifts tels que, application de bureau ou mobile Teams pour les scénarios de travail et de responsable de première ligne suivants :

* Publiez des équipes et des groupes de planification dans JDA et affichez-les dans Teams.

* Activez des scénarios de planification enrichis, y compris la demande de permutations d'équipe et de congés.

* Définir la disponibilité des utilisateurs à [l'aide de l'API Microsoft Graph pour Shifts.](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)

Pour plus d'informations sur la contribution et la suggestion, voir [Obtenir sur GitHub.](https://aka.ms/JDAShiftsConnector)</br></br>

## <a name="see-also"></a>Voir aussi

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
