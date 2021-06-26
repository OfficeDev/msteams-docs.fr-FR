---
title: Créer une page de contenu
author: surbhigupta
description: Comment créer une page de contenu
keywords: 'onglets teams : canal de groupe configurable statique'
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1ec2c0381ba371393a03cda69ffc44a5f49924e
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140200"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="b98a6-104">Créer une page de contenu pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="b98a6-104">Create a content page for your tab</span></span>

<span data-ttu-id="b98a6-105">Une page de contenu est une page web qui est rendue dans le client Teams client.</span><span class="sxs-lookup"><span data-stu-id="b98a6-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="b98a6-106">Ces éléments font partie des éléments ci-après :</span><span class="sxs-lookup"><span data-stu-id="b98a6-106">These are part of:</span></span>

* <span data-ttu-id="b98a6-107">Onglet personnalisé d’étendue personnelle : dans ce cas, la page de contenu est la première page que l’utilisateur rencontre.</span><span class="sxs-lookup"><span data-stu-id="b98a6-107">A personal-scoped custom tab: In this case, the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="b98a6-108">Onglet personnalisé de canal ou de groupe : la page de contenu s’affiche après que l’utilisateur épingle et configure l’onglet dans le contexte approprié.</span><span class="sxs-lookup"><span data-stu-id="b98a6-108">A channel or group custom tab: The content page is displayed after the user pins and configures the tab in the appropriate context.</span></span>
* <span data-ttu-id="b98a6-109">Module [de tâche](~/task-modules-and-cards/what-are-task-modules.md): vous pouvez créer une page de contenu et l’incorporer en tant que vue web à l’intérieur d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="b98a6-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="b98a6-110">La page est restituer à l’intérieur de la fenêtre pop-up modale.</span><span class="sxs-lookup"><span data-stu-id="b98a6-110">The page is rendered inside the modal pop-up.</span></span>

<span data-ttu-id="b98a6-111">Cet article est spécifique à l’utilisation de pages de contenu en tant qu’onglets ; Toutefois, la majorité des conseils présentés ici s’appliquent, quelle que soit la présentation de la page de contenu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b98a6-111">This article is specific to using content pages as tabs; however the majority of the guidance here applies regardless of how the content page is presented to the user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="b98a6-112">Recommandations en matière de contenu d’onglet et de conception</span><span class="sxs-lookup"><span data-stu-id="b98a6-112">Tab content and design guidelines</span></span>

<span data-ttu-id="b98a6-113">L’objectif global de votre onglet est de fournir un accès à un contenu significatif et attrayant qui a une valeur pratique et un objectif évident.</span><span class="sxs-lookup"><span data-stu-id="b98a6-113">Your tab's overall objective is to provide access to meaningful and engaging content that has practical value and an evident purpose.</span></span> <span data-ttu-id="b98a6-114">Vous devez vous concentrer sur le nettoyage, l’intuitive et l’immersif du contenu de votre conception d’onglet.</span><span class="sxs-lookup"><span data-stu-id="b98a6-114">You must focus on making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="b98a6-115">Pour plus d’informations, voir [recommandations en matière](~/tabs/design/tabs.md) de conception d’onglets [et Microsoft Teams de validation du store.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span><span class="sxs-lookup"><span data-stu-id="b98a6-115">For more information, see [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="b98a6-116">Intégrer votre code avec Teams</span><span class="sxs-lookup"><span data-stu-id="b98a6-116">Integrate your code with Teams</span></span>

<span data-ttu-id="b98a6-117">Pour que votre page s’affiche Teams, vous devez inclure le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page.</span><span class="sxs-lookup"><span data-stu-id="b98a6-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> 

<span data-ttu-id="b98a6-118">Le code suivant fournit un exemple de la façon dont votre page et le client Teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="b98a6-118">The following code provides an example of how your page and the Teams client communicate:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="access-additional-content"></a><span data-ttu-id="b98a6-119">Accéder à du contenu supplémentaire</span><span class="sxs-lookup"><span data-stu-id="b98a6-119">Access additional content</span></span>

<span data-ttu-id="b98a6-120">Vous pouvez accéder à du contenu supplémentaire à l’aide du SDK pour interagir avec Teams, créer des liens profonds, utiliser des modules de tâche et vérifier si les domaines d’URL sont inclus dans le `validDomains` tableau.</span><span class="sxs-lookup"><span data-stu-id="b98a6-120">You can access additional content by using the SDK to interact with Teams, creating deep links, using task modules, and verifying if URL domains are included in the `validDomains` array.</span></span>

