---
title: Envoyer et recevoir des messages avec un bot
description: Indique comment envoyer et recevoir des messages avec des robots dans Microsoft teams
keywords: messages des robots teams
ms.date: 05/20/2019
ms.openlocfilehash: 864473c7f502d96987a48e5837840236c45f59c7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674027"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="6281a-104">Avoir une conversation avec un robot Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="6281a-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="6281a-105">Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6281a-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="6281a-106">Il existe trois types de conversations (également appelées étendues) dans teams :</span><span class="sxs-lookup"><span data-stu-id="6281a-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="6281a-107">`teams`Également appelés conversations de canal, visibles par tous les membres du canal.</span><span class="sxs-lookup"><span data-stu-id="6281a-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="6281a-108">`personal`Les conversations entre les robots et un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6281a-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="6281a-109">`groupChat`Conversation entre un bot et deux utilisateurs ou plus.</span><span class="sxs-lookup"><span data-stu-id="6281a-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="6281a-110">Un bot se comporte de manière légèrement différente en fonction du type de conversation impliquée :</span><span class="sxs-lookup"><span data-stu-id="6281a-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="6281a-111">Les [robots dans les conversations de conversation de groupe et de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) exigent que l’utilisateur appelle le robot pour l’appeler dans un canal.</span><span class="sxs-lookup"><span data-stu-id="6281a-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="6281a-112">Les [robots dans les conversations avec un seul utilisateur](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) ne nécessitent pas de @ mentions-l’utilisateur peut simplement taper.</span><span class="sxs-lookup"><span data-stu-id="6281a-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention -  the user can just type.</span></span>

<span data-ttu-id="6281a-113">Pour que le bot fonctionne dans une étendue particulière, il doit être indiqué comme étant pris en charge par cette étendue dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="6281a-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="6281a-114">Les étendues sont définies et décrites plus en détail dans la [référence de manifeste](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="6281a-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="6281a-115">Messages proactifs</span><span class="sxs-lookup"><span data-stu-id="6281a-115">Proactive messages</span></span>

<span data-ttu-id="6281a-116">Les robots peuvent participer à une conversation ou initier une conversation.</span><span class="sxs-lookup"><span data-stu-id="6281a-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="6281a-117">La plupart des communications sont en réponse à un autre message.</span><span class="sxs-lookup"><span data-stu-id="6281a-117">Most communication is in response to another message.</span></span> <span data-ttu-id="6281a-118">Si un bot lance une conversation, il s’appelle un *message proactif*.</span><span class="sxs-lookup"><span data-stu-id="6281a-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="6281a-119">Exemples :</span><span class="sxs-lookup"><span data-stu-id="6281a-119">Examples include:</span></span>

* <span data-ttu-id="6281a-120">Messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="6281a-120">Welcome messages</span></span>
* <span data-ttu-id="6281a-121">Notifications d’événements</span><span class="sxs-lookup"><span data-stu-id="6281a-121">Event notifications</span></span>
* <span data-ttu-id="6281a-122">Interrogation des messages</span><span class="sxs-lookup"><span data-stu-id="6281a-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="6281a-123">Notions de base sur les conversations</span><span class="sxs-lookup"><span data-stu-id="6281a-123">Conversation basics</span></span>

<span data-ttu-id="6281a-124">Chaque message est un `Activity` objet de type `messageType: message`.</span><span class="sxs-lookup"><span data-stu-id="6281a-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="6281a-125">Lorsqu’un utilisateur envoie un message, teams publie le message dans votre bot ; plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot.</span><span class="sxs-lookup"><span data-stu-id="6281a-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="6281a-126">Votre bot examine le message pour déterminer son type et répond en conséquence.</span><span class="sxs-lookup"><span data-stu-id="6281a-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="6281a-127">Les robots prennent également en charge les messages de style événement.</span><span class="sxs-lookup"><span data-stu-id="6281a-127">Bots also support event-style messages.</span></span> <span data-ttu-id="6281a-128">Pour plus d’informations, voir [gérer les événements bot dans Microsoft teams](~/resources/bot-v3/bots-notifications.md) .</span><span class="sxs-lookup"><span data-stu-id="6281a-128">See [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md) for more details.</span></span> <span data-ttu-id="6281a-129">La reconnaissance vocale n’est pas prise en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="6281a-129">Speech is currently not supported.</span></span>

