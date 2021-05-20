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
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a><span data-ttu-id="860cc-103">Envoyer l’id du locataire et l’id de conversation aux en-têtes de demande du bot</span><span class="sxs-lookup"><span data-stu-id="860cc-103">Send tenant ID and conversation ID to the request headers of the bot</span></span>

<span data-ttu-id="860cc-104">Les demandes sortantes actuelles au bot ne contiennent pas dans l’en-tête ou l’URL aucune information qui aide les bots à acheminer le trafic sans déballer toute la charge utile.</span><span class="sxs-lookup"><span data-stu-id="860cc-104">The current outgoing requests to the bot do not contain in the header or URL any information that helps bots route the traffic without unpacking the entire payload.</span></span> <span data-ttu-id="860cc-105">Les activités sont envoyées au bot via une URL similaire à https://<your_domain>/api/messages.</span><span class="sxs-lookup"><span data-stu-id="860cc-105">The activities are sent to the bot through a URL similar to https://<your_domain>/api/messages.</span></span> <span data-ttu-id="860cc-106">Les demandes sont reçues pour afficher l’identité de la conversation et l’identité du locataire dans les en-têtes.</span><span class="sxs-lookup"><span data-stu-id="860cc-106">Requests are received to show the conversation ID and tenant ID in the headers.</span></span>

## <a name="request-header-fields"></a><span data-ttu-id="860cc-107">Demander des champs d’en-tête</span><span class="sxs-lookup"><span data-stu-id="860cc-107">Request header fields</span></span>

<span data-ttu-id="860cc-108">Deux champs d’en-tête de demande non standard sont ajoutés à toutes les demandes envoyées aux bots, tant pour le flux asynchrone que pour le flux synchrone.</span><span class="sxs-lookup"><span data-stu-id="860cc-108">Two non-standard request header fields are added to all the requests sent to bots, for both asynchronous flow and synchronous flow.</span></span> <span data-ttu-id="860cc-109">Le tableau suivant fournit les champs d’en-tête de demande et leurs valeurs :</span><span class="sxs-lookup"><span data-stu-id="860cc-109">The following table provides the request header fields and their values:</span></span>

| <span data-ttu-id="860cc-110">Clé de champ</span><span class="sxs-lookup"><span data-stu-id="860cc-110">Field key</span></span> | <span data-ttu-id="860cc-111">Valeur</span><span class="sxs-lookup"><span data-stu-id="860cc-111">Value</span></span> |
|----------------|-----------------|
| <span data-ttu-id="860cc-112">x-ms-conversation-id</span><span class="sxs-lookup"><span data-stu-id="860cc-112">x-ms-conversation-id</span></span> | <span data-ttu-id="860cc-113">L’iD de conversation correspondant à l’activité de demande s’il y a lieu, confirmé ou vérifié.</span><span class="sxs-lookup"><span data-stu-id="860cc-113">The conversation ID corresponding to the request activity if applicable and confirmed or verified.</span></span> |
| <span data-ttu-id="860cc-114">x-ms-locataire-id</span><span class="sxs-lookup"><span data-stu-id="860cc-114">x-ms-tenant-id</span></span> | <span data-ttu-id="860cc-115">L’iD du locataire correspondant à la conversation dans l’activité de demande.</span><span class="sxs-lookup"><span data-stu-id="860cc-115">The tenant ID corresponding to the conversation in the request activity.</span></span> |

<span data-ttu-id="860cc-116">Si le locataire ou l’iD de conversation n’est pas présent dans l’activité ou n’a pas été validé du côté du service, la valeur est vide.</span><span class="sxs-lookup"><span data-stu-id="860cc-116">If the tenant or conversation ID is not present in the activity or was not validated on the service side, the value is empty.</span></span>

![Demander des champs d’en-tête](~/assets/images/bots/requestheaderfields.png)
