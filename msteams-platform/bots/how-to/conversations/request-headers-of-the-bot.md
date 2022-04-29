---
title: Envoyer l’ID de locataire et l’ID de conversation aux en-têtes de demande du bot
description: Décrit comment envoyer l’ID de locataire et l’ID de conversation aux en-têtes de demande du bot.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 9b63dd81eeccbf78989a31a06baa5d678916acef
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111289"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>Envoyer l’ID de locataire et l’ID de conversation aux en-têtes de demande du bot

Les demandes sortantes actuelles adressées au bot ne contiennent pas d’informations dans l’en-tête ou l’URL qui aident les bots à acheminer le trafic sans décompresser la charge utile entière. Les activités sont envoyées au bot via une URL similaire à https://<your_domain>/api/messages. Les demandes sont reçues pour afficher l’ID de conversation et l’ID de locataire dans les en-têtes.

## <a name="request-header-fields"></a>Champs d’en-tête de demande

Deux champs d’en-tête de demande non standard sont ajoutés à toutes les demandes envoyées aux bots, à la fois pour le flux asynchrone et le flux synchrone. Le tableau suivant fournit les champs d’en-tête de demande et leurs valeurs :

| Clé de champ | Valeur |
|----------------|-----------------|
| x-ms-conversation-id | ID de conversation correspondant à l’activité de demande, le cas échéant, et confirmé ou vérifié. |
| x-ms-tenant-id | ID de locataire correspondant à la conversation dans l’activité de demande. |

Si le locataire ou l’ID de conversation n’est pas présent dans l’activité ou n’a pas été validé côté service, la valeur est vide.

![Champs d’en-tête de demande](~/assets/images/bots/requestheaderfields.png)
