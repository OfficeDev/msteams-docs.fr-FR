---
title: Points d’entrée pour les applications Teams
author: heath-hamilton
description: Décrit l’endroit où les personnes peuvent découvrir et utiliser votre application dans Teams.
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: c26b938f56af6f09c0e4ba274b9b3f4da19d08ee
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566172"
---
# <a name="entry-points-for-teams-apps"></a>Points d’entrée pour les applications Teams

La Teams offre un ensemble flexible de points d’entrée, tels que l’équipe, le canal et le chat où les gens peuvent découvrir et utiliser votre application. Votre application peut être aussi simple que l'intégration d'un contenu web existant dans un onglet ou une application à plusieurs facettes avec laquelle les utilisateurs interagissent dans plusieurs contextes.
Les applications les plus réussies sont natives Teams, alors choisissez soigneusement les points d’entrée de votre application.

## <a name="shared-app-experiences"></a>Expériences d’application partagées

L’équipe, le canal et le chat sont des espaces de collaboration. Les applications dans ces contextes sont accessibles à tous dans cet espace. Les espaces de collaboration se concentrent généralement sur des workflows supplémentaires ou le déverrouillage de nouvelles interactions sociales.

La liste suivante montre comment les Teams’applications sont couramment utilisées dans des contextes collaboratifs :

* [**Les onglets**](~/tabs/what-are-tabs.md) offrent une expérience web intégrée en plein écran configurée pour l’équipe, le canal ou la conversation de groupe. Tous les membres interagissent avec le même contenu web, de sorte qu’une expérience d’application apatride d’une seule page est typique.

* [**Les extensions de messagerie**](~/messaging-extensions/what-are-messaging-extensions.md) sont des raccourcis permettant d'insérer du contenu externe dans une conversation ou de prendre des mesures concernant les messages sans quitter Teams. [Le déploiement de liens fournit un contenu](~/messaging-extensions/how-to/link-unfurling.md) riche lors du partage de contenu à partir d’une URL commune.

* [**Les bots**](~/bots/what-are-bots.md) interagissent avec les membres de la conversation par le biais de chat et de répondre à des événements, tels que l’ajout d’un nouveau membre ou le changement de nom d’un canal. 
   > [!NOTE]
   > Les conversations avec un bot dans ces contextes sont visibles par tous les membres de l’équipe, du canal ou du groupe, de sorte que les conversations bot doivent être pertinentes pour tout le monde.

* [**Les webhooks et connecteurs**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permettent à un service externe de publier des messages dans une conversation et aux utilisateurs d’envoyer des messages à un service.

* [**L’API REST Microsoft Graph**](/graph/teams-concept-overview) pour obtenir des données sur les équipes, les canaux et les conversations de groupe pour automatiser et gérer les processus Teams.

## <a name="personal-app-experiences"></a>Expériences personnelles d’application

[Les applications personnelles](../concepts/design/personal-apps.md) sont la partie de votre application Teams qui se concentre sur les communications avec un seul utilisateur. L’expérience dans ce contexte est propre à chaque utilisateur.

La liste suivante montre comment Teams capacités sont couramment utilisées dans des contextes personnels :

* [**Les bots**](~/bots/what-are-bots.md) ont des conversations à deux avec un utilisateur. Les bots qui nécessitent des conversations à plusieurs tours ou qui fournissent des notifications pertinentes uniquement pour un utilisateur spécifique sont mieux adaptés aux applications personnelles.

* [**Les onglets**](~/tabs/what-are-tabs.md) fournissent une expérience Web intégrée en plein écran qui est significative pour l’utilisateur qui la regarde.

## <a name="see-also"></a>Voir aussi

[Teams de conception d’applications](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Comprendre les cas d’utilisation](../concepts/design/understand-use-cases.md)
