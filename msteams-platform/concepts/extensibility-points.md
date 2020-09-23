---
title: Points d’entrée pour les applications teams
author: heath-hamilton
description: Décrit comment et où les personnes utilisent votre application dans Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 1c68467177fc440993f059133f049f18785374b7
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209780"
---
# <a name="entry-points-for-teams-apps"></a>Points d’entrée pour les applications teams

La plateforme teams fournit un ensemble flexible de points d’entrée où les utilisateurs peuvent découvrir et utiliser votre application. Votre application peut être aussi simple que d’incorporer un site Web existant dans un onglet personnel ou dans une application à plusieurs facettes avec laquelle les utilisateurs interagissent sur plusieurs points d’entrée.

Les applications les plus performantes se sentent natives à Teams, il est donc important de planifier soigneusement les points d’entrée de votre application.

## <a name="teams-channels-and-group-chats"></a>Équipes, canaux et conversations de groupe

Les équipes, les canaux et les conversations de groupe sont des espaces de collaboration. Les applications qui utilisent ces points d’entrée sont accessibles à tous les membres et se concentrent généralement sur des flux de travail supplémentaires ou déverrouillent de nouvelles interactions sociales.

Voici comment les fonctionnalités des applications teams sont couramment utilisées dans les contextes collaboratifs :

* Les [**onglets**](~/tabs/what-are-tabs.md) fournissent une expérience Web intégrée en plein écran configurée pour l’équipe, le canal ou la conversation de groupe. Tous les membres interagissent avec le même contenu Web, de sorte qu’une expérience d’application de page unique sans état est typique.

* Les [**extensions de messagerie**](~/messaging-extensions/what-are-messaging-extensions.md) sont des raccourcis permettant d’insérer du contenu externe dans une conversation ou de prendre des mesures sur les messages sans quitter Teams. Link unfurling fournit un contenu enrichi lors du partage de contenu à partir d’une URL commune.

* Les [**robots**](~/bots/what-are-bots.md) interagissent avec les membres de la conversation via une conversation et répondent aux événements (par exemple, l’ajout d’un nouveau membre ou le changement de nom d’un canal). Les conversations avec un bot dans ces contextes sont visibles par tous les membres de l’équipe, du canal ou du groupe, de sorte que les conversations de bot doivent être pertinentes pour tout le monde.

* Les [**connecteurs et les webhooks**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permettent à un service externe de publier des messages dans une conversation et à des utilisateurs d’envoyer des messages à un service.

* [**API REST Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) pour obtenir des données sur des équipes, des canaux et des conversations de groupe afin d’automatiser et de gérer les processus de teams.

## <a name="personal-apps"></a>Applications personnelles

Les [applications personnelles](~/concepts/design/personal-apps.md) se concentrent sur les interactions avec un seul utilisateur. L’expérience dans ce contexte est propre à chaque utilisateur. Les utilisateurs peuvent épingler des applications personnelles sur le rail de navigation gauche pour un accès rapide.

Voici comment les fonctionnalités teams sont couramment utilisées dans les contextes personnels :

* Les [**robots**](~/bots/what-are-bots.md) ont des conversations un à un avec un utilisateur. Les robots qui nécessitent des conversations à tour de rôle ou qui fournissent des notifications propres à un utilisateur spécifique sont mieux adaptés à des contextes personnels.

* Les [**onglets**](~/tabs/what-are-tabs.md) fournissent une expérience Web incorporée en plein écran qui est significative pour les utilisateurs individuels.

## <a name="ui-components"></a>Composants de l’interface utilisateur

Les applications présentent généralement un ou plusieurs composants d’interface utilisateur standard de teams. La création de votre application à l’aide de ces composants conduit à des expériences enrichies qui semblent natives pour les utilisateurs de teams.

### <a name="cards"></a>Cartes

Les [cartes](~/task-modules-and-cards/what-are-cards.md) sont des conteneurs d’interface utilisateur définis par JSON, qui peuvent contenir du texte mis en forme, des médias, des contrôles (tels que des listes déroulantes et des cases d’option) et des boutons qui déclenchent une action.

Les actions de carte peuvent envoyer des charges utiles vers l’API de votre application, ouvrir un lien, initier des flux d’authentification ou envoyer des messages vers les conversations. La plateforme teams prend en charge plusieurs cartes, notamment des cartes adaptatives, des cartes héros, des cartes miniatures, etc. Vous pouvez combiner des collections de cartes et des affichages dans une liste ou un carrousel.

### <a name="task-modules"></a>Modules de tâche

Les [modules de tâches](~/task-modules-and-cards/what-are-task-modules.md) fournissent des expériences modales dans Teams. Elles sont particulièrement utiles pour lancer des flux de travail, collecter des entrées d’utilisateur ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power BI. Dans les modules de tâches, vous pouvez exécuter du code frontal personnalisé, afficher un `<iframe>` widget ou afficher une carte adaptative.

Lorsque vous envisagez de créer votre application, rappelez-vous que les modaux sont naturels pour que les utilisateurs entrent des informations ou exécutent des tâches par rapport à un onglet ou à une expérience de robot basée sur une conversation.

### <a name="deep-links"></a>Liens profonds

Votre application peut créer [des liens détaillés d’URL](~/concepts/build-and-test/deep-links.md) pour vous aider à parcourir votre utilisateur via votre application, ainsi que le client Teams. Vous pouvez créer un lien profond pour la plupart des entités dans Teams, et certains (comme une nouvelle demande de réunion) vous permettent de pré-remplir des informations à l’aide de chaînes de requête dans l’URL.

Par exemple, votre robot de conversation peut envoyer un message à un canal avec un lien détaillé vers un module de tâches qui entraîne l’envoi d’une carte en tant que message un-à-un à un utilisateur, qui, à son tour, contient un lien profond permettant de créer une réunion avec un utilisateur spécifique à une date/heure donnée. Utilisez des liens profonds pour vous connecter entre les différents points d’extension disponibles pour votre application, en gardant à tout moment votre utilisateur dans le contexte approprié.

### <a name="web-based-content"></a>Contenu Web

Le [contenu Web](~/tabs/how-to/create-tab-pages/content-page.md) est une page Web que vous hébergez et qui peut être incorporée dans un sous-onglet ou un module de tâches.
