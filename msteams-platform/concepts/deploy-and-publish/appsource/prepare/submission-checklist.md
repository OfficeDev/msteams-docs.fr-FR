---
title: Préparer l'envoi de votre magasin
description: Décrit les dernières étapes avant de soumettre votre Microsoft Teams’application à coté sur le magasin.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 975d3ef8fc8bdc8d6d7c336cf3a61a3a42ef5315
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566032"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="9e734-103">Préparez votre soumission Microsoft Teams magasin</span><span class="sxs-lookup"><span data-stu-id="9e734-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="9e734-104">Vous avez conçu, construit et testé votre application Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9e734-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="9e734-105">Maintenant, vous êtes prêt à l’énumérer afin que les gens puissent découvrir et commencer à utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="9e734-106">Avant de soumettre votre application à [Partner Center,](/office/dev/store/use-partner-center-to-submit-to-appsource)assurez-vous d’avoir fait ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="9e734-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="9e734-107">Valider votre package d’application</span><span class="sxs-lookup"><span data-stu-id="9e734-107">Validate your app package</span></span>

<span data-ttu-id="9e734-108">Bien que votre application fonctionne peut-être dans un environnement de test, vous devez vérifier votre paquet d’applications pour éviter de tomber sur des problèmes pendant le processus de soumission.</span><span class="sxs-lookup"><span data-stu-id="9e734-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="9e734-109">L’Microsoft Teams validation d’application vous aide à identifier et à résoudre les problèmes avant de vous soumettre au Partner Center.</span><span class="sxs-lookup"><span data-stu-id="9e734-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="9e734-110">L’outil vérifie automatiquement les configurations de votre application par rapport aux mêmes cas de test utilisés lors de la validation en magasin.</span><span class="sxs-lookup"><span data-stu-id="9e734-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="9e734-111">Allez à [l’outil Microsoft Teams validation de l’application](https://dev.teams.microsoft.com/appvalidation.html).</span><span class="sxs-lookup"><span data-stu-id="9e734-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="9e734-112">(Note: L’outil est également disponible dans [App Studio](../../../build-and-test/app-studio-overview.md).)</span><span class="sxs-lookup"><span data-stu-id="9e734-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="9e734-113">Télécharger paquet d’applications pour exécuter les tests automatisés.</span><span class="sxs-lookup"><span data-stu-id="9e734-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="9e734-114">Consultez la liste **de vérification préliminaire et** examinez les cas de test difficiles à automatiser.</span><span class="sxs-lookup"><span data-stu-id="9e734-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="9e734-115">[Résoudre les problèmes avec vos configurations ou](~/resources/schema/manifest-schema.md) application en général si les tests automatisés vous donnent des erreurs ou si vous n’avez pas satisfait à tous les critères de la liste de contrôle.</span><span class="sxs-lookup"><span data-stu-id="9e734-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="9e734-116">Compiler les instructions de test</span><span class="sxs-lookup"><span data-stu-id="9e734-116">Compile testing instructions</span></span>

<span data-ttu-id="9e734-117">Fournissez des instructions et des ressources pour aider les examinateurs à tester votre application, y compris les comptes de test, les informations d’identification et les clés de licence.</span><span class="sxs-lookup"><span data-stu-id="9e734-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="9e734-118">Vous pouvez ajouter des instructions dans Partner Center ou les télécharger sur un emplacement accessible au public sur SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9e734-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="9e734-119">Liste des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="9e734-119">Feature list</span></span>

<span data-ttu-id="9e734-120">Fournissez des détails sur les capacités de votre application dans Teams et les étapes pour tester chacune d’entre vous.</span><span class="sxs-lookup"><span data-stu-id="9e734-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="9e734-121">Comptes</span><span class="sxs-lookup"><span data-stu-id="9e734-121">Accounts</span></span>

<span data-ttu-id="9e734-122">Vous devez fournir des comptes de test si votre application nécessite une licence ou une liste de sécurité backend.</span><span class="sxs-lookup"><span data-stu-id="9e734-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="9e734-123">Tous les comptes que vous fournissez doivent inclure des données pré-remplies pour faciliter les tests.</span><span class="sxs-lookup"><span data-stu-id="9e734-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="9e734-124">Selon les fonctionnalités de votre application, vous devrez peut-être fournir tous les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9e734-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="9e734-125">Compte admin (requis)</span><span class="sxs-lookup"><span data-stu-id="9e734-125">Admin account (required)</span></span>
* <span data-ttu-id="9e734-126">Compte non admin (requis)</span><span class="sxs-lookup"><span data-stu-id="9e734-126">Non-admin account (required)</span></span>
* <span data-ttu-id="9e734-127">Un compte qui n’est pas préconfiguré afin de tester correctement l’expérience de connecte de première série (requise)</span><span class="sxs-lookup"><span data-stu-id="9e734-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="9e734-128">Un compte ayant accès à des fonctionnalités premium ou améliorées (le cas échéant)</span><span class="sxs-lookup"><span data-stu-id="9e734-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="9e734-129">Deux comptes dans le même locataire pour tester l’expérience de collaboration pour les applications qui fonctionnent dans des contextes partagés (le cas échéant)</span><span class="sxs-lookup"><span data-stu-id="9e734-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="9e734-130">Configurations des locataires</span><span class="sxs-lookup"><span data-stu-id="9e734-130">Tenant configurations</span></span>

