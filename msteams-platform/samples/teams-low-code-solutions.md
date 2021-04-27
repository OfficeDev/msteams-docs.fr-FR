---
title: Créer des applications personnalisées à code faible pour Microsoft Teams
author: laujan
description: Détailler les solutions Microsoft faibles et sans solutions de code disponibles pour Teams
localization_priority: Normal
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: c3fa4fb1792579a344596cbb080d96015292f7c4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020414"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>Créer des applications personnalisées à code faible pour Microsoft Teams

Microsoft Teams est extensible et adaptatif. Cela signifie que vous pouvez créer des applications personnalisées pour Teams qui répondent aux besoins distincts de vos utilisateurs. Les applications personnalisées à code faible gagnent du temps, fournissent des solutions rapides et répondent à la demande que les applications créées à partir de zéro. Ce document donne une vue d'ensemble de Microsoft Power Platform, des agents power virtual chatbot et de l'Assistant virtuel.

Les plateformes à code faible offrent une approche intuitive du développement de logiciels et nécessitent peu ou pas de codage pour créer des applications et des processus. Ils permettent aux développeurs sans expérience de créer facilement des applications personnalisées avec peu ou pas de codage, et aux développeurs professionnels de développer et déployer rapidement l'application. Ces plateformes se composent d'une interface visuelle, de connecteurs vers des services back-end et d'un système de gestion du cycle de vie des applications intégré pour créer, déboguer, déployer et gérer des applications. Microsoft Power Platform est la passerelle innovantes pour créer rapidement des applications compatibles avec Teams à l'aide d'attributs de code faible.

## <a name="teams-and-microsoft-power-platform"></a>Teams et Microsoft Power Platform

Microsoft Power Platform combine quatre technologies Microsoft robustes, telles que Power BI, Power Apps, Power Automate, anciennement Microsoft Flow et Power Virtual Agents dans une plateforme d'application puissante. Ces technologies vous permettent de créer des solutions, d'automatiser des processus, d'analyser des données et de créer des agents virtuels dans un environnement unifié et intégré :

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Services de plateforme d'alimentation":::

> [!NOTE]
> Vous ne devez pas utiliser Microsoft Power Platform pour créer des applications qui doivent être publiées dans le magasin d'applications Teams. Les applications Microsoft Power Platform peuvent être publiées dans le magasin d'applications d'une organisation uniquement.

### <a name="-teams-and-power-bi"></a>✔ Teams et Power BI

[L'onglet Power BI](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/) pour Microsoft Teams ajoute la prise en charge des rapports dans l'espace de travail Teams et permet aux utilisateurs de partager du contenu Power BI [interactif](/power-bi/collaborate-share/service-embed-report-microsoft-teams) et de collaborer avec d'autres personnes dans les canaux et conversations [Teams.](/power-bi/collaborate-share/service-collaborate-microsoft-teams) Vous pouvez créer du contenu [d'application Power BI](/power-bi/collaborate-share/service-create-distribute-apps) empaqueté à partir de zéro et le distribuer en tant qu'application ou créer une application de modèle dans Power [BI](/connect-data/service-template-apps-create). En outre, utilisez la nouvelle [application Power BI dans Teams](https://go.microsoft.com/fwlink/?linkid=2143643) pour apporter toute votre expérience de service Power BI de base dans Teams.

### <a name="-teams-and-power-apps"></a>✔ Teams et Power Apps

