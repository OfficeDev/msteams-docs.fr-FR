---
title: Concepts de base d’une conversation
description: Dans ce module, découvrez le type de conversation de bot dans un canal, la conversation personnelle et les étendues de conversation de groupe dans Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: ab27bc6000712cd046d92d9e020bfbe8fa65daa0
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791817"
---
# <a name="conversation-basics"></a>Concepts de base d’une conversation

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Une conversation est une série de messages envoyés entre votre bot Microsoft Teams et un ou plusieurs utilisateurs. Le tableau suivant fournit les trois types de conversations, également appelés étendues dans Teams :

| Type de conversation | Description |
| ------- | ----------- |
| `channel` | Ce type de conversation est visible par tous les membres du canal. |
| `personal` | Ce type de conversation inclut les conversations entre les bots et un seul utilisateur. |
| `groupChat` | Ce type de conversation inclut la conversation entre un bot et deux utilisateurs ou plus. Il active également votre bot dans les conversations de réunion. |

Un bot se comporte différemment selon la conversation dans laquelle il est impliqué :

* Les bots dans les conversations de canal et de groupe doivent être @mentionnés par l’utilisateur pour être appelés dans un canal.

* Les bots dans une conversation à deux n’ont pas besoin d’être @mentionnés. Tous les messages envoyés par l’utilisateur acheminent vers votre bot.

> [!NOTE]
> Les bots peuvent être activés pour recevoir tous les messages de canal dans une équipe sans être @mentioned à l’aide d’autorisations de consentement spécifiques aux ressources (RSC). Cette fonctionnalité est actuellement disponible dans [préversion publique des développeurs](../../../resources/dev-preview/developer-preview-intro.md) uniquement. Pour plus d’informations, consultez [recevoir tous les messages de canal avec RSC](channel-messages-with-rsc.md).

Pour que le bot fonctionne dans une conversation ou une étendue particulière, ajoutez la prise en charge de cette étendue dans le [manifeste de l’application](~/resources/schema/manifest-schema.md).

Chaque message dans une conversation de bot est un `Activity` objet de type `messageType: message`. Lorsqu’un utilisateur envoie un message, Teams publie le message sur votre bot et le bot gère le message. En outre, pour définir les commandes principales auxquelles votre bot répond, vous pouvez ajouter un menu de commandes avec une liste déroulante de commandes pour votre bot. Les bots d’un groupe ou d’un canal reçoivent uniquement des messages lorsqu’ils sont mentionnés @botname. Teams envoie des notifications à votre bot pour les événements de conversation qui se produisent dans les étendues où votre bot est actif. Vous pouvez capturer ces événements dans votre code et prendre des mesures sur ceux-ci.

Un bot peut également envoyer des messages proactifs aux utilisateurs. Un message proactif est un message envoyé par un bot qui ne répond pas à la demande d’un utilisateur. Vous pouvez mettre en forme les messages de votre bot pour inclure des cartes enrichies qui incluent des éléments interactifs, tels que des boutons, du texte, des images, de l’audio, de la vidéo, etc. Le bot peut mettre à jour dynamiquement les messages après leur envoi, au lieu d’avoir vos messages sous forme d’instantanés statiques de données. Les messages peuvent également être supprimés à l’aide de la méthode `DeleteActivity` du Bot Framework.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Messages dans les conversations des robots](~/bots/how-to/conversations/conversation-messages.md)
