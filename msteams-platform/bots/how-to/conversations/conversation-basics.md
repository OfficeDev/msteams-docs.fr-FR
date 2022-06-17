---
title: Concepts de base d’une conversation
description: Dans ce module, découvrez les conversations de bot dans un canal, une conversation personnelle et un environnement de conversation de groupe dans Teams.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 682555cadaeca5f50a942de98b2dcdd85ce0f6b2
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142919"
---
# <a name="conversation-basics"></a>Concepts de base d’une conversation

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Une conversation est une série de messages envoyés entre votre bot Microsoft Teams et un ou plusieurs utilisateurs. Le tableau suivant fournit les trois types de conversations, également appelés étendues dans Teams :

| Type de conversation | Description |
| ------- | ----------- |
| `channel` | Ce type de conversation est visible par tous les membres du canal. |
| `personal` | Ce type de conversation inclut les conversations entre les bots et un seul utilisateur. |
| `groupChat` | Ce type de conversation inclut la conversation entre un bot et au moins deux utilisateurs. Il active également votre bot dans les conversations de réunion. |

Un bot se comporte différemment en fonction de la conversation dans lequel il est impliqué :

* Les bots dans les conversations de canal et de groupe doivent être @mentionnés par l’utilisateur pour être appelés dans un canal.

* Les bots d’une conversation un-à-un ne nécessitent pas de @mention. Tous les messages envoyés par l’utilisateur sont acheminés vers votre bot.

> [!NOTE]
> Les bots peuvent être activés pour recevoir tous les messages de canal dans une équipe sans être @mentioned à l’aide d’autorisations de consentement spécifiques aux ressources (RSC). Cette fonctionnalité est actuellement disponible dans [préversion publique des développeurs](../../../resources/dev-preview/developer-preview-intro.md) uniquement. Pour plus d’informations, consultez [recevoir tous les messages de canal avec RSC](channel-messages-with-rsc.md).

Pour que le bot fonctionne dans une conversation ou une étendue particulière, ajoutez la prise en charge de cette étendue dans le [manifeste de l’application](~/resources/schema/manifest-schema.md).

Chaque message d’une conversation de bot est un `Activity` objet de type `messageType: message`. Lorsqu’un utilisateur envoie un message, Teams publie le message sur votre bot et le bot gère le message. En outre, pour définir les commandes principales auxquelles votre bot répond, vous pouvez ajouter un menu de commandes avec une liste déroulante de commandes pour votre bot. Les bots d’un groupe ou d’un canal ne reçoivent des messages que lorsqu’ils sont mentionnés @botname. Teams envoie des notifications à votre bot pour les événements de conversation qui se produisent dans les étendues où votre bot est actif. Vous pouvez capturer ces événements dans votre code et prendre des mesures à leur sujet.

Un bot peut également envoyer des messages proactifs aux utilisateurs. Un message proactif est un message envoyé par un bot qui n’est pas en réponse à une demande d’un utilisateur. Vous pouvez mettre en forme vos messages de bot pour inclure des cartes enrichies qui incluent des éléments interactifs, tels que des boutons, du texte, des images, de l’audio, de la vidéo, etc. Le bot peut mettre à jour dynamiquement les messages après les avoir envoyés, au lieu d’avoir vos messages en tant qu’instantanés statiques de données. Les messages peuvent également être supprimés à l’aide de la méthode `DeleteActivity` du Bot Framework.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Messages dans les conversations des robots](~/bots/how-to/conversations/conversation-messages.md)
