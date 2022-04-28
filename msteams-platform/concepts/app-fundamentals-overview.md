---
title: Vue d’ensemble de la planification de votre application
author: heath-hamilton
description: Présentez les éléments de la planification d’une application, de la compréhension des cas d’usage, des fonctionnalités d’application et d’autres fonctionnalités Teams.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
keywords: fonctionnalité d’appareil d’extensibilité des points d’entrée
ms.openlocfilehash: f91ae1de96845c913d5001660a1e9f09985ca25a
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104027"
---
# <a name="plan-your-app-with-teams-features"></a>Planifier votre application avec les fonctionnalités Teams

La création d’une application Teams exceptionnelle consiste à trouver la bonne combinaison de fonctionnalités pour répondre aux besoins de votre utilisateur. La conception, les fonctionnalités et les capacités d'une application découlent de cet objectif.

Au fond, Teams est une plateforme de collaboration. Il s’agit également d’une plateforme sociale, une multiplateforme en mode natif, qui se trouve au cœur d’Office 365 et offre un canevas personnel pour vous permettre de créer des applications.

Dans cette section, découvrez comment :

* Identifiez et mappez les cas d’utilisation aux fonctionnalités Teams.
* Utilisez la liste de vérification de planification.
* Planifiez au-delà du déploiement de l’application.

## <a name="plan-with-teams"></a>Planifier avec Teams

Teams en tant que plateforme vous offre des kits de ressources, des bibliothèques et des applications à chaque étape du développement d’applications. Examinons le cycle de vie de création d’applications :

:::image type="content" source="../assets/images/app-fundamentals/plan-app.png" alt-text="Illustration montre la planification de votre application" border="true":::

