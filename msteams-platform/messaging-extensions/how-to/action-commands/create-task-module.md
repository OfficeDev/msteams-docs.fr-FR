---
title: Créer et envoyer le module de tâches
author: clearab
description: Comment gérer l’action d’appel initiale et répondre avec un module de tâche à partir d’une commande d’extension de messagerie d’action
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072874"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="b43af-103">Créer et envoyer le module de tâches</span><span class="sxs-lookup"><span data-stu-id="b43af-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="b43af-104">Si vous ne remplissez pas le module de tâche avec les paramètres définis dans le manifeste de l’application, vous devez créer le module de tâche pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b43af-104">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users.</span></span> <span data-ttu-id="b43af-105">Utilisez une carte adaptative ou un affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-105">Use either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="b43af-106">Demande d’appel initiale</span><span class="sxs-lookup"><span data-stu-id="b43af-106">The initial invoke request</span></span>

<span data-ttu-id="b43af-107">À l’aide de cette méthode, votre service reçoit un objet de type et vous devez répondre avec un objet contenant la carte adaptative ou une URL vers `Activity` `composeExtension/fetchTask` l’affichage web `task` incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-107">Using this method your service will receive an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either the adaptive card or a URL to the embedded web view.</span></span> <span data-ttu-id="b43af-108">Avec les propriétés d’activité standard du bot, la charge utile d’appel initiale contient les métadonnées de requête suivantes :</span><span class="sxs-lookup"><span data-stu-id="b43af-108">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="b43af-109">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="b43af-109">Property name</span></span>|<span data-ttu-id="b43af-110">Objectif</span><span class="sxs-lookup"><span data-stu-id="b43af-110">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="b43af-111">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-111">Type of request.</span></span> <span data-ttu-id="b43af-112">Il doit `invoke` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-112">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="b43af-113">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b43af-113">Type of command that is issued to your service.</span></span> <span data-ttu-id="b43af-114">Il doit `composeExtension/fetchTask` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-114">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="b43af-115">ID de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-115">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="b43af-116">Nom de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-116">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="b43af-117">ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-117">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="b43af-118">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b43af-118">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="b43af-119">ID de canal (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="b43af-119">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="b43af-120">ID d’équipe (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="b43af-120">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="b43af-121">Contient l’ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="b43af-121">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="b43af-122">Contexte qui a déclenché l’événement.</span><span class="sxs-lookup"><span data-stu-id="b43af-122">The context that triggered the event.</span></span> <span data-ttu-id="b43af-123">Il doit `compose` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-123">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="b43af-124">Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-124">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="b43af-125">Il doit `default` s’y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="b43af-125">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a><span data-ttu-id="b43af-126">Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’une conversation 1:1 sont répertoriées dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="b43af-126">Payload activity properties when invoked a task module from 1:1 chat are listed in the following section:</span></span>

|<span data-ttu-id="b43af-127">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="b43af-127">Property name</span></span>|<span data-ttu-id="b43af-128">Objectif</span><span class="sxs-lookup"><span data-stu-id="b43af-128">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="b43af-129">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-129">Type of request.</span></span> <span data-ttu-id="b43af-130">Il doit `invoke` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-130">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="b43af-131">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b43af-131">Type of command that is issued to your service.</span></span> <span data-ttu-id="b43af-132">Il doit `composeExtension/fetchTask` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-132">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="b43af-133">ID de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-133">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="b43af-134">Nom de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-134">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="b43af-135">ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-135">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="b43af-136">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b43af-136">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="b43af-137">Nom source de l’endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="b43af-137">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="b43af-138">Obtient ou définit l’ID du message auquel ce message est une réponse.</span><span class="sxs-lookup"><span data-stu-id="b43af-138">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="b43af-139">Contient l’ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="b43af-139">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="b43af-140">Contexte qui a déclenché l’événement.</span><span class="sxs-lookup"><span data-stu-id="b43af-140">The context that triggered the event.</span></span> <span data-ttu-id="b43af-141">Il doit `compose` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-141">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="b43af-142">Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-142">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="b43af-143">Il doit `default` s’y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="b43af-143">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a><span data-ttu-id="b43af-144">Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’une conversation de groupe sont répertoriées dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="b43af-144">Payload activity properties when invoked a task module from a group chat are listed in the following section:</span></span>

