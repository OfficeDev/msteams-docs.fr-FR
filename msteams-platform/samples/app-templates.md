---
title: Modèles d'application Microsoft Teams
description: Liens et descriptions des modèles d'application pour la plateforme Microsoft Teams
ms.topic: reference
keywords: Démonstration des exemples de modèles Microsoft Teams
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 04f32e7f35863d7c4b3e8744984eb6e27ec63396
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075758"
---
# <a name="app-templates-for-microsoft-teams"></a>Modèles d’application pour Microsoft Teams

Les modèles d'application sont des exemples d'applications complètes pour Microsoft Teams qui sont open source et disponibles sur GitHub. Chaque modèle d'application contient des instructions détaillées sur le déploiement et l'installation de cette application pour votre organisation. Il fournit également un exemple d'application que vous pouvez installer et commencer à utiliser immédiatement. Le code source complet est également disponible, ce qui vous permet de l'explorer en détail ou de le modifier pour répondre à vos besoins spécifiques.
Tous les modèles d'application sont fournis sous les termes du contrat [de licence MIT.](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)

> [!NOTE] 
> Vous devez obtenir une licence et prendre en charge les applications créées à partir de modèles d'application pour vos utilisateurs et organisations.

**&#9734; indique les modèles d'application nouvellement publiés.**

### <a name="key-benefits"></a>Principaux avantages

* **Déployez directement dans le cloud :** Tous les modèles d'application incluent des scripts de déploiement qui vous permettent d'héberger tous les services requis dans Microsoft Azure ou la plateforme Power. 
* **Exemple de code recommandé :** Les modèles d'application respectent les meilleures pratiques recommandées en matière de sécurité et d'infrastructure. Toutes les modifications apportées aux modèles d'application par la communauté sont examinées pour garantir la conformité.
* **Personnalisables et extensibles :** Bien que tous les modèles d'application soient déployés avec une configuration minimale, l'ensemble de la base de code et des scripts de déploiement sont fournis, afin que vous pouvez facilement les personnaliser ou les étendre pour répondre à vos besoins uniques.
* **Documentation détaillée :** Tous les modèles d'application sont accompagnés d'une documentation de bout en bout sur l'architecture de la solution, le déploiement et les étapes de configuration.  

## <a name="adoption-bot"></a>Bot d'adoption 

