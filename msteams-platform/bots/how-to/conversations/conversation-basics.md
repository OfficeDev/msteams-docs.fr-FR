---
title: Concepts de base d’une conversation
description: Présentation des conversations
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: conversations basics messages
ms.openlocfilehash: c06f8765ae17f28f3abb1dff67d77aad4e76958c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020034"
---
# <a name="conversation-basics"></a><span data-ttu-id="db7a9-103">Concepts de base d’une conversation</span><span class="sxs-lookup"><span data-stu-id="db7a9-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="db7a9-104">Une conversation est une série de messages envoyés entre votre bot Microsoft Teams et un ou plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="db7a9-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="db7a9-105">Le tableau suivant fournit les trois types de conversations, également appelés étendues dans Teams :</span><span class="sxs-lookup"><span data-stu-id="db7a9-105">The following table provides the three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="db7a9-106">Type de conversation</span><span class="sxs-lookup"><span data-stu-id="db7a9-106">Conversation type</span></span> | <span data-ttu-id="db7a9-107">Description</span><span class="sxs-lookup"><span data-stu-id="db7a9-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="db7a9-108">Ce type de conversation est visible par tous les membres du canal.</span><span class="sxs-lookup"><span data-stu-id="db7a9-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="db7a9-109">Ce type de conversation inclut les conversations entre les bots et un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db7a9-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="db7a9-110">Ce type de conversation inclut la conversation entre un bot et au moins deux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="db7a9-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="db7a9-111">Il active également votre bot dans les conversations de réunion.</span><span class="sxs-lookup"><span data-stu-id="db7a9-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="db7a9-112">Un bot se comporte différemment en fonction de la conversation dans qui il est impliqué :</span><span class="sxs-lookup"><span data-stu-id="db7a9-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="db7a9-113">Les bots dans les conversations de canal et de groupe nécessitent que l'utilisateur mentionne @ le bot pour l'appeler dans un canal.</span><span class="sxs-lookup"><span data-stu-id="db7a9-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="db7a9-114">Les bots d'une conversation un-à-un ne nécessitent pas de mention @ .</span><span class="sxs-lookup"><span data-stu-id="db7a9-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="db7a9-115">Tous les messages envoyés par l'utilisateur sont acheminés vers votre bot.</span><span class="sxs-lookup"><span data-stu-id="db7a9-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="db7a9-116">Pour que le bot fonctionne dans une conversation ou une étendue particulière, ajoutez la prise en charge à cette étendue dans le manifeste [de l'application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="db7a9-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

<span data-ttu-id="db7a9-117">Chaque message d'une conversation de bot est `Activity` un objet de type `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="db7a9-117">Each message in a bot conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="db7a9-118">Lorsqu'un utilisateur envoie un message, Teams publie le message à votre bot et le bot gère le message.</span><span class="sxs-lookup"><span data-stu-id="db7a9-118">When a user sends a message, Teams posts the message to your bot and the bot handles the message.</span></span> <span data-ttu-id="db7a9-119">En outre, pour définir les commandes principales à qui votre bot répond, vous pouvez ajouter un menu de commandes avec une liste déroulante de commandes pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="db7a9-119">In addition, to define core commands that your bot responds to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="db7a9-120">Les bots d'un groupe ou d'un canal reçoivent uniquement des messages lorsqu'ils sont mentionnés @botname.</span><span class="sxs-lookup"><span data-stu-id="db7a9-120">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="db7a9-121">Teams envoie des notifications à votre bot pour les événements de conversation qui se produisent dans les étendues où votre bot est actif.</span><span class="sxs-lookup"><span data-stu-id="db7a9-121">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="db7a9-122">Vous pouvez capturer ces événements dans votre code et agir dessus.</span><span class="sxs-lookup"><span data-stu-id="db7a9-122">You can capture these events in your code and take action on them.</span></span> 

<span data-ttu-id="db7a9-123">Un bot peut également envoyer des messages proactifs aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="db7a9-123">A bot can also send proactive messages to users.</span></span> <span data-ttu-id="db7a9-124">Un message proactif est un message envoyé par un bot qui ne répond pas à une demande d'un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db7a9-124">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="db7a9-125">Vous pouvez mettre en forme vos messages de bot pour inclure des cartes enrichies qui incluent des éléments interactifs, tels que des boutons, du texte, des images, de l'audio, de la vidéo, etc.</span><span class="sxs-lookup"><span data-stu-id="db7a9-125">You can format your bot messages to include rich cards that include interactive elements, such as buttons, text, images, audio, video, and so on.</span></span> <span data-ttu-id="db7a9-126">Le bot peut mettre à jour dynamiquement les messages après les avoir envoyés, au lieu d'avoir vos messages en tant que captures instantanées statiques des données.</span><span class="sxs-lookup"><span data-stu-id="db7a9-126">Bot can dynamically update messages after sending them, instead of having your messages as static snapshots of data.</span></span> <span data-ttu-id="db7a9-127">Les messages peuvent également être supprimés à l'aide de la méthode `DeleteActivity` Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="db7a9-127">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="next-step"></a><span data-ttu-id="db7a9-128">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="db7a9-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db7a9-129">Messages dans les conversations des robots</span><span class="sxs-lookup"><span data-stu-id="db7a9-129">Messages in bot conversations</span></span>](~/bots/how-to/conversations/conversation-messages.md)
