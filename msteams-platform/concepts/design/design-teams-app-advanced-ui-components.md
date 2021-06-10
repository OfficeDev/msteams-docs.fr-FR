---
title: Concevoir votre application avec des composants d’interface utilisateur avancés
author: heath-hamilton
description: Découvrez les composants d’interface utilisateur utilisés dans Teams .
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: ae1c2793586dc638d56051e105482aac92e01091
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644928"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a><span data-ttu-id="0085c-103">Conception de votre application Microsoft Teams avec des composants d’interface utilisateur avancés</span><span class="sxs-lookup"><span data-stu-id="0085c-103">Designing your Microsoft Teams app with advanced UI components</span></span>

<span data-ttu-id="0085c-104">Les composants suivants sont une combinaison de [composants](~/concepts/design/design-teams-app-basic-ui-components.md) d’interface utilisateur de base que vous pouvez utiliser pour les situations Teams conception courantes, telles que la navigation.</span><span class="sxs-lookup"><span data-stu-id="0085c-104">The following components are a combination of [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md) that you can use for common Teams design situations, such as navigation.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="0085c-105">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0085c-105">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="0085c-106">Basé sur <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">l’interface utilisateur Fluent,</a>le kit Microsoft Teams’interface utilisateur inclut des composants et des modèles spécifiquement conçus pour créer des applications Teams web.</span><span class="sxs-lookup"><span data-stu-id="0085c-106">Based on <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>, the Microsoft Teams UI Kit includes components and patterns that are designed specifically for building Teams apps.</span></span> <span data-ttu-id="0085c-107">Dans le kit d’interface utilisateur, vous pouvez récupérer et insérer les composants répertoriés ici directement dans votre conception et voir d’autres exemples d’utilisation de chaque composant.</span><span class="sxs-lookup"><span data-stu-id="0085c-107">In the UI kit, you can grab and insert the components listed here directly into your design and see more examples of how to use each component.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0085c-108">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="0085c-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a><span data-ttu-id="0085c-109">Barre de navigation</span><span class="sxs-lookup"><span data-stu-id="0085c-109">Breadcrumb</span></span>

<span data-ttu-id="0085c-110">Les barre de navigation sont une aide à la navigation qui véhicule la hiérarchie de votre application.</span><span class="sxs-lookup"><span data-stu-id="0085c-110">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="0085c-111">Ils aident les utilisateurs à comprendre comment la page qu’ils affichent s’intègre à l’expérience globale et offrent un accès en un clic aux niveaux supérieurs de cette hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="0085c-111">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0085c-112">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="0085c-112">Top use cases</span></span>

* <span data-ttu-id="0085c-113">Hiérarchie de communication</span><span class="sxs-lookup"><span data-stu-id="0085c-113">Communicate hierarchy</span></span>
* <span data-ttu-id="0085c-114">Navigation</span><span class="sxs-lookup"><span data-stu-id="0085c-114">Navigation</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0085c-115">Desktop</span><span class="sxs-lookup"><span data-stu-id="0085c-115">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="L’exemple montre un modèle de lacrumb sur le bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0085c-117">Mobile</span><span class="sxs-lookup"><span data-stu-id="0085c-117">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="L’exemple montre un modèle de lacrumb sur mobile." border="false":::

---

## <a name="left-nav"></a><span data-ttu-id="0085c-119">Navigation gauche</span><span class="sxs-lookup"><span data-stu-id="0085c-119">Left nav</span></span>

<span data-ttu-id="0085c-120">Utilisez le navigation de gauche pour parcourir plusieurs pages dans votre onglet Teams gauche. Dans l’exemple suivant, le navigation gauche se trouve entre la liste de canaux et le contenu de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="0085c-120">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0085c-121">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="0085c-121">Top use cases</span></span>

* <span data-ttu-id="0085c-122">Parcourez plusieurs pages dans un Teams onglet.</span><span class="sxs-lookup"><span data-stu-id="0085c-122">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="0085c-123">Décomposez les applications complexes en plusieurs pages.</span><span class="sxs-lookup"><span data-stu-id="0085c-123">Break down complex apps into multiple pages.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0085c-124">Desktop</span><span class="sxs-lookup"><span data-stu-id="0085c-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="L’exemple montre un modèle de navigation gauche sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0085c-126">Mobile</span><span class="sxs-lookup"><span data-stu-id="0085c-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="L’exemple montre un modèle de navigation gauche sur un appareil mobile." border="false":::

---

## <a name="notification-bar"></a><span data-ttu-id="0085c-128">Barre de notification</span><span class="sxs-lookup"><span data-stu-id="0085c-128">Notification bar</span></span>

