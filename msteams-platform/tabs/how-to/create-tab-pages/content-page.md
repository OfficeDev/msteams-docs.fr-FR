---
title: Créer une page de contenu
author: laujan
description: Comment créer une page de contenu
keywords: 'onglets teams : canal de groupe configurable statique'
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 9dc6c73d877d9355c5d4a9653e0d8ed669fb347e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020379"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="afd49-104">Créer une page de contenu pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="afd49-104">Create a content page for your tab</span></span>

<span data-ttu-id="afd49-105">Une page de contenu est une page web qui est rendue dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="afd49-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="afd49-106">En règle générale, ces éléments font partie des éléments ci-après :</span><span class="sxs-lookup"><span data-stu-id="afd49-106">Typically these are part of:</span></span>

* <span data-ttu-id="afd49-107">Onglet personnalisé d'étendue personnelle : dans ce cas, la page de contenu est la première page que l'utilisateur rencontre.</span><span class="sxs-lookup"><span data-stu-id="afd49-107">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="afd49-108">Onglet personnalisé canal/groupe : une fois que l'utilisateur épingle et configure l'onglet dans le contexte approprié, la page de contenu s'affiche.</span><span class="sxs-lookup"><span data-stu-id="afd49-108">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="afd49-109">Module [de tâche](~/task-modules-and-cards/what-are-task-modules.md) : vous pouvez créer une page de contenu et l'incorporer en tant que vue web à l'intérieur d'un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="afd49-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="afd49-110">La page s'restituera à l'intérieur de la fenêtre popup modale.</span><span class="sxs-lookup"><span data-stu-id="afd49-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="afd49-111">Cet article est spécifique à l'utilisation de pages de contenu en tant qu'onglets ; Toutefois, la majorité des conseils présentés ici s'appliquent, quelle que soit la façon dont la page de contenu est présentée à l'utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="afd49-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="afd49-112">Recommandations en matière de contenu d'onglet et de style</span><span class="sxs-lookup"><span data-stu-id="afd49-112">Tab content and style guidelines</span></span>

