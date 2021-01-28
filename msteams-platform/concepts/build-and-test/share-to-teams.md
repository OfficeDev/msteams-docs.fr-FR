---
title: Créer un bouton de partage Teams
description: Comment ajouter le bouton Share to Teams incorporé sur votre site web
ms.topic: reference
keywords: Partager Teams entre équipes
ms.openlocfilehash: 46091c957137cc871095ca6a57c0d61fa79d9458
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014333"
---
# <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="0035f-104">Créer un bouton Partager vers Teams sur votre site web</span><span class="sxs-lookup"><span data-stu-id="0035f-104">Create a Share-to-Teams button for your website</span></span>

>[!NOTE]
> * <span data-ttu-id="0035f-105">Seules les versions de bureau de Edge et Chrome sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0035f-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="0035f-106">L’utilisation de freemium ou de comptes invités n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="0035f-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="0035f-107">Les sites web tiers peuvent utiliser le script de lancement pour incorporer des boutons Partager à Teams sur leurs pages web, ce qui lance l’expérience Partager avec Teams dans une fenêtre popup lorsque vous cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="0035f-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="0035f-108">Cela vous permettra de partager un lien directement avec une personne ou un canal Microsoft Teams sans changer de contexte.</span><span class="sxs-lookup"><span data-stu-id="0035f-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![Fenêtre pop-up Partager avec Teams](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="0035f-110">Comment incorporer un bouton Partager avec Teams</span><span class="sxs-lookup"><span data-stu-id="0035f-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="0035f-111">Tout d’abord, vous devez ajouter le `launcher.js` script sur votre page web.</span><span class="sxs-lookup"><span data-stu-id="0035f-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="0035f-112">Ensuite, ajoutez un élément HTML sur votre page web avec l’attribut de classe et le lien `teams-share-button` à partager dans `data-href` l’attribut.</span><span class="sxs-lookup"><span data-stu-id="0035f-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="0035f-113">Cela ajoute l’icône Microsoft Teams à votre site web.</span><span class="sxs-lookup"><span data-stu-id="0035f-113">This will add the Microsoft Teams icon to your website.</span></span>

