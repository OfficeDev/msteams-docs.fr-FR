---
title: Envoyer l’ID client et l’ID de conversation aux en-têtes de requête du bot
description: décrit comment envoyer l’ID client et l’ID de conversation aux en-têtes de requête du bot.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 76f667453114ab202d43217b9a4c01a6d14cc1a8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565892"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>Envoyer l’ID client et l’ID de conversation aux en-têtes de requête du bot

Les demandes sortantes en cours au bot ne contiennent pas dans l’en-tête ou l’URL des informations qui permettent aux bots d’router le trafic sans décompresser toute la charge utile. Les activités sont envoyées au bot via une URL similaire à https://<your_domain>/api/messages. Les demandes sont reçues pour afficher l’ID de conversation et l’ID de client dans les en-têtes.

## <a name="request-header-fields"></a>Champs d’en-tête de requête

Deux champs d’en-tête de requête non standard sont ajoutés à toutes les demandes envoyées aux bots, à la fois pour le flux asynchrone et le flux synchrone. Le tableau suivant fournit les champs d’en-tête de requête et leurs valeurs :

| Clé de champ | Valeur |
|----------------|-----------------|
| x-ms-conversation-id | ID de conversation correspondant à l’activité de demande, le cas échéant, et confirmé ou vérifié. |
| x-ms-tenant-id | ID de client correspondant à la conversation dans l’activité de demande. |

Si le client ou l’ID de conversation n’est pas présent dans l’activité ou n’a pas été validé côté service, la valeur est vide.

![Champs d’en-tête de requête](~/assets/images/bots/requestheaderfields.png)
