---
title: Conception de notifications de flux d’activités
author: heath-hamilton
description: Découvrez comment concevoir des notifications de flux d’activités pour votre application Teams et obtenir le kit Microsoft Teams’interface utilisateur.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 61a2a6da2a5ed0cb3126b9798094b06c575c9b6c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631289"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a><span data-ttu-id="0428a-103">Conception de notifications de flux d’activités pour Microsoft Teams application</span><span class="sxs-lookup"><span data-stu-id="0428a-103">Designing activity feed notifications for your Microsoft Teams app</span></span>

<span data-ttu-id="0428a-104">Le flux d’activités permet aux utilisateurs d’accéder à leurs notifications Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0428a-104">The activity feed is a surface for users to access their notifications in Microsoft Teams.</span></span> <span data-ttu-id="0428a-105">Le flux conserve les notifications des quatre semaines passées.</span><span class="sxs-lookup"><span data-stu-id="0428a-105">The feed retains notifications from the past four weeks.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0428a-106">Desktop</span><span class="sxs-lookup"><span data-stu-id="0428a-106">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="Un exemple montre une notification d’application qui s’affiche dans le flux Teams’activité." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0428a-108">Mobile</span><span class="sxs-lookup"><span data-stu-id="0428a-108">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="Un exemple montre une notification d’application qui s’affiche dans le flux d Teams sur mobile." border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="0428a-110">Anatomie</span><span class="sxs-lookup"><span data-stu-id="0428a-110">Anatomy</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Concevoir l’anatomie de la notification Teams flux d’activités." border="false":::

|<span data-ttu-id="0428a-112">Compteur</span><span class="sxs-lookup"><span data-stu-id="0428a-112">Counter</span></span>|<span data-ttu-id="0428a-113">Description</span><span class="sxs-lookup"><span data-stu-id="0428a-113">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0428a-114">1</span><span class="sxs-lookup"><span data-stu-id="0428a-114">1</span></span>|<span data-ttu-id="0428a-115">**Avatar**: indique qui a initié l’activité.</span><span class="sxs-lookup"><span data-stu-id="0428a-115">**Avatar**: Shows who initiated the activity.</span></span>|
|<span data-ttu-id="0428a-116">2</span><span class="sxs-lookup"><span data-stu-id="0428a-116">2</span></span>|<span data-ttu-id="0428a-117">**Icône type d’activité/application**: représente le type d’activité.</span><span class="sxs-lookup"><span data-stu-id="0428a-117">**Activity type/app icon**: Depicts the type of activity.</span></span> <span data-ttu-id="0428a-118">Pour les notifications d’application, l’icône de ligne est remplacée par une icône d’application.</span><span class="sxs-lookup"><span data-stu-id="0428a-118">For app notifications, the line icon is replaced with an app icon.</span></span>|
|<span data-ttu-id="0428a-119">3</span><span class="sxs-lookup"><span data-stu-id="0428a-119">3</span></span>|<span data-ttu-id="0428a-120">**Titre (première ligne) : Actor + reason**: *Actor*: Nom de l’utilisateur ou de l’application qui a initié l’activité.</span><span class="sxs-lookup"><span data-stu-id="0428a-120">**Title (first line): Actor + reason**: *Actor*: Name of the user or app that initiated the activity.</span></span> <span data-ttu-id="0428a-121">*Raison*: décrit l’activité.</span><span class="sxs-lookup"><span data-stu-id="0428a-121">*Reason*: Describes the activity.</span></span>|
|<span data-ttu-id="0428a-122">4 </span><span class="sxs-lookup"><span data-stu-id="0428a-122">4</span></span>|<span data-ttu-id="0428a-123">**Timestamp :** indique quand l’activité s’est produite.</span><span class="sxs-lookup"><span data-stu-id="0428a-123">**Timestamp**: Shows when the activity happened.</span></span>|
|<span data-ttu-id="0428a-124">5 </span><span class="sxs-lookup"><span data-stu-id="0428a-124">5</span></span>|<span data-ttu-id="0428a-125">**Emplacement (deuxième ligne)**: indique où l’activité s’est produite Teams.</span><span class="sxs-lookup"><span data-stu-id="0428a-125">**Location (second line)**: Shows where the activity happened in Teams.</span></span>|
|<span data-ttu-id="0428a-126">6 </span><span class="sxs-lookup"><span data-stu-id="0428a-126">6</span></span>|<span data-ttu-id="0428a-127">**Informations tertiaires (troisième ligne)**: Facultatif.</span><span class="sxs-lookup"><span data-stu-id="0428a-127">**Tertiary information (third line)**: Optional.</span></span> <span data-ttu-id="0428a-128">Affiche un aperçu de texte ou des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0428a-128">Shows preview text or additional information.</span></span>|

