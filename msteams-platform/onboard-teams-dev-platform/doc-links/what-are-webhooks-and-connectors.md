---
title: Qu’est-ce qu’un webhooks et un connecteur ?
author: clearab
description: Découvrez comment les webhooks et les connecteurs peuvent connecter vos services Web au client Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651937"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="1a03d-103">Qu’est-ce qu’un webhooks et un connecteur ?</span><span class="sxs-lookup"><span data-stu-id="1a03d-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="1a03d-104">Les webhooks et les connecteurs sont des méthodes simples pour connecter des systèmes et des services externes avec des canaux et des conversations Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1a03d-104">Webhooks and connectors are straightforward ways to connect external systems and services with Microsoft Teams channels and chats.</span></span>

<span data-ttu-id="1a03d-105">Les utilisateurs peuvent, par exemple, s’abonner à des notifications à partir d’une autre application (généralement sous la forme de cartes).</span><span class="sxs-lookup"><span data-stu-id="1a03d-105">Users can, for example, subscribe to notifications from another app (typically in the form of cards).</span></span>

## <a name="incoming-webhooks"></a><span data-ttu-id="1a03d-106">Webhooks entrants</span><span class="sxs-lookup"><span data-stu-id="1a03d-106">Incoming webhooks</span></span>

<span data-ttu-id="1a03d-107">Les webhooks entrants constituent le type de connecteur le plus simple, ainsi qu’un moyen rapide et simple de connecter le canal d’une équipe à un service externe.</span><span class="sxs-lookup"><span data-stu-id="1a03d-107">Incoming webhooks are the simplest type of connector and a quick and easy way to connect a team's channel to an external service.</span></span> <span data-ttu-id="1a03d-108">Pour n’importe quel canal (s’il est activé pour cette équipe), vous pouvez exposer un point de terminaison HTTPs qui accepte le format JSON correctement mis en forme et insérer des messages dans le canal.</span><span class="sxs-lookup"><span data-stu-id="1a03d-108">For any channel (if enabled for that team), you can expose an HTTPS endpoint that accepts correctly formatted JSON and insert messages into the channel.</span></span>

<span data-ttu-id="1a03d-109">Consultez la rubrique [créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="1a03d-109">See [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="1a03d-110">Scénarios utilisateur</span><span class="sxs-lookup"><span data-stu-id="1a03d-110">User scenarios</span></span>

<span data-ttu-id="1a03d-111">Les webhooks entrants conviennent mieux aux scénarios spécifiques à une équipe particulière.</span><span class="sxs-lookup"><span data-stu-id="1a03d-111">Incoming webhooks are best for scenarios unique to a particular team.</span></span> <span data-ttu-id="1a03d-112">Par exemple, vous pouvez créer un webhook entrant dans votre canal DevOps et configurer vos services de génération, de déploiement et de surveillance pour envoyer des alertes.</span><span class="sxs-lookup"><span data-stu-id="1a03d-112">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment, and monitoring services to send alerts.</span></span>

## <a name="office-365-connectors"></a><span data-ttu-id="1a03d-113">Connecteurs Office 365</span><span class="sxs-lookup"><span data-stu-id="1a03d-113">Office 365 Connectors</span></span>

<span data-ttu-id="1a03d-114">Un connecteur Office 365 vous permet de créer une page de configuration personnalisée pour le webhook entrant et de l’empaqueter dans le cadre d’une application Teams.</span><span class="sxs-lookup"><span data-stu-id="1a03d-114">An Office 365 Connector allows you to create a custom configuration page for your incoming webhook and package it as part of a Teams app.</span></span> <span data-ttu-id="1a03d-115">Vous pouvez ensuite distribuer cette application plus largement ou même dans notre magasin d’applications.</span><span class="sxs-lookup"><span data-stu-id="1a03d-115">You can then distribute that app more broadly or even to our app store.</span></span> <span data-ttu-id="1a03d-116">Vous envoyez des messages principalement à l’aide de cartes de connecteur Office 365 qui peuvent également disposer d’un ensemble limité d’actions de carte.</span><span class="sxs-lookup"><span data-stu-id="1a03d-116">You send messages primarily using Office 365 Connector cards that can also have a limited set of card actions.</span></span> <span data-ttu-id="1a03d-117">Ils sont configurés au niveau du canal mais installés au niveau de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="1a03d-117">They are configured on the channel level but installed at the team level.</span></span>

<span data-ttu-id="1a03d-118">Voir [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span><span class="sxs-lookup"><span data-stu-id="1a03d-118">See [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="1a03d-119">Scénarios utilisateur</span><span class="sxs-lookup"><span data-stu-id="1a03d-119">User scenarios</span></span>

<span data-ttu-id="1a03d-120">Un connecteur météo qui vous permet de choisir un emplacement et une heure de réception des mises à jour de la prévision de demain.</span><span class="sxs-lookup"><span data-stu-id="1a03d-120">A weather connector that lets you choose a location and time of day to receive updates about tomorrow's forecast.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="1a03d-121">Webhooks sortants</span><span class="sxs-lookup"><span data-stu-id="1a03d-121">Outgoing webhooks</span></span>

<span data-ttu-id="1a03d-122">Les webhooks sortants permettent à vos utilisateurs d’envoyer des messages texte d’un canal vers vos services web.</span><span class="sxs-lookup"><span data-stu-id="1a03d-122">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="1a03d-123">Une fois configurés, les utilisateurs peuvent @mention votre application et envoyer un message à votre service externe.</span><span class="sxs-lookup"><span data-stu-id="1a03d-123">Once configured, users can @mention your app and send a message to your external service.</span></span> <span data-ttu-id="1a03d-124">Votre service dispose de cinq secondes pour envoyer une réponse au message, contenant potentiellement du texte ou une carte.</span><span class="sxs-lookup"><span data-stu-id="1a03d-124">Your service has five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="1a03d-125">Les webhooks sortants sont configurés en fonction de chaque équipe et ne peuvent pas être inclus dans une application teams normale.</span><span class="sxs-lookup"><span data-stu-id="1a03d-125">Outgoing webhooks are configured on a per-team basis and can't be included as part of a normal Teams app.</span></span>

<span data-ttu-id="1a03d-126">Consultez la rubrique [créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="1a03d-126">See [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="1a03d-127">Scénarios utilisateur</span><span class="sxs-lookup"><span data-stu-id="1a03d-127">User scenarios</span></span>

<span data-ttu-id="1a03d-128">Les webhooks sortants conviennent mieux à la réalisation de flux de travail spécifiques à une équipe qui ne nécessitent pas de collecter ou d’échanger de grandes quantités d’informations.</span><span class="sxs-lookup"><span data-stu-id="1a03d-128">Outgoing webhooks are best suited for completing team-specific workflows that don't require collecting or exchanging large amounts of information.</span></span>

## <a name="learn-more"></a><span data-ttu-id="1a03d-129">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="1a03d-129">Learn more</span></span>

* [<span data-ttu-id="1a03d-130">Planification de votre application</span><span class="sxs-lookup"><span data-stu-id="1a03d-130">Planning your app</span></span>](../../concepts/extensibility-points.md)
* [<span data-ttu-id="1a03d-131">Création de votre application</span><span class="sxs-lookup"><span data-stu-id="1a03d-131">Building your app</span></span>](../../concepts/building-an-app.md)
* [<span data-ttu-id="1a03d-132">Publication de votre application</span><span class="sxs-lookup"><span data-stu-id="1a03d-132">Publishing your app</span></span>](../../concepts/deploy-and-publish/overview.md)
