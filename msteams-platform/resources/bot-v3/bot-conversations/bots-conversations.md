---
title: Envoyer et recevoir des messages avec un bot
description: Décrit comment envoyer et recevoir des messages avec des bots dans Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: messages de bots teams
ms.date: 05/20/2019
ms.openlocfilehash: efa7658aef87650e360c79523ac1c282dc4814fd
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630459"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="2557e-104">Avoir une conversation avec un bot Microsoft Teams’équipe</span><span class="sxs-lookup"><span data-stu-id="2557e-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="2557e-105">Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2557e-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="2557e-106">Il existe trois types de conversations (ou portées) dans Teams :</span><span class="sxs-lookup"><span data-stu-id="2557e-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="2557e-107">`teams` Également appelées conversations de canal, visibles par tous les membres du canal.</span><span class="sxs-lookup"><span data-stu-id="2557e-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="2557e-108">`personal` Conversations entre les bots et un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2557e-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="2557e-109">`groupChat` Discutez entre un bot et au moins deux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2557e-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="2557e-110">Un bot se comporte légèrement différemment selon le type de conversation dans qui il est impliqué :</span><span class="sxs-lookup"><span data-stu-id="2557e-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="2557e-111">[Les bots dans les conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) de canal et de groupe nécessitent que l’utilisateur @mention le bot pour l’appeler dans un canal.</span><span class="sxs-lookup"><span data-stu-id="2557e-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="2557e-112">[Les bots dans les conversations d’un](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) seul utilisateur ne nécessitent pas de @mention - l’utilisateur peut simplement taper.</span><span class="sxs-lookup"><span data-stu-id="2557e-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @mention -  the user can just type.</span></span>

<span data-ttu-id="2557e-113">Pour que le bot fonctionne dans une étendue particulière, il doit être répertorié en tant que prise en charge de cette étendue dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="2557e-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="2557e-114">Les étendues sont définies et abordées plus en détail dans la [Référence du manifeste.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="2557e-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="2557e-115">Messages proactifs</span><span class="sxs-lookup"><span data-stu-id="2557e-115">Proactive messages</span></span>

<span data-ttu-id="2557e-116">Les bots peuvent participer à une conversation ou en initier une.</span><span class="sxs-lookup"><span data-stu-id="2557e-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="2557e-117">La plupart des communications sont en réponse à un autre message.</span><span class="sxs-lookup"><span data-stu-id="2557e-117">Most communication is in response to another message.</span></span> <span data-ttu-id="2557e-118">Si un bot initie une conversation, il s’agit *d’un message proactif.*</span><span class="sxs-lookup"><span data-stu-id="2557e-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="2557e-119">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2557e-119">Examples include:</span></span>

* <span data-ttu-id="2557e-120">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="2557e-120">Welcome messages</span></span>
* <span data-ttu-id="2557e-121">Notifications d’événement</span><span class="sxs-lookup"><span data-stu-id="2557e-121">Event notifications</span></span>
* <span data-ttu-id="2557e-122">Interrogation des messages</span><span class="sxs-lookup"><span data-stu-id="2557e-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="2557e-123">Concepts de base d’une conversation</span><span class="sxs-lookup"><span data-stu-id="2557e-123">Conversation basics</span></span>

<span data-ttu-id="2557e-124">Chaque message est un objet `Activity` de type `messageType: message`.</span><span class="sxs-lookup"><span data-stu-id="2557e-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="2557e-125">Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot.</span><span class="sxs-lookup"><span data-stu-id="2557e-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="2557e-126">Votre bot examine le message pour déterminer son type et répond en conséquence.</span><span class="sxs-lookup"><span data-stu-id="2557e-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="2557e-127">Les bots supportent également les messages de type événement.</span><span class="sxs-lookup"><span data-stu-id="2557e-127">Bots also support event-style messages.</span></span> <span data-ttu-id="2557e-128">Pour plus d’informations, voir [Gérer les événements de bot dans Microsoft Teams](~/resources/bot-v3/bots-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="2557e-128">For more information, see [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md).</span></span> <span data-ttu-id="2557e-129">La reconnaissance vocale n’est actuellement pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2557e-129">Speech is currently not supported.</span></span>

