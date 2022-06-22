---
title: Intégrer les applications Web
author: Rajeshwari-v
description: Dans cet article, vous allez commencer à intégrer des applications web et des fonctionnalités d’appareil à l’application Microsoft Teams. Plateforme Power pour créer des applications Power, Power Virtual Agents, Virtual Assistant, modèles d’application, connecteurs Shift, Moodle LMS.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 4df1e9ebbcdf23fce9c875384b2918c84fe0edd2
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189775"
---
# <a name="integrate-web-apps"></a>Intégrer les applications Web

Vous pouvez fournir une expérience utilisateur enrichie en intégrant les fonctionnalités d’une application web existante dans la plateforme Microsoft Teams. Veillez à suivre les instructions de conception [Teams](~/concepts/design/understand-use-cases.md) pour rendre votre application native dans Teams.
Ce document fournit une vue d’ensemble des conditions préalables pour intégrer des applications web à Teams, la plateforme Power pour créer des applications Power, Power Virtual Agents, Virtual Assistant, des modèles d’application, des connecteurs Shift, Moodle LMS, la création d’un bouton Partager vers Teams pour votre site web, l’ajout d’un onglet Teams dans SharePoint, la création de liens profonds et l’intégration des fonctionnalités des appareils.

## <a name="prerequisites"></a>Configuration requise

Pour une intégration efficace, veillez à mieux comprendre les conditions préalables suivantes :

* Fonctionnalités de Teams.
* Configuration requise pour SharePoint pour le stockage de fichiers et de données.
* Exigences de l’API.
* Authentification.
* Liaison approfondie de votre application à Teams.
* Mappez les cas d’usage de votre application aux fonctionnalités de la plateforme Teams.
* Déterminez les points d’entrée de votre application, tels que l’utilisation personnelle, la collaboration ou les deux.

## <a name="low-code-platforms"></a>Plateformes à faible code

Les plateformes à faible code offrent une approche intuitive du développement de logiciels et nécessitent peu ou pas de codage pour créer des applications et des processus. Vous pouvez créer facilement des applications personnalisées avec des plateformes à faible code. Ces plateformes se composent d’une interface visuelle, de connecteurs pour back end services et d’un système intégré de gestion du cycle de vie des applications pour générer, déboguer, déployer et gérer des applications. Microsoft fournit les passerelles innovantes suivantes pour créer rapidement des applications compatibles avec Teams à l’aide d’attributs de code faible :

* Plateforme Microsoft Power.
* Modèles d’application Microsoft Teams.

## <a name="microsoft-power-platform"></a>Microsoft Power Platform

La plateforme Microsoft Power combine quatre technologies Microsoft robustes, telles que Power BI, Power Apps, Power Automate et Power Virtual Agents dans une plateforme d’application puissante. Ces technologies vous permettent de créer des solutions, d’automatiser des processus, d’analyser des données et de créer des agents virtuels dans un environnement unifié et intégré.

>[!NOTE]
>Vous ne devez pas utiliser Microsoft Power Platform pour créer des applications destinées à être publiées dans la boutique d'applications Teams. Les applications Microsoft Power Platform peuvent être publiées dans l’App Store d’une organisation uniquement.

### <a name="power-apps"></a>Power Apps

Avec Power Apps, vous pouvez créer des applications métier qui se connectent à vos données métier et sont adaptées aux besoins de votre organisation. Power Apps permet un large éventail de scénarios d'application pour résoudre les défis commerciaux grâce à des applications canevas. Une fois l’application créée, vous pouvez l’exporter à partir du portail Power Apps maker et l’incorporer dans Teams.

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent est une solution d’interface graphique guidée sans code. Il est construit sur la Power Platform de Microsoft et le Bot Framework. Il permet à chaque membre de votre équipe de créer et de gérer des chatbots conversationnels riches qui s’intègrent facilement à la plateforme Teams. Vous pouvez concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement, à créer un service web ou à vous inscrire directement auprès du Bot Framework.

### <a name="create-virtual-assistant"></a>Créer un assistant virtuel

Virtual Assistant est un modèle Microsoft open-source qui vous permet de créer une solution conversationnelle robuste tout en gardant le contrôle total de l'expérience utilisateur, de la marque de l'organisation et des données nécessaires.

## <a name="app-templates"></a>Modèles d’application

Vous pouvez utiliser un modèle d’application pour créer des applications personnalisées en fonction des besoins de votre organisation. Il s’agit d’applications prêtes pour la production pour Microsoft Teams qui sont basées sur la communauté, open source et disponibles sur GitHub. Chaque modèle contient des instructions détaillées pour déployer et installer l’application pour votre organisation. Il fournit une application prête à l’emploi que vous pouvez installer et commencer à utiliser immédiatement.

## <a name="install-moodle-lms"></a>Installer Moodle LMS

