---
title: Envoyer l’id du locataire et l’id de conversation aux en-têtes de demande du bot
description: décrit comment envoyer l’identité du locataire et l’id de conversation aux en-têtes de demande du bot.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 76f667453114ab202d43217b9a4c01a6d14cc1a8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565892"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>Envoyer l’id du locataire et l’id de conversation aux en-têtes de demande du bot

Les demandes sortantes actuelles au bot ne contiennent pas dans l’en-tête ou l’URL aucune information qui aide les bots à acheminer le trafic sans déballer toute la charge utile. Les activités sont envoyées au bot via une URL similaire à https://<your_domain>/api/messages. Les demandes sont reçues pour afficher l’identité de la conversation et l’identité du locataire dans les en-têtes.

## <a name="request-header-fields"></a>Demander des champs d’en-tête

Deux champs d’en-tête de demande non standard sont ajoutés à toutes les demandes envoyées aux bots, tant pour le flux asynchrone que pour le flux synchrone. Le tableau suivant fournit les champs d’en-tête de demande et leurs valeurs :

| Clé de champ | Valeur |
|----------------|-----------------|
| x-ms-conversation-id | L’iD de conversation correspondant à l’activité de demande s’il y a lieu, confirmé ou vérifié. |
| x-ms-locataire-id | L’iD du locataire correspondant à la conversation dans l’activité de demande. |

Si le locataire ou l’iD de conversation n’est pas présent dans l’activité ou n’a pas été validé du côté du service, la valeur est vide.

![Demander des champs d’en-tête](~/assets/images/bots/requestheaderfields.png)
