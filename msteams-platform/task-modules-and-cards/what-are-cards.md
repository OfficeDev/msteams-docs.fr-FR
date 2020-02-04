---
title: Présentation des cartes
description: Décrit les cartes et leur utilisation dans les robots, les connecteurs et les extensions de messagerie
keywords: messages de la fiche robots de connecteurs
ms.openlocfilehash: a260313c6e9442ce7bd76524e41e6465617bafb5
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673738"
---
# <a name="cards"></a>Fiche

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

## <a name="cards-in-connectors"></a>Cartes dans les connecteurs

Les cartes ont d’abord été définies dans le cadre d’Outlook et d’Office 365, et sont utilisées dans le cadre des connecteurs Office 365. À l’instar de nombreuses applications Office 365, teams prend en charge les connecteurs. Pour en savoir plus sur les connecteurs dans [les connecteurs Office 365 pour Microsoft teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), consultez la spécification relative aux cartes dans les connecteurs en [référence aux cartes de messages](/outlook/actionable-messages/card-reference)intégrant des actions.

## <a name="cards-in-bots"></a>Cartes dans les robots

Microsoft bot Framework a étendu la spécification des cartes en ajoutant un ensemble de cartes prédéfinies que les robots pourraient utiliser dans le cadre de messages de robots. Teams prend en charge les robots à l’aide de l’infrastructure bot, mais il prend en charge un ensemble légèrement différent de ces cartes. Vous trouverez des informations générales sur les cartes dans l’infrastructure de robots dans [Ajouter des pièces jointes aux messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards). Ces cartes sont appelées *cartes simples* dans Teams.

Dans Teams, les robots peuvent utiliser n’importe quel type de carte : simple, connecteur ou adaptatif. Les cartes prises en charge par les robots dans teams sont détaillées dans la [référence des cartes de visite](~/task-modules-and-cards/cards/cards-reference.md).  

## <a name="cards-in-messaging-extensions"></a>Cartes dans les extensions de messagerie

Les [extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) peuvent également renvoyer une carte. Les extensions de messagerie peuvent utiliser n’importe quel type de carte : simple, connecteur ou adaptatif. Ces cartes se trouvent dans la [référence de la carte teams](~/task-modules-and-cards/cards/cards-reference.md).

## <a name="card-reference"></a>Référence de carte

Toutes les cartes utilisées par teams sont répertoriées dans la référence de la [carte teams](~/task-modules-and-cards/cards/cards-reference.md). Cette référence décrit également les différences entre les cartes et les cartes de robot dans Teams.