<span data-ttu-id="afd49-113">L'objectif global de votre onglet doit être de fournir un accès à un contenu significatif et attrayant qui a une valeur pratique et un objectif évident.</span><span class="sxs-lookup"><span data-stu-id="afd49-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="afd49-114">Cela ne signifie pas que vous devez éviter un style agréable, mais vous devez vous concentrer sur la réduction de l'encombrement en rendant votre conception d'onglet propre, intuitive de navigation et immersif de contenu.</span><span class="sxs-lookup"><span data-stu-id="afd49-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="afd49-115">Voir [contenu et conversations, à l'aide d'onglets](~/tabs/design/tabs.md) et de conseils sur le processus d'approbation des applications [Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="afd49-115">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="afd49-116">Intégrer votre code à Teams</span><span class="sxs-lookup"><span data-stu-id="afd49-116">Integrate your code with Teams</span></span>

<span data-ttu-id="afd49-117">Pour que votre page s'affiche dans Teams, vous devez inclure le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et inclure un appel après le chargement `microsoftTeams.initialize()` de votre page.</span><span class="sxs-lookup"><span data-stu-id="afd49-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="afd49-118">C'est ainsi que votre page et le client Teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="afd49-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="afd49-119">Accès à du contenu supplémentaire</span><span class="sxs-lookup"><span data-stu-id="afd49-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="afd49-120">Utilisation du SDK pour interagir avec Teams</span><span class="sxs-lookup"><span data-stu-id="afd49-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="afd49-121">Le [SDK JavaScript client Teams](~/tabs/how-to/using-teams-client-sdk.md) fournit de nombreuses fonctions supplémentaires qui peuvent vous être utiles lors du développement de votre page de contenu.</span><span class="sxs-lookup"><span data-stu-id="afd49-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="afd49-122">Liens profonds</span><span class="sxs-lookup"><span data-stu-id="afd49-122">Deep links</span></span>

<span data-ttu-id="afd49-123">Vous pouvez créer des liens profonds vers des entités dans Teams.</span><span class="sxs-lookup"><span data-stu-id="afd49-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="afd49-124">En règle générale, ils sont utilisés pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Voir [Créer des liens profonds vers du contenu et des fonctionnalités dans Microsoft Teams.](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="afd49-124">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="afd49-125">Modules de tâche</span><span class="sxs-lookup"><span data-stu-id="afd49-125">Task Modules</span></span>

<span data-ttu-id="afd49-126">Un module de tâche est une expérience popup modale que vous pouvez déclencher à partir de votre onglet. En règle générale, dans une page de contenu, vous ne souhaitez pas parcourir plusieurs pages pour votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afd49-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="afd49-127">Au lieu de cela, vous allez utiliser des modules de tâche pour présenter des formulaires pour recueillir des informations supplémentaires, afficher les détails d'un élément dans une liste ou toute autre fois que vous devez présenter à l'utilisateur des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="afd49-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="afd49-128">Les modules de tâche eux-mêmes peuvent être des pages de contenu supplémentaires ou être entièrement créés à l'aide de cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="afd49-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="afd49-129">Pour plus [d'informations, voir Utilisation des modules](~/task-modules-and-cards/task-modules/task-modules-tabs.md) de tâche dans les onglets.</span><span class="sxs-lookup"><span data-stu-id="afd49-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="afd49-130">Domaines valides</span><span class="sxs-lookup"><span data-stu-id="afd49-130">Valid Domains</span></span>

<span data-ttu-id="afd49-131">Assurez-vous que tous les domaines d'URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau de votre [manifeste.](~/concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="afd49-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="afd49-132">Pour plus d'informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence du schéma de manifeste.</span><span class="sxs-lookup"><span data-stu-id="afd49-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="afd49-133">Toutefois, n'oubliez pas que les fonctionnalités de base de votre onglet existent dans Teams et non en dehors de Teams.</span><span class="sxs-lookup"><span data-stu-id="afd49-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="afd49-134">Réordesser les onglets personnels statiques</span><span class="sxs-lookup"><span data-stu-id="afd49-134">Reorder static personal tabs</span></span>

<span data-ttu-id="afd49-135">À partir de la version de manifeste 1.7, les développeurs peuvent réorganiser tous les onglets de leur application personnelle.</span><span class="sxs-lookup"><span data-stu-id="afd49-135">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="afd49-136">En particulier, un développeur peut déplacer l'onglet de conversation du *bot,* qui est toujours en première position par défaut, n'importe où dans l'en-tête de l'onglet de l'application personnelle.</span><span class="sxs-lookup"><span data-stu-id="afd49-136">In particular, a developer can move the *bot chat* tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="afd49-137">Nous avons déclaré deux mots clés entityId d'onglet réservé, *conversations* et *à propos de*.</span><span class="sxs-lookup"><span data-stu-id="afd49-137">We’ve declared two reserved tab entityId keywords, *conversations* and *about*.</span></span>

<span data-ttu-id="afd49-138">Si vous créez un bot avec une *étendue* personnelle, il s'affiche par défaut au premier onglet d'une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="afd49-138">If you create a bot with a *personal* scope, it will show up in the first tab position in a personal app by default.</span></span> <span data-ttu-id="afd49-139">Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, *conversations*.</span><span class="sxs-lookup"><span data-stu-id="afd49-139">If you wish to move it to another position, you must add a static tab object to your manifest with the reserved keyword, *conversations*.</span></span> <span data-ttu-id="afd49-140">*L'onglet conversation* s'affiche sur le web ou sur le Bureau en fonction de l'endroit où vous ajoutez l'onglet *de conversation* dans le `staticTabs` tableau.</span><span class="sxs-lookup"><span data-stu-id="afd49-140">The *conversation* tab appears on web or desktop based on where you add the *conversation* tab in the `staticTabs` array.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="afd49-141">Afficher un indicateur de chargement natif</span><span class="sxs-lookup"><span data-stu-id="afd49-141">Show a native loading indicator</span></span>

<span data-ttu-id="afd49-142">À partir du schéma de manifeste [v1.7,](../../../resources/schema/manifest-schema.md)vous pouvez fournir un indicateur de chargement [natif](../../../resources/schema/manifest-schema.md#showloadingindicator) partout où votre contenu web est chargé dans Teams, par [exemple,](#integrate-your-code-with-teams)page de contenu d'onglet, [page de configuration,](configuration-page.md) [page](removal-page.md) de suppression et modules de tâche dans les [onglets.](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="afd49-142">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> 1. <span data-ttu-id="afd49-143">Le comportement sur les clients mobiles n'est pas configurable via cette propriété de manifeste.</span><span class="sxs-lookup"><span data-stu-id="afd49-143">The behavior on mobile clients is not configurable through this manifest property.</span></span> <span data-ttu-id="afd49-144">Les clients mobiles montrent un indicateur de chargement natif par défaut sur les pages de contenu et les modules de tâche iframe.</span><span class="sxs-lookup"><span data-stu-id="afd49-144">Mobile clients show a native loading indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="afd49-145">Cet indicateur sur mobile s'affiche lorsqu'une demande d'extraction de contenu est effectuée et est rejetée dès que la demande est terminée.</span><span class="sxs-lookup"><span data-stu-id="afd49-145">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>
> 2. <span data-ttu-id="afd49-146">Si vous indiquez dans le manifeste de votre application, toutes les pages de configuration, de contenu et de suppression d'onglets et tous les modules de tâche iframe doivent respecter le protocole obligatoire  `"showLoadingIndicator : true`  ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="afd49-146">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>


1. <span data-ttu-id="afd49-147">Pour afficher l'indicateur de chargement, `"showLoadingIndicator": true` ajoutez-le à votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="afd49-147">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="afd49-148">N'oubliez pas d'appeler `microsoftTeams.initialize();` .</span><span class="sxs-lookup"><span data-stu-id="afd49-148">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="afd49-149">**Facultatif**.</span><span class="sxs-lookup"><span data-stu-id="afd49-149">**Optional**.</span></span> <span data-ttu-id="afd49-150">Si vous êtes prêt à imprimer à l'écran et que vous souhaitez charger différée le reste du contenu de votre application, vous pouvez masquer manuellement l'indicateur de chargement en appelant `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="afd49-150">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="afd49-151">**Obligatoire**.</span><span class="sxs-lookup"><span data-stu-id="afd49-151">**Mandatory**.</span></span> <span data-ttu-id="afd49-152">Enfin, appelez `microsoftTeams.appInitialization.notifySuccess()` Teams pour informer Teams que votre application a été correctement chargée.</span><span class="sxs-lookup"><span data-stu-id="afd49-152">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="afd49-153">Teams masquera ensuite l'indicateur de chargement, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="afd49-153">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="afd49-154">Si elle n'est pas appelée dans les 30 secondes, elle est supposée que votre application a été hors délai et qu'un écran d'erreur avec une option de nouvelle tentative  `notifySuccess`  s'affiche.</span><span class="sxs-lookup"><span data-stu-id="afd49-154">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="afd49-155">Si le chargement de votre application échoue, vous pouvez appeler Teams pour lui faire savoir `microsoftTeams.appInitialization.notifyFailure(reason);` qu'une erreur s'est produite.</span><span class="sxs-lookup"><span data-stu-id="afd49-155">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="afd49-156">Un écran d'erreur s'affiche ensuite pour l'utilisateur :</span><span class="sxs-lookup"><span data-stu-id="afd49-156">An error screen will then be shown to the user:</span></span>

```typescript
``
/* List of failure reasons */
export const enum FailedReason {
    AuthFailed = "AuthFailed",
    Timeout = "Timeout",
    Other = "Other"
}
```
>
