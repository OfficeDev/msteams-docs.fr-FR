---
title: Points extensibles dans le client teams
author: clearab
description: Comprenez les points d’extensibilité disponibles pour votre application dans le client Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0624aefa7873678b1d69c1d5796340cdac69c381
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867131"
---
# <a name="extensible-points-in-the-teams-client"></a>Points extensibles dans le client teams

Une application élaborée sur la plateforme Microsoft Teams développe le client Microsoft Teams (web, mobile et bureau) avec les services web que vous hébergez. La plateforme Teams offre un ensemble complet et flexible de points d’extension, de concepts d’interface utilisateur et d’API dont vous pouvez tirer parti lors de la création de votre application. Votre application peut être aussi simple que d’incorporer votre site web existant dans un onglet pour votre équipe ou une application polyvalente complète qui engage vos utilisateurs dans toute la portée du client Teams. Vous pouvez décider d’intégrer une application existante ou de créer une expérience entièrement conçue pour Teams.

Il existe plusieurs emplacements dans lesquels le client Microsoft Teams peut être étendu pour permettre aux utilisateurs de communiquer avec votre application. Selon votre scénario, vous pouvez décider de vous concentrer sur un point d’extension unique (par exemple, un bot de conversation personnel) ou de combiner plusieurs points d’extension.

## <a name="teams-channels-and-group-chats"></a>Les équipes, canaux et conversations de groupe

Les équipes, canaux et conversations de groupe permettent à plusieurs utilisateurs de collaborer. Les applications dans ce contexte sont accessibles à tous les membres du groupe ou de la conversation, qui se concentre généralement sur l’activation de flux de travail collaboratifs supplémentaires ou la déverrouillage de nouvelles interactions sociales. Votre application a accès aux API permettant d’obtenir des informations sur les membres de la conversation, les canaux d’une équipe et les métadonnées relatives à l’équipe ou à la conversation.

Elles peuvent être étendues par les éléments suivants :

* Les [**robots de conversation**](~/bots/what-are-bots.md) interagissent avec les membres de la conversation par le biais de la conversation et répondent aux événements (par exemple, un nouveau membre ajouté ou un canal renommé). Toutes les conversations avec un robot dans ce contexte sont visibles par tous les membres du canal ou du groupe. Vous devez donc vous assurer que la conversation concerne tout le monde.

* [**Onglets configurables**](~/tabs/what-are-tabs.md) offrant une expérience Web intégrée en plein écran configurée pour le canal ou la conversation de groupe dans laquelle il est installé. Tous les membres communiquent sur la même application web partagée. Une expérience d’application d’une seule page sans état est donc représentative.

