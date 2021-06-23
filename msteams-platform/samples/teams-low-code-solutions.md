---
title: Créer des applications personnalisées à code faible pour Microsoft Teams
author: surbhigupta
description: Détaille les solutions Microsoft à faible et sans code disponibles pour Teams
localization_priority: Normal
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3c7f2dc76f01a47226598e5480e9b39ce9dd173a
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069128"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>Créer des applications personnalisées à code faible pour Microsoft Teams

Microsoft Teams est extensible et adaptatif. Cela signifie que vous pouvez créer des applications personnalisées pour Teams qui répondent aux besoins distincts de vos utilisateurs. Les applications personnalisées à code faible gagnent du temps, fournissent des solutions rapides et répondent à la demande que les applications créées à partir de zéro. Ce document donne une vue d’ensemble de Microsoft Power Platform, Power Virtual Agents chatbot et Virtual Assistant.

Les plateformes à code faible offrent une approche intuitive du développement de logiciels avec un codage minimal ou aucun codage pour créer des applications et des processus. Ils permettent aux développeurs sans expérience de créer facilement des applications personnalisées avec peu ou pas de codage, et aux développeurs professionnels de développer et déployer rapidement l’application. Ces plateformes se composent d’une interface visuelle, de connecteurs vers des services back-end et d’un système de gestion du cycle de vie des applications intégré pour créer, déboguer, déployer et gérer des applications. Microsoft Power Platform est la passerelle innovantes pour créer rapidement Teams applications compatibles à l’aide d’attributs de code faible.

## <a name="teams-and-microsoft-power-platform"></a>Teams et Microsoft Power Platform

Microsoft Power Platform combine quatre technologies Microsoft robustes, telles que Power BI, Power Apps, Power Automate, anciennement Microsoft Flow et Power Virtual Agents dans une plateforme d’applications puissante. Ces technologies vous permettent de créer des solutions, d’automatiser des processus, d’analyser des données et de créer des agents virtuels dans un environnement unifié et intégré :

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Services de plateforme d’alimentation":::

> [!NOTE]
> Vous ne devez pas utiliser Microsoft Power Platform pour créer des applications qui doivent être publiées dans Teams app store. Les applications Microsoft Power Platform peuvent être publiées dans le magasin d’applications d’une organisation uniquement.

### <a name="-teams-and-power-bi"></a>✔ Teams et Power BI

