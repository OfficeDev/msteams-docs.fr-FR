---
title: Créer et envoyer le module de tâches
author: clearab
description: Comment gérer l'action d'appel initiale et répondre avec un module de tâche à partir d'une commande d'extension de messagerie d'action
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fbe90b3a3af8dbb053fdbaf6b4cd9b96344eaf00
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075590"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="12d44-103">Créer et envoyer le module de tâches</span><span class="sxs-lookup"><span data-stu-id="12d44-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="12d44-104">Vous pouvez créer le module de tâche à l'aide d'une carte adaptative ou d'un affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-104">You can create the task module using an Adaptive Card or an embedded web view.</span></span> <span data-ttu-id="12d44-105">Pour créer un module de tâche, vous devez effectuer le processus appelé demande d'appel initiale.</span><span class="sxs-lookup"><span data-stu-id="12d44-105">To create a task module, you must perform the process called the initial invoke request.</span></span> <span data-ttu-id="12d44-106">Ce document traite de la demande d'appel initiale, des propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une conversation 1:1, d'une conversation de groupe, d'un canal (nouveau billet), d'un canal (réponse au thread) et d'une zone de commande.</span><span class="sxs-lookup"><span data-stu-id="12d44-106">This document covers the initial invoke request, payload activity properties when a task module is invoked from 1:1 chat, group chat, channel (new post), channel (reply to thread), and command box.</span></span> 
> [!NOTE]
> <span data-ttu-id="12d44-107">Si vous ne remplissez pas le module de tâche avec des paramètres définis dans le manifeste de l'application, vous devez créer le module de tâche pour les utilisateurs avec une carte adaptative ou un affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-107">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users with either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="12d44-108">Demande d'appel initiale</span><span class="sxs-lookup"><span data-stu-id="12d44-108">The initial invoke request</span></span>

