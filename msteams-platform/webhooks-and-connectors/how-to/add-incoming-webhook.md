---
title: Créer un webhook entrant
author: laujan
description: explique comment ajouter des webhooks entrants à Teams’application et publier des demandes externes Teams avec des webhooks entrants
keywords: onglets teams webhook sortant
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 53fe9725148579325386fa4677bebb61fdb72c56
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140107"
---
# <a name="create-incoming-webhook"></a><span data-ttu-id="341bc-104">Créer un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="341bc-104">Create Incoming Webhook</span></span>

<span data-ttu-id="341bc-105">Le webhook entrant permet à toutes les applications externes de partager du contenu Teams canaux.</span><span class="sxs-lookup"><span data-stu-id="341bc-105">Incoming Webhook allows any external apps to share content in Teams channels.</span></span> <span data-ttu-id="341bc-106">Ces webhooks sont utilisés comme outils de suivi et de notification.</span><span class="sxs-lookup"><span data-stu-id="341bc-106">These webhooks are used as tracking and notifying tools.</span></span> <span data-ttu-id="341bc-107">Ils fournissent une URL unique à laquelle vous envoyez une charge utile JSON avec un message au format de carte.</span><span class="sxs-lookup"><span data-stu-id="341bc-107">They provide a unique URL, to which you send a JSON payload with a message in card format.</span></span> <span data-ttu-id="341bc-108">Les cartes sont des conteneurs d’interface utilisateur qui incluent du contenu et des actions liées à une seule rubrique.</span><span class="sxs-lookup"><span data-stu-id="341bc-108">Cards are user interface containers that include content and actions related to a single topic.</span></span> <span data-ttu-id="341bc-109">Teams utiliser des cartes dans les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="341bc-109">Teams use cards within the following capabilities:</span></span>

* <span data-ttu-id="341bc-110">Bots</span><span class="sxs-lookup"><span data-stu-id="341bc-110">Bots</span></span>
* <span data-ttu-id="341bc-111">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="341bc-111">Messaging extensions</span></span>
* <span data-ttu-id="341bc-112">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="341bc-112">Connectors</span></span>

## <a name="key-features-of-incoming-webhook"></a><span data-ttu-id="341bc-113">Principales fonctionnalités du webhook entrant</span><span class="sxs-lookup"><span data-stu-id="341bc-113">Key features of Incoming Webhook</span></span>

<span data-ttu-id="341bc-114">Le tableau suivant fournit les fonctionnalités et la description du webhook entrant :</span><span class="sxs-lookup"><span data-stu-id="341bc-114">The following table provides the features and description of Incoming Webhook:</span></span>

