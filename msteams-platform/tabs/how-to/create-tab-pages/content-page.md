---
title: Créer une page de contenu
author: laujan
description: procédure de création d’une page de contenu
keywords: onglets teams groupe de canaux configurable statique
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 91a7d643d3a631610989e31eae14265cd725dbd0
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818905"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="95f55-104">Créer une page de contenu pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="95f55-104">Create a content page for your tab</span></span>

<span data-ttu-id="95f55-105">Une page de contenu est une page Web qui s’affiche dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="95f55-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="95f55-106">En règle générale, il s’agit des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="95f55-106">Typically these are part of:</span></span>

* <span data-ttu-id="95f55-107">Onglet personnalisé d’étendue personnelle : cette instance de contenu est la première page rencontrée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="95f55-107">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="95f55-108">Un onglet personnalisé canal/groupe-une fois que l’utilisateur épingle et configure l’onglet dans le contexte approprié, la page de contenu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="95f55-108">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="95f55-109">Un [module de tâches](~/task-modules-and-cards/what-are-task-modules.md) : vous pouvez créer une page de contenu et l’incorporer en tant que WebView à l’intérieur d’un module de tâches.</span><span class="sxs-lookup"><span data-stu-id="95f55-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="95f55-110">La page s’affiche dans le menu contextuel modal.</span><span class="sxs-lookup"><span data-stu-id="95f55-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="95f55-111">Cet article est spécifique à l’utilisation des pages de contenu en tant qu’onglets ; Toutefois, la majorité des conseils s’appliquent indépendamment de la présentation de la page de contenu à l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="95f55-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="95f55-112">Contenu des onglets et règles de style</span><span class="sxs-lookup"><span data-stu-id="95f55-112">Tab content and style guidelines</span></span>

