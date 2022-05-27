---
title: Envoyer l’ID de locataire et l’ID de conversation aux en-têtes de demande du bot
description: Décrit comment envoyer l’ID de locataire et l’ID de conversation aux en-têtes de demande du bot.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 8aca2c11dbdfc84abe8c4d0ec40e2748d04f6301
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757289"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>Envoyer l’ID de locataire et l’ID de conversation aux en-têtes de demande du bot

Les requêtes sortantes actuelles adressées au bot ne contiennent dans l’en-tête ou l’URL aucune information qui permet aux bots d’acheminer le trafic sans décompresser la charge utile entière. Les activités sont envoyées au bot via une URL similaire à https://<your_domain>/api/messages. Les demandes sont reçues pour afficher l’ID de conversation et l’ID de locataire dans les en-têtes.

## <a name="request-header-fields"></a>Champs d’en-tête de demande

Deux champs d’en-tête de demande non standard sont ajoutés à toutes les demandes envoyées aux bots, à la fois pour le flux asynchrone et le flux synchrone. Le tableau suivant fournit les champs d’en-tête de demande et leurs valeurs :

| Clé de champ | Valeur |
|----------------|-----------------|
| x-ms-conversation-id | ID de conversation correspondant à l’activité de demande, le cas échéant, et confirmé ou vérifié. |
| x-ms-tenant-id | ID de locataire correspondant à la conversation dans l’activité de demande. |

Si le locataire ou l’ID de conversation n’est pas présent dans l’activité ou n’a pas été validé côté service, la valeur est vide.

![Champs d’en-tête de demande](~/assets/images/bots/requestheaderfields.png)
