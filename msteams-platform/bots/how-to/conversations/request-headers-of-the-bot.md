---
title: Envoyer l’ID de locataire et l’ID de conversation aux en-têtes de demande du bot
description: Découvrez comment router le trafic du bot sans décompresser la charge utile entière à l’aide de l’ID de locataire et de l’ID de conversation présents dans les en-têtes de demande du bot dans Teams.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 3132d91d4b3d0b290ee8e1fb35ebeea076217fe8
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100146"
---
# <a name="request-headers-of-the-bot"></a>Demander les en-têtes du bot

Les requêtes sortantes actuelles adressées au bot ne contiennent dans l’en-tête ou l’URL aucune information qui permet aux bots d’acheminer le trafic sans décompresser la charge utile entière. Les activités sont envoyées au bot via une URL similaire à https://<your_domain>/api/messages. Les demandes sont reçues pour afficher l’ID de conversation et l’ID de locataire dans les en-têtes.

## <a name="request-header-fields"></a>Champs d’en-tête de demande

Deux champs d’en-tête de demande non standard sont ajoutés à toutes les demandes envoyées aux bots, à la fois pour le flux asynchrone et le flux synchrone. Le tableau suivant fournit les champs d’en-tête de demande et leurs valeurs :

| Clé de champ | Valeur |
|----------------|-----------------|
| x-ms-conversation-id | ID de conversation correspondant à l’activité de demande, le cas échéant, et confirmé ou vérifié. |
| x-ms-tenant-id | ID de locataire correspondant à la conversation dans l’activité de demande. |

Si le locataire ou l’ID de conversation n’est pas présent dans l’activité ou n’a pas été validé côté service, la valeur est vide.

![Champs d’en-tête de demande](~/assets/images/bots/requestheaderfields.png)