[L’onglet Power BI](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/) pour Microsoft Teams ajoute la prise en charge des rapports dans l’espace de travail Teams et permet aux utilisateurs de partager du contenu [Power BI interactif](/power-bi/collaborate-share/service-embed-report-microsoft-teams) et de collaborer avec d’autres personnes dans des canaux Teams et [des](/power-bi/collaborate-share/service-collaborate-microsoft-teams) conversations. Vous pouvez créer du contenu [Power BI d’application](/power-bi/collaborate-share/service-create-distribute-apps) empaqueté à partir de zéro et le distribuer en tant qu’application ou créer un modèle d’application [dans Power BI](/power-bi/connect-data/service-template-apps-create). En outre, utilisez la nouvelle application [Power BI dans Teams](https://go.microsoft.com/fwlink/?linkid=2143643) pour apporter toute votre expérience de service Power BI de base Teams.

### <a name="-teams-and-power-apps"></a>✔ Teams et Power Apps

Avec [Power Apps,](/powerapps/powerapps-overview)vous pouvez créer des applications métiers qui se connectent à vos données métiers et qui sont adaptées aux besoins de votre organisation.  Power Apps un large éventail de scénarios d’application pour relever les défis de l’entreprise par le biais [d’applications de canevas.](/powerapps/maker/#canvas-apps) Après la création, vous pouvez exporter l’application à partir du portail Power Apps maker et [l’incorporer dans Microsoft Teams](/power-platform/admin/embed-app-teams).

La nouvelle [application Power Apps dans](https://go.microsoft.com/fwlink/?linkid=2143374) Teams offre une expérience intégrée aux créateurs d’applications pour créer et modifier des applications et des flux de travail au sein Teams. Ils peuvent rapidement publier et partager les applications avec les membres de l’équipe. Les membres peuvent utiliser les applications sans avoir à basculer entre plusieurs applications et services.

### <a name="-teams-and-power-automate"></a>✔ Teams et Power Automate

Vous pouvez [créer des flux pour automatiser](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) des tâches de travail répétitives directement dans l’environnement Teams avec l’application Power Automate dans [Teams](/power-automate/flows-teams). Vous pouvez [déclencher un flux à partir de n’importe](/power-automate/trigger-flow-teams-message) quel message Microsoft Teams et utiliser des cartes [adaptatives dans Power Automate](/power-automate/create-adaptive-cards). En outre, vous pouvez créer des flux pour personnaliser et ajouter une valeur supplémentaire à Microsoft Teams à partir de la nouvelle application Power Apps [dans](https://go.microsoft.com/fwlink/?linkid=2143539) Teams.

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams et Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) est une solution d’interface graphique sans code, guidée, qui repose sur microsoft Power Platform et Bot Framework. Il permet à chaque membre de votre équipe de créer et de gérer des chatbots riches et conversationnels qui s’intègrent facilement à la plateforme Teams web. Tout le contenu rédigé dans Power Virtual Agents est rendu naturellement dans Teams et les robots Power Virtual Agents dialoguent avec les utilisateurs dans Teams zone de conversation native. Vous pouvez [intégrer votre chatbot Power Virtual Agents pour](/power-virtual-agents/publication-add-bot-to-microsoft-teams) Teams via le portail [Power Virtual Agents.](https://powervirtualagents.microsoft.com)

Utilisez la nouvelle [application Power Virtual Agents dans](https://aka.ms/pva-teams-docs) Teams, pour créer, gérer et publier facilement des chatbots de conversation à partir de Teams. Vous pouvez partager vos bots avec d’autres personnes de votre organisation pour discuter et obtenir des réponses à leurs questions.

### <a name="-virtual-assistant-for-teams"></a>✔ Virtual Assistant pour Teams

Virtual Assistant est un modèle open source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant un contrôle total de l’expérience utilisateur, de la marque organisationnelle et des données nécessaires. Vous pouvez configurer votre assistant virtuel pour [l’intégration dans l’environnement Teams.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro) 

### <a name="-power-platform-learn-modules"></a>✔ modules Power Platform Learn

|  Rubrique  |  Liens  |
|:---------|:----------------------|
|Power BI|[Power BI pour les créateurs d’applications](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[Power BI pour les développeurs](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[Power Apps pour les créateurs d’applications](/learn/browse/?products=power-apps&roles=maker)</br>[Power Apps pour les développeurs](/learn/browse/?products=power-apps)|
|Power Automate|[Power Automate pour les créateurs d’applications](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[Power Automate pour les développeurs](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[Power Virtual Agents développeurs et développeurs d’applications](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Project Derdale (prévisualisation)

> [!NOTE]
> Project **Sont** renommés projet **Dataverse pour Teams**.

[Project Sont une](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) nouvelle plateforme de données à code faible bientôt disponible Microsoft Teams. Il permet aux développeurs de créer des solutions power platform Teams directement dans Teams. Pour plus d’informations sur Project, voir Teams [Blog Microsoft Project Raisons.](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)

### <a name="-microsoft-blog-insights"></a>✔ de blog Microsoft

[Un examen plus étroit des fonctionnalités de plateforme de données Project Androiddale](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[Annonce des mises à jour Teams et power platform pour aider les clients à s’adapter au travail à distance](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams forme l’avenir du travail avec des fonctionnalités de code faible pour améliorer votre espace de travail numérique](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ gestion des applications power platform

> [!div class="nextstepaction"]
> [Gérer les applications Microsoft Power Platform dans le Centre d Microsoft Teams’administration Microsoft Power Platform](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>Voir aussi

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