![Icône Partager avec Teams](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="0035f-115">Si vous le souhaitez, si vous souhaitez une taille d’icône différente pour le bouton Partager avec Teams, utilisez `data-icon-px-size` l’attribut.</span><span class="sxs-lookup"><span data-stu-id="0035f-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="0035f-116">Si vous savez que l’aperçu de l’URL à partir de votre lien à partager ne s’affichera pas bien dans Teams (par exemple, le lien nécessiterait l’authentification de l’utilisateur), vous pouvez désactiver l’aperçu de l’URL en ajoutant le jeu d’attributs à `data-preview` `false` .</span><span class="sxs-lookup"><span data-stu-id="0035f-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="0035f-117">Si votre page restituera dynamiquement le contenu, vous pouvez utiliser la méthode pour forcer le bouton Partager à s’restituer à `shareToMicrosoftTeams.renderButtons()` l’endroit approprié dans le pipeline. </span><span class="sxs-lookup"><span data-stu-id="0035f-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="0035f-118">Création de l’aperçu de votre site web</span><span class="sxs-lookup"><span data-stu-id="0035f-118">Crafting your website preview</span></span>

<span data-ttu-id="0035f-119">Lorsque votre site web est partagé avec Teams, la carte insérée dans le canal sélectionné contient un aperçu de votre site web.</span><span class="sxs-lookup"><span data-stu-id="0035f-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="0035f-120">Vous pouvez contrôler le comportement de cet aperçu en vous assurant que les métadon données appropriées sont ajoutées au site web en cours de partage `data-href` (l’URL).</span><span class="sxs-lookup"><span data-stu-id="0035f-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="0035f-121">Le tableau ci-dessous présente les balises nécessaires.</span><span class="sxs-lookup"><span data-stu-id="0035f-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="0035f-122">Vous pouvez utiliser les versions html par défaut ou la version Open Graph.</span><span class="sxs-lookup"><span data-stu-id="0035f-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="0035f-123">Pour que l’aperçu s’affiche, vous devez :</span><span class="sxs-lookup"><span data-stu-id="0035f-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="0035f-124">Incluez soit une image miniature, soit un titre et une description (pour obtenir de meilleurs résultats, incluez les trois).</span><span class="sxs-lookup"><span data-stu-id="0035f-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="0035f-125">L’URL partagée ne peut pas nécessiter d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0035f-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="0035f-126">Si c’est le cas, vous pouvez toujours le partager, mais l’aperçu ne sera pas créé.</span><span class="sxs-lookup"><span data-stu-id="0035f-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="0035f-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="0035f-127">Value</span></span>|<span data-ttu-id="0035f-128">Balise META</span><span class="sxs-lookup"><span data-stu-id="0035f-128">Meta tag</span></span>| <span data-ttu-id="0035f-129">Open Graph</span><span class="sxs-lookup"><span data-stu-id="0035f-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="0035f-130">Titre</span><span class="sxs-lookup"><span data-stu-id="0035f-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="0035f-131">Description</span><span class="sxs-lookup"><span data-stu-id="0035f-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="0035f-132">Image miniature</span><span class="sxs-lookup"><span data-stu-id="0035f-132">Thumbnail Image</span></span>| <span data-ttu-id="0035f-133">aucune</span><span class="sxs-lookup"><span data-stu-id="0035f-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="0035f-134">Partager avec Teams pour l’Éducation</span><span class="sxs-lookup"><span data-stu-id="0035f-134">Share to Teams for Education</span></span>

<span data-ttu-id="0035f-135">Pour les enseignants qui utilisent le bouton Partager avec Teams, vous avez une option supplémentaire pour `Create an Assignment` .</span><span class="sxs-lookup"><span data-stu-id="0035f-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="0035f-136">Cela vous permet de créer rapidement une affectation dans l’équipe sélectionnée en fonction du lien partagé.</span><span class="sxs-lookup"><span data-stu-id="0035f-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![Fenêtre pop-up Partager avec Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="0035f-138">Définition launcher.js complète</span><span class="sxs-lookup"><span data-stu-id="0035f-138">Full launcher.js definition</span></span>

| <span data-ttu-id="0035f-139">Propriété</span><span class="sxs-lookup"><span data-stu-id="0035f-139">Property</span></span> | <span data-ttu-id="0035f-140">Attribut HTML</span><span class="sxs-lookup"><span data-stu-id="0035f-140">HTML attribute</span></span> | <span data-ttu-id="0035f-141">Type</span><span class="sxs-lookup"><span data-stu-id="0035f-141">Type</span></span> | <span data-ttu-id="0035f-142">Par défaut</span><span class="sxs-lookup"><span data-stu-id="0035f-142">Default</span></span> | <span data-ttu-id="0035f-143">Description</span><span class="sxs-lookup"><span data-stu-id="0035f-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="0035f-144">href</span><span class="sxs-lookup"><span data-stu-id="0035f-144">href</span></span> | `data-href` | <span data-ttu-id="0035f-145">string</span><span class="sxs-lookup"><span data-stu-id="0035f-145">string</span></span> | <span data-ttu-id="0035f-146">s/o</span><span class="sxs-lookup"><span data-stu-id="0035f-146">n/a</span></span> | <span data-ttu-id="0035f-147">Href du contenu à partager.</span><span class="sxs-lookup"><span data-stu-id="0035f-147">The href of the content to share.</span></span> |
| <span data-ttu-id="0035f-148">preview</span><span class="sxs-lookup"><span data-stu-id="0035f-148">preview</span></span> | `data-preview` | <span data-ttu-id="0035f-149">booléen (sous la mesure d’une chaîne)</span><span class="sxs-lookup"><span data-stu-id="0035f-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="0035f-150">Indique si un aperçu du contenu à partager est à afficher ou non.</span><span class="sxs-lookup"><span data-stu-id="0035f-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="0035f-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="0035f-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="0035f-152">number (en tant que chaîne)</span><span class="sxs-lookup"><span data-stu-id="0035f-152">number (as a string)</span></span> | `32` | <span data-ttu-id="0035f-153">Taille en pixels du bouton Partager avec Teams à restituer.</span><span class="sxs-lookup"><span data-stu-id="0035f-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="0035f-154">msgText</span><span class="sxs-lookup"><span data-stu-id="0035f-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="0035f-155">string</span><span class="sxs-lookup"><span data-stu-id="0035f-155">string</span></span> | <span data-ttu-id="0035f-156">s/o</span><span class="sxs-lookup"><span data-stu-id="0035f-156">n/a</span></span> | <span data-ttu-id="0035f-157">Texte par défaut à insérer avant le lien dans la zone de composition du message (limite de 200 caractères)</span><span class="sxs-lookup"><span data-stu-id="0035f-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="0035f-158">assignInstr</span><span class="sxs-lookup"><span data-stu-id="0035f-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="0035f-159">string</span><span class="sxs-lookup"><span data-stu-id="0035f-159">string</span></span> | <span data-ttu-id="0035f-160">s/o</span><span class="sxs-lookup"><span data-stu-id="0035f-160">n/a</span></span> | <span data-ttu-id="0035f-161">Texte par défaut à insérer dans le champ d’affectations « Instructions » (limite de 200 caractères)</span><span class="sxs-lookup"><span data-stu-id="0035f-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="0035f-162">assignTitle</span><span class="sxs-lookup"><span data-stu-id="0035f-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="0035f-163">string</span><span class="sxs-lookup"><span data-stu-id="0035f-163">string</span></span> | <span data-ttu-id="0035f-164">s/o</span><span class="sxs-lookup"><span data-stu-id="0035f-164">n/a</span></span> | <span data-ttu-id="0035f-165">Texte par défaut à insérer dans le champ « Titre » des affectations (limite de 50 caractères)</span><span class="sxs-lookup"><span data-stu-id="0035f-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="0035f-166">Méthodes</span><span class="sxs-lookup"><span data-stu-id="0035f-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="0035f-167">`options` (facultatif) : `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="0035f-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="0035f-168">Restituer tous les boutons de partage actuellement présents sur la page.</span><span class="sxs-lookup"><span data-stu-id="0035f-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="0035f-169">Si un objet facultatif est fourni avec une liste d’éléments, ces éléments sont restituer dans `options` des boutons de partage.</span><span class="sxs-lookup"><span data-stu-id="0035f-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="0035f-170">Définition des valeurs de formulaire par défaut</span><span class="sxs-lookup"><span data-stu-id="0035f-170">Setting default form values</span></span>

<span data-ttu-id="0035f-171">Si vous le souhaitez, vous pouvez choisir de définir des valeurs par défaut pour les champs suivants dans le formulaire Partager avec Teams :</span><span class="sxs-lookup"><span data-stu-id="0035f-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="0035f-172">Dites quelque chose à ce sujet ( `msgText` )</span><span class="sxs-lookup"><span data-stu-id="0035f-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="0035f-173">Instructions d’affectation ( `assignInstr` )</span><span class="sxs-lookup"><span data-stu-id="0035f-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="0035f-174">Titre de l’affectation ( `assignTitle` )</span><span class="sxs-lookup"><span data-stu-id="0035f-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="0035f-175">Exemple : valeurs de formulaire par défaut</span><span class="sxs-lookup"><span data-stu-id="0035f-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
