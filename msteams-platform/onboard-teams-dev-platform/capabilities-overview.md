---
title: Présentation des fonctionnalités des applications teams
author: heath-hamilton
description: ''
ms.topic: overview
ms.author: heath-hamilton
ms.openlocfilehash: 580d75b648bde1caf0e85647c89635804c91fb70
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651970"
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
