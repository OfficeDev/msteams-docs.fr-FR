---
title: Connecteurs Shifts prêts pour la production
description: Découvrez les avantages de l’utilisation des connecteurs Shifts de gestion du personnel pour Teams, tels que le connecteur Kronos-to-Teams Shifts et le connecteur JDA-to-Teams Shifts
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
ms.localizationpriority: high
keywords: Connecteurs Microsoft Teams kronos
ms.author: lajanuar
ms.openlocfilehash: 3a294d20bc2032df7ef5dfa225922e9dccabf1df
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111765"
---
# <a name="production-ready-shifts-connectors"></a>Connecteurs Shifts prêts pour la production  

Les connecteurs de gestion du personnel (WFM) Teams Shifts sont des intégrations prêtes pour la production, open source et basées sur la communauté, utiles pour les travailleurs de première ligne. Ils offrent une expérience transparente et un processus rapide pour la transformation numérique des travailleurs de première ligne avec Teams Shifts.

Chaque connecteur fournit des conseils détaillés pour le déploiement et l’intégration à votre organisation. Le code source complet est disponible dans le référentiel GitHub. Vous pouvez explorer en détail ou dupliquer, et personnaliser pour répondre à vos besoins spécifiques.

Ce document donne une vue d’ensemble des principaux avantages des connecteurs WFM Teams Shifts, du connecteur Kronos-to-Teams Shifts et du connecteur JDA-to-Teams Shifts.

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Principaux avantages des connecteurs WFM Teams Shifts

Voici les principaux avantages des connecteurs WFM Teams Shifts :

* **Expérience Plug-and-Play :** tous les connecteurs WFM Shifts incluent des scripts de déploiement ARM Azure qui vous permettent d’héberger tous les services nécessaires dans Microsoft Azure. Aucun codage n’est requis pour déployer les applications.

* **Code prêt pour la production :** tous les connecteurs Shifts sont conformes aux meilleures pratiques recommandées en matière de sécurité et d’infrastructure, et toutes les modifications soumises par la communauté sont examinées pour garantir la conformité continue.

* **Personnalisable et extensible :** alors que tous les connecteurs WFM Shifts sont prêts à être déployés pour une utilisation immédiate, l’ensemble des scripts de base de code et de déploiement sont facilement disponibles. Vous pouvez facilement les personnaliser ou les étendre pour répondre à vos besoins uniques.

* **Documentation détaillée et prise en charge :** tous les connecteurs WFM Shifts sont accompagnés d’une documentation de bout en bout pour l’architecture de la solution, le déploiement et les étapes de configuration. Les référentiels de connecteurs sont surveillés afin que vous puissiez signaler les problèmes, les défis ou les difficultés que vous rencontrez via le suivi des problèmes du référentiel GitHub.

* **Intégration transparente :** l’intégration entre les solutions WFM et Teams Shifts permet aux employés de première ligne d’utiliser l’application Teams Shifts pour afficher ou gérer leurs planifications et heures de travail. En outre, elle permet d’utiliser toutes les autres fonctionnalités de collaboration enrichies fournies dans Teams directement à partir de leur appareil mobile ou de leur bureau sans avoir à basculer le contexte vers une autre application.  

Ouvrir l’affichage des plannings dans Teams :

L’affichage des plannings dans Teams est illustré dans l’image suivante :

![Ouvrir les plannings dans Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Connecteur Kronos-to-Teams Shifts

Avec le code open source, vous pouvez intégrer Kronos Workforce Central version 8.1 et versions ultérieures, avec Teams Shifts tels que l’application de bureau ou mobile Teams pour les scénarios de travail et de gestion de première ligne suivants :

* Afficher le planification.

* Publier et demander des plannings ouverts.

* Permuter les plannings.

* Demander un congé.

* Proposer des plannings.

Pour plus d’informations sur le déploiement du connecteur Kronos-to-Teams Shifts, consultez [Obtenir sur GitHub](https://aka.ms/KronosShiftsConnector).

## <a name="jda-to-teams-shifts-connector"></a>Connecteur JDA-to-Teams Shifts

Avec le code open source, vous pouvez intégrer JDA, par exemple BlueYonder version 17.2 et versions ultérieures, avec Teams Shifts tels que l’application de bureau ou mobile Teams pour les scénarios de travail et de gestionnaire de première ligne suivants :

* Publier des groupes de plannings et de planification dans JDA et les afficher dans Teams.

* Activer des scénarios de planification enrichis, notamment la demande de permutation de plannings et de congés.

* Définir la disponibilité des utilisateurs à l’aide de [Microsoft API Graph pour Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).

Pour plus d’informations sur la contribution et la suggestion, consultez [Obtenir sur GitHub](https://aka.ms/JDAShiftsConnector).

## <a name="see-also"></a>Voir aussi

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
