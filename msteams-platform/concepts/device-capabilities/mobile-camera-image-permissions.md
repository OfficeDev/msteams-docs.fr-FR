---
title: Intégrer les fonctionnalités médias
author: Rajeshwari-v
description: Utilisation du SDK Teams client JavaScript pour activer les fonctionnalités multimédias
keywords: Média d’autorisations d’appareil natif des fonctionnalités du microphone d’image de l’appareil photo
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: e2d3c6e4b9e80d5b09cf597a29e7f3ba67355715
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994377"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="5937a-104">Intégrer les fonctionnalités médias</span><span class="sxs-lookup"><span data-stu-id="5937a-104">Integrate media capabilities</span></span> 

<span data-ttu-id="5937a-105">Ce document vous guide sur l’intégration des fonctionnalités multimédias.</span><span class="sxs-lookup"><span data-stu-id="5937a-105">This document guides you on how to integrate media capabilities.</span></span> <span data-ttu-id="5937a-106">Cette intégration associe les fonctionnalités natives  de l’appareil, telles que la caméra et le **microphone,** à la plateforme Teams réseau.</span><span class="sxs-lookup"><span data-stu-id="5937a-106">This integration combines the native device capabilities, such as the **camera** and **microphone** with the Teams platform.</span></span>  

<span data-ttu-id="5937a-107">Vous pouvez utiliser [Microsoft Teams SDK client JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit les outils nécessaires pour que votre application accède aux autorisations d’appareil d’un [utilisateur.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="5937a-107">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="5937a-108">Utilisez les API de fonctionnalité multimédia appropriées pour intégrer  les fonctionnalités natives de l’appareil, telles que l’appareil photo et le **microphone,** à la plateforme Teams dans votre application mobile Microsoft Teams, et créez une expérience plus riche.</span><span class="sxs-lookup"><span data-stu-id="5937a-108">Use suitable  media capability APIs to integrate the native device capabilities, such as the **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="5937a-109">Avantage de l’intégration des fonctionnalités multimédias</span><span class="sxs-lookup"><span data-stu-id="5937a-109">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="5937a-110">Le principal avantage de l’intégration des fonctionnalités d’appareil dans vos applications Teams est qu’il tire parti des contrôles Teams natifs pour offrir une expérience riche et immersive à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5937a-110">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="5937a-111">Pour intégrer des fonctionnalités multimédias, vous devez mettre à jour le fichier manifeste de l’application et appeler les API de fonctionnalité multimédia.</span><span class="sxs-lookup"><span data-stu-id="5937a-111">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="5937a-112">Pour une intégration efficace, vous devez bien comprendre les extraits de [code](#code-snippets) pour appeler les API respectives, ce qui vous permet d’utiliser les fonctionnalités multimédias natives.</span><span class="sxs-lookup"><span data-stu-id="5937a-112">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="5937a-113">Il est important de vous familiariser avec les erreurs de réponse [d’API](#error-handling) pour gérer les erreurs dans votre Teams application.</span><span class="sxs-lookup"><span data-stu-id="5937a-113">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> * <span data-ttu-id="5937a-114">Actuellement, Microsoft Teams prise en charge des fonctionnalités multimédias est disponible uniquement pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="5937a-114">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>    
> * <span data-ttu-id="5937a-115">Actuellement, Teams ne prend pas en charge les autorisations d’appareil pour les applications à fenêtres multiples, les onglets et le bureau secondaire de la réunion.</span><span class="sxs-lookup"><span data-stu-id="5937a-115">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span> 

## <a name="update-manifest"></a><span data-ttu-id="5937a-116">Mettre à jour le manifeste</span><span class="sxs-lookup"><span data-stu-id="5937a-116">Update manifest</span></span>

<span data-ttu-id="5937a-117">Mettez à jour [Teams’applicationmanifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la `devicePermissions` propriété et en spécifiant `media` .</span><span class="sxs-lookup"><span data-stu-id="5937a-117">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="5937a-118">Il permet à votre application de demander les autorisations  requises aux utilisateurs avant de commencer à utiliser l’appareil photo pour capturer l’image, d’ouvrir la galerie pour sélectionner une image à soumettre en pièce jointe ou d’utiliser le **microphone** pour enregistrer la conversation.</span><span class="sxs-lookup"><span data-stu-id="5937a-118">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="5937a-119">**L’invite Demander des autorisations** s’affiche automatiquement lorsqu’une API Teams est lancée.</span><span class="sxs-lookup"><span data-stu-id="5937a-119">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="5937a-120">Pour plus d’informations, voir [Demander des autorisations d’appareil.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="5937a-120">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="5937a-121">API de fonctionnalité multimédia</span><span class="sxs-lookup"><span data-stu-id="5937a-121">Media capability APIs</span></span>

<span data-ttu-id="5937a-122">Les [API selectMedia,](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)et [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) vous permettent d’utiliser les fonctionnalités multimédias natives comme suit :</span><span class="sxs-lookup"><span data-stu-id="5937a-122">The [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="5937a-123">Utilisez le **microphone natif pour** permettre aux utilisateurs d’enregistrer du contenu **audio** (enregistrer 10 minutes de conversation) à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="5937a-123">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="5937a-124">Utilisez le contrôle **d’appareil photo natif** pour permettre aux utilisateurs de **capturer et d’attacher** des images en mouvement.</span><span class="sxs-lookup"><span data-stu-id="5937a-124">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="5937a-125">Utilisez la prise **en charge de la galerie native** pour permettre aux utilisateurs de sélectionner des images **d’appareil** en tant que pièces jointes.</span><span class="sxs-lookup"><span data-stu-id="5937a-125">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="5937a-126">Utilisez le contrôle **visionneuse d’images natives** **pour afficher un aperçu de plusieurs images** à la fois.</span><span class="sxs-lookup"><span data-stu-id="5937a-126">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="5937a-127">Prise **en charge du transfert d’images** de grande taille (de 1 Mo à 50 Mo) via le pont du SDK.</span><span class="sxs-lookup"><span data-stu-id="5937a-127">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="5937a-128">Prise en **charge des fonctionnalités d’image avancées** permettant aux utilisateurs d’afficher un aperçu et de modifier des images :</span><span class="sxs-lookup"><span data-stu-id="5937a-128">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="5937a-129">Analysez le document, le tableau blanc et les cartes de visite par le biais de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="5937a-129">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
> * <span data-ttu-id="5937a-130">Les API , et les API peuvent être appelés à partir de plusieurs surfaces Teams, telles que les modules de tâche, les onglets et `selectMedia` `getMedia` les applications `viewImages` personnelles.</span><span class="sxs-lookup"><span data-stu-id="5937a-130">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces, such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="5937a-131">Pour plus d’informations, voir [Points d’entrée Teams applications.](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="5937a-131">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
> * <span data-ttu-id="5937a-132">`selectMedia` L’API a été étendue pour prendre en charge les propriétés de microphone et audio.</span><span class="sxs-lookup"><span data-stu-id="5937a-132">`selectMedia` API has been extended to support microphone and audio properties.</span></span>

<span data-ttu-id="5937a-133">Vous devez utiliser l’ensemble d’API suivant pour activer les fonctionnalités multimédias de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="5937a-133">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="5937a-134">API</span><span class="sxs-lookup"><span data-stu-id="5937a-134">API</span></span>      | <span data-ttu-id="5937a-135">Description</span><span class="sxs-lookup"><span data-stu-id="5937a-135">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="5937a-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Appareil photo)**</span><span class="sxs-lookup"><span data-stu-id="5937a-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="5937a-137">Cette API permet aux utilisateurs de capturer ou de sélectionner **du contenu multimédia** à partir de l’appareil photo de l’appareil et de le renvoyer à l’application web.</span><span class="sxs-lookup"><span data-stu-id="5937a-137">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="5937a-138">Les utilisateurs peuvent modifier, rogner, faire pivoter, annoter ou dessiner sur des images avant l’envoi.</span><span class="sxs-lookup"><span data-stu-id="5937a-138">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="5937a-139">En réponse à , l’application web reçoit les ID multimédias des images sélectionnées et une miniature du `selectMedia` média sélectionné.</span><span class="sxs-lookup"><span data-stu-id="5937a-139">In response to `selectMedia`, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="5937a-140">Cette API peut être configurée davantage via la configuration [ImageProps.](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5937a-140">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="5937a-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span><span class="sxs-lookup"><span data-stu-id="5937a-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="5937a-142">Définissez [mediaType sur](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) `4` dans `selectMedia` l’API pour accéder à la fonctionnalité microphone.</span><span class="sxs-lookup"><span data-stu-id="5937a-142">Set the [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in `selectMedia` API for accessing microphone  capability.</span></span> <span data-ttu-id="5937a-143">Cette API permet également aux utilisateurs d’enregistrer du contenu audio à partir du microphone de l’appareil et de renvoyer des clips enregistrés à l’application web.</span><span class="sxs-lookup"><span data-stu-id="5937a-143">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="5937a-144">Les utilisateurs peuvent suspendre, ré-enregistrer et lire l’aperçu de l’enregistrement avant la soumission.</span><span class="sxs-lookup"><span data-stu-id="5937a-144">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="5937a-145">En réponse à **selectMedia,** l’application web reçoit les ID multimédias de l’enregistrement audio sélectionné.</span><span class="sxs-lookup"><span data-stu-id="5937a-145">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="5937a-146">Utilisez `maxDuration` , si vous avez besoin de configurer une durée en minutes pour l’enregistrement de la conversation.</span><span class="sxs-lookup"><span data-stu-id="5937a-146">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="5937a-147">La durée actuelle de l’enregistrement est de 10 minutes, après quoi l’enregistrement se termine.</span><span class="sxs-lookup"><span data-stu-id="5937a-147">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="5937a-148">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="5937a-148">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="5937a-149">Cette API récupère le média capturé par l’API en blocs, quelle que `selectMedia` soit la taille du média.</span><span class="sxs-lookup"><span data-stu-id="5937a-149">This API retrieves the media captured by `selectMedia` API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="5937a-150">Ces blocs sont assemblés et renvoyés à l’application web en tant que fichier ou blob.</span><span class="sxs-lookup"><span data-stu-id="5937a-150">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="5937a-151">La rupture du média en blocs plus petits facilite le transfert de fichiers de grande taille.</span><span class="sxs-lookup"><span data-stu-id="5937a-151">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="5937a-152">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="5937a-152">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="5937a-153">Cette API permet à l’utilisateur d’afficher des images en mode plein écran en tant que liste de défilement.</span><span class="sxs-lookup"><span data-stu-id="5937a-153">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|


<span data-ttu-id="5937a-154">**Expérience d’application web pour l’API selectMedia pour la fonctionnalité d’image** 
 ![ Expérience d’appareil photo et d’image dans Teams](../../assets/images/tabs/image-capability.png)</span><span class="sxs-lookup"><span data-stu-id="5937a-154">**Web app experience for selectMedia API for image capability**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability.png)</span></span>

<span data-ttu-id="5937a-155">**Expérience d’application web pour l’API selectMedia pour la fonctionnalité de microphone** 
 ![ expérience d’application web pour la fonctionnalité de microphone](../../assets/images/tabs/microphone-capability.png)</span><span class="sxs-lookup"><span data-stu-id="5937a-155">**Web app experience for selectMedia API for microphone capability**
![web app experience for microphone capability](../../assets/images/tabs/microphone-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="5937a-156">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="5937a-156">Error handling</span></span>

<span data-ttu-id="5937a-157">Vous devez vous assurer de gérer ces erreurs de manière appropriée dans votre Teams application.</span><span class="sxs-lookup"><span data-stu-id="5937a-157">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="5937a-158">Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées :</span><span class="sxs-lookup"><span data-stu-id="5937a-158">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 


|<span data-ttu-id="5937a-159">Code d’erreur</span><span class="sxs-lookup"><span data-stu-id="5937a-159">Error code</span></span> |  <span data-ttu-id="5937a-160">Nom de l’erreur</span><span class="sxs-lookup"><span data-stu-id="5937a-160">Error name</span></span>     | <span data-ttu-id="5937a-161">Condition</span><span class="sxs-lookup"><span data-stu-id="5937a-161">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="5937a-162">**100**</span><span class="sxs-lookup"><span data-stu-id="5937a-162">**100**</span></span> | <span data-ttu-id="5937a-163">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="5937a-163">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="5937a-164">L’API n’est pas prise en charge sur la plateforme actuelle.</span><span class="sxs-lookup"><span data-stu-id="5937a-164">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="5937a-165">**404**</span><span class="sxs-lookup"><span data-stu-id="5937a-165">**404**</span></span> | <span data-ttu-id="5937a-166">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="5937a-166">FILE_NOT_FOUND</span></span> | <span data-ttu-id="5937a-167">Le fichier spécifié n’est pas trouvé à l’emplacement donné.</span><span class="sxs-lookup"><span data-stu-id="5937a-167">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="5937a-168">**500**</span><span class="sxs-lookup"><span data-stu-id="5937a-168">**500**</span></span> | <span data-ttu-id="5937a-169">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="5937a-169">INTERNAL_ERROR</span></span> | <span data-ttu-id="5937a-170">Une erreur interne est rencontrée lors de l’opération requise.</span><span class="sxs-lookup"><span data-stu-id="5937a-170">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="5937a-171">**1000**</span><span class="sxs-lookup"><span data-stu-id="5937a-171">**1000**</span></span> | <span data-ttu-id="5937a-172">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="5937a-172">PERMISSION_DENIED</span></span> |<span data-ttu-id="5937a-173">L’autorisation est refusée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5937a-173">Permission is denied by the user.</span></span>|
| <span data-ttu-id="5937a-174">**2000**</span><span class="sxs-lookup"><span data-stu-id="5937a-174">**2000**</span></span> |<span data-ttu-id="5937a-175">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="5937a-175">NETWORK_ERROR</span></span> | <span data-ttu-id="5937a-176">Problème réseau.</span><span class="sxs-lookup"><span data-stu-id="5937a-176">Network issue.</span></span>|
| <span data-ttu-id="5937a-177">**3000**</span><span class="sxs-lookup"><span data-stu-id="5937a-177">**3000**</span></span> | <span data-ttu-id="5937a-178">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="5937a-178">NO_HW_SUPPORT</span></span> | <span data-ttu-id="5937a-179">Le matériel sous-jacent ne prend pas en charge la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5937a-179">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="5937a-180">**4000**</span><span class="sxs-lookup"><span data-stu-id="5937a-180">**4000**</span></span>| <span data-ttu-id="5937a-181">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="5937a-181">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="5937a-182">Un ou plusieurs arguments ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="5937a-182">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="5937a-183">**5000**</span><span class="sxs-lookup"><span data-stu-id="5937a-183">**5000**</span></span> | <span data-ttu-id="5937a-184">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="5937a-184">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="5937a-185">L’utilisateur n’est pas autorisé à effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="5937a-185">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="5937a-186">**6000**</span><span class="sxs-lookup"><span data-stu-id="5937a-186">**6000**</span></span> |<span data-ttu-id="5937a-187">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="5937a-187">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="5937a-188">L’opération n’a pas pu être achevée en raison de ressources insuffisantes.</span><span class="sxs-lookup"><span data-stu-id="5937a-188">Operation could not be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="5937a-189">**7000**</span><span class="sxs-lookup"><span data-stu-id="5937a-189">**7000**</span></span> | <span data-ttu-id="5937a-190">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="5937a-190">THROTTLE</span></span> | <span data-ttu-id="5937a-191">La plateforme a limitée la demande car l’API a été fréquemment invoquée.</span><span class="sxs-lookup"><span data-stu-id="5937a-191">Platform throttled the request as the API was invoked frequently.</span></span>|
|  <span data-ttu-id="5937a-192">**8000**</span><span class="sxs-lookup"><span data-stu-id="5937a-192">**8000**</span></span> | <span data-ttu-id="5937a-193">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="5937a-193">USER_ABORT</span></span> |<span data-ttu-id="5937a-194">L’utilisateur abandonne l’opération.</span><span class="sxs-lookup"><span data-stu-id="5937a-194">User aborts the operation.</span></span>|
| <span data-ttu-id="5937a-195">**9000**</span><span class="sxs-lookup"><span data-stu-id="5937a-195">**9000**</span></span>| <span data-ttu-id="5937a-196">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="5937a-196">OLD_PLATFORM</span></span> | <span data-ttu-id="5937a-197">Le code de plateforme est obsolète et n’implémente pas cette API.</span><span class="sxs-lookup"><span data-stu-id="5937a-197">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="5937a-198">**10000**</span><span class="sxs-lookup"><span data-stu-id="5937a-198">**10000**</span></span>| <span data-ttu-id="5937a-199">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="5937a-199">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="5937a-200">La valeur de retour est trop grande et a dépassé les limites de taille de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="5937a-200">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="5937a-201">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="5937a-201">Code snippets</span></span>

<span data-ttu-id="5937a-202">**Appel `selectMedia` API de** capture d’images à l’aide de l’appareil photo :</span><span class="sxs-lookup"><span data-stu-id="5937a-202">**Calling `selectMedia` API** for capturing images using camera:</span></span>

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

<span data-ttu-id="5937a-203">**Appel `getMedia` API permettant** de récupérer des médias de grande taille en blocs :</span><span class="sxs-lookup"><span data-stu-id="5937a-203">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

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

<span data-ttu-id="5937a-204">**Appel `viewImages` API par ID renvoyé par `selectMedia` l’API**:</span><span class="sxs-lookup"><span data-stu-id="5937a-204">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

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

<span data-ttu-id="5937a-205">**Appel `viewImages` API par URL**:</span><span class="sxs-lookup"><span data-stu-id="5937a-205">**Calling `viewImages` API by URL**:</span></span>

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

<span data-ttu-id="5937a-206">**Appel `selectMedia` et API pour `getMedia` l’enregistrement audio via le microphone**:</span><span class="sxs-lookup"><span data-stu-id="5937a-206">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="5937a-207">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5937a-207">See also</span></span>

* [<span data-ttu-id="5937a-208">Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="5937a-208">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="5937a-209">Intégrer des fonctionnalités d’emplacement dans Teams</span><span class="sxs-lookup"><span data-stu-id="5937a-209">Integrate location capabilities in Teams</span></span>](location-capability.md)
