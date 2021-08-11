---
title: Concepts de base d’une conversation
description: Présentation des conversations
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: conversations basics messages
ms.openlocfilehash: 886c2764c2d8dceecb0f6a0e960b3487d9360c3682e46c9a8098f6fb8a2876bf
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705860"
---
# <a name="conversation-basics"></a>Concepts de base d’une conversation

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Une conversation est une série de messages envoyés entre votre bot Microsoft Teams et un ou plusieurs utilisateurs. Le tableau suivant fournit les trois types de conversations, également appelés étendues dans Teams :

| Type de conversation | Description |
| ------- | ----------- |
| `channel` | Ce type de conversation est visible par tous les membres du canal. |
| `personal` | Ce type de conversation inclut les conversations entre les bots et un seul utilisateur. |
| `groupChat` | Ce type de conversation inclut la conversation entre un bot et au moins deux utilisateurs. Il active également votre bot dans les conversations de réunion. |

Un bot se comporte différemment en fonction de la conversation dans qui il est impliqué :

* Les bots dans les conversations de canal et de groupe doivent être @mentionnés par l’utilisateur pour être appelés dans un canal.

* Les bots dans une conversation un-à-un ne nécessitent pas de @mention. Tous les messages envoyés par l’utilisateur sont acheminés vers votre bot.

> [!NOTE]
> Les bots peuvent être activés pour recevoir tous les messages de canal dans une équipe sans être @mentioned à l’aide des autorisations de consentement spécifiques aux ressources (RSC). Cette fonctionnalité est actuellement disponible en prévisualisation [pour les](../../../resources/dev-preview/developer-preview-intro.md) développeurs publics uniquement. Pour plus d’informations, [voir recevoir tous les messages de canal avec RSC.](channel-messages-with-rsc.md)

Pour que le bot fonctionne dans une conversation ou une étendue particulière, ajoutez la prise en charge à cette étendue dans le manifeste [de l’application.](~/resources/schema/manifest-schema.md)

Chaque message d’une conversation de bot est `Activity` un objet de type `messageType: message` . Lorsqu’un utilisateur envoie un message, Teams publie le message à votre bot et le bot gère le message. En outre, pour définir les commandes principales à qui votre bot répond, vous pouvez ajouter un menu de commandes avec une liste déroulante de commandes pour votre bot. Les bots d’un groupe ou d’un canal reçoivent uniquement des messages lorsqu’ils sont mentionnés @botname. Teams envoie des notifications à votre bot pour les événements de conversation qui se produisent dans les étendues où votre bot est actif. Vous pouvez capturer ces événements dans votre code et agir dessus.

Un bot peut également envoyer des messages proactifs aux utilisateurs. Un message proactif est un message envoyé par un bot qui ne répond pas à une demande d’un utilisateur. Vous pouvez mettre en forme vos messages de bot pour inclure des cartes enrichies qui incluent des éléments interactifs, tels que des boutons, du texte, des images, de l’audio, de la vidéo, etc. Le bot peut mettre à jour dynamiquement les messages après les avoir envoyés, au lieu d’avoir vos messages en tant que captures instantanées statiques des données. Les messages peuvent également être supprimés à l’aide de la méthode `DeleteActivity` Bot Framework.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Messages dans les conversations des robots](~/bots/how-to/conversations/conversation-messages.md)
