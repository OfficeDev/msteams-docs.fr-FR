---
title: Comprendre les fonctionnalités de l’application Teams
author: heath-hamilton
description: Fonctionnalités de l’application Teams expliquées
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034704"
---
# <a name="understanding-teams-app-capabilities"></a>Comprendre les fonctionnalités de l’application Teams

*Les fonctionnalités sont* les points d’extension pour la création d’applications sur la plateforme Microsoft Teams.

Il existe plusieurs façons d’étendre Teams, de sorte que chaque application est unique : certaines n’ont qu’une seule fonctionnalité (par exemple, un webhook), tandis que d’autres ont quelques-unes pour donner des options aux utilisateurs. Par exemple, votre application peut afficher des données dans un emplacement central (onglet) et présenter ces mêmes informations via une interface de conversation (bot).

Votre application Teams a une ou toutes les fonctionnalités principales suivantes :

* [Onglets](../tabs/what-are-tabs.md)
* [Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks et connecteurs](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

Votre application peut également tirer parti des fonctionnalités avancées, telles que [l’API Microsoft Graph pour Teams.](https://docs.microsoft.com/graph/teams-concept-overview)

Consultez l’illustration suivante pour vous faire une idée des fonctionnalités qui offriraient les fonctionnalités de votre application.

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Carte d’esprit illustrant les fonctionnalités de l’application Teams.":::

## <a name="doing-whats-best-for-your-users"></a>Faire ce qui est le mieux pour vos utilisateurs

À mesure que vous vous familiariserez avec le développement d’applications Teams, vous commencerez à comprendre ses subtiles. Il existe plusieurs façons de créer certaines fonctionnalités (telles que la collecte d’entrées utilisateur). Par exemple, vous pouvez incorporer un formulaire web dans un onglet à l’aide d’un `<iframe>` . Vous pouvez également le faire dans un onglet à l’aide d’un module de tâche, une convention d’interface utilisateur Teams, pour une expérience plus native que vos utilisateurs préfèrent.

Le choix des fonctionnalités et de la conception qui vous sont nécessaires revient à comprendre d’abord les cas [d’utilisation de votre public.](../concepts/design/understand-use-cases.md)
