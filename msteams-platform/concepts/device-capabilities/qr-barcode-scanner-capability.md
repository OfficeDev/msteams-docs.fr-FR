---
title: Intégrer la fonctionnalité de scanneur QR ou code-barres
author: Rajeshwari-v
description: Comment utiliser le SDK client JavaScript teams pour tirer parti des fonctionnalités de QR ou de scanneur de code-barres
keywords: Fonctionnalités natives d'appareil photo qr code qrcode code-barres scanneur de scanneur de codes-barres
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: ede791a6cd566a0fc725a04e0b615ae1b8eeb0eb
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058340"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="819d7-104">Intégrer la fonctionnalité de scanneur QR ou code-barres</span><span class="sxs-lookup"><span data-stu-id="819d7-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="819d7-105">Ce document vous guide sur l'intégration de la fonctionnalité de QR ou de scanneur de code-barres.</span><span class="sxs-lookup"><span data-stu-id="819d7-105">This document guides you on how to integrate the QR or barcode scanner capability.</span></span> 

<span data-ttu-id="819d7-106">Le code-barres est une méthode de représentation des données sous forme visuelle et lisible par l'ordinateur.</span><span class="sxs-lookup"><span data-stu-id="819d7-106">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="819d7-107">Le code-barres contient des informations sur un produit, telles qu'un type, une taille, un fabricant et un pays d'origine sous la forme de barres et d'espaces.</span><span class="sxs-lookup"><span data-stu-id="819d7-107">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="819d7-108">Le code est lu à l'aide du scanneur optique sur votre appareil photo natif.</span><span class="sxs-lookup"><span data-stu-id="819d7-108">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="819d7-109">Pour une expérience de collaboration enrichie, vous pouvez intégrer la fonctionnalité de QR ou de scanneur de code-barres fournie dans la plateforme Teams avec votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="819d7-109">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span>   