Avec [Power Apps,](/powerapps/powerapps-overview)vous pouvez créer des applications d'entreprise qui se connectent à vos données métiers et sont adaptées aux besoins de votre organisation.  Power Apps permet de mettre en place un large éventail de scénarios d'application pour relever les défis de l'entreprise par le biais [d'applications de canevas.](/powerapps/maker/#canvas-apps) Après la création, vous pouvez exporter l'application à partir du portail Power Apps maker et [l'incorporer dans Microsoft Teams.](/power-platform/admin/embed-app-teams)

La nouvelle [application Power Apps dans](https://go.microsoft.com/fwlink/?linkid=2143374) Teams offre une expérience intégrée aux créateurs d'applications pour créer et modifier des applications et des flux de travail dans Teams. Ils peuvent rapidement publier et partager les applications avec les membres de l'équipe. Les membres peuvent utiliser les applications sans avoir à basculer entre plusieurs applications et services.

### <a name="-teams-and-power-automate"></a>✔ Teams et Power Automate

Vous pouvez [créer des flux pour automatiser des](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) tâches de travail répétitives directement dans l'environnement Teams avec l'application Power [Automate dans Teams.](/power-automate/flows-teams) Vous pouvez [déclencher un flux à partir de n'importe quel message dans Microsoft Teams](/power-automate/trigger-flow-teams-message) et utiliser des cartes [adaptatives dans Power Automate.](/power-automate/create-adaptive-cards) En outre, vous pouvez créer des flux pour personnaliser et ajouter une valeur ajoutée à Microsoft Teams à partir de la nouvelle [application Power Apps](https://go.microsoft.com/fwlink/?linkid=2143539) dans Teams.

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams et les agents power virtual

[Power Virtual Agents est](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) une solution d'interface graphique guidée sans code, qui repose sur microsoft Power Platform et Bot Framework. Il permet à chaque membre de votre équipe de créer et de maintenir des chatbots de conversation riches et conversationnels qui s'intègrent facilement à la plateforme Teams. Tout le contenu rédigé dans Les agents power virtual s'restituera naturellement dans les bots Teams et Les agents virtuels Power impliquent des utilisateurs dans le canevas de conversation native Teams. Vous pouvez [intégrer votre chatbot d'agents virtuels Power](/power-virtual-agents/publication-add-bot-to-microsoft-teams) à Teams via le portail Power Virtual [Agents](https://powervirtualagents.microsoft.com).

Utilisez la nouvelle [application Power Virtual Agents](https://aka.ms/pva-teams-docs) dans Teams pour créer, gérer et publier facilement des chatbots de conversation à partir de Teams. Vous pouvez partager vos bots avec d'autres personnes de votre organisation pour discuter et obtenir des réponses à leurs questions.

### <a name="-virtual-assistant-for-teams"></a>✔ Virtual Assistant pour Teams

Assistant virtuel est un modèle open source Microsoft qui vous permet de créer une solution conversationnelle robuste tout en conservant un contrôle total de l'expérience utilisateur, de la marque organisationnelle et des données nécessaires. Vous pouvez configurer votre assistant virtuel pour [l'intégration dans l'environnement Teams.](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro) 

### <a name="-power-platform-learn-modules"></a>✔ modules Power Platform Learn

|  Rubrique  |  Liens  |
|:---------|:----------------------|
|Power BI|[Power BI pour les créateurs d'applications](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[Power BI pour les développeurs](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[Power Apps pour les créateurs d'applications](/learn/browse/?products=power-apps&roles=maker)</br>[Power Apps pour les développeurs](/learn/browse/?products=power-apps)|
|Power Automate|[Power Automate pour les créateurs d'applications](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[Power Automate pour les développeurs](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[Agents Power Virtual pour les développeurs et les créateurs d'applications](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ ProjectDale (prévisualisation)

> [!NOTE]
> **ProjectDaldale est** renommé projet **Dataverse pour Teams.**

[ProjectDaldale est](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) une nouvelle plateforme de données à code faible bientôt disponible dans Microsoft Teams. Il permet aux développeurs de créer des solutions Power Platform Teams directement dans Teams. Pour plus d'informations sur ProjectDale, consultez le [blog Teams de Microsoft ProjectDale.](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)

### <a name="-microsoft-blog-insights"></a>✔ de blog Microsoft

[Un examen plus étroit des fonctionnalités de plateforme de données dans Project Androiddale](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[Annonce des mises à jour de Power Platform et Teams pour aider les clients à s'adapter au travail à distance](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams met en forme l'avenir du travail avec des fonctionnalités de code faible pour améliorer votre espace de travail numérique](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ gestion des applications de plateforme Power Platform

> [!div class="nextstepaction"]
> [Gérer les applications Microsoft Power Platform dans le Centre d'administration Microsoft Teams](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)