## <a name="types-of-activity-feed-notification-cards"></a><span data-ttu-id="0428a-129">Types de cartes de notification de flux d’activités</span><span class="sxs-lookup"><span data-stu-id="0428a-129">Types of activity feed notification cards</span></span>

<span data-ttu-id="0428a-130">Les variantes suivantes montrent les types de cartes de notification de flux d’activités que vous pouvez afficher.</span><span class="sxs-lookup"><span data-stu-id="0428a-130">The following variants show the kinds of activity feed notification cards you can display.</span></span> <span data-ttu-id="0428a-131">Le logo de l’application remplace l’avatar de l’utilisateur pour les notifications générées par l’application.</span><span class="sxs-lookup"><span data-stu-id="0428a-131">The app logo replaces the user avatar for app-generated notifications.</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Variantes de Teams de flux d’activités." border="false":::

## <a name="manage-activity-feed-notifications"></a><span data-ttu-id="0428a-133">Gérer les notifications de flux d’activités</span><span class="sxs-lookup"><span data-stu-id="0428a-133">Manage activity feed notifications</span></span>

<span data-ttu-id="0428a-134">Les utilisateurs peuvent gérer les notifications envoyées à partir de votre application dans la page Teams paramètres.</span><span class="sxs-lookup"><span data-stu-id="0428a-134">Users can manage notifications sent from your app in the Teams settings page.</span></span>

## <a name="related-system-notifications"></a><span data-ttu-id="0428a-135">Notifications système associées</span><span class="sxs-lookup"><span data-stu-id="0428a-135">Related system notifications</span></span>

<span data-ttu-id="0428a-136">Chaque activité génère une notification système.</span><span class="sxs-lookup"><span data-stu-id="0428a-136">Each activity generates a system notification.</span></span> <span data-ttu-id="0428a-137">Ce qui s’affiche dépend de ce que l’utilisateur configure dans ses paramètres de notification.</span><span class="sxs-lookup"><span data-stu-id="0428a-137">What displays depends on what the user configures in their notification settings.</span></span> <span data-ttu-id="0428a-138">Les utilisateurs peuvent également choisir un style de notification en fonction de leur système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="0428a-138">Users can also choose a notification style based on their operating system.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0428a-139">Desktop</span><span class="sxs-lookup"><span data-stu-id="0428a-139">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Variantes de cartes Teams d’activité sur différents systèmes d’exploitation." border="false":::

|<span data-ttu-id="0428a-141">Compteur</span><span class="sxs-lookup"><span data-stu-id="0428a-141">Counter</span></span>|<span data-ttu-id="0428a-142">Description</span><span class="sxs-lookup"><span data-stu-id="0428a-142">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0428a-143">1</span><span class="sxs-lookup"><span data-stu-id="0428a-143">1</span></span>|<span data-ttu-id="0428a-144">Teams personnalisée</span><span class="sxs-lookup"><span data-stu-id="0428a-144">Teams custom</span></span>|
|<span data-ttu-id="0428a-145">2</span><span class="sxs-lookup"><span data-stu-id="0428a-145">2</span></span>|<span data-ttu-id="0428a-146">Windows</span><span class="sxs-lookup"><span data-stu-id="0428a-146">Windows</span></span>|
|<span data-ttu-id="0428a-147">3</span><span class="sxs-lookup"><span data-stu-id="0428a-147">3</span></span>|<span data-ttu-id="0428a-148">Mac</span><span class="sxs-lookup"><span data-stu-id="0428a-148">Mac</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="0428a-149">Mobile</span><span class="sxs-lookup"><span data-stu-id="0428a-149">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Variantes de Teams de flux d’activités sur Android et iOS." border="false":::

|<span data-ttu-id="0428a-151">Compteur</span><span class="sxs-lookup"><span data-stu-id="0428a-151">Counter</span></span>|<span data-ttu-id="0428a-152">Description</span><span class="sxs-lookup"><span data-stu-id="0428a-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0428a-153">1</span><span class="sxs-lookup"><span data-stu-id="0428a-153">1</span></span>|<span data-ttu-id="0428a-154">Android</span><span class="sxs-lookup"><span data-stu-id="0428a-154">Android</span></span>|
|<span data-ttu-id="0428a-155">2</span><span class="sxs-lookup"><span data-stu-id="0428a-155">2</span></span>|<span data-ttu-id="0428a-156">iOS</span><span class="sxs-lookup"><span data-stu-id="0428a-156">iOS</span></span>|

---

## <a name="next-step"></a><span data-ttu-id="0428a-157">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="0428a-157">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0428a-158">Implémenter des notifications de flux d’activités</span><span class="sxs-lookup"><span data-stu-id="0428a-158">Implement activity feed notifications</span></span>](/graph/teams-send-activityfeednotifications)