<span data-ttu-id="819d7-110">Vous pouvez utiliser le [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit les outils nécessaires à votre application pour accéder aux fonctionnalités natives de l'appareil de l'utilisateur. [](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="819d7-110">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="819d7-111">Utilisez `scanBarCode` l'API pour intégrer la fonctionnalité de scanneur dans votre application.</span><span class="sxs-lookup"><span data-stu-id="819d7-111">Use the `scanBarCode` API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="819d7-112">Avantage de l'intégration des fonctionnalités de QR ou de scanneur de code-barres</span><span class="sxs-lookup"><span data-stu-id="819d7-112">Advantage of integrating QR or barcode scanner capability</span></span>

<span data-ttu-id="819d7-113">Voici les avantages de l'intégration des fonctionnalités de QR ou de scanneur de code-barres :</span><span class="sxs-lookup"><span data-stu-id="819d7-113">Following are the advantages of integration of QR or barcode scanner capabilities:</span></span> 

* <span data-ttu-id="819d7-114">L'intégration permet aux développeurs d'applications web sur la plateforme Teams de tirer parti des fonctionnalités d'analyse de QR ou de code-barres avec le SDK client JavaScript teams.</span><span class="sxs-lookup"><span data-stu-id="819d7-114">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="819d7-115">Avec cette fonctionnalité, l'utilisateur doit aligner uniquement une QR ou un code-barres dans un cadre au centre de l'interface utilisateur du scanneur et le code est analysé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="819d7-115">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="819d7-116">Les données stockées sont partagées avec l'application web d'appel.</span><span class="sxs-lookup"><span data-stu-id="819d7-116">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="819d7-117">Cela évite les désagréments et les erreurs humaines liés à la saisie manuelle de codes de produit longs ou d'autres informations pertinentes.</span><span class="sxs-lookup"><span data-stu-id="819d7-117">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="819d7-118">Pour intégrer la fonctionnalité de QR ou de scanneur de code-barres, vous devez mettre à jour le fichier manifeste de l'application et appeler `scanBarCode` l'API.</span><span class="sxs-lookup"><span data-stu-id="819d7-118">To integrate QR or barcode scanner capability, you must update the app manifest file and call the `scanBarCode` API.</span></span> <span data-ttu-id="819d7-119">Pour une intégration efficace, vous devez bien comprendre l'extrait de [code](#code-snippet) pour appeler l'API, ce qui vous permet d'utiliser la QR native ou la fonctionnalité de scanneur de `scanBarCode` code-barres.</span><span class="sxs-lookup"><span data-stu-id="819d7-119">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the `scanBarCode` API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="819d7-120">L'API fournit une erreur pour une norme de code-barres non pris en place.</span><span class="sxs-lookup"><span data-stu-id="819d7-120">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="819d7-121">Il est important de vous familiariser avec les erreurs de [réponse d'API](#error-handling) pour gérer les erreurs dans votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="819d7-121">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="819d7-122">Actuellement, la prise en charge de Microsoft Teams pour la QR ou la fonctionnalité de scanneur de code-barres est disponible uniquement pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="819d7-122">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="819d7-123">Mettre à jour le manifeste</span><span class="sxs-lookup"><span data-stu-id="819d7-123">Update manifest</span></span>

<span data-ttu-id="819d7-124">Mettez à jour votre application Teams [manifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la propriété et en `devicePermissions` spécifiant `media` .</span><span class="sxs-lookup"><span data-stu-id="819d7-124">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="819d7-125">Il permet à votre application de demander les autorisations requises aux utilisateurs avant qu'ils ne commencent à utiliser la fonctionnalité de QR ou de scanneur de code-barres.</span><span class="sxs-lookup"><span data-stu-id="819d7-125">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="819d7-126">**L'invite Demander des autorisations** s'affiche automatiquement lorsqu'une API Teams pertinente est lancée.</span><span class="sxs-lookup"><span data-stu-id="819d7-126">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="819d7-127">Pour plus d'informations, voir [Demander des autorisations d'appareil.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="819d7-127">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="819d7-128">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="819d7-128">ScanBarCode API</span></span>

<span data-ttu-id="819d7-129">L'API appelle le contrôle scanneur qui permet à l'utilisateur d'analyser différents types de codes-barres et renvoie le résultat sous forme `ScanBarCode` de chaîne.</span><span class="sxs-lookup"><span data-stu-id="819d7-129">The `ScanBarCode` API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="819d7-130">Pour personnaliser l'expérience d'analyse du code-barres, la configuration facultative du code-barres est transmise en tant qu'entrée à `ScanBarCode` l'API.</span><span class="sxs-lookup"><span data-stu-id="819d7-130">To customize the barcode scanning experience, optional barcode configuration is passed as input to `ScanBarCode` API.</span></span> <span data-ttu-id="819d7-131">Vous pouvez spécifier l'intervalle de délai d'analyse en secondes à l'aide `timeOutIntervalInSec` de .</span><span class="sxs-lookup"><span data-stu-id="819d7-131">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="819d7-132">Sa valeur par défaut est 30 secondes et la valeur maximale est de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="819d7-132">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="819d7-133">**L'API scanBarCode()** prend en charge les types de codes-barres suivants :</span><span class="sxs-lookup"><span data-stu-id="819d7-133">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="819d7-134">Type de code-barres</span><span class="sxs-lookup"><span data-stu-id="819d7-134">Barcode Type</span></span> | <span data-ttu-id="819d7-135">Pris en charge sur Android</span><span class="sxs-lookup"><span data-stu-id="819d7-135">Supported on Android</span></span> | <span data-ttu-id="819d7-136">Pris en charge sur iOS</span><span class="sxs-lookup"><span data-stu-id="819d7-136">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="819d7-137">Barre de code</span><span class="sxs-lookup"><span data-stu-id="819d7-137">Codebar</span></span> | <span data-ttu-id="819d7-138">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-138">Yes</span></span> | <span data-ttu-id="819d7-139">Non</span><span class="sxs-lookup"><span data-stu-id="819d7-139">No</span></span> |
| <span data-ttu-id="819d7-140">Code 39</span><span class="sxs-lookup"><span data-stu-id="819d7-140">Code 39</span></span> | <span data-ttu-id="819d7-141">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-141">Yes</span></span> | <span data-ttu-id="819d7-142">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-142">Yes</span></span> | 
| <span data-ttu-id="819d7-143">Code 93</span><span class="sxs-lookup"><span data-stu-id="819d7-143">Code 93</span></span> | <span data-ttu-id="819d7-144">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-144">Yes</span></span> | <span data-ttu-id="819d7-145">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-145">Yes</span></span> |
| <span data-ttu-id="819d7-146">Code 128</span><span class="sxs-lookup"><span data-stu-id="819d7-146">Code 128</span></span> | <span data-ttu-id="819d7-147">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-147">Yes</span></span> | <span data-ttu-id="819d7-148">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-148">Yes</span></span> |
| <span data-ttu-id="819d7-149">EAN-13</span><span class="sxs-lookup"><span data-stu-id="819d7-149">EAN-13</span></span> | <span data-ttu-id="819d7-150">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-150">Yes</span></span> | <span data-ttu-id="819d7-151">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-151">Yes</span></span> |
| <span data-ttu-id="819d7-152">EAN-8</span><span class="sxs-lookup"><span data-stu-id="819d7-152">EAN-8</span></span> | <span data-ttu-id="819d7-153">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-153">Yes</span></span> | <span data-ttu-id="819d7-154">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-154">Yes</span></span> |
| <span data-ttu-id="819d7-155">ITF</span><span class="sxs-lookup"><span data-stu-id="819d7-155">ITF</span></span> | <span data-ttu-id="819d7-156">Non</span><span class="sxs-lookup"><span data-stu-id="819d7-156">No</span></span> | <span data-ttu-id="819d7-157">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-157">Yes</span></span> |
| <span data-ttu-id="819d7-158">QR Code</span><span class="sxs-lookup"><span data-stu-id="819d7-158">QR Code</span></span> | <span data-ttu-id="819d7-159">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-159">Yes</span></span> | <span data-ttu-id="819d7-160">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-160">Yes</span></span> |
| <span data-ttu-id="819d7-161">RSS étendu</span><span class="sxs-lookup"><span data-stu-id="819d7-161">RSS Expanded</span></span> | <span data-ttu-id="819d7-162">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-162">Yes</span></span> | <span data-ttu-id="819d7-163">Non</span><span class="sxs-lookup"><span data-stu-id="819d7-163">No</span></span> |
| <span data-ttu-id="819d7-164">RSS-14</span><span class="sxs-lookup"><span data-stu-id="819d7-164">RSS-14</span></span> | <span data-ttu-id="819d7-165">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-165">Yes</span></span> | <span data-ttu-id="819d7-166">Non</span><span class="sxs-lookup"><span data-stu-id="819d7-166">No</span></span> |
| <span data-ttu-id="819d7-167">UPC-A</span><span class="sxs-lookup"><span data-stu-id="819d7-167">UPC-A</span></span> | <span data-ttu-id="819d7-168">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-168">Yes</span></span> | <span data-ttu-id="819d7-169">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-169">Yes</span></span> |
| <span data-ttu-id="819d7-170">UPC-E</span><span class="sxs-lookup"><span data-stu-id="819d7-170">UPC-E</span></span> | <span data-ttu-id="819d7-171">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-171">Yes</span></span> | <span data-ttu-id="819d7-172">Oui</span><span class="sxs-lookup"><span data-stu-id="819d7-172">Yes</span></span> |

<span data-ttu-id="819d7-173">**Expérience d'application web pour `ScanBarCode` API pour l'expérience d'application** web QR ou de scanneur de code-barres pour la 
 ![ fonctionnalité de scanneur de code-barres ou qr](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span><span class="sxs-lookup"><span data-stu-id="819d7-173">**Web app experience for `ScanBarCode` API for QR or barcode scanner capability**
![web app experience for qr or barcode scanner capability](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="819d7-174">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="819d7-174">Error handling</span></span>

<span data-ttu-id="819d7-175">Vous devez veiller à gérer ces erreurs de manière appropriée dans votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="819d7-175">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="819d7-176">Le tableau suivant répertorie les codes d'erreur et les conditions dans lesquelles les erreurs sont générées :</span><span class="sxs-lookup"><span data-stu-id="819d7-176">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="819d7-177">Code d’erreur</span><span class="sxs-lookup"><span data-stu-id="819d7-177">Error code</span></span> |  <span data-ttu-id="819d7-178">Nom de l'erreur</span><span class="sxs-lookup"><span data-stu-id="819d7-178">Error name</span></span>     | <span data-ttu-id="819d7-179">Condition</span><span class="sxs-lookup"><span data-stu-id="819d7-179">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="819d7-180">**100**</span><span class="sxs-lookup"><span data-stu-id="819d7-180">**100**</span></span> | <span data-ttu-id="819d7-181">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="819d7-181">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="819d7-182">L'API n'est pas prise en charge sur la plateforme actuelle.</span><span class="sxs-lookup"><span data-stu-id="819d7-182">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="819d7-183">**500**</span><span class="sxs-lookup"><span data-stu-id="819d7-183">**500**</span></span> | <span data-ttu-id="819d7-184">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="819d7-184">INTERNAL_ERROR</span></span> | <span data-ttu-id="819d7-185">Une erreur interne est rencontrée lors de l'opération requise.</span><span class="sxs-lookup"><span data-stu-id="819d7-185">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="819d7-186">**1000**</span><span class="sxs-lookup"><span data-stu-id="819d7-186">**1000**</span></span> | <span data-ttu-id="819d7-187">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="819d7-187">PERMISSION_DENIED</span></span> |<span data-ttu-id="819d7-188">L'autorisation est refusée par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="819d7-188">Permission is denied by the user.</span></span>|
| <span data-ttu-id="819d7-189">**3000**</span><span class="sxs-lookup"><span data-stu-id="819d7-189">**3000**</span></span> | <span data-ttu-id="819d7-190">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="819d7-190">NO_HW_SUPPORT</span></span> | <span data-ttu-id="819d7-191">Le matériel sous-jacent ne prend pas en charge la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="819d7-191">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="819d7-192">**4000**</span><span class="sxs-lookup"><span data-stu-id="819d7-192">**4000**</span></span> | <span data-ttu-id="819d7-193">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="819d7-193">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="819d7-194">Un ou plusieurs arguments ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="819d7-194">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="819d7-195">**8000**</span><span class="sxs-lookup"><span data-stu-id="819d7-195">**8000**</span></span> | <span data-ttu-id="819d7-196">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="819d7-196">USER_ABORT</span></span> |<span data-ttu-id="819d7-197">L'utilisateur abandonne l'opération.</span><span class="sxs-lookup"><span data-stu-id="819d7-197">User aborts the operation.</span></span>|
| <span data-ttu-id="819d7-198">**8001**</span><span class="sxs-lookup"><span data-stu-id="819d7-198">**8001**</span></span> | <span data-ttu-id="819d7-199">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="819d7-199">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="819d7-200">Nous n'avons pas pu détecter le code-barres dans l'intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="819d7-200">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="819d7-201">**9000**</span><span class="sxs-lookup"><span data-stu-id="819d7-201">**9000**</span></span> | <span data-ttu-id="819d7-202">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="819d7-202">OLD_PLATFORM</span></span> | <span data-ttu-id="819d7-203">Le code de plateforme est obsolète et n'implémente pas cette API.</span><span class="sxs-lookup"><span data-stu-id="819d7-203">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="819d7-204">Extrait de code</span><span class="sxs-lookup"><span data-stu-id="819d7-204">Code snippet</span></span>

<span data-ttu-id="819d7-205">**Appel `ScanBarCode()` API pour** analyser la QR ou le code-barres à l'aide de l'appareil photo :</span><span class="sxs-lookup"><span data-stu-id="819d7-205">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

```javascript
const config: microsoftTeams.media.BarCodeConfig = {
  timeOutIntervalInSec: 30};
microsoftTeams.media.scanBarCode((error: microsoftTeams.SdkError, decodedText: string) => {
  if (error) {
    if (error.message) {
      output(" ErrorCode: " + error.errorCode + error.message);
    } else {
      output(" ErrorCode: " + error.errorCode);
    }
  } else if (decodedText) {
    output(decodedText);
  }
}, config);
```

## <a name="see-also"></a><span data-ttu-id="819d7-206">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="819d7-206">See also</span></span>

- [<span data-ttu-id="819d7-207">Intégrer des fonctionnalités multimédias dans Teams</span><span class="sxs-lookup"><span data-stu-id="819d7-207">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

- [<span data-ttu-id="819d7-208">Intégrer des fonctionnalités d'emplacement dans Teams</span><span class="sxs-lookup"><span data-stu-id="819d7-208">Integrate location capabilities in Teams</span></span>](location-capability.md)
