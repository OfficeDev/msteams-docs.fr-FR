---
title: Créer une liste dans le Store pour votre application
description: Décrit comment créer une description dans le Store pour votre Microsoft Teams application.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 270936ca967c17caaa8a56f85057b20ca3d6a409
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101428"
---
# <a name="create-a-store-listing-for-your-microsoft-teams-app"></a><span data-ttu-id="eacad-103">Créer une liste dans le Store pour votre Microsoft Teams application</span><span class="sxs-lookup"><span data-stu-id="eacad-103">Create a store listing for your Microsoft Teams app</span></span>

<span data-ttu-id="eacad-104">Les informations que [](https://partner.microsoft.com) vous soumettez à l'&#8212;y compris votre nom, descriptions, icônes et images&#8212;deviennent le Microsoft Teams Store et la description Microsoft AppSource de votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-104">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Microsoft Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="eacad-105">Une liste dans le Store peut être la première impression de votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-105">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="eacad-106">Augmentez vos installations avec une liste qui transmet efficacement les avantages, les fonctionnalités et la marque de votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-106">Increase your installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

## <a name="specify-a-short-name"></a><span data-ttu-id="eacad-107">Spécifier un nom court</span><span class="sxs-lookup"><span data-stu-id="eacad-107">Specify a short name</span></span>

<span data-ttu-id="eacad-108">Le nom de votre application (en particulier, son nom [*court)*](~/resources/schema/manifest-schema.md#name)joue un rôle crucial dans la façon dont les utilisateurs la découvrent dans le Store.</span><span class="sxs-lookup"><span data-stu-id="eacad-108">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

<span data-ttu-id="eacad-109">L'exemple suivant montre comment afficher le nom court d'une application dans une liste du Store.</span><span class="sxs-lookup"><span data-stu-id="eacad-109">The following example highlights where an app's short name displays in a store listing.</span></span>

:::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Exemple de capture d'écran sur laquelle le nom court d'une application s'affiche dans une liste du Store.":::

### <a name="best-practices-for-names"></a><span data-ttu-id="eacad-111">Meilleures pratiques en matière de noms</span><span class="sxs-lookup"><span data-stu-id="eacad-111">Best practices for names</span></span>

<span data-ttu-id="eacad-112">**À faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-112">**Do:**</span></span>

* <span data-ttu-id="eacad-113">Choisissez un nom simple et facile à se souvenir qui donne des indications sur ce que fait votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-113">Choose a simple, memorable name that hints at what your app does.</span></span>
* <span data-ttu-id="eacad-114">Soyez distinctif.</span><span class="sxs-lookup"><span data-stu-id="eacad-114">Be distinctive.</span></span>
* <span data-ttu-id="eacad-115">Évitez les fautes de frappe et grammaticales.</span><span class="sxs-lookup"><span data-stu-id="eacad-115">Avoid typos and grammatical errors.</span></span>

<span data-ttu-id="eacad-116">**À ne pas faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-116">**Don't:**</span></span>

* <span data-ttu-id="eacad-117">Utilisez des termes désobligeants ou désobligeants.</span><span class="sxs-lookup"><span data-stu-id="eacad-117">Use profane or derogatory terms.</span></span>
* <span data-ttu-id="eacad-118">Utilisez un langage qui ne fait pas l'différence sur le plan culturel ou sur le plan culturel.</span><span class="sxs-lookup"><span data-stu-id="eacad-118">Use racially or culturally insensitive language.</span></span>
* <span data-ttu-id="eacad-119">Utilisez des termes génériques ou des noms similaires aux applications existantes.</span><span class="sxs-lookup"><span data-stu-id="eacad-119">Use generic terms or names similar to existing apps.</span></span>
* <span data-ttu-id="eacad-120">Incluez « Teams », « Microsoft », les noms de produits Microsoft existants/à venir ou « app » dans le nom.</span><span class="sxs-lookup"><span data-stu-id="eacad-120">Include "Teams", "Microsoft", existing/upcoming Microsoft product names, or  "app" in the name.</span></span>

> [!NOTE]
> <span data-ttu-id="eacad-121">Si votre application fait partie d'un partenariat officiel avec Microsoft, le nom de votre application doit être donné en premier (par exemple, *Connecteur Salesforce pour Microsoft Teams*).</span><span class="sxs-lookup"><span data-stu-id="eacad-121">If your app is part of an official partnership with Microsoft, the name of your app must come first (for example, *Salesforce Connector for Microsoft Teams*).</span></span>

## <a name="write-descriptions"></a><span data-ttu-id="eacad-122">Écrire des descriptions</span><span class="sxs-lookup"><span data-stu-id="eacad-122">Write descriptions</span></span>

<span data-ttu-id="eacad-123">Vous avez besoin d'une description courte et longue de votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-123">You need a short and long description of your app.</span></span>

### <a name="short-description"></a><span data-ttu-id="eacad-124">Description brève</span><span class="sxs-lookup"><span data-stu-id="eacad-124">Short description</span></span>

<span data-ttu-id="eacad-125">Résumé concis de votre application qui doit être original, attrayant et adressé à votre public cible.</span><span class="sxs-lookup"><span data-stu-id="eacad-125">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="eacad-126">Dans l'idéal, conservez la description courte en une phrase.</span><span class="sxs-lookup"><span data-stu-id="eacad-126">Ideally, keep the short description to one sentence.</span></span>

<span data-ttu-id="eacad-127">L'exemple suivant montre comment afficher la description courte d'une application dans une description dans le Store :</span><span class="sxs-lookup"><span data-stu-id="eacad-127">The following example highlights where an app's short description displays in a store listing:</span></span>

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Exemple de capture d'écran sur laquelle la description courte d'une application s'affiche dans une description dans le Store.":::

#### <a name="best-practices-for-short-descriptions"></a><span data-ttu-id="eacad-129">Meilleures pratiques pour les brèves descriptions</span><span class="sxs-lookup"><span data-stu-id="eacad-129">Best practices for short descriptions</span></span>

<span data-ttu-id="eacad-130">**À faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-130">**Do:**</span></span>

* <span data-ttu-id="eacad-131">Mettez les informations les plus importantes en premier.</span><span class="sxs-lookup"><span data-stu-id="eacad-131">Put the most important information first.</span></span>
* <span data-ttu-id="eacad-132">Incluez des mots clés que les clients sont susceptibles de rechercher.</span><span class="sxs-lookup"><span data-stu-id="eacad-132">Include keywords that customers are likely to search for.</span></span>

<span data-ttu-id="eacad-133">**À ne pas faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-133">**Don't:**</span></span>

* <span data-ttu-id="eacad-134">Répétez le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-134">Repeat your app name.</span></span>
* <span data-ttu-id="eacad-135">S'appuyer sur du jargon ou une terminologie spécialisée.</span><span class="sxs-lookup"><span data-stu-id="eacad-135">Rely on jargon or specialized terminology.</span></span> <span data-ttu-id="eacad-136">(Vous ne pouvez pas supposer que les utilisateurs savent quoi rechercher.)</span><span class="sxs-lookup"><span data-stu-id="eacad-136">(You can't assume users know what to look for.)</span></span>

### <a name="long-description"></a><span data-ttu-id="eacad-137">Description longue</span><span class="sxs-lookup"><span data-stu-id="eacad-137">Long description</span></span>

<span data-ttu-id="eacad-138">La description longue peut fournir un narratif attrayant qui met en évidence les principales fonctionnalités de votre application, les problèmes qu'elle résout et son public cible.</span><span class="sxs-lookup"><span data-stu-id="eacad-138">The long description can provide an engaging narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="eacad-139">Bien que cette description puisse prendre jusqu'à 4 000 caractères, la plupart des utilisateurs ne lisent qu'entre 300 et 500 mots.</span><span class="sxs-lookup"><span data-stu-id="eacad-139">While this description can be as long as 4000 characters, most users will only read between 300-500 words.</span></span>

<span data-ttu-id="eacad-140">L'exemple suivant montre comment afficher la description longue d'une application dans une description dans le Store :</span><span class="sxs-lookup"><span data-stu-id="eacad-140">The following example highlights where an app's long description displays in a store listing:</span></span>

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Exemple de capture d'écran sur laquelle la description longue d'une application s'affiche dans une description dans le Store.":::

#### <a name="usage-examples"></a><span data-ttu-id="eacad-142">Exemples d’utilisation</span><span class="sxs-lookup"><span data-stu-id="eacad-142">Usage examples</span></span>

<span data-ttu-id="eacad-143">Les expressions suivantes sont des exemples de ce qui est autorisé lors de l'écriture de descriptions longues :</span><span class="sxs-lookup"><span data-stu-id="eacad-143">The following phrases are examples of what's allowed when writing long descriptions:</span></span>

* <span data-ttu-id="eacad-144">« <*nom de votre* application> fonctionne avec Microsoft Teams »</span><span class="sxs-lookup"><span data-stu-id="eacad-144">"<*Your app name*> works with Microsoft Teams"</span></span>
* <span data-ttu-id="eacad-145">"... un <*type d'application>* pour Microsoft Teams »</span><span class="sxs-lookup"><span data-stu-id="eacad-145">"... a <*type of app*> for Microsoft Teams"</span></span>
* <span data-ttu-id="eacad-146">« <*nom de votre* application> s'intègre à Microsoft Teams »</span><span class="sxs-lookup"><span data-stu-id="eacad-146">"<*Your app name*> integrates with Microsoft Teams"</span></span>
* <span data-ttu-id="eacad-147">"... intégré à Microsoft Teams »</span><span class="sxs-lookup"><span data-stu-id="eacad-147">"... integrated with Microsoft Teams"</span></span>
* <span data-ttu-id="eacad-148">"... pour les utilisateurs qui travaillent avec Microsoft Teams »</span><span class="sxs-lookup"><span data-stu-id="eacad-148">"... for users working with Microsoft Teams"</span></span>
* <span data-ttu-id="eacad-149">"... pour <*tâches spécifiques>* dans Microsoft Teams »</span><span class="sxs-lookup"><span data-stu-id="eacad-149">"... for <*specific task*> within Microsoft Teams"</span></span>
* <span data-ttu-id="eacad-150">"... intégré à ...</span><span class="sxs-lookup"><span data-stu-id="eacad-150">"... built on ..."</span></span>
* <span data-ttu-id="eacad-151">"... s'exécute sur ...</span><span class="sxs-lookup"><span data-stu-id="eacad-151">"... runs on ..."</span></span>
* <span data-ttu-id="eacad-152">"... activé par ...</span><span class="sxs-lookup"><span data-stu-id="eacad-152">"... enabled by ..."</span></span>
* <span data-ttu-id="eacad-153">"... développé pour ...</span><span class="sxs-lookup"><span data-stu-id="eacad-153">"... developed for ..."</span></span>
* <span data-ttu-id="eacad-154">"... conçu pour ...</span><span class="sxs-lookup"><span data-stu-id="eacad-154">"... designed for ..."</span></span>

#### <a name="best-practices-for-long-descriptions"></a><span data-ttu-id="eacad-155">Meilleures pratiques pour les descriptions longues</span><span class="sxs-lookup"><span data-stu-id="eacad-155">Best practices for long descriptions</span></span>

<span data-ttu-id="eacad-156">**À faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-156">**Do:**</span></span>

* <span data-ttu-id="eacad-157">Utilisez [Markdown pour](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) mettre en forme votre description.</span><span class="sxs-lookup"><span data-stu-id="eacad-157">Use [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) to format your description.</span></span>
* <span data-ttu-id="eacad-158">List features with bullet points so it's easier to scan the description.</span><span class="sxs-lookup"><span data-stu-id="eacad-158">List features with bullet points so it's easier to scan the description.</span></span>
* <span data-ttu-id="eacad-159">Utilisez la voix active et parlez directement aux utilisateurs (par exemple, *vous pouvez...*).</span><span class="sxs-lookup"><span data-stu-id="eacad-159">Use active voice and speak to users directly (for example, *You can ...*).</span></span>
* <span data-ttu-id="eacad-160">Inclure un lien d'aide ou de support.</span><span class="sxs-lookup"><span data-stu-id="eacad-160">Include a help or support link.</span></span>
* <span data-ttu-id="eacad-161">Identifiez les informations suivantes le cas échéant : limitations, informations de mise en place, dépendances de compte et mises à jour de publication.</span><span class="sxs-lookup"><span data-stu-id="eacad-161">Identify the following if applicable: limitations, set up information, account dependencies, and release updates.</span></span>

<span data-ttu-id="eacad-162">**À ne pas faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-162">**Don't:**</span></span>

* <span data-ttu-id="eacad-163">Dépassez 500 mots.</span><span class="sxs-lookup"><span data-stu-id="eacad-163">Exceed 500 words.</span></span>
* <span data-ttu-id="eacad-164">Inclure un trop grand nombre de mots clés.</span><span class="sxs-lookup"><span data-stu-id="eacad-164">Include too many keywords.</span></span> <span data-ttu-id="eacad-165">(Il est gênant et n'aidera pas les personnes à trouver votre application.)</span><span class="sxs-lookup"><span data-stu-id="eacad-165">(It's distracting and won't help people find your app.)</span></span>
* <span data-ttu-id="eacad-166">Utilisez la langue suivante, sauf si l'application a suivi un processus de certification officiel :</span><span class="sxs-lookup"><span data-stu-id="eacad-166">Use the following language unless the app has gone through an official certification process:</span></span>
  * <span data-ttu-id="eacad-167">"... certifié pour ...</span><span class="sxs-lookup"><span data-stu-id="eacad-167">"... certified for ..."</span></span>
  * <span data-ttu-id="eacad-168">" ... optimisé par ...</span><span class="sxs-lookup"><span data-stu-id="eacad-168">" ... powered by ..."</span></span>

### <a name="best-practices-for-all-descriptions"></a><span data-ttu-id="eacad-169">Meilleures pratiques pour toutes les descriptions</span><span class="sxs-lookup"><span data-stu-id="eacad-169">Best practices for all descriptions</span></span>

<span data-ttu-id="eacad-170">**À faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-170">**Do:**</span></span>

* <span data-ttu-id="eacad-171">Référencez les noms des produits Microsoft uniquement lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eacad-171">Reference Microsoft product names only when necessary.</span></span> <span data-ttu-id="eacad-172">Pour plus d'informations sur les instructions, voir Les recommandations en matière de marque et [de marque Microsoft.](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)</span><span class="sxs-lookup"><span data-stu-id="eacad-172">For more information on the guidelines, see [Microsoft Trademark and Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).</span></span>
* <span data-ttu-id="eacad-173">Si vous avez besoin de **référencer Teams,** écrivez la première référence en **tant que Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="eacad-173">If you need to reference **Teams**, write the first reference as **Microsoft Teams**.</span></span> <span data-ttu-id="eacad-174">Les références suivantes peuvent être raccourcies **Teams**.</span><span class="sxs-lookup"><span data-stu-id="eacad-174">Subsequent references can be shortened to **Teams**.</span></span>
* <span data-ttu-id="eacad-175">**Reportez-vous Microsoft 365** au lieu de **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="eacad-175">Refer to **Microsoft 365** instead of **Office 365**.</span></span>
* <span data-ttu-id="eacad-176">Évitez les fautes de frappe et grammaticales.</span><span class="sxs-lookup"><span data-stu-id="eacad-176">Avoid typos and grammatical errors.</span></span>
* <span data-ttu-id="eacad-177">Évitez les majuscules inutiles (par exemple, **Utilisateurs** au lieu des **utilisateurs).**</span><span class="sxs-lookup"><span data-stu-id="eacad-177">Avoid unnecessary capitalizations (for example, **Users** instead of **users**).</span></span>
* <span data-ttu-id="eacad-178">Évitez les acronymes.</span><span class="sxs-lookup"><span data-stu-id="eacad-178">Avoid acronyms.</span></span>

<span data-ttu-id="eacad-179">**À ne pas faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-179">**Don't:**</span></span>

* <span data-ttu-id="eacad-180">Abréviation de Microsoft en **tant que MS** ou **MSFT**.</span><span class="sxs-lookup"><span data-stu-id="eacad-180">Abbreviate Microsoft as **MS** or **MSFT**.</span></span>
* <span data-ttu-id="eacad-181">Indiquez que l'application est une offre de Microsoft, y compris à l'aide de balises ou de balises microsoft.</span><span class="sxs-lookup"><span data-stu-id="eacad-181">Indicate the app is an offering from Microsoft, including using Microsoft slogans or taglines.</span></span>
* <span data-ttu-id="eacad-182">Utilisez des noms de marque protégés par des droits d'auteur que vous ne possédez pas.</span><span class="sxs-lookup"><span data-stu-id="eacad-182">Use copyrighted brand names you don't own.</span></span>

## <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="eacad-183">Respecter les instructions de conception des icônes</span><span class="sxs-lookup"><span data-stu-id="eacad-183">Adhere to icon design guidelines</span></span>

<span data-ttu-id="eacad-184">Les icônes sont l'un des principaux éléments que les utilisateurs voient lors de la navigation dans le Store.</span><span class="sxs-lookup"><span data-stu-id="eacad-184">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="eacad-185">Vos icônes doivent communiquer l'objectif de la marque de votre application tout en respectant les Teams requises.</span><span class="sxs-lookup"><span data-stu-id="eacad-185">Your icons should communicate your app's brand purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="eacad-186">Pour plus d'informations, voir [des instructions spécifiques sur la conception d Teams icônes d'application.](~/concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="eacad-186">For more information, see [specific guidance on designing Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="capture-screenshots"></a><span data-ttu-id="eacad-187">Capture d'écran</span><span class="sxs-lookup"><span data-stu-id="eacad-187">Capture screenshots</span></span>

<span data-ttu-id="eacad-188">Les captures d'écran fournissent un aperçu visuel de votre application pour compléter le nom, l'icône et les descriptions de votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-188">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

### <a name="requirements-for-screenshots"></a><span data-ttu-id="eacad-189">Conditions requises pour les captures d'écran</span><span class="sxs-lookup"><span data-stu-id="eacad-189">Requirements for screenshots</span></span>

* <span data-ttu-id="eacad-190">Jusqu'à cinq captures d'écran par liste.</span><span class="sxs-lookup"><span data-stu-id="eacad-190">Up to five screenshots per listing.</span></span>
* <span data-ttu-id="eacad-191">Les types de fichiers pris en charge sont PNG, JPEG et GIF.</span><span class="sxs-lookup"><span data-stu-id="eacad-191">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="eacad-192">Les dimensions doivent être de 1 366 x 768 pixels.</span><span class="sxs-lookup"><span data-stu-id="eacad-192">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="eacad-193">Taille maximale de 1 024 Ko.</span><span class="sxs-lookup"><span data-stu-id="eacad-193">Maximum size of 1,024 KB.</span></span>

### <a name="best-practices-for-screenshots"></a><span data-ttu-id="eacad-194">Meilleures pratiques pour les captures d'écran</span><span class="sxs-lookup"><span data-stu-id="eacad-194">Best practices for screenshots</span></span>

<span data-ttu-id="eacad-195">**À faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-195">**Do:**</span></span>

* <span data-ttu-id="eacad-196">Concentrez-vous sur les fonctionnalités de votre application (par exemple, comment les personnes peuvent communiquer avec votre bot).</span><span class="sxs-lookup"><span data-stu-id="eacad-196">Focus on your app's capabilities (for example, how people can communicate with your bot).</span></span>
* <span data-ttu-id="eacad-197">Incluez du contenu qui représente précisément votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-197">Include content that accurately represents your app.</span></span>
* <span data-ttu-id="eacad-198">Utilisez du texte judicieusement.</span><span class="sxs-lookup"><span data-stu-id="eacad-198">Use text judiciously.</span></span>
* Captures d'écran avec une couleur qui reflète votre marque et inclut du contenu marketing, similaire à l'exemple [Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) suivant (les exigences de dimension s'appliquent à l'image entière et pas seulement à la capture d'écran) : capture d'écran de l'exemple d'application tierce   :::image type="content" source="../../../../assets/images/freshdesk.png" alt-text="Freshdesk":::

<span data-ttu-id="eacad-200">**À ne pas faire :**</span><span class="sxs-lookup"><span data-stu-id="eacad-200">**Don't:**</span></span>

* <span data-ttu-id="eacad-201">Afficher des appareils spécifiques, tels que des téléphones ou des ordinateurs portables.</span><span class="sxs-lookup"><span data-stu-id="eacad-201">Show specific devices, such as phones or laptops.</span></span>
* <span data-ttu-id="eacad-202">Afficher le chrome ou l'interface utilisateur qui n'est pas dans votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-202">Display chrome or UI that isn't in your app.</span></span>
* <span data-ttu-id="eacad-203">Capturez les Teams ou l'interface utilisateur du navigateur dans vos captures d'écran.</span><span class="sxs-lookup"><span data-stu-id="eacad-203">Capture any Teams or browser UI in your screenshots.</span></span>
* <span data-ttu-id="eacad-204">Incluez des maquettes qui reflètent de manière incorrecte l'interface utilisateur réelle de votre application, comme l'affichage de votre application dans un navigateur au lieu d'un Teams onglet.</span><span class="sxs-lookup"><span data-stu-id="eacad-204">Include mockups that inaccurately reflect your app's actual UI, such as showing your app in  a browser instead of a Teams tab.</span></span>

<span data-ttu-id="eacad-205">Pour plus d'informations sur les meilleures pratiques, voir [créer des images efficaces pour les magasins d'applications Microsoft.](/office/dev/store/craft-effective-appsource-store-images)</span><span class="sxs-lookup"><span data-stu-id="eacad-205">For more best practices, see [craft effective images for Microsoft app stores](/office/dev/store/craft-effective-appsource-store-images).</span></span>

## <a name="create-a-video"></a><span data-ttu-id="eacad-206">Créer une vidéo</span><span class="sxs-lookup"><span data-stu-id="eacad-206">Create a video</span></span>

<span data-ttu-id="eacad-207">Une vidéo peut être le moyen le plus efficace de communiquer pourquoi les personnes doivent utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="eacad-207">A video can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="eacad-208">Vous devez répondre aux questions suivantes dans une vidéo :</span><span class="sxs-lookup"><span data-stu-id="eacad-208">You should address the following questions in a video:</span></span>

* <span data-ttu-id="eacad-209">Qui votre application est-elle pour ?</span><span class="sxs-lookup"><span data-stu-id="eacad-209">Who is your app for?</span></span>
* <span data-ttu-id="eacad-210">Quels problèmes votre application peut-elle résoudre ?</span><span class="sxs-lookup"><span data-stu-id="eacad-210">What problems can your app solve?</span></span>
* <span data-ttu-id="eacad-211">Comment fonctionne votre application ?</span><span class="sxs-lookup"><span data-stu-id="eacad-211">How does your app work?</span></span>
* <span data-ttu-id="eacad-212">Quels autres avantages bénéficiez-vous de l'utilisation de votre application ?</span><span class="sxs-lookup"><span data-stu-id="eacad-212">What other benefits do you get from using your app?</span></span>

<span data-ttu-id="eacad-213">Si vous incluez une vidéo, elle apparaît avant vos captures d'écran dans la liste.</span><span class="sxs-lookup"><span data-stu-id="eacad-213">If you include a video, it appears before your screenshots in the listing.</span></span>

### <a name="best-practices-for-videos"></a><span data-ttu-id="eacad-214">Meilleures pratiques pour les vidéos</span><span class="sxs-lookup"><span data-stu-id="eacad-214">Best practices for videos</span></span>

* <span data-ttu-id="eacad-215">Conservez votre vidéo entre 30 et 90 secondes.</span><span class="sxs-lookup"><span data-stu-id="eacad-215">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="eacad-216">Visez la qualité.</span><span class="sxs-lookup"><span data-stu-id="eacad-216">Aim for quality.</span></span> <span data-ttu-id="eacad-217">Dans une liste, les utilisateurs voient votre vidéo avant les captures d'écran.</span><span class="sxs-lookup"><span data-stu-id="eacad-217">In a listing, users will see your video before screenshots.</span></span>

## <a name="localize-your-store-listing"></a><span data-ttu-id="eacad-218">Localisez votre liste dans le Store</span><span class="sxs-lookup"><span data-stu-id="eacad-218">Localize your store listing</span></span>

<span data-ttu-id="eacad-219">L'Partner Center prend [en charge les listes de magasins localisées.](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)</span><span class="sxs-lookup"><span data-stu-id="eacad-219">Partner Center supports [localized store listings](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="eacad-220">Pour plus d'informations, voir comment localiser votre [liste Teams'application.](../../../../concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="eacad-220">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="eacad-221">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="eacad-221">See also</span></span>

* [<span data-ttu-id="eacad-222">Créer des listes Microsoft 365 magasins efficaces</span><span class="sxs-lookup"><span data-stu-id="eacad-222">Create effective Microsoft 365 Stores listings</span></span>](/office/dev/store/create-effective-office-store-listings)
* <span data-ttu-id="eacad-223">Teams de conception d'application pour [la copie, le contenu et](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content) l'expression de [marque](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)</span><span class="sxs-lookup"><span data-stu-id="eacad-223">Teams app design guidelines for [copy and content](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content) and [brand expression](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)</span></span>
* [<span data-ttu-id="eacad-224">Recommandations en matière de marque et de marque Microsoft</span><span class="sxs-lookup"><span data-stu-id="eacad-224">Microsoft Trademark and Brand Guidelines</span></span>](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)

## <a name="next-step"></a><span data-ttu-id="eacad-225">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="eacad-225">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eacad-226">Préparer votre soumission au Store</span><span class="sxs-lookup"><span data-stu-id="eacad-226">Prepare your store submission</span></span>](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