|<span data-ttu-id="b43af-145">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="b43af-145">Property name</span></span>|<span data-ttu-id="b43af-146">Objectif</span><span class="sxs-lookup"><span data-stu-id="b43af-146">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="b43af-147">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-147">Type of request.</span></span> <span data-ttu-id="b43af-148">Il doit `invoke` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-148">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="b43af-149">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b43af-149">Type of command that is issued to your service.</span></span> <span data-ttu-id="b43af-150">Il doit `composeExtension/fetchTask` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-150">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="b43af-151">ID de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-151">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="b43af-152">Nom de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-152">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="b43af-153">ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-153">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="b43af-154">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b43af-154">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="b43af-155">Nom source de l’endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="b43af-155">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="b43af-156">Obtient ou définit l’ID du message auquel ce message est une réponse.</span><span class="sxs-lookup"><span data-stu-id="b43af-156">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="b43af-157">Contient l’ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="b43af-157">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="b43af-158">Contexte qui a déclenché l’événement.</span><span class="sxs-lookup"><span data-stu-id="b43af-158">The context that triggered the event.</span></span> <span data-ttu-id="b43af-159">Il doit `compose` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-159">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="b43af-160">Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-160">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="b43af-161">Il doit `default` s’y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="b43af-161">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a><span data-ttu-id="b43af-162">Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’un canal (nouveau billet) sont répertoriées dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="b43af-162">Payload activity properties when invoked a task module from a channel (new post) are listed in the following section:</span></span>

