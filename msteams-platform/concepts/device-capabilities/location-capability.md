---
title: Intégrer les fonctionnalités d’emplacement
author: Rajeshwari-v
description: Utilisation du SDK Teams client JavaScript pour tirer parti des fonctionnalités d’emplacement
keywords: autorisations natives d’appareil pour les fonctionnalités de carte d’emplacement
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 3e6c4bda9a1a0024380cb295cd280db1d630f019
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211610"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="d2551-104">Intégrer les fonctionnalités d’emplacement</span><span class="sxs-lookup"><span data-stu-id="d2551-104">Integrate location capabilities</span></span> 

<span data-ttu-id="d2551-105">Vous pouvez intégrer les fonctionnalités d’emplacement de l’appareil natif à votre Teams application.</span><span class="sxs-lookup"><span data-stu-id="d2551-105">You can integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="d2551-106">Vous pouvez utiliser [Microsoft Teams SDK client JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit les outils nécessaires à votre application pour accéder aux fonctionnalités natives de l’appareil de l’utilisateur. [](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="d2551-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="d2551-107">Utilisez les API d’emplacement, telles [que getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) et [showLocation,](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) pour intégrer les fonctionnalités dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d2551-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="d2551-108">Avantages de l’intégration des fonctionnalités d’emplacement</span><span class="sxs-lookup"><span data-stu-id="d2551-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="d2551-109">Le principal avantage de l’intégration des fonctionnalités d’emplacement dans vos applications Teams est qu’elle permet aux développeurs d’applications web sur la plateforme Teams d’exploiter les fonctionnalités d’emplacement avec Microsoft Teams SDK client JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d2551-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="d2551-110">Les exemples suivants montrent comment l’intégration des fonctionnalités d’emplacement est utilisée dans différents scénarios :</span><span class="sxs-lookup"><span data-stu-id="d2551-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="d2551-111">Dans une usine, le responsable peut suivre la présence des employés en leur demandant de prendre un selfie à proximité de l’usine et de le partager via l’application spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d2551-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="d2551-112">Les données d’emplacement sont également capturées et envoyées avec l’image.</span><span class="sxs-lookup"><span data-stu-id="d2551-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="d2551-113">Les fonctionnalités d’emplacement permettent au personnel de maintenance d’un fournisseur de services de partager des données d’état d’état authentiques des pylônes cellulaires avec la direction.</span><span class="sxs-lookup"><span data-stu-id="d2551-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="d2551-114">La direction peut comparer les différences entre les informations d’emplacement capturées et les données envoyées par le personnel de maintenance.</span><span class="sxs-lookup"><span data-stu-id="d2551-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="d2551-115">Pour intégrer des fonctionnalités d’emplacement, vous devez mettre à jour le fichier manifeste de l’application et appeler les API.</span><span class="sxs-lookup"><span data-stu-id="d2551-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="d2551-116">Pour une intégration efficace, vous devez bien comprendre les [extraits](#code-snippets) de code pour appeler les API d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="d2551-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="d2551-117">Il est important de vous familiariser avec les erreurs de réponse [d’API](#error-handling) pour gérer les erreurs dans votre Teams application.</span><span class="sxs-lookup"><span data-stu-id="d2551-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="d2551-118">Actuellement, Microsoft Teams prise en charge des fonctionnalités d’emplacement est disponible uniquement pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="d2551-118">Currently, Microsoft Teams support for location capabilities is available for mobile clients only.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="d2551-119">Mettre à jour le manifeste</span><span class="sxs-lookup"><span data-stu-id="d2551-119">Update manifest</span></span>

<span data-ttu-id="d2551-120">Mettez à jour [Teams’applicationmanifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la `devicePermissions` propriété et en spécifiant `geolocation` .</span><span class="sxs-lookup"><span data-stu-id="d2551-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="d2551-121">Il permet à votre application de demander les autorisations requises aux utilisateurs avant de commencer à utiliser les fonctionnalités de localisation.</span><span class="sxs-lookup"><span data-stu-id="d2551-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span> <span data-ttu-id="d2551-122">La mise à jour du manifeste de l’application est la suivante :</span><span class="sxs-lookup"><span data-stu-id="d2551-122">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="d2551-123">**L’invite Demander des autorisations** s’affiche automatiquement lorsqu’une API Teams est lancée.</span><span class="sxs-lookup"><span data-stu-id="d2551-123">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="d2551-124">Pour plus d’informations, voir [demander des autorisations d’appareil.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="d2551-124">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="d2551-125">API d’emplacement</span><span class="sxs-lookup"><span data-stu-id="d2551-125">Location APIs</span></span>

<span data-ttu-id="d2551-126">Vous devez utiliser l’ensemble d’API suivant pour activer les fonctionnalités d’emplacement de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="d2551-126">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="d2551-127">API</span><span class="sxs-lookup"><span data-stu-id="d2551-127">API</span></span>      | <span data-ttu-id="d2551-128">Description</span><span class="sxs-lookup"><span data-stu-id="d2551-128">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="d2551-129">getLocation</span><span class="sxs-lookup"><span data-stu-id="d2551-129">getLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="d2551-130">Fournit l’emplacement actuel de l’appareil de l’utilisateur ou ouvre le s picker d’emplacement natif et renvoie l’emplacement choisi par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2551-130">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="d2551-131">showLocation</span><span class="sxs-lookup"><span data-stu-id="d2551-131">showLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | <span data-ttu-id="d2551-132">Affiche l’emplacement sur la carte.</span><span class="sxs-lookup"><span data-stu-id="d2551-132">Shows location on map.</span></span> |

> [!NOTE]
> <span data-ttu-id="d2551-133">`getLocation()`L’API est livré avec les [configurations d’entrée suivantes](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)et `allowChooseLocation` `showMap` .</span><span class="sxs-lookup"><span data-stu-id="d2551-133">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="d2551-134">Si la valeur est `allowChooseLocation` *true,* les utilisateurs peuvent choisir n’importe quel emplacement de leur choix.</span><span class="sxs-lookup"><span data-stu-id="d2551-134">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="d2551-135">Si la valeur est *false,* les utilisateurs ne peuvent pas modifier leur emplacement actuel.</span><span class="sxs-lookup"><span data-stu-id="d2551-135">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="d2551-136">Si la valeur est `showMap` *false,* l’emplacement actuel est récupéré sans afficher la carte.</span><span class="sxs-lookup"><span data-stu-id="d2551-136">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="d2551-137">`showMap` est ignoré si `allowChooseLocation` est définie sur *true*.</span><span class="sxs-lookup"><span data-stu-id="d2551-137">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="d2551-138">L’image suivante illustre l’expérience d’application web des fonctionnalités de localisation :</span><span class="sxs-lookup"><span data-stu-id="d2551-138">The following image depicts web app experience of location capabilities:</span></span>

![expérience d’application web pour les fonctionnalités de localisation](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a><span data-ttu-id="d2551-140">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="d2551-140">Code snippets</span></span>

<span data-ttu-id="d2551-141">**Api `getLocation` d’appel pour récupérer l’emplacement :**</span><span class="sxs-lookup"><span data-stu-id="d2551-141">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="d2551-142">**Api `showLocation` d’appel pour afficher l’emplacement :**</span><span class="sxs-lookup"><span data-stu-id="d2551-142">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="error-handling"></a><span data-ttu-id="d2551-143">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="d2551-143">Error handling</span></span>

<span data-ttu-id="d2551-144">Vous devez vous assurer de gérer ces erreurs de manière appropriée dans votre Teams application.</span><span class="sxs-lookup"><span data-stu-id="d2551-144">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="d2551-145">Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées :</span><span class="sxs-lookup"><span data-stu-id="d2551-145">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="d2551-146">Code d’erreur</span><span class="sxs-lookup"><span data-stu-id="d2551-146">Error code</span></span> |  <span data-ttu-id="d2551-147">Nom de l’erreur</span><span class="sxs-lookup"><span data-stu-id="d2551-147">Error name</span></span>     | <span data-ttu-id="d2551-148">Condition</span><span class="sxs-lookup"><span data-stu-id="d2551-148">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="d2551-149">**100**</span><span class="sxs-lookup"><span data-stu-id="d2551-149">**100**</span></span> | <span data-ttu-id="d2551-150">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="d2551-150">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="d2551-151">L’API n’est pas prise en charge sur la plateforme actuelle.</span><span class="sxs-lookup"><span data-stu-id="d2551-151">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="d2551-152">**500**</span><span class="sxs-lookup"><span data-stu-id="d2551-152">**500**</span></span> | <span data-ttu-id="d2551-153">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="d2551-153">INTERNAL_ERROR</span></span> | <span data-ttu-id="d2551-154">Une erreur interne est rencontrée lors de l’opération requise.</span><span class="sxs-lookup"><span data-stu-id="d2551-154">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="d2551-155">**1000**</span><span class="sxs-lookup"><span data-stu-id="d2551-155">**1000**</span></span> | <span data-ttu-id="d2551-156">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="d2551-156">PERMISSION_DENIED</span></span> |<span data-ttu-id="d2551-157">Autorisations d’emplacement refusées par l’utilisateur Teams’application ou l’application web.</span><span class="sxs-lookup"><span data-stu-id="d2551-157">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="d2551-158">**4000**</span><span class="sxs-lookup"><span data-stu-id="d2551-158">**4000**</span></span> | <span data-ttu-id="d2551-159">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="d2551-159">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="d2551-160">L’API est invoquée avec des arguments obligatoires erronés ou insuffisants.</span><span class="sxs-lookup"><span data-stu-id="d2551-160">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="d2551-161">**8000**</span><span class="sxs-lookup"><span data-stu-id="d2551-161">**8000**</span></span> | <span data-ttu-id="d2551-162">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="d2551-162">USER_ABORT</span></span> |<span data-ttu-id="d2551-163">L’utilisateur a annulé l’opération.</span><span class="sxs-lookup"><span data-stu-id="d2551-163">User cancelled the operation.</span></span>|
| <span data-ttu-id="d2551-164">**9000**</span><span class="sxs-lookup"><span data-stu-id="d2551-164">**9000**</span></span> | <span data-ttu-id="d2551-165">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="d2551-165">OLD_PLATFORM</span></span> | <span data-ttu-id="d2551-166">L’utilisateur se trouve sur une ancienne build de plateforme où l’implémentation de l’API n’est pas présente.</span><span class="sxs-lookup"><span data-stu-id="d2551-166">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="d2551-167">La mise à niveau de la build doit résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="d2551-167">Upgrading the build should resolve the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="d2551-168">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d2551-168">See also</span></span>

* [<span data-ttu-id="d2551-169">Intégrer des fonctionnalités multimédias dans Teams</span><span class="sxs-lookup"><span data-stu-id="d2551-169">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="d2551-170">Intégrer le code QR ou la fonctionnalité de scanneur de code-barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="d2551-170">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="d2551-171">Intégrer la fonctionnalité s’il s’Teams</span><span class="sxs-lookup"><span data-stu-id="d2551-171">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)
