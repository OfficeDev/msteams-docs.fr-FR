---
title: Présentation des cartes
description: Décrit les cartes et leur utilisation dans les robots, les connecteurs et les extensions de messagerie
keywords: messages de la fiche robots de connecteurs
ms.openlocfilehash: 6d850f83183f12fa0c228a7a89b23e58f523e15b
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651655"
---
# <a name="cards"></a>Cartes

Une *carte* est un conteneur d’interface utilisateur (IU) pour des informations courtes ou associées. Les cartes peuvent avoir plusieurs propriétés et pièces jointes. Les cartes peuvent inclure des boutons qui peuvent déclencher des [actions de carte](~/task-modules-and-cards/cards/cards-actions.md).

## <a name="adaptive-cards"></a>Cartes adaptatives

Les [cartes adaptatives](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) sont une nouvelle spécification de produit croisé pour les cartes dans les produits Microsoft, notamment les robots, Cortana, Outlook et Windows. Il s’agit du type de carte recommandé pour le développement de nouvelles équipes. Pour obtenir des informations générales de l’équipe cartes adaptatives, consultez la rubrique [vue d’ensemble des cartes](/adaptive-cards). Vous pouvez utiliser des cartes adaptatives partout où vous pouvez utiliser des cartes héros existantes, des cartes Office 365 et des cartes miniatures.

En plus des cartes adaptatives, teams prend en charge deux autres types de cartes :

* Les cartes de connecteur, utilisées dans le cadre des connecteurs Office 365.
* Cartes simples de l’infrastructure de robot, telles que les cartes miniature et héros.

Ces types de carte sont décrits plus en détail dans la référence de la [carte teams](~/task-modules-and-cards/cards/cards-reference.md).

Teams utilise les cartes de trois façons différentes :

* Connecteurs
* Bots
* Extensions de messagerie

## <a name="adaptive-cards-and-incoming-webhooks"></a>Cartes adaptatives et webhooks entrants

> [!NOTE]
> Les cartes adaptatives sont prises en charge dans les webhooks entrants dans le cadre du [programme public developer preview](../resources/dev-preview/developer-preview-intro.md). Les aperçus publics sont disponibles pour l’accès anticipé et les commentaires. Bien que la publication soit stable et qu’elle ait subi des tests approfondis, elle n’est pas destinée à être utilisée en production.
>
> ✔ Au sein de l’aperçu du développeur, tous les éléments de schéma de carte adaptative native, à l’exception `Action.Submit` de, sont entièrement pris en charge.
>
> ✔ Les actions prises en charge sont [**action. OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**action. ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)et [**action. ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

## <a name="cards-in-connectors"></a>Cartes dans les connecteurs

Les cartes ont d’abord été définies dans le cadre d’Outlook et d’Office 365, et sont utilisées dans le cadre des connecteurs Office 365. À l’instar de nombreuses applications Office 365, teams prend en charge les connecteurs. Pour en savoir plus sur les connecteurs dans [les connecteurs Office 365 pour Microsoft teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), consultez la spécification relative aux cartes dans les connecteurs en [référence aux cartes de messages](/outlook/actionable-messages/card-reference)intégrant des actions.

## <a name="cards-in-bots"></a>Cartes dans les robots

Microsoft bot Framework a étendu la spécification des cartes en ajoutant un ensemble de cartes prédéfinies que les robots pourraient utiliser dans le cadre de messages de robots. Teams prend en charge les robots à l’aide de l’infrastructure bot, mais il prend en charge un ensemble légèrement différent de ces cartes. Vous trouverez des informations générales sur les cartes dans l’infrastructure de robots dans [Ajouter des pièces jointes aux messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards). Ces cartes sont appelées *cartes simples* dans Teams.

Dans Teams, les robots peuvent utiliser n’importe quel type de carte : simple, connecteur ou adaptatif. Les cartes prises en charge par les robots dans teams sont détaillées dans la [référence des cartes de visite](~/task-modules-and-cards/cards/cards-reference.md).  

## <a name="cards-in-messaging-extensions"></a>Cartes dans les extensions de messagerie

Les [extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) peuvent également renvoyer une carte. Les extensions de messagerie peuvent utiliser n’importe quel type de carte : simple, connecteur ou adaptatif. Ces cartes se trouvent dans la [référence de la carte teams](~/task-modules-and-cards/cards/cards-reference.md).

## <a name="card-reference"></a>Référence de carte

Toutes les cartes utilisées par teams sont répertoriées dans la référence de la [carte teams](~/task-modules-and-cards/cards/cards-reference.md). Cette référence décrit également les différences entre les cartes et les cartes de robot dans Teams.