<span data-ttu-id="6281a-130">Les messages sont en grande partie identiques pour toutes les étendues, mais il existe des différences entre l’accès au bot dans l’interface utilisateur et les différences par rapport aux scènes que vous devrez connaître.</span><span class="sxs-lookup"><span data-stu-id="6281a-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="6281a-131">La conversation de base est gérée via le connecteur de l’infrastructure bot, une seule API REST pour permettre à votre bot de communiquer avec teams et d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="6281a-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="6281a-132">Le kit de développement logiciel (SDK) du générateur de robots offre un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux de conversation et l’État, et des méthodes simples pour incorporer des services cognitifs tels que le traitement du langage naturel (NLP).</span><span class="sxs-lookup"><span data-stu-id="6281a-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="6281a-133">Contenu du message</span><span class="sxs-lookup"><span data-stu-id="6281a-133">Message content</span></span>

<span data-ttu-id="6281a-134">Votre robot peut envoyer du texte enrichi, des images et des cartes.</span><span class="sxs-lookup"><span data-stu-id="6281a-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="6281a-135">Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.</span><span class="sxs-lookup"><span data-stu-id="6281a-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="6281a-136">Vous pouvez spécifier le type de contenu que votre robot peut gérer dans la page Paramètres de Microsoft teams de votre robot.</span><span class="sxs-lookup"><span data-stu-id="6281a-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="6281a-137">Format</span><span class="sxs-lookup"><span data-stu-id="6281a-137">Format</span></span> | <span data-ttu-id="6281a-138">De l’utilisateur au bot</span><span class="sxs-lookup"><span data-stu-id="6281a-138">From user to bot</span></span>  | <span data-ttu-id="6281a-139">Du bot à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6281a-139">From bot to user</span></span> |  <span data-ttu-id="6281a-140">Notes</span><span class="sxs-lookup"><span data-stu-id="6281a-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="6281a-141">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="6281a-141">Rich text</span></span> | <span data-ttu-id="6281a-142">✔</span><span class="sxs-lookup"><span data-stu-id="6281a-142">✔</span></span> | <span data-ttu-id="6281a-143">✔</span><span class="sxs-lookup"><span data-stu-id="6281a-143">✔</span></span> |  |
| <span data-ttu-id="6281a-144">Images</span><span class="sxs-lookup"><span data-stu-id="6281a-144">Pictures</span></span> | <span data-ttu-id="6281a-145">✔</span><span class="sxs-lookup"><span data-stu-id="6281a-145">✔</span></span> | <span data-ttu-id="6281a-146">✔</span><span class="sxs-lookup"><span data-stu-id="6281a-146">✔</span></span> | <span data-ttu-id="6281a-147">Taille maximale 1024 x 1024 et 1 Mo au format PNG, JPEG ou GIF ; les images GIF animées ne sont pas prises en charge</span><span class="sxs-lookup"><span data-stu-id="6281a-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span> |
| <span data-ttu-id="6281a-148">Fiche</span><span class="sxs-lookup"><span data-stu-id="6281a-148">Cards</span></span> | <span data-ttu-id="6281a-149">✖</span><span class="sxs-lookup"><span data-stu-id="6281a-149">✖</span></span> | <span data-ttu-id="6281a-150">✔</span><span class="sxs-lookup"><span data-stu-id="6281a-150">✔</span></span> | <span data-ttu-id="6281a-151">Voir la [référence de la carte teams](~/task-modules-and-cards/cards/cards-reference.md) pour les cartes prises en charge</span><span class="sxs-lookup"><span data-stu-id="6281a-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="6281a-152">Emojis</span><span class="sxs-lookup"><span data-stu-id="6281a-152">Emojis</span></span> | <span data-ttu-id="6281a-153">✖</span><span class="sxs-lookup"><span data-stu-id="6281a-153">✖</span></span> | <span data-ttu-id="6281a-154">✔</span><span class="sxs-lookup"><span data-stu-id="6281a-154">✔</span></span> | <span data-ttu-id="6281a-155">Teams prend actuellement en charge les Emoji via UTF-16 (par exemple, U + 1F600 pour Grinning face)</span><span class="sxs-lookup"><span data-stu-id="6281a-155">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span> |
|