### <a name="use-the-sdk-to-interact-with-teams"></a><span data-ttu-id="b98a6-121">Utiliser le SDK pour interagir avec les Teams</span><span class="sxs-lookup"><span data-stu-id="b98a6-121">Use the SDK to interact with Teams</span></span>

<span data-ttu-id="b98a6-122">Le [Teams SDK JavaScript client](~/tabs/how-to/using-teams-client-sdk.md) fournit de nombreuses fonctions supplémentaires que vous pouvez trouver utiles lors du développement de votre page de contenu.</span><span class="sxs-lookup"><span data-stu-id="b98a6-122">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions that you can find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="b98a6-123">Liens profonds</span><span class="sxs-lookup"><span data-stu-id="b98a6-123">Deep links</span></span>

<span data-ttu-id="b98a6-124">Vous pouvez créer des liens profonds vers des entités dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b98a6-124">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="b98a6-125">Ceux-ci sont utilisés pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Pour plus d’informations, voir [créer des liens profonds vers du contenu et](~/concepts/build-and-test/deep-links.md)des fonctionnalités dans Teams .</span><span class="sxs-lookup"><span data-stu-id="b98a6-125">These are used to create links that navigate to content and information within your tab. For more information, see [create deep links to content and features in Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="b98a6-126">Modules de tâche</span><span class="sxs-lookup"><span data-stu-id="b98a6-126">Task modules</span></span>