Le bot d'adoption est un bot de conversation utilisateur créé avec Power Virtual Agent pour Teams PVA. Il est considéré comme la version PVA de FAQ Plus. Le bot d'adoption répond à plus de 100 questions courantes sur Microsoft 365 et Teams. Vous pouvez modifier les rubriques existantes, ajouter vos propres rubriques et les faq existantes. Si les utilisateurs ont besoin d'aide supplémentaire, le bot d'adoption peut les connecter à des experts ou même être étendus pour ouvrir des tickets de service avec des connecteurs de flux premium. Ce bot est auto-installé ou intégré à une application personnalisée, telle que le Hub [d'adoption.](https://github.com/akporzondek/adoption_hub)

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a>Outil d'adoption - Plateforme de gestion champion &#9734;

Le modèle d'application de plateforme de gestion Des champions (CMP) vous permet de gérer, de mettre à l'échelle et d'inciter vos champions de travail d'équipe à atteindre d'autres objectifs. Ce modèle d'application repose sur SharePoint Framework et est chargé dans un onglet au sein d'une équipe. Les groupes peuvent tirer parti de cet outil pour gérer l'appartenance au programme, fournir un classement et des types d'événements pour la journalisation, et des outils pour superposer des badges numériques aux participants du programme.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a>Outil d'adoption : parcours d'apprentissage Microsoft 365 (mise en route) &#9734;

Le modèle d'application De mise en route vous permet d'apporter la puissance des parcours d'apprentissage Microsoft 365 à l'intérieur de Microsoft Teams. Ce modèle d'application vous permet d'accorder un accès facile à des pages de formation spécifiques ou à d'autres ressources intranet et de charger le contenu directement dans Teams. Vous pouvez également modifier le nom ou le logo de l'application pour qu'il corresponde à la marque de votre entreprise.

[L'obtenir sur GitHub](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a>Gestionnaire de rendez-vous 

Le Gestionnaire de rendez-vous est un modèle d'application Teams pour aider les entreprises à créer, gérer et mener des rendez-vous virtuels avec des clients via Teams. Les nouvelles demandes de rendez-vous des consommateurs sont visibles dans les canaux Teams, où elles sont rapidement affectées et réassignées au personnel d'une équipe. Les demandes de rendez-vous sont vues à des niveaux d'équipe ou personnels via des onglets personnalisés. Chaque rendez-vous est associé à une réunion en ligne Teams, de ce fait, le personnel et les consommateurs peuvent facilement participer à la réunion à l'heure prévue.

Le modèle d'application s'intègre à Microsoft Bookings pour faciliter la gestion des rendez-vous. Les rendez-vous programmés apparaissent automatiquement dans les calendriers des membres du personnel affectés, et les consommateurs reçoivent des notifications et rappels par courrier électronique personnalisables avec des liens de réunion incorporés.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

![Vue d'ensemble du ](../assets/images/appointment-manager-overview.png)
 ![ gestionnaire de rendez-vous dans Teams](../assets/images/appointment-manager-2.png)

## <a name="ask-away"></a>Demander l'absence

Ask Away est un [bot Microsoft Teams](../bots/what-are-bots.md) qui permet aux utilisateurs d'effectuer des questions et réponses, appelées sessions Q&A dans Teams. À l'aide du bot Ask Away, les membres de l'équipe peuvent soumettre et voter des questions partagées par des collègues, ce qui permet aux hôtes Q&A de collecter facilement des questions les plus importantes au sein d'un canal ou d'une conversation. Le bot est utilisé pour mener une session Q&A en temps réel dans une réunion Teams et permet aux participants de soumettre des questions en direct par le biais d'une conversation.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![Affichage de la boîte de dialogue de la fenêtre d'affichage du classement pour que les utilisateurs votent sur des questions](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a>Informations du collaborateur

Associate Insights est un [modèle Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) qui permet aux employés de première ligne de capturer et d'envoyer directement l'opinion, l'opinion et la perception des clients. Les employés de première ligne sont souvent le premier représentant de l'entreprise à contacter des clients dans un point de contact un-à-un. Les données collectées sont partagées et utilisées en collaboration par les équipes professionnelles, par exemple via un onglet Power BI Teams, pour améliorer le produit et améliorer l'expérience client.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![Affichage des commentaires sur les informations générées par l'application](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vue Power BI des informations générées par l'application](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a>Présence

L'application De présence est un [onglet Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) épinglé dans une équipe. Il est conçu pour enregistrer la présence dans les paramètres, tels que les environnements d'apprentissage et de formation. Les utilisateurs peuvent marquer ou modifier l'assistance jusqu'à 30 jours dans le passé et afficher des rapports de présence récapitulés pour un groupe entier ou des participants individuels. Pour plus d'informations sur la présence des équipes, voir [Obtenir sur GitHub.](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

L'image suivante affiche la démonstration de l'application de présence :  

![Démonstration de l'application de participation](../assets/images/attendance-app.png)

## <a name="book-a-room"></a>Réserver une salle

Book-a-room est un [bot Microsoft Teams](../bots/what-are-bots.md) qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pendant 30, 60 ou 90 minutes à partir de l'heure actuelle. La durée par défaut est 30 minutes. Le bot Book-a-room s'étendue à des conversations personnelles ou 1:1. Pour plus d'informations sur l'application De réservation de salle, voir [Obtenir sur GitHub.](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)  
L'image suivante affiche la démonstration du Livre dans une salle :

![Démonstration du livre dans une salle](../assets/images/book-a-room.png)

## <a name="building-access"></a>Création d'un accès

Building Access est une application basée sur Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) qui prend en charge l'administration de seuils d'occupation et de normes de d'éloignement social en permettant aux directeurs d'installations de gérer, de suivre et de signaler la présence des employés sur site. L'application, conçue à l'aide de Microsoft [Power Apps](/powerapps/powerapps-overview)et [Power Automate,](/power-automate/getting-started)s'intègre de façon profonde à Microsoft Teams et permet aux organisations de déterminer la préparation, d'établir des critères d'éligibilité pour l'accès sur site et de recueillir des informations pour la planification future.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Création d'une carte de réservation Access](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Création d'une vue de touche d'accès rapide](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a>Célébrations

La fête est une application Teams qui permet aux membres de l'équipe de se mettre à l'anniversaire, aux anniversaires et à d'autres événements périodiques. Il se souvenir des événements spéciaux de tous les membres de l'équipe et envoie un message convivial dans toutes les équipes sélectionnées au moment de la création de l'événement, pour que les membres de l'équipe se sentent spéciaux lors de leur journée.

L'application fournit une interface simple permettant à tous les membres de l'équipe d'ajouter et d'afficher leurs événements, et permet également à l'utilisateur de sélectionner les équipes dans lesquelles les événements sont partagés.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a>Liste de vérification

La liste de contrôle est une application [d'extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Microsoft Teams personnalisée qui vous permet de collaborer avec votre équipe en créant une liste de contrôle partagée dans une conversation ou un canal. L'application est prise en charge sur tous les clients de plateforme Teams, tels que le navigateur de bureau, iOS et Android. L'application est prête pour le déploiement dans le cadre de votre abonnement Microsoft 365.  

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![Créer une liste de contrôle en affichage Teams](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a>Salle de classe 

Classroom Drop-in est une application basée sur la plateforme Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)qui permet aux responsables système de rechercher des équipes de classe, c'est-à-dire des salles de classe virtuelles et de s'ajouter eux-mêmes ou d'autres à ces équipes de classe pour une période de présentation spécifiée, selon vos besoins. L'application conçue à l'aide de Microsoft [Power Apps](/powerapps/powerapps-overview) et [Power Automate](/power-automate/getting-started), s'intègre en profondeur à Microsoft Teams pour garantir que les établissements d'enseignement peuvent optimiser leurs opérations dans un environnement d'apprentissage hybride en fournissant l'accès aux parties prenantes pertinentes pour les équipes de classe selon les besoins de l'entreprise.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Demande de salle de classe](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a>Communicateur d’entreprise

L'application Communicator entreprise permet aux équipes d'entreprise de créer et d'envoyer des messages destinés à plusieurs équipes ou à un grand nombre d'employés par conversation, ce qui permet à l'organisation d'atteindre les employés là où elles collaborent. Utilisez ce modèle pour plusieurs scénarios tels que les annonces de nouvelles initiatives, l'intégration des employés, l'apprentissage et le développement modernes ou les diffusions à l'échelle de l'organisation.

L'application fournit une interface simple pour que les utilisateurs désignés créent, prévisualiser, collaborent et envoient des messages.

Il fournit une base pour créer des fonctionnalités de communication ciblées personnalisées telles que la télémétrie personnalisée sur le nombre d'utilisateurs reconnus ou ayant interagi avec un message.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![Affichage de la zone Communicator composition jCompany](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a>Recherche de groupe de contacts

L'application de recherche de groupe de contacts offre une approche pratique et utile pour la création, l'accès et la gestion des groupes de contacts de votre organisation, anciennement appelés listes de distribution ou groupes de communication. Les utilisateurs peuvent rapidement afficher et discuter avec les membres du groupe, afficher l'état des membres et créer une conversation de groupe avec des membres sélectionnés dans le groupe de contacts, le tout dans l'environnement Teams.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

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

## <a name="co-worker-appreciation"></a>Collègues 

À l'aide du modèle de collaboration de Microsoft Teams, les utilisateurs peuvent reconnaître les succès de leurs collègues dans le contexte de Teams. Lorsque des collègues choisissent de récompenser un collègue, les destinataires et les autres membres de l'équipe sont marqués dans une conversation de canal et reçoivent une notification concernant les détails de l'attribution du canal. Les prix sont enregistrés dans l'application Teams, qui est sécurisée, portable et facilement partageable. Il s'agit de la version powerApps du modèle d'application Open Badges, avec un classement.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![Globalement](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a>CrowdSourcer

CrowdSourcer est un [bot Microsoft Teams](../bots/what-are-bots.md) qui fournit aux équipes des informations interrogés provenant de façon collaborative à partir des membres du groupe. Il permet de répondre aux questions fréquemment posées tout en permettant aux participants de s'impliquer activement et de contribuer à une ressource d'informations agréable et utile.

[L'obtenir sur Github](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interaction de l'utilisateur final de la source de contenu](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a>Autocollants personnalisés

L'expression autonome est essentielle à une culture d'équipe saine. Ce modèle d'application est une [extension](~/messaging-extensions/what-are-messaging-extensions.md) de messagerie qui permet à vos utilisateurs d'utiliser des autocollants personnalisés et des GIF dans Microsoft Teams. Ce modèle offre une expérience de configuration web simple dans laquelle toute personne ayant un accès à la configuration peut télécharger les GIF, les autocollants et les images qu'elle souhaite que ses utilisateurs disposent, ce qui permet à toute votre équipe d'utiliser n'importe quel ensemble d'autocollants de votre choix.

Cette application permet également de partager facilement des images, des GIF et des autocollants dans les équipes sans avoir besoin d'accéder aux sites SharePoint ou aux canaux individuels en tant que mécanismes de stockage et de partage. Par exemple, les équipes produit peuvent facilement partager des images de produit et des GIF sur les réseaux sociaux, le marketing et les équipes commerciales par programme. Vous pouvez également étendre cette application en déclenchant un flux de notification à des équipes ou des individus spécifiques lorsque de nouvelles images et des GIF sont disponibles.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Application Autocollants](../assets/images/stickers.png)

## <a name="employee-ideas"></a>Idées d'employés

L'application Idées d'employés est la version PowerApps du modèle d'application Idées intéressantes basé sur Azure. L'application permet aux utilisateurs de Teams de configurer et de configurer une campagne d'idées. Une campagne d'idées est une catégorie de regroupement d'idées autour de thèmes courants.

Les utilisateurs de Teams peuvent également effectuer les activités suivantes :

* Configurez un formulaire d'envoi standard que les employés doivent envoyer pour chaque idée. 
* Examiner et gérer les idées et la liste des campagnes.
* Modifier et supprimer des campagnes.
* Passer en revue les conseils d'idées.
* Votez pour et partagez des idées prioritaires.
* Soumettre des idées pour une campagne.
* Afficher l'idée d'un autre membre de l'équipe.
* Votez sur la plupart des idées aimées.
* Examinez les performances de leurs idées par rapport aux autres au sein d'une campagne.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![Gérer l'affichage campagne](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a>E-Ent 

E-Titre est une application [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) qui améliore la télémédeicine et les soins virtuels en automatisant le processus d'émission de courrier électronique aux patients. Les professionnels de la santé peuvent rapidement passer en revue les rendez-vous, générer des courriers électroniques et envoyer des courriers électroniques avec des pièces jointes électroniques aux patients directement dans la plateforme Teams.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![Capture d'écran de l'application E-Nouvelle. Montre comment un fournisseur de soins de santé peut sélectionner un bouton générer pour commander une ordonnance pour un patient.](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Capture d'écran de l'application E-Nouvelle. Montre comment les administrateurs peuvent gérer les fournisseurs de soins de santé qui utilisent l'application.](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a>Formation des employés 

La formation des employés est une application Microsoft Teams qui permet aux organisateurs de publier, de suivre et de promouvoir facilement des événements d'apprentissage et de formation pour votre organisation.  Avec l'application, les planificateurs d'événements peuvent envoyer des rappels et des notifications aux personnes inscrites aux événements et les employés peuvent indiquer leur intérêt pour les événements à venir, rester informés des événements en cours et partager des détails des événements avec leurs collègues via l'extension de messagerie Teams.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    **Afficher les événements de formation des employés** ![ Image de l'onglet Formation des employés](../assets/images/employee-training-discover-tab.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    **Créer un événement de formation pour les employés** ![ Formulaire de création d'événement pour la formation des employés](../assets/images/employee-training-create-event.jpg)
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a>Expert Finder

Expert Finder est un [bot Microsoft Teams](../bots/what-are-bots.md) qui identifie des membres spécifiques de l'organisation en fonction de leurs compétences, de leurs intérêts et de leurs attributs d'éducation. Les membres trouvent des experts au sein d'une organisation qui correspondent à une recherche par mot clé des profils utilisateur Azure Active Directory.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Démonstration des résultats de la recherche du finder expert](../assets/images/expert-finder.png)

## <a name="faq-plus"></a>Forum aux questions

Les réponses aux questions fréquemment posées par les utilisateurs&bots sont un moyen simple de fournir des réponses aux questions fréquemment posées par les utilisateurs. Toutefois, la plupart des bots ne parviennent pas à interagir avec les utilisateurs de manière significative, car il n'y a aucun humain dans la boucle lorsque le bot échoue. Le bot FAQ est une question-&un bot qui met un humain dans la boucle lorsqu'il n'est pas en mesure de vous aider. Vous pouvez poser une question au bot et le bot répond par une réponse s'il est contenu dans la base de connaissances. Si ce n'est pas le cas, le bot permet à l'utilisateur d'envoyer une requête qui est ensuite publiée à une équipe pré-configurée d'experts qui aident à fournir un support en agissant sur les notifications à partir de l'équipe elle-même.

> [!NOTE]
> La dernière version de **FAQ Plus** prend en charge les résolutions&A améliorées en permettant à une équipe d'experts d'effectuer les choses suivantes :
>
> &#x2714; ajoutez de nouvelles Q&directement à la base de connaissances à l'aide des extensions de message.
>
> &#x2714; modifier et supprimer des&des paires A ajoutées par un bot.
>
> &#x2714; l'historique des révisions de Q&As.
>
> &#x2714; configurer une réponse avec des détails supplémentaires à afficher en tant que [carte adaptative.](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)
>
[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ Plus gif](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a>Obtenir une application de support

L'application Obtenir un support est utilisée par les organisations qui utilisent Microsoft Teams, pour permettre à n'importe quel ensemble d'utilisateurs de demander de l'aide aux superviseurs. Cette application inclut les fonctionnalités suivantes :
* Demande d'assistance sur différentes catégories à partir d'une application Power.
* Notifications envoyées aux demandeurs les informant de la personne affectée.
* Notifications envoyées aux superviseurs affectés les informant des personnes qui ont besoin d'aide. 
* Analyse des escalades et des modèles dans SharePoint et PowerBI.S

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Obtenir un gif de support](../assets/images/get-support.gif)

## <a name="goal-tracker"></a>Suivi des objectifs

L'application De suivi des objectifs est une solution complète pour votre organisation qui permet de prendre en charge l'établissement d'objectifs, l'observation de la progression et l'accusé de succès dans Microsoft Teams. L'application permet aux utilisateurs de définir, suivre et mettre à jour des objectifs au niveau professionnel, personnel et d'équipe. Les membres de l'équipe reçoivent également des rappels et des mises à jour d'état à temps pour rester concentrés et suivre.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a>Bonnes idées

L'application Bonnes idées prend en charge et favorise l'innovation et la créativité au sein de votre organisation. L'application permet à vos employés de partager des idées avec leurs collègues et leur direction, de découvrir de nouvelles soumissions, de faire la une pour la considération des pairs et de voter pour les meilleures propositions au sein de Microsoft Teams.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a>Activités de groupe

Activités de groupe est une application Microsoft Teams qui permet aux propriétaires d'équipes de créer rapidement des groupes d'activités et de gérer les flux de travail de collaboration dans le contexte de Microsoft Teams. Les auteurs d'activités sont activés pour créer des activités, distribuer de manière aléatoire les membres de l'équipe dans des groupes et éventuellement faire envoyer des rappels au bot jusqu'à ce que les activités soient terminées.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Liste des activités de groupe dans Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Message de notification d'activité de groupe dans un canal](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a>Développer vos compétences

L'application Développer vos compétences prend en charge la croissance et le développement professionnels en permettant aux employés de contribuer à des projets supplémentaires pour votre organisation tout en apprendant simultanément de nouvelles compétences. Les employés peuvent utiliser l'application pour rechercher des opportunités qui répondent à leurs intérêts, profiter d'une collaboration significative avec leurs homologues et acquérir de nouveaux niveaux d'expertise et de fonctionnalités, le tout dans l'environnement Teams.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![Affichage des projets disponibles](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vue des compétences acquises de la visionneuse](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a>Prise en charge RH

Le bot de support rh est une question-&un bot qui apporte un professionnel du support technique ou un expert de l'équipe RH en boucle lorsqu'il n'est pas en mesure de vous aider. Vous pouvez poser une question au bot et le bot répond par une réponse s'il est contenu dans la base de connaissances. Si ce n'est pas le cas, le bot permet à l'utilisateur d'envoyer une requête qui est ensuite publiée dans une équipe pré-configurée d'experts qui aident à fournir un support en agissant sur les notifications à partir de leur équipe elle-même. En outre, le bot suggère des liens vers des stratégies ou des questions RH recommandées en recherchant des balises pré-configurées dans la question. Ces vignettes sont trouvées dans l'onglet associé en tant que référence rapide. Le support RH fonctionne bien pour les questions de poids faible&A et pour fournir un support rapide lors du lancement de nouveaux projets ou initiatives dans l'organisation.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Prise en charge RH](../assets/images/expert-user.png)

## <a name="icebreaker"></a>Brise-glace

Icebreaker est un [bot Microsoft Teams](../bots/what-are-bots.md) qui permet à votre équipe de se rapprocher en couplant deux membres d'équipe aléatoires par semaine pour se réunir. Le bot facilite la planification en suggérant automatiquement des heures libres qui fonctionnent pour les deux membres. Renforcez les connexions personnelles et créez une communauté étroite avec cette application.

En plus d'encourager les connexions personnelles au sein de l'ensemble de votre équipe, l'application Icebreaker peut contribuer à promouvoir les communautés basées sur l'intérêt au sein de votre organisation. Par exemple, vous pouvez utiliser cette application pour un groupe d'intérêt DevOps afin d'aider les idées et les meilleures pratiques à se propager de façon organique au sein de votre organisation.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Application icebreaker](../assets/images/icebreaker.png)

## <a name="incentives"></a>Primes incitatives

Les primes incitatives sont un [modèle Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) qui gère et suit la participation des employés incentivisés aux activités désignées, telles que les formations et les initiatives de gestion des changements. Les administrateurs utilisent l'application pour établir des activités désignées, affecter des points pour l'achèvement et spécifier les niveaux de point d'éligibilité requis pour les primes. Les employés utilisent l'application pour afficher leurs points cumulés et, dès qu'ils sont éligibles, ils demandent et demandent des avantages.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Démonstration d'application de primes incitatives](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a>Reporter d'incident

Le reporter d'incidents [est un bot Microsoft Teams](../bots/what-are-bots.md)  qui optimise la gestion des incidents dans votre organisation. Le bot facilite la collecte automatisée des données d'incident, les rapports d'incident personnalisés, les notifications des parties prenantes pertinentes et le suivi des incidents de bout en bout.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Affichage de l'étendue du groupe de reporter d'incidents](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Vue d'étendue personnelle du reporter d'incident](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection"></a>Inspection 

 L'inspection est une application Microsoft Teams qui permet aux employés de première ligne d'inspecter n'importe quoi, des emplacements aux ressources et équipements. Par exemple, un magasin de vente au détail, une usine de fabrication ou des véhicules et des ordinateurs. Il existe deux applications dans cette solution, chacune destinée à différents types d'utilisateurs.

L'application permet aux employés de première ligne d'inspecter un bien ou une zone, de gérer la qualité des produits et services ou de maintenir la sécurité sur l'espace de travail. Il facilite la communication entre les membres de l'équipe pour résoudre les problèmes trouvés lors de l'inspection. L'application fournit des rapports simples aux responsables pour accélérer la résolution des problèmes et mettre en évidence les tendances.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Vue d'ensemble de l'inspection](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a>Rapports de problèmes

L'application Rapports de problèmes permet aux employés et aux responsables de lever et de gérer les problèmes. Il se compose de deux applications, Issue reporting app for reporting issues and Manage Issues app for managing issues.

Les responsables d'équipe utilisent l'application Gérer les problèmes pour configurer l'expérience d'application, y compris le canal dans lequel les messages Microsoft Teams et les tâches du Planificateur sont créés par l'application. Les responsables utilisent également l'application pour créer des formulaires de modèle afin de collecter des détails lorsqu'un utilisateur signale un problème. Par exemple, examinez, modifiez ou supprimez des formulaires de modèle d'émission. L'application est également utilisée pour passer en revue les problèmes de l'équipe, signaler l'historique des problèmes et gérer efficacement la résolution des problèmes.

Les employés utilisent l'application De rapport de problèmes pour enregistrer les problèmes et les détails nécessaires pour les résoudre. L'application est également utilisée pour modifier et résoudre les problèmes existants et obtenir une vue d'avant-plan des problèmes individuels ou d'équipe.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Affichage de l'équipe de rapports de problèmes](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a>Intégration de nouveaux employés 

L'intégration de nouveaux employés est une solution intégrée d'intégration de Microsoft Teams et de [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) Nouveaux employés qui permet à votre organisation de fournir une expérience d'intégration cohérente et de haute qualité aux employés lors de leur parcours d'embauche. L'application est utilisée par les équipes de ressources humaines et les responsables de l'embauche pour fournir des informations pertinentes tout au long du processus d'orientation et de création, ainsi que par les nouveaux employés pour partager des commentaires, fournir des introductions et effectuer des tâches d'intégration.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    **Carte de bienvenue des nouveaux employés** ![ Image de la carte de bienvenue des nouveaux employés](../assets/images/new-employee-welcome-card.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    **Liste de vérification des nouveaux employés** ![ Image de la liste de contrôle des nouveaux employés](../assets/images/new-employee-checklist.png)  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a>Ouvrir des badges

Open Badges est une application Microsoft Teams qui permet aux utilisateurs de gagner des badges d'identification d'apprentissage numérique dans le contexte Teams et de les partager partout. L'utilisation des fonctionnalités de l'autorité d'émission de badge numérique tiers, [Badgr](https://badgr.org/), badges attribués sont enregistrées dans le profil Badgr d'un destinataire et disponibles pour créer et partager une image complète des parcours d'apprentissage de la durée de vie.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a>Sondage 

Poll est une application [d'extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Microsoft Teams personnalisée qui vous permet de créer et d'envoyer rapidement des sondages dans une conversation ou un canal pour recueillir les opinions et les préférences de l'équipe. L'application est prise en charge sur tous les clients de plateforme Teams, tels que le bureau, le navigateur, iOS et Android, et est prête pour le déploiement dans le cadre de votre abonnement Microsoft 365.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Créer un sondage en affichage Teams](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a>Réponses rapides

Les réponses rapides sont une application Microsoft Teams qui fournit une solution robuste pour répondre efficacement aux questions fréquemment posées par les utilisateurs. Au lieu de répondre à chaque requête manuellement et en continu, l'application crée une bibliothèque de réponses pour une expérience utilisateur interactive via les [extensions](../messaging-extensions/what-are-messaging-extensions.md)de messagerie Teams.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![Exemple d'affichage des réponses](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a>Questionnaire &#9734;

Questionnaire est une application [d'extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Teams personnalisée qui vous permet de créer un questionnaire au sein d'une conversation ou d'un canal pour vérifier les connaissances et obtenir des résultats instantanés. Vous pouvez utiliser les questionnaires pour les examens en cours et hors connexion, la vérification des connaissances au sein de l'équipe et pour des questionnaires amusants au sein d'une équipe. L'application Quiz est prise en charge sur plusieurs plateformes, telles que les clients teams de bureau, de navigateur, iOS et Android. Cette application est prête pour le déploiement dans le cadre de votre abonnement Microsoft 365 existant.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Créer un questionnaire en affichage Teams](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a>Assistance rapide

Quick Assist est une application basée sur microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) qui permet aux associés de se connecter rapidement aux experts pour obtenir des réponses rapides, rechercher des informations, suivre des demandes ouvertes et permettre aux experts de recevoir des notifications pour passer rapidement à un appel pour répondre aux questions. L'application conçue à l'aide de Microsoft [Power Apps](/powerapps/powerapps-overview) et [Power Automate](/power-automate/getting-started), s'intègre en profondeur à Microsoft Teams pour permettre aux organisations de connecter facilement des travailleurs de l'entreprise aux liaisons d'entreprise pour résoudre les requêtes des clients et offrir une expérience client excellente. 

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![Interface de demande de l'utilisateur final](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![Affichage des demandes d'expert](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a>Reflect 

Reflect est une application [d'extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Microsoft Teams personnalisée qui fournit une ressource sécurisée et inclusive pour que les membres de votre équipe partagent l'état de leur bien-être émotionnel avec leurs collègues ou responsables de groupe directement au sein de Teams. L'application est disponible dans les conversations de canal, de groupe, de réunion et 1:1 et la réponse d'enregistrement est définie sur public, privé à expéditeur ou entièrement anonyme.

[L'obtenir sur GitHub](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    **Sondage de bien-être**
    
    ![Refléter le sondage de l'utilisateur de l'application](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a>Prise en charge à distance

Le support à distance est [un bot Microsoft Teams](../bots/what-are-bots.md) qui fournit une interface axée entre les demandeurs de support dans toute votre organisation et l'équipe de support interne.  Les utilisateurs finaux peuvent soumettre, modifier ou retirer des demandes de support, et l'équipe de support peut répondre, gérer et mettre à jour les demandes dans la plateforme Teams.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a>Demander une équipe

Demander une équipe est une application Microsoft Teams qui optimise la création d'équipes pour votre organisation d'entreprise. L'application prend en charge la normalisation et les meilleures pratiques lors de la création d'instances d'équipe par le biais de l'intégration d'un formulaire de demande guidé par l'Assistant, d'un processus d'approbation incorporé, d'un tableau de bord d'état des demandes et de builds d'équipe automatisées.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Affichage de la page de démarrage demande-à-équipe](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Affichage de la page de l'Assistant Demande-à-équipe](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a>Scrums pour les canaux

Scrums for Channels est une application d'assistant scrum qui permet aux utilisateurs de planifier et d'exécuter des scrums dans les canaux de Microsoft Teams. L'application est excellente pour les équipes distantes et les équipes composées de membres de différents emplacements géographiques et fuseaux horaires pour partager des mises à jour quotidiennes et garantir la participation à des réunions de secours.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> Pour effectuer des réunions scrum dans une conversation de groupe, voir [Scrums for Group Chat](#scrums-for-group-chat) app template.

:::row:::
  :::column span="2":::
    ![Scrums pour l'affichage des paramètres des canaux](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrums pour l'affichage d'état des membres de l'équipe des canaux](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a>Scrums pour la conversation de groupe

> [!NOTE]
> Le modèle d'application État de Scrums est mis à jour et est désormais Scrums pour la conversation de groupe.

Scrums for Group Chat est un assistant scrum positif qui permet aux membres de conversation de groupe d'exécuter des réunions de stand-up asynchrones et de partager facilement leurs mises à jour quotidiennes. Elle permet à tous les membres de la conversation de groupe de contribuer à la scrum et d'afficher les mises à jour réalisées par d'autres personnes dans la scrum en cours d'exécution.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Démonstration Scrums for Group Chat](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a>Partager maintenant 

L'application Partager maintenant favorise l'échange positif d'informations entre collègues en permettant à vos utilisateurs de partager facilement du contenu dans l'environnement Teams. Les utilisateurs engagent l'application pour partager des éléments d'intérêt avec les membres de l'équipe, découvrir de nouveaux contenus partagés, définir des préférences et des favoris de signet pour une lecture ultérieure.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![Sélectionner un affichage de contenu](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a>Recherche de liste SharePoint

La collaboration dans Microsoft Teams référence assez souvent les informations contenues dans les éléments d'une liste SharePoint. Coller un lien vers l'élément en question force tout le monde à basculer le contexte de la conversation, à trouver les informations nécessaires, puis à revenir à Teams pour poursuivre la conversation. À mesure que la conversation se poursuit, les utilisateurs doivent revenir à l'élément de référence plusieurs fois pour vérifier les nouveaux commentaires et actualiser leurs informations contenues dans l'élément. Ce basculement de contexte crée un obstacle à la collaboration en douceur.
Pour résoudre ce problème, le modèle d'application Recherche de liste est utilisé. De nombreux utilisateurs utilisent SharePoint pour alimenter certains des flux de travail principaux de leur organisation. Toutefois, la collaboration autour de listes est difficile. À l'aide du modèle d'application Recherche de liste dans Microsoft Teams, les utilisateurs peuvent insérer des informations à partir d'éléments de liste SharePoint directement dans une conversation pour réduire le basculement de contexte provoqué lors de l'insertion d'un lien dans une conversation. Les informations sont insérées sous la forme d'une carte mise en forme automatique facile à lire, ce qui permet aux utilisateurs de rester impliqués dans la conversation.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Application de recherche de liste](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a>Vérifications du personnel

Les vérifications du personnel sont une application [Power Apps](/powerapps/powerapps-overview) qui permet de contrôler la communication entre votre entreprise et le personnel sur le terrain. Le personnel peut facilement fournir des informations critiques et des mises à jour d'état sur une base programmée ou ad hoc directement à partir de Teams. L'application prend en charge l'emplacement en temps réel, les photos, les notes, les notifications de rappel et les flux de travail automatisés.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![Créer un affichage d'enregistrement](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a>Enquête

L'enquête est une application [d'extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Microsoft Teams personnalisée qui vous permet de créer une enquête dans une conversation ou un canal pour collecter des données et obtenir des informations actionnables. L'application est prise en charge sur tous les clients de plateforme Teams, tels que le bureau, le navigateur, iOS et Android, et est prête pour le déploiement dans le cadre de votre abonnement Microsoft 365.  

[L'obtenir sur GitHub](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Créer une enquête en affichage Teams](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a>Time Tally 

Un projet peut inclure plusieurs tâches et divers projets peuvent être affectés à des employés. Les responsables doivent comprendre l'avancement du projet tout au long du temps passé par les employés sur ces tâches. Cette activité peut être fastidieuse, car les employés doivent remplir les feuilles de temps. L'application Time Tally permet aux employés de remplir rapidement leurs feuilles de temps, à l'aide de l'appareil mobile, et les responsables n'ont pas à suivre les employés sur l'entrée de feuille de temps. Les responsables peuvent afficher l'utilisation du projet en fonction des ressources, et ils peuvent approuver ou rejeter les entrées. Les notifications de rappel sont envoyées pour garantir la conformité de la feuille de temps. En outre, les données historiques et les utilisations sont disponibles pour l'analyse.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Time Tally](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a>Formation &#9734;

La formation est une application [d'extension](../messaging-extensions/what-are-messaging-extensions.md) de messagerie Teams personnalisée qui permet aux utilisateurs de publier une formation au sein d'une conversation ou d'un canal pour le partage des connaissances hors connexion et l'upsqualing. L'application est prise en charge sur plusieurs clients de plateforme Teams, tels que le bureau, le navigateur, iOS et Android. Cette application est prête pour le déploiement dans le cadre de votre abonnement Microsoft 365.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Créer une formation dans l'affichage Teams](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a>Arrondi virtuel

Les fournisseurs d'urgence et d'hôpital font de nombreuses **opérations** par jour. Ces vérifications rapides sur les patients sont destinées à fournir une vérification de l'état du patient et à s'assurer que ses préoccupations sont traitées. Bien que l'arrondi soit une pratique essentielle pour s'assurer que les patients sont surveillés par plusieurs types de fournisseurs, ils représentent un drainage considérable de l'PPE, car pour chaque visite, à partir de chaque fournisseur, un nouveau masque et un nouvel ensemble de gants sont utilisés. Grâce à ces modèles d'application, les travailleurs médicaux peuvent facilement mener des séries de cycles virtuellement, par le biais d'une réunion Microsoft Teams entre le fournisseur et le patient.

La solution d'arrondi virtuel est également référencé dans le billet de [blog](https://aka.ms/teamsvirtualrounding)Microsoft Health and Life Sciences .

[L'obtenir sur GitHub](https://github.com/SmartterHealth/Virtual-Rounding)

![Arrondi virtuel](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a>Gestion des visiteurs

L'application Gestion des visiteurs permet à votre organisation et à vos employés de gérer facilement et efficacement le processus des visiteurs sur site, directement à partir de Microsoft Teams. L'application permet aux employés de créer des demandes de visiteurs, de suivre de manière centralisée l'état d'une demande via le tableau de bord du visiteur et de recevoir des notifications en temps réel lorsqu'un visiteur arrive.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![Créer un affichage de demande](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Notification d'arrivée des visiteurs](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards"></a>Workplace Lieu de travail

Workplace Lieu de travail est un modèle d'application Teams qui fournit une infrastructure positive pour favoriser la reconnaissance et encourager la culture de reconnaissance des employés dans l'espace de travail moderne. L'application vous permet de configurer et de gérer un programme de reconnaissance et de reconnaissance des employés, appelé programme R&R, dans lequel les employés peuvent facilement nommer et approuver des collègues et votre responsable R&R peut afficher les candidats envoyés, accorder des prix et annoncer des destinataires.

[L'obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![Carte de poste de travail ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Onglet liste des listes de classements de l'espace de travail](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

Pour plus d'informations sur le modèle d'application, voir [Modèle d'application.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)

## <a name="see-also"></a>Voir aussi

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