<span data-ttu-id="6281a-156">Pour plus d’informations sur les types d’interaction des robots pris en charge par l’infrastructure de robot (les robots dans teams sont basés sur), voir la documentation de l’infrastructure de robot sur le [flux de conversation](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) et les concepts connexes dans la documentation du kit de développement logiciel (SDK) du [Générateur de robots pour .net](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) et [le kit de développement logiciel (SDK) du générateur](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="6281a-156">For more information on the types of bot interaction supported by the Bot Framework (which bots in teams are based on), see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="6281a-157">Mise en forme des messages</span><span class="sxs-lookup"><span data-stu-id="6281a-157">Message formatting</span></span>

<span data-ttu-id="6281a-158">Vous pouvez définir la propriété [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) facultative d’un `message` pour contrôler le mode d’affichage du contenu de texte de votre message.</span><span class="sxs-lookup"><span data-stu-id="6281a-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="6281a-159">Consultez la rubrique [mise en forme](~/resources/bot-v3/bots-message-format.md) des messages pour une description détaillée de la mise en forme prise en charge dans les messages bot.</span><span class="sxs-lookup"><span data-stu-id="6281a-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="6281a-160">Vous pouvez définir la propriété [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) Optional pour contrôler le rendu du contenu de texte de votre message.</span><span class="sxs-lookup"><span data-stu-id="6281a-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="6281a-161">Pour plus d’informations sur la façon dont teams prend en charge la mise en forme de texte dans Teams, consultez la rubrique [formatage du texte dans les messages bot](~/resources/bot-v3/bots-text-formats.md)</span><span class="sxs-lookup"><span data-stu-id="6281a-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="6281a-162">Pour plus d’informations sur la mise en forme des cartes dans les messages, voir [Card Formatting](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="6281a-162">For information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="6281a-163">Messages d’image</span><span class="sxs-lookup"><span data-stu-id="6281a-163">Picture messages</span></span>

<span data-ttu-id="6281a-164">Les images sont envoyées par l’ajout de pièces jointes à un message.</span><span class="sxs-lookup"><span data-stu-id="6281a-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="6281a-165">Vous trouverez plus d’informations sur les pièces jointes dans la documentation de l' [infrastructure bot](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="6281a-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="6281a-166">Les images peuvent être d’au moins 1024 × 1024 et 1 Mo au format PNG, JPEG ou GIF ; l’image GIF animée n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6281a-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="6281a-167">Nous vous recommandons de spécifier la hauteur et la largeur de chaque image à l’aide de XML.</span><span class="sxs-lookup"><span data-stu-id="6281a-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="6281a-168">Si vous utilisez la démarque, la taille de l’image est par défaut de 256 × 256.</span><span class="sxs-lookup"><span data-stu-id="6281a-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="6281a-169">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6281a-169">For example:</span></span>

* <span data-ttu-id="6281a-170">Utilisant`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="6281a-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="6281a-171">Ne pas utiliser `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="6281a-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="6281a-172">Réception de messages</span><span class="sxs-lookup"><span data-stu-id="6281a-172">Receiving messages</span></span>

<span data-ttu-id="6281a-173">Selon les étendues déclarées, votre robot peut recevoir des messages dans les contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="6281a-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="6281a-174">**conversation personnelle** Les utilisateurs peuvent interagir dans une conversation privée avec un bot en sélectionnant simplement le bot ajouté dans l’historique de la conversation ou en tapant son nom ou son ID d’application dans la zone à : d’une nouvelle conversation.</span><span class="sxs-lookup"><span data-stu-id="6281a-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="6281a-175">**Canaux** Un bot peut être mentionné (« @_botname_») dans un canal s’il a été ajouté à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="6281a-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="6281a-176">Notez que les réponses supplémentaires à un bot dans un canal nécessitent de mentionner le bot.</span><span class="sxs-lookup"><span data-stu-id="6281a-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="6281a-177">Il ne répond pas aux réponses qui ne sont pas mentionnées.</span><span class="sxs-lookup"><span data-stu-id="6281a-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="6281a-178">Pour les messages entrants, votre bot [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) reçoit un objet `messageType: message`de type.</span><span class="sxs-lookup"><span data-stu-id="6281a-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) object of type `messageType: message`.</span></span> <span data-ttu-id="6281a-179">Bien que `Activity` l’objet puisse contenir d’autres types d’informations, comme les [mises à jour de canal](~/resources/bot-v3/bots-notifications.md#channel-updates) envoyées à `message` votre bot, le type représente la communication entre le bot et l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6281a-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="6281a-180">Votre bot reçoit une charge qui contient le message `Text` de l’utilisateur ainsi que d’autres informations sur l’utilisateur, la source du message et des informations sur les équipes.</span><span class="sxs-lookup"><span data-stu-id="6281a-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="6281a-181">De note :</span><span class="sxs-lookup"><span data-stu-id="6281a-181">Of note:</span></span>

* <span data-ttu-id="6281a-182">`timestamp`Date et heure du message en temps universel coordonné (UTC)</span><span class="sxs-lookup"><span data-stu-id="6281a-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC)</span></span>
* <span data-ttu-id="6281a-183">`localTimestamp`Date et heure du message dans le fuseau horaire de l’expéditeur</span><span class="sxs-lookup"><span data-stu-id="6281a-183">`localTimestamp` The date and time of the message in the time zone of the sender</span></span>
* <span data-ttu-id="6281a-184">`channelId`Toujours « msteams ».</span><span class="sxs-lookup"><span data-stu-id="6281a-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="6281a-185">Cela fait référence à un canal d’infrastructure bot, pas à un canal Teams.</span><span class="sxs-lookup"><span data-stu-id="6281a-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="6281a-186">`from.id`Un ID unique et chiffré pour cet utilisateur pour votre bot ; Cette clé est appropriée si votre application a besoin de stocker des données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6281a-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="6281a-187">Il est unique pour votre robot et ne peut pas être directement utilisé en dehors de votre instance de robot de manière significative pour identifier cet utilisateur</span><span class="sxs-lookup"><span data-stu-id="6281a-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user</span></span>
* <span data-ttu-id="6281a-188">`channelData.tenant.id`ID de client de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6281a-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="6281a-189">`from.id`est unique pour votre bot et ne peut pas être directement utilisé en dehors de votre instance de robot de manière significative pour identifier cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6281a-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="6281a-190">Combinaison d’interactions de canal et de privé avec votre robot</span><span class="sxs-lookup"><span data-stu-id="6281a-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="6281a-191">Lors de l’interaction dans un canal, votre robot doit être intelligent quant à la prise en main de certaines conversations avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6281a-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="6281a-192">Par exemple, supposons qu’un utilisateur tente de coordonner une tâche complexe, telle que la planification d’un ensemble de membres d’équipe.</span><span class="sxs-lookup"><span data-stu-id="6281a-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="6281a-193">Au lieu d’avoir l’intégralité de la séquence d’interactions visible par le canal, envisagez d’envoyer un message de conversation personnelle à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6281a-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="6281a-194">Votre robot doit être en mesure de transférer facilement l’utilisateur entre les conversations personnelles et les conversations de canal sans perte d’État.</span><span class="sxs-lookup"><span data-stu-id="6281a-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="6281a-195">N’oubliez pas de mettre à jour le canal une fois l’interaction terminée pour avertir les autres membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="6281a-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="6281a-196">Exemple de schéma entrant complet</span><span class="sxs-lookup"><span data-stu-id="6281a-196">Full inbound schema example</span></span>

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
> <span data-ttu-id="6281a-197">Le champ de texte pour les messages entrants contient parfois des mentions.</span><span class="sxs-lookup"><span data-stu-id="6281a-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="6281a-198">Assurez-vous de vérifier et de les supprimer correctement.</span><span class="sxs-lookup"><span data-stu-id="6281a-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="6281a-199">Pour plus d’informations, consultez la rubrique [mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span><span class="sxs-lookup"><span data-stu-id="6281a-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="6281a-200">Données de canal teams</span><span class="sxs-lookup"><span data-stu-id="6281a-200">Teams channel data</span></span>

<span data-ttu-id="6281a-201">L' `channelData` objet contient des informations spécifiques aux équipes et constitue la source définitive des ID d’équipe et de canal.</span><span class="sxs-lookup"><span data-stu-id="6281a-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="6281a-202">Vous devez mettre en cache et utiliser ces ID en tant que clés pour le stockage local.</span><span class="sxs-lookup"><span data-stu-id="6281a-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="6281a-203">L' `channelData` objet n’est pas inclus dans les messages dans les conversations personnelles, étant donné qu’ils ont lieu en dehors de n’importe quel canal.</span><span class="sxs-lookup"><span data-stu-id="6281a-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="6281a-204">Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6281a-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="6281a-205">`eventType`Type d’événement teams ; transmis uniquement en cas d' [événements de modification de canal](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="6281a-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates)</span></span>
* <span data-ttu-id="6281a-206">`tenant.id`ID de locataire Azure Active Directory ; transmis dans tous les contextes</span><span class="sxs-lookup"><span data-stu-id="6281a-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="6281a-207">`team`Transmis uniquement dans les contextes de canal, pas dans la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="6281a-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="6281a-208">`id`GUID du canal</span><span class="sxs-lookup"><span data-stu-id="6281a-208">`id` GUID for the channel</span></span>
  * <span data-ttu-id="6281a-209">`name`Nom de l’équipe ; transmis uniquement en cas d' [événement de changement de nom d’équipe](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span><span class="sxs-lookup"><span data-stu-id="6281a-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span></span>
* <span data-ttu-id="6281a-210">`channel`Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour des événements dans des canaux dans teams où le bot a été ajouté</span><span class="sxs-lookup"><span data-stu-id="6281a-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="6281a-211">`id`GUID du canal</span><span class="sxs-lookup"><span data-stu-id="6281a-211">`id` GUID for the channel</span></span>
  * <span data-ttu-id="6281a-212">`name`Nom du canal ; transmis uniquement en cas d' [événements de modification de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).</span><span class="sxs-lookup"><span data-stu-id="6281a-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="6281a-213">`channelData.teamsTeamId`Déconseillées.</span><span class="sxs-lookup"><span data-stu-id="6281a-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="6281a-214">Cette propriété est incluse uniquement à des fins de compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="6281a-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="6281a-215">`channelData.teamsChannelId`Déconseillées.</span><span class="sxs-lookup"><span data-stu-id="6281a-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="6281a-216">Cette propriété est incluse uniquement à des fins de compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="6281a-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="6281a-217">Exemple d’objet channelData (événement channelCreated)</span><span class="sxs-lookup"><span data-stu-id="6281a-217">Example channelData object (channelCreated event)</span></span>

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

### <a name="net-example"></a><span data-ttu-id="6281a-218">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="6281a-218">.NET example</span></span>

<span data-ttu-id="6281a-219">Le package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) fournit un `TeamsChannelData` objet spécialisé, qui expose les propriétés permettant d’accéder aux informations spécifiques aux équipes.</span><span class="sxs-lookup"><span data-stu-id="6281a-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="6281a-220">Envoi de réponses à des messages</span><span class="sxs-lookup"><span data-stu-id="6281a-220">Sending replies to messages</span></span>

<span data-ttu-id="6281a-221">Pour répondre à un message existant, appelez [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) le .net ou [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) dans node. js.</span><span class="sxs-lookup"><span data-stu-id="6281a-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) in Node.js.</span></span> <span data-ttu-id="6281a-222">Le kit de développement logiciel (SDK) du générateur de robots gère tous les détails.</span><span class="sxs-lookup"><span data-stu-id="6281a-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="6281a-223">Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6281a-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) endpoint.</span></span>