Moodle est un système LMS (Learning Management System) open source populaire. Il est désormais intégré à Teams. Cette intégration permet aux enseignants et enseignants de collaborer autour des cours Moodle, de poser des questions sur les notes et les devoirs, et de rester informés des notifications directement dans Teams.

## <a name="create-a-share-to-teams-button-for-your-website"></a>Créer un bouton Partager vers Teams sur votre site web

Les sites web tiers peuvent utiliser le script du lanceur pour incorporer des boutons Partager dans Teams sur leurs pages web. Lorsque vous sélectionnez le bouton, il lance l’expérience Partager vers Teams dans une fenêtre contextuelle. Cela vous permet de partager un lien directement avec une personne ou un canal Microsoft Teams sans changer de contexte.

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>Ajouter un onglet Microsoft Teams dans SharePoint

Vous pouvez bénéficier d’une expérience d’intégration enrichie entre Teams et SharePoint en ajoutant un onglet Teams dans SharePoint en tant que composant WebPart SPFx.

## <a name="create-deep-link"></a>Créer un lien profond

Vous pouvez créer des liens profonds vers les entités dans Teams. Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Ces liens approfondis accèdent au contenu et aux informations de votre onglet. Vous pouvez utiliser des liens profonds pour lier votre application à Teams, car elles relient plusieurs éléments d’une application pour une expérience Teams plus native.

## <a name="integrate-device-capabilities"></a>Intégrer les fonctionnalités de l’appareil

La plateforme Teams améliore en permanence les fonctionnalités de développement en s’alignant sur les expériences internes intégrées. La plateforme Teams améliorée permet aux partenaires d’accéder et d’intégrer les fonctionnalités natives des appareils, telles que l’appareil photo, le QR ou le scanneur de codes-barres, la galerie de photos, le microphone et l’emplacement à l’aide d’API dédiées disponibles dans le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams.

## <a name="integrate-people-picker"></a>Intégrer Sélecteur de personnes

Vous pouvez intégrer le contrôle sélecteur de personnes natives Teams qui permet aux utilisateurs de rechercher et de sélectionner des personnes dans l’expérience d’application web.

## <a name="integrate-teams-in-your-external-app"></a>Intégrer Teams dans votre application externe

Vous pouvez incorporer vos propres expériences dans Teams en créant des applications Teams. Si vous souhaitez *inverse* ce modèle et intégrer Teams ou d’autres fonctionnalités de communication dans votre propre expérience d’application externe, consultez [Azure Communication Services](/azure/communication-services/overview). Azure Communication Services sont des services basés sur le cloud avec des API REST et des kits de développement logiciel (SDK) de bibliothèque de client pour vous aider à intégrer la communication dans vos propres applications personnalisées. Vous pouvez incorporer des composants Web React génériques ou de style Teams pour appeler et discuter à l’aide de la [bibliothèque d’interface utilisateur](https://azure.github.io/communication-ui-library/).

Azure Communication Services applications peuvent utiliser la fonctionnalité de préversion publique pour [interagir avec Teams](/azure/communication-services/concepts/teams-interop) et permettre à votre application personnalisée de rejoindre des réunions Teams de manière anonyme. Par exemple, vous pouvez intégrer les appels vidéo dans une application bancaire mobile et permettre aux utilisateurs finaux de rencontrer virtuellement des employés de banque à l’aide de Teams.

Vous pouvez également intégrer Microsoft 365 identité pour créer des applications externes qui incorporent des appels vidéo et RTC pour le compte d’un utilisateur Teams. Si vous avez utilisé [SDK Skype Entreprise](/skype-sdk/appsdk/skypeappsdk) par le passé, ces fonctionnalités dans le cadre de Azure Communication Services sont recommandées en remplacement.

## <a name="see-also"></a>Voir aussi

* [mappez les cas d’utilisation de votre application aux fonctionnalités de la plateforme Teams](~/concepts/design/map-use-cases.md)
* [Déterminer les points d’entrée de votre application](~/concepts/extensibility-points.md)
* [Considérations relatives à l’intégration de Teams](~/samples/integrating-web-apps.md)
* [créer des applications personnalisées à faible code pour Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Ajouter un chatbot Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [créer des d’assistant virtuel](~/samples/virtual-assistant.md)
* [Modèles d’application pour Microsoft Teams](~/samples/app-templates.md)
* [connecteurs Shift prêts pour la production](~/samples/shifts-wfm-connectors.md)
* [Installer Moodle LMS](~/resources/moodleinstructions.md)
* [Partager vers Teams à partir d’applications web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Ajouter un onglet Teams à SharePoint](~/tabs/how-to/tabs-in-sharepoint.md)
* [Créer des liens plus étroits](~/concepts/build-and-test/deep-links.md)
* [Fonctionnalités de l’appareil](~/concepts/device-capabilities/device-capabilities-overview.md)
* [contrôle sélecteur de personnes](~/concepts/device-capabilities/people-picker-capability.md)
