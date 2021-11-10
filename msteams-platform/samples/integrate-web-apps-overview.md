---
title: Intégrer les applications Web
author: Rajeshwari-v
description: Vue d’ensemble de l’intégration des applications web et des fonctionnalités d’appareil Microsoft Teams application.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: Partage d’assistant d’agent virtuel lien profond avec les applications power platform power apps pour les personnes Teams
ms.openlocfilehash: 54f5345f44c35abbefabba642899a92d515e0aa2
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889215"
---
# <a name="integrate-web-apps"></a>Intégrer les applications Web

Vous pouvez fournir une expérience utilisateur enrichie en intégrant les fonctionnalités d’une application web existante à Microsoft Teams plateforme. Veillez à suivre [Teams de conception](~/concepts/design/understand-use-cases.md) pour rendre votre application native à Teams.
Ce document donne une vue d’ensemble des conditions préalables à l’intégration d’applications web à Teams, à la plateforme Power pour créer des applications Power, des Power Virtual Agents, des Virtual Assistant, des modèles d’application, des connecteurs Shift, Le LMS à LMS, la création d’un bouton Share-to-Teams pour votre site web, l’ajout d’un onglet Microsoft Teams dans SharePoint, la création de liens profonds et l’intégration des fonctionnalités d’appareil.

## <a name="prerequisites"></a>Configuration requise   

Pour une intégration efficace, assurez-vous de mieux comprendre les conditions préalables suivantes :
* Teams fonctionnalités. 
* SharePoint requises pour le stockage de fichiers et de données.
* Conditions requises pour les API.
* Authentification.
* Liaison approfondie de votre application avec Teams.
* Maptez les cas d’utilisation de votre application Teams fonctionnalités de plateforme.
* Déterminez les points d’entrée de votre application, tels que l’utilisation personnelle, la collaboration ou les deux.

## <a name="low-code-platforms"></a>Plateformes de code faible

Les plateformes à code faible offrent une approche intuitive du développement de logiciels et nécessitent peu ou pas de codage pour créer des applications et des processus. Vous pouvez créer facilement des applications personnalisées avec des plateformes à code faible. Ces plateformes se composent d’une interface visuelle, de connecteurs vers des services back end et d’un système de gestion du cycle de vie des applications intégré pour créer, déboguer, déployer et gérer des applications. Microsoft fournit les passerelles innovantes suivantes pour créer rapidement des applications compatibles Teams à l’aide d’attributs de code faible :
* Plateforme Microsoft Power
* Microsoft Teams modèles d’application

## <a name="microsoft-power-platform"></a>Plateforme Microsoft Power

La plateforme Microsoft Power combine quatre technologies Microsoft robustes, telles que Power BI, Power Apps, Power Automate et Power Virtual Agents dans une plateforme d’applications puissante. Ces technologies vous permettent de créer des solutions, d’automatiser des processus, d’analyser des données et de créer des agents virtuels dans un environnement unifié et intégré.

### <a name="power-apps"></a>Power Apps

Avec Power Apps, vous pouvez créer des applications métiers qui se connectent à vos données métiers et qui sont adaptées aux besoins de votre organisation. Power Apps un large éventail de scénarios d’application pour relever les défis de l’entreprise par le biais d’applications de canevas. Après avoir construit l’application, vous pouvez l’exporter à partir du portail Power Apps maker et l’incorporer dans Microsoft Teams.

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent est une solution d’interface graphique guidée sans code. Il repose sur microsoft Power Platform et Bot Framework. Il permet à chaque membre de votre équipe de créer et de gérer des chatbots de conversation enrichis qui s’intègrent facilement à la plateforme Teams de conversation. Vous pouvez concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement, à créer un service web ou à vous inscrire directement à Bot Framework.

### <a name="create-virtual-assistant"></a>Créer un assistant virtuel

Virtual Assistant est un modèle open source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant un contrôle total de l’expérience utilisateur, de la marque organisationnelle et des données nécessaires. 

## <a name="app-templates"></a>Modèles d’application

Vous pouvez utiliser un modèle d’application pour créer des applications personnalisées en fonction des besoins de votre organisation. Ce sont des applications prêtes pour la production Microsoft Teams qui sont pilotées par la communauté, open source et disponibles sur GitHub. Chaque modèle contient des instructions détaillées pour déployer et installer l’application pour votre organisation. Il fournit une application prête à l’emploi que vous pouvez installer et commencer à utiliser immédiatement. 

## <a name="teams-shifts-work-force-management-connectors"></a>Teams Shifts Work Force Management connectors

Teams Les connecteurs de gestion des équipes de travail sont des intégrations prêtes pour la production, open source et communautaires. Ils offrent une expérience transparente et un processus rapide pour la transformation numérique des employés de première ligne avec Teams Shifts.

## <a name="install-moodle-lms"></a>Installer Moodle LMS