<span data-ttu-id="6281a-224">Le contenu du message lui-même peut contenir du texte simple ou une partie des [cartes et des actions de carte](~/task-modules-and-cards/cards/cards-actions.md)fournis.</span><span class="sxs-lookup"><span data-stu-id="6281a-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="6281a-225">Veuillez noter que dans votre schéma sortant, vous devez toujours utiliser le même `serviceUrl` que celui que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="6281a-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="6281a-226">N’oubliez pas que la valeur `serviceUrl` de tend à être stable mais peut varier.</span><span class="sxs-lookup"><span data-stu-id="6281a-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="6281a-227">Lors de l’arrivée d’un nouveau message, votre robot doit vérifier sa `serviceUrl`valeur stockée.</span><span class="sxs-lookup"><span data-stu-id="6281a-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="6281a-228">Mise à jour des messages</span><span class="sxs-lookup"><span data-stu-id="6281a-228">Updating messages</span></span>

<span data-ttu-id="6281a-229">Au lieu de faire en sorte que vos messages soient des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages insérés après les avoir envoyés.</span><span class="sxs-lookup"><span data-stu-id="6281a-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="6281a-230">Vous pouvez utiliser les mises à jour de messages dynamiques pour des scénarios tels que les mises à jour de sondage, la modification des actions disponibles après une pression sur un bouton ou tout autre changement d’état asynchrone.</span><span class="sxs-lookup"><span data-stu-id="6281a-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="6281a-231">Le nouveau message n’a pas besoin de correspondre au type d’origine.</span><span class="sxs-lookup"><span data-stu-id="6281a-231">The new message need not match the original in type.</span></span> <span data-ttu-id="6281a-232">Par exemple, si le message d’origine contient une pièce jointe, le nouveau message peut être un simple message texte.</span><span class="sxs-lookup"><span data-stu-id="6281a-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="6281a-233">Vous pouvez mettre à jour uniquement le contenu envoyé dans les mises en page et les messages à une seule pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="6281a-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="6281a-234">La publication de mises à jour de messages avec plusieurs pièces jointes dans la mise en forme de liste n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6281a-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="6281a-235">API REST</span><span class="sxs-lookup"><span data-stu-id="6281a-235">REST API</span></span>

