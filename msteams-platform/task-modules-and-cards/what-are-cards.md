---
title: Cartes
description: Décrit les cartes et leur utilisation dans des bots, des connecteurs et des extensions de messagerie
ms.localizationpriority: high
keywords: connecteurs bots cartes messagerie
ms.topic: overview
ms.openlocfilehash: fc18c1048ec019a5532b50babff8e2d419343c1f
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756477"
---
# <a name="cards"></a>Cartes

Une carte est un conteneur d’interface utilisateur (IU) pour des informations courtes ou connexes. Les cartes peuvent avoir plusieurs propriétés et pièces jointes et inclure des boutons qui déclenchent des [actions de carte](~/task-modules-and-cards/cards/cards-actions.md). L’utilisation de cartes vous permet d’organiser des informations en groupes et de permettre aux utilisateurs d’interagir avec des parties spécifiques de celles-ci.

Les bots pour Teams prennent en charge les types de cartes suivants :

* Carte adaptative
* Carte Hero
* Carte de liste
* Carte Connecteur Office 365
* Carte de réception
* Carte de signature
* Carte miniature
* Collections de cartes

Vous pouvez ajouter une mise en forme de texte enrichi à vos cartes à l’aide de Markdown ou HTML, suivant le type de carte. Les cartes sont utilisées par les bots et les extensions de messagerie dans Microsoft Teams. Elles ajoutent et répondent aux actions de ces cartes, `openUrl`, `messageBack`, `imBack`, `invoke` et `signin`.

Teams utilise des cartes dans trois endroits différents :

* Connecteurs
* Bots
* Extensions de messages

## <a name="cards-in-connectors"></a>Cartes dans les connecteurs

Les cartes ont d’abord été définies comme partie d’Outlook et d’Office 365 et sont désormais utilisées dans le cadre des Connecteurs Office 365. Comme de nombreuses applications Office 365, Teams prend en charge les connecteurs. Pour obtenir plus d’informations, voir [créer des connecteurs Office 365](../webhooks-and-connectors/how-to/connectors-creating.md). Vous trouverez la spécification des cartes dans les connecteurs dans la [référence de carte de message actionnable](/outlook/actionable-messages/card-reference).

## <a name="cards-in-bots"></a>Cartes dans les bots

Microsoft Bot Framework étend la spécification des cartes en ajoutant un ensemble de cartes prédéfinies que les bots peuvent utiliser dans le cadre des messages de bot. Teams prend en charge les bots en utilisant Bot Framework, mais l’application prend en charge un autre jeu de ces cartes. Des informations générales sur les cartes dans Bot Framework sont disponibles dans [Ajout de pièces jointes de carte enrichie aux messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards). Ces cartes sont appelées cartes simples dans Teams.

Les bots dans Teams peuvent utiliser des cartes simples, des cartes de connecteur ou des Cartes adaptatives. [Les types de cartes](~/task-modules-and-cards/cards/cards-reference.md) fournissent des informations sur les cartes et sont pris en charge par les bots dans Teams.

## <a name="cards-in-message-extensions"></a>Cartes dans les extensions de message

Les [extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) peuvent également renvoyer une carte. Les extensions de messagerie peuvent utiliser des cartes simples, des cartes de connecteur ou des Cartes adaptatives. Vous trouverez ces cartes dans les [types de cartes](~/task-modules-and-cards/cards/cards-reference.md).

## <a name="types-of-cards"></a>Types de cartes

Toutes les cartes utilisées par Teams sont répertoriées dans les [types de cartes](~/task-modules-and-cards/cards/cards-reference.md). Cette référence décrit également les différences entre les cartes Bot Framework et les cartes dans Teams.

## <a name="adaptive-cards"></a>Cartes adaptatives

Les [Cartes adaptatives](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) sont une nouvelle spécification inter-produits pour les cartes des produits Microsoft, notamment les bots, Cortana, Outlook et Windows. Elles constituent le type de carte recommandé pour les nouveaux développements Teams. Pour obtenir des informations générales sur l’équipe des Cartes adaptatives, voir [Vue d’ensemble du format Cartes adaptatives](/adaptive-cards). Vous pouvez utiliser des Cartes adaptatives partout où vous utilisez des cartes Hero, des cartes Office 365 et des cartes miniatures existantes.

Outre les Cartes adaptatives, Teams prend en charge deux autres types de cartes :

* Cartes de connecteur : utilisées dans le cadre des Connecteurs Office 365.
* Cartes simples : utilisées à partir de Bot Framework, telles que les cartes miniatures et Hero.

### <a name="people-picker-in-adaptive-cards"></a>Sélecteur de personnes dans les Cartes adaptatives

Le [Sélecteur de personnes](cards/people-picker.md#people-picker-in-adaptive-cards) ajouté en tant que contrôle d’entrée dans les Cartes adaptatives permet la recherche et la sélection de personnes. Vous pouvez l’utiliser dans les conversations, les canaux, les modules de tâche et les onglets. Les clients mobiles et de bureau prennent en charge le Sélecteur de personnes, offrant une expérience de saisie inline.

### <a name="type-ahead-search-in-adaptive-cards"></a>Recherche en saisie semi-automatique dans les Cartes adaptatives  

La recherche en saisie semi-automatique en tant que contrôle d’entrée dans les Cartes adaptatives permet une expérience de [recherche dynamique](~/task-modules-and-cards/cards/dynamic-search.md) à partir d’un jeu de données chargé de manière dynamique. Elle permet également aux utilisateurs d’effectuer une recherche statique en saisie semi-automatique dans une liste avec un nombre de choix limité. Les clients mobiles et de bureau prennent en charge l’expérience de recherche dynamique en saisie semi-automatique.

### <a name="adaptive-cards-and-incoming-webhooks"></a>Cartes adaptatives et Webhooks entrants

> [!NOTE]
>
> * Tous les éléments de schéma de Carte adaptative native, à l’exception de `Action.Submit`, sont entièrement pris en charge.
> * Les actions prises en charge sont [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), et [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

Les Cartes adaptatives avec Webhooks entrants vous permettent d’utiliser les fonctionnalités enrichies et flexibles des Cartes adaptatives. Elles envoient des données à l’aide des Webhooks entrants dans Teams à partir de leur service web.

## <a name="support-for-azure-ad-object-id-and-upn-in-user-mention"></a>Support pour Azure AD Object ID et UPN dans la mention de l'utilisateur

Les bots avec Cartes adaptatives prennent en charge les ID de mention utilisateur, tels que l’ID d’objet Microsoft Azure Active Directory (Azure AD) et le nom d’utilisateur principal (UPN) en plus des ID existants. Les webhooks entrants commencent à prendre en charge la mention utilisateur dans les cartes adaptatives avec l’ID Azure AD’objet et l’UPN.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Types de cartes](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="see-also"></a>Voir aussi

* [Mettre en forme des cartes dans Microsoft Teams](~/task-modules-and-cards/cards/cards-format.md)
* [Conception de Cartes adaptatives](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Cartes adaptatives dans les bots](../bots/how-to/conversations/conversation-messages.md#adaptive-cards)
