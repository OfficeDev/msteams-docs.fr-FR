---
title: Présentation des fonctionnalités des applications teams
author: heath-hamilton
description: Explications sur les fonctionnalités des applications teams
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e7a6fe61fa5c74547ce20cc895afdd044f35e512
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210277"
---
# <a name="understanding-teams-app-capabilities"></a>Présentation des fonctionnalités des applications teams

Les *fonctionnalités* sont les points d’extension pour la création d’applications sur la plateforme Microsoft Teams.

Il existe plusieurs façons d’étendre Teams, de sorte que chaque application est unique : une seule capacité (par exemple, un webhook), tandis que d’autres ont quelques possibilités pour les utilisateurs. Par exemple, votre application peut afficher les données dans un emplacement central (onglet) et présenter ces mêmes informations par le biais d’une interface de conversation (bot).

Votre application teams peut avoir une ou toutes les fonctionnalités de base suivantes :

* [Onglets](../tabs/what-are-tabs.md)
* [Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks et connecteurs](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

Votre application peut également tirer parti de fonctionnalités avancées, telles que l' [API Microsoft Graph pour teams](https://docs.microsoft.com/graph/teams-concept-overview).

Reportez-vous à l’illustration suivante pour obtenir une idée des fonctionnalités qui fourniraient les fonctionnalités souhaitées dans votre application.

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Diagramme d’idées illustrant les fonctionnalités des applications Teams.":::

## <a name="doing-whats-best-for-your-users"></a>Faire ce qui convient le mieux pour vos utilisateurs

Lorsque vous vous familiarisez avec le développement d’applications Teams, vous commencerez à comprendre ses subtilités. Il existe plusieurs façons de créer certaines fonctionnalités (par exemple, la collecte des données entrées par l’utilisateur). Par exemple, vous pouvez incorporer un formulaire Web dans un onglet à l’aide d’un `<iframe>` . Vous pouvez également effectuer cette opération dans un onglet à l’aide d’un module de tâches, une convention de l’interface utilisateur Teams, pour une expérience plus Native que vos utilisateurs préféreront.

Le choix des fonctionnalités et de la conception appropriées ne revient pas à [comprendre les cas d’utilisation de votre public](../concepts/design/understand-use-cases.md).
