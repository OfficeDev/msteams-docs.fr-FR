---
title: Recevoir tous les messages de canal avec RSC
author: surbhigupta12
description: Recevoir tous les messages de canal avec des autorisations RSC
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 833bdbc015cf852fcd899ce4e75f742448b89978
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631325"
---
# <a name="receive-all-channel-messages-with-rsc"></a><span data-ttu-id="ba7a4-103">Recevoir tous les messages de canal avec RSC</span><span class="sxs-lookup"><span data-stu-id="ba7a4-103">Receive all channel messages with RSC</span></span>

> [!NOTE]
> <span data-ttu-id="ba7a4-104">Cette fonctionnalité est actuellement disponible en prévisualisation [pour les développeurs publics](../../../resources/dev-preview/developer-preview-intro.md) uniquement.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-104">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="ba7a4-105">Le modèle d’autorisations de consentement spécifique aux ressources(RSC), développé à l’origine pour Teams Graph API, est désormais étendu aux scénarios de bot.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-105">The resource-specific consent (RSC) permissions model, originally developed for Teams Graph APIs, is now extended to bot scenarios.</span></span>

<span data-ttu-id="ba7a4-106">Actuellement, les bots peuvent uniquement recevoir des messages de canal utilisateur lorsqu’ils sont @mentioned.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-106">Currently, bots can only receive user channel messages when they are @mentioned.</span></span> <span data-ttu-id="ba7a4-107">À l’aide de RSC, vous pouvez désormais demander aux propriétaires d’équipe de consentir à ce qu’un bot reçoie des messages utilisateur sur les canaux standard d’une équipe sans @mentioned.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-107">Using RSC, you can now request team owners to consent for a bot to receive user messages across standard channels in a team without being @mentioned.</span></span> <span data-ttu-id="ba7a4-108">Cette fonctionnalité est activée en spécifiant l’autorisation dans le manifeste d’une `ChannelMessage.Read.Group` application Teams RSC.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-108">This capability is enabled by specifying the `ChannelMessage.Read.Group` permission in the manifest of an RSC enabled Teams app.</span></span> <span data-ttu-id="ba7a4-109">Après la configuration, les propriétaires d’équipe peuvent donner leur consentement pendant le processus d’installation de l’application.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-109">After configuration, team owners can grant consent during the app installation process.</span></span>