<span data-ttu-id="b98a6-127">Un module de tâche est une expérience de fenêtre pop-up modale que vous pouvez déclencher à partir de votre onglet. Dans une page de contenu, vous pouvez utiliser des modules de tâche pour présenter des formulaires pour recueillir des informations supplémentaires, afficher les détails d’un élément dans une liste ou présenter à l’utilisateur des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b98a6-127">A task module is a modal pop-up experience that you can trigger from your tab. In a content page, you can use task modules to present forms for gathering additional information, displaying the details of an item in a list, or presenting the user with additional information.</span></span> <span data-ttu-id="b98a6-128">Les modules de tâche eux-mêmes peuvent être des pages de contenu supplémentaires ou créés entièrement à l’aide de cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="b98a6-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="b98a6-129">Pour plus d’informations, voir [l’utilisation de modules de tâche dans les onglets.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="b98a6-129">For more information, see [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

### <a name="valid-domains"></a><span data-ttu-id="b98a6-130">Domaines valides</span><span class="sxs-lookup"><span data-stu-id="b98a6-130">Valid domains</span></span>

<span data-ttu-id="b98a6-131">Assurez-vous que tous les domaines d’URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau dans votre [manifeste.](~/concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="b98a6-131">Ensure that all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="b98a6-132">Pour plus d’informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence du schéma de manifeste.</span><span class="sxs-lookup"><span data-stu-id="b98a6-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span>

> [!NOTE]
> <span data-ttu-id="b98a6-133">La fonctionnalité de base de votre onglet existe au sein Teams et non en dehors de Teams.</span><span class="sxs-lookup"><span data-stu-id="b98a6-133">The core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="b98a6-134">Afficher un indicateur de chargement natif</span><span class="sxs-lookup"><span data-stu-id="b98a6-134">Show a native loading indicator</span></span>

<span data-ttu-id="b98a6-135">À partir [du schéma de manifeste v1.7,](../../../resources/schema/manifest-schema.md)vous pouvez fournir un indicateur de chargement [natif.](../../../resources/schema/manifest-schema.md#showloadingindicator)</span><span class="sxs-lookup"><span data-stu-id="b98a6-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator).</span></span> <span data-ttu-id="b98a6-136">Par exemple, page de [contenu d’onglet,](#integrate-your-code-with-teams) [page de configuration,](configuration-page.md) [page de suppression](removal-page.md)et [modules de tâche dans les onglets](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="b98a6-136">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="b98a6-137">Le comportement sur les clients mobiles n’est pas configurable via la propriété de l’indicateur de chargement natif.</span><span class="sxs-lookup"><span data-stu-id="b98a6-137">The behavior on mobile clients is not configurable through the native loading indicator property.</span></span> <span data-ttu-id="b98a6-138">Les clients mobiles affichent cet indicateur par défaut sur les pages de contenu et les modules de tâche iframe.</span><span class="sxs-lookup"><span data-stu-id="b98a6-138">Mobile clients show this indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="b98a6-139">Cet indicateur sur mobile s’affiche lorsqu’une demande d’extraction de contenu est effectuée et est rejetée dès que la demande est terminée.</span><span class="sxs-lookup"><span data-stu-id="b98a6-139">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>

<span data-ttu-id="b98a6-140">Si vous indiquez dans le manifeste de votre application, toutes les pages de configuration, de contenu et de suppression d’onglets et tous les modules de tâche iframe doivent suivre `showLoadingIndicator : true`  les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b98a6-140">If you indicate `showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow these steps:</span></span>

<span data-ttu-id="b98a6-141">**Pour afficher l’indicateur de chargement**</span><span class="sxs-lookup"><span data-stu-id="b98a6-141">**To show the loading indicator**</span></span>

1. <span data-ttu-id="b98a6-142">`"showLoadingIndicator": true`Ajoutez-le à votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="b98a6-142">Add `"showLoadingIndicator": true` to your manifest.</span></span>
1. <span data-ttu-id="b98a6-143">Appel `microsoftTeams.initialize();`.</span><span class="sxs-lookup"><span data-stu-id="b98a6-143">Call `microsoftTeams.initialize();`.</span></span>
1. <span data-ttu-id="b98a6-144">Dans le **cas d’une** étape obligatoire, appelez Teams `microsoftTeams.appInitialization.notifySuccess()` que votre application a été correctement chargée.</span><span class="sxs-lookup"><span data-stu-id="b98a6-144">As a **mandatory** step, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="b98a6-145">Teams masque ensuite l’indicateur de chargement, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="b98a6-145">Teams then hides the loading indicator, if applicable.</span></span> <span data-ttu-id="b98a6-146">Si elle n’est pas appelée dans les 30 secondes, elle est supposée que votre application a été hors délai et qu’un écran d’erreur avec une option de nouvelle `notifySuccess`  tentative s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b98a6-146">If `notifySuccess`  is not called within 30 seconds, it is assumed that your app timed out and an error screen with a retry option appears.</span></span>
1. <span data-ttu-id="b98a6-147">**Si vous le** souhaitez, si vous êtes prêt à imprimer à l’écran et que vous souhaitez charger différément le reste du contenu de votre application, vous pouvez masquer manuellement l’indicateur de chargement en `microsoftTeams.appInitialization.notifyAppLoaded();` appelant.</span><span class="sxs-lookup"><span data-stu-id="b98a6-147">**Optionally**, if you are ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`.</span></span>
1. <span data-ttu-id="b98a6-148">Si le chargement de votre application échoue, vous pouvez appeler Teams `microsoftTeams.appInitialization.notifyFailure(reason);` savoir qu’une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="b98a6-148">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="b98a6-149">Un écran d’erreur s’affiche pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b98a6-149">An error screen is shown to the user.</span></span> <span data-ttu-id="b98a6-150">Le code suivant fournit un exemple de raisons d’échec d’application :</span><span class="sxs-lookup"><span data-stu-id="b98a6-150">The following code provides an example of application failure reasons:</span></span>

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a><span data-ttu-id="b98a6-151">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b98a6-151">See also</span></span>

* [<span data-ttu-id="b98a6-152">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="b98a6-152">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="b98a6-153">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="b98a6-153">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="b98a6-154">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="b98a6-154">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="b98a6-155">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="b98a6-155">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="b98a6-156">Créer une page de contenu</span><span class="sxs-lookup"><span data-stu-id="b98a6-156">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="b98a6-157">Créer une page de suppression pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="b98a6-157">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="b98a6-158">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="b98a6-158">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="b98a6-159">Obtenir un contexte Teams pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="b98a6-159">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="b98a6-160">Créer des onglets avec les Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="b98a6-160">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="b98a6-161">Déploiement du lien des onglets et vue des étapes</span><span class="sxs-lookup"><span data-stu-id="b98a6-161">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="b98a6-162">Créer des onglets de conversation</span><span class="sxs-lookup"><span data-stu-id="b98a6-162">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="b98a6-163">Modifications des marges de l’onglet</span><span class="sxs-lookup"><span data-stu-id="b98a6-163">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="b98a6-164">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b98a6-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b98a6-165">Créer une page de configuration</span><span class="sxs-lookup"><span data-stu-id="b98a6-165">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