<span data-ttu-id="12d44-109">Dans le processus de la demande d'appel initiale, votre service reçoit un objet de type et vous devez répondre avec un objet contenant une carte adaptative ou une URL vers l'affichage `Activity` `composeExtension/fetchTask` web `task` incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-109">In the process of the initial invoke request, your service receives an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either an Adaptive Card or a URL to the embedded web view.</span></span> <span data-ttu-id="12d44-110">En plus des propriétés d'activité standard du bot, la charge utile d'appel initiale contient les métadonnées de requête suivantes :</span><span class="sxs-lookup"><span data-stu-id="12d44-110">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="12d44-111">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="12d44-111">Property name</span></span>|<span data-ttu-id="12d44-112">Objectif</span><span class="sxs-lookup"><span data-stu-id="12d44-112">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="12d44-113">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-113">Type of request.</span></span> <span data-ttu-id="12d44-114">Il doit `invoke` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-114">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="12d44-115">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="12d44-115">Type of command that is issued to your service.</span></span> <span data-ttu-id="12d44-116">Il doit `composeExtension/fetchTask` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-116">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="12d44-117">ID de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-117">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="12d44-118">Nom de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-118">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="12d44-119">Azure Active Directory'ID d'objet de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-119">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="12d44-120">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12d44-120">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="12d44-121">ID de canal (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="12d44-121">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="12d44-122">ID d'équipe (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="12d44-122">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="12d44-123">Contient l'ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="12d44-123">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="12d44-124">Contexte qui a déclenché l'événement.</span><span class="sxs-lookup"><span data-stu-id="12d44-124">The context that triggered the event.</span></span> <span data-ttu-id="12d44-125">Il doit `compose` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-125">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="12d44-126">Thème client de l'utilisateur, utile pour la mise en forme de l'affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-126">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="12d44-127">Il doit `default` s'y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="12d44-127">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="12d44-128">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-128">Example</span></span>

<span data-ttu-id="12d44-129">Le code de la demande d'appel initiale est donné dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="12d44-129">The code for the initial invoke request is given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a><span data-ttu-id="12d44-130">Propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une conversation 1:1</span><span class="sxs-lookup"><span data-stu-id="12d44-130">Payload activity properties when a task module is invoked from 1:1 chat</span></span> 

<span data-ttu-id="12d44-131">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une conversation 1:1 sont répertoriées comme suit :</span><span class="sxs-lookup"><span data-stu-id="12d44-131">The payload activity properties when a task module is invoked from 1:1 chat are listed as follows:</span></span>

|<span data-ttu-id="12d44-132">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="12d44-132">Property name</span></span>|<span data-ttu-id="12d44-133">Objectif</span><span class="sxs-lookup"><span data-stu-id="12d44-133">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="12d44-134">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-134">Type of request.</span></span> <span data-ttu-id="12d44-135">Il doit `invoke` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-135">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="12d44-136">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="12d44-136">Type of command that is issued to your service.</span></span> <span data-ttu-id="12d44-137">Il doit `composeExtension/fetchTask` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-137">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="12d44-138">ID de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-138">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="12d44-139">Nom de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-139">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="12d44-140">Azure Active Directory'ID d'objet de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-140">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="12d44-141">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12d44-141">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="12d44-142">Nom source de l'endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="12d44-142">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="12d44-143">Obtient ou définit l'ID du message auquel ce message est une réponse.</span><span class="sxs-lookup"><span data-stu-id="12d44-143">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="12d44-144">Contient l'ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="12d44-144">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="12d44-145">Contexte qui a déclenché l'événement.</span><span class="sxs-lookup"><span data-stu-id="12d44-145">The context that triggered the event.</span></span> <span data-ttu-id="12d44-146">Il doit `compose` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-146">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="12d44-147">Thème client de l'utilisateur, utile pour la mise en forme de l'affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-147">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="12d44-148">Il doit `default` s'y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="12d44-148">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="12d44-149">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-149">Example</span></span>

<span data-ttu-id="12d44-150">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une conversation 1:1 sont données dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="12d44-150">The payload activity properties when a task module is invoked from 1:1 chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```
## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a><span data-ttu-id="12d44-151">Propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une conversation de groupe</span><span class="sxs-lookup"><span data-stu-id="12d44-151">Payload activity properties when a task module is invoked from a group chat</span></span> 

<span data-ttu-id="12d44-152">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une conversation de groupe sont répertoriées comme suit :</span><span class="sxs-lookup"><span data-stu-id="12d44-152">The payload activity properties when a task module is invoked from a group chat are listed as follows:</span></span>

|<span data-ttu-id="12d44-153">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="12d44-153">Property name</span></span>|<span data-ttu-id="12d44-154">Objectif</span><span class="sxs-lookup"><span data-stu-id="12d44-154">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="12d44-155">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-155">Type of request.</span></span> <span data-ttu-id="12d44-156">Il doit `invoke` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-156">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="12d44-157">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="12d44-157">Type of command that is issued to your service.</span></span> <span data-ttu-id="12d44-158">Il doit `composeExtension/fetchTask` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-158">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="12d44-159">ID de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-159">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="12d44-160">Nom de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-160">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="12d44-161">Azure Active Directory'ID d'objet de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-161">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="12d44-162">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12d44-162">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="12d44-163">Nom source de l'endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="12d44-163">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="12d44-164">Obtient ou définit l'ID du message auquel ce message est une réponse.</span><span class="sxs-lookup"><span data-stu-id="12d44-164">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="12d44-165">Contient l'ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="12d44-165">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="12d44-166">Contexte qui a déclenché l'événement.</span><span class="sxs-lookup"><span data-stu-id="12d44-166">The context that triggered the event.</span></span> <span data-ttu-id="12d44-167">Il doit `compose` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-167">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="12d44-168">Thème client de l'utilisateur, utile pour la mise en forme de l'affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-168">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="12d44-169">Il doit `default` s'y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="12d44-169">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="12d44-170">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-170">Example</span></span>

<span data-ttu-id="12d44-171">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une conversation de groupe sont données dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="12d44-171">The payload activity properties when a task module is invoked from a group chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a><span data-ttu-id="12d44-172">Propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'un canal (nouveau billet)</span><span class="sxs-lookup"><span data-stu-id="12d44-172">Payload activity properties when a task module is invoked from a channel (new post)</span></span> 

<span data-ttu-id="12d44-173">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'un canal (nouveau billet) sont répertoriées comme suit :</span><span class="sxs-lookup"><span data-stu-id="12d44-173">The payload activity properties when a task module is invoked from a channel (new post) are listed as follows:</span></span>

|<span data-ttu-id="12d44-174">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="12d44-174">Property name</span></span>|<span data-ttu-id="12d44-175">Objectif</span><span class="sxs-lookup"><span data-stu-id="12d44-175">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="12d44-176">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-176">Type of request.</span></span> <span data-ttu-id="12d44-177">Il doit `invoke` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-177">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="12d44-178">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="12d44-178">Type of command that is issued to your service.</span></span> <span data-ttu-id="12d44-179">Il doit `composeExtension/fetchTask` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-179">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="12d44-180">ID de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-180">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="12d44-181">Nom de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-181">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="12d44-182">Azure Active Directory'ID d'objet de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-182">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="12d44-183">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12d44-183">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="12d44-184">ID de canal (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="12d44-184">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="12d44-185">ID d'équipe (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="12d44-185">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="12d44-186">Nom source de l'endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="12d44-186">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="12d44-187">Obtient ou définit l'ID du message auquel ce message est une réponse.</span><span class="sxs-lookup"><span data-stu-id="12d44-187">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="12d44-188">Contient l'ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="12d44-188">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="12d44-189">Contexte qui a déclenché l'événement.</span><span class="sxs-lookup"><span data-stu-id="12d44-189">The context that triggered the event.</span></span> <span data-ttu-id="12d44-190">Il doit `compose` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-190">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="12d44-191">Thème client de l'utilisateur, utile pour la mise en forme de l'affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-191">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="12d44-192">Elle doit être `default` , `contrast` ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="12d44-192">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="12d44-193">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-193">Example</span></span>

<span data-ttu-id="12d44-194">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'un canal (nouveau billet) sont données dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="12d44-194">The payload activity properties when a task module is invoked from a channel (new post) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a><span data-ttu-id="12d44-195">Propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'un canal (réponse au thread)</span><span class="sxs-lookup"><span data-stu-id="12d44-195">Payload activity properties when a task module is invoked from a channel (reply to thread)</span></span> 

<span data-ttu-id="12d44-196">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'un canal (réponse au thread) sont répertoriées comme suit :</span><span class="sxs-lookup"><span data-stu-id="12d44-196">The payload activity properties when a task module is invoked from a channel (reply to thread) are listed as follows:</span></span>

|<span data-ttu-id="12d44-197">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="12d44-197">Property name</span></span>|<span data-ttu-id="12d44-198">Objectif</span><span class="sxs-lookup"><span data-stu-id="12d44-198">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="12d44-199">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-199">Type of request.</span></span> <span data-ttu-id="12d44-200">Il doit `invoke` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-200">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="12d44-201">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="12d44-201">Type of command that is issued to your service.</span></span> <span data-ttu-id="12d44-202">Il doit `composeExtension/fetchTask` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-202">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="12d44-203">ID de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-203">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="12d44-204">Nom de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-204">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="12d44-205">Azure Active Directory'ID d'objet de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-205">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="12d44-206">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12d44-206">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="12d44-207">ID de canal (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="12d44-207">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="12d44-208">ID d'équipe (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="12d44-208">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="12d44-209">Nom source de l'endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="12d44-209">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="12d44-210">Obtient ou définit l'ID du message auquel ce message est une réponse.</span><span class="sxs-lookup"><span data-stu-id="12d44-210">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="12d44-211">Contient l'ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="12d44-211">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="12d44-212">Contexte qui a déclenché l'événement.</span><span class="sxs-lookup"><span data-stu-id="12d44-212">The context that triggered the event.</span></span> <span data-ttu-id="12d44-213">Il doit `compose` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-213">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="12d44-214">Thème client de l'utilisateur, utile pour la mise en forme de l'affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-214">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="12d44-215">Il doit `default` s'y `contrast` trouver, ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="12d44-215">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="12d44-216">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-216">Example</span></span>

<span data-ttu-id="12d44-217">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'un canal (réponse au thread) sont données dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="12d44-217">The payload activity properties when a task module is invoked from a channel (reply to thread) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a><span data-ttu-id="12d44-218">Propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une zone de commande</span><span class="sxs-lookup"><span data-stu-id="12d44-218">Payload activity properties when a task module is invoked from a command box</span></span> 

<span data-ttu-id="12d44-219">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une zone de commande sont répertoriées comme suit :</span><span class="sxs-lookup"><span data-stu-id="12d44-219">The payload activity properties when a task module is invoked from a command box are listed as follows:</span></span>

|<span data-ttu-id="12d44-220">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="12d44-220">Property name</span></span>|<span data-ttu-id="12d44-221">Objectif</span><span class="sxs-lookup"><span data-stu-id="12d44-221">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="12d44-222">Type de demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-222">Type of request.</span></span> <span data-ttu-id="12d44-223">Il doit `invoke` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-223">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="12d44-224">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="12d44-224">Type of command that is issued to your service.</span></span> <span data-ttu-id="12d44-225">Il doit `composeExtension/fetchTask` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-225">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="12d44-226">ID de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-226">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="12d44-227">Nom de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-227">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="12d44-228">Azure Active Directory'ID d'objet de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="12d44-228">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="12d44-229">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12d44-229">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="12d44-230">Nom source de l'endroit où le module de tâche est appelé.</span><span class="sxs-lookup"><span data-stu-id="12d44-230">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="12d44-231">Contient l'ID de la commande qui a été invoquée.</span><span class="sxs-lookup"><span data-stu-id="12d44-231">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="12d44-232">Contexte qui a déclenché l'événement.</span><span class="sxs-lookup"><span data-stu-id="12d44-232">The context that triggered the event.</span></span> <span data-ttu-id="12d44-233">Il doit `compose` l'être.</span><span class="sxs-lookup"><span data-stu-id="12d44-233">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="12d44-234">Thème client de l'utilisateur, utile pour la mise en forme de l'affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-234">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="12d44-235">Elle doit être `default` , `contrast` ou `dark` .</span><span class="sxs-lookup"><span data-stu-id="12d44-235">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="12d44-236">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-236">Example</span></span>

<span data-ttu-id="12d44-237">Les propriétés de l'activité de charge utile lorsqu'un module de tâche est appelé à partir d'une zone de commande sont données dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="12d44-237">The payload activity properties when a task module is invoked from a command box are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a><span data-ttu-id="12d44-238">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-238">Example</span></span> 

<span data-ttu-id="12d44-239">La section de code suivante est un exemple de `fetchTask` requête :</span><span class="sxs-lookup"><span data-stu-id="12d44-239">The following code section is an example of `fetchTask` request:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="12d44-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="12d44-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="12d44-241">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="12d44-241">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="12d44-242">JSON</span><span class="sxs-lookup"><span data-stu-id="12d44-242">JSON</span></span>](#tab/json)

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

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="12d44-243">Demande d'appel initiale à partir d'un message</span><span class="sxs-lookup"><span data-stu-id="12d44-243">Initial invoke request from a message</span></span>

<span data-ttu-id="12d44-244">Lorsque votre bot est appelé à partir d'un message, l'objet de la demande d'appel initiale doit contenir les détails du message à partir de quel message votre extension de messagerie `value` est invoquée.</span><span class="sxs-lookup"><span data-stu-id="12d44-244">When your bot is invoked from a message,  the `value` object in the initial invoke request must contain the details of the message that your messaging extension is invoked from.</span></span> <span data-ttu-id="12d44-245">Les tableaux et les tableaux sont facultatifs et ne sont pas présents s'il n'y a aucune réaction ou `reactions` mention dans le message `mentions` d'origine.</span><span class="sxs-lookup"><span data-stu-id="12d44-245">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span> <span data-ttu-id="12d44-246">La section suivante est un exemple de `value` l'objet :</span><span class="sxs-lookup"><span data-stu-id="12d44-246">The following section is an example of the `value` object:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="12d44-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="12d44-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="12d44-248">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="12d44-248">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="12d44-249">JSON</span><span class="sxs-lookup"><span data-stu-id="12d44-249">JSON</span></span>](#tab/json)

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

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="12d44-250">Répondre à fetchTask</span><span class="sxs-lookup"><span data-stu-id="12d44-250">Respond to the fetchTask</span></span>

<span data-ttu-id="12d44-251">Répondez à la demande d'appel avec un objet qui contient un objet avec la carte adaptative ou l'URL web, ou `task` un message de chaîne `taskInfo` simple.</span><span class="sxs-lookup"><span data-stu-id="12d44-251">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the Adaptive Card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="12d44-252">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="12d44-252">Property name</span></span>|<span data-ttu-id="12d44-253">Objectif</span><span class="sxs-lookup"><span data-stu-id="12d44-253">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="12d44-254">Il peut `continue` s'agit de présenter un formulaire ou `message` d'utiliser une fenêtre popup simple.</span><span class="sxs-lookup"><span data-stu-id="12d44-254">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="12d44-255">Objet `taskInfo` d'un formulaire ou `string` d'un message.</span><span class="sxs-lookup"><span data-stu-id="12d44-255">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="12d44-256">Le schéma de l'objet taskInfo est :</span><span class="sxs-lookup"><span data-stu-id="12d44-256">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="12d44-257">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="12d44-257">Property name</span></span>|<span data-ttu-id="12d44-258">Objectif</span><span class="sxs-lookup"><span data-stu-id="12d44-258">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="12d44-259">Titre du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="12d44-259">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="12d44-260">Il doit s'agit d'un nombre integer (en pixels) `small` ou , ou , `medium` `large` .</span><span class="sxs-lookup"><span data-stu-id="12d44-260">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="12d44-261">Il doit s'agit d'un nombre integer (en pixels) `small` ou , ou , `medium` `large` .</span><span class="sxs-lookup"><span data-stu-id="12d44-261">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="12d44-262">Carte adaptative définissant le formulaire (si vous en utilisez un).</span><span class="sxs-lookup"><span data-stu-id="12d44-262">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="12d44-263">URL à ouvrir dans le module de tâche en tant qu'affichage web incorporé.</span><span class="sxs-lookup"><span data-stu-id="12d44-263">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="12d44-264">Si un client ne prend pas en charge la fonctionnalité de module de tâche, cette URL est ouverte dans un onglet de navigateur.</span><span class="sxs-lookup"><span data-stu-id="12d44-264">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a><span data-ttu-id="12d44-265">Répondre à fetchTask avec une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="12d44-265">Respond to the fetchTask with an Adaptive Card</span></span>

<span data-ttu-id="12d44-266">Lorsque vous utilisez une carte adaptative, vous devez répondre avec un objet contenant `task` `value` une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="12d44-266">When using an adaptive card, you must respond with a `task` object with the `value` object containing an Adaptive Card.</span></span>

#### <a name="example"></a><span data-ttu-id="12d44-267">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-267">Example</span></span>

<span data-ttu-id="12d44-268">La section de code suivante est un exemple de `fetchTask` réponse avec une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="12d44-268">The following code section is an example to `fetchTask` response with an adaptive card:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="12d44-269">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="12d44-269">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="12d44-270">Cet exemple utilise le [package AdaptiveCards NuGet en](https://www.nuget.org/packages/AdaptiveCards) plus du SDK Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="12d44-270">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="12d44-271">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="12d44-271">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="12d44-272">JSON</span><span class="sxs-lookup"><span data-stu-id="12d44-272">JSON</span></span>](#tab/json)

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

### <a name="create-a-task-module-with-an-embedded-web-view"></a><span data-ttu-id="12d44-273">Créer un module de tâche avec un affichage web incorporé</span><span class="sxs-lookup"><span data-stu-id="12d44-273">Create a task module with an embedded web view</span></span>

<span data-ttu-id="12d44-274">Lorsque vous utilisez un affichage web incorporé, vous devez répondre avec un objet avec l'objet contenant l'URL du formulaire web que `task` `value` vous souhaitez charger.</span><span class="sxs-lookup"><span data-stu-id="12d44-274">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form that you want to load.</span></span> <span data-ttu-id="12d44-275">Les domaines d'une URL que vous souhaitez charger doivent être inclus dans le tableau dans le manifeste `validDomains` de votre application.</span><span class="sxs-lookup"><span data-stu-id="12d44-275">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="12d44-276">Pour plus d'informations sur la création de votre affichage web incorporé, voir la [documentation du module de tâche.](~/task-modules-and-cards/what-are-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="12d44-276">For more information on building your embedded web view, see the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md).</span></span> 

# <a name="cnet"></a>[<span data-ttu-id="12d44-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="12d44-277">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="12d44-278">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="12d44-278">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="12d44-279">JSON</span><span class="sxs-lookup"><span data-stu-id="12d44-279">JSON</span></span>](#tab/json)

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="12d44-280">Demande d'installation de votre bot de conversation</span><span class="sxs-lookup"><span data-stu-id="12d44-280">Request to install your conversational bot</span></span>

<span data-ttu-id="12d44-281">Si l'application contient un bot de conversation, installez-le dans la conversation, puis chargez le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="12d44-281">If the app contains a conversational bot, install the bot in the conversation and then load the task module.</span></span> <span data-ttu-id="12d44-282">Le bot est utile pour obtenir un contexte supplémentaire pour le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="12d44-282">The bot is useful to get additional context for the task module.</span></span> <span data-ttu-id="12d44-283">Un exemple de ce scénario consiste à extraire la liste de membres pour remplir un contrôle de s picker de personnes ou la liste des canaux d'une équipe.</span><span class="sxs-lookup"><span data-stu-id="12d44-283">An example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="12d44-284">Lorsque l'extension de messagerie reçoit l'appel, vérifiez si le bot est installé dans le contexte actuel `composeExtension/fetchTask` pour faciliter le flux.</span><span class="sxs-lookup"><span data-stu-id="12d44-284">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="12d44-285">Par exemple, vérifiez le flux avec un appel d'obtenir une liste.</span><span class="sxs-lookup"><span data-stu-id="12d44-285">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="12d44-286">Si le bot n'est pas installé, renvoyer une carte adaptative avec une action qui demande à l'utilisateur d'installer le bot.</span><span class="sxs-lookup"><span data-stu-id="12d44-286">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="12d44-287">L'utilisateur doit avoir l'autorisation d'installer les applications à cet emplacement pour vérification.</span><span class="sxs-lookup"><span data-stu-id="12d44-287">The user must have the permission to install the apps in that location for checking.</span></span> <span data-ttu-id="12d44-288">Si l'installation de l'application échoue, l'utilisateur reçoit un message pour contacter l'administrateur.</span><span class="sxs-lookup"><span data-stu-id="12d44-288">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example"></a><span data-ttu-id="12d44-289">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-289">Example</span></span> 

<span data-ttu-id="12d44-290">La section de code suivante est un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="12d44-290">The following code section is an example of the response:</span></span>

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

<span data-ttu-id="12d44-291">Après l'installation du bot conversationnel, il reçoit un autre message d'appel `name = composeExtension/submitAction` avec , et `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="12d44-291">After the installation of conversational bot, it receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example"></a><span data-ttu-id="12d44-292">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-292">Example</span></span> 

<span data-ttu-id="12d44-293">La section de code suivante est un exemple de réponse de tâche à l'appel :</span><span class="sxs-lookup"><span data-stu-id="12d44-293">The following code section is an example of the task response to the invoke:</span></span>

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

<span data-ttu-id="12d44-294">La réponse à la tâche à l'appel doit être similaire à celle du bot installé.</span><span class="sxs-lookup"><span data-stu-id="12d44-294">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example"></a><span data-ttu-id="12d44-295">Exemple</span><span class="sxs-lookup"><span data-stu-id="12d44-295">Example</span></span> 

<span data-ttu-id="12d44-296">La section de code suivante est un exemple d'installation juste-à-temps de l'application avec carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="12d44-296">The following code section is an example of just-in time installation of app with Adaptive card:</span></span> 

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

## <a name="code-sample"></a><span data-ttu-id="12d44-297">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="12d44-297">Code sample</span></span>

| <span data-ttu-id="12d44-298">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="12d44-298">Sample Name</span></span>           | <span data-ttu-id="12d44-299">Description</span><span class="sxs-lookup"><span data-stu-id="12d44-299">Description</span></span> | <span data-ttu-id="12d44-300">.NET</span><span class="sxs-lookup"><span data-stu-id="12d44-300">.NET</span></span>    | <span data-ttu-id="12d44-301">Node.js</span><span class="sxs-lookup"><span data-stu-id="12d44-301">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="12d44-302">Teams d'extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="12d44-302">Teams messaging extension action</span></span>| <span data-ttu-id="12d44-303">Décrit comment définir des commandes d'action, créer un module de tâche et répondre à une action d'soumission de module de tâche.</span><span class="sxs-lookup"><span data-stu-id="12d44-303">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="12d44-304">View</span><span class="sxs-lookup"><span data-stu-id="12d44-304">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="12d44-305">View</span><span class="sxs-lookup"><span data-stu-id="12d44-305">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="12d44-306">Teams d'extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="12d44-306">Teams messaging extension search</span></span>   |  <span data-ttu-id="12d44-307">Décrit comment définir des commandes de recherche et répondre aux recherches.</span><span class="sxs-lookup"><span data-stu-id="12d44-307">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="12d44-308">View</span><span class="sxs-lookup"><span data-stu-id="12d44-308">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="12d44-309">View</span><span class="sxs-lookup"><span data-stu-id="12d44-309">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="12d44-310">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="12d44-310">See also</span></span>

[<span data-ttu-id="12d44-311">Définir les commandes d’action</span><span class="sxs-lookup"><span data-stu-id="12d44-311">Define action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a><span data-ttu-id="12d44-312">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="12d44-312">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="12d44-313">Répondre à la commande d'action</span><span class="sxs-lookup"><span data-stu-id="12d44-313">Respond to action command</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

