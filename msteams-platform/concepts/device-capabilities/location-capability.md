---
title: Intégrer les fonctionnalités d’emplacement
author: Rajeshwari-v
description: Comment utiliser le client JavaScript SDK Teams tirer parti des capacités de localisation
keywords: fonctionnalités de carte de localisation autorisations d’appareil natif
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b85f19e74d0a8121dd290fc395c1018178437b3a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566186"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="9a57d-104">Intégrer les fonctionnalités d’emplacement</span><span class="sxs-lookup"><span data-stu-id="9a57d-104">Integrate location capabilities</span></span> 

<span data-ttu-id="9a57d-105">Ce document vous guide sur la façon d’intégrer les capacités de localisation de l’appareil natif à votre Teams appe.</span><span class="sxs-lookup"><span data-stu-id="9a57d-105">This document guides you on how to integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="9a57d-106">Vous pouvez utiliser [Microsoft Teams client JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), qui fournit les outils nécessaires pour que votre application accède aux fonctionnalités de l’appareil [natif de l’utilisateur.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="9a57d-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="9a57d-107">Utilisez les API de localisation, telles que [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) et [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) pour intégrer les fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="9a57d-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="9a57d-108">Avantages de l’intégration des capacités de localisation</span><span class="sxs-lookup"><span data-stu-id="9a57d-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="9a57d-109">Le principal avantage de l’intégration des fonctionnalités de localisation dans vos applications Teams est qu’il permet aux développeurs d’applications Web sur la plate-forme Teams de tirer parti des fonctionnalités de localisation avec Microsoft Teams client JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="9a57d-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="9a57d-110">Des exemples suivants montrent comment l’intégration des capacités de localisation est utilisée dans différents scénarios :</span><span class="sxs-lookup"><span data-stu-id="9a57d-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="9a57d-111">Dans une usine, le superviseur peut suivre la présence des travailleurs en leur demandant de prendre un selfie à proximité de l’usine et de le partager via l’application spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9a57d-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="9a57d-112">Les données de localisation sont également capturées et envoyées avec l’image.</span><span class="sxs-lookup"><span data-stu-id="9a57d-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="9a57d-113">Les capacités de localisation permettent au personnel d’entretien d’un fournisseur de services de partager les données de santé authentiques des tours cellulaires avec la direction.</span><span class="sxs-lookup"><span data-stu-id="9a57d-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="9a57d-114">La direction peut comparer n’importe quel décalage entre les informations de localisation saisies et les données soumises par le personnel de maintenance.</span><span class="sxs-lookup"><span data-stu-id="9a57d-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="9a57d-115">Pour intégrer les fonctionnalités de localisation, vous devez mettre à jour le fichier manifeste de l’application et appeler les API.</span><span class="sxs-lookup"><span data-stu-id="9a57d-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="9a57d-116">Pour une intégration efficace, vous devez avoir une bonne compréhension des [extraits de code pour appeler](#code-snippets) les API de localisation.</span><span class="sxs-lookup"><span data-stu-id="9a57d-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="9a57d-117">Il est important de vous familiariser avec les erreurs [de réponse API](#error-handling) pour gérer les erreurs dans votre application Teams apprité.</span><span class="sxs-lookup"><span data-stu-id="9a57d-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="9a57d-118">Actuellement, le Microsoft Teams pour les capacités de localisation n’est disponible que pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="9a57d-118">Currently, Microsoft Teams support for location capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="9a57d-119">Manifeste de mise à jour</span><span class="sxs-lookup"><span data-stu-id="9a57d-119">Update manifest</span></span>

<span data-ttu-id="9a57d-120">Mettez à jour Teams application [manifest.jsdans le](../../resources/schema/manifest-schema.md#devicepermissions) fichier en ajoutant la propriété et en `devicePermissions` spécifier `geolocation` .</span><span class="sxs-lookup"><span data-stu-id="9a57d-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="9a57d-121">Il permet à votre application de demander les autorisations requises aux utilisateurs avant qu’ils ne commencent à utiliser les fonctionnalités de localisation.</span><span class="sxs-lookup"><span data-stu-id="9a57d-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="9a57d-122">**L’invite autorisations** de demande s’affiche automatiquement lorsqu’une Teams api est lancée.</span><span class="sxs-lookup"><span data-stu-id="9a57d-122">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="9a57d-123">Pour plus d’informations, consultez les [autorisations de l’appareil de demande](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="9a57d-123">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="9a57d-124">API de localisation</span><span class="sxs-lookup"><span data-stu-id="9a57d-124">Location APIs</span></span>

<span data-ttu-id="9a57d-125">Vous devez utiliser l’ensemble d’API suivants pour activer les capacités de localisation de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="9a57d-125">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="9a57d-126">API</span><span class="sxs-lookup"><span data-stu-id="9a57d-126">API</span></span>      | <span data-ttu-id="9a57d-127">Description</span><span class="sxs-lookup"><span data-stu-id="9a57d-127">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="9a57d-128">getLocation (en)</span><span class="sxs-lookup"><span data-stu-id="9a57d-128">getLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="9a57d-129">Donne l’emplacement actuel de l’appareil de l’utilisateur ou ouvre le cueilleur de localisation natif et renvoie l’emplacement choisi par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9a57d-129">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="9a57d-130">showLocation</span><span class="sxs-lookup"><span data-stu-id="9a57d-130">showLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | <span data-ttu-id="9a57d-131">Affiche l’emplacement sur la carte.</span><span class="sxs-lookup"><span data-stu-id="9a57d-131">Shows location on map.</span></span> |

> [!NOTE]

> <span data-ttu-id="9a57d-132">`getLocation()`L’API est livré avec les [configurations d’entrée suivantes](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` et `showMap` .</span><span class="sxs-lookup"><span data-stu-id="9a57d-132">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="9a57d-133">Si la valeur est `allowChooseLocation` *vraie, alors les* utilisateurs peuvent choisir n’importe quel endroit de leur choix.</span><span class="sxs-lookup"><span data-stu-id="9a57d-133">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="9a57d-134">Si la valeur est *fausse,* alors les utilisateurs ne peuvent pas modifier leur emplacement actuel.</span><span class="sxs-lookup"><span data-stu-id="9a57d-134">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="9a57d-135">Si la valeur est `showMap` *fausse,* l’emplacement actuel est récupéré sans afficher la carte.</span><span class="sxs-lookup"><span data-stu-id="9a57d-135">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="9a57d-136">`showMap` est ignoré si `allowChooseLocation` est mis à *vrai*.</span><span class="sxs-lookup"><span data-stu-id="9a57d-136">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="9a57d-137">**Expérience d’application Web pour les fonctionnalités de localisation** 
 ![ expérience d’application web pour les fonctionnalités de localisation](../../assets/images/tabs/location-capability.png)</span><span class="sxs-lookup"><span data-stu-id="9a57d-137">**Web app experience for location capabilities**
![web app experience for location capabilities](../../assets/images/tabs/location-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="9a57d-138">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="9a57d-138">Error handling</span></span>

<span data-ttu-id="9a57d-139">Vous devez vous assurer de gérer ces erreurs de manière appropriée dans Teams application.</span><span class="sxs-lookup"><span data-stu-id="9a57d-139">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="9a57d-140">Le tableau suivant énumère les codes d’erreur et les conditions dans lesquelles les erreurs sont générées :</span><span class="sxs-lookup"><span data-stu-id="9a57d-140">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="9a57d-141">Code d’erreur</span><span class="sxs-lookup"><span data-stu-id="9a57d-141">Error code</span></span> |  <span data-ttu-id="9a57d-142">Nom de l’erreur</span><span class="sxs-lookup"><span data-stu-id="9a57d-142">Error name</span></span>     | <span data-ttu-id="9a57d-143">Condition</span><span class="sxs-lookup"><span data-stu-id="9a57d-143">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="9a57d-144">**100**</span><span class="sxs-lookup"><span data-stu-id="9a57d-144">**100**</span></span> | <span data-ttu-id="9a57d-145">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="9a57d-145">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="9a57d-146">L’API n’est pas prise en charge sur la plate-forme actuelle.</span><span class="sxs-lookup"><span data-stu-id="9a57d-146">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="9a57d-147">**500**</span><span class="sxs-lookup"><span data-stu-id="9a57d-147">**500**</span></span> | <span data-ttu-id="9a57d-148">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="9a57d-148">INTERNAL_ERROR</span></span> | <span data-ttu-id="9a57d-149">L’erreur interne est rencontrée lors de l’exécution de l’opération requise.</span><span class="sxs-lookup"><span data-stu-id="9a57d-149">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="9a57d-150">**1000**</span><span class="sxs-lookup"><span data-stu-id="9a57d-150">**1000**</span></span> | <span data-ttu-id="9a57d-151">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="9a57d-151">PERMISSION_DENIED</span></span> |<span data-ttu-id="9a57d-152">Utilisateur refusé les autorisations de localisation à l Teams appe ou l’application Web .</span><span class="sxs-lookup"><span data-stu-id="9a57d-152">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="9a57d-153">**4000**</span><span class="sxs-lookup"><span data-stu-id="9a57d-153">**4000**</span></span> | <span data-ttu-id="9a57d-154">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="9a57d-154">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="9a57d-155">L’API est invoquée avec des arguments obligatoires erronés ou insuffisants.</span><span class="sxs-lookup"><span data-stu-id="9a57d-155">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="9a57d-156">**8000**</span><span class="sxs-lookup"><span data-stu-id="9a57d-156">**8000**</span></span> | <span data-ttu-id="9a57d-157">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="9a57d-157">USER_ABORT</span></span> |<span data-ttu-id="9a57d-158">L’utilisateur a annulé l’opération.</span><span class="sxs-lookup"><span data-stu-id="9a57d-158">User cancelled the operation.</span></span>|
| <span data-ttu-id="9a57d-159">**9000**</span><span class="sxs-lookup"><span data-stu-id="9a57d-159">**9000**</span></span> | <span data-ttu-id="9a57d-160">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="9a57d-160">OLD_PLATFORM</span></span> | <span data-ttu-id="9a57d-161">L’utilisateur est sur l’ancienne plate-forme de construction où la mise en œuvre de l’API n’est pas présente.</span><span class="sxs-lookup"><span data-stu-id="9a57d-161">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="9a57d-162">La mise à niveau de la build devrait résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="9a57d-162">Upgrading the build should resolve the issue.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="9a57d-163">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="9a57d-163">Code snippets</span></span>

<span data-ttu-id="9a57d-164">**Appel `getLocation` api pour récupérer l’emplacement:**</span><span class="sxs-lookup"><span data-stu-id="9a57d-164">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="9a57d-165">**Appel `showLocation` api pour afficher l’emplacement :**</span><span class="sxs-lookup"><span data-stu-id="9a57d-165">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="see-also"></a><span data-ttu-id="9a57d-166">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9a57d-166">See also</span></span>

* [<span data-ttu-id="9a57d-167">Intégrer les capacités des médias dans Teams</span><span class="sxs-lookup"><span data-stu-id="9a57d-167">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="9a57d-168">Intégrer la capacité de scanner de code QR ou de code à barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="9a57d-168">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