|<span data-ttu-id="b43af-163">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="b43af-163">Property name</span></span>|<span data-ttu-id="b43af-164">Objectif</span><span class="sxs-lookup"><span data-stu-id="b43af-164">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="b43af-165">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-165">Type of request.</span></span> <span data-ttu-id="b43af-166">Il doit `invoke` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-166">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="b43af-167">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b43af-167">Type of command that is issued to your service.</span></span> <span data-ttu-id="b43af-168">Il doit `composeExtension/fetchTask` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-168">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="b43af-169">ID de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-169">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="b43af-170">Nom de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-170">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="b43af-171">ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-171">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="b43af-172">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b43af-172">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="b43af-173">ID de canal (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="b43af-173">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="b43af-174">ID d’équipe (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="b43af-174">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="b43af-175">Nom source de l’endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="b43af-175">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="b43af-176">Obtient ou définit l’ID du message auquel ce message est une réponse.</span><span class="sxs-lookup"><span data-stu-id="b43af-176">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="b43af-177">Contient l’ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="b43af-177">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="b43af-178">Contexte qui a déclenché l’événement.</span><span class="sxs-lookup"><span data-stu-id="b43af-178">The context that triggered the event.</span></span> <span data-ttu-id="b43af-179">Il doit `compose` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-179">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="b43af-180">Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-180">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="b43af-181">Il doit `default` s’y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="b43af-181">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a><span data-ttu-id="b43af-182">Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’un canal (réponse au thread) sont répertoriées dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="b43af-182">Payload activity properties when invoked a task module from a channel (reply to thread) are listed in the following section:</span></span>

|<span data-ttu-id="b43af-183">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="b43af-183">Property name</span></span>|<span data-ttu-id="b43af-184">Objectif</span><span class="sxs-lookup"><span data-stu-id="b43af-184">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="b43af-185">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-185">Type of request.</span></span> <span data-ttu-id="b43af-186">Il doit `invoke` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-186">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="b43af-187">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b43af-187">Type of command that is issued to your service.</span></span> <span data-ttu-id="b43af-188">Il doit `composeExtension/fetchTask` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-188">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="b43af-189">ID de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-189">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="b43af-190">Nom de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-190">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="b43af-191">ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-191">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="b43af-192">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b43af-192">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="b43af-193">ID de canal (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="b43af-193">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="b43af-194">ID d’équipe (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="b43af-194">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="b43af-195">Nom source de l’endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="b43af-195">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="b43af-196">Obtient ou définit l’ID du message auquel ce message est une réponse.</span><span class="sxs-lookup"><span data-stu-id="b43af-196">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="b43af-197">Contient l’ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="b43af-197">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="b43af-198">Contexte qui a déclenché l’événement.</span><span class="sxs-lookup"><span data-stu-id="b43af-198">The context that triggered the event.</span></span> <span data-ttu-id="b43af-199">Il doit `compose` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-199">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="b43af-200">Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-200">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="b43af-201">Il doit `default` s’y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="b43af-201">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a><span data-ttu-id="b43af-202">Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’une zone de commande sont répertoriées dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="b43af-202">Payload activity properties when invoked a task module from a command box are listed in the following section:</span></span>

|<span data-ttu-id="b43af-203">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="b43af-203">Property name</span></span>|<span data-ttu-id="b43af-204">Objectif</span><span class="sxs-lookup"><span data-stu-id="b43af-204">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="b43af-205">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-205">Type of request.</span></span> <span data-ttu-id="b43af-206">Il doit `invoke` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-206">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="b43af-207">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b43af-207">Type of command that is issued to your service.</span></span> <span data-ttu-id="b43af-208">Il doit `composeExtension/fetchTask` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-208">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="b43af-209">ID de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-209">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="b43af-210">Nom de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-210">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="b43af-211">ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="b43af-211">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="b43af-212">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b43af-212">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="b43af-213">Nom source de l’endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="b43af-213">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="b43af-214">Contient l’ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="b43af-214">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="b43af-215">Contexte qui a déclenché l’événement.</span><span class="sxs-lookup"><span data-stu-id="b43af-215">The context that triggered the event.</span></span> <span data-ttu-id="b43af-216">Il doit `compose` l’être.</span><span class="sxs-lookup"><span data-stu-id="b43af-216">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="b43af-217">Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-217">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="b43af-218">Il doit `default` s’y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="b43af-218">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example-fetchtask-request"></a><span data-ttu-id="b43af-219">Exemple de requête fetchTask</span><span class="sxs-lookup"><span data-stu-id="b43af-219">Example fetchTask request</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b43af-220">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b43af-220">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="b43af-221">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b43af-221">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="b43af-222">JSON</span><span class="sxs-lookup"><span data-stu-id="b43af-222">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="b43af-223">Demande d’appel initiale à partir d’un message</span><span class="sxs-lookup"><span data-stu-id="b43af-223">Initial invoke request from a message</span></span>

<span data-ttu-id="b43af-224">Lorsque votre bot est appelé à partir d’un message plutôt que de la zone de composition ou de la barre de commandes, l’objet de la demande initiale doit contenir les détails du message à partir de quel message votre extension de messagerie est `value` invoquée.</span><span class="sxs-lookup"><span data-stu-id="b43af-224">When your bot is invoked from a message rather than the compose area or the command bar, the `value` object in the initial request must contain the details of the message your messaging extension is invoked from.</span></span> <span data-ttu-id="b43af-225">Consultez la section suivante pour obtenir l’exemple de cet objet.</span><span class="sxs-lookup"><span data-stu-id="b43af-225">See the following section  for the example of this object .</span></span> <span data-ttu-id="b43af-226">Les tableaux et les tableaux sont facultatifs et ne sont pas présents s’il n’y a aucune réaction ou `reactions` mention dans le message `mentions` d’origine.</span><span class="sxs-lookup"><span data-stu-id="b43af-226">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b43af-227">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b43af-227">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="b43af-228">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b43af-228">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="b43af-229">JSON</span><span class="sxs-lookup"><span data-stu-id="b43af-229">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="b43af-230">Répondre à la tâche fetchTask</span><span class="sxs-lookup"><span data-stu-id="b43af-230">Respond to the fetchTask</span></span>

<span data-ttu-id="b43af-231">Répondez à la demande d’appel avec un objet qui contient un objet avec la carte adaptative ou l’URL web, ou `task` un message de chaîne `taskInfo` simple.</span><span class="sxs-lookup"><span data-stu-id="b43af-231">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the adaptive card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="b43af-232">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="b43af-232">Property name</span></span>|<span data-ttu-id="b43af-233">Objectif</span><span class="sxs-lookup"><span data-stu-id="b43af-233">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="b43af-234">Il peut `continue` s’agit de présenter un formulaire ou `message` d’utiliser une fenêtre popup simple.</span><span class="sxs-lookup"><span data-stu-id="b43af-234">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="b43af-235">Objet `taskInfo` d’un formulaire ou `string` d’un message.</span><span class="sxs-lookup"><span data-stu-id="b43af-235">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="b43af-236">Le schéma de l’objet taskInfo est :</span><span class="sxs-lookup"><span data-stu-id="b43af-236">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="b43af-237">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="b43af-237">Property name</span></span>|<span data-ttu-id="b43af-238">Objectif</span><span class="sxs-lookup"><span data-stu-id="b43af-238">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="b43af-239">Titre du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="b43af-239">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="b43af-240">Il doit s’agit d’un nombre integer (en pixels) `small` ou , ou , `medium` `large` .</span><span class="sxs-lookup"><span data-stu-id="b43af-240">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="b43af-241">Il doit s’agit d’un nombre integer (en pixels) `small` ou , ou , `medium` `large` .</span><span class="sxs-lookup"><span data-stu-id="b43af-241">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="b43af-242">Carte adaptative définissant le formulaire (si vous en utilisez un).</span><span class="sxs-lookup"><span data-stu-id="b43af-242">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="b43af-243">URL à ouvrir dans le module de tâche en tant qu’affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-243">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="b43af-244">Si un client ne prend pas en charge la fonctionnalité de module de tâche, cette URL est ouverte dans un onglet de navigateur.</span><span class="sxs-lookup"><span data-stu-id="b43af-244">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="with-an-adaptive-card"></a><span data-ttu-id="b43af-245">Avec une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="b43af-245">With an adaptive card</span></span>

<span data-ttu-id="b43af-246">Lorsque vous utilisez une carte adaptative, vous devez répondre avec un objet contenant `task` `value` une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="b43af-246">When using an adaptive card, you must respond with a `task` object with the `value` object containing an adaptive card.</span></span>

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a><span data-ttu-id="b43af-247">Exemple de réponse fetchTask avec une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="b43af-247">Example fetchTask response with an adaptive card</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b43af-248">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b43af-248">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="b43af-249">Cet exemple utilise le [package NuGet AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) en plus du SDK Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b43af-249">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="b43af-250">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b43af-250">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[<span data-ttu-id="b43af-251">JSON</span><span class="sxs-lookup"><span data-stu-id="b43af-251">JSON</span></span>](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a><span data-ttu-id="b43af-252">Avec un affichage web incorporé</span><span class="sxs-lookup"><span data-stu-id="b43af-252">With an embedded web view</span></span>

<span data-ttu-id="b43af-253">Lorsque vous utilisez un affichage web incorporé, vous devez répondre avec un objet avec l’objet contenant l’URL du formulaire web que vous `task` `value` souhaitez charger.</span><span class="sxs-lookup"><span data-stu-id="b43af-253">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form you'd like to load.</span></span> <span data-ttu-id="b43af-254">Les domaines d’une URL que vous souhaitez charger doivent être inclus dans le tableau dans le manifeste `validDomains` de votre application.</span><span class="sxs-lookup"><span data-stu-id="b43af-254">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="b43af-255">Consultez la [documentation du module de](~/task-modules-and-cards/what-are-task-modules.md) tâche pour obtenir des informations complètes sur la création de votre affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43af-255">See the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md) for complete information on building your embedded web view.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b43af-256">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b43af-256">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="b43af-257">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b43af-257">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[<span data-ttu-id="b43af-258">JSON</span><span class="sxs-lookup"><span data-stu-id="b43af-258">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="b43af-259">Demande d’installation de votre bot de conversation</span><span class="sxs-lookup"><span data-stu-id="b43af-259">Request to install your conversational bot</span></span>

<span data-ttu-id="b43af-260">Si l’application contient un bot de conversation, installez-le dans la conversation avant de charger le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="b43af-260">If the app contains a conversational bot, install the bot in the conversation before loading the task module.</span></span> <span data-ttu-id="b43af-261">Il est utile d’obtenir un contexte supplémentaire pour le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="b43af-261">It is useful to get additional context for the task module.</span></span> <span data-ttu-id="b43af-262">L’exemple type de ce scénario consiste à extraire la liste de membres pour remplir un contrôle de s picker de personnes ou la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="b43af-262">Typical example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="b43af-263">Lorsque l’extension de messagerie reçoit l’appel, vérifiez si le bot est installé dans le contexte actuel `composeExtension/fetchTask` pour faciliter le flux.</span><span class="sxs-lookup"><span data-stu-id="b43af-263">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="b43af-264">Par exemple, vérifiez le flux avec un appel d’obtenir une liste de membres.</span><span class="sxs-lookup"><span data-stu-id="b43af-264">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="b43af-265">Si le bot n’est pas installé, renvoyer une carte adaptative avec une action qui demande à l’utilisateur d’installer le bot.</span><span class="sxs-lookup"><span data-stu-id="b43af-265">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="b43af-266">Voir l’action dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="b43af-266">See the action in the following example.</span></span> <span data-ttu-id="b43af-267">L’utilisateur doit être autorisé à installer les applications à cet emplacement pour vérification.</span><span class="sxs-lookup"><span data-stu-id="b43af-267">The user must have permission to install the apps in that location for checking.</span></span> <span data-ttu-id="b43af-268">Si l’installation de l’application échoue, l’utilisateur reçoit un message pour contacter l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b43af-268">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example-of-the-response"></a><span data-ttu-id="b43af-269">Exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="b43af-269">Example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="b43af-270">Après l’installation, le bot reçoit un autre message d’appel avec `name = composeExtension/submitAction` , et `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="b43af-270">After the installation, the bot receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example-of-the-invoke"></a><span data-ttu-id="b43af-271">Exemple d’appel :</span><span class="sxs-lookup"><span data-stu-id="b43af-271">Example of the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="b43af-272">La réponse à la tâche à l’appel doit être similaire à celle du bot installé.</span><span class="sxs-lookup"><span data-stu-id="b43af-272">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a><span data-ttu-id="b43af-273">Exemple d’installation juste-à-temps de l’application avec carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="b43af-273">Example of just-in time installation of app with Adaptive card:</span></span> 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="next-steps"></a><span data-ttu-id="b43af-274">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b43af-274">Next steps</span></span>

<span data-ttu-id="b43af-275">Si vous autorisez vos utilisateurs à renvoyer une réponse à partir du module de tâche, vous devez gérer l’action d’envoi.</span><span class="sxs-lookup"><span data-stu-id="b43af-275">If you allow your users to send a response back from the task module, you must handle the submit action.</span></span>

* [<span data-ttu-id="b43af-276">Créer et répondre avec un module de tâche</span><span class="sxs-lookup"><span data-stu-id="b43af-276">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
