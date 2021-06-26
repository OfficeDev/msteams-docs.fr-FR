---
title: Webhooks et connecteurs
author: clearab
description: Comprendre comment les webhooks et les connecteurs peuvent connecter vos services web au client Teams web.
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2cb763a6637abd3faa500de871119f0b829871bf
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140053"
---
# <a name="webhooks-and-connectors"></a><span data-ttu-id="2db8f-103">Webhooks et connecteurs</span><span class="sxs-lookup"><span data-stu-id="2db8f-103">Webhooks and connectors</span></span>

<span data-ttu-id="2db8f-104">Les webhooks et les connecteurs permettent de connecter les services web aux canaux et aux équipes Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2db8f-104">Webhooks and connectors help to connect the web services to channels and teams in Microsoft Teams.</span></span> <span data-ttu-id="2db8f-105">Les webhooks sont des rappels HTTP définis par l’utilisateur qui avertit les utilisateurs de toute action qui a eu lieu dans Microsoft Teams canal.</span><span class="sxs-lookup"><span data-stu-id="2db8f-105">Webhooks are user defined HTTP callback that notifies users about any action that has taken place in the Microsoft Teams channel.</span></span> <span data-ttu-id="2db8f-106">C’est un moyen pour une application d’obtenir des données en temps réel.</span><span class="sxs-lookup"><span data-stu-id="2db8f-106">It is a way for an app to get real time data.</span></span> <span data-ttu-id="2db8f-107">Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir les notifications et les messages de vos services web.</span><span class="sxs-lookup"><span data-stu-id="2db8f-107">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="2db8f-108">Ils exposent un point de terminaison HTTPS pour que votre service publie des messages sous forme de cartes.</span><span class="sxs-lookup"><span data-stu-id="2db8f-108">They expose an HTTPS endpoint for your service to post messages in the form of cards.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="2db8f-109">Webhooks sortants</span><span class="sxs-lookup"><span data-stu-id="2db8f-109">Outgoing Webhooks</span></span>

<span data-ttu-id="2db8f-110">Les webhooks vous aident Teams à s’intégrer à des applications externes.</span><span class="sxs-lookup"><span data-stu-id="2db8f-110">Webhooks help Teams to integrate with external apps.</span></span> <span data-ttu-id="2db8f-111">Avec les webhooks sortants, vous pouvez envoyer des messages texte à partir d’un canal aux services web.</span><span class="sxs-lookup"><span data-stu-id="2db8f-111">With Outgoing Webhooks, you can send text messages from a channel to the web services.</span></span> <span data-ttu-id="2db8f-112">Après avoir configuré les webhooks sortants, les utilisateurs peuvent @mention webhook sortant et envoyer un message aux services web.</span><span class="sxs-lookup"><span data-stu-id="2db8f-112">After configuring the Outgoing Webhooks, users can @mention Outgoing Webhook and send a message to web services.</span></span> <span data-ttu-id="2db8f-113">Le service répond dans les dix secondes au message avec un texte ou une carte.</span><span class="sxs-lookup"><span data-stu-id="2db8f-113">The service responds within ten seconds to the message with a text or a card.</span></span>

> [!NOTE]
> <span data-ttu-id="2db8f-114">Les webhooks sortants sont configurés par équipe et ne peuvent pas être inclus dans le cadre d’une application Teams normale.</span><span class="sxs-lookup"><span data-stu-id="2db8f-114">Outgoing Webhooks are configured on a per team basis and cannot be included as part of a normal Teams app.</span></span>

## <a name="connectors"></a><span data-ttu-id="2db8f-115">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2db8f-115">Connectors</span></span>

<span data-ttu-id="2db8f-116">Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir des notifications et des messages des services web.</span><span class="sxs-lookup"><span data-stu-id="2db8f-116">Connectors allow users to subscribe to receive notifications and messages from the web services.</span></span> <span data-ttu-id="2db8f-117">Ils exposent le point de terminaison HTTPS pour que le service publie des messages Teams canaux, généralement sous forme de cartes.</span><span class="sxs-lookup"><span data-stu-id="2db8f-117">They expose the HTTPS endpoint for the service to post messages to Teams channels, typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="2db8f-118">Webhooks entrants</span><span class="sxs-lookup"><span data-stu-id="2db8f-118">Incoming Webhooks</span></span>

