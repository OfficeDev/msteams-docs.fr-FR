---
title: Créer une page de contenu
author: laujan
description: comment créer une page de contenu
keywords: équipes onglets canal de groupe configurable statique
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 136160cb9154d62be40d8e29075ac1fc86135a6b
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566676"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="915dc-104">Créez une page de contenu pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="915dc-104">Create a content page for your tab</span></span>

<span data-ttu-id="915dc-105">Une page de contenu est une page Web qui est rendue dans le Teams client.</span><span class="sxs-lookup"><span data-stu-id="915dc-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="915dc-106">En règle générale, ceux-ci font partie de:</span><span class="sxs-lookup"><span data-stu-id="915dc-106">Typically these are part of:</span></span>

* <span data-ttu-id="915dc-107">Onglet personnalisé à portée personnelle : dans ce cas, la page de contenu est la première page que l’utilisateur rencontre.</span><span class="sxs-lookup"><span data-stu-id="915dc-107">A personal-scoped custom tab: In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="915dc-108">Onglet personnalisé canal/groupe : après que l’utilisateur épingle et configure l’onglet dans le contexte approprié, la page de contenu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="915dc-108">A channel/group custom tab: After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="915dc-109">Un [module de tâches :](~/task-modules-and-cards/what-are-task-modules.md)Vous pouvez créer une page de contenu et l’intégrer comme une webview à l’intérieur d’un module de tâches.</span><span class="sxs-lookup"><span data-stu-id="915dc-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="915dc-110">La page sera rendue à l’intérieur du popup modal.</span><span class="sxs-lookup"><span data-stu-id="915dc-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="915dc-111">Cet article est spécifique à l’utilisation de pages de contenu comme onglets; toutefois, la majorité des directives ici s’appliqueraient indépendamment de la façon dont la page de contenu est présentée à l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="915dc-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="915dc-112">Lignes directrices sur le contenu et la conception des onglets</span><span class="sxs-lookup"><span data-stu-id="915dc-112">Tab content and design guidelines</span></span>

