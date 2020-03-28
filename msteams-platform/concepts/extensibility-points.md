---
title: Points extensibles dans le client teams
author: clearab
description: Comprenez les points d’extensibilité disponibles pour votre application dans le client Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1db9b6828ef8a4e186160351b90c01f253df552d
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034028"
---
# <a name="extensible-points-in-the-teams-client"></a>Points extensibles dans le client teams

Une application construite sur la plateforme Microsoft teams étend le client Microsoft Teams (Web, mobile et de bureau) avec les services Web que vous hébergez. La plateforme teams fournit un ensemble complet et flexible de points d’extensibilité, de constructions d’interface utilisateur et d’API qui vous permettent de tirer parti de lors de la création de votre application. Votre application peut être aussi simple que d’incorporer votre site Web existant dans un onglet pour votre équipe, ou une application à plusieurs facettes complète qui accèdera à vos utilisateurs dans l’ensemble de la gamme du client Teams. Vous pouvez choisir d’intégrer une application existante ou de créer une nouvelle expérience entièrement intégrée à Teams.

Il existe plusieurs emplacements où le client Microsoft teams peut être étendu pour permettre aux utilisateurs d’interagir avec votre application. En fonction de votre scénario, vous pouvez choisir de vous concentrer sur un seul point d’extension (par exemple, un bot de conversation personnelle) ou de combiner plusieurs points d’extension.

## <a name="teams-channels-and-group-chats"></a>Équipes, canaux et conversations de groupe

Les équipes, les canaux et les conversations de groupe permettent à plusieurs personnes de collaborer. Les applications dans ce contexte sont accessibles à tous les membres du groupe ou de la conversation, qui se concentre généralement sur l’activation de flux de travail collaboratifs supplémentaires ou la déverrouillage de nouvelles interactions sociales. Votre application aura accès aux API lui permettant d’obtenir des informations sur les membres de la conversation, les canaux d’une équipe et les métadonnées relatives à l’équipe ou à la conversation.

Elles peuvent être étendues par les éléments suivants :

* Les [**robots de conversation**](~/bots/what-are-bots.md) interagissent avec les membres de la conversation par le biais de la conversation et répondent aux événements (par exemple, un nouveau membre ajouté ou un canal renommé). Toutes les conversations avec un bot dans ce contexte sont visibles par tous les membres du canal ou du groupe, vous devez donc vous assurer que la conversation est pertinente pour tout le monde.

* [**Onglets configurables**](~/tabs/what-are-tabs.md) offrant une expérience Web intégrée en plein écran configurée pour le canal ou la conversation de groupe dans laquelle il est installé. Tous les membres interagissent sur la même application Web partagée, de sorte qu’une expérience d’application de page unique sans état est typique.

