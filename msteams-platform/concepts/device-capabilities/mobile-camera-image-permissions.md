---
title: Intégrer les fonctionnalités médias
description: Comment utiliser le SDK client JavaScript teams pour activer les fonctionnalités multimédias
keywords: Média d’autorisations d’appareil natif des fonctionnalités du microphone d’image de l’appareil photo
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 375d68c7c712b7a8d2f7114b47aae61c889b4197
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449578"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="58cf5-104">Intégrer les fonctionnalités médias</span><span class="sxs-lookup"><span data-stu-id="58cf5-104">Integrate media capabilities</span></span> 

<span data-ttu-id="58cf5-105">Ce document vous guide sur l’intégration des fonctionnalités multimédias.</span><span class="sxs-lookup"><span data-stu-id="58cf5-105">This document guides you on how to integrate media capabilities.</span></span> <span data-ttu-id="58cf5-106">Cette intégration combine les fonctionnalités natives de l’appareil, telles que la **caméra** et **le microphone,** avec la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="58cf5-106">This integration combines the native device capabilities, such as the **camera** and **microphone** with the Teams platform.</span></span>  

<span data-ttu-id="58cf5-107">Vous pouvez utiliser le [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit les outils nécessaires pour que votre application accède aux autorisations d’appareil d’un [utilisateur.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="58cf5-107">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="58cf5-108">Utilisez les API de fonctionnalité multimédia appropriées pour intégrer  les fonctionnalités natives de l’appareil, telles que la caméra et le **microphone,** à la plateforme Teams dans votre application mobile Microsoft Teams, et créez une expérience plus riche.</span><span class="sxs-lookup"><span data-stu-id="58cf5-108">Use suitable  media capability APIs to integrate the native device capabilities, such as the **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="58cf5-109">Avantage de l’intégration des fonctionnalités multimédias</span><span class="sxs-lookup"><span data-stu-id="58cf5-109">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="58cf5-110">Le principal avantage de l’intégration des fonctionnalités des appareils dans vos applications Teams est qu’il tire parti des contrôles Teams natifs pour offrir une expérience riche et immersive à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="58cf5-110">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="58cf5-111">Pour intégrer des fonctionnalités multimédias, vous devez mettre à jour le fichier manifeste de l’application et appeler les API de fonctionnalité multimédia.</span><span class="sxs-lookup"><span data-stu-id="58cf5-111">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="58cf5-112">Pour une intégration efficace, vous devez bien comprendre les extraits de [code](#code-snippets) pour appeler les API respectives, ce qui vous permet d’utiliser les fonctionnalités multimédias natives.</span><span class="sxs-lookup"><span data-stu-id="58cf5-112">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="58cf5-113">Il est important de vous familiariser avec les erreurs de [réponse d’API](#error-handling) pour gérer les erreurs dans votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="58cf5-113">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="58cf5-114">Actuellement, la prise en charge des fonctionnalités multimédias par Microsoft Teams est disponible uniquement pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="58cf5-114">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="58cf5-115">Mettre à jour le manifeste</span><span class="sxs-lookup"><span data-stu-id="58cf5-115">Update manifest</span></span>

<span data-ttu-id="58cf5-116">Mettez à jour votre application Teams [manifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la propriété et en `devicePermissions` spécifiant `media` .</span><span class="sxs-lookup"><span data-stu-id="58cf5-116">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="58cf5-117">Il permet à votre application de demander les autorisations  requises aux utilisateurs avant de commencer à utiliser l’appareil photo pour capturer l’image, d’ouvrir la galerie pour sélectionner une image à soumettre en pièce jointe ou d’utiliser le **microphone** pour enregistrer la conversation.</span><span class="sxs-lookup"><span data-stu-id="58cf5-117">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="58cf5-118">**L’invite Demander des autorisations** s’affiche automatiquement lorsqu’une API Teams pertinente est lancée.</span><span class="sxs-lookup"><span data-stu-id="58cf5-118">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="58cf5-119">Pour plus d’informations, voir [Demander des autorisations d’appareil.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="58cf5-119">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="58cf5-120">API de fonctionnalité multimédia</span><span class="sxs-lookup"><span data-stu-id="58cf5-120">Media capability APIs</span></span>

<span data-ttu-id="58cf5-121">Les [API selectMedia,](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)et [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) vous permettent d’utiliser les fonctionnalités multimédias natives comme suit :</span><span class="sxs-lookup"><span data-stu-id="58cf5-121">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="58cf5-122">Utilisez le **microphone natif pour** permettre aux utilisateurs d’enregistrer du contenu **audio** (enregistrer 10 minutes de conversation) à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="58cf5-122">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="58cf5-123">Utilisez le contrôle **d’appareil photo natif** pour permettre aux utilisateurs de **capturer et d’attacher des images** en mouvement.</span><span class="sxs-lookup"><span data-stu-id="58cf5-123">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="58cf5-124">Utilisez la prise **en charge de la galerie native** pour permettre aux utilisateurs de sélectionner des images **d’appareil** en tant que pièces jointes.</span><span class="sxs-lookup"><span data-stu-id="58cf5-124">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="58cf5-125">Utilisez le contrôle **visionneuse d’images natives** **pour afficher un aperçu de plusieurs images** à la fois.</span><span class="sxs-lookup"><span data-stu-id="58cf5-125">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="58cf5-126">Prise **en charge du transfert d’images** de grande taille (de 1 Mo à 50 Mo) via le pont du SDK.</span><span class="sxs-lookup"><span data-stu-id="58cf5-126">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="58cf5-127">Prise en **charge des fonctionnalités d’image avancées** permettant aux utilisateurs d’afficher un aperçu et de modifier des images :</span><span class="sxs-lookup"><span data-stu-id="58cf5-127">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="58cf5-128">Analysez le document, le tableau blanc et les cartes de visite par le biais de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="58cf5-128">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
> * <span data-ttu-id="58cf5-129">Les API , et les API peuvent être appelés à partir de plusieurs surfaces Teams, telles que les modules de tâche, les `selectMedia` `getMedia` `viewImages` onglets et les applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="58cf5-129">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces, such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="58cf5-130">Pour plus d’informations, voir [Points d’entrée pour les applications Teams.](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="58cf5-130">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
> * <span data-ttu-id="58cf5-131">`selectMedia` L’API a été étendue pour prendre en charge les propriétés de microphone et audio.</span><span class="sxs-lookup"><span data-stu-id="58cf5-131">`selectMedia` API has been extended to support microphone and audio properties.</span></span>

<span data-ttu-id="58cf5-132">Vous devez utiliser l’ensemble d’API suivant pour activer les fonctionnalités multimédias de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="58cf5-132">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="58cf5-133">API</span><span class="sxs-lookup"><span data-stu-id="58cf5-133">API</span></span>      | <span data-ttu-id="58cf5-134">Description</span><span class="sxs-lookup"><span data-stu-id="58cf5-134">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="58cf5-135">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) **(Appareil photo)**</span><span class="sxs-lookup"><span data-stu-id="58cf5-135">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="58cf5-136">Cette API permet aux utilisateurs de capturer ou de sélectionner **du contenu multimédia** à partir de l’appareil photo de l’appareil et de le renvoyer à l’application web.</span><span class="sxs-lookup"><span data-stu-id="58cf5-136">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="58cf5-137">Les utilisateurs peuvent modifier, rogner, faire pivoter, annoter ou dessiner sur des images avant l’envoi.</span><span class="sxs-lookup"><span data-stu-id="58cf5-137">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="58cf5-138">En réponse à , l’application web reçoit les ID multimédias des images sélectionnées et une miniature du `selectMedia` média sélectionné.</span><span class="sxs-lookup"><span data-stu-id="58cf5-138">In response to `selectMedia`, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="58cf5-139">Cette API peut être configurée davantage via la configuration [ImageProps.](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="58cf5-139">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="58cf5-140">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)</span><span class="sxs-lookup"><span data-stu-id="58cf5-140">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="58cf5-141">Définissez [mediaType sur](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) `4` dans `selectMedia` l’API pour accéder à la fonctionnalité microphone.</span><span class="sxs-lookup"><span data-stu-id="58cf5-141">Set the [mediaType](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in `selectMedia` API for accessing microphone  capability.</span></span> <span data-ttu-id="58cf5-142">Cette API permet également aux utilisateurs d’enregistrer du contenu audio à partir du microphone de l’appareil et de renvoyer des clips enregistrés à l’application web.</span><span class="sxs-lookup"><span data-stu-id="58cf5-142">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="58cf5-143">Les utilisateurs peuvent suspendre, ré-enregistrer et lire l’aperçu de l’enregistrement avant la soumission.</span><span class="sxs-lookup"><span data-stu-id="58cf5-143">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="58cf5-144">En réponse à **selectMedia,** l’application web reçoit les ID multimédias de l’enregistrement audio sélectionné.</span><span class="sxs-lookup"><span data-stu-id="58cf5-144">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="58cf5-145">Utilisez `maxDuration` , si vous avez besoin de configurer une durée en minutes pour l’enregistrement de la conversation.</span><span class="sxs-lookup"><span data-stu-id="58cf5-145">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="58cf5-146">La durée actuelle de l’enregistrement est de 10 minutes, après quoi l’enregistrement se termine.</span><span class="sxs-lookup"><span data-stu-id="58cf5-146">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="58cf5-147">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="58cf5-147">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="58cf5-148">Cette API récupère le média capturé par l’API en blocs, quelle que `selectMedia` soit la taille du média.</span><span class="sxs-lookup"><span data-stu-id="58cf5-148">This API retrieves the media captured by `selectMedia` API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="58cf5-149">Ces blocs sont assemblés et renvoyés à l’application web en tant que fichier ou blob.</span><span class="sxs-lookup"><span data-stu-id="58cf5-149">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="58cf5-150">La rupture du média en blocs plus petits facilite le transfert de fichiers de grande taille.</span><span class="sxs-lookup"><span data-stu-id="58cf5-150">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="58cf5-151">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="58cf5-151">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="58cf5-152">Cette API permet à l’utilisateur d’afficher des images en mode plein écran en tant que liste de défilement.</span><span class="sxs-lookup"><span data-stu-id="58cf5-152">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|


<span data-ttu-id="58cf5-153">**Expérience d’application web pour l’API selectMedia pour la fonctionnalité d’image** 
 ![ Expérience d’appareil photo et d’image dans Teams](../../assets/images/tabs/image-capability.png)</span><span class="sxs-lookup"><span data-stu-id="58cf5-153">**Web app experience for selectMedia API for image capability**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability.png)</span></span>

<span data-ttu-id="58cf5-154">**Expérience d’application web pour l’API selectMedia pour la fonctionnalité de microphone** 
 ![ expérience d’application web pour la fonctionnalité de microphone](../../assets/images/tabs/microphone-capability.png)</span><span class="sxs-lookup"><span data-stu-id="58cf5-154">**Web app experience for selectMedia API for microphone capability**
![web app experience for microphone capability](../../assets/images/tabs/microphone-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="58cf5-155">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="58cf5-155">Error handling</span></span>

<span data-ttu-id="58cf5-156">Vous devez veiller à gérer ces erreurs de manière appropriée dans votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="58cf5-156">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="58cf5-157">Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées :</span><span class="sxs-lookup"><span data-stu-id="58cf5-157">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 


|<span data-ttu-id="58cf5-158">Code d’erreur</span><span class="sxs-lookup"><span data-stu-id="58cf5-158">Error code</span></span> |  <span data-ttu-id="58cf5-159">Nom de l’erreur</span><span class="sxs-lookup"><span data-stu-id="58cf5-159">Error name</span></span>     | <span data-ttu-id="58cf5-160">Condition</span><span class="sxs-lookup"><span data-stu-id="58cf5-160">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="58cf5-161">**100**</span><span class="sxs-lookup"><span data-stu-id="58cf5-161">**100**</span></span> | <span data-ttu-id="58cf5-162">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="58cf5-162">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="58cf5-163">L’API n’est pas prise en charge sur la plateforme actuelle.</span><span class="sxs-lookup"><span data-stu-id="58cf5-163">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="58cf5-164">**404**</span><span class="sxs-lookup"><span data-stu-id="58cf5-164">**404**</span></span> | <span data-ttu-id="58cf5-165">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="58cf5-165">FILE_NOT_FOUND</span></span> | <span data-ttu-id="58cf5-166">Le fichier spécifié n’est pas trouvé à l’emplacement donné.</span><span class="sxs-lookup"><span data-stu-id="58cf5-166">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="58cf5-167">**500**</span><span class="sxs-lookup"><span data-stu-id="58cf5-167">**500**</span></span> | <span data-ttu-id="58cf5-168">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="58cf5-168">INTERNAL_ERROR</span></span> | <span data-ttu-id="58cf5-169">Une erreur interne est rencontrée lors de l’opération requise.</span><span class="sxs-lookup"><span data-stu-id="58cf5-169">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="58cf5-170">**1000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-170">**1000**</span></span> | <span data-ttu-id="58cf5-171">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="58cf5-171">PERMISSION_DENIED</span></span> |<span data-ttu-id="58cf5-172">L’autorisation est refusée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58cf5-172">Permission is denied by the user.</span></span>|
| <span data-ttu-id="58cf5-173">**2000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-173">**2000**</span></span> |<span data-ttu-id="58cf5-174">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="58cf5-174">NETWORK_ERROR</span></span> | <span data-ttu-id="58cf5-175">Problème réseau.</span><span class="sxs-lookup"><span data-stu-id="58cf5-175">Network issue.</span></span>|
| <span data-ttu-id="58cf5-176">**3000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-176">**3000**</span></span> | <span data-ttu-id="58cf5-177">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="58cf5-177">NO_HW_SUPPORT</span></span> | <span data-ttu-id="58cf5-178">Le matériel sous-jacent ne prend pas en charge la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="58cf5-178">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="58cf5-179">**4000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-179">**4000**</span></span>| <span data-ttu-id="58cf5-180">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="58cf5-180">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="58cf5-181">Un ou plusieurs arguments ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="58cf5-181">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="58cf5-182">**5000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-182">**5000**</span></span> | <span data-ttu-id="58cf5-183">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="58cf5-183">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="58cf5-184">L’utilisateur n’est pas autorisé à effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="58cf5-184">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="58cf5-185">**6000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-185">**6000**</span></span> |<span data-ttu-id="58cf5-186">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="58cf5-186">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="58cf5-187">L’opération n’a pas pu être achevée en raison de ressources insuffisantes.</span><span class="sxs-lookup"><span data-stu-id="58cf5-187">Operation could not be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="58cf5-188">**7000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-188">**7000**</span></span> | <span data-ttu-id="58cf5-189">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="58cf5-189">THROTTLE</span></span> | <span data-ttu-id="58cf5-190">La plateforme a limitée la demande car l’API a été fréquemment invoquée.</span><span class="sxs-lookup"><span data-stu-id="58cf5-190">Platform throttled the request as the API was invoked frequently.</span></span>|
|  <span data-ttu-id="58cf5-191">**8000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-191">**8000**</span></span> | <span data-ttu-id="58cf5-192">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="58cf5-192">USER_ABORT</span></span> |<span data-ttu-id="58cf5-193">L’utilisateur abandonne l’opération.</span><span class="sxs-lookup"><span data-stu-id="58cf5-193">User aborts the operation.</span></span>|
| <span data-ttu-id="58cf5-194">**9000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-194">**9000**</span></span>| <span data-ttu-id="58cf5-195">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="58cf5-195">OLD_PLATFORM</span></span> | <span data-ttu-id="58cf5-196">Le code de plateforme est obsolète et n’implémente pas cette API.</span><span class="sxs-lookup"><span data-stu-id="58cf5-196">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="58cf5-197">**10000**</span><span class="sxs-lookup"><span data-stu-id="58cf5-197">**10000**</span></span>| <span data-ttu-id="58cf5-198">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="58cf5-198">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="58cf5-199">La valeur de retour est trop grande et a dépassé les limites de taille de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="58cf5-199">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="58cf5-200">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="58cf5-200">Code snippets</span></span>

<span data-ttu-id="58cf5-201">**Appel `selectMedia` API de** capture d’images à l’aide de l’appareil photo :</span><span class="sxs-lookup"><span data-stu-id="58cf5-201">**Calling `selectMedia` API** for capturing images using camera:</span></span>

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

<span data-ttu-id="58cf5-202">**Appel `getMedia` API permettant** de récupérer des médias de grande taille en blocs :</span><span class="sxs-lookup"><span data-stu-id="58cf5-202">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

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

<span data-ttu-id="58cf5-203">**Appel `viewImages` API par ID renvoyé par `selectMedia` l’API**:</span><span class="sxs-lookup"><span data-stu-id="58cf5-203">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

```javascript
// View images by id:
// Assumption: attachmentArray = select Media API Output
let uriList = [];
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

<span data-ttu-id="58cf5-204">**Appel `viewImages` API par URL**:</span><span class="sxs-lookup"><span data-stu-id="58cf5-204">**Calling `viewImages` API by URL**:</span></span>

```javascript
// View Images by URL:
// Assumption 2 urls, url1 and url2
let uriList = [];
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
```

<span data-ttu-id="58cf5-205">**Appel `selectMedia` et API pour `getMedia` l’enregistrement audio via le microphone**:</span><span class="sxs-lookup"><span data-stu-id="58cf5-205">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

```javascript
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Audio,
    maxMediaCount: 1,
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    // If you want to directly use the audio file (for smaller file sizes (~4MB))    if (attachments) {
    let audioResult = attachments[0];
    var videoElement = document.createElement("video");
    videoElement.setAttribute("src", ("data:" + y.mimeType + ";base64," + y.preview));
    //To use the audio file via get Media API for bigger audio file sizes greater than 4MB        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("video")) {
            videoElement.setAttribute("src", URL.createObjectURL(blob));
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

## <a name="see-also"></a><span data-ttu-id="58cf5-206">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="58cf5-206">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="58cf5-207">Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="58cf5-207">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="58cf5-208">Intégrer des fonctionnalités d’emplacement dans Teams</span><span class="sxs-lookup"><span data-stu-id="58cf5-208">Integrate location capabilities in Teams</span></span>](location-capability.md)