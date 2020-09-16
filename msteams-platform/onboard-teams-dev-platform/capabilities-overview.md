---
title: Présentation des fonctionnalités des applications teams
author: heath-hamilton
description: vue d’ensemble des fonctionnalités de teams et des points d’extension
ms.topic: overview
ms.author: v-heha
ms.openlocfilehash: f83cf0240b32d35028135b48e7d4c56b939777a9
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819080"
---
# <a name="understanding-teams-app-capabilities"></a>Présentation des fonctionnalités des applications teams

Les *fonctionnalités* sont les points d’extension pour la création d’applications sur la plateforme Microsoft Teams.

Il existe plusieurs façons d’étendre le client teams : toutes les applications sont uniques : une seule capacité (par exemple, un webhook), tandis que d’autres ont quelques possibilités pour les utilisateurs. Par exemple, votre application peut afficher les données dans un emplacement central (onglet) et présenter ces mêmes informations par le biais d’une interface de conversation (bot).

Votre application teams peut avoir une ou toutes les fonctionnalités de base suivantes :

* [Onglets](../tabs/what-are-tabs.md)
* [Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)
* [Webhooks et connecteurs](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [Bots](../bots/what-are-bots.md)

Votre application peut également tirer parti de fonctionnalités avancées, telles que l' [API REST Microsoft Graph](../graph-api/rsc/resource-specific-consent.md).

Reportez-vous à l’illustration suivante pour obtenir une idée des fonctionnalités qui fourniraient les fonctionnalités souhaitées dans votre application.

![Diagramme d’idées illustrant les fonctionnalités des applications teams](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a>Faire ce qui convient le mieux pour vos utilisateurs

Lorsque vous vous familiarisez avec le développement d’applications Teams, vous commencerez à comprendre ses subtilités. Il existe plusieurs façons de créer certaines fonctionnalités (par exemple, la collecte des données entrées par l’utilisateur). Par exemple, vous pouvez incorporer un formulaire Web dans un onglet à l’aide d’un `<iframe>` . Vous pouvez également effectuer cette opération dans un onglet à l’aide d’un module de tâches, une convention de l’interface utilisateur Teams, pour une expérience plus Native que vos utilisateurs préféreront.

Le choix de la combinaison appropriée de fonctionnalités et de conventions de l’interface utilisateur, des contrôles et des éléments ne revient pas à [comprendre les cas d’utilisation de votre audience](../concepts/design/understand-use-cases.md).

## <a name="learn-more"></a>En savoir plus

* [Démarrer la planification de votre application](../concepts/extensibility-points.md)
