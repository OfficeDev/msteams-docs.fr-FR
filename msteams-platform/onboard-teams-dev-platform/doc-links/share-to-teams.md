---
title: Ajout d’un bouton partager à teams à votre site Web
description: Comment ajouter le bouton partager à teams incorporé sur votre site Web
keywords: Partager des équipes partager partage-équipe
ms.openlocfilehash: 0ebd47af068bf523f27c19241b85d2137af3ada6
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651955"
---
# <a name="adding-a-share-to-teams-button-to-your-website"></a><span data-ttu-id="a106d-104">Ajout d’un bouton partager à teams à votre site Web</span><span class="sxs-lookup"><span data-stu-id="a106d-104">Adding a Share to Teams button to your website</span></span>

>[!NOTE]
> * <span data-ttu-id="a106d-105">Seules les versions de bureau Edge et chrome sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="a106d-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="a106d-106">L’utilisation de comptes freemium ou invités n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="a106d-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="a106d-107">Les sites Web tiers peuvent utiliser le script de lancement pour incorporer les boutons partager à teams sur leurs pages Web, ce qui lancera l’expérience de partage vers teams dans une fenêtre contextuelle lorsque vous cliquerez dessus.</span><span class="sxs-lookup"><span data-stu-id="a106d-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="a106d-108">Cela vous permettra de partager un lien directement avec une personne ou un canal Microsoft teams sans basculer le contexte.</span><span class="sxs-lookup"><span data-stu-id="a106d-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![Partager le menu contextuel teams](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="a106d-110">Comment incorporer un bouton partager à teams</span><span class="sxs-lookup"><span data-stu-id="a106d-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="a106d-111">Tout d’abord, vous devez ajouter le `launcher.js` script sur votre page Web.</span><span class="sxs-lookup"><span data-stu-id="a106d-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="a106d-112">Ensuite, ajoutez un élément HTML sur votre page Web avec l' `teams-share-button` attribut Class et le lien à partager dans l' `data-href` attribut.</span><span class="sxs-lookup"><span data-stu-id="a106d-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="a106d-113">Cette opération ajoute l’icône Microsoft teams à votre site Web.</span><span class="sxs-lookup"><span data-stu-id="a106d-113">This will add the Microsoft Teams icon to your website.</span></span>

![Icône partager avec teams](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="a106d-115">Éventuellement, si vous voulez une taille d’icône différente pour le bouton partager avec Teams, utilisez l' `data-icon-px-size` attribut.</span><span class="sxs-lookup"><span data-stu-id="a106d-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="a106d-116">Si vous êtes certain que l’aperçu de l’URL de votre lien à partager ne s’affiche pas correctement dans Teams (par exemple, le lien nécessite l’authentification de l’utilisateur), vous pouvez désactiver l’aperçu de l’URL en ajoutant l' `data-preview` attribut défini à `false` .</span><span class="sxs-lookup"><span data-stu-id="a106d-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="a106d-117">Si votre page affiche le contenu de manière dynamique, vous pouvez utiliser la `shareToMicrosoftTeams.renderButtons()` méthode pour forcer le rendu du bouton **partager** à l’emplacement approprié dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="a106d-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="a106d-118">Conception de l’aperçu de votre site Web</span><span class="sxs-lookup"><span data-stu-id="a106d-118">Crafting your website preview</span></span>

<span data-ttu-id="a106d-119">Lorsque votre site Web est partagé avec Teams, la carte insérée dans la chaîne sélectionnée contiendra un aperçu de votre site Web.</span><span class="sxs-lookup"><span data-stu-id="a106d-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="a106d-120">Vous pouvez contrôler le comportement de cet aperçu en veillant à ce que les méta-données appropriées soient ajoutées au site Web partagé ( `data-href` URL).</span><span class="sxs-lookup"><span data-stu-id="a106d-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="a106d-121">Le tableau suivant présente les balises nécessaires.</span><span class="sxs-lookup"><span data-stu-id="a106d-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="a106d-122">Vous pouvez utiliser les versions par défaut de HTML ou la version d’Open Graph.</span><span class="sxs-lookup"><span data-stu-id="a106d-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="a106d-123">Pour afficher l’aperçu, vous devez :</span><span class="sxs-lookup"><span data-stu-id="a106d-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="a106d-124">Inclure une image miniature, ou les deux, un titre et une description (pour de meilleurs résultats, incluez les trois).</span><span class="sxs-lookup"><span data-stu-id="a106d-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="a106d-125">L’URL partagée ne peut pas exiger l’authentification.</span><span class="sxs-lookup"><span data-stu-id="a106d-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="a106d-126">Si c’est le cas, vous pouvez toujours le partager, mais l’aperçu n’est pas créé.</span><span class="sxs-lookup"><span data-stu-id="a106d-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="a106d-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="a106d-127">Value</span></span>|<span data-ttu-id="a106d-128">Balise META</span><span class="sxs-lookup"><span data-stu-id="a106d-128">Meta tag</span></span>| <span data-ttu-id="a106d-129">Ouvrir un graphique</span><span class="sxs-lookup"><span data-stu-id="a106d-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="a106d-130">Titre</span><span class="sxs-lookup"><span data-stu-id="a106d-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="a106d-131">Description</span><span class="sxs-lookup"><span data-stu-id="a106d-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="a106d-132">Image miniature</span><span class="sxs-lookup"><span data-stu-id="a106d-132">Thumbnail Image</span></span>| <span data-ttu-id="a106d-133">aucune</span><span class="sxs-lookup"><span data-stu-id="a106d-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="a106d-134">Partager avec teams pour l’éducation</span><span class="sxs-lookup"><span data-stu-id="a106d-134">Share to Teams for Education</span></span>

<span data-ttu-id="a106d-135">Pour les enseignants qui utilisent le bouton partager avec Teams, une option supplémentaire est proposée `Create an Assignment` .</span><span class="sxs-lookup"><span data-stu-id="a106d-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="a106d-136">Cela vous permet de créer rapidement une affectation dans l’équipe choisie en fonction du lien partagé.</span><span class="sxs-lookup"><span data-stu-id="a106d-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![Partager le menu contextuel teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="a106d-138">Définition de launcher.js complète</span><span class="sxs-lookup"><span data-stu-id="a106d-138">Full launcher.js definition</span></span>

| <span data-ttu-id="a106d-139">Propriété</span><span class="sxs-lookup"><span data-stu-id="a106d-139">Property</span></span> | <span data-ttu-id="a106d-140">Attribut HTML</span><span class="sxs-lookup"><span data-stu-id="a106d-140">HTML attribute</span></span> | <span data-ttu-id="a106d-141">Type</span><span class="sxs-lookup"><span data-stu-id="a106d-141">Type</span></span> | <span data-ttu-id="a106d-142">Par défaut</span><span class="sxs-lookup"><span data-stu-id="a106d-142">Default</span></span> | <span data-ttu-id="a106d-143">Description</span><span class="sxs-lookup"><span data-stu-id="a106d-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="a106d-144">href</span><span class="sxs-lookup"><span data-stu-id="a106d-144">href</span></span> | `data-href` | <span data-ttu-id="a106d-145">string</span><span class="sxs-lookup"><span data-stu-id="a106d-145">string</span></span> | <span data-ttu-id="a106d-146">s/o</span><span class="sxs-lookup"><span data-stu-id="a106d-146">n/a</span></span> | <span data-ttu-id="a106d-147">Href du contenu à partager.</span><span class="sxs-lookup"><span data-stu-id="a106d-147">The href of the content to share.</span></span> |
| <span data-ttu-id="a106d-148">preview</span><span class="sxs-lookup"><span data-stu-id="a106d-148">preview</span></span> | `data-preview` | <span data-ttu-id="a106d-149">Boolean (sous forme de chaîne)</span><span class="sxs-lookup"><span data-stu-id="a106d-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="a106d-150">Indique si un aperçu du contenu à partager doit être affiché ou non.</span><span class="sxs-lookup"><span data-stu-id="a106d-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="a106d-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="a106d-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="a106d-152">nombre (sous forme de chaîne)</span><span class="sxs-lookup"><span data-stu-id="a106d-152">number (as a string)</span></span> | `32` | <span data-ttu-id="a106d-153">Taille en pixels du bouton partager-à-teams à afficher.</span><span class="sxs-lookup"><span data-stu-id="a106d-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="a106d-154">msgText</span><span class="sxs-lookup"><span data-stu-id="a106d-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="a106d-155">string</span><span class="sxs-lookup"><span data-stu-id="a106d-155">string</span></span> | <span data-ttu-id="a106d-156">s/o</span><span class="sxs-lookup"><span data-stu-id="a106d-156">n/a</span></span> | <span data-ttu-id="a106d-157">Texte par défaut à insérer avant le lien dans la zone de composition du message (200 caractères maximum)</span><span class="sxs-lookup"><span data-stu-id="a106d-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="a106d-158">assignInstr</span><span class="sxs-lookup"><span data-stu-id="a106d-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="a106d-159">string</span><span class="sxs-lookup"><span data-stu-id="a106d-159">string</span></span> | <span data-ttu-id="a106d-160">s/o</span><span class="sxs-lookup"><span data-stu-id="a106d-160">n/a</span></span> | <span data-ttu-id="a106d-161">Texte par défaut à insérer dans le champ « instructions » des affectations (200 caractères maximum)</span><span class="sxs-lookup"><span data-stu-id="a106d-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="a106d-162">assignTitle</span><span class="sxs-lookup"><span data-stu-id="a106d-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="a106d-163">string</span><span class="sxs-lookup"><span data-stu-id="a106d-163">string</span></span> | <span data-ttu-id="a106d-164">s/o</span><span class="sxs-lookup"><span data-stu-id="a106d-164">n/a</span></span> | <span data-ttu-id="a106d-165">Texte par défaut à insérer dans le champ affectations « title » (50 caractères maximum)</span><span class="sxs-lookup"><span data-stu-id="a106d-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="a106d-166">Méthodes</span><span class="sxs-lookup"><span data-stu-id="a106d-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="a106d-167">`options` (facultatif) : `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="a106d-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="a106d-168">Affiche tous les boutons de partage actuellement sur la page.</span><span class="sxs-lookup"><span data-stu-id="a106d-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="a106d-169">Si un `options` objet facultatif est fourni avec une liste d’éléments, ces éléments seront rendus dans les boutons de partage.</span><span class="sxs-lookup"><span data-stu-id="a106d-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="a106d-170">Définition des valeurs de formulaire par défaut</span><span class="sxs-lookup"><span data-stu-id="a106d-170">Setting default form values</span></span>

<span data-ttu-id="a106d-171">Vous pouvez également définir des valeurs par défaut pour les champs suivants dans le formulaire partager avec teams :</span><span class="sxs-lookup"><span data-stu-id="a106d-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="a106d-172">Signification de ce ( `msgText` )</span><span class="sxs-lookup"><span data-stu-id="a106d-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="a106d-173">Instructions d’affectation ( `assignInstr` )</span><span class="sxs-lookup"><span data-stu-id="a106d-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="a106d-174">Titre de l’affectation ( `assignTitle` )</span><span class="sxs-lookup"><span data-stu-id="a106d-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="a106d-175">Exemple : valeurs de formulaire par défaut</span><span class="sxs-lookup"><span data-stu-id="a106d-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
