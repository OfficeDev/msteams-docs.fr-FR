---
title: Solution Teams pour la création d’applications
author: heath-hamilton
description: Découvrez comment planifier, concevoir, générer, étendre à Microsoft 365, tester, distribuer, monétiser et intégrer votre application à Teams.
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 11/02/2021
ms.openlocfilehash: ac4f3a208484a093460a14777a351aa4abc10af7
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100783"
---
# <a name="the-teams-solution"></a>La solution Teams


Plateforme Microsoft Teams est une plateforme puissante et flexible qui vous permet de créer des applications pour Teams. Il fournit une vaste suite d’environnements et d’outils de développement pour prendre en charge le développement d’applications.

## <a name="the-user-story"></a>Le récit utilisateur :

Vous avez affiché les offres Teams. Vous pouvez désormais les mapper aux besoins de l’utilisateur. Revoyons le scénario.

Le développeur de l’agence Tours and Travel souhaite créer une application pour ses utilisateurs, les voyageur. L’application doit :

- Vérifiez et envoyez les prévisions aux voyageurs inscrits auprès de l’agence de voyage.
- Informez les utilisateurs un jour avant la date de départ afin qu’ils puissent planifier.

Collez et mappez les exigences aux fonctionnalités Teams :

| Besoins de l’application utilisateur | Vérifier les prévisions | Notification avant le voyage | Utilisateur inscrit |
| --- |:---:|:---:|:---:|
| **Fonctionnalité** | Bot | &nbsp; | &nbsp; |
| **Intégration** | &nbsp; | &nbsp; | :::image type="icon" source="assets/icons/microsoft-icon.png"::: Microsoft Graph, API Météo |
| **Scope** | &nbsp; | Application personnelle | &nbsp; |
| **Point d'intégration** | &nbsp; | Conversation | &nbsp; |

La **solution d’application Teams** : un *bot de conversation personnelle* de l’application Teams qui vérifie et *envoie des notifications de prévision* à *des utilisateurs inscrits* avant leur date de voyage.

:::image type="content" source="../msteams-platform/assets/images/overview/developer-scenario-solution.png" alt-text="Un développeur d’une agence de voyages crée un bot pour Teams qui envoie des prévisions météorologiques aux clients afin qu’ils puissent planifier leurs dates de voyage":::

Teams offers these and many more capabilities to bring your users a feature-rich app solution. To develop this app:

1. Créez une application de bot de conversation personnelle.
1. Intégrez-la à une API de prévisions météorologiques externe pour vous connecter et demander des prévisions pour une date et un emplacement spécifiques.
1. Intégrez avec :::image type="icon" source="assets/icons/teams-icon.png"::: Microsoft Graph pour les utilisateurs inscrits.
1. Vérifiez et envoyez les détails des prévisions en fonction de la date et de l’emplacement du voyage de l’utilisateur.

## <a name="choose-what-suits-you"></a>Choisissez ce qui vous convient

Vous pouvez créer une application Teams conformément aux exigences de votre application. En fonction de facteurs, tels que les besoins de l’entreprise, l’environnement de développement, les connaissances du domaine, sélectionnez l’environnement et les outils que vous souhaitez créer votre application.

Une application Teams vous offre la flexibilité de choisir votre environnement de build. Il inclut des outils, des infrastructures et des langues pour aborder le développement de votre application.

:::image type="content" source="../msteams-platform/assets/images/overview/tools-of-your-choice.png" alt-text="Besoin commercial de l’application":::

Build your Teams app in the environment that works for your particular requirements. You can even select a combination.

Par exemple, vous pouvez utiliser le Kit de ressources Teams pour créer une application avec JavaScript et l’héberger sur un site SharePoint.

## <a name="teams-collaborative-platform"></a>Plateforme collaborative Teams

Une application Teams offre à vos utilisateurs les avantages d’un espace de travail collaboratif.

En tant que plateforme de création d’applications, Teams offre la gamme complète d’applications et de kits de ressources. La plateforme Teams vous prend en charge à chaque étape, de la planification de votre application à sa distribution.

:::image type="content" source="../msteams-platform/assets/images/overview/teams-dev-life-cycle.png" alt-text="Description d’un cycle de vie du développement d’applications Teams. Planifier, concevoir, générer, étendre, tester, déployer, distribuer. Détails affichés dans une liste à puces ci-dessous.":::

