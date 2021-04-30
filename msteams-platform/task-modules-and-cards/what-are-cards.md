---
title: Présentation des cartes
description: Décrit les cartes et leur utilisation dans les bots, les connecteurs et les extensions de messagerie
localization_priority: Normal
ms.topic: conceptual
keywords: connecteurs bots cartes messagerie
ms.openlocfilehash: 77dcbb7d0472b584623e878df956a6165296f4cf
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088751"
---
# <a name="cards"></a>Cartes

Une *carte* est un conteneur d'interface utilisateur (IU) pour des informations courtes ou connexes. Les cartes peuvent avoir plusieurs propriétés et pièces jointes. Les cartes peuvent inclure des boutons qui peuvent déclencher des [actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)

## <a name="adaptive-cards"></a>Cartes adaptatives

[Les cartes](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) adaptatives sont une nouvelle spécification entre produits pour les cartes des produits Microsoft, notamment bots, Cortana, Outlook et Windows. Ils sont le type de carte recommandé pour les nouveaux Teams développement. Pour obtenir des informations générales de l'équipe de cartes adaptatives, voir [Vue d'ensemble des cartes adaptatives.](/adaptive-cards) Vous pouvez utiliser des cartes adaptatives partout où vous pouvez utiliser des cartes Hero, des cartes Office365 et des cartes miniatures existantes.

Outre les cartes adaptatives, Teams prend en charge deux autres types de cartes :

* Cartes de connecteur, utilisées dans le cadre Office 365 connecteurs.
* Cartes simples de l'infrastructure du bot, telles que les cartes miniatures et hero.

Ces types de carte sont décrits plus en Teams [référence de carte.](~/task-modules-and-cards/cards/cards-reference.md)

Teams utilise des cartes à trois endroits différents :

* Connecteurs
* Bots
* Extensions de messagerie

## <a name="adaptive-cards-and-incoming-webhooks"></a>Cartes adaptatives et webhooks entrants

> [!NOTE]
>
> ✔ Tous les éléments du schéma de la carte adaptative native, à l'exception`Action.Submit`, sont entièrement pris en charge.
>
> ✔ actions prises en charge sont [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard,**](https://adaptivecards.io/explorer/Action.ShowCard.html) [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) [**etAction.Execute**](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

## <a name="cards-in-connectors"></a>Cartes dans les connecteurs

Les cartes ont d'abord été définies dans Outlook et Office 365 et sont utilisées dans le cadre des connecteurs Office 365 de connexion. Comme de Office 365 applications, Teams prend en charge les connecteurs. Vous pouvez en savoir plus sur les connecteurs dans [Office 365 connecteurs](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)pour Microsoft Teams et trouver la spécification pour les cartes dans les connecteurs dans la référence de carte de [message actionnable.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Cartes dans les bots

Le Microsoft Bot Framework étendu la spécification des cartes en ajoutant un ensemble de cartes prédéfinës que les bots peuvent utiliser dans le cadre des messages de bot. Teams prend en charge les bots à l'aide de Bot Framework, mais il prend en charge un ensemble légèrement différent de ces cartes. Des informations générales sur les cartes dans Bot Framework sont disponibles dans Ajouter des pièces jointes de carte [enrichie aux messages.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Ces cartes sont appelées *cartes simples* dans Teams.

Les bots Teams peuvent utiliser n'importe quel type de carte : simple, connecteur ou adaptatif. Les cartes qui sont pris en charge par les bots dans Teams sont détaillées dans Teams [référence de carte.](~/task-modules-and-cards/cards/cards-reference.md)  

## <a name="cards-in-messaging-extensions"></a>Cartes dans les extensions de messagerie

[Les extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) peuvent également renvoyer une carte. Les extensions de messagerie peuvent utiliser n'importe quel type de carte : simple, connecteur ou adaptatif. Ces cartes sont trouvées dans la [Teams de carte de visite.](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="card-reference"></a>Référence de carte

Toutes les cartes utilisées par Teams sont répertoriées dans la Teams [de carte de visite.](~/task-modules-and-cards/cards/cards-reference.md) Cette référence décrit également les différences entre les cartes Bot Framework et les cartes Teams.