<span data-ttu-id="2557e-130">Les messages sont pour la plupart identiques dans toutes les étendues, mais il existe des différences dans l’accès au bot dans l’interface utilisateur et des différences en arrière-plan que vous devez connaître.</span><span class="sxs-lookup"><span data-stu-id="2557e-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="2557e-131">La conversation de base est gérée par le biais du connecteur Bot Framework, une API REST unique permettant à votre bot de communiquer avec Teams et d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="2557e-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="2557e-132">Le SDK Bot Builder fournit un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux et l’état des conversations, ainsi que des moyens simples d’incorporer des services cognitives tels que le traitement du langage naturel (NLP).</span><span class="sxs-lookup"><span data-stu-id="2557e-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="2557e-133">Contenu du message</span><span class="sxs-lookup"><span data-stu-id="2557e-133">Message content</span></span>

<span data-ttu-id="2557e-134">Votre bot peut envoyer du texte enrichi, des images et des cartes.</span><span class="sxs-lookup"><span data-stu-id="2557e-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="2557e-135">Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.</span><span class="sxs-lookup"><span data-stu-id="2557e-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="2557e-136">Vous pouvez spécifier le type de contenu que votre bot peut gérer dans la page Microsoft Teams paramètres de votre bot.</span><span class="sxs-lookup"><span data-stu-id="2557e-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="2557e-137">Format</span><span class="sxs-lookup"><span data-stu-id="2557e-137">Format</span></span> | <span data-ttu-id="2557e-138">De l’utilisateur au bot</span><span class="sxs-lookup"><span data-stu-id="2557e-138">From user to bot</span></span>  | <span data-ttu-id="2557e-139">Du bot à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2557e-139">From bot to user</span></span> |  <span data-ttu-id="2557e-140">Notes</span><span class="sxs-lookup"><span data-stu-id="2557e-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="2557e-141">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2557e-141">Rich text</span></span> | <span data-ttu-id="2557e-142">✔</span><span class="sxs-lookup"><span data-stu-id="2557e-142">✔</span></span> | <span data-ttu-id="2557e-143">✔</span><span class="sxs-lookup"><span data-stu-id="2557e-143">✔</span></span> |  |
| <span data-ttu-id="2557e-144">Images</span><span class="sxs-lookup"><span data-stu-id="2557e-144">Pictures</span></span> | <span data-ttu-id="2557e-145">✔</span><span class="sxs-lookup"><span data-stu-id="2557e-145">✔</span></span> | <span data-ttu-id="2557e-146">✔</span><span class="sxs-lookup"><span data-stu-id="2557e-146">✔</span></span> | <span data-ttu-id="2557e-147">Maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2557e-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported.</span></span> |
| <span data-ttu-id="2557e-148">Cartes</span><span class="sxs-lookup"><span data-stu-id="2557e-148">Cards</span></span> | <span data-ttu-id="2557e-149">✖</span><span class="sxs-lookup"><span data-stu-id="2557e-149">✖</span></span> | <span data-ttu-id="2557e-150">✔</span><span class="sxs-lookup"><span data-stu-id="2557e-150">✔</span></span> | <span data-ttu-id="2557e-151">Voir la référence [Teams carte de visite](~/task-modules-and-cards/cards/cards-reference.md) pour les cartes pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2557e-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="2557e-152">Emojis</span><span class="sxs-lookup"><span data-stu-id="2557e-152">Emojis</span></span> | <span data-ttu-id="2557e-153">✖</span><span class="sxs-lookup"><span data-stu-id="2557e-153">✖</span></span> | <span data-ttu-id="2557e-154">✔</span><span class="sxs-lookup"><span data-stu-id="2557e-154">✔</span></span> | <span data-ttu-id="2557e-155">Teams prend actuellement en charge les emojis via UTF-16, par exemple, U+1F600 pour le visage de panoramique.</span><span class="sxs-lookup"><span data-stu-id="2557e-155">Teams currently supports emojis via UTF-16 such as, U+1F600 for grinning face.</span></span> |
|

