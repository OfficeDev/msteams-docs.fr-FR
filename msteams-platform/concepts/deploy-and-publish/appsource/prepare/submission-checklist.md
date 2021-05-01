---
title: Préparer votre soumission au Store
description: Décrit les dernières étapes avant de soumettre votre Microsoft Teams pour qu'elle soit répertoriée dans le Store.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: d46d21c3d984b5688c00857e485210b0f0fcf2c7
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101680"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="9dd11-103">Préparer votre soumission Microsoft Teams store</span><span class="sxs-lookup"><span data-stu-id="9dd11-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="9dd11-104">Vous avez conçu, créé et testé votre application Microsoft Teams web.</span><span class="sxs-lookup"><span data-stu-id="9dd11-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="9dd11-105">Vous êtes maintenant prêt à la réen lister pour que les personnes peuvent découvrir et commencer à utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="9dd11-106">Avant de soumettre votre application à [l'Partner Center,](/office/dev/store/use-partner-center-to-submit-to-appsource)assurez-vous que vous avez effectué les choses suivantes.</span><span class="sxs-lookup"><span data-stu-id="9dd11-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="9dd11-107">Valider votre package d'application</span><span class="sxs-lookup"><span data-stu-id="9dd11-107">Validate your app package</span></span>

<span data-ttu-id="9dd11-108">Bien que votre application fonctionne peut-être dans un environnement de test, vous devez vérifier votre package d'application pour éviter les problèmes pendant le processus de soumission.</span><span class="sxs-lookup"><span data-stu-id="9dd11-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="9dd11-109">L Microsoft Teams de validation d'application vous permet d'identifier et de résoudre les problèmes avant de les soumettre à l'Partner Center.</span><span class="sxs-lookup"><span data-stu-id="9dd11-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="9dd11-110">L'outil vérifie automatiquement les configurations de votre application par rapport aux mêmes cas de test utilisés lors de la validation du Store.</span><span class="sxs-lookup"><span data-stu-id="9dd11-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="9dd11-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span><span class="sxs-lookup"><span data-stu-id="9dd11-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="9dd11-112">(Remarque : l'outil est également disponible [dans App Studio.)](../../../build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9dd11-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="9dd11-113">Télécharger votre package d'application pour exécuter les tests automatisés.</span><span class="sxs-lookup"><span data-stu-id="9dd11-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="9dd11-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span><span class="sxs-lookup"><span data-stu-id="9dd11-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="9dd11-115">[Corrigez les problèmes de configuration ou](~/resources/schema/manifest-schema.md) d'application en général si les tests automatisés vous donnent des erreurs ou si vous n'avez pas satisfait à tous les critères de la liste de contrôle.</span><span class="sxs-lookup"><span data-stu-id="9dd11-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="9dd11-116">Compiler les instructions de test</span><span class="sxs-lookup"><span data-stu-id="9dd11-116">Compile testing instructions</span></span>

<span data-ttu-id="9dd11-117">Fournissez des instructions et des ressources pour aider les réviseurs à tester votre application, y compris les comptes de test, les informations d'identification et les clés de licence.</span><span class="sxs-lookup"><span data-stu-id="9dd11-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="9dd11-118">Vous pouvez ajouter des instructions dans l'Partner Center ou les télécharger vers un emplacement disponible publiquement sur SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dd11-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="9dd11-119">Liste des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="9dd11-119">Feature list</span></span>

<span data-ttu-id="9dd11-120">Fournissez des détails sur les fonctionnalités de votre application dans Teams et les étapes de test de chacune d'elles.</span><span class="sxs-lookup"><span data-stu-id="9dd11-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="9dd11-121">Comptes</span><span class="sxs-lookup"><span data-stu-id="9dd11-121">Accounts</span></span>

<span data-ttu-id="9dd11-122">Vous devez fournir des comptes de test si votre application nécessite une licence ou une liste sécurisée back-end.</span><span class="sxs-lookup"><span data-stu-id="9dd11-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="9dd11-123">Tous les comptes que vous fournissez doivent inclure des données pré-remplies pour faciliter le test.</span><span class="sxs-lookup"><span data-stu-id="9dd11-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="9dd11-124">En fonction des fonctionnalités de votre application, vous devrez peut-être fournir les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9dd11-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="9dd11-125">Compte d'administrateur (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="9dd11-125">Admin account (required)</span></span>
* <span data-ttu-id="9dd11-126">Compte non administrateur (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="9dd11-126">Non-admin account (required)</span></span>
* <span data-ttu-id="9dd11-127">Un compte qui n'est pas pré-configuré afin de tester correctement l'expérience de première utilisation de la première utilisation de la signature (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="9dd11-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="9dd11-128">Un compte ayant accès aux fonctionnalités premium ou mises à niveau (le cas échéant)</span><span class="sxs-lookup"><span data-stu-id="9dd11-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="9dd11-129">Deux comptes dans le même client pour tester l'expérience de collaboration pour les applications qui fonctionnent dans des contextes partagés (le cas échéant)</span><span class="sxs-lookup"><span data-stu-id="9dd11-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="9dd11-130">Configurations client</span><span class="sxs-lookup"><span data-stu-id="9dd11-130">Tenant configurations</span></span>

<span data-ttu-id="9dd11-131">Si vous devez configurer un client Teams pour utiliser votre application, incluez ces instructions et les comptes administrateur et non administrateur pour la validation.</span><span class="sxs-lookup"><span data-stu-id="9dd11-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="9dd11-132">Vidéo (facultatif)</span><span class="sxs-lookup"><span data-stu-id="9dd11-132">Video (optional)</span></span>

<span data-ttu-id="9dd11-133">Fournissez un enregistrement de votre application afin que Microsoft puisse bien comprendre ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="9dd11-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="9dd11-134">Créer les détails de la description dans le Store</span><span class="sxs-lookup"><span data-stu-id="9dd11-134">Create your store listing details</span></span>

<span data-ttu-id="9dd11-135">Les informations que [](https://partner.microsoft.com) vous envoyez à l'&#8212;de l'&#8212;, y compris votre nom, descriptions, icônes et images&#8212;, deviennent le Teams Store et la description Microsoft AppSource de votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="9dd11-136">Une liste dans le Store peut être la première impression de votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="9dd11-137">Augmentez les installations avec une liste qui transmet efficacement les avantages, les fonctionnalités et la marque de votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="9dd11-138">Spécifier un nom court</span><span class="sxs-lookup"><span data-stu-id="9dd11-138">Specify a short name</span></span>

<span data-ttu-id="9dd11-139">Le nom de votre application (en particulier, son nom [*court)*](~/resources/schema/manifest-schema.md#name)joue un rôle crucial dans la façon dont les utilisateurs la découvrent dans le Store.</span><span class="sxs-lookup"><span data-stu-id="9dd11-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Exemple de capture d'écran sur laquelle le nom court d'une application s'affiche dans une liste du Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="9dd11-141">Assurez-vous que votre nom court respecte les instructions [de validation du Store.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)</span><span class="sxs-lookup"><span data-stu-id="9dd11-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="9dd11-142">Écrire des descriptions</span><span class="sxs-lookup"><span data-stu-id="9dd11-142">Write descriptions</span></span>

<span data-ttu-id="9dd11-143">Vous devez avoir une description courte et longue de votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="9dd11-144">Description brève</span><span class="sxs-lookup"><span data-stu-id="9dd11-144">Short description</span></span>

<span data-ttu-id="9dd11-145">Résumé concis de votre application qui doit être original, attrayant et adressé à votre public cible.</span><span class="sxs-lookup"><span data-stu-id="9dd11-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="9dd11-146">Conservez la description courte jusqu'à une phrase.</span><span class="sxs-lookup"><span data-stu-id="9dd11-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Exemple de capture d'écran sur laquelle la description courte d'une application s'affiche dans une description dans le Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="9dd11-148">Assurez-vous que votre brève description respecte les instructions [de validation du Store.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)</span><span class="sxs-lookup"><span data-stu-id="9dd11-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="9dd11-149">Description longue</span><span class="sxs-lookup"><span data-stu-id="9dd11-149">Long description</span></span>

<span data-ttu-id="9dd11-150">La description longue peut fournir un narratif qui met en évidence les principales fonctionnalités de votre application, les problèmes qu'elle résout et son public cible.</span><span class="sxs-lookup"><span data-stu-id="9dd11-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="9dd11-151">Bien que cette description puisse prendre jusqu'à 4 000 caractères, la plupart des utilisateurs ne lisent qu'entre 300 et 500 mots.</span><span class="sxs-lookup"><span data-stu-id="9dd11-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Exemple de capture d'écran sur laquelle la description longue d'une application s'affiche dans une description dans le Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="9dd11-153">Assurez-vous que votre description longue respecte les instructions [de validation du Store.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)</span><span class="sxs-lookup"><span data-stu-id="9dd11-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="9dd11-154">Respecter les instructions de conception des icônes</span><span class="sxs-lookup"><span data-stu-id="9dd11-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="9dd11-155">Les icônes sont l'un des principaux éléments que les utilisateurs voient lors de la navigation dans le Store.</span><span class="sxs-lookup"><span data-stu-id="9dd11-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="9dd11-156">Vos icônes doivent communiquer la marque et l'objectif de votre application tout en respectant les Teams requises.</span><span class="sxs-lookup"><span data-stu-id="9dd11-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="9dd11-157">Pour plus d'informations, voir [les conseils sur la création Teams icônes d'application.](~/concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="9dd11-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="9dd11-158">Capture d'écran</span><span class="sxs-lookup"><span data-stu-id="9dd11-158">Capture screenshots</span></span>

<span data-ttu-id="9dd11-159">Les captures d'écran fournissent un aperçu visuel de votre application pour compléter le nom, l'icône et les descriptions de votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Exemple de capture d'écran sur laquelle les captures d'écran d'application s'affichent dans une liste du Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="9dd11-161">Souvenez-vous des captures d'écran suivantes :</span><span class="sxs-lookup"><span data-stu-id="9dd11-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="9dd11-162">Vous pouvez avoir jusqu'à cinq captures d'écran par liste.</span><span class="sxs-lookup"><span data-stu-id="9dd11-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="9dd11-163">Les types de fichiers pris en charge sont PNG, JPEG et GIF.</span><span class="sxs-lookup"><span data-stu-id="9dd11-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="9dd11-164">Les dimensions doivent être de 1 366 x 768 pixels.</span><span class="sxs-lookup"><span data-stu-id="9dd11-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="9dd11-165">Taille maximale de 1 024 Ko.</span><span class="sxs-lookup"><span data-stu-id="9dd11-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="9dd11-166">Pour obtenir les meilleures pratiques, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="9dd11-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="9dd11-167">Teams de validation du magasin d'informations</span><span class="sxs-lookup"><span data-stu-id="9dd11-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [<span data-ttu-id="9dd11-168">Création d'images efficaces pour les magasins d'applications Microsoft</span><span class="sxs-lookup"><span data-stu-id="9dd11-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="9dd11-169">Créer une vidéo</span><span class="sxs-lookup"><span data-stu-id="9dd11-169">Create a video</span></span>

<span data-ttu-id="9dd11-170">Une vidéo dans votre liste peut être le moyen le plus efficace de communiquer pourquoi les personnes doivent utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="9dd11-171">Vous devez répondre aux questions suivantes dans une vidéo :</span><span class="sxs-lookup"><span data-stu-id="9dd11-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="9dd11-172">Qui votre application est-elle pour ?</span><span class="sxs-lookup"><span data-stu-id="9dd11-172">Who is your app for?</span></span>
* <span data-ttu-id="9dd11-173">Quels problèmes votre application peut-elle résoudre ?</span><span class="sxs-lookup"><span data-stu-id="9dd11-173">What problems can your app solve?</span></span>
* <span data-ttu-id="9dd11-174">Comment fonctionne votre application ?</span><span class="sxs-lookup"><span data-stu-id="9dd11-174">How does your app work?</span></span>
* <span data-ttu-id="9dd11-175">Quels autres avantages bénéficiez-vous de l'utilisation de votre application ?</span><span class="sxs-lookup"><span data-stu-id="9dd11-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="9dd11-176">Meilleures pratiques pour les vidéos</span><span class="sxs-lookup"><span data-stu-id="9dd11-176">Best practices for videos</span></span>

* <span data-ttu-id="9dd11-177">Conservez votre vidéo entre 30 et 90 secondes.</span><span class="sxs-lookup"><span data-stu-id="9dd11-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="9dd11-178">Visez la qualité.</span><span class="sxs-lookup"><span data-stu-id="9dd11-178">Aim for quality.</span></span> <span data-ttu-id="9dd11-179">Dans une liste, les utilisateurs voient votre vidéo avant les captures d'écran.</span><span class="sxs-lookup"><span data-stu-id="9dd11-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="9dd11-180">Sélectionner une catégorie pour votre application</span><span class="sxs-lookup"><span data-stu-id="9dd11-180">Select a category for your app</span></span>

<span data-ttu-id="9dd11-181">Lors de la soumission, vous êtes invité à catégoriser votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="9dd11-182">Le tableau suivant ma Teams catégories de magasin aux catégories répertoriées dans [l'Partner Center](https://aka.ms/PartnerCenterHomePage).</span><span class="sxs-lookup"><span data-stu-id="9dd11-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="9dd11-183">Teams catégories</span><span class="sxs-lookup"><span data-stu-id="9dd11-183">Teams categories</span></span>       | <span data-ttu-id="9dd11-184">Catégories de l'Centre partenaires</span><span class="sxs-lookup"><span data-stu-id="9dd11-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="9dd11-185">Analyse et bi</span><span class="sxs-lookup"><span data-stu-id="9dd11-185">Analytics and BI</span></span> | <span data-ttu-id="9dd11-186">Analyse, visualisation des données et bi</span><span class="sxs-lookup"><span data-stu-id="9dd11-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="9dd11-187">Développeur et informatique</span><span class="sxs-lookup"><span data-stu-id="9dd11-187">Developer and IT</span></span> | <span data-ttu-id="9dd11-188">Outils de développement, administrateur informatique</span><span class="sxs-lookup"><span data-stu-id="9dd11-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="9dd11-189">Éducation</span><span class="sxs-lookup"><span data-stu-id="9dd11-189">Education</span></span> | <span data-ttu-id="9dd11-190">Éducation</span><span class="sxs-lookup"><span data-stu-id="9dd11-190">Education</span></span> |
| <span data-ttu-id="9dd11-191">Ressources humaines</span><span class="sxs-lookup"><span data-stu-id="9dd11-191">Human resources</span></span> | <span data-ttu-id="9dd11-192">Ressources humaines et recrutement</span><span class="sxs-lookup"><span data-stu-id="9dd11-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="9dd11-193">Productivité</span><span class="sxs-lookup"><span data-stu-id="9dd11-193">Productivity</span></span> | <span data-ttu-id="9dd11-194">Gestion de contenu, fichiers et documents, productivité, formation et didacticiels, et utilitaires</span><span class="sxs-lookup"><span data-stu-id="9dd11-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="9dd11-195">Gestion de projet</span><span class="sxs-lookup"><span data-stu-id="9dd11-195">Project management</span></span> | <span data-ttu-id="9dd11-196">Communication, gestion Project, flux de travail et gestion de l'entreprise</span><span class="sxs-lookup"><span data-stu-id="9dd11-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="9dd11-197">Ventes et support</span><span class="sxs-lookup"><span data-stu-id="9dd11-197">Sales and support</span></span> | <span data-ttu-id="9dd11-198">Gestion des clients et des contacts, support client, gestion financière, ventes et marketing</span><span class="sxs-lookup"><span data-stu-id="9dd11-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="9dd11-199">Social et fun</span><span class="sxs-lookup"><span data-stu-id="9dd11-199">Social and fun</span></span> | <span data-ttu-id="9dd11-200">Galeries d'images et de vidéos, style de vie, actualités et météo, réseau social, voyage et navigation</span><span class="sxs-lookup"><span data-stu-id="9dd11-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="9dd11-201">Localisez votre liste dans le Store</span><span class="sxs-lookup"><span data-stu-id="9dd11-201">Localize your store listing</span></span>

<span data-ttu-id="9dd11-202">L'Partner Center prend [en charge les listes de magasins localisées.](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)</span><span class="sxs-lookup"><span data-stu-id="9dd11-202">Partner Center supports [localized store listings](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="9dd11-203">Pour plus d'informations, voir comment localiser votre [liste Teams'application.](../../../../concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="9dd11-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="9dd11-204">Vérification Publisher complète</span><span class="sxs-lookup"><span data-stu-id="9dd11-204">Complete Publisher Verification</span></span>

<span data-ttu-id="9dd11-205">[Publisher vérification est](/azure/active-directory/develop/publisher-verification-overview) requise pour Teams applications répertoriées dans le Windows Store. Pour plus d'informations, voir [les questions fréquemment posées,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)comment marquer votre application comme éditeur vérifié et résoudre les problèmes de vérification de [l'éditeur](/azure/active-directory/develop/troubleshoot-publisher-verification). [](/azure/active-directory/develop/mark-app-as-publisher-verified)</span><span class="sxs-lookup"><span data-stu-id="9dd11-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="9dd11-206">Attestation d'Publisher complète</span><span class="sxs-lookup"><span data-stu-id="9dd11-206">Complete Publisher Attestation</span></span>

<span data-ttu-id="9dd11-207">[Publisher attestation est](/microsoft-365-app-certification/docs/attestation) également requise pour Teams applications répertoriées dans le Windows Store.</span><span class="sxs-lookup"><span data-stu-id="9dd11-207">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="9dd11-208">Le processus inclut la réalisation d'une auto-évaluation de la sécurité, de la gestion des données et des pratiques de conformité de votre application qui peuvent aider les clients potentiels à prendre des décisions éclairées sur l'utilisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="9dd11-208">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="9dd11-209">Si vous soumettez une nouvelle application, vous ne pouvez pas terminer officiellement l'attestation d'Publisher tant que votre application n'est pas répertoriée dans le Teams store.</span><span class="sxs-lookup"><span data-stu-id="9dd11-209">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="9dd11-210">Si vous êtes en train de mettre à jour une application répertoriée, Publisher attestation avant de soumettre la dernière version de l'application pour validation.</span><span class="sxs-lookup"><span data-stu-id="9dd11-210">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="9dd11-211">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="9dd11-211">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9dd11-212">Soumettre votre application</span><span class="sxs-lookup"><span data-stu-id="9dd11-212">Submit your app</span></span>](https://docs.microsoft.com/office/dev/store/add-in-submission-guide)
