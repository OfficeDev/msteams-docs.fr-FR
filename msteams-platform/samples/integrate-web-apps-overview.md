---
title: Intégrer les applications Web
author: Rajeshwari-v
description: Vue d’ensemble de l’intégration d’applications web et de fonctionnalités d’appareil à Microsoft Teams application.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: Power Platform Power Apps People picker deep link virtual agent assistant share-to-Teams
ms.openlocfilehash: 8fe6b41f129497d439d9cf5ef391c800d6ddea0e
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685589"
---
# <a name="integrate-web-apps"></a>Intégrer les applications Web

Vous pouvez fournir une expérience utilisateur enrichie en intégrant les fonctionnalités d’une application web existante dans Microsoft Teams plateforme. Veillez à suivre [Teams instructions de conception](~/concepts/design/understand-use-cases.md) pour rendre votre application native à Teams.
Ce document donne une vue d’ensemble des prérequis pour intégrer des applications web à Teams, Power Platform pour créer des applications Power, Power Virtual Agents, Virtual Assistant, des modèles d’application, des connecteurs Shift, Moodle LMS, la création d’un bouton De partage à Teams pour votre site web, l’ajout d’un Microsoft Teams  tabulation dans SharePoint, création de liens profonds et intégration des fonctionnalités de l’appareil.

## <a name="prerequisites"></a>Configuration requise

Pour une intégration efficace, assurez-vous d’avoir une meilleure compréhension des prérequis suivants :

* Teams fonctionnalités.
* SharePoint exigences pour le stockage de fichiers et de données.
* Exigences de l’API.
* Authentification.
* Liaison approfondie de votre application avec Teams.
* Mappez les cas d’utilisation de votre application aux fonctionnalités de plateforme Teams.
* Déterminez les points d’entrée de votre application, tels que l’utilisation personnelle, la collaboration ou les deux.

## <a name="low-code-platforms"></a>Plateformes à faible code

Les plateformes à faible code offrent une approche intuitive du développement de logiciels et nécessitent peu ou pas de codage pour générer des applications et des processus. Vous pouvez créer facilement des applications personnalisées avec des plateformes à faible code. Ces plateformes se composent d’une interface visuelle, de connecteurs pour les services principaux et d’un système de gestion intégré du cycle de vie des applications pour générer, déboguer, déployer et gérer des applications. Microsoft fournit les passerelles innovantes suivantes pour créer rapidement des applications compatibles Teams à l’aide d’attributs de code faible :

* Plateforme Microsoft Power
* modèles d’application Microsoft Teams

## <a name="microsoft-power-platform"></a>Plateforme Microsoft Power

La plateforme Microsoft Power combine quatre technologies Microsoft robustes, telles que Power BI, Power Apps, Power Automate et Power Virtual Agents dans une plateforme d’application puissante. Ces technologies vous permettent de créer des solutions, d’automatiser des processus, d’analyser des données et de créer des agents virtuels dans un environnement unifié et intégré.

>[!NOTE]
>Vous ne devez pas utiliser Microsoft Power Platform pour créer des applications qui doivent être publiées dans l’app store Teams. Les applications Microsoft Power Platform peuvent être publiées dans l’App Store d’une organisation uniquement.

### <a name="power-apps"></a>Power Apps

Avec Power Apps, vous pouvez créer des applications métier qui se connectent à vos données métier et sont adaptées aux besoins de votre organisation. Power Apps permettre à un large éventail de scénarios d’application de résoudre les problèmes métier par le biais d’applications canevas. Après avoir créé l’application, vous pouvez l’exporter à partir du portail Power Apps maker et l’incorporer dans Microsoft Teams.

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent est une solution d’interface graphique guidée sans code. Il repose sur Microsoft Power Platform et Bot Framework. Il permet à chaque membre de votre équipe de créer et de maintenir des chatbots conversationnels riches qui s’intègrent facilement à la plateforme Teams. Vous pouvez concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement, à créer un service web ou à vous inscrire directement auprès de Bot Framework.

### <a name="create-virtual-assistant"></a>Créer un assistant virtuel

Virtual Assistant est un modèle open source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant un contrôle total de l’expérience utilisateur, de la personnalisation organisationnelle et des données nécessaires.

## <a name="app-templates"></a>Modèles d’application

Vous pouvez utiliser un modèle d’application pour créer des applications personnalisées en fonction des besoins de votre organisation. Il s’agit d’applications prêtes pour la production pour les Microsoft Teams qui sont basées sur la communauté, open source et disponibles sur GitHub. Chaque modèle contient des instructions détaillées pour déployer et installer l’application pour votre organisation. Il fournit une application prête à l’emploi que vous pouvez installer et commencer à utiliser immédiatement.

## <a name="teams-shifts-work-force-management-connectors"></a>Teams déplace les connecteurs de gestion de la force de travail

Teams les connecteurs de gestion de la force de travail Shifts sont des intégrations prêtes pour la production, open source et basées sur la communauté. Ils offrent une expérience transparente et un processus rapide pour la transformation numérique des travailleurs de première ligne avec Teams Shifts.