* [**Webhooks et connecteurs**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permettant aux services externes de publier des messages dans la conversation et à vos utilisateurs d’envoyer des messages à votre service. Vous pouvez tirer parti de cartes et d’actions de carte pour créer des messages enrichis et actionnables.

### <a name="personal-apps"></a>Applications personnelles

Les [applications personnelles](~/concepts/design/personal-apps.md) sont la partie de votre application de teams qui se concentre sur les interactions avec un utilisateur unique. L’expérience est propre à chaque utilisateur individuel. Cette partie de votre application peut être épinglée au rail de navigation de gauche, ce qui permet à vos utilisateurs d’y accéder en un clic.

Elles peuvent contenir les éléments suivants :

* Les [**bots de conversation**](~/bots/what-are-bots.md) ayant une conversation un-à-un avec l’utilisateur. Étant donné qu’il s’agit d’une conversation privée, si votre application doit avoir une conversation à tour de rôle ou fournir une notification qui s’applique uniquement à un seul utilisateur, il est généralement préférable de disposer de cette interaction dans une application personnelle.

* [**Onglets personnels**](~/tabs/what-are-tabs.md) offrant une expérience Web intégrée en plein écran.

## <a name="messages"></a>Messages

Les messages sont au cœur de la collaboration dans Teams. Avec une [**commande action d’extension de messagerie**](~/messaging-extensions/what-are-messaging-extensions.md), votre application peut permettre aux utilisateurs d’appeler l’API de votre application à partir d’un message, en envoyant le contenu du message à votre application à des fins de traitement ou d’action. Votre application peut répondre en présentant un formulaire (un module de tâche) à l’utilisateur pour recueillir davantage d’informations, envoyer une réponse au courrier d’origine ou envoyer un message directement à l’utilisateur.

## <a name="writing-messages"></a>Rédaction de messages

Votre application peut aider les utilisateurs à concevoir des messages plus efficaces en leur permettant de rechercher ou de prendre des mesures, dans un système externe, et d’insérer les résultats dans un format riche et structuré complet avec des boutons actionnables.

Votre application peut permettre aux utilisateurs de créer des messages plus performants de trois manières :

* [**Extension de messagerie : commandes de recherche**](~/messaging-extensions/what-are-messaging-extensions.md) leur permettant de rechercher rapidement un système externe, de prévisualiser les résultats de cette recherche, puis d’insérer le résultat dans la conversation sous forme de carte enrichie.

* [**Extension de messagerie-Link unfurling**](~/messaging-extensions/what-are-messaging-extensions.md) permet à votre application de surveiller les domaines Web qui vous intéressent. Lorsqu’une URL contenant ce domaine est collée dans la boîte de dialogue de composition de message, l’API de votre application est appelée, ce qui vous permet d’ajouter une carte enrichie au message contenant des informations supplémentaires sur l’élément qui est lié.

* [**Extension de messagerie : les commandes d’action**](~/messaging-extensions/what-are-messaging-extensions.md) présentent votre utilisateur avec un formulaire modal (un module de tâches), soumettez les résultats du formulaire à votre application, puis insérez un message directement dans la conversation ou créez une partie d’un message que l’utilisateur peut modifier avant de l’envoyer à la conversation.

## <a name="user-interface-ui-elements"></a>Éléments de l’interface utilisateur (IU)

Outre les points d’extension, la plateforme Microsoft Teams fournit des éléments d’interface utilisateur flexibles dont les applications peuvent tirer parti. Ces éléments vous permettent de créer des expériences enrichies, natives pour le client Teams.

### <a name="cards--card-actions"></a>Cartes et actions de carte

Les [cartes](~/task-modules-and-cards/what-are-cards.md) sont des conteneurs d’interface utilisateur définis par schématisées JSON, qui peuvent contenir plusieurs propriétés et pièces jointes. Elles peuvent contenir du texte mis en forme, des multimédias, des contrôles (tels que des zones de liste déroulantes et des cases d’option), ainsi que des boutons déclenchant des actions de carte. Les actions de carte peuvent envoyer des charges utiles vers l’API de votre application, ouvrir un lien, initier des flux d’authentification ou envoyer des messages vers les conversations. La plateforme Microsoft Teams prend en charge plusieurs types de cartes (cartes adaptatives, cartes Heroes, cartes miniatures, et bien plus encore). Elles peuvent être combinées dans des collections de cartes et affichées dans une liste ou un carrousel.

### <a name="task-modules"></a>Modules de tâches

Les [modules de tâches](~/task-modules-and-cards/what-are-task-modules.md) vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. À l’intérieur de la fenêtre contextuelle, vous pouvez exécuter votre propre code HTML/JavaScript personnalisé, afficher un `<iframe>` widget tel qu’une vidéo YouTube ou une vidéo Microsoft Stream, ou afficher une carte adaptative. Ils sont particulièrement utiles pour initier et effectuer des tâches, ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power BI. Une expérience contextuelle est souvent plus naturelle pour les utilisateurs qui initient et effectuent des tâches, par rapport à une expérience d’onglet ou de bot basée sur une conversation.

### <a name="deep-links"></a>Liens profonds

Votre application peut créer [des liens détaillés d’URL](~/concepts/build-and-test/deep-links.md) pour vous aider à parcourir votre utilisateur via votre application, ainsi que le client Teams. Vous pouvez créer un lien profond pour la plupart des entités au sein de Teams, et certaines (par exemples, une nouvelle demande de réunion) vous permettent de pré-peupler des informations à l’aide de chaînes de requête dans l’URL. Par exemple, votre bot de conversation peut envoyer un message vers un canal avec un lien profond à un module de tâche qui génère une carte envoyée comme message individuel à un utilisateur, qui à son tour contient un lien profond pour créer une réunion avec un utilisateur spécifique à une date et heure donnée. Utilisez des liens profonds pour vous connecter entre les différents points d’extension disponibles pour votre application, en gardant à tout moment votre utilisateur dans le contexte approprié.

### <a name="web-content-pages"></a>Pages de contenu web

Une [page de contenu Web](~/tabs/how-to/create-tab-pages/content-page.md) est une page Web que vous hébergez et qui peut être incorporée dans un onglet ou un module de tâches. Pour autoriser l’incorporation de votre page web dans un client Microsoft Teams, elle doit :

* Être hébergée sur un HTTPS.
* Pouvoir être incorporée dans un `<iframe>` par le client Teams.
* Inclure le kit de développement logiciel (SDK) de client JavaScript Microsoft Teams et appeler la méthode `initialize()` du kit de développement au chargement de la page.
