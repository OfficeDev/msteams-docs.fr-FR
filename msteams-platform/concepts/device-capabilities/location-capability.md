---
title: Intégrer les fonctionnalités d’emplacement
description: Comment utiliser le SDK client JavaScript teams pour tirer parti des fonctionnalités d’emplacement
keywords: autorisations natives d’appareil pour les fonctionnalités de carte d’emplacement
ms.author: lajanuar
ms.openlocfilehash: b941080eaece2cd2346bfa046ae97f855195ff20
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596195"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="3edac-104">Intégrer les fonctionnalités d’emplacement</span><span class="sxs-lookup"><span data-stu-id="3edac-104">Integrate location capabilities</span></span> 

<span data-ttu-id="3edac-105">Ce document vous guide sur l’intégration des fonctionnalités d’emplacement de l’appareil natif à votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="3edac-105">This document guides you on how to integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="3edac-106">Vous pouvez utiliser le [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit les outils nécessaires à votre application pour accéder aux fonctionnalités natives de l’appareil de l’utilisateur. [](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="3edac-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="3edac-107">Utilisez les API d’emplacement, telles [que getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) et [showLocation,](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) pour intégrer les fonctionnalités dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3edac-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="3edac-108">Avantages de l’intégration des fonctionnalités d’emplacement</span><span class="sxs-lookup"><span data-stu-id="3edac-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="3edac-109">Le principal avantage de l’intégration des fonctionnalités d’emplacement dans vos applications Teams est qu’elle permet aux développeurs d’applications web sur la plateforme Teams d’utiliser la fonctionnalité d’emplacement avec le SDK client JavaScript Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3edac-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="3edac-110">Les exemples suivants montrent comment l’intégration des fonctionnalités d’emplacement est utilisée dans différents scénarios :</span><span class="sxs-lookup"><span data-stu-id="3edac-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="3edac-111">Dans une usine, le responsable peut suivre la présence des employés en leur demandant de prendre un selfie à proximité de l’usine et de le partager via l’application spécifiée.</span><span class="sxs-lookup"><span data-stu-id="3edac-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="3edac-112">Les données d’emplacement sont également capturées et envoyées avec l’image.</span><span class="sxs-lookup"><span data-stu-id="3edac-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="3edac-113">Les fonctionnalités d’emplacement permettent au personnel de maintenance d’un fournisseur de services de partager des données d’état d’état authentiques des pylônes cellulaires avec la direction.</span><span class="sxs-lookup"><span data-stu-id="3edac-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="3edac-114">La direction peut comparer les différences entre les informations d’emplacement capturées et les données envoyées par le personnel de maintenance.</span><span class="sxs-lookup"><span data-stu-id="3edac-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="3edac-115">Pour intégrer des fonctionnalités d’emplacement, vous devez mettre à jour le fichier manifeste de l’application et appeler les API.</span><span class="sxs-lookup"><span data-stu-id="3edac-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="3edac-116">Pour une intégration efficace, vous devez bien comprendre les [extraits](#code-snippets) de code pour appeler les API d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="3edac-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="3edac-117">Il est important de vous familiariser avec les erreurs de [réponse d’API](#error-handling) pour gérer les erreurs dans votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="3edac-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="3edac-118">Actuellement, la prise en charge des fonctionnalités de localisation par Microsoft Teams est disponible uniquement pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="3edac-118">Currently, Microsoft Teams support for location capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="3edac-119">Mettre à jour le manifeste</span><span class="sxs-lookup"><span data-stu-id="3edac-119">Update manifest</span></span>

<span data-ttu-id="3edac-120">Mettez à jour votre application Teams [manifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la propriété et en `devicePermissions` spécifiant `geolocation` .</span><span class="sxs-lookup"><span data-stu-id="3edac-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="3edac-121">Il permet à votre application de demander les autorisations requises aux utilisateurs avant de commencer à utiliser les fonctionnalités de localisation.</span><span class="sxs-lookup"><span data-stu-id="3edac-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="3edac-122">**L’invite Demander des autorisations** s’affiche automatiquement lorsqu’une API Teams pertinente est lancée.</span><span class="sxs-lookup"><span data-stu-id="3edac-122">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="3edac-123">Pour plus d’informations, voir [demander des autorisations d’appareil.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="3edac-123">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="3edac-124">API d’emplacement</span><span class="sxs-lookup"><span data-stu-id="3edac-124">Location APIs</span></span>

<span data-ttu-id="3edac-125">Vous devez utiliser l’ensemble d’API suivant pour activer les fonctionnalités d’emplacement de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="3edac-125">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="3edac-126">API</span><span class="sxs-lookup"><span data-stu-id="3edac-126">API</span></span>      | <span data-ttu-id="3edac-127">Description</span><span class="sxs-lookup"><span data-stu-id="3edac-127">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="3edac-128">getLocation</span><span class="sxs-lookup"><span data-stu-id="3edac-128">getLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="3edac-129">Fournit l’emplacement actuel de l’appareil de l’utilisateur ou ouvre le s picker d’emplacement natif et renvoie l’emplacement choisi par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3edac-129">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="3edac-130">showLocation</span><span class="sxs-lookup"><span data-stu-id="3edac-130">showLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | <span data-ttu-id="3edac-131">Affiche l’emplacement sur la carte</span><span class="sxs-lookup"><span data-stu-id="3edac-131">Shows location on map</span></span> |

> [!NOTE]

> <span data-ttu-id="3edac-132">`getLocation()`L’API est livré avec les [configurations d’entrée suivantes](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)et `allowChooseLocation` `showMap` .</span><span class="sxs-lookup"><span data-stu-id="3edac-132">The `getLocation()` API comes along with following [input configurations](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="3edac-133">Si la valeur est `allowChooseLocation` *true,* les utilisateurs peuvent choisir n’importe quel emplacement de leur choix.</span><span class="sxs-lookup"><span data-stu-id="3edac-133">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="3edac-134">Si la valeur est *false,* les utilisateurs ne peuvent pas modifier leur emplacement actuel.</span><span class="sxs-lookup"><span data-stu-id="3edac-134">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="3edac-135">Si la valeur est `showMap` *false,* l’emplacement actuel est récupéré sans afficher la carte.</span><span class="sxs-lookup"><span data-stu-id="3edac-135">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="3edac-136">`showMap` est ignoré si `allowChooseLocation` est définie sur *true*.</span><span class="sxs-lookup"><span data-stu-id="3edac-136">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span> 


<span data-ttu-id="3edac-137">**Expérience d’application web pour les fonctionnalités de localisation** 
 ![ expérience d’application web pour les fonctionnalités de localisation](../../assets/images/tabs/location-capability.png)</span><span class="sxs-lookup"><span data-stu-id="3edac-137">**Web app experience for location capabilities**
![web app experience for location capabilities](../../assets/images/tabs/location-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="3edac-138">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="3edac-138">Error handling</span></span>

<span data-ttu-id="3edac-139">Vous devez veiller à gérer ces erreurs de manière appropriée dans votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="3edac-139">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="3edac-140">Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées :</span><span class="sxs-lookup"><span data-stu-id="3edac-140">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="3edac-141">Code d’erreur</span><span class="sxs-lookup"><span data-stu-id="3edac-141">Error code</span></span> |  <span data-ttu-id="3edac-142">Nom de l’erreur</span><span class="sxs-lookup"><span data-stu-id="3edac-142">Error name</span></span>     | <span data-ttu-id="3edac-143">Condition</span><span class="sxs-lookup"><span data-stu-id="3edac-143">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="3edac-144">**100**</span><span class="sxs-lookup"><span data-stu-id="3edac-144">**100**</span></span> | <span data-ttu-id="3edac-145">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="3edac-145">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="3edac-146">L’API n’est pas prise en charge sur la plateforme actuelle.</span><span class="sxs-lookup"><span data-stu-id="3edac-146">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="3edac-147">**500**</span><span class="sxs-lookup"><span data-stu-id="3edac-147">**500**</span></span> | <span data-ttu-id="3edac-148">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="3edac-148">INTERNAL_ERROR</span></span> | <span data-ttu-id="3edac-149">Une erreur interne est rencontrée lors de l’opération requise.</span><span class="sxs-lookup"><span data-stu-id="3edac-149">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="3edac-150">**1000**</span><span class="sxs-lookup"><span data-stu-id="3edac-150">**1000**</span></span> | <span data-ttu-id="3edac-151">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="3edac-151">PERMISSION_DENIED</span></span> |<span data-ttu-id="3edac-152">Autorisations d’emplacement refusées par l’utilisateur pour l’application Teams ou l’application web.</span><span class="sxs-lookup"><span data-stu-id="3edac-152">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="3edac-153">**4000**</span><span class="sxs-lookup"><span data-stu-id="3edac-153">**4000**</span></span> | <span data-ttu-id="3edac-154">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="3edac-154">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="3edac-155">L’API est invoquée avec des arguments obligatoires erronés ou insuffisants.</span><span class="sxs-lookup"><span data-stu-id="3edac-155">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="3edac-156">**8000**</span><span class="sxs-lookup"><span data-stu-id="3edac-156">**8000**</span></span> | <span data-ttu-id="3edac-157">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="3edac-157">USER_ABORT</span></span> |<span data-ttu-id="3edac-158">L’utilisateur a annulé l’opération.</span><span class="sxs-lookup"><span data-stu-id="3edac-158">User cancelled the operation.</span></span>|
| <span data-ttu-id="3edac-159">**9000**</span><span class="sxs-lookup"><span data-stu-id="3edac-159">**9000**</span></span> | <span data-ttu-id="3edac-160">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="3edac-160">OLD_PLATFORM</span></span> | <span data-ttu-id="3edac-161">L’utilisateur se trouve sur une ancienne build de plateforme où l’implémentation de l’API n’est pas présente.</span><span class="sxs-lookup"><span data-stu-id="3edac-161">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="3edac-162">La mise à niveau de la build doit résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="3edac-162">Upgrading the build should resolve the issue.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="3edac-163">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="3edac-163">Code snippets</span></span>

<span data-ttu-id="3edac-164">**Api `getLocation` d’appel pour récupérer l’emplacement :**</span><span class="sxs-lookup"><span data-stu-id="3edac-164">**Calling `getLocation` API to retrieve the location:**</span></span>

```javascript
let locationProps = {"allowChooseLocation":true,"showMap":true};
microsoftTeams.location.getLocation(locationProps, (err: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
          if (err) {
            output(err);
            return;
          }
          output(JSON.stringify(location));
});
```

<span data-ttu-id="3edac-165">**Api `showLocation` d’appel pour afficher l’emplacement :**</span><span class="sxs-lookup"><span data-stu-id="3edac-165">**Calling `showLocation` API to display the location:**</span></span>

```javascript
let location = {"latitude":17,"longitude":17};
microsoftTeams.location.showLocation(location, (err: microsoftTeams.SdkError, result: boolean) => {
          if (err) {
            output(err);
            return;
          }
     output(result);
});
```

## <a name="see-also"></a><span data-ttu-id="3edac-166">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3edac-166">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3edac-167">Intégrer des fonctionnalités multimédias dans Teams</span><span class="sxs-lookup"><span data-stu-id="3edac-167">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3edac-168">Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="3edac-168">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
