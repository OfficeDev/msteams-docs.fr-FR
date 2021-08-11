---
title: Cartes
description: Décrit les cartes et leur utilisation dans les bots, les connecteurs et les extensions de messagerie
localization_priority: Normal
keywords: connecteurs bots cartes messagerie
ms.topic: overview
ms.openlocfilehash: 5fce5983e5197bfde37d2c92d427e8135b294d422eb019ef207eeb7f0e5be9f3
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706631"
---
# <a name="cards"></a>Cartes

Une carte est un conteneur d’interface utilisateur (IU) pour des informations courtes ou connexes. Les cartes peuvent avoir plusieurs propriétés et pièces jointes et peuvent inclure des boutons, qui déclenchent des [actions de carte.](~/task-modules-and-cards/cards/cards-actions.md) À l’aide de cartes, vous pouvez organiser les informations en groupes et donner aux utilisateurs la possibilité d’interagir avec des parties spécifiques des informations.

Les bots pour Teams les types de cartes suivants : carte adaptative, carte hero, carte de liste, carte de connecteur Office 365, carte de reçu, carte de connexion, carte miniature et collections de cartes. Vous pouvez ajouter une mise en forme de texte enrichi à vos cartes à l’aide de Markdown ou html, en fonction du type de carte. Cartes utilisées par les bots et extensions de messagerie dans Microsoft Teams, ajouter et répondre à ces actions de carte, `openUrl` `messageBack` , , et `imBack` `invoke` `signin` .

Teams utilise des cartes à trois endroits différents :

* Connecteurs
* Bots
* Extensions de messagerie

## <a name="cards-in-connectors"></a>Cartes dans les connecteurs

Les cartes ont d’abord été définies dans Outlook et Office 365 et sont désormais utilisées dans le cadre des connecteurs Office 365 de connexion. Comme de nombreuses applications Office 365, Teams prend en charge les connecteurs. Pour plus d’informations, [voir Office 365 Connectors for Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md). Vous pouvez trouver la spécification pour les cartes dans les connecteurs dans la référence [de carte de message actionnable.](/outlook/actionable-messages/card-reference)

## <a name="cards-in-bots"></a>Cartes dans les bots

Le Microsoft Bot Framework étend la spécification des cartes en ajoutant un ensemble de cartes prédéfinës que les bots peuvent utiliser dans le cadre des messages de bot. Teams prend en charge les bots à l’aide de Bot Framework, mais il prend en charge un autre ensemble de ces cartes. Des informations générales sur les cartes dans Bot Framework sont disponibles dans l’ajout de pièces jointes de carte [enrichie aux messages.](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) Ces cartes sont appelées cartes simples dans Teams.

Les bots dans Teams peuvent utiliser des cartes simples, des cartes de connecteur ou des cartes adaptatives. [Les types de cartes fournissent](~/task-modules-and-cards/cards/cards-reference.md) des informations sur les cartes, pris en charge par les bots Teams.

## <a name="cards-in-messaging-extensions"></a>Cartes dans les extensions de messagerie

[Les extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) peuvent également renvoyer une carte. Les extensions de messagerie peuvent utiliser des cartes simples, des cartes de connecteur ou des cartes adaptatives. Ces cartes sont trouvées dans [les types de cartes.](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="types-of-cards"></a>Types de cartes

Toutes les cartes utilisées par Teams sont répertoriées dans les [types de cartes.](~/task-modules-and-cards/cards/cards-reference.md) Cette référence décrit également les différences entre les cartes Bot Framework et les cartes Teams.

## <a name="adaptive-cards"></a>Cartes adaptatives

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

[Les cartes](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) adaptatives sont une nouvelle spécification de produit croisé pour les cartes dans les produits Microsoft, y compris les bots, Cortana, Outlook et Windows. Ils sont le type de carte recommandé pour les nouveaux Teams développement. Pour obtenir des informations générales sur l’équipe des cartes adaptatives, voir [vue d’ensemble des cartes adaptatives.](/adaptive-cards) Vous pouvez utiliser des cartes adaptatives partout où vous utilisez des cartes Hero, des cartes Office 365 et des cartes miniatures existantes.

Outre les cartes adaptatives, Teams prend en charge deux autres types de cartes :

* Cartes de connecteur : utilisées dans le cadre Office 365 connecteurs.
* Cartes simples : utilisées à partir de Bot Framework, telles que les cartes miniatures et hero.

### <a name="adaptive-cards-and-incoming-webhooks"></a>Cartes adaptatives et webhooks entrants

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * Tous les éléments de schéma de carte adaptative native, à l’exception `Action.Submit` de , sont entièrement pris en charge.
> * Les actions prises en charge sont [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard,**](https://adaptivecards.io/explorer/Action.ShowCard.html) [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)et [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Les cartes adaptatives avec les webhooks entrants vous permettent d’utiliser les fonctionnalités riches et flexibles des cartes adaptatives. Il envoie des données à l’aide de webhooks entrants Teams partir de leur service web.

## <a name="see-also"></a>Voir aussi

* [Formater des cartes dans Teams](~/task-modules-and-cards/cards/cards-format.md)
* [Concevoir des cartes adaptatives](~/task-modules-and-cards/cards/design-effective-cards.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Types de cartes](~/task-modules-and-cards/cards/cards-reference.md)