<span data-ttu-id="2557e-156">Pour plus d’informations sur les types d’interaction de bot pris en charge par Bot Framework, sur lesquels les bots dans les équipes sont basés, voir la documentation Bot Framework sur le flux de [conversation](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) et les concepts associés dans la documentation du [SDK Bot Builder](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) pour .NET et du [SDK Bot Builder ](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="2557e-156">For more information on the types of bot interaction supported by the Bot Framework, which bots in teams are based on, see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="2557e-157">Mise en forme de messages</span><span class="sxs-lookup"><span data-stu-id="2557e-157">Message formatting</span></span>

<span data-ttu-id="2557e-158">Vous pouvez définir la propriété facultative d’un contrôle de la façon dont le contenu de texte de votre [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) `message` message est rendu.</span><span class="sxs-lookup"><span data-stu-id="2557e-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="2557e-159">Voir [la mise en forme des messages](~/resources/bot-v3/bots-message-format.md) pour obtenir une description détaillée de la mise en forme prise en charge dans les messages du bot.</span><span class="sxs-lookup"><span data-stu-id="2557e-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="2557e-160">Vous pouvez définir la propriété facultative pour contrôler le rendu du contenu du texte [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) de votre message.</span><span class="sxs-lookup"><span data-stu-id="2557e-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="2557e-161">Pour plus d’informations sur la façon dont Teams prend en charge la mise en forme du texte dans les équipes, voir La mise en forme du texte [dans les messages du bot.](~/resources/bot-v3/bots-text-formats.md)</span><span class="sxs-lookup"><span data-stu-id="2557e-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="2557e-162">Pour plus d’informations sur la mise en forme des cartes dans les messages, voir [Mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="2557e-162">For more information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="2557e-163">Messages image</span><span class="sxs-lookup"><span data-stu-id="2557e-163">Picture messages</span></span>

<span data-ttu-id="2557e-164">Les images sont envoyées en ajoutant des pièces jointes à un message.</span><span class="sxs-lookup"><span data-stu-id="2557e-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="2557e-165">Vous trouverez plus d’informations sur les pièces jointes dans la [documentation bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2557e-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="2557e-166">Les images peuvent être au maximum 1 024 × 1 024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2557e-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="2557e-167">Nous vous recommandons de spécifier la hauteur et la largeur de chaque image à l’aide de XML.</span><span class="sxs-lookup"><span data-stu-id="2557e-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="2557e-168">Si vous utilisez Markdown, la taille par défaut de l’image est 256×256.</span><span class="sxs-lookup"><span data-stu-id="2557e-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="2557e-169">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2557e-169">For example:</span></span>

* <span data-ttu-id="2557e-170">Utiliser `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="2557e-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="2557e-171">Ne pas utiliser `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="2557e-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="2557e-172">Réception de messages</span><span class="sxs-lookup"><span data-stu-id="2557e-172">Receiving messages</span></span>

<span data-ttu-id="2557e-173">Selon les étendues déclarées, votre bot peut recevoir des messages dans les contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="2557e-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="2557e-174">**conversation personnelle** Les utilisateurs peuvent interagir dans une conversation privée avec un bot en sélectionnant simplement le bot ajouté dans l’historique des conversations ou en tapant son nom ou son ID d’application dans la zone À : d’une nouvelle conversation.</span><span class="sxs-lookup"><span data-stu-id="2557e-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="2557e-175">**Canaux** Un bot peut être mentionné (« @_botname_») dans un canal s’il a été ajouté à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="2557e-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="2557e-176">Notez que les réponses supplémentaires à un bot dans un canal nécessitent de mentionner le bot.</span><span class="sxs-lookup"><span data-stu-id="2557e-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="2557e-177">Il ne répondra pas aux réponses lorsqu’il n’est pas mentionné.</span><span class="sxs-lookup"><span data-stu-id="2557e-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="2557e-178">Pour les messages entrants, votre bot reçoit un objet [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) de type `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="2557e-178">For incoming messages, your bot receives an [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object of type `messageType: message`.</span></span> <span data-ttu-id="2557e-179">Bien que l’objet puisse contenir d’autres types d’informations, tels que les mises à jour de canal envoyées à votre bot, le type représente la `Activity` communication entre le bot et [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2557e-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="2557e-180">Votre bot reçoit une charge utile qui contient le message de l’utilisateur, ainsi que d’autres informations sur l’utilisateur, la source du message et `Text` les Teams données.</span><span class="sxs-lookup"><span data-stu-id="2557e-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="2557e-181">Remarque :</span><span class="sxs-lookup"><span data-stu-id="2557e-181">Of note:</span></span>

* <span data-ttu-id="2557e-182">`timestamp` Date et heure du message en temps universel coordonné (UTC).</span><span class="sxs-lookup"><span data-stu-id="2557e-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC).</span></span>
* <span data-ttu-id="2557e-183">`localTimestamp` Date et heure du message dans le fuseau horaire de l’expéditeur.</span><span class="sxs-lookup"><span data-stu-id="2557e-183">`localTimestamp` The date and time of the message in the time zone of the sender.</span></span>
* <span data-ttu-id="2557e-184">`channelId` Toujours « msteams ».</span><span class="sxs-lookup"><span data-stu-id="2557e-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="2557e-185">Il s’agit d’un canal d’infrastructure de bot, et non d’un canal d’équipes.</span><span class="sxs-lookup"><span data-stu-id="2557e-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="2557e-186">`from.id` Un ID unique et chiffré pour cet utilisateur pour votre bot ; convient comme clé si votre application doit stocker des données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2557e-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="2557e-187">Il est unique pour votre bot et ne peut pas être directement utilisé en dehors de votre instance de bot d’une manière significative pour identifier cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2557e-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>
* <span data-ttu-id="2557e-188">`channelData.tenant.id` ID de client de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2557e-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="2557e-189">`from.id` est unique pour votre bot et ne peut pas être directement utilisé en dehors de votre instance de bot d’une manière significative pour identifier cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2557e-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="2557e-190">Combinaison d’interactions canal et privée avec votre bot</span><span class="sxs-lookup"><span data-stu-id="2557e-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="2557e-191">Lorsque vous interagissez dans un canal, votre bot doit être intelligent pour mettre certaines conversations hors connexion avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2557e-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="2557e-192">Par exemple, supposons qu’un utilisateur tente de coordonner une tâche complexe, telle que la planification avec un ensemble de membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="2557e-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="2557e-193">Plutôt que d’avoir toute la séquence d’interactions visible pour le canal, envisagez d’envoyer un message de conversation personnelle à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2557e-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="2557e-194">Votre bot doit pouvoir facilement faire passer l’utilisateur entre les conversations personnelles et les conversations de canal sans perte d’état.</span><span class="sxs-lookup"><span data-stu-id="2557e-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="2557e-195">N’oubliez pas de mettre à jour le canal une fois l’interaction terminée pour en informer les autres membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="2557e-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="2557e-196">Exemple de schéma entrant complet</span><span class="sxs-lookup"><span data-stu-id="2557e-196">Full inbound schema example</span></span>

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

> [!NOTE]
> <span data-ttu-id="2557e-197">Le champ de texte pour les messages entrants contient parfois des mentions.</span><span class="sxs-lookup"><span data-stu-id="2557e-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="2557e-198">Assurez-vous de les vérifier et de les bander correctement.</span><span class="sxs-lookup"><span data-stu-id="2557e-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="2557e-199">Pour plus d’informations, voir [Mentions.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)</span><span class="sxs-lookup"><span data-stu-id="2557e-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="2557e-200">Teams canal de distribution</span><span class="sxs-lookup"><span data-stu-id="2557e-200">Teams channel data</span></span>

<span data-ttu-id="2557e-201">L’objet contient des Teams spécifiques et constitue la source définitive des ID d’équipe et `channelData` de canal.</span><span class="sxs-lookup"><span data-stu-id="2557e-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="2557e-202">Vous devez mettre en cache et utiliser ces ID comme clés pour le stockage local.</span><span class="sxs-lookup"><span data-stu-id="2557e-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="2557e-203">`channelData`L’objet n’est pas inclus dans les messages dans les conversations personnelles, car ils ont lieu en dehors d’un canal.</span><span class="sxs-lookup"><span data-stu-id="2557e-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="2557e-204">Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2557e-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="2557e-205">`eventType`Teams type d’événement ; transmis uniquement en cas d’événements [de modification de canal.](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="2557e-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="2557e-206">`tenant.id`Azure Active Directory ID de client ; transmis dans tous les contextes.</span><span class="sxs-lookup"><span data-stu-id="2557e-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts.</span></span>
* <span data-ttu-id="2557e-207">`team` Transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="2557e-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="2557e-208">`id` GUID du canal.</span><span class="sxs-lookup"><span data-stu-id="2557e-208">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="2557e-209">`name`Nom de l’équipe ; transmis uniquement dans les cas d’événements [de changement de nom d’équipe.](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span><span class="sxs-lookup"><span data-stu-id="2557e-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates).</span></span>
* <span data-ttu-id="2557e-210">`channel` Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes où le bot a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="2557e-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="2557e-211">`id` GUID du canal.</span><span class="sxs-lookup"><span data-stu-id="2557e-211">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="2557e-212">`name`Nom du canal ; transmis uniquement en cas d’événements [de modification de canal.](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="2557e-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="2557e-213">`channelData.teamsTeamId` Deprecated.</span><span class="sxs-lookup"><span data-stu-id="2557e-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="2557e-214">Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="2557e-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="2557e-215">`channelData.teamsChannelId` Deprecated.</span><span class="sxs-lookup"><span data-stu-id="2557e-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="2557e-216">Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="2557e-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="2557e-217">Exemple d’objet channelData (événement channelCreated)</span><span class="sxs-lookup"><span data-stu-id="2557e-217">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

### <a name="net-example"></a><span data-ttu-id="2557e-218">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="2557e-218">.NET example</span></span>

<span data-ttu-id="2557e-219">Le package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet fournit un objet spécialisé, qui expose les propriétés pour accéder Teams `TeamsChannelData` des informations spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2557e-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="2557e-220">Envoi de réponses aux messages</span><span class="sxs-lookup"><span data-stu-id="2557e-220">Sending replies to messages</span></span>

<span data-ttu-id="2557e-221">Pour répondre à un message existant, [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) appelez .NET ou [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="2557e-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) in Node.js.</span></span> <span data-ttu-id="2557e-222">Le SDK Bot Builder gère tous les détails.</span><span class="sxs-lookup"><span data-stu-id="2557e-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="2557e-223">Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2557e-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) endpoint.</span></span>

<span data-ttu-id="2557e-224">Le contenu du message lui-même peut contenir du texte simple ou certaines des cartes et [actions](~/task-modules-and-cards/cards/cards-actions.md)de carte fournies par Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="2557e-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="2557e-225">Notez que dans votre schéma sortant, vous devez toujours utiliser le même schéma que celui `serviceUrl` que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="2557e-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="2557e-226">N’ignorez pas que la valeur `serviceUrl` tend à être stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="2557e-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="2557e-227">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée de `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="2557e-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="2557e-228">Mise à jour des messages</span><span class="sxs-lookup"><span data-stu-id="2557e-228">Updating messages</span></span>

<span data-ttu-id="2557e-229">Au lieu que vos messages soient des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages en ligne après les avoir envoyés.</span><span class="sxs-lookup"><span data-stu-id="2557e-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="2557e-230">Vous pouvez utiliser des mises à jour de messages dynamiques pour des scénarios tels que les mises à jour des sondages, la modification des actions disponibles après l’utilisation d’un bouton ou tout autre changement d’état asynchrone.</span><span class="sxs-lookup"><span data-stu-id="2557e-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="2557e-231">Le nouveau message ne doit pas nécessairement correspondre au type d’origine.</span><span class="sxs-lookup"><span data-stu-id="2557e-231">The new message need not match the original in type.</span></span> <span data-ttu-id="2557e-232">Par exemple, si le message d’origine contenait une pièce jointe, le nouveau message peut être un message texte simple.</span><span class="sxs-lookup"><span data-stu-id="2557e-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="2557e-233">Vous pouvez mettre à jour uniquement le contenu envoyé dans les messages à pièce jointe unique et les dispositions carrousels.</span><span class="sxs-lookup"><span data-stu-id="2557e-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="2557e-234">La publication de mises à jour dans des messages avec plusieurs pièces jointes dans la mise en page de liste n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2557e-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="2557e-235">API REST</span><span class="sxs-lookup"><span data-stu-id="2557e-235">REST API</span></span>

<span data-ttu-id="2557e-236">Pour émettre une mise à jour de message, effectuez simplement une requête PUT sur le point de terminaison à l’aide `/v3/conversations/<conversationId>/activities/<activityId>/` d’un ID d’activité donné.</span><span class="sxs-lookup"><span data-stu-id="2557e-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="2557e-237">Pour terminer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel POST d’origine.</span><span class="sxs-lookup"><span data-stu-id="2557e-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="2557e-238">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="2557e-238">.NET example</span></span>

<span data-ttu-id="2557e-239">Vous pouvez utiliser la `UpdateActivityAsync` méthode dans le SDK Bot Builder pour mettre à jour un message existant.</span><span class="sxs-lookup"><span data-stu-id="2557e-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a><span data-ttu-id="2557e-240">Node.js exemple</span><span class="sxs-lookup"><span data-stu-id="2557e-240">Node.js example</span></span>

<span data-ttu-id="2557e-241">Vous pouvez utiliser la `session.connector.update` méthode dans le SDK Bot Builder pour mettre à jour un message existant.</span><span class="sxs-lookup"><span data-stu-id="2557e-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="2557e-242">Démarrage d’une conversation (messagerie proactive)</span><span class="sxs-lookup"><span data-stu-id="2557e-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="2557e-243">Vous pouvez créer une conversation personnelle avec un utilisateur ou démarrer une nouvelle chaîne de réponse dans un canal pour votre bot d’équipe.</span><span class="sxs-lookup"><span data-stu-id="2557e-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="2557e-244">Cela vous permet d’envoyer un message à vos utilisateurs sans qu’ils contactent d’abord votre bot.</span><span class="sxs-lookup"><span data-stu-id="2557e-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="2557e-245">Pour plus d’informations, voir les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="2557e-245">For more information, see the following topics:</span></span>

<span data-ttu-id="2557e-246">Pour [plus d’informations générales](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) sur les conversations démarrées par des bots, voir messagerie proactive pour les bots.</span><span class="sxs-lookup"><span data-stu-id="2557e-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="2557e-247">Suppression de messages</span><span class="sxs-lookup"><span data-stu-id="2557e-247">Deleting messages</span></span>

<span data-ttu-id="2557e-248">Les messages peuvent être supprimés à l’aide de la méthode connecteurs dans [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) le [SDK BotBuilder](/bot-framework/bot-builder-overview-getstarted).</span><span class="sxs-lookup"><span data-stu-id="2557e-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