<span data-ttu-id="95f55-113">L’objectif général de votre onglet doit être de fournir un accès à du contenu pertinent et attrayant qui a une valeur pratique et un objectif évident.</span><span class="sxs-lookup"><span data-stu-id="95f55-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="95f55-114">Cela ne signifie pas que vous devez vous conformer à un style agréable, mais vous devez vous concentrer sur la réduction du courrier non trié en rendant le design de votre onglet propre, intuitif et le contenu immersif.</span><span class="sxs-lookup"><span data-stu-id="95f55-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="95f55-115">Voir le [contenu et les conversations, en même temps à l’aide des onglets et de l’aide sur](~/tabs/design/tabs.md) le [processus d’approbation des applications Microsoft teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="95f55-115">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="95f55-116">Intégration de votre code à teams</span><span class="sxs-lookup"><span data-stu-id="95f55-116">Integrate your code with Teams</span></span>

<span data-ttu-id="95f55-117">Pour que votre page s’affiche dans Teams, vous devez inclure le [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) et inclure un appel à `microsoftTeams.initialize()` après le chargement de votre page.</span><span class="sxs-lookup"><span data-stu-id="95f55-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="95f55-118">Voici comment votre page et le client teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="95f55-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="95f55-119">Accès à du contenu supplémentaire</span><span class="sxs-lookup"><span data-stu-id="95f55-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="95f55-120">Utilisation du kit de développement logiciel (SDK) pour interagir avec teams</span><span class="sxs-lookup"><span data-stu-id="95f55-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="95f55-121">Le [Kit de développement logiciel (SDK) du client teams](~/tabs/how-to/using-teams-client-sdk.md) fournit de nombreuses fonctions supplémentaires que vous pouvez trouver utiles lorsque vous développez votre page de contenu.</span><span class="sxs-lookup"><span data-stu-id="95f55-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developer your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="95f55-122">Liens profonds</span><span class="sxs-lookup"><span data-stu-id="95f55-122">Deep links</span></span>

<span data-ttu-id="95f55-123">Vous pouvez créer des liens approfondis vers des entités dans Teams.</span><span class="sxs-lookup"><span data-stu-id="95f55-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="95f55-124">En règle générale, ces éléments sont utilisés pour créer des liens qui naviguent vers le contenu et les informations au sein de votre onglet. Voir [créer des liens détaillés vers du contenu et des fonctionnalités dans Microsoft teams](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="95f55-124">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="95f55-125">Modules de tâches</span><span class="sxs-lookup"><span data-stu-id="95f55-125">Task Modules</span></span>

<span data-ttu-id="95f55-126">Un module de tâches est une expérience de type popup modale que vous pouvez déclencher à partir de votre onglet. En règle générale, dans une page de contenu, vous ne souhaitez pas parcourir votre utilisateur sur plusieurs pages.</span><span class="sxs-lookup"><span data-stu-id="95f55-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="95f55-127">Au lieu de cela, vous utiliserez des modules de tâches pour présenter des formulaires permettant de collecter des informations supplémentaires, en affichant les détails d’un élément dans une liste ou à tout autre moment pour présenter à l’utilisateur des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="95f55-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="95f55-128">Les modules de tâches eux-mêmes peuvent être des pages de contenu supplémentaires ou être entièrement créés à l’aide de cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="95f55-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="95f55-129">Pour obtenir des informations complètes, voir [utilisation des modules de tâches dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md) .</span><span class="sxs-lookup"><span data-stu-id="95f55-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="95f55-130">Domaines valides</span><span class="sxs-lookup"><span data-stu-id="95f55-130">Valid Domains</span></span>

<span data-ttu-id="95f55-131">Assurez-vous que tous les domaines d’URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau dans votre [manifeste](~/concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="95f55-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="95f55-132">Pour plus d’informations, consultez la rubrique [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence de schéma de manifeste.</span><span class="sxs-lookup"><span data-stu-id="95f55-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="95f55-133">Toutefois, gardez à l’esprit que la fonctionnalité principale de votre onglet existe dans teams et non en dehors de teams.</span><span class="sxs-lookup"><span data-stu-id="95f55-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="95f55-134">Afficher un indicateur de chargement natif</span><span class="sxs-lookup"><span data-stu-id="95f55-134">Show a native loading indicator</span></span>

<span data-ttu-id="95f55-135">À partir [du schéma de manifeste version 1.7](../../../resources/schema/manifest-schema.md), vous pouvez fournir un indicateur de [chargement natif](../../../resources/schema/manifest-schema.md#showloadingindicator) où le contenu de votre site Web est chargé dans Teams, par exemple, page de contenu de l' [onglet](#integrate-your-code-with-teams), page de [configuration](configuration-page.md), [page de suppression](removal-page.md) et [modules de tâches dans les onglets](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="95f55-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="95f55-136">Si vous indiquez  `"showLoadingIndicator : true`  dans votre manifeste d’application, toutes les pages de configuration d’onglet, de contenu et de suppression, ainsi que tous les modules de tâches basés sur iframe doivent suivre le protocole obligatoire, ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="95f55-136">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

1. <span data-ttu-id="95f55-137">Pour afficher l’indicateur de chargement, ajoutez `"showLoadingIndicator": true` à votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="95f55-137">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="95f55-138">N’oubliez pas d’appeler `microsoftTeams.initialize();` .</span><span class="sxs-lookup"><span data-stu-id="95f55-138">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="95f55-139">**Facultatif**.</span><span class="sxs-lookup"><span data-stu-id="95f55-139">**Optional**.</span></span> <span data-ttu-id="95f55-140">Si vous êtes prêt à imprimer à l’écran et si vous souhaitez charger en différé le reste du contenu de votre application, vous pouvez masquer manuellement l’indicateur de chargement en appelant `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="95f55-140">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="95f55-141">**Obligatoire**.</span><span class="sxs-lookup"><span data-stu-id="95f55-141">**Mandatory**.</span></span> <span data-ttu-id="95f55-142">Enfin, appelez `microsoftTeams.appInitialization.notifySuccess()` pour avertir les équipes que votre application a été chargée avec succès.</span><span class="sxs-lookup"><span data-stu-id="95f55-142">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="95f55-143">Le cas échéant, teams masque l’indicateur de chargement.</span><span class="sxs-lookup"><span data-stu-id="95f55-143">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="95f55-144">Si  `notifySuccess`  n’est pas appelé dans les 30 secondes, il est supposé que votre application a expiré et un écran d’erreur contenant une option Retry apparaît.</span><span class="sxs-lookup"><span data-stu-id="95f55-144">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="95f55-145">Si votre application ne se charge pas, vous pouvez appeler `microsoftTeams.appInitialization.notifyFailure(reason);` pour informer les équipes qu’une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="95f55-145">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="95f55-146">Un écran d’erreur s’affiche ensuite à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="95f55-146">An error screen will then be shown to the user:</span></span>

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
