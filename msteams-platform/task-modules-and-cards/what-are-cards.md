---
title: Présentation des cartes
description: Décrit les cartes et leur utilisation dans les bots, les connecteurs et les extensions de messagerie
keywords: connecteurs bots cartes messagerie
ms.openlocfilehash: 00c649a1339f05b782e03a2c0db5cba2445f66bc
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777923"
---
# <a name="cards"></a>Cartes

Une *carte est* un conteneur d’interface utilisateur (IU) pour des informations courtes ou connexes. Les cartes peuvent avoir plusieurs propriétés et pièces jointes. Les cartes peuvent inclure des boutons qui peuvent déclencher des [actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)

## <a name="adaptive-cards"></a>Cartes adaptatives

[Les cartes adaptatives](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) sont une nouvelle spécification entre produits pour les cartes des produits Microsoft, notamment Bots, Cortana, Outlook et Windows. Ils sont le type de carte recommandé pour le nouveau développement Teams. Pour obtenir des informations générales de l’équipe de cartes adaptatives, voir [Vue d’ensemble des cartes adaptatives.](/adaptive-cards) Vous pouvez utiliser des cartes adaptatives partout où vous pouvez utiliser des cartes Hero, des cartes Office365 et des cartes miniatures existantes.

En plus des cartes adaptatives, Teams prend en charge deux autres types de cartes :

* Cartes de connecteur, utilisées dans le cadre des connecteurs Office 365.
* Cartes simples de l’infrastructure du bot, telles que les cartes miniatures et hero.

Ces types de carte sont décrits plus en plus dans la référence de [carte Teams.](~/task-modules-and-cards/cards/cards-reference.md)

Teams utilise des cartes à trois endroits différents :

* Connecteurs
* Bots
* Extensions de messagerie

## <a name="adaptive-cards-and-incoming-webhooks"></a>Cartes adaptatives et webhooks entrants

> [!NOTE]
>
> ✔ Tous les éléments du schéma de la carte adaptative native, à l'exception`Action.Submit`, sont entièrement pris en charge.
>
> ✔ actions prises en charge sont [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)et [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

## <a name="cards-in-connectors"></a>Cartes dans les connecteurs

Les cartes ont d’abord été définies dans le cadre d’Outlook et d’Office 365 et sont utilisées dans le cadre des connecteurs Office 365. Comme de nombreuses applications Office 365, Teams prend en charge les connecteurs. Vous pouvez en savoir plus sur les connecteurs dans les [connecteurs Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)pour Microsoft Teams et trouver la spécification des cartes dans les connecteurs dans la référence de carte de [message actionnable.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Cartes dans les bots

Microsoft Bot Framework a étendu la spécification des cartes en ajoutant un ensemble de cartes prédéfinies que les bots peuvent utiliser dans le cadre des messages de bot. Teams prend en charge les bots à l’aide de Bot Framework, mais il prend en charge un ensemble légèrement différent de ces cartes. Des informations générales sur les cartes dans Bot Framework sont disponibles dans Ajouter des pièces jointes de carte [enrichie aux messages.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Ces cartes sont appelées *cartes simples* dans Teams.

Les bots dans Teams peuvent utiliser n’importe quel type de carte : simple, connecteur ou adaptatif. Les cartes qui sont pris en charge par les bots dans Teams sont détaillées dans la référence de [carte Teams.](~/task-modules-and-cards/cards/cards-reference.md)  

## <a name="cards-in-messaging-extensions"></a>Cartes dans les extensions de messagerie

[Les extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) peuvent également renvoyer une carte. Les extensions de messagerie peuvent utiliser n’importe quel type de carte : simple, connecteur ou adaptatif. Ces cartes sont trouvées dans la référence [de carte Teams.](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="card-reference"></a>Référence de carte

Toutes les cartes utilisées par Teams sont répertoriées dans la référence de [carte Teams.](~/task-modules-and-cards/cards/cards-reference.md) Cette référence décrit également les différences entre les cartes Bot Framework et les cartes dans Teams.
