---
title: Comprendre les capacités de l’application
author: heath-hamilton
description: Teams d’applications expliquées
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 209d187681b1370440931fcd40744965395b13e8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565150"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>Comprendre les Microsoft Teams’applications

L’extensibilité ou les points d’entrée sont différentes façons dont une application peut se manifester à un utilisateur. Par exemple, un utilisateur peut interagir avec une application sur un onglet de toile pour faire une activité ou peut choisir de faire de même à l’aide d’un bot conversationnel. Les différentes fonctionnalités utilisées pour créer votre application Teams vous permettent d’augmenter sa portée d’utilisation.

Il existe plusieurs façons d’étendre Teams, de sorte que chaque application est unique. Certains n’ont qu’une seule capacité, comme un webhook, tandis que d’autres ont plus d’une fonctionnalité pour donner aux utilisateurs diverses options. Par exemple, votre application peut afficher des données dans un emplacement central, c’est-à-dire **l’onglet** et présenter ces mêmes informations via une interface conversationnelle, c’est-à-dire **le bot**.

## <a name="app-capabilities"></a>Fonctionnalités de l’application

Votre Teams’application a une ou toutes les fonctionnalités de base suivantes :

* [Onglets](../tabs/what-are-tabs.md)
* [Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks et connecteurs](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

Votre application peut également tirer parti des fonctionnalités avancées, telles que [l’API microsoft Graph pour Teams](/graph/teams-concept-overview).

L’illustration suivante vous donne une idée des fonctionnalités qui fourniront les fonctionnalités que vous souhaitez dans votre application :

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Carte mentale illustrant ce que Teams d’application sont.":::

## <a name="always-consider-your-user"></a>Considérez toujours votre utilisateur

En vous familiarisez avec le développement Teams’applications, vous comprenez ses fondamentaux fondamentaux. Vous comprenez qu’il existe plus d’une façon de construire certaines fonctionnalités. Dans de tels scénarios, réfléchissez à la façon dont vous pouvez fournir une expérience plus native à votre utilisateur.
Par exemple, vous pouvez collecter l’entrée de l’utilisateur sous un formulaire construit comme onglet dans l’application. Vous pouvez également le faire à l’aide d’un module de tâches sans changer de vue et perturber le flux de travail de l’utilisateur. Il est important de choisir des points d’extension qui offrent le moins d’écart par rapport au flux de travail régulier d’un utilisateur.

## <a name="see-also"></a>Voir aussi

[Créez des applications pour Teams](../overview.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Points d'entrée de l'application Teams](../concepts/extensibility-points.md)