* [Avant de créer](#before-you-build)
* [Pendant la build](#during-build)
* [Post-build](#post-build)
* [Liste de vérification de planification](../concepts/design/planning-checklist.md)

### <a name="before-you-build"></a>Avant de créer

Comprendre l’utilisateur et ses préoccupations sont les premiers indicateurs de la façon dont une application Teams peut vous aider. Créez votre cas d’usage autour du problème, déterminez comment une application peut le résoudre et dessinez une solution.

* **Comprendre votre cas d’utilisation et les fonctionnalités d’application Teams**: comprendre les besoins de votre utilisateur et identifier les fonctionnalités appropriées.

* **Mapper vos cas d’usage**: mappez les cas d’usage courants aux fonctionnalités Teams en fonction des exigences, telles que le partage, la collaboration, les flux de travail, les plateformes sociales pertinentes, etc.

* **Planifier des onglets réactifs pour Teams mobile**: cela couvre les scénarios courants et aide à planifier des applications pour Teams mobile.

### <a name="during-build"></a>Pendant la build

* **Créer et générer un projet d’application**: avec Teams, vous pouvez choisir l’environnement de génération qui correspond le mieux aux besoins de votre application. Utilisez le Kit de ressources Teams ou d’autres Kits de développement logiciel (SDK), tels que C#, Blazor, Node.js, etc. pour commencer.

* **Concevoir l’interface utilisateur de votre application**: utilisez le Kit de ressources d’interface utilisateur Teams et la bibliothèque d’interface utilisateur pour concevoir la disposition de votre application.

* **Utiliser Teams en tant que plateforme**: la plateforme Teams vous aide à créer une application unique ou multi-capacité. Votre application Teams est prise en charge par les produits et services intégrés qui renforcent l’expérience de l’application.

    :::image type="content" source="../assets/images/overview/teams-solution.png" alt-text="Représentation conceptuelle de la solution Teams." border="true":::

    Vos applications apparaissent dans Teams sous forme d’onglets, de bots, d’extensions de message, de connecteurs et de webhooks, ou en tant qu’application multi-fonctionnalités. Ces fonctionnalités sont optimisées sur le serveur principal par les applications Azure, Microsoft Graph, SharePoint et Power qui permettent d’automatiser les tâches et les processus.

    Ensemble, ces fonctionnalités donnent vie à votre solution d’application.

* **Intégrer des fonctionnalités d’appareil**: vous pouvez intégrer les fonctionnalités natives de l’appareil dans votre application, telles que l’appareil photo, la QR ou le scanneur de codes-barres, la galerie de photos, le microphone et l’emplacement.

### <a name="post-build"></a>Post-build

* Intégrez votre application à Teams et à d’autres applications, telles que Microsoft 365, Microsoft Graph, etc.
* Utilisez Developer Portal pour configurer, gérer et déployer votre application.

#### <a name="government-community-cloud"></a>Cloud communautaire pour le secteur public

Cloud de la communauté du secteur public (GCC) est une copie axée sur le secteur public de l’environnement commercial. Le Ministère de la défense (DOD) et les sous-traitants fédéral doivent respecter les exigences strictes en matière de cybersécurité et de conformité. À cet effet, GCC-High a été créé pour répondre aux besoins du DOD et des sous-traitants fédéral. GCC-High est une copie du cloud DOD, mais il existe dans son propre environnement souverain. Le cloud DOD est conçu pour le département de la Défense uniquement.

Le tableau suivant inclut les fonctionnalités et la disponibilité de Teams pour GCC, GCC-High et DOD :

| Fonctionnalités   | GCC | GCC-High | DOD |
|-------------|---------|---|---|
| Applications appartenant à Teams comme dans les applications développées en interne | ✔️ L’application est activée si elle a GCC. | ✔️ L’application est activée si elle a GCC-High. | ✔️ L’application est activée si elle possède un DOD. |
| Applications Microsoft | ✔️ Applications Microsoft conformes à GCC | ✔️ Applications Microsoft conformes à GCC-High | ✔️ Applications Microsoft conformes à DOD |
| Applications 3p ou tierces | ✔️ Des applications tierces sont disponibles. Désactivées par défaut et l’administrateur client utilise sa propre discrétion pour les activer. | ❌ | ❌ |
| Bots | ✔️ | ❌ | ❌ |
| Applications de tabulation personnalisées ou métier |  ✔️ | ✔️ | ✔️ |
| Chargement indépendant d’applications | ✔️ | ❌ | ❌ |
| Bots personnalisés ou Lob | ✔️ | ❌ | ❌ |
| Extensions de message personnalisées | ❌ | ❌ | ❌ |
| Connecteurs personnalisés | ❌ | ❌ | ❌ |

La liste suivante permet d’identifier la disponibilité de GCC, GCC-High et DOD pour les fonctionnalités suivantes :

* Pour les applications tierces, consultez [applications web](../samples/integrating-web-apps.md) et [extensibilité des applications de réunion](../apps-in-teams-meetings/meeting-app-extensibility.md).
* Pour les bots, consultez [créer votre premier bot conversationnel pour Teams](../get-started/first-app-bot.md), [concevoir votre bot Teams](../bots/design/bots.md), [ajouter des bots aux applications Microsoft Teams](../resources/bot-v3/bots-overview.md)et [bots dans Teams](../bots/what-are-bots.md).
* Pour le chargement indépendant des applications, consultez [permettre à votre application Teams d’être personnalisée](../concepts/design/enable-app-customization.md), [distribuer votre application Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md)et [Charger votre application dans Teams](../concepts/deploy-and-publish/apps-upload.md).
* Pour les connecteurs personnalisés, consultez [créer des connecteurs Office 365 pour Teams](../webhooks-and-connectors/how-to/connectors-creating.md).

</details>

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Cas d’utilisation et fonctionnalités Teams](design/understand-use-cases.md)

## <a name="see-also"></a>Voir aussi

* [Liste de vérification de planification](../concepts/design/planning-checklist.md)
* [Considérations relatives à l’intégration de Teams](../samples/integrating-web-apps.md)
* [Créer votre première application Microsoft Teams de messagerie](../build-your-first-app/build-first-app-overview.md)