| <span data-ttu-id="341bc-115">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="341bc-115">Features</span></span> | <span data-ttu-id="341bc-116">Description</span><span class="sxs-lookup"><span data-stu-id="341bc-116">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="341bc-117">Cartes adaptatives utilisant un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="341bc-117">Adaptive Cards using an Incoming Webhook</span></span>|<span data-ttu-id="341bc-118">Les cartes adaptatives peuvent être envoyées via des webhooks entrants.</span><span class="sxs-lookup"><span data-stu-id="341bc-118">Adaptive Cards can be sent through Incoming Webhooks.</span></span> <span data-ttu-id="341bc-119">Pour plus d’informations, voir [Envoyer des cartes adaptatives à l’aide de webhooks entrants.](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)</span><span class="sxs-lookup"><span data-stu-id="341bc-119">For more information, see [Send Adaptive Cards using Incoming Webhooks](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook).</span></span>|
|<span data-ttu-id="341bc-120">Prise en charge de la messagerie actionnable</span><span class="sxs-lookup"><span data-stu-id="341bc-120">Actionable messaging support</span></span>|<span data-ttu-id="341bc-121">Les cartes de message actionnables sont prises en charge dans tous Office 365 groupes, y compris Teams.</span><span class="sxs-lookup"><span data-stu-id="341bc-121">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="341bc-122">Si vous envoyez des messages par le biais de cartes, vous devez utiliser le format de carte de message actionnable.</span><span class="sxs-lookup"><span data-stu-id="341bc-122">If you send messages through cards, you must use the actionable message card format.</span></span> <span data-ttu-id="341bc-123">Pour plus d’informations, voir la référence de carte de [message actionnable héritée](/outlook/actionable-messages/message-card-reference) et l’aire de [jeu de carte de message.](https://messagecardplayground.azurewebsites.net)</span><span class="sxs-lookup"><span data-stu-id="341bc-123">For more information, see [legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and [message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="341bc-124">Prise en charge indépendante de la messagerie HTTPS</span><span class="sxs-lookup"><span data-stu-id="341bc-124">Independent HTTPS messaging support</span></span>|<span data-ttu-id="341bc-125">Les cartes fournissent des informations clairement et de manière cohérente.</span><span class="sxs-lookup"><span data-stu-id="341bc-125">Cards provide information clearly and consistently.</span></span> <span data-ttu-id="341bc-126">Tout outil ou infrastructure qui peut envoyer des demandes HTTPS POST peut envoyer des messages Teams via un webhook entrant.</span><span class="sxs-lookup"><span data-stu-id="341bc-126">Any tool or framework that can send HTTPS POST requests, can send messages to Teams through an Incoming Webhook.</span></span>|
|<span data-ttu-id="341bc-127">Prise en charge de Markdown</span><span class="sxs-lookup"><span data-stu-id="341bc-127">Markdown support</span></span>|<span data-ttu-id="341bc-128">Tous les champs de texte dans les cartes de messagerie actionnables prendre en charge markdown de base.</span><span class="sxs-lookup"><span data-stu-id="341bc-128">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="341bc-129">N’utilisez pas de balises HTML dans vos cartes.</span><span class="sxs-lookup"><span data-stu-id="341bc-129">Do not use HTML markup in your cards.</span></span> <span data-ttu-id="341bc-130">Le code HTML est ignoré et traité comme texte brut.</span><span class="sxs-lookup"><span data-stu-id="341bc-130">HTML is ignored and treated as plain text.</span></span>|
|<span data-ttu-id="341bc-131">Configuration limitée</span><span class="sxs-lookup"><span data-stu-id="341bc-131">Scoped configuration</span></span>|<span data-ttu-id="341bc-132">Le webhook entrant est limitée et configurée au niveau du canal.</span><span class="sxs-lookup"><span data-stu-id="341bc-132">Incoming Webhook is scoped and configured at the channel level.</span></span>|
|<span data-ttu-id="341bc-133">Définitions de ressources sécurisées</span><span class="sxs-lookup"><span data-stu-id="341bc-133">Secure resource definitions</span></span>|<span data-ttu-id="341bc-134">Les messages sont formatés en tant que charges utiles JSON.</span><span class="sxs-lookup"><span data-stu-id="341bc-134">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="341bc-135">Cette structure de messagerie déclarative empêche l’insertion de code malveillant.</span><span class="sxs-lookup"><span data-stu-id="341bc-135">This declarative messaging structure prevents the insertion of malicious code.</span></span>|

> [!NOTE]
> * <span data-ttu-id="341bc-136">Teams bots, extensions de messagerie, webhook entrant et Bot Framework prisent en charge les cartes adaptatives, une infrastructure de plateforme de cartes croisées ouverte.</span><span class="sxs-lookup"><span data-stu-id="341bc-136">Teams bots, messaging extensions, Incoming Webhook, and the Bot Framework support Adaptive Cards, an open cross card platform framework.</span></span> <span data-ttu-id="341bc-137">Actuellement, [les connecteurs Teams ne](../../webhooks-and-connectors/how-to/connectors-creating.md) prisent pas en charge les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="341bc-137">Currently, [Teams connectors](../../webhooks-and-connectors/how-to/connectors-creating.md) do not support Adaptive Cards.</span></span> <span data-ttu-id="341bc-138">Toutefois, il est possible de créer un [flux](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) qui publie des cartes adaptatives sur Teams canal.</span><span class="sxs-lookup"><span data-stu-id="341bc-138">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts Adaptive Cards to a Teams channel.</span></span>
> * <span data-ttu-id="341bc-139">Pour plus d’informations sur les cartes et les webhooks, voir [Cartes adaptatives et Webhooks entrants.](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)</span><span class="sxs-lookup"><span data-stu-id="341bc-139">For more information on cards and webhooks, see [Adaptive cards and Incoming Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks).</span></span>

## <a name="create-incoming-webhook"></a><span data-ttu-id="341bc-140">Créer un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="341bc-140">Create Incoming Webhook</span></span>

<span data-ttu-id="341bc-141">**Pour ajouter un webhook entrant à un canal Teams web**</span><span class="sxs-lookup"><span data-stu-id="341bc-141">**To add an Incoming Webhook to a Teams channel**</span></span>

1. <span data-ttu-id="341bc-142">Go to the channel where you want to add the webhook and select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="341bc-142">Go to the channel where you want to add the webhook and select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="341bc-143">Sélectionnez **connecteurs** dans le menu déroulant :</span><span class="sxs-lookup"><span data-stu-id="341bc-143">Select **Connectors** from the dropdown menu:</span></span>

    ![Select Connector](~/assets/images/connectors.png)

1. <span data-ttu-id="341bc-145">Recherchez **le webhook entrant et** sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="341bc-145">Search for **Incoming Webhook** and select **Add**.</span></span>
1. <span data-ttu-id="341bc-146">Sélectionnez **Configurer,** fournissez un nom et téléchargez une image pour votre webhook si nécessaire :</span><span class="sxs-lookup"><span data-stu-id="341bc-146">Select **Configure**, provide a name, and upload an image for your webhook if required:</span></span>

    ![Bouton Configurer](~/assets/images/configure.png)

1. <span data-ttu-id="341bc-148">La fenêtre de boîte de dialogue présente une URL unique qui mase au canal.</span><span class="sxs-lookup"><span data-stu-id="341bc-148">The dialog window presents a unique URL that maps to the channel.</span></span> <span data-ttu-id="341bc-149">Copiez et enregistrez l’URL de webhook, pour envoyer des informations Microsoft Teams et sélectionnez **Terminé**:</span><span class="sxs-lookup"><span data-stu-id="341bc-149">Copy and save the webhook URL, to send information to Microsoft Teams and select **Done**:</span></span>

    ![Unique URL](~/assets/images/url.png)

<span data-ttu-id="341bc-151">Le webhook est disponible dans le canal Teams webhook.</span><span class="sxs-lookup"><span data-stu-id="341bc-151">The webhook is available in the Teams channel.</span></span>

> [!NOTE]
> <span data-ttu-id="341bc-152">Dans Teams, sélectionnez **Paramètres** autorisations de membre autoriser les membres à créer, mettre à jour et supprimer des  >    >  **connecteurs,** afin que n’importe quel membre d’équipe puisse ajouter, modifier ou supprimer un connecteur.</span><span class="sxs-lookup"><span data-stu-id="341bc-152">In Teams, select **Settings** > **Member permissions** > **Allow members to create, update, and remove connectors**, so that any team member can add, modify, or delete a connector.</span></span>

## <a name="remove-incoming-webhook"></a><span data-ttu-id="341bc-153">Supprimer le webhook entrant</span><span class="sxs-lookup"><span data-stu-id="341bc-153">Remove Incoming Webhook</span></span>

<span data-ttu-id="341bc-154">**Pour supprimer un webhook entrant d’un canal Teams web**</span><span class="sxs-lookup"><span data-stu-id="341bc-154">**To remove an Incoming Webhook from a Teams channel**</span></span>

1. <span data-ttu-id="341bc-155">Go to the channel.</span><span class="sxs-lookup"><span data-stu-id="341bc-155">Go to the channel.</span></span>
1. <span data-ttu-id="341bc-156">Sélectionnez &#8226;&#8226;&#8226; **options supplémentaires dans** la barre de navigation supérieure.</span><span class="sxs-lookup"><span data-stu-id="341bc-156">Select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="341bc-157">Sélectionnez **connecteurs** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="341bc-157">Select **Connectors** from the dropdown menu.</span></span>
1. <span data-ttu-id="341bc-158">Sur la gauche, sous **Gérer,** **sélectionnez Configuré.**</span><span class="sxs-lookup"><span data-stu-id="341bc-158">On the left, under **Manage**, select **Configured**.</span></span>
1. <span data-ttu-id="341bc-159">Sélectionnez **< *le 1*> configuré pour** voir la liste de vos connecteurs actuels :</span><span class="sxs-lookup"><span data-stu-id="341bc-159">Select the **<*1*> Configured** to see a list of your current connectors:</span></span>

    ![Webhook configuré](~/assets/images/configured.png)

1. <span data-ttu-id="341bc-161">Sélectionnez **Gérer** en côté du connecteur que vous souhaitez supprimer :</span><span class="sxs-lookup"><span data-stu-id="341bc-161">Select **Manage** next to the connector that you want to remove:</span></span>

    ![Gérer le webhook](~/assets/images/manage.png)

1. <span data-ttu-id="341bc-163">Sélectionnez **Supprimer**:</span><span class="sxs-lookup"><span data-stu-id="341bc-163">Select **Remove**:</span></span>

    ![Supprimer un webhook](~/assets/images/remove.png)

    <span data-ttu-id="341bc-165">La **boîte de dialogue Supprimer la configuration** s’affiche :</span><span class="sxs-lookup"><span data-stu-id="341bc-165">The **Remove Configuration** dialog box appears:</span></span>

    ![Supprimer la configuration](~/assets/images/removeconfiguration.png)

1. <span data-ttu-id="341bc-167">Complétez les champs et les case à cocher de la boîte de dialogue, puis **sélectionnez Supprimer**:</span><span class="sxs-lookup"><span data-stu-id="341bc-167">Complete the dialog box fields and checkboxes and select **Remove**:</span></span>

    ![Suppression finale](~/assets/images/finalremove.png)

    <span data-ttu-id="341bc-169">Le webhook est supprimé du canal Teams webhook.</span><span class="sxs-lookup"><span data-stu-id="341bc-169">The webhook is removed from the Teams channel.</span></span>

## <a name="see-also"></a><span data-ttu-id="341bc-170">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="341bc-170">See also</span></span>

* [<span data-ttu-id="341bc-171">Créer un webhook sortant</span><span class="sxs-lookup"><span data-stu-id="341bc-171">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [<span data-ttu-id="341bc-172">Créer un connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="341bc-172">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="341bc-173">Créer et envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="341bc-173">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