<span data-ttu-id="9e734-131">Si vous devez configurer un Teams pour utiliser votre application, incluez ces instructions et les comptes d’administration et non admin pour validation.</span><span class="sxs-lookup"><span data-stu-id="9e734-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="9e734-132">Vidéo (facultatif)</span><span class="sxs-lookup"><span data-stu-id="9e734-132">Video (optional)</span></span>

<span data-ttu-id="9e734-133">Fournissez un enregistrement de votre application afin que Microsoft puisse bien comprendre ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="9e734-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="9e734-134">Créez les détails de votre annonce de magasin</span><span class="sxs-lookup"><span data-stu-id="9e734-134">Create your store listing details</span></span>

<span data-ttu-id="9e734-135">Les informations que vous soumettez [à Partner Center](https://partner.microsoft.com)&#8212;y compris votre nom, descriptions, icônes et images&#8212;devient le magasin Teams et microsoft AppSource liste pour votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="9e734-136">Une annonce de magasin peut être la première impression de quelqu’un de votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="9e734-137">Augmentez les installations avec une liste qui transmet efficacement les avantages, les fonctionnalités et la marque de votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="9e734-138">Spécifier un nom court</span><span class="sxs-lookup"><span data-stu-id="9e734-138">Specify a short name</span></span>

<span data-ttu-id="9e734-139">Le nom de votre application (en particulier, son nom [*court) joue*](~/resources/schema/manifest-schema.md#name)un rôle crucial dans la façon dont les utilisateurs la découvrent dans le magasin.</span><span class="sxs-lookup"><span data-stu-id="9e734-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Exemple de capture d’écran met en évidence où le nom court d’une application s’affiche dans une annonce de magasin.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="9e734-141">Assurez-vous que votre nom court respecte les lignes directrices [de validation du magasin.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)</span><span class="sxs-lookup"><span data-stu-id="9e734-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="9e734-142">Rédiger des descriptions</span><span class="sxs-lookup"><span data-stu-id="9e734-142">Write descriptions</span></span>

<span data-ttu-id="9e734-143">Vous devez avoir une description courte et longue de votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="9e734-144">Description brève</span><span class="sxs-lookup"><span data-stu-id="9e734-144">Short description</span></span>

<span data-ttu-id="9e734-145">Un résumé concis de votre application qui doit être original, engageant et dirigé vers votre public cible.</span><span class="sxs-lookup"><span data-stu-id="9e734-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="9e734-146">Gardez la courte description à une phrase.</span><span class="sxs-lookup"><span data-stu-id="9e734-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Exemple de capture d’écran met en évidence où la courte description d’une application s’affiche dans une annonce de magasin.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="9e734-148">Assurez-vous que votre courte description respecte les lignes directrices [de validation du magasin.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)</span><span class="sxs-lookup"><span data-stu-id="9e734-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="9e734-149">Description longue</span><span class="sxs-lookup"><span data-stu-id="9e734-149">Long description</span></span>

<span data-ttu-id="9e734-150">La longue description peut fournir un récit qui met en évidence les principales fonctionnalités de votre application, les problèmes qu’elle résout, et son public cible.</span><span class="sxs-lookup"><span data-stu-id="9e734-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="9e734-151">Bien que cette description puisse aller jusqu’à 4 000 caractères, la plupart des utilisateurs ne liront qu’entre 300 et 500 mots.</span><span class="sxs-lookup"><span data-stu-id="9e734-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Exemple de capture d’écran met en évidence où la longue description d’une application s’affiche dans une liste de magasins.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="9e734-153">Assurez-vous que votre longue description respecte les lignes directrices [de validation du magasin.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)</span><span class="sxs-lookup"><span data-stu-id="9e734-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="9e734-154">Respecter les lignes directrices sur la conception d’icônes</span><span class="sxs-lookup"><span data-stu-id="9e734-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="9e734-155">Les icônes sont l’un des principaux éléments que les utilisateurs voient lors de la navigation dans le magasin.</span><span class="sxs-lookup"><span data-stu-id="9e734-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="9e734-156">Vos icônes doivent communiquer la marque et le but de votre application tout en respectant les Teams exigences.</span><span class="sxs-lookup"><span data-stu-id="9e734-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="9e734-157">Pour plus d’informations, consultez [les conseils sur la création Teams icônes d’applications](~/concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="9e734-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="9e734-158">Capturez des captures d’écran</span><span class="sxs-lookup"><span data-stu-id="9e734-158">Capture screenshots</span></span>

<span data-ttu-id="9e734-159">Les captures d’écran fournissent un aperçu visuel important de votre application pour compléter le nom, l’icône et les descriptions de votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Exemple de capture d’écran met en évidence où les captures d’écran d’application s’affichent dans une liste de magasins.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="9e734-161">Rappelez-vous ce qui suit sur les captures d’écran:</span><span class="sxs-lookup"><span data-stu-id="9e734-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="9e734-162">Vous pouvez avoir jusqu’à cinq captures d’écran par annonce.</span><span class="sxs-lookup"><span data-stu-id="9e734-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="9e734-163">Les types de fichiers pris en charge incluent PNG, JPEG et GIF.</span><span class="sxs-lookup"><span data-stu-id="9e734-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="9e734-164">Les dimensions doivent être de 1366x768 pixels.</span><span class="sxs-lookup"><span data-stu-id="9e734-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="9e734-165">Taille maximale de 1 024 KB.</span><span class="sxs-lookup"><span data-stu-id="9e734-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="9e734-166">Pour les meilleures pratiques, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e734-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="9e734-167">Teams de validation des magasins</span><span class="sxs-lookup"><span data-stu-id="9e734-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [<span data-ttu-id="9e734-168">Créez des images efficaces pour les magasins d’applications Microsoft</span><span class="sxs-lookup"><span data-stu-id="9e734-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="9e734-169">Créer une vidéo</span><span class="sxs-lookup"><span data-stu-id="9e734-169">Create a video</span></span>

<span data-ttu-id="9e734-170">Une vidéo dans votre annonce peut être le moyen le plus efficace de communiquer pourquoi les gens devraient utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="9e734-171">Vous devez répondre aux questions suivantes dans une vidéo :</span><span class="sxs-lookup"><span data-stu-id="9e734-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="9e734-172">Qui est votre application pour?</span><span class="sxs-lookup"><span data-stu-id="9e734-172">Who is your app for?</span></span>
* <span data-ttu-id="9e734-173">Quels problèmes votre application peut-elle résoudre ?</span><span class="sxs-lookup"><span data-stu-id="9e734-173">What problems can your app solve?</span></span>
* <span data-ttu-id="9e734-174">Comment fonctionne votre application ?</span><span class="sxs-lookup"><span data-stu-id="9e734-174">How does your app work?</span></span>
* <span data-ttu-id="9e734-175">Quels autres avantages bénéficiez-vous de l’utilisation de votre application ?</span><span class="sxs-lookup"><span data-stu-id="9e734-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="9e734-176">Meilleures pratiques pour les vidéos</span><span class="sxs-lookup"><span data-stu-id="9e734-176">Best practices for videos</span></span>

* <span data-ttu-id="9e734-177">Gardez votre vidéo entre 30-90 secondes.</span><span class="sxs-lookup"><span data-stu-id="9e734-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="9e734-178">Visez la qualité.</span><span class="sxs-lookup"><span data-stu-id="9e734-178">Aim for quality.</span></span> <span data-ttu-id="9e734-179">Dans une annonce, les utilisateurs verront votre vidéo avant les captures d’écran.</span><span class="sxs-lookup"><span data-stu-id="9e734-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="9e734-180">Sélectionnez une catégorie pour votre application</span><span class="sxs-lookup"><span data-stu-id="9e734-180">Select a category for your app</span></span>

<span data-ttu-id="9e734-181">Lors de la soumission, il vous est demandé de classer votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="9e734-182">Les cartes de tableau suivantes Teams les catégories de magasins aux catégories énumérées dans [Partner Center](https://aka.ms/PartnerCenterHomePage).</span><span class="sxs-lookup"><span data-stu-id="9e734-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="9e734-183">Teams catégories</span><span class="sxs-lookup"><span data-stu-id="9e734-183">Teams categories</span></span>       | <span data-ttu-id="9e734-184">Catégories de centres partenaires</span><span class="sxs-lookup"><span data-stu-id="9e734-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="9e734-185">Analyse et BI</span><span class="sxs-lookup"><span data-stu-id="9e734-185">Analytics and BI</span></span> | <span data-ttu-id="9e734-186">Analyse, visualisation de données et BI</span><span class="sxs-lookup"><span data-stu-id="9e734-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="9e734-187">Développeur et informatique</span><span class="sxs-lookup"><span data-stu-id="9e734-187">Developer and IT</span></span> | <span data-ttu-id="9e734-188">Outils de développeur, administrateur informatique</span><span class="sxs-lookup"><span data-stu-id="9e734-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="9e734-189">Éducation</span><span class="sxs-lookup"><span data-stu-id="9e734-189">Education</span></span> | <span data-ttu-id="9e734-190">Éducation</span><span class="sxs-lookup"><span data-stu-id="9e734-190">Education</span></span> |
| <span data-ttu-id="9e734-191">Ressources humaines</span><span class="sxs-lookup"><span data-stu-id="9e734-191">Human resources</span></span> | <span data-ttu-id="9e734-192">Ressources humaines et recrutement</span><span class="sxs-lookup"><span data-stu-id="9e734-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="9e734-193">Productivité</span><span class="sxs-lookup"><span data-stu-id="9e734-193">Productivity</span></span> | <span data-ttu-id="9e734-194">Gestion de contenu, fichiers et documents, productivité, formation et didacticiels et services publics</span><span class="sxs-lookup"><span data-stu-id="9e734-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="9e734-195">Gestion de projet</span><span class="sxs-lookup"><span data-stu-id="9e734-195">Project management</span></span> | <span data-ttu-id="9e734-196">Communication, Project, Workflow et Gestion d’entreprise</span><span class="sxs-lookup"><span data-stu-id="9e734-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="9e734-197">Ventes et support</span><span class="sxs-lookup"><span data-stu-id="9e734-197">Sales and support</span></span> | <span data-ttu-id="9e734-198">Gestion de la clientèle et des contacts, soutien à la clientèle, gestion financière, ventes et marketing</span><span class="sxs-lookup"><span data-stu-id="9e734-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="9e734-199">Social et amusant</span><span class="sxs-lookup"><span data-stu-id="9e734-199">Social and fun</span></span> | <span data-ttu-id="9e734-200">Galeries d’images et de vidéos, mode de vie, nouvelles et météo, social, voyage et navigation</span><span class="sxs-lookup"><span data-stu-id="9e734-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="9e734-201">Localisez votre annonce de magasin</span><span class="sxs-lookup"><span data-stu-id="9e734-201">Localize your store listing</span></span>

<span data-ttu-id="9e734-202">Partner Center prend en [charge les annonces localisées des magasins](/office/dev/store/prepare-localized-solutions).</span><span class="sxs-lookup"><span data-stu-id="9e734-202">Partner Center supports [localized store listings](/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="9e734-203">Pour plus d’informations, [découvrez comment localiser votre liste d Teams apprisation .](../../../../concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="9e734-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="9e734-204">Vérification complète Publisher’œil</span><span class="sxs-lookup"><span data-stu-id="9e734-204">Complete Publisher Verification</span></span>

<span data-ttu-id="9e734-205">[Publisher vérification est](/azure/active-directory/develop/publisher-verification-overview) nécessaire pour les Teams les applications répertoriées dans le magasin.</span><span class="sxs-lookup"><span data-stu-id="9e734-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.</span></span> <span data-ttu-id="9e734-206">Pour plus d’informations, [consultez les questions fréquemment posées,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)comment marquer votre application comme éditeur [vérifié, et](/azure/active-directory/develop/mark-app-as-publisher-verified)la vérification de [l’éditeur de dépannage](/azure/active-directory/develop/troubleshoot-publisher-verification).</span><span class="sxs-lookup"><span data-stu-id="9e734-206">For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="9e734-207">Attestation Publisher complète</span><span class="sxs-lookup"><span data-stu-id="9e734-207">Complete Publisher Attestation</span></span>

<span data-ttu-id="9e734-208">[Publisher attestation est](/microsoft-365-app-certification/docs/attestation) également nécessaire pour les Teams les applications répertoriées dans le magasin.</span><span class="sxs-lookup"><span data-stu-id="9e734-208">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="9e734-209">Le processus comprend l’auto-évaluation des pratiques de sécurité, de traitement des données et de conformité de votre application qui peuvent aider les clients potentiels à prendre des décisions éclairées concernant l’utilisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="9e734-209">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="9e734-210">Si vous soumettez une nouvelle application, vous ne pouvez pas remplir officiellement l’attestation Publisher tant que votre application n’est pas répertoriée sur le Teams store.</span><span class="sxs-lookup"><span data-stu-id="9e734-210">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="9e734-211">Si vous mettez à jour une application répertoriée, remplissez Publisher attestation avant de soumettre la dernière version de l’application pour validation.</span><span class="sxs-lookup"><span data-stu-id="9e734-211">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="9e734-212">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="9e734-212">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e734-213">Envoyer votre application</span><span class="sxs-lookup"><span data-stu-id="9e734-213">Submit your app</span></span>](/office/dev/store/add-in-submission-guide)