<span data-ttu-id="0085c-129">Une barre de notification est une zone dédiée à l’affichage de messages brefs et importants qui ne nécessitent pas que l’utilisateur prenne des mesures immédiates.</span><span class="sxs-lookup"><span data-stu-id="0085c-129">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="0085c-130">Des icônes et couleurs d’arrière-plan spécifiques sont associées à des types de messages spécifiques (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="0085c-130">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0085c-131">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="0085c-131">Top use cases</span></span>

* <span data-ttu-id="0085c-132">Messages critiques, erreurs et avertissements</span><span class="sxs-lookup"><span data-stu-id="0085c-132">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="0085c-133">Messages de réussite</span><span class="sxs-lookup"><span data-stu-id="0085c-133">Success messages</span></span>
* <span data-ttu-id="0085c-134">Messages d’information ou promotionnels</span><span class="sxs-lookup"><span data-stu-id="0085c-134">Informational or promotional messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0085c-135">Desktop</span><span class="sxs-lookup"><span data-stu-id="0085c-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="L’exemple montre les modèles d’interface utilisateur de la barre de notification sur le bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0085c-137">Mobile</span><span class="sxs-lookup"><span data-stu-id="0085c-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="Exemple de modèle d’interface utilisateur de barre de notification sur mobile." border="false":::

---

## <a name="stage"></a><span data-ttu-id="0085c-139">Phase</span><span class="sxs-lookup"><span data-stu-id="0085c-139">Stage</span></span>

<span data-ttu-id="0085c-140">L’étape permet aux utilisateurs d’ouvrir une entité (par exemple, une image, un fichier ou un site web) dans Teams au lieu de l’ouvrir dans une autre application ou navigateur.</span><span class="sxs-lookup"><span data-stu-id="0085c-140">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="0085c-141">Le cas d’utilisation principal de l’étape est l’affichage ; la surface ne doit pas être utilisée pour des interactions complexes.</span><span class="sxs-lookup"><span data-stu-id="0085c-141">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="0085c-142">(Remarque d’implémentation : créez votre étape à l’aide d’un [module de tâche de grande taille.)](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="0085c-142">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0085c-143">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="0085c-143">Top use cases</span></span>

* <span data-ttu-id="0085c-144">Ouvrir une entité dans Teams au lieu d’une autre application ou navigateur</span><span class="sxs-lookup"><span data-stu-id="0085c-144">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="0085c-145">Média à la une ou autre contenu</span><span class="sxs-lookup"><span data-stu-id="0085c-145">Spotlight media or other content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0085c-146">Desktop</span><span class="sxs-lookup"><span data-stu-id="0085c-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="L’exemple montre un modèle d’étape sur le bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0085c-148">Mobile</span><span class="sxs-lookup"><span data-stu-id="0085c-148">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="0085c-149">Votre application peut lancer une étape à partir d’une carte adaptative, d’un lien partagé ou de composants visuels (tels qu’un graphique).</span><span class="sxs-lookup"><span data-stu-id="0085c-149">Your app can launch a stage from an Adaptive Card, shared link, or visual components (such as a chart).</span></span>

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="L’exemple montre un modèle d’étape sur mobile." border="false":::

---

## <a name="toolbar"></a><span data-ttu-id="0085c-151">Barre d'outils</span><span class="sxs-lookup"><span data-stu-id="0085c-151">Toolbar</span></span>

<span data-ttu-id="0085c-152">Une barre d’outils est un conteneur permettant de grouper un ensemble de contrôles.</span><span class="sxs-lookup"><span data-stu-id="0085c-152">A toolbar is a container for grouping a set of controls.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0085c-153">Principaux cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="0085c-153">Top use cases</span></span>

* <span data-ttu-id="0085c-154">Actions contextuelles sur le contenu de l’application</span><span class="sxs-lookup"><span data-stu-id="0085c-154">Contextual actions on app content</span></span>
* <span data-ttu-id="0085c-155">Filtre contextuel et recherche</span><span class="sxs-lookup"><span data-stu-id="0085c-155">Contextual filter and find</span></span>
* <span data-ttu-id="0085c-156">Navigation et barre de navigation</span><span class="sxs-lookup"><span data-stu-id="0085c-156">Navigation and breadcrumbs</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0085c-157">Desktop</span><span class="sxs-lookup"><span data-stu-id="0085c-157">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="L’exemple montre un modèle de barre d’outils sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0085c-159">Mobile</span><span class="sxs-lookup"><span data-stu-id="0085c-159">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="L’exemple montre un modèle de barre d’outils sur mobile." border="false":::

---