<span data-ttu-id="6281a-236">Pour émettre une mise à jour de message, effectuez simplement une requête `/v3/conversations/<conversationId>/activities/<activityId>/` put sur le point de terminaison à l’aide d’un ID d’activité donné.</span><span class="sxs-lookup"><span data-stu-id="6281a-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="6281a-237">Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel POST d’origine.</span><span class="sxs-lookup"><span data-stu-id="6281a-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="6281a-238">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="6281a-238">.NET example</span></span>

<span data-ttu-id="6281a-239">Vous pouvez utiliser la `UpdateActivityAsync` méthode dans le kit de développement logiciel (SDK) du générateur de robots pour mettre à jour un message existant.</span><span class="sxs-lookup"><span data-stu-id="6281a-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

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

### <a name="nodejs-example"></a><span data-ttu-id="6281a-240">Exemple node. js</span><span class="sxs-lookup"><span data-stu-id="6281a-240">Node.js example</span></span>

<span data-ttu-id="6281a-241">Vous pouvez utiliser la `session.connector.update` méthode dans le kit de développement logiciel (SDK) du générateur de robots pour mettre à jour un message existant.</span><span class="sxs-lookup"><span data-stu-id="6281a-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

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

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="6281a-242">Démarrage d’une conversation (messagerie proactive)</span><span class="sxs-lookup"><span data-stu-id="6281a-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="6281a-243">Vous pouvez créer une conversation personnelle avec un utilisateur ou démarrer une nouvelle chaîne de réponse dans un canal pour votre robot d’équipe.</span><span class="sxs-lookup"><span data-stu-id="6281a-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="6281a-244">Cela vous permet d’envoyer un message à votre utilisateur ou à vos utilisateurs sans qu’ils commencent par contacter le robot.</span><span class="sxs-lookup"><span data-stu-id="6281a-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="6281a-245">Pour plus d’informations, voir les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="6281a-245">For more information, see the following topics:</span></span>

<span data-ttu-id="6281a-246">Consultez la rubrique [messagerie proactive pour les robots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) pour obtenir des informations plus générales sur les conversations démarrées par les robots.</span><span class="sxs-lookup"><span data-stu-id="6281a-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="6281a-247">Suppression de messages</span><span class="sxs-lookup"><span data-stu-id="6281a-247">Deleting messages</span></span>

<span data-ttu-id="6281a-248">Les messages peuvent être supprimés à l' [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) aide de la méthode Connectors dans le [Kit de développement logiciel (SDK) BotBuilder](/bot-framework/bot-builder-overview-getstarted).</span><span class="sxs-lookup"><span data-stu-id="6281a-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

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
