---
title: Points d’entrée pour les applications Teams
author: heath-hamilton
description: Décrit les points d’entrée de votre application, tels que l’équipe, le canal et la conversation dans une expérience d’application personnelle et partagée
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 1bfaed5ec9c2ef1bec9dc3699dbb5914be213a44
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889078"
---
# <a name="entry-points-for-teams-apps"></a>Points d’entrée pour les applications Teams

La plateforme Teams fournit un ensemble flexible de points d’entrée, tels qu’une équipe, un canal et une conversation, où les personnes peuvent découvrir et utiliser votre application. Votre application peut être aussi simple que l'intégration d'un contenu web existant dans un onglet ou une application à plusieurs facettes avec laquelle les utilisateurs interagissent dans plusieurs contextes.
Les applications les plus réussies sont natives Teams, donc choisissez soigneusement les points d’entrée de votre application.

## <a name="shared-app-experiences"></a>Expériences d’application partagées

Les équipes, les canaux et les discussions sont des espaces de collaboration. Les applications dans ces contextes sont disponibles pour tout le monde dans cet espace. Les espaces de collaboration se concentrent généralement sur des flux de travail supplémentaires ou sur le déverrouillage de nouvelles interactions sociales.

La liste suivante montre comment les fonctionnalités Teams’application sont couramment utilisées dans des contextes de collaboration :

* [**Les onglets**](~/tabs/what-are-tabs.md) offrent une expérience web intégrée en plein écran configurée pour l’équipe, le canal ou la conversation de groupe. Tous les membres interagissent avec le même contenu web, de sorte qu’une expérience d’application mono-page sans état est typique.

* [**Les extensions de messagerie**](~/messaging-extensions/what-are-messaging-extensions.md) sont des raccourcis permettant d'insérer du contenu externe dans une conversation ou de prendre des mesures concernant les messages sans quitter Teams. [Le déploiement de liens fournit](~/messaging-extensions/how-to/link-unfurling.md) un contenu enrichi lors du partage de contenu à partir d’une URL commune.

* Les bots interagissent avec les membres de la conversation par le biais d’une conversation et de la réponse à des [**événements,**](~/bots/what-are-bots.md) tels que l’ajout d’un nouveau membre ou le changement de nom d’un canal. 
   > [!NOTE]
   > Les conversations avec un bot dans ces contextes sont visibles par tous les membres de l’équipe, du canal ou du groupe, de sorte que les conversations de bot doivent être pertinentes pour tout le monde.

* [**Les webhooks et connecteurs**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permettent à un service externe de publier des messages dans une conversation et aux utilisateurs d’envoyer des messages à un service.

* [**L’API REST Microsoft Graph**](/graph/teams-concept-overview) pour obtenir des données sur les équipes, les canaux et les conversations de groupe pour automatiser et gérer les processus Teams.

## <a name="personal-app-experiences"></a>Expériences d’application personnelles

[Les applications personnelles](../concepts/design/personal-apps.md) sont la partie de votre application Teams qui se concentre sur les communications avec un seul utilisateur. L’expérience dans ce contexte est propre à chaque utilisateur.

La liste suivante montre comment les fonctionnalités Teams sont couramment utilisées dans les contextes personnels :

* [**Les bots**](~/bots/what-are-bots.md) ont des conversations à deux avec un utilisateur. Les bots qui nécessitent des conversations à plusieurs tours ou qui fournissent des notifications pertinentes uniquement pour un utilisateur spécifique sont mieux adaptés aux applications personnelles.

* [**Les onglets**](~/tabs/what-are-tabs.md) offrent une expérience web incorporée plein écran qui est significative pour l’utilisateur qui la regarde.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Comprendre les cas d’utilisation](../concepts/design/understand-use-cases.md)

## <a name="see-also"></a>Voir aussi

[Teams de conception d’application](../concepts/design/design-teams-app-overview.md) <br>
[Créer votre première application Microsoft Teams de messagerie](../build-your-first-app/build-first-app-overview.md)