## <a name="install-moodle-lms"></a>Installer Moodle LMS

Moodle est un Learning Management System (LMS) open source populaire. Il est maintenant intégré à Microsoft Teams. Cette intégration permet aux enseignants et aux enseignants de collaborer autour des cours Moodle, de poser des questions sur les notes et les devoirs, et de rester informés des notifications directement dans Teams.

## <a name="create-a-share-to-teams-button-for-your-website"></a>Créer un bouton Partager vers Teams sur votre site web

Les sites web tiers peuvent utiliser le script de lancement pour incorporer Share à Teams boutons sur leurs pages web. Lorsque vous sélectionnez le bouton, il lance le partage pour Teams expérience dans une fenêtre contextuelle. Cela vous permet de partager un lien directement vers n’importe quelle personne ou Microsoft Teams canal sans changer de contexte.

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>Ajouter un onglet Microsoft Teams dans SharePoint

Vous pouvez bénéficier d’une expérience d’intégration enrichie entre Microsoft Teams et SharePoint en ajoutant un onglet Microsoft Teams dans SharePoint en tant que composant WebPart SPFx.

## <a name="create-deep-link"></a>Créer un lien profond

Vous pouvez créer des liens profonds vers les entités dans Teams. Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Ces liens profonds accèdent au contenu et aux informations de votre onglet. Vous pouvez utiliser des liens profonds pour lier votre application à Teams, car elles relient plusieurs éléments d’une application pour une expérience de Teams plus native.

## <a name="integrate-device-capabilities"></a>Intégrer les fonctionnalités de l’appareil

Microsoft Teams plateforme améliore en permanence les fonctionnalités des développeurs en s’alignant sur les expériences internes intégrées. La plateforme Teams améliorée permet aux partenaires d’accéder et d’intégrer les fonctionnalités d’appareil natif, telles que l’appareil photo, QR ou le scanneur de codes-barres, la galerie de photos, le microphone et l’emplacement à l’aide d’API dédiées disponibles dans Microsoft Teams kit de développement logiciel (SDK) client JavaScript.

## <a name="integrate-people-picker"></a>Intégrer Sélecteur de personnes

Vous pouvez intégrer le contrôle de sélecteur de personnes natives Teams qui permet aux utilisateurs de rechercher et de sélectionner des personnes dans l’expérience d’application web.

## <a name="integrate-teams-in-your-external-app"></a>Intégrer Teams dans votre application externe

Vous pouvez incorporer vos propres expériences dans Microsoft Teams en créant Teams applications. Si vous souhaitez *inverser* ce modèle et intégrer Teams ou d’autres fonctionnalités de communication dans votre propre expérience d’application externe, consultez [Azure Communication Services](/azure/communication-services/overview). Azure Communication Services sont des services cloud avec des API REST et des kits de développement logiciel (SDK) de bibliothèque de client pour vous aider à intégrer la communication dans vos propres applications personnalisées. Vous pouvez incorporer des composants Web React génériques ou Teams pour appeler et discuter à l’aide de la bibliothèque d’interface [utilisateur](https://azure.github.io/communication-ui-library/).

Azure Communication Services applications peuvent utiliser la fonctionnalité de préversion publique pour [interagir avec Teams](/azure/communication-services/concepts/teams-interop) et permettre à votre application personnalisée de rejoindre Teams réunions de manière anonyme. Par exemple, vous pouvez intégrer l’appel vidéo dans une application bancaire mobile et autoriser les utilisateurs finaux à rencontrer virtuellement des employés de banque à l’aide de Microsoft Teams.

Vous pouvez également intégrer Microsoft 365 identité pour créer des applications externes qui incorporent des appels vidéo et RTC pour le compte d’un utilisateur Teams. Si vous avez utilisé [Skype Entreprise SDK](/skype-sdk/appsdk/skypeappsdk) par le passé, ces fonctionnalités font partie de Azure Communication Services sont recommandées en guise de remplacement.

## <a name="see-also"></a>Voir aussi

* [Mapper les cas d’usage de votre application aux fonctionnalités de plateforme Teams](~/concepts/design/map-use-cases.md)
* [Déterminer les points d’entrée de votre application](~/concepts/extensibility-points.md)
* [Considérations relatives à l’intégration de Teams](~/samples/integrating-web-apps.md)
* [Créer des applications personnalisées à faible code pour Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Ajouter un chatbot Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [Créer un assistant virtuel](~/samples/virtual-assistant.md)
* [Modèles d’application pour Microsoft Teams](~/samples/app-templates.md)
* [Connecteurs Shift prêts pour la production](~/samples/shifts-wfm-connectors.md)
* [Installer Moodle LMS](~/resources/moodleinstructions.md)
* [Partager vers Teams à partir d’applications web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Ajouter un onglet Teams à SharePoint](~/tabs/how-to/tabs-in-sharepoint.md)
* [Créer des liens plus étroits](~/concepts/build-and-test/deep-links.md)
* [Fonctionnalités de l’appareil](~/concepts/device-capabilities/device-capabilities-overview.md)
* [contrôle sélecteur de personnes](~/concepts/device-capabilities/people-picker-capability.md)
