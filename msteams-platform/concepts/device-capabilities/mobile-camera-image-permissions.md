---
title: Intégrer les fonctionnalités médias
author: Rajeshwari-v
description: Utilisation du SDK Teams client JavaScript pour activer les fonctionnalités multimédias
keywords: Média d’autorisations d’appareil natif des fonctionnalités du microphone d’image de l’appareil photo
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 22d4a791e83cf36f18b75a3846865835b0ee024f
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211624"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="48eb0-104">Intégrer les fonctionnalités médias</span><span class="sxs-lookup"><span data-stu-id="48eb0-104">Integrate media capabilities</span></span> 

<span data-ttu-id="48eb0-105">Vous pouvez intégrer des fonctionnalités  natives d’appareil, telles que l’appareil photo et le **microphone,** à Teams application.</span><span class="sxs-lookup"><span data-stu-id="48eb0-105">You can integrate native device capabilities, such as the **camera** and **microphone** with your Teams app.</span></span> <span data-ttu-id="48eb0-106">Pour l’intégration, vous pouvez utiliser [Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), qui fournit les outils nécessaires pour que votre application accède aux autorisations d’appareil d’un [utilisateur.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="48eb0-106">For integration, you can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="48eb0-107">Utilisez les API de fonctionnalité multimédia appropriées pour  intégrer les fonctionnalités de l’appareil, telles que la caméra et le **microphone,** à la plateforme Teams dans votre application mobile Microsoft Teams, et créez une expérience plus riche.</span><span class="sxs-lookup"><span data-stu-id="48eb0-107">Use suitable media capability APIs to integrate the device capabilities, such as **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="48eb0-108">Avantage de l’intégration des fonctionnalités multimédias</span><span class="sxs-lookup"><span data-stu-id="48eb0-108">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="48eb0-109">Le principal avantage de l’intégration des fonctionnalités d’appareil dans vos applications Teams est qu’il tire parti des contrôles Teams natifs pour offrir une expérience riche et immersive à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="48eb0-109">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="48eb0-110">Pour intégrer des fonctionnalités multimédias, vous devez mettre à jour le fichier manifeste de l’application et appeler les API de fonctionnalité multimédia.</span><span class="sxs-lookup"><span data-stu-id="48eb0-110">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="48eb0-111">Pour une intégration efficace, vous devez bien comprendre les extraits de [code](#code-snippets) pour appeler les API respectives, ce qui vous permet d’utiliser les fonctionnalités multimédias natives.</span><span class="sxs-lookup"><span data-stu-id="48eb0-111">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="48eb0-112">Il est important de vous familiariser avec les erreurs de réponse [d’API](#error-handling) pour gérer les erreurs dans votre Teams application.</span><span class="sxs-lookup"><span data-stu-id="48eb0-112">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> * <span data-ttu-id="48eb0-113">Actuellement, Microsoft Teams prise en charge des fonctionnalités multimédias est disponible uniquement pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="48eb0-113">Currently, Microsoft Teams support for media capabilities is available for mobile clients only.</span></span>   
> * <span data-ttu-id="48eb0-114">Actuellement, Teams ne prend pas en charge les autorisations d’appareil pour les applications à fenêtres multiples, les onglets et le bureau secondaire de la réunion.</span><span class="sxs-lookup"><span data-stu-id="48eb0-114">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span>    

## <a name="update-manifest"></a><span data-ttu-id="48eb0-115">Mettre à jour le manifeste</span><span class="sxs-lookup"><span data-stu-id="48eb0-115">Update manifest</span></span>

<span data-ttu-id="48eb0-116">Mettez à jour [Teams’applicationmanifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la `devicePermissions` propriété et en spécifiant `media` .</span><span class="sxs-lookup"><span data-stu-id="48eb0-116">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="48eb0-117">Il permet à votre application de demander les autorisations  requises aux utilisateurs avant de commencer à utiliser l’appareil photo pour capturer l’image, d’ouvrir la galerie pour sélectionner une image à soumettre en pièce jointe ou d’utiliser le **microphone** pour enregistrer la conversation.</span><span class="sxs-lookup"><span data-stu-id="48eb0-117">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span> <span data-ttu-id="48eb0-118">La mise à jour du manifeste de l’application est la suivante :</span><span class="sxs-lookup"><span data-stu-id="48eb0-118">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="48eb0-119">**L’invite Demander des autorisations** s’affiche automatiquement lorsqu’une API Teams est lancée.</span><span class="sxs-lookup"><span data-stu-id="48eb0-119">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="48eb0-120">Pour plus d’informations, voir [Demander des autorisations d’appareil.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="48eb0-120">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="48eb0-121">API de fonctionnalité multimédia</span><span class="sxs-lookup"><span data-stu-id="48eb0-121">Media capability APIs</span></span>

<span data-ttu-id="48eb0-122">Les [API selectMedia,](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)et [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) vous permettent d’utiliser les fonctionnalités multimédias natives comme suit :</span><span class="sxs-lookup"><span data-stu-id="48eb0-122">The [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="48eb0-123">Utilisez le **microphone natif pour** permettre aux utilisateurs d’enregistrer du contenu **audio** (enregistrer 10 minutes de conversation) à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="48eb0-123">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="48eb0-124">Utilisez le contrôle **d’appareil photo natif** pour permettre aux utilisateurs de **capturer et d’attacher** des images en mouvement.</span><span class="sxs-lookup"><span data-stu-id="48eb0-124">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="48eb0-125">Utilisez la prise **en charge de la galerie native** pour permettre aux utilisateurs de sélectionner des images **d’appareil** en tant que pièces jointes.</span><span class="sxs-lookup"><span data-stu-id="48eb0-125">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="48eb0-126">Utilisez le contrôle **visionneuse d’images natives** **pour afficher un aperçu de plusieurs images** à la fois.</span><span class="sxs-lookup"><span data-stu-id="48eb0-126">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="48eb0-127">Prise **en charge du transfert d’images** de grande taille (de 1 Mo à 50 Mo) via le pont du SDK.</span><span class="sxs-lookup"><span data-stu-id="48eb0-127">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="48eb0-128">Prise en **charge des fonctionnalités d’image avancées** permettant aux utilisateurs d’afficher un aperçu et de modifier des images :</span><span class="sxs-lookup"><span data-stu-id="48eb0-128">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="48eb0-129">Analysez le document, le tableau blanc et les cartes de visite par le biais de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="48eb0-129">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
> * <span data-ttu-id="48eb0-130">Les API , et les API peuvent être appelés à partir de plusieurs surfaces Teams, telles que les modules de tâche, les onglets et `selectMedia` `getMedia` les applications `viewImages` personnelles.</span><span class="sxs-lookup"><span data-stu-id="48eb0-130">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces, such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="48eb0-131">Pour plus d’informations, voir [Points d’entrée Teams applications.](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="48eb0-131">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
> * <span data-ttu-id="48eb0-132">`selectMedia` L’API a été étendue pour prendre en charge les propriétés de microphone et audio.</span><span class="sxs-lookup"><span data-stu-id="48eb0-132">`selectMedia` API has been extended to support microphone and audio properties.</span></span>

<span data-ttu-id="48eb0-133">Vous devez utiliser l’ensemble d’API suivant pour activer les fonctionnalités multimédias de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="48eb0-133">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="48eb0-134">API</span><span class="sxs-lookup"><span data-stu-id="48eb0-134">API</span></span>      | <span data-ttu-id="48eb0-135">Description</span><span class="sxs-lookup"><span data-stu-id="48eb0-135">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="48eb0-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Appareil photo)**</span><span class="sxs-lookup"><span data-stu-id="48eb0-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="48eb0-137">Cette API permet aux utilisateurs de capturer ou de sélectionner **du contenu multimédia** à partir de l’appareil photo de l’appareil et de le renvoyer à l’application web.</span><span class="sxs-lookup"><span data-stu-id="48eb0-137">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="48eb0-138">Les utilisateurs peuvent modifier, rogner, faire pivoter, annoter ou dessiner sur des images avant l’envoi.</span><span class="sxs-lookup"><span data-stu-id="48eb0-138">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="48eb0-139">En réponse à , l’application web reçoit les ID multimédias des images sélectionnées et une miniature du `selectMedia` média sélectionné.</span><span class="sxs-lookup"><span data-stu-id="48eb0-139">In response to `selectMedia`, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="48eb0-140">Cette API peut être configurée davantage via la configuration [ImageProps.](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="48eb0-140">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="48eb0-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span><span class="sxs-lookup"><span data-stu-id="48eb0-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="48eb0-142">Définissez [mediaType sur](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) `4` dans `selectMedia` l’API pour accéder à la fonctionnalité microphone.</span><span class="sxs-lookup"><span data-stu-id="48eb0-142">Set the [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in `selectMedia` API for accessing microphone  capability.</span></span> <span data-ttu-id="48eb0-143">Cette API permet également aux utilisateurs d’enregistrer du contenu audio à partir du microphone de l’appareil et de renvoyer des clips enregistrés à l’application web.</span><span class="sxs-lookup"><span data-stu-id="48eb0-143">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="48eb0-144">Les utilisateurs peuvent suspendre, ré-enregistrer et lire l’aperçu de l’enregistrement avant la soumission.</span><span class="sxs-lookup"><span data-stu-id="48eb0-144">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="48eb0-145">En réponse à **selectMedia,** l’application web reçoit les ID multimédias de l’enregistrement audio sélectionné.</span><span class="sxs-lookup"><span data-stu-id="48eb0-145">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="48eb0-146">Utilisez `maxDuration` , si vous avez besoin de configurer une durée en minutes pour l’enregistrement de la conversation.</span><span class="sxs-lookup"><span data-stu-id="48eb0-146">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="48eb0-147">La durée actuelle de l’enregistrement est de 10 minutes, après quoi l’enregistrement se termine.</span><span class="sxs-lookup"><span data-stu-id="48eb0-147">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="48eb0-148">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="48eb0-148">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="48eb0-149">Cette API récupère le média capturé par l’API en blocs, quelle que `selectMedia` soit la taille du média.</span><span class="sxs-lookup"><span data-stu-id="48eb0-149">This API retrieves the media captured by `selectMedia` API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="48eb0-150">Ces blocs sont assemblés et renvoyés à l’application web en tant que fichier ou blob.</span><span class="sxs-lookup"><span data-stu-id="48eb0-150">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="48eb0-151">La rupture du média en blocs plus petits facilite le transfert de fichiers de grande taille.</span><span class="sxs-lookup"><span data-stu-id="48eb0-151">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="48eb0-152">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="48eb0-152">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="48eb0-153">Cette API permet à l’utilisateur d’afficher des images en mode plein écran en tant que liste de défilement.</span><span class="sxs-lookup"><span data-stu-id="48eb0-153">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|

<span data-ttu-id="48eb0-154">L’image suivante illustre l’expérience d’application web de `selectMedia` l’API pour la fonctionnalité d’image :</span><span class="sxs-lookup"><span data-stu-id="48eb0-154">The following image depicts web app experience of `selectMedia` API for image capability:</span></span>

![Expérience d’appareil photo et d’image dans Teams](../../assets/images/tabs/image-capability.png)

<span data-ttu-id="48eb0-156">L’image suivante illustre l’expérience d’application web de `selectMedia` l’API pour la fonctionnalité de microphone :</span><span class="sxs-lookup"><span data-stu-id="48eb0-156">The following image depicts web app experience of `selectMedia` API for microphone capability:</span></span>

![expérience d’application web pour la fonctionnalité de microphone](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a><span data-ttu-id="48eb0-158">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="48eb0-158">Error handling</span></span>

<span data-ttu-id="48eb0-159">Vous devez vous assurer de gérer ces erreurs de manière appropriée dans votre Teams application.</span><span class="sxs-lookup"><span data-stu-id="48eb0-159">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="48eb0-160">Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées :</span><span class="sxs-lookup"><span data-stu-id="48eb0-160">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="48eb0-161">Code d’erreur</span><span class="sxs-lookup"><span data-stu-id="48eb0-161">Error code</span></span> |  <span data-ttu-id="48eb0-162">Nom de l’erreur</span><span class="sxs-lookup"><span data-stu-id="48eb0-162">Error name</span></span>     | <span data-ttu-id="48eb0-163">Condition</span><span class="sxs-lookup"><span data-stu-id="48eb0-163">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="48eb0-164">**100**</span><span class="sxs-lookup"><span data-stu-id="48eb0-164">**100**</span></span> | <span data-ttu-id="48eb0-165">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="48eb0-165">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="48eb0-166">L’API n’est pas prise en charge sur la plateforme actuelle.</span><span class="sxs-lookup"><span data-stu-id="48eb0-166">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="48eb0-167">**404**</span><span class="sxs-lookup"><span data-stu-id="48eb0-167">**404**</span></span> | <span data-ttu-id="48eb0-168">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="48eb0-168">FILE_NOT_FOUND</span></span> | <span data-ttu-id="48eb0-169">Le fichier spécifié n’est pas trouvé à l’emplacement donné.</span><span class="sxs-lookup"><span data-stu-id="48eb0-169">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="48eb0-170">**500**</span><span class="sxs-lookup"><span data-stu-id="48eb0-170">**500**</span></span> | <span data-ttu-id="48eb0-171">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="48eb0-171">INTERNAL_ERROR</span></span> | <span data-ttu-id="48eb0-172">Une erreur interne est rencontrée lors de l’opération requise.</span><span class="sxs-lookup"><span data-stu-id="48eb0-172">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="48eb0-173">**1000**</span><span class="sxs-lookup"><span data-stu-id="48eb0-173">**1000**</span></span> | <span data-ttu-id="48eb0-174">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="48eb0-174">PERMISSION_DENIED</span></span> |<span data-ttu-id="48eb0-175">L’autorisation est refusée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48eb0-175">Permission is denied by the user.</span></span>|
| <span data-ttu-id="48eb0-176">**3000**</span><span class="sxs-lookup"><span data-stu-id="48eb0-176">**3000**</span></span> | <span data-ttu-id="48eb0-177">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="48eb0-177">NO_HW_SUPPORT</span></span> | <span data-ttu-id="48eb0-178">Le matériel sous-jacent ne prend pas en charge la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="48eb0-178">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="48eb0-179">**4000**</span><span class="sxs-lookup"><span data-stu-id="48eb0-179">**4000**</span></span>| <span data-ttu-id="48eb0-180">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="48eb0-180">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="48eb0-181">Un ou plusieurs arguments ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="48eb0-181">One or more arguments are invalid.</span></span>|
|  <span data-ttu-id="48eb0-182">**8000**</span><span class="sxs-lookup"><span data-stu-id="48eb0-182">**8000**</span></span> | <span data-ttu-id="48eb0-183">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="48eb0-183">USER_ABORT</span></span> |<span data-ttu-id="48eb0-184">L’utilisateur abandonne l’opération.</span><span class="sxs-lookup"><span data-stu-id="48eb0-184">User aborts the operation.</span></span>|
| <span data-ttu-id="48eb0-185">**9000**</span><span class="sxs-lookup"><span data-stu-id="48eb0-185">**9000**</span></span>| <span data-ttu-id="48eb0-186">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="48eb0-186">OLD_PLATFORM</span></span> | <span data-ttu-id="48eb0-187">Le code de plateforme est obsolète et n’implémente pas cette API.</span><span class="sxs-lookup"><span data-stu-id="48eb0-187">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="48eb0-188">**10000**</span><span class="sxs-lookup"><span data-stu-id="48eb0-188">**10000**</span></span>| <span data-ttu-id="48eb0-189">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="48eb0-189">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="48eb0-190">La valeur de retour est trop grande et a dépassé les limites de taille de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="48eb0-190">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="48eb0-191">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="48eb0-191">Code snippets</span></span>

<span data-ttu-id="48eb0-192">**Appel `selectMedia` API de** capture d’images à l’aide de l’appareil photo :</span><span class="sxs-lookup"><span data-stu-id="48eb0-192">**Calling `selectMedia` API** for capturing images using camera:</span></span>

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

<span data-ttu-id="48eb0-193">**Appel `getMedia` API permettant** de récupérer des médias de grande taille en blocs :</span><span class="sxs-lookup"><span data-stu-id="48eb0-193">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

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

<span data-ttu-id="48eb0-194">**Appel `viewImages` API par ID renvoyé par `selectMedia` l’API**:</span><span class="sxs-lookup"><span data-stu-id="48eb0-194">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

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

<span data-ttu-id="48eb0-195">**Appel `viewImages` API par URL**:</span><span class="sxs-lookup"><span data-stu-id="48eb0-195">**Calling `viewImages` API by URL**:</span></span>

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

<span data-ttu-id="48eb0-196">**Appel `selectMedia` et API pour `getMedia` l’enregistrement audio via le microphone**:</span><span class="sxs-lookup"><span data-stu-id="48eb0-196">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="48eb0-197">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="48eb0-197">See also</span></span>

* [<span data-ttu-id="48eb0-198">Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="48eb0-198">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="48eb0-199">Intégrer des fonctionnalités d’emplacement dans Teams</span><span class="sxs-lookup"><span data-stu-id="48eb0-199">Integrate location capabilities in Teams</span></span>](location-capability.md)
* [<span data-ttu-id="48eb0-200">Intégrer la fonctionnalité s’il s’Teams</span><span class="sxs-lookup"><span data-stu-id="48eb0-200">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)