From designing to building and distributing a Teams app, you can use various tools and services. An example development flow can be:

1. Planifiez votre projet et déterminez l’exigence.
1. Design the app. Use Teams UI Kit and UI Library for designing tabs UI.
1. Créez l’application avec JavaScript à l’aide du Kit de ressources Teams.
1. Étendez les fonctionnalités en ajoutant des fonctionnalités Teams et des données M365 avec :::image type="icon" source="assets/icons/microsoft-icon.png"::: Microsoft Graph.
1. Testez l’application sur un locataire de développeur avec des exemples de données utilisateur.
1. Déployez l’application sur Azure.
1. Gérez et publiez les applications dans le Store avec Developer Portal. Monétisez votre application avec des options, telles que les offres SaaS, les achats in-app et bien plus encore.

## <a name="next-step"></a>Étape suivante

:::row:::
    :::column span="1":::
        **Commencer la création**
    :::column-end:::
    :::column span="2":::
        Familiarisez-vous rapidement avec la création d’applications pour Teams en configurant votre environnement et en créant une application simple.

        > [!div class="nextstepaction"]
        > [Créer votre première application](get-started/get-started-overview.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Voir aussi

:::row:::
    :::column span="1":::
        **Planifier votre application**
    :::column-end:::
    :::column span="2":::
        Comprendre et mapper les cas d’utilisation de votre application aux fonctionnalités Teams.

        > [!div class="nextstepaction"]
        > [Planifier votre application](~/concepts/app-fundamentals-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Concevoir votre application**
    :::column-end:::
    :::column span="2":::
        Concevez l’interface utilisateur de votre application avec le Kit d’interface utilisateur Teams.

        > [!div class="nextstepaction"]
        > [Concevoir votre application Teams](~/concepts/design/design-teams-app-process.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Créer votre application**
    :::column-end:::
    :::column span="2":::
        Looking for app development inspiration? Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways a Teams app can help your users.

        > [!div class="nextstepaction"]
        > [Voir les scénarios d’application](https://adoption.microsoft.com/en-us/extensibility-look-book-gallery/)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Développez votre application dans Microsoft 365**
    :::column-end:::
    :::column span="2":::
Vous pouvez prévisualiser vos applications Teams exécutées dans d’autres expériences Microsoft 365 à utilisation élevée avec le Kit de développement logiciel (SDK) client JavaScript Teams v2 Preview.

        > [!div class="nextstepaction"]
        > [Étendre votre application](m365-apps/overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Tester votre application**
    :::column-end:::
    :::column span="2":::
        Après avoir intégré votre application à Teams, vous devez tester votre application avant de la publier.

        > [!div class="nextstepaction"]
        > [Tester votre application](concepts/build-and-test/test-app-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Distribuer votre application.**
    :::column-end:::
    :::column span="2":::
        Vous pouvez fournir votre application Teams à une personne, une équipe, une organisation ou toute personne qui souhaite l’utiliser.

        > [!div class="nextstepaction"]
        > [Distribuer votre application.](~/concepts/deploy-and-publish/apps-publish-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Monétiser votre application**
    :::column-end:::
    :::column span="2":::
        Teams store propose des options de monétisation d’applications, telles que les offres SaaS et les achats in-app. Choisissez l’option de monétisation la plus adaptée à Teams application.

        > [!div class="nextstepaction"]
        > [Monétiser votre application](concepts/deploy-and-publish/appsource/prepare/monetize-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **S'intégrer aux équipes**
    :::column-end:::
    :::column span="2":::
        Associez les fonctionnalités que les utilisateurs apprécient dans une application, un service ou un système web existant aux fonctionnalités collaboratives de Teams.

        > [!div class="nextstepaction"]
        > [Intégrer une application existante](samples/integrating-web-apps.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Un petit code suffit**
    :::column-end:::
    :::column span="2":::
        You don't need to be an expert programmer to build a great Teams app. Try one of several low-code solutions.

        > [!div class="nextstepaction"]
        > [Créer une application à faible code](samples/teams-low-code-solutions.md)
    :::column-end:::
:::row-end:::
