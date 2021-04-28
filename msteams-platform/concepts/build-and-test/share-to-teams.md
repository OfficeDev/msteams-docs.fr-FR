---
title: Bouton Créer un partage avec Teams
description: Comment ajouter le bouton Share to Teams incorporé sur votre site web
ms.topic: reference
localization_priority: Normal
keywords: Partager Teams entre équipes
ms.openlocfilehash: c8bbb371e2d68bf063c3aa5e02c7cf3ec911c0b8
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058473"
---
# <a name="create-share-to-teams-button"></a><span data-ttu-id="1eb6b-104">Bouton Créer un partage avec Teams</span><span class="sxs-lookup"><span data-stu-id="1eb6b-104">Create Share-to-Teams button</span></span>

<span data-ttu-id="1eb6b-105">Les sites web tiers peuvent utiliser le script de lancement pour incorporer des boutons Share-to-Teams sur leurs pages web.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-105">Third-party websites can use the launcher script to embed Share-to-Teams buttons on their webpages.</span></span> <span data-ttu-id="1eb6b-106">Lorsque vous sélectionnez, l'expérience Partager avec Teams s'ouvre dans une fenêtre fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-106">When you select, it launches the Share-to-Teams experience in a pop-up window.</span></span> <span data-ttu-id="1eb6b-107">Cela vous permet de partager un lien directement avec une personne ou un canal Microsoft Teams sans changer de contexte.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-107">This allows you to share a link directly to any person or Microsoft Teams channel without switching the context.</span></span> <span data-ttu-id="1eb6b-108">Ce document vous guide sur la création et l'incorporation d'un bouton Share-to-Teams pour votre site web, la création de l'aperçu de votre site web et l'extension de Share-to-Teams pour l'Éducation.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-108">This document guides you on how to create, and embed a Share-to-Teams button for your website, craft your website preview, and extend Share-to-Teams for Education.</span></span>

> [!NOTE]
> * <span data-ttu-id="1eb6b-109">Seules les versions de bureau de Edge et Chrome sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-109">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="1eb6b-110">L'utilisation de freemium ou de comptes invités n'est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-110">Use of Freemium or guest accounts is not supported.</span></span>  

<span data-ttu-id="1eb6b-111">L'image suivante affiche l'expérience de partage à teams :</span><span class="sxs-lookup"><span data-stu-id="1eb6b-111">The following image displays the Share-to-Teams pop-up experience:</span></span>

