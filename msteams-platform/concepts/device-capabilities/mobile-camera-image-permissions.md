---
title: Fonctionnalités de l’appareil photo et de l’image dans teams
description: Comment utiliser le kit de développement logiciel (SDK) du client JavaScript teams pour activer les fonctionnalités d’image et de caméra natives
keywords: fonctionnalités de l’image de l’appareil photo natives
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d0ca4dc9c289ec525aa99ea0e156a9f91f5b5d4a
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576873"
---
# <a name="camera-and-image-capabilities-in-teams"></a><span data-ttu-id="1bd98-104">Fonctionnalités de l’appareil photo et de l’image dans teams</span><span class="sxs-lookup"><span data-stu-id="1bd98-104">Camera and image capabilities in Teams</span></span>

>[!IMPORTANT]
>
> * <span data-ttu-id="1bd98-105">Actuellement, la prise en charge de teams pour les fonctionnalités d’image et de caméra est uniquement disponible pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="1bd98-105">At present, Teams support for camera and image capabilities is only available for mobile clients.</span></span>
>* <span data-ttu-id="1bd98-106">Les `selectMedia` `getMedia` API, et `viewImages` peuvent être appelées à partir de plusieurs surfaces Teams, telles que des modules de tâches, des onglets et des applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="1bd98-106">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="1bd98-107">Pour plus d’informations, _consultez la rubrique_ [points d’entrée pour les applications teams](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="1bd98-107">For more details, _see_ [Entry points for Teams apps](../extensibility-points.md)</span></span>

<span data-ttu-id="1bd98-108">Vous pouvez utiliser le  [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)pour intégrer facilement les fonctionnalités de caméra et d’image dans votre application mobile Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1bd98-108">You can use the  [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), to easily integrate camera and image capabilities within your Microsoft Teams mobile app.</span></span> <span data-ttu-id="1bd98-109">Le kit de développement logiciel (SDK) fournit les outils nécessaires à votre application pour accéder aux autorisations de l' [appareil](native-device-permissions.md?tabs=desktop#device-permissions) d’un utilisateur et créer une expérience plus riche.</span><span class="sxs-lookup"><span data-stu-id="1bd98-109">The SDK provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md?tabs=desktop#device-permissions) and build a richer experience.</span></span>

<span data-ttu-id="1bd98-110">Les API [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)et [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) vous permettent d’utiliser les fonctionnalités de caméra/image natives comme suit :</span><span class="sxs-lookup"><span data-stu-id="1bd98-110">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native camera/image capabilities as follows:</span></span>

* <span data-ttu-id="1bd98-111">Utilisez le **contrôle** de la caméra native pour permettre aux utilisateurs de **capturer et de joindre des images** en déplacement.</span><span class="sxs-lookup"><span data-stu-id="1bd98-111">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="1bd98-112">Utilisez la **prise en charge** de la Galerie native pour permettre aux utilisateurs de **Sélectionner des images d’appareil** en pièces jointes.</span><span class="sxs-lookup"><span data-stu-id="1bd98-112">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="1bd98-113">Utilisez **le contrôle** de l’afficheur d’images natives pour afficher un **aperçu de plusieurs images** à la fois.</span><span class="sxs-lookup"><span data-stu-id="1bd98-113">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="1bd98-114">Prise en charge du **transfert d’image volumineux** (jusqu’à 50 Mo) via le pont SDK</span><span class="sxs-lookup"><span data-stu-id="1bd98-114">Support **large image transfer** (up to 50 MB) via the SDK bridge</span></span>
* <span data-ttu-id="1bd98-115">Prise en charge des **fonctionnalités d’image avancées** permettant aux utilisateurs de prévisualiser et de modifier les images :</span><span class="sxs-lookup"><span data-stu-id="1bd98-115">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="1bd98-116">Numérisez un document, un tableau blanc, des cartes de visite, etc., via l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="1bd98-116">Scan document, whiteboard, business cards, etc., through the camera.</span></span>
  * <span data-ttu-id="1bd98-117">Rogner et faire pivoter les images.</span><span class="sxs-lookup"><span data-stu-id="1bd98-117">Crop and rotate the images.</span></span>
  * <span data-ttu-id="1bd98-118">Ajouter du texte, de l’entrée manuscrite ou une annotation à main levée à l’image.</span><span class="sxs-lookup"><span data-stu-id="1bd98-118">Add text, ink, or freehand annotation to the image.</span></span>

## <a name="get-started"></a><span data-ttu-id="1bd98-119">Prise en main</span><span class="sxs-lookup"><span data-stu-id="1bd98-119">Get started</span></span>

<span data-ttu-id="1bd98-120">Mettez à jour votre application teams [manifest.jssur](../../resources/schema/manifest-schema.md#devicepermissions) fichier en ajoutant la `devicePermissions`  propriété et en spécifiant `media` .</span><span class="sxs-lookup"><span data-stu-id="1bd98-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions`  property and specifying `media`.</span></span> <span data-ttu-id="1bd98-121">Cela permet à votre application de demander aux utilisateurs finaux les autorisations requises avant d’utiliser l’appareil photo pour capturer l’image ou ouvrir la Galerie pour sélectionner une image à envoyer en tant que pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="1bd98-121">This allows your app to ask for requisite permissions from end-users before they use the camera to capture the image or open the gallery to select an image to submit as an attachment.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="1bd98-122">L’invite _demander des autorisations_ s’affiche automatiquement lorsqu’une API teams pertinente est initiée.</span><span class="sxs-lookup"><span data-stu-id="1bd98-122">The _Request Permissions_ prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="1bd98-123">Pour plus d’informations, *consultez la rubrique* [Request Device permissions](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="1bd98-123">For more details, *see* [Request device permissions](native-device-permissions.md).</span></span>

## <a name="using-camera-and-image-capability-apis"></a><span data-ttu-id="1bd98-124">Utilisation des API de fonctionnalité d’image et de caméra</span><span class="sxs-lookup"><span data-stu-id="1bd98-124">Using camera and image capability APIs</span></span>

<span data-ttu-id="1bd98-125">Vous pouvez utiliser l’ensemble d’API suivant pour activer les fonctionnalités de l’appareil photo et du périphérique d’image :</span><span class="sxs-lookup"><span data-stu-id="1bd98-125">You can use the following set of APIs to enable camera and image device capabilities:</span></span>

| <span data-ttu-id="1bd98-126">API</span><span class="sxs-lookup"><span data-stu-id="1bd98-126">API</span></span>      | <span data-ttu-id="1bd98-127">Description</span><span class="sxs-lookup"><span data-stu-id="1bd98-127">Description</span></span>   |
| --- | --- |
| [<span data-ttu-id="1bd98-128">**selectMedia**</span><span class="sxs-lookup"><span data-stu-id="1bd98-128">**selectMedia**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| <span data-ttu-id="1bd98-129">Cette API permet aux utilisateurs de **capturer ou de sélectionner des médias à partir d’un périphérique natif** et de revenir à l’application Web.</span><span class="sxs-lookup"><span data-stu-id="1bd98-129">This API allows users to **capture or select media from a native device** and return to the web-app.</span></span> <span data-ttu-id="1bd98-130">Les utilisateurs peuvent choisir de modifier, découper, faire pivoter, annoter ou dessiner sur des images avant leur envoi.</span><span class="sxs-lookup"><span data-stu-id="1bd98-130">Users may choose to edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="1bd98-131">En réponse à **selectMedia**, l’application Web reçoit les ID de médias des images sélectionnées et peut recevoir une miniature du média sélectionné.</span><span class="sxs-lookup"><span data-stu-id="1bd98-131">In response to **selectMedia**, the web-app will receive media ids of selected images and may receive a thumbnail of the selected media.</span></span> |
| [<span data-ttu-id="1bd98-132">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="1bd98-132">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="1bd98-133">Cette API récupère le média dans des segments quelle que soit la taille.</span><span class="sxs-lookup"><span data-stu-id="1bd98-133">This API retrieves the media in chunks irrespective of size.</span></span> <span data-ttu-id="1bd98-134">Ces segments sont assemblés et renvoyés à l’application Web sous la forme d’un fichier/BLOB.</span><span class="sxs-lookup"><span data-stu-id="1bd98-134">These chunks are assembled and sent back to the web app as a file/blob.</span></span> <span data-ttu-id="1bd98-135">Avec cette API, une image est divisée en morceaux plus petits pour faciliter le transfert d’image volumineux.</span><span class="sxs-lookup"><span data-stu-id="1bd98-135">With this API an image is broken into smaller chunks to facilitate large image transfer.</span></span> |
| [<span data-ttu-id="1bd98-136">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="1bd98-136">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="1bd98-137">Cette API permet à l’utilisateur d’afficher des images en mode plein écran sous la forme d’une liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="1bd98-137">This API enables the user to view images full-screen mode as a scrollable list.</span></span>|

<span data-ttu-id="1bd98-138">**Expérience des applications Web pour l’API selectMedia** 
 ![ appareil photo et image de l’appareil dans teams](../../assets/images/tabs/image-capability-screenshot.jpg)</span><span class="sxs-lookup"><span data-stu-id="1bd98-138">**Web app experience for selectMedia API**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability-screenshot.jpg)</span></span>

## <a name="error-handling"></a><span data-ttu-id="1bd98-139">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="1bd98-139">Error handling</span></span>

<span data-ttu-id="1bd98-140">Vous devez comprendre les codes d’erreur de réponse de l’API et les gérer de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="1bd98-140">You should understand the API response error codes and handle them appropriately.</span></span> <span data-ttu-id="1bd98-141">Vous trouverez ci-dessous la liste des codes d’erreur pouvant être renvoyés par la plateforme :</span><span class="sxs-lookup"><span data-stu-id="1bd98-141">Below is a list of error codes that may be returned by the platform:</span></span>

|<span data-ttu-id="1bd98-142">Code d'erreur</span><span class="sxs-lookup"><span data-stu-id="1bd98-142">Error code</span></span> |  <span data-ttu-id="1bd98-143">Nom de l’erreur</span><span class="sxs-lookup"><span data-stu-id="1bd98-143">Error Name</span></span>     | <span data-ttu-id="1bd98-144">Condition</span><span class="sxs-lookup"><span data-stu-id="1bd98-144">Condition</span></span>|
| --- | --- | --- |
| <span data-ttu-id="1bd98-145">**100**</span><span class="sxs-lookup"><span data-stu-id="1bd98-145">**100**</span></span> | <span data-ttu-id="1bd98-146">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="1bd98-146">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="1bd98-147">L’API n’est pas prise en charge dans la plateforme actuelle.</span><span class="sxs-lookup"><span data-stu-id="1bd98-147">API not supported in the current platform.</span></span>|
| <span data-ttu-id="1bd98-148">**404**</span><span class="sxs-lookup"><span data-stu-id="1bd98-148">**404**</span></span> | <span data-ttu-id="1bd98-149">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="1bd98-149">FILE_NOT_FOUND</span></span> | <span data-ttu-id="1bd98-150">Le fichier spécifié est introuvable à l’emplacement donné.</span><span class="sxs-lookup"><span data-stu-id="1bd98-150">The file specified was not found on the given location.</span></span>|
| <span data-ttu-id="1bd98-151">**500**</span><span class="sxs-lookup"><span data-stu-id="1bd98-151">**500**</span></span> | <span data-ttu-id="1bd98-152">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="1bd98-152">INTERNAL_ERROR</span></span> | <span data-ttu-id="1bd98-153">Une erreur interne s’est produite lors de l’exécution de l’opération requise.</span><span class="sxs-lookup"><span data-stu-id="1bd98-153">Internal error encountered while performing the required operation.</span></span>|
| <span data-ttu-id="1bd98-154">**1000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-154">**1000**</span></span> | <span data-ttu-id="1bd98-155">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="1bd98-155">PERMISSION_DENIED</span></span> |<span data-ttu-id="1bd98-156">Autorisations refusées par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1bd98-156">Permissions denied by the user.</span></span>|
| <span data-ttu-id="1bd98-157">**2000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-157">**2000**</span></span> |<span data-ttu-id="1bd98-158">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="1bd98-158">NETWORK_ERROR</span></span> | <span data-ttu-id="1bd98-159">Problème réseau.</span><span class="sxs-lookup"><span data-stu-id="1bd98-159">Network issue.</span></span>|
| <span data-ttu-id="1bd98-160">**3000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-160">**3000**</span></span> | <span data-ttu-id="1bd98-161">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="1bd98-161">NO_HW_SUPPORT</span></span> | <span data-ttu-id="1bd98-162">Le matériel sous-jacent ne prend pas en charge la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1bd98-162">Underlying hardware doesn't support the capability.</span></span>|
| <span data-ttu-id="1bd98-163">**4000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-163">**4000**</span></span>| <span data-ttu-id="1bd98-164">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="1bd98-164">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="1bd98-165">Un ou plusieurs arguments ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="1bd98-165">One or more arguments is invalid.</span></span>|
| <span data-ttu-id="1bd98-166">**5000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-166">**5000**</span></span> | <span data-ttu-id="1bd98-167">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="1bd98-167">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="1bd98-168">L’utilisateur n’est pas autorisé à effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="1bd98-168">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="1bd98-169">**6000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-169">**6000**</span></span> |<span data-ttu-id="1bd98-170">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="1bd98-170">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="1bd98-171">L’opération n’a pas pu aboutir en raison de ressources insuffisantes.</span><span class="sxs-lookup"><span data-stu-id="1bd98-171">The operation couldn't be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="1bd98-172">**7000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-172">**7000**</span></span> | <span data-ttu-id="1bd98-173">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="1bd98-173">THROTTLE</span></span> | <span data-ttu-id="1bd98-174">La plateforme limite la demande, car l’API a été appelée trop fréquemment.</span><span class="sxs-lookup"><span data-stu-id="1bd98-174">The platform throttled the request because the API was invoked too frequently.</span></span>|
|  <span data-ttu-id="1bd98-175">**8000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-175">**8000**</span></span> | <span data-ttu-id="1bd98-176">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="1bd98-176">USER_ABORT</span></span> |<span data-ttu-id="1bd98-177">L’utilisateur a abandonné l’opération.</span><span class="sxs-lookup"><span data-stu-id="1bd98-177">User aborted the operation.</span></span>|
| <span data-ttu-id="1bd98-178">**9000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-178">**9000**</span></span>| <span data-ttu-id="1bd98-179">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="1bd98-179">OLD_PLATFORM</span></span> | <span data-ttu-id="1bd98-180">Le code de plateforme est obsolète et n’implémente pas cette API.</span><span class="sxs-lookup"><span data-stu-id="1bd98-180">The platform code is outdated and doesn't implement this API.</span></span>|
| <span data-ttu-id="1bd98-181">**10000**</span><span class="sxs-lookup"><span data-stu-id="1bd98-181">**10000**</span></span>| <span data-ttu-id="1bd98-182">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="1bd98-182">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="1bd98-183">La valeur renvoyée est trop importante et a dépassé les limites de taille de plateforme.</span><span class="sxs-lookup"><span data-stu-id="1bd98-183">The return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="sample-code-snippets"></a><span data-ttu-id="1bd98-184">Exemples d’extraits de code</span><span class="sxs-lookup"><span data-stu-id="1bd98-184">Sample code snippets</span></span>

<span data-ttu-id="1bd98-185">**API d’appel `selectMedia`**</span><span class="sxs-lookup"><span data-stu-id="1bd98-185">**Calling `selectMedia` API**</span></span>

```javascript
let imageProp: microsoftTeams.media.ImageProps = {
    sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
    startMode: microsoftTeams.media.CameraStartMode.Photo,
    ink: false,
    cameraSwitcher: false,
    textSticker: false,
    enableFilter: true,
};
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Image,
    maxMediaCount: 10,
    imageProps: imageProp
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    if (attachments) {
        let y = attachments[0];
        img.src = ("data:" + y.mimeType + ";base64," + y.preview);
    }
});
```

<span data-ttu-id="1bd98-186">**API d’appel `getMedia`**</span><span class="sxs-lookup"><span data-stu-id="1bd98-186">**Calling `getMedia` API**</span></span>

```javascript
let media: microsoftTeams.media.Media = attachments[0]
media.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("image")) {
            img.src = (URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

<span data-ttu-id="1bd98-187">**`viewImages`API d’appel par ID**</span><span class="sxs-lookup"><span data-stu-id="1bd98-187">**Calling `viewImages`  API by ID**</span></span>

```javascript
view images by id:
    assumption: attachmentArray = select Media API Outputlet uriList = [];
if (attachmentArray && attachmentArray.length > 0) {
    for (let i = 0; i < attachmentArray.length; i++) {
        let file = attachmentArray[i];
        if (file.mimeType.includes("image")) {
            let imageUri = {
                value: file.content,
                type: 1,
            }
            uriList.push(imageUri);
        } else {
            alert("File type is not image");
        }
    }
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

<span data-ttu-id="1bd98-188">**Appel de l’API viewImages par URL**</span><span class="sxs-lookup"><span data-stu-id="1bd98-188">**Calling viewImages API by URL**</span></span>

```javascript
View Images by URL:
    // Assumption 2 urls, url1 and url2let uriList = [];
    if (URL1 != null && URL1.length > 0) {
        let imageUri = {
            value: URL1,
            type: 2,
        }
        uriList.push(imageUri);
    }
if (URL2 != null && URL2.length > 0) {
    let imageUri = {
        value: URL2,
        type: 2,
    }
    uriList.push(imageUri);
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
}
```