<span data-ttu-id="ba7a4-110">Pour plus d’informations sur l’activation du RSC pour votre application, voir le consentement spécifique à [la ressource dans Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="ba7a4-110">For more information about enabling RSC for your app, see [resource-specific consent in Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).</span></span>

## <a name="enable-bots-to-receive-all-channel-messages"></a><span data-ttu-id="ba7a4-111">Activer les bots pour recevoir tous les messages de canal</span><span class="sxs-lookup"><span data-stu-id="ba7a4-111">Enable bots to receive all channel messages</span></span>

<span data-ttu-id="ba7a4-112">`ChannelMessage.Read.Group`L’autorisation RSC est étendue aux bots.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-112">The `ChannelMessage.Read.Group` RSC permission is extended to bots.</span></span> <span data-ttu-id="ba7a4-113">Avec le consentement de l’utilisateur, cette autorisation permet aux applications graphiques d’obtenir tous les messages d’une conversation et aux robots de recevoir tous les messages de canal sans être @mentioned.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-113">With user consent, this permission allows graph applications to get all messages in a conversation and bots to receive all channel messages without being @mentioned.</span></span>

## <a name="update-app-manifest"></a><span data-ttu-id="ba7a4-114">Mettre à jour le manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="ba7a4-114">Update app manifest</span></span>

<span data-ttu-id="ba7a4-115">Pour que votre bot reçoit tous les messages de canal, RSC doit être configuré dans le manifeste Teams’application avec l’autorisation spécifiée `ChannelMessage.Read.Group` dans la `webApplicationInfo` propriété.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-115">For your bot to receive all channel messages, RSC must be configured in the Teams app manifest with the `ChannelMessage.Read.Group` permission specified in the `webApplicationInfo` property.</span></span>

![Mettre à jour le manifeste de l’application](~/bots/how-to/conversations/Media/appmanifest.png)

<span data-ttu-id="ba7a4-117">Voici un exemple de `webApplicationInfo` l’objet :</span><span class="sxs-lookup"><span data-stu-id="ba7a4-117">The following is an example of the `webApplicationInfo` object:</span></span>

* <span data-ttu-id="ba7a4-118">**id**: ID de votre Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="ba7a4-118">**id**: Your Azure Active Directory (AAD) app ID.</span></span> <span data-ttu-id="ba7a4-119">Il peut s’en trouver de même que votre ID de bot.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-119">This can be the same as your bot ID.</span></span>
* <span data-ttu-id="ba7a4-120">**ressource**: Toute chaîne.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-120">**resource**: Any string.</span></span> <span data-ttu-id="ba7a4-121">Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-121">This field has no operation in RSC, but must be added and have a value to avoid error response.</span></span>
* <span data-ttu-id="ba7a4-122">**applicationPermissions**: les autorisations RSC pour votre application doivent `ChannelMessage.Read.Group` être spécifiées.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-122">**applicationPermissions**: RSC permissions for your app with `ChannelMessage.Read.Group` must be specified.</span></span> <span data-ttu-id="ba7a4-123">Pour plus d’informations, [voir autorisations spécifiques aux ressources.](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="ba7a4-123">For more information, see [resource-specific permissions](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).</span></span>

<span data-ttu-id="ba7a4-124">Le code suivant fournit un exemple de manifeste d’application :</span><span class="sxs-lookup"><span data-stu-id="ba7a4-124">The following code provides an example of the app manifest:</span></span>

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team-to-test"></a><span data-ttu-id="ba7a4-125">Chargement de version test dans une équipe</span><span class="sxs-lookup"><span data-stu-id="ba7a4-125">Sideload in a team to test</span></span>

<span data-ttu-id="ba7a4-126">Pour tester le chargement d’une version test dans une équipe, si tous les messages de canal d’une équipe avec RSC sont reçus sans être @mentioned :</span><span class="sxs-lookup"><span data-stu-id="ba7a4-126">To sideload in a team to test, whether all channel messages in a team with RSC are received without being @mentioned:</span></span>

1. <span data-ttu-id="ba7a4-127">Sélectionnez ou créez une équipe.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-127">Select or create a team.</span></span>
1. <span data-ttu-id="ba7a4-128">Sélectionnez les &#x25CF;&#x25CF;&#x25CF; dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-128">Select the ellipses &#x25CF;&#x25CF;&#x25CF; from the left pane.</span></span> <span data-ttu-id="ba7a4-129">Le menu déroulant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-129">The drop-down menu appears.</span></span>
1. <span data-ttu-id="ba7a4-130">Sélectionnez **Gérer l’équipe** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-130">Select **Manage team** from the drop-down menu.</span></span> <span data-ttu-id="ba7a4-131">Les détails s’affichent.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-131">The details appear.</span></span>

   ![Gestion des applications en équipe](~/bots/how-to/conversations/Media/managingteam.png)

1. <span data-ttu-id="ba7a4-133">Sélectionner **les applications**.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-133">Select **Apps**.</span></span> <span data-ttu-id="ba7a4-134">Plusieurs applications s’affichent.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-134">Multiple apps appear.</span></span>
1. <span data-ttu-id="ba7a4-135">Sélectionnez **Télécharger une application personnalisée dans** le coin inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-135">Select **Upload a custom app** from the lower right corner.</span></span>

    ![Téléchargement d’une application personnalisée](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. <span data-ttu-id="ba7a4-137">Sélectionnez le package d’application dans la **boîte de** dialogue Ouvrir.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-137">Select the app package from the **Open** dialog box.</span></span>
1. <span data-ttu-id="ba7a4-138">Sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-138">Select **Open**.</span></span>

    ![Sélection d’un package d’application](~/bots/how-to/conversations/Media/selectapppackage.png)

1. <span data-ttu-id="ba7a4-140">Sélectionnez **Ajouter** dans la fenêtre pop-up des détails de l’application pour ajouter le bot à votre équipe sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-140">Select **Add** from the app details pop-up, to add the bot to your selected team.</span></span>

    ![Ajout du bot](~/bots/how-to/conversations/Media/addingbot.png)

1. <span data-ttu-id="ba7a4-142">Sélectionnez un canal et entrez un message dans le canal pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-142">Select a channel and enter a message in the channel for your bot.</span></span>

    <span data-ttu-id="ba7a4-143">Le bot reçoit le message sans être @mentioned.</span><span class="sxs-lookup"><span data-stu-id="ba7a4-143">The bot receives the message without being @mentioned.</span></span>

    ![Le bot reçoit un message](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="see-also"></a><span data-ttu-id="ba7a4-145">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ba7a4-145">See also</span></span>

* [<span data-ttu-id="ba7a4-146">Conversations de robots</span><span class="sxs-lookup"><span data-stu-id="ba7a4-146">Bot conversations</span></span>](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [<span data-ttu-id="ba7a4-147">Consentement spécifique à la ressource</span><span class="sxs-lookup"><span data-stu-id="ba7a4-147">Resource-specific consent</span></span>](/microsoftteams/resource-specific-consent)
* [<span data-ttu-id="ba7a4-148">Tester le consentement spécifique aux ressources</span><span class="sxs-lookup"><span data-stu-id="ba7a4-148">Test resource-specific consent</span></span>](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [<span data-ttu-id="ba7a4-149">Télécharger application personnalisée dans Teams</span><span class="sxs-lookup"><span data-stu-id="ba7a4-149">Upload custom app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