* [**Webhooks et connecteurs**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permettant aux services externes de publier des messages dans la conversation et à vos utilisateurs d’envoyer des messages à votre service. Vous pouvez tirer parti des cartes et des actions de carte pour créer des messages riches et actionnables.

### <a name="personal-apps"></a>Applications personnelles

Les [applications personnelles](~/concepts/design/personal-apps.md) sont la partie de votre application de teams qui se concentre sur les interactions avec un utilisateur unique. L’expérience est propre à chaque utilisateur. Cette partie de votre application peut être épinglée sur le rail de navigation de gauche permettant un accès en un clic pour vos utilisateurs.

Ils peuvent contenir :

* Les [**bots de conversation**](~/bots/what-are-bots.md) ayant une conversation un-à-un avec l’utilisateur. Étant donné qu’il s’agit d’une conversation privée, si votre application doit avoir une conversation à tour de rôle ou fournir une notification qui s’applique uniquement à un seul utilisateur, il est généralement préférable de disposer de cette interaction dans une application personnelle.

* [**Onglets personnels**](~/tabs/what-are-tabs.md)offrant une expérience Web intégrée en plein écran.

## <a name="messages"></a>Messages

Les messages sont le cœur de la collaboration dans Teams. Avec une [**commande action d’extension de messagerie**](~/messaging-extensions/what-are-messaging-extensions.md), votre application peut permettre aux utilisateurs d’appeler l’API de votre application à partir d’un message, en envoyant le contenu du message à votre application à des fins de traitement ou d’action. Votre application peut répondre en présentant un formulaire (un module de tâches) à l’utilisateur pour recueillir des informations supplémentaires, envoyer une réponse au message d’origine ou envoyer un message directement à l’utilisateur.

## <a name="writing-messages"></a>Écriture de messages

Votre application peut aider les utilisateurs à concevoir des messages plus efficaces en leur permettant de rechercher ou de prendre des mesures, dans un système externe, et d’insérer les résultats dans un format riche et structuré complet avec des boutons actionnables.

Votre application peut aider les utilisateurs à créer des messages plus efficaces de trois façons :

* [**Extension de messagerie : commandes de recherche**](~/messaging-extensions/what-are-messaging-extensions.md) leur permettant de rechercher rapidement un système externe, de prévisualiser les résultats de cette recherche, puis d’insérer le résultat dans la conversation sous forme de carte enrichie.

* [**Extension de messagerie-Link unfurling**](~/messaging-extensions/what-are-messaging-extensions.md) permet à votre application de surveiller les domaines Web qui vous intéressent. Lorsqu’une URL contenant ce domaine est collée dans la boîte de message de composition, l’API de votre application est appelée, ce qui vous permet d’ajouter une carte enrichie au message avec des informations supplémentaires sur l’élément lié.

* [**Extension de messagerie : les commandes d’action**](~/messaging-extensions/what-are-messaging-extensions.md) présentent votre utilisateur avec un formulaire modal (un module de tâches), soumettez les résultats du formulaire à votre application, puis insérez un message directement dans la conversation ou créez une partie d’un message que l’utilisateur peut modifier avant de l’envoyer à la conversation.

## <a name="user-interface-ui-elements"></a>Éléments de l’interface utilisateur (IU)

Outre les points d’extensibilité, la plateforme Microsoft teams fournit des éléments d’interface utilisateur souples pour que les applications tirent parti de. Ces éléments vous permettent de créer des expériences enrichies qui semblent natives pour le client Teams.

### <a name="cards--card-actions"></a>Cartes & actions de carte

Les [cartes](~/task-modules-and-cards/what-are-cards.md) sont des conteneurs d’interface utilisateur définis par schématisées JSON, qui peuvent contenir plusieurs propriétés et pièces jointes. Ils peuvent contenir du texte mis en forme, des médias, des contrôles (par exemple, des zones de liste déroulante et des cases d’option), ainsi que des boutons qui déclenchent des actions de carte. Les actions de carte peuvent envoyer des charges utiles à l’API de votre application, ouvrir un lien, initier des flux d’authentification ou envoyer des messages à des conversations. La plateforme Microsoft teams prend en charge plusieurs types de cartes, notamment des cartes adaptatives, des cartes héros, des cartes miniatures, etc. Elles peuvent être combinées en collections de cartes et affichées dans une liste ou un carrousel.

### <a name="task-modules"></a>Modules de tâches

Les [modules de tâches](~/task-modules-and-cards/what-are-task-modules.md) vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. À l’intérieur de la fenêtre contextuelle, vous pouvez exécuter votre propre code HTML/ `<iframe>` JavaScript personnalisé, afficher un widget tel qu’une vidéo YouTube ou une vidéo Microsoft Stream, ou afficher une carte adaptative. Elles sont particulièrement utiles pour lancer et effectuer des tâches ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power BI. Une expérience contextuelle est souvent plus naturelle pour les utilisateurs qui initient et effectuent des tâches par rapport à un onglet ou à une expérience de robot basée sur une conversation.

### <a name="deep-links"></a>Liens profonds

Votre application peut créer [des liens détaillés d’URL](~/concepts/build-and-test/deep-links.md) pour vous aider à parcourir votre utilisateur via votre application, ainsi que le client Teams. Vous pouvez créer un deeplink pour la plupart des entités dans Teams, et certains (comme une nouvelle demande de réunion) vous permettent de pré-remplir des informations à l’aide de chaînes de requête dans l’URL. Par exemple, votre robot de conversation peut envoyer un message à un canal avec un deeplink à un module de tâches qui entraîne l’envoi d’une carte en tant que message un-à-un à un utilisateur, qui contient à son tour un deeplink pour créer une réunion avec un utilisateur spécifique à une date/heure donnée. Utilisez des liens détaillés pour vous connecter à travers les différents points d’extension disponibles pour votre application, en gardant votre utilisateur dans le contexte approprié en permanence.

### <a name="web-content-pages"></a>Pages de contenu Web

Une [page de contenu Web](~/tabs/how-to/create-tab-pages/content-page.md) est une page Web que vous hébergez et qui peut être incorporée dans un onglet ou un module de tâches. Pour autoriser l’incorporation de votre page Web dans un client Microsoft Teams, vous devez :

* Être hébergé sur un protocole HTTPs.
* Pouvoir être incorporée dans un `<iframe>` par le client Teams.
* Incluez le kit de développement logiciel (SDK) JavaScript client Microsoft `initialize()` teams et appelez la méthode du kit de développement logiciel sur le chargement de la page.