<span data-ttu-id="915dc-113">L’objectif global de votre onglet devrait être de fournir l’accès à un contenu significatif et engageant qui a une valeur pratique et un but évident.</span><span class="sxs-lookup"><span data-stu-id="915dc-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="915dc-114">Cela ne signifie pas que vous devriez renoncer à un style agréable, mais vous devez vous concentrer sur la minimisation de l’encombrement en rendant votre conception d’onglet propre, navigation intuitive, et le contenu immersif.</span><span class="sxs-lookup"><span data-stu-id="915dc-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="915dc-115">Pour plus d’informations, consultez les lignes [directrices de conception des onglets](~/tabs/design/tabs.md) [et les Microsoft Teams de validation des magasins](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span><span class="sxs-lookup"><span data-stu-id="915dc-115">For more information, see the [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="915dc-116">Intégrez votre code à Teams</span><span class="sxs-lookup"><span data-stu-id="915dc-116">Integrate your code with Teams</span></span>

<span data-ttu-id="915dc-117">Pour que votre page s’affiche en Teams, vous devez [inclure le client JavaScript Microsoft Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et inclure un appel `microsoftTeams.initialize()` après que votre page se charge.</span><span class="sxs-lookup"><span data-stu-id="915dc-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="915dc-118">C’est ainsi que votre page et Teams client communiquent :</span><span class="sxs-lookup"><span data-stu-id="915dc-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="915dc-119">Accès à du contenu supplémentaire</span><span class="sxs-lookup"><span data-stu-id="915dc-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="915dc-120">Utiliser le SDK pour interagir avec Teams</span><span class="sxs-lookup"><span data-stu-id="915dc-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="915dc-121">Le [Teams client JavaScript SDK fournit de nombreuses](~/tabs/how-to/using-teams-client-sdk.md) fonctions supplémentaires que vous pouvez trouver utiles lors du développement de votre page de contenu.</span><span class="sxs-lookup"><span data-stu-id="915dc-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="915dc-122">Liens profonds</span><span class="sxs-lookup"><span data-stu-id="915dc-122">Deep links</span></span>

<span data-ttu-id="915dc-123">Vous pouvez créer des liens profonds avec des entités en Teams.</span><span class="sxs-lookup"><span data-stu-id="915dc-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="915dc-124">En règle générale, ceux-ci sont utilisés pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Pour plus d’informations, [voir Créer des liens profonds vers le contenu et les fonctionnalités dans Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="915dc-124">Typically, these are used to create links that navigate to content and information within your tab. For more information, see [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="915dc-125">Modules de tâches</span><span class="sxs-lookup"><span data-stu-id="915dc-125">Task Modules</span></span>

<span data-ttu-id="915dc-126">Un module de tâche est une expérience modale popup-like que vous pouvez déclencher à partir de votre onglet. En règle générale, dans une page de contenu, vous ne souhaitez pas naviguer sur votre utilisateur à travers plusieurs pages.</span><span class="sxs-lookup"><span data-stu-id="915dc-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="915dc-127">Au lieu de cela, vous utiliserez des modules de tâches pour présenter des formulaires pour recueillir des informations supplémentaires, afficher les détails d’un élément dans une liste, ou tout autre moment où vous devez présenter à l’utilisateur des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="915dc-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="915dc-128">Les modules de tâches eux-mêmes peuvent être des pages de contenu supplémentaires, ou créés complètement à l’aide de cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="915dc-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="915dc-129">Voir Utilisation [de modules de tâches dans les onglets pour](~/task-modules-and-cards/task-modules/task-modules-tabs.md) des informations complètes.</span><span class="sxs-lookup"><span data-stu-id="915dc-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="915dc-130">Domaines valides</span><span class="sxs-lookup"><span data-stu-id="915dc-130">Valid Domains</span></span>

<span data-ttu-id="915dc-131">Assurez-vous que tous les domaines URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau dans votre [manifeste](~/concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="915dc-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="915dc-132">Pour plus d’informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence manifeste du schéma.</span><span class="sxs-lookup"><span data-stu-id="915dc-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="915dc-133">Cependant, n’oubliez pas que la fonctionnalité de base de votre onglet existe dans Teams et non en dehors de Teams.</span><span class="sxs-lookup"><span data-stu-id="915dc-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="915dc-134">Réorganiser les onglets personnels statiques</span><span class="sxs-lookup"><span data-stu-id="915dc-134">Reorder static personal tabs</span></span>

<span data-ttu-id="915dc-135">À partir de la version manifeste 1.7, les développeurs peuvent réorganiser tous les onglets de leur application personnelle.</span><span class="sxs-lookup"><span data-stu-id="915dc-135">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="915dc-136">En particulier, un développeur peut déplacer l’onglet *de chat bot,* qui est toujours par défaut à la première position, n’importe où dans l’en-tête de l’onglet application personnelle.</span><span class="sxs-lookup"><span data-stu-id="915dc-136">In particular, a developer can move the *bot chat* tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="915dc-137">Nous avons déclaré deux mots clés, conversations et *environ* *.*</span><span class="sxs-lookup"><span data-stu-id="915dc-137">We’ve declared two reserved tab entityId keywords, *conversations* and *about*.</span></span>

<span data-ttu-id="915dc-138">Si vous créez un bot avec une *portée* personnelle, il s’affichera dans la première position de l’onglet dans une application personnelle par défaut.</span><span class="sxs-lookup"><span data-stu-id="915dc-138">If you create a bot with a *personal* scope, it will show up in the first tab position in a personal app by default.</span></span> <span data-ttu-id="915dc-139">Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, *conversations*.</span><span class="sxs-lookup"><span data-stu-id="915dc-139">If you wish to move it to another position, you must add a static tab object to your manifest with the reserved keyword, *conversations*.</span></span> <span data-ttu-id="915dc-140">*L’onglet conversation* s’affiche sur le Web ou le bureau en fonction de l’endroit où vous ajoutez *l’onglet conversation* dans le `staticTabs` tableau.</span><span class="sxs-lookup"><span data-stu-id="915dc-140">The *conversation* tab appears on web or desktop based on where you add the *conversation* tab in the `staticTabs` array.</span></span> 

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

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="915dc-141">Afficher un indicateur de chargement natif</span><span class="sxs-lookup"><span data-stu-id="915dc-141">Show a native loading indicator</span></span>

<span data-ttu-id="915dc-142">En commençant [par le schéma manifeste v1.7](../../../resources/schema/manifest-schema.md), vous pouvez fournir un indicateur de chargement natif [partout](../../../resources/schema/manifest-schema.md#showloadingindicator) où votre contenu Web est chargé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="915dc-142">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams.</span></span> <span data-ttu-id="915dc-143">Par exemple, page [de contenu d’onglet,](#integrate-your-code-with-teams) [page de configuration,](configuration-page.md) [page de suppression,](removal-page.md) [et modules de tâche dans les onglets.](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="915dc-143">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="915dc-144">Le comportement sur les clients mobiles n’est pas configurable grâce à cette propriété manifeste.</span><span class="sxs-lookup"><span data-stu-id="915dc-144">The behavior on mobile clients is not configurable through this manifest property.</span></span> <span data-ttu-id="915dc-145">Les clients mobiles affichent un indicateur de chargement natif par défaut sur toutes les pages de contenu et les modules de tâches basés sur iframe.</span><span class="sxs-lookup"><span data-stu-id="915dc-145">Mobile clients show a native loading indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="915dc-146">Cet indicateur sur mobile s’affiche lorsqu’une demande est faite pour récupérer du contenu et est rejeté dès que la demande est terminée.</span><span class="sxs-lookup"><span data-stu-id="915dc-146">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>
> * <span data-ttu-id="915dc-147">Si vous indiquez  `"showLoadingIndicator : true`  dans votre manifeste d’application, alors toutes les pages de configuration, de contenu et de suppression d’onglets et tous les modules de tâches basés sur iframe doivent suivre le protocole obligatoire, ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="915dc-147">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

<span data-ttu-id="915dc-148">**Pour afficher l’indicateur de chargement**</span><span class="sxs-lookup"><span data-stu-id="915dc-148">**To show the loading indicator**</span></span>

* <span data-ttu-id="915dc-149">Ajoutez `"showLoadingIndicator": true` à votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="915dc-149">Add `"showLoadingIndicator": true` to your manifest.</span></span> 
* <span data-ttu-id="915dc-150">N’oubliez pas d’appeler `microsoftTeams.initialize();` .</span><span class="sxs-lookup"><span data-stu-id="915dc-150">Remember to call `microsoftTeams.initialize();`.</span></span>
* <span data-ttu-id="915dc-151">**Facultatif**: Si vous êtes prêt à imprimer à l’écran et souhaitez charger paresseux le reste du contenu de votre application, vous pouvez masquer manuellement l’indicateur de chargement en appelant `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="915dc-151">**Optional**: If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
* <span data-ttu-id="915dc-152">**Obligatoire**: Enfin, appelez `microsoftTeams.appInitialization.notifySuccess()` pour informer Teams que votre application a chargé avec succès.</span><span class="sxs-lookup"><span data-stu-id="915dc-152">**Mandatory**: Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="915dc-153">Teams cachera alors l’indicateur de chargement le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="915dc-153">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="915dc-154">Si  `notifySuccess`  elle n’est pas appelée dans les 30 secondes, on suppose que votre application est expirée et qu’un écran d’erreur avec une option de nouvelle tentative s’affiche.</span><span class="sxs-lookup"><span data-stu-id="915dc-154">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
* <span data-ttu-id="915dc-155">Si votre application ne se charge pas, vous pouvez appeler pour `microsoftTeams.appInitialization.notifyFailure(reason);` vous faire savoir Teams’il y a eu une erreur.</span><span class="sxs-lookup"><span data-stu-id="915dc-155">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="915dc-156">Un écran d’erreur sera alors affiché à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="915dc-156">An error screen will then be shown to the user:</span></span>

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
