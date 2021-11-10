---
title: Comprendre les fonctionnalités de l’application
author: heath-hamilton
description: Description des Teams d’application, telles que les onglets, les bots, les extensions de messagerie et les webhooks et connecteurs.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.date: 09/22/2020
keywords: tabs bots messaging extensions webhooks connectors gcc
ms.openlocfilehash: e4db8bde75d2d396ada5c0789b8cc06731701443
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888145"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>Comprendre Microsoft Teams fonctionnalités de l’application

L’extensibilité ou les points d’entrée sont différentes façons dont une application peut se manifester pour un utilisateur. Par exemple, un utilisateur peut interagir avec une application sur un onglet de zone de dessin pour faire une activité ou peut choisir d’en faire de même à l’aide d’un bot de conversation. Les différentes fonctionnalités utilisées pour créer votre application Teams vous permettent d’augmenter son étendue d’utilisation.

Il existe plusieurs façons d’étendre Teams, de sorte que chaque application est unique. Certaines n’ont qu’une seule fonctionnalité, telle qu’un webhook, tandis que d’autres disposent de plusieurs fonctionnalités pour offrir différentes options aux utilisateurs. Par exemple, votre application peut afficher des données  dans un emplacement central, autrement dit, l’onglet et présenter ces mêmes informations via une interface de conversation, autrement dit, le **bot**.

## <a name="app-capabilities"></a>Fonctionnalités de l’application

Vos applications Teams ont une ou toutes les fonctionnalités principales suivantes :

* [Onglets](../tabs/what-are-tabs.md)
* [Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks et connecteurs](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

Votre application peut également tirer parti des fonctionnalités avancées, telles que [l’API Microsoft Graph pour Teams](/graph/teams-concept-overview).

L’illustration suivante vous donne une idée des fonctionnalités qui fourniront les fonctionnalités que vous souhaitez dans votre application :

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Carte d’esprit illustrant Teams fonctionnalités de l’application.":::

## <a name="always-consider-your-user"></a>Toujours prendre en compte votre utilisateur

Lorsque vous vous familiarisez avec Teams développement d’applications, vous en comprenez les principes de base. Vous comprenez qu’il existe plusieurs façons de créer certaines fonctionnalités. Dans de tels scénarios, réfléchissez à la façon dont vous pouvez offrir une expérience plus native à votre utilisateur.
Par exemple, vous pouvez collecter les entrées utilisateur dans un formulaire créé sous la forme d’un onglet dans l’application. Vous pouvez également le faire à l’aide d’un module de tâche sans changer d’affichage et perturber le flux de travail de l’utilisateur. Il est important de choisir des points d’extension qui fournissent le moins d’écart par rapport au flux de travail normal d’un utilisateur.

## <a name="government-community-cloud-gcc"></a>Government Community Cloud (GCC)

Cloud de la communauté du secteur public est une copie de l’environnement commercial axée sur le gouvernement. Le département de la Défense (DOD) et les sous-traitants fédéraux doivent répondre aux exigences strictes en matière de cybersécurité et de conformité. À cet effet, GCC-High a été créé pour répondre aux besoins des sous-traitants DOD et fédéraux. GCC-High est une copie du cloud DOD, mais il existe dans son propre environnement souverain. Le cloud DOD est conçu pour le département de la Défense uniquement.

Le tableau suivant inclut Teams fonctionnalités et la disponibilité de Cloud de la communauté du secteur public, Cloud de la communauté du secteur public-High et DOD :

| Fonctionnalités   | GCC | GCC-High | DOD |
|-------------|---------|
| Teams comme dans les applications développées en interne | ✔️'application est activée si elle Cloud de la communauté du secteur public. | ✔️'application est activée si elle Cloud de la communauté du secteur public-High. | ✔️'application est activée si elle possède un DOD. |
| Applications Microsoft | ✔️ applications Microsoft compatibles avec Cloud de la communauté du secteur public | ✔️ applications Microsoft compatibles avec GCC-High | ✔️ applications Microsoft compatibles avec LE DOD |
| Applications 3p ou tierces | ✔️ applications tierces sont disponibles. Désactivée par défaut et l’administrateur client utilise sa propre discrétion pour l’activer. | ❌ | ❌ |
| Bots | ✔️ | ❌ | ❌ |
| Applications personnalisées ou d’onglets Lob |  ✔️ | ✔️ | ✔️ |
| Chargement de version de version d’application | ✔️ | ❌ | ❌ |
| Bots personnalisés ou Lob | ✔️ | ❌ | ❌ |
| Extensions de messagerie personnalisées | ❌ | ❌ | ❌ |
| Connecteurs personnalisés | ❌ | ❌ | ❌ |

La liste suivante permet d’identifier la disponibilité de Cloud de la communauté du secteur public, Cloud de la communauté du secteur public-High et DOD pour les fonctionnalités :

* Pour les applications tierces, voir [applications web et](../samples/integrating-web-apps.md) [extensibilité des applications de réunion.](../apps-in-teams-meetings/meeting-app-extensibility.md)
* Pour les bots, voir créer votre premier [bot de conversation](../get-started/first-app-bot.md)pour Teams , la conception de votre bot [Teams](../bots/design/bots.md), ajouter des [bots](../resources/bot-v3/bots-overview.md)aux applications Microsoft Teams et les [bots](../bots/what-are-bots.md)dans Teams .
* Pour le chargement de version d’Teams, voir activer la personnalisation de votre application [Teams,](../concepts/design/enable-app-customization.md)distribuer votre [application Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md)et Télécharger votre application dans [Teams](../concepts/deploy-and-publish/apps-upload.md).
* Pour les connecteurs personnalisés, [voir créer Office 365 connecteurs pour Teams](../webhooks-and-connectors/how-to/connectors-creating.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Points d'entrée de l'application Teams](../concepts/extensibility-points.md)

## <a name="see-also"></a>Voir aussi

[Créer des applications pour Teams](../overview.md) 
 [Créer votre première application Microsoft Teams de messagerie](../build-your-first-app/build-first-app-overview.md)