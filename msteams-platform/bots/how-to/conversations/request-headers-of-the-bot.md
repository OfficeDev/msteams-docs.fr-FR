---
title: Envoyer l’ID client et l’ID de conversation aux en-têtes de requête du bot
description: décrit comment envoyer l’ID client et l’ID de conversation aux en-têtes de requête du bot.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: b3938b3011e09016f8594b2b17ba627d4922947b
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922527"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a><span data-ttu-id="a2e22-103">Envoyer l’ID client et l’ID de conversation aux en-têtes de requête du bot</span><span class="sxs-lookup"><span data-stu-id="a2e22-103">Send tenant ID and conversation ID to the request headers of the bot</span></span>

<span data-ttu-id="a2e22-104">Les demandes sortantes en cours au bot ne contiennent pas dans l’en-tête ou l’URL d’informations qui permettent aux bots d’router le trafic sans décompresser toute la charge utile.</span><span class="sxs-lookup"><span data-stu-id="a2e22-104">The current outgoing requests to the bot do not contain in the header or URL any information that helps bots route the traffic without unpacking the entire payload.</span></span> <span data-ttu-id="a2e22-105">Les activités sont envoyées au bot via une URL similaire à https://<your_domain>/api/messages.</span><span class="sxs-lookup"><span data-stu-id="a2e22-105">The activities are sent to the bot through a URL similar to https://<your_domain>/api/messages.</span></span> <span data-ttu-id="a2e22-106">Les demandes sont reçues pour afficher l’ID de conversation et l’ID de client dans les en-têtes.</span><span class="sxs-lookup"><span data-stu-id="a2e22-106">Requests are received to show the conversation ID and tenant ID in the headers.</span></span>

## <a name="request-header-fields"></a><span data-ttu-id="a2e22-107">Champs d’en-tête de requête</span><span class="sxs-lookup"><span data-stu-id="a2e22-107">Request header fields</span></span>

<span data-ttu-id="a2e22-108">Deux champs d’en-tête de requête non standard sont ajoutés à toutes les demandes envoyées aux bots, à la fois pour le flux asynchrone et le flux synchrone.</span><span class="sxs-lookup"><span data-stu-id="a2e22-108">Two non-standard request header fields are added to all the requests sent to bots, for both asynchronous flow and synchronous flow.</span></span> <span data-ttu-id="a2e22-109">Le tableau suivant fournit les champs d’en-tête de requête et leurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="a2e22-109">The following table provides the request header fields and their values.</span></span>

| <span data-ttu-id="a2e22-110">Clé de champ</span><span class="sxs-lookup"><span data-stu-id="a2e22-110">Field key</span></span> | <span data-ttu-id="a2e22-111">Valeur</span><span class="sxs-lookup"><span data-stu-id="a2e22-111">Value</span></span> |
|----------------|-----------------|
| <span data-ttu-id="a2e22-112">x-ms-conversation-id</span><span class="sxs-lookup"><span data-stu-id="a2e22-112">x-ms-conversation-id</span></span> | <span data-ttu-id="a2e22-113">ID de conversation correspondant à l’activité de demande, le cas échéant, et confirmé ou vérifié.</span><span class="sxs-lookup"><span data-stu-id="a2e22-113">The conversation ID corresponding to the request activity if applicable and confirmed or verified.</span></span> |
| <span data-ttu-id="a2e22-114">x-ms-tenant-id</span><span class="sxs-lookup"><span data-stu-id="a2e22-114">x-ms-tenant-id</span></span> | <span data-ttu-id="a2e22-115">ID de client correspondant à la conversation dans l’activité de demande.</span><span class="sxs-lookup"><span data-stu-id="a2e22-115">The tenant ID corresponding to the conversation in the request activity.</span></span> |

<span data-ttu-id="a2e22-116">Si le client ou l’ID de conversation n’est pas présent dans l’activité ou n’a pas été validé côté service, la valeur est vide.</span><span class="sxs-lookup"><span data-stu-id="a2e22-116">If the tenant or conversation ID is not present in the activity or was not validated on the service side, the value is empty.</span></span>

![Champs d’en-tête de requête](~/assets/images/bots/requestheaderfields.png)
