---
title: Créer une page de contenu
author: laujan
description: ''
keywords: onglets teams groupe de canaux configurable statique
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: ac85e000c9bdaebf28cb33143a7c82a348d3771e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673789"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="bf703-103">Créer une page de contenu pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="bf703-103">Create a content page for your tab</span></span>

<span data-ttu-id="bf703-104">Une page de contenu est une page Web qui s’affiche dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="bf703-104">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="bf703-105">En règle générale, il s’agit des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf703-105">Typically these are part of:</span></span>

* <span data-ttu-id="bf703-106">Onglet personnalisé d’étendue personnelle : cette instance de contenu est la première page rencontrée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bf703-106">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="bf703-107">Un onglet personnalisé canal/groupe-une fois que l’utilisateur épingle et configure l’onglet dans le contexte approprié, la page de contenu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bf703-107">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="bf703-108">Un [module de tâches](~/task-modules-and-cards/what-are-task-modules.md) : vous pouvez créer une page de contenu et l’incorporer en tant que WebView à l’intérieur d’un module de tâches.</span><span class="sxs-lookup"><span data-stu-id="bf703-108">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="bf703-109">La page s’affiche dans le menu contextuel modal.</span><span class="sxs-lookup"><span data-stu-id="bf703-109">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="bf703-110">Cet article est spécifique à l’utilisation des pages de contenu en tant qu’onglets ; Toutefois, la majorité des conseils s’appliquent indépendamment de la présentation de la page de contenu à l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="bf703-110">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="bf703-111">Contenu des onglets et règles de style</span><span class="sxs-lookup"><span data-stu-id="bf703-111">Tab content and style guidelines</span></span>

<span data-ttu-id="bf703-112">L’objectif général de votre onglet doit être de fournir un accès à du contenu pertinent et attrayant qui a une valeur pratique et un objectif évident.</span><span class="sxs-lookup"><span data-stu-id="bf703-112">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="bf703-113">Cela ne signifie pas que vous devez vous conformer à un style agréable, mais vous devez vous concentrer sur la réduction du courrier non trié en rendant le design de votre onglet propre, intuitif et le contenu immersif.</span><span class="sxs-lookup"><span data-stu-id="bf703-113">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="bf703-114">Voir le [contenu et les conversations, en même temps à l’aide des onglets et de l’aide sur](~/tabs/design/tabs.md) le [processus d’approbation des applications Microsoft teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="bf703-114">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="bf703-115">Intégration de votre code à teams</span><span class="sxs-lookup"><span data-stu-id="bf703-115">Integrate your code with Teams</span></span>

<span data-ttu-id="bf703-116">Pour que votre page s’affiche dans Teams, vous devez inclure le [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) et inclure un appel à `microsoftTeams.initialize()` après le chargement de votre page.</span><span class="sxs-lookup"><span data-stu-id="bf703-116">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="bf703-117">Voici comment votre page et le client teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="bf703-117">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="bf703-118">Accès à du contenu supplémentaire</span><span class="sxs-lookup"><span data-stu-id="bf703-118">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="bf703-119">Utilisation du kit de développement logiciel (SDK) pour interagir avec teams</span><span class="sxs-lookup"><span data-stu-id="bf703-119">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="bf703-120">Le [Kit de développement logiciel (SDK) du client teams](~/tabs/how-to/using-teams-client-sdk.md) fournit de nombreuses fonctions supplémentaires que vous pouvez trouver utiles lorsque vous développez votre page de contenu.</span><span class="sxs-lookup"><span data-stu-id="bf703-120">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developer your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="bf703-121">Liens profonds</span><span class="sxs-lookup"><span data-stu-id="bf703-121">Deep links</span></span>

<span data-ttu-id="bf703-122">Vous pouvez créer des liens approfondis vers des entités dans Teams.</span><span class="sxs-lookup"><span data-stu-id="bf703-122">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="bf703-123">En règle générale, ces éléments sont utilisés pour créer des liens qui naviguent vers le contenu et les informations au sein de votre onglet. Voir [créer des liens détaillés vers du contenu et des fonctionnalités dans Microsoft teams](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="bf703-123">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="bf703-124">Modules de tâches</span><span class="sxs-lookup"><span data-stu-id="bf703-124">Task Modules</span></span>

<span data-ttu-id="bf703-125">Un module de tâches est une expérience de type popup modale que vous pouvez déclencher à partir de votre onglet. généralement dans une page de contenu, vous ne souhaitez pas parcourir votre utilisateur sur plusieurs pages.</span><span class="sxs-lookup"><span data-stu-id="bf703-125">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="bf703-126">Au lieu de cela, vous utiliserez des modules de tâches pour présenter des formulaires permettant de collecter des informations supplémentaires, en affichant les détails d’un élément dans une liste ou à tout autre moment pour présenter à l’utilisateur des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="bf703-126">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="bf703-127">Les modules de tâches eux-mêmes peuvent être des pages de contenu supplémentaires ou être entièrement créés à l’aide de cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="bf703-127">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="bf703-128">Pour obtenir des informations complètes, voir [utilisation des modules de tâches dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md) .</span><span class="sxs-lookup"><span data-stu-id="bf703-128">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="bf703-129">Domaines valides</span><span class="sxs-lookup"><span data-stu-id="bf703-129">Valid Domains</span></span>

<span data-ttu-id="bf703-130">Assurez-vous que tous les domaines d’URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau dans votre [manifeste](~/concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="bf703-130">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="bf703-131">Pour plus d’informations, consultez la rubrique [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence de schéma de manifeste.</span><span class="sxs-lookup"><span data-stu-id="bf703-131">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="bf703-132">Toutefois, gardez à l’esprit que la fonctionnalité principale de votre onglet existe dans teams et non en dehors de teams.</span><span class="sxs-lookup"><span data-stu-id="bf703-132">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>