Il s’agit d’un système open source Learning Management System (LMS) populaire. Il est désormais intégré à Microsoft Teams. Cette intégration permet aux enseignants et aux enseignants de collaborer autour des cours DeNtact, de poser des questions sur les notes et les devoirs, et de rester à jour avec des notifications directement dans Teams.

## <a name="create-a-share-to-teams-button-for-your-website"></a>Créer un bouton Partager vers Teams sur votre site web

Les sites web tiers peuvent utiliser le script de lancement pour incorporer le partage Teams boutons sur leurs pages web. Lorsque vous sélectionnez le bouton, il lance le partage pour Teams expérience utilisateur dans une fenêtre pop-up. Cela vous permet de partager un lien directement avec n’importe quelle personne Microsoft Teams canal sans changer de contexte.

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>Ajouter un Microsoft Teams dans SharePoint

Vous pouvez obtenir une expérience d’intégration riche entre Microsoft Teams et SharePoint en ajoutant un onglet Microsoft Teams dans SharePoint en tant que SPFx web. 

## <a name="create-deep-link"></a>Créer un lien profond

Vous pouvez créer des liens profonds vers les entités dans Teams. Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Ces liens profonds naviguent vers le contenu et les informations de votre onglet. Vous pouvez utiliser des liens profonds pour lier votre application à Teams car ils relient plusieurs parties d’une application pour une expérience Teams native.

## <a name="integrate-device-capabilities"></a>Intégrer des fonctionnalités d’appareil

Microsoft Teams plateforme améliore en permanence les capacités des développeurs en s’alignant sur les expériences intégrées de la première partie. La plateforme Teams améliorée permet aux partenaires d’accéder et d’intégrer les fonctionnalités natives de l’appareil, telles que l’appareil photo, le scanneur de QR ou de code-barres, la galerie de photos, le microphone et l’emplacement à l’aide d’API dédiées disponibles dans le SDK client JavaScript Microsoft Teams. 

## <a name="integrate-people-picker"></a>Intégrer Sélecteur de personnes

Vous pouvez intégrer le contrôle Teams sélecateur de personnes natives qui permet aux utilisateurs de rechercher et de sélectionner des personnes dans l’expérience d’application web.

## <a name="integrate-teams-in-your-external-app"></a>Intégrer des Teams dans votre application externe
Vous pouvez incorporer vos propres expériences dans Microsoft Teams en Teams applications. Si vous souhaitez  inverser ce modèle et intégrer Teams ou d’autres fonctionnalités de communication dans votre propre expérience d’application externe, voir [Azure Communication Services](/azure/communication-services/overview). Azure Communication Services est un service basé sur le cloud avec des API REST et des SDK de bibliothèque client pour vous aider à intégrer la communication dans vos propres applications personnalisées. Vous pouvez incorporer des composants Web Teams génériques ou de style React pour appeler et discuter à l’aide de la bibliothèque d’interface [utilisateur.](https://azure.github.io/communication-ui-library/)

Les applications Azure Communication Services peuvent utiliser la fonctionnalité de prévisualisation publique pour interopérer avec [Teams](/azure/communication-services/concepts/teams-interop) et permettre à votre application personnalisée de participer Teams réunions de manière anonyme. Par exemple, vous pouvez intégrer des appels vidéo dans une application bancaire mobile et permettre aux utilisateurs finaux de rencontrer virtuellement des employés de la banque à l’aide Microsoft Teams. 

Vous pouvez également intégrer Microsoft 365 pour créer des applications externes qui incorporent la vidéo et les appels PSTN au nom d’Teams utilisateur. Si vous avez utilisé [des SDK Skype Entreprise](/skype-sdk/appsdk/skypeappsdk) par le passé, ces fonctionnalités dans le cadre d’Azure Communication Services sont recommandées en remplacement.

## <a name="see-also"></a>Voir aussi

* [Ma map les cas d’utilisation de votre application Teams fonctionnalités de plateforme](~/concepts/design/map-use-cases.md)
* [Déterminer les points d’entrée de votre application](~/concepts/extensibility-points.md)
* [Intégrer les applications Web](~/samples/integrating-web-apps.md)
* [Créer des applications personnalisées à code faible pour Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Ajouter un chatbot Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [Créer un assistant virtuel](~/samples/virtual-assistant.md)
* [Modèles d’application pour Microsoft Teams](~/samples/app-templates.md)
* [Connecteurs Shift prêts pour la production](~/samples/shifts-wfm-connectors.md)
* [Installer Moodle LMS](~/resources/moodleinstructions.md)
* [Créer un bouton de partage Teams](~/concepts/build-and-test/share-to-teams.md)
* [Ajouter un onglet Teams à SharePoint](~/tabs/how-to/tabs-in-sharepoint.md)
* [Créer des liens plus étroits](~/concepts/build-and-test/deep-links.md)
* [Fonctionnalités de l’appareil](~/concepts/device-capabilities/device-capabilities-overview.md)
* [contrôle du s picker de personnes](~/concepts/device-capabilities/people-picker-capability.md)