<span data-ttu-id="2db8f-119">Les webhooks entrants vous aident à publier des messages à partir d’applications Teams.</span><span class="sxs-lookup"><span data-stu-id="2db8f-119">Incoming Webhooks help in posting messages from apps to Teams.</span></span> <span data-ttu-id="2db8f-120">Si les webhooks entrants sont activés pour une équipe dans un canal, il expose le point de terminaison HTTPS, qui accepte le format JSON correct et insère les messages dans ce canal.</span><span class="sxs-lookup"><span data-stu-id="2db8f-120">If Incoming Webhooks are enabled for a team in any channel, it exposes the HTTPS endpoint, which accepts correctly formatted JSON and inserts the messages into that channel.</span></span> <span data-ttu-id="2db8f-121">Par exemple, vous pouvez créer un webhook entrant dans votre canal DevOps, configurer votre build et déployer et surveiller simultanément les services pour envoyer des alertes.</span><span class="sxs-lookup"><span data-stu-id="2db8f-121">For example, you can create an Incoming Webhook in your DevOps channel, configure your build, and simultaneously deploy and monitor services to send alerts.</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="2db8f-122">Connecteurs Office 365</span><span class="sxs-lookup"><span data-stu-id="2db8f-122">Office 365 Connectors</span></span>

<span data-ttu-id="2db8f-123">Office 365 Les connecteurs vous permettent de créer une page de configuration personnalisée pour votre webhook entrant et de les créer un package dans le cadre d’Teams app.</span><span class="sxs-lookup"><span data-stu-id="2db8f-123">Office 365 Connectors allow you to create a custom configuration page for your Incoming Webhook and package them as part of a Teams app.</span></span> <span data-ttu-id="2db8f-124">Vous envoyez des messages principalement à l’aide Office 365 cartes connecteur et vous avez la possibilité d’y ajouter un ensemble limité d’actions de carte.</span><span class="sxs-lookup"><span data-stu-id="2db8f-124">You send messages primarily using Office 365 Connector cards and have the ability to add a limited set of card actions to them.</span></span> <span data-ttu-id="2db8f-125">Par exemple, un connecteur météo qui permet aux utilisateurs de sélectionner un emplacement et une heure de la journée, pour recevoir des mises à jour sur la météo de demain.</span><span class="sxs-lookup"><span data-stu-id="2db8f-125">For example, a weather connector that allows users to select a location and time of day, to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="2db8f-126">Ils sont configurés au niveau du canal, mais sont installés au niveau de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="2db8f-126">They are configured on a channel level but are installed at a team level.</span></span>

> [!NOTE]
> <span data-ttu-id="2db8f-127">Vous pouvez distribuer l’application Office 365 Connector Teams à notre AppStore.</span><span class="sxs-lookup"><span data-stu-id="2db8f-127">You can distribute the Office 365 Connector Teams app to our AppStore.</span></span>

## <a name="create-and-send-messages"></a><span data-ttu-id="2db8f-128">Créer et envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="2db8f-128">Create and send messages</span></span>

<span data-ttu-id="2db8f-129">Les messages actionnables permettent aux utilisateurs d’agir sans quitter leur client de messagerie, ce qui augmente l’implication des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2db8f-129">Actionable messages allow users to take action without leaving their email client, increasing user engagement.</span></span> <span data-ttu-id="2db8f-130">Avec Office 365 webhooks entrants, vous pouvez envoyer des messages en publiant une charge utile JSON sur l’URL du webhook.</span><span class="sxs-lookup"><span data-stu-id="2db8f-130">With Office 365 and Incoming Webhooks, you can send messages by posting a JSON payload to the webhook URL.</span></span>

## <a name="see-also"></a><span data-ttu-id="2db8f-131">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2db8f-131">See also</span></span>

* [<span data-ttu-id="2db8f-132">Créer un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="2db8f-132">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="2db8f-133">Créer un connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="2db8f-133">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="2db8f-134">Créer et envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="2db8f-134">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="next-step"></a><span data-ttu-id="2db8f-135">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="2db8f-135">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2db8f-136">Créer un webhook sortant</span><span class="sxs-lookup"><span data-stu-id="2db8f-136">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