![Fenêtre popup Share-to-Teams](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a><span data-ttu-id="1eb6b-113">Incorporer un bouton Partager dans Teams</span><span class="sxs-lookup"><span data-stu-id="1eb6b-113">Embed a Share to Teams button</span></span>

1. <span data-ttu-id="1eb6b-114">Ajoutez `launcher.js` le script sur votre page web.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-114">Add the `launcher.js` script on your webpage.</span></span>

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. <span data-ttu-id="1eb6b-115">Ajoutez un élément HTML sur votre page web avec l'attribut de classe et `teams-share-button` le lien à partager dans l'attribut. `data-href`</span><span class="sxs-lookup"><span data-stu-id="1eb6b-115">Add a HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    <span data-ttu-id="1eb6b-116">Une fois que vous avez terminé, l'icône Microsoft Teams est ajoutée à votre site web.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-116">After completing this, the Microsoft Teams icon gets added to your website.</span></span> <span data-ttu-id="1eb6b-117">L'image suivante montre l'icône Partager avec Teams :</span><span class="sxs-lookup"><span data-stu-id="1eb6b-117">The following image shows Share-to-Teams icon:</span></span>

    ![Icône Partager avec Teams](~/assets/icons/share-to-teams-icon.png)

1. <span data-ttu-id="1eb6b-119">Sinon, si vous souhaitez une taille d'icône différente pour le bouton Partager avec Teams, utilisez `data-icon-px-size` l'attribut.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-119">Alternatively, if you want a different icon size for the Share-to Teams button, use the `data-icon-px-size` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. <span data-ttu-id="1eb6b-120">Si le lien partagé nécessite une authentification utilisateur et que l'aperçu de l'URL de votre lien à partager n'est pas bien restituer dans Teams, vous pouvez désactiver l'aperçu de l'URL en ajoutant le jeu d'attributs `data-preview` à `false` .</span><span class="sxs-lookup"><span data-stu-id="1eb6b-120">If the shared link requires user authentication, and the URL preview from your link to be shared does not render well in Teams then, you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. <span data-ttu-id="1eb6b-121">Si votre page restituera dynamiquement le contenu, vous pouvez utiliser la méthode pour forcer le bouton Partager à s'restituer à `shareToMicrosoftTeams.renderButtons()` l'endroit approprié dans le pipeline. </span><span class="sxs-lookup"><span data-stu-id="1eb6b-121">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="craft-your-website-preview"></a><span data-ttu-id="1eb6b-122">Création de la prévisualisation de votre site web</span><span class="sxs-lookup"><span data-stu-id="1eb6b-122">Craft your website preview</span></span>

<span data-ttu-id="1eb6b-123">Lorsque votre site web est partagé avec Teams, la carte insérée dans le canal sélectionné contient un aperçu de votre site web.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-123">When your website is shared to Teams, the card that is inserted into the selected channel contains a preview of your website.</span></span> <span data-ttu-id="1eb6b-124">Vous pouvez contrôler le comportement de cet aperçu en vous assurant que les métadon données appropriées sont ajoutées au site web en cours de partage, telles que `data-href` l'URL.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-124">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared, such as the `data-href` URL.</span></span>  

<span data-ttu-id="1eb6b-125">**Pour afficher l'aperçu**</span><span class="sxs-lookup"><span data-stu-id="1eb6b-125">**To display the preview**</span></span>

* <span data-ttu-id="1eb6b-126">Vous devez inclure soit une **image miniature,** soit un **titre** et une **description.**</span><span class="sxs-lookup"><span data-stu-id="1eb6b-126">You must include either a **Thumbnail image**, or both a **Title** and **Description**.</span></span> <span data-ttu-id="1eb6b-127">Pour obtenir de meilleurs résultats, incluez les trois.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-127">For best results, include all three.</span></span>
* <span data-ttu-id="1eb6b-128">L'URL partagée ne nécessite pas d'authentification.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-128">The shared URL does not require authentication.</span></span> <span data-ttu-id="1eb6b-129">Si elle nécessite une authentification, vous pouvez la partager, mais l'aperçu n'est pas créé.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-129">If it requires authentication, you can share it, but the preview is not created.</span></span>

<span data-ttu-id="1eb6b-130">Le tableau suivant présente les balises nécessaires :</span><span class="sxs-lookup"><span data-stu-id="1eb6b-130">The following table outlines the necessary tags:</span></span>

|<span data-ttu-id="1eb6b-131">Valeur</span><span class="sxs-lookup"><span data-stu-id="1eb6b-131">Value</span></span>|<span data-ttu-id="1eb6b-132">Balise META</span><span class="sxs-lookup"><span data-stu-id="1eb6b-132">Meta tag</span></span>| <span data-ttu-id="1eb6b-133">Open Graph</span><span class="sxs-lookup"><span data-stu-id="1eb6b-133">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="1eb6b-134">Titre</span><span class="sxs-lookup"><span data-stu-id="1eb6b-134">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="1eb6b-135">Description</span><span class="sxs-lookup"><span data-stu-id="1eb6b-135">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="1eb6b-136">Image miniature</span><span class="sxs-lookup"><span data-stu-id="1eb6b-136">Thumbnail Image</span></span>| <span data-ttu-id="1eb6b-137">aucun.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-137">none.</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

<span data-ttu-id="1eb6b-138">Vous pouvez utiliser les versions html par défaut ou la version Open Graph.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-138">You can use either the html default versions, or the Open Graph version.</span></span>

## <a name="share-to-teams-for-education"></a><span data-ttu-id="1eb6b-139">Partager avec Teams pour l'Éducation</span><span class="sxs-lookup"><span data-stu-id="1eb6b-139">Share to Teams for Education</span></span>

<span data-ttu-id="1eb6b-140">Pour les enseignants qui utilisent le bouton Partager avec Teams, il existe une option supplémentaire pour `Create an Assignment` .</span><span class="sxs-lookup"><span data-stu-id="1eb6b-140">For teachers using the Share to Teams button, there is an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="1eb6b-141">Cela vous permet de créer rapidement une affectation dans l'équipe sélectionnée, en fonction du lien partagé.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-141">This enables you to quickly create an assignment in the chosen Team, based on the shared link.</span></span> <span data-ttu-id="1eb6b-142">L'image suivante affiche Share-to-Teams pour l'éducation :</span><span class="sxs-lookup"><span data-stu-id="1eb6b-142">The following image displays Share-to-Teams for education:</span></span> 

![Partager avec l'éducation popup Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="1eb6b-144">Définition launcher.js complète</span><span class="sxs-lookup"><span data-stu-id="1eb6b-144">Full launcher.js definition</span></span>

| <span data-ttu-id="1eb6b-145">Propriété</span><span class="sxs-lookup"><span data-stu-id="1eb6b-145">Property</span></span> | <span data-ttu-id="1eb6b-146">Attribut HTML</span><span class="sxs-lookup"><span data-stu-id="1eb6b-146">HTML attribute</span></span> | <span data-ttu-id="1eb6b-147">Type</span><span class="sxs-lookup"><span data-stu-id="1eb6b-147">Type</span></span> | <span data-ttu-id="1eb6b-148">Par défaut</span><span class="sxs-lookup"><span data-stu-id="1eb6b-148">Default</span></span> | <span data-ttu-id="1eb6b-149">Description</span><span class="sxs-lookup"><span data-stu-id="1eb6b-149">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="1eb6b-150">href</span><span class="sxs-lookup"><span data-stu-id="1eb6b-150">href</span></span> | `data-href` | <span data-ttu-id="1eb6b-151">string</span><span class="sxs-lookup"><span data-stu-id="1eb6b-151">string</span></span> | <span data-ttu-id="1eb6b-152">s/o</span><span class="sxs-lookup"><span data-stu-id="1eb6b-152">n/a</span></span> | <span data-ttu-id="1eb6b-153">Href du contenu à partager.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-153">The href of the content to share.</span></span> |
| <span data-ttu-id="1eb6b-154">preview</span><span class="sxs-lookup"><span data-stu-id="1eb6b-154">preview</span></span> | `data-preview` | <span data-ttu-id="1eb6b-155">booléen (sous la mesure d'une chaîne)</span><span class="sxs-lookup"><span data-stu-id="1eb6b-155">boolean (as a string)</span></span> | `true` | <span data-ttu-id="1eb6b-156">Indique si un aperçu du contenu à partager doit être présenté ou non.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-156">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="1eb6b-157">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="1eb6b-157">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="1eb6b-158">number (en tant que chaîne)</span><span class="sxs-lookup"><span data-stu-id="1eb6b-158">number (as a string)</span></span> | `32` | <span data-ttu-id="1eb6b-159">Taille en pixels du bouton Partager avec Teams à restituer.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-159">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="1eb6b-160">msgText</span><span class="sxs-lookup"><span data-stu-id="1eb6b-160">msgText</span></span> | `data-msg-text` | <span data-ttu-id="1eb6b-161">string</span><span class="sxs-lookup"><span data-stu-id="1eb6b-161">string</span></span> | <span data-ttu-id="1eb6b-162">s/o</span><span class="sxs-lookup"><span data-stu-id="1eb6b-162">n/a</span></span> | <span data-ttu-id="1eb6b-163">Texte par défaut à insérer avant le lien dans la zone de composition du message.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-163">Default Text to be inserted before the link in the message compose box.</span></span> <span data-ttu-id="1eb6b-164">Le nombre maximal de caractères est de 200.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-164">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="1eb6b-165">assignInstr</span><span class="sxs-lookup"><span data-stu-id="1eb6b-165">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="1eb6b-166">string</span><span class="sxs-lookup"><span data-stu-id="1eb6b-166">string</span></span> | <span data-ttu-id="1eb6b-167">s/o</span><span class="sxs-lookup"><span data-stu-id="1eb6b-167">n/a</span></span> | <span data-ttu-id="1eb6b-168">Texte par défaut à insérer dans le champ « Instructions » des affectations.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-168">Default Text to be inserted in the assignments "Instructions" field.</span></span> <span data-ttu-id="1eb6b-169">Le nombre maximal de caractères est de 200.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-169">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="1eb6b-170">assignTitle</span><span class="sxs-lookup"><span data-stu-id="1eb6b-170">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="1eb6b-171">string</span><span class="sxs-lookup"><span data-stu-id="1eb6b-171">string</span></span> | <span data-ttu-id="1eb6b-172">s/o</span><span class="sxs-lookup"><span data-stu-id="1eb6b-172">n/a</span></span> | <span data-ttu-id="1eb6b-173">Texte par défaut à insérer dans le champ « Titre » des affectations.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-173">Default Text to be inserted in the assignments "Title" field.</span></span> <span data-ttu-id="1eb6b-174">Le nombre maximal de caractères est de 50.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-174">Maximum number of characters is 50.</span></span> |

### <a name="methods"></a><span data-ttu-id="1eb6b-175">Méthodes</span><span class="sxs-lookup"><span data-stu-id="1eb6b-175">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="1eb6b-176">`options` (facultatif) : `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="1eb6b-176">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="1eb6b-177">Actuellement, tous les boutons de partage sont restituer sur la page.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-177">Currently, all share buttons are rendered on the page.</span></span> <span data-ttu-id="1eb6b-178">Si un objet facultatif est fourni avec une liste d'éléments, ces éléments sont restituer dans `options` des boutons de partage.</span><span class="sxs-lookup"><span data-stu-id="1eb6b-178">If an optional `options` object is supplied with a list of elements, those elements are rendered into share buttons.</span></span>

### <a name="set-default-form-values"></a><span data-ttu-id="1eb6b-179">Définir les valeurs de formulaire par défaut</span><span class="sxs-lookup"><span data-stu-id="1eb6b-179">Set default form values</span></span>

<span data-ttu-id="1eb6b-180">Vous pouvez choisir de définir des valeurs par défaut pour les champs suivants dans le formulaire Partager avec Teams :</span><span class="sxs-lookup"><span data-stu-id="1eb6b-180">You can select to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="1eb6b-181">Dites quelque chose à ce sujet : `msgText`</span><span class="sxs-lookup"><span data-stu-id="1eb6b-181">Say something about this: `msgText`</span></span>
* <span data-ttu-id="1eb6b-182">Instructions d'affectation : `assignInstr`</span><span class="sxs-lookup"><span data-stu-id="1eb6b-182">Assignment Instructions: `assignInstr`</span></span>
* <span data-ttu-id="1eb6b-183">Titre de l'affectation : `assignTitle`</span><span class="sxs-lookup"><span data-stu-id="1eb6b-183">Assignment Title: `assignTitle`</span></span>

#### <a name="example"></a><span data-ttu-id="1eb6b-184">Exemple</span><span class="sxs-lookup"><span data-stu-id="1eb6b-184">Example</span></span>

 <span data-ttu-id="1eb6b-185">Les valeurs de formulaire par défaut sont données dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1eb6b-185">Default form values are given in the following example:</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a><span data-ttu-id="1eb6b-186">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1eb6b-186">See also</span></span>

- [<span data-ttu-id="1eb6b-187">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="1eb6b-187">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
