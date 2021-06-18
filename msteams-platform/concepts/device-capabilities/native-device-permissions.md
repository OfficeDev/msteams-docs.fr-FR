---
title: Demander des autorisations d’appareil pour votre application Microsoft Teams client
keywords: autorisations des fonctionnalités des applications Teams
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui nécessitent généralement le consentement de l’utilisateur
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 920ab47a60340fd9a14e4f5dfb2e39a8ad8f3a89
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994349"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="f59f3-104">Demander des autorisations d’appareil pour votre application Microsoft Teams client</span><span class="sxs-lookup"><span data-stu-id="f59f3-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="f59f3-105">Vous pouvez enrichir votre application Teams avec des fonctionnalités natives d’appareil, telles que la caméra, le microphone et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="f59f3-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="f59f3-106">Ce document vous guide sur la façon de demander le consentement de l’utilisateur et d’accéder aux autorisations natives de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="f59f3-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="f59f3-107">Pour intégrer des fonctionnalités multimédias dans Microsoft Teams application mobile, voir [Intégrer les fonctionnalités multimédias.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="f59f3-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="f59f3-108">Pour intégrer la fonctionnalité de QR ou de scanneur de code-barres dans votre application mobile Microsoft Teams, voir Intégrer la [QR](qr-barcode-scanner-capability.md)ou la fonctionnalité de scanneur de code-barres dans Teams .</span><span class="sxs-lookup"><span data-stu-id="f59f3-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md).</span></span>
> * <span data-ttu-id="f59f3-109">Pour intégrer des fonctionnalités d’emplacement dans Microsoft Teams application mobile, voir [Intégrer les fonctionnalités d’emplacement.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="f59f3-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="f59f3-110">Autorisations d’appareil natives</span><span class="sxs-lookup"><span data-stu-id="f59f3-110">Native device permissions</span></span>

<span data-ttu-id="f59f3-111">Vous devez demander les autorisations d’appareil pour accéder aux fonctionnalités natives de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="f59f3-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="f59f3-112">Les autorisations d’appareil fonctionnent de la même manière pour toutes les constructions d’application, telles que les onglets, les modules de tâche ou les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="f59f3-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="f59f3-113">L’utilisateur doit se rendre sur la page d’autorisations Teams paramètres pour gérer les autorisations d’appareil.</span><span class="sxs-lookup"><span data-stu-id="f59f3-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="f59f3-114">En accédant aux fonctionnalités de l’appareil, vous pouvez créer des expériences plus riches sur la plateforme Teams, telles que :</span><span class="sxs-lookup"><span data-stu-id="f59f3-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="f59f3-115">Capturer et afficher des images.</span><span class="sxs-lookup"><span data-stu-id="f59f3-115">Capture and view images.</span></span>
* <span data-ttu-id="f59f3-116">Analysez la QR ou le code-barres.</span><span class="sxs-lookup"><span data-stu-id="f59f3-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="f59f3-117">Enregistrez et partagez de courtes vidéos.</span><span class="sxs-lookup"><span data-stu-id="f59f3-117">Record and share short videos.</span></span>
* <span data-ttu-id="f59f3-118">Enregistrez les mémos audio et enregistrez-les pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f59f3-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="f59f3-119">Utilisez les informations d’emplacement de l’utilisateur pour afficher les informations pertinentes.</span><span class="sxs-lookup"><span data-stu-id="f59f3-119">Use the location information of the user to display relevant information.</span></span>

> [!NOTE]
> <span data-ttu-id="f59f3-120">Actuellement, Teams ne prend pas en charge les autorisations d’appareil pour les applications à fenêtres multiples, les onglets et le bureau secondaire de la réunion.</span><span class="sxs-lookup"><span data-stu-id="f59f3-120">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span> 

## <a name="access-device-permissions"></a><span data-ttu-id="f59f3-121">Autorisations d’accès aux appareils</span><span class="sxs-lookup"><span data-stu-id="f59f3-121">Access device permissions</span></span>

<span data-ttu-id="f59f3-122">Le [Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) fournit les outils nécessaires à votre application mobile Teams pour accéder aux [autorisations](#manage-permissions) d’appareil de l’utilisateur et créer une expérience plus riche.</span><span class="sxs-lookup"><span data-stu-id="f59f3-122">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="f59f3-123">Bien que l’accès à ces fonctionnalités soit standard dans les navigateurs web modernes, vous devez informer Teams sur les fonctionnalités que vous utilisez en mettant à jour votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="f59f3-123">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="f59f3-124">Cette mise à jour vous permet de demander des autorisations pendant que votre application s’exécute sur Teams client de bureau.</span><span class="sxs-lookup"><span data-stu-id="f59f3-124">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="f59f3-125">Actuellement, Microsoft Teams prise en charge des fonctionnalités multimédias et de scanneur de code-barres QR est disponible uniquement pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="f59f3-125">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="f59f3-126">Gérer les autorisations</span><span class="sxs-lookup"><span data-stu-id="f59f3-126">Manage permissions</span></span>

<span data-ttu-id="f59f3-127">Un utilisateur peut gérer les autorisations d’appareil  Teams  paramètres en sélectionnant Autoriser ou refuser des autorisations pour des applications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="f59f3-127">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="f59f3-128">Bureau</span><span class="sxs-lookup"><span data-stu-id="f59f3-128">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="f59f3-129">Ouvrez votre Teams application.</span><span class="sxs-lookup"><span data-stu-id="f59f3-129">Open your Teams app.</span></span>
1. <span data-ttu-id="f59f3-130">Sélectionnez votre icône de profil dans le coin supérieur droit de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f59f3-130">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="f59f3-131">Sélectionnez **Paramètres**  >  **autorisations** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="f59f3-131">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="f59f3-132">Sélectionnez les paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="f59f3-132">Select your desired settings.</span></span>

   ![Écran des paramètres de bureau des autorisations d’appareil](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="f59f3-134">Mobile</span><span class="sxs-lookup"><span data-stu-id="f59f3-134">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="f59f3-135">Ouvrez Teams.</span><span class="sxs-lookup"><span data-stu-id="f59f3-135">Open Teams.</span></span>
1. <span data-ttu-id="f59f3-136">Go to **Paramètres**  >  **App Permissions**.</span><span class="sxs-lookup"><span data-stu-id="f59f3-136">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="f59f3-137">Sélectionnez l’application pour laquelle vous devez choisir les paramètres.</span><span class="sxs-lookup"><span data-stu-id="f59f3-137">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="f59f3-138">Sélectionnez les paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="f59f3-138">Select your desired settings.</span></span>

    ![Écran des paramètres mobiles des autorisations d’appareil](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="f59f3-140">Spécifier des autorisations</span><span class="sxs-lookup"><span data-stu-id="f59f3-140">Specify permissions</span></span>

<span data-ttu-id="f59f3-141">Mettez à jour les propriétés de votre application en ajoutant et en spécifiant les cinq propriétés que vous `manifest.json` utilisez dans votre application `devicePermissions` :</span><span class="sxs-lookup"><span data-stu-id="f59f3-141">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="f59f3-142">Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement :</span><span class="sxs-lookup"><span data-stu-id="f59f3-142">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="f59f3-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="f59f3-143">Property</span></span>      | <span data-ttu-id="f59f3-144">Description</span><span class="sxs-lookup"><span data-stu-id="f59f3-144">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="f59f3-145">media</span><span class="sxs-lookup"><span data-stu-id="f59f3-145">media</span></span>         | <span data-ttu-id="f59f3-146">Autorisation d’utiliser la caméra, le microphone, les haut-parleurs et d’accéder à la galerie multimédia.</span><span class="sxs-lookup"><span data-stu-id="f59f3-146">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="f59f3-147">géolocalisation</span><span class="sxs-lookup"><span data-stu-id="f59f3-147">geolocation</span></span>   | <span data-ttu-id="f59f3-148">Autorisation de renvoyer l’emplacement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f59f3-148">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="f59f3-149">notifications</span><span class="sxs-lookup"><span data-stu-id="f59f3-149">notifications</span></span> | <span data-ttu-id="f59f3-150">Autorisation d’envoyer des notifications à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f59f3-150">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="f59f3-151">midi</span><span class="sxs-lookup"><span data-stu-id="f59f3-151">midi</span></span>          | <span data-ttu-id="f59f3-152">Autorisation d’envoyer et de recevoir des informations MIDI (Music Instrument Digital Interface) à partir d’un instrument de musique numérique.</span><span class="sxs-lookup"><span data-stu-id="f59f3-152">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="f59f3-153">openExternal</span><span class="sxs-lookup"><span data-stu-id="f59f3-153">openExternal</span></span>  | <span data-ttu-id="f59f3-154">Autorisation d’ouvrir des liens dans des applications externes.</span><span class="sxs-lookup"><span data-stu-id="f59f3-154">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="f59f3-155">Vérifier les autorisations de votre application</span><span class="sxs-lookup"><span data-stu-id="f59f3-155">Check permissions from your app</span></span>

<span data-ttu-id="f59f3-156">Après l’ajout au manifeste de votre application, vérifiez les autorisations à l’aide de `devicePermissions` **l’API d’autorisations HTML5** sans provoquer d’invite :</span><span class="sxs-lookup"><span data-stu-id="f59f3-156">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

``` Javascript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="f59f3-157">Utiliser Teams API pour obtenir des autorisations d’appareil</span><span class="sxs-lookup"><span data-stu-id="f59f3-157">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="f59f3-158">Tirez parti de l’API HTML5 ou Teams appropriée pour afficher une invite pour obtenir l’autorisation d’accès aux autorisations d’appareil.</span><span class="sxs-lookup"><span data-stu-id="f59f3-158">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f59f3-159">Prise en `camera` charge de , et est activée par le biais de `gallery` `microphone` [**l’API selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f59f3-159">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="f59f3-160">Utilisez [**l’API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) pour une capture d’image unique.</span><span class="sxs-lookup"><span data-stu-id="f59f3-160">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="f59f3-161">La prise `location` en charge est activée via [**l’API getLocation.**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f59f3-161">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="f59f3-162">Vous devez l’utiliser pour l’emplacement, car l’API de géolocalisation HTML5 n’est actuellement pas entièrement prise `getLocation API` en charge Teams client de bureau.</span><span class="sxs-lookup"><span data-stu-id="f59f3-162">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="f59f3-163">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f59f3-163">For example:</span></span>
 * <span data-ttu-id="f59f3-164">Pour demander à l’utilisateur d’accéder à son emplacement, vous devez appeler `getCurrentPosition()` :</span><span class="sxs-lookup"><span data-stu-id="f59f3-164">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="f59f3-165">Pour demander à l’utilisateur d’accéder à son appareil photo sur un ordinateur de bureau ou sur le web, vous devez appeler `getUserMedia()` :</span><span class="sxs-lookup"><span data-stu-id="f59f3-165">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="f59f3-166">Pour capturer l’image sur un appareil mobile, Teams mobile demande l’autorisation lorsque vous appelez `captureImage()` :</span><span class="sxs-lookup"><span data-stu-id="f59f3-166">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="f59f3-167">Les notifications inviteront l’utilisateur à appeler `requestPermission()` :</span><span class="sxs-lookup"><span data-stu-id="f59f3-167">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="f59f3-168">Pour utiliser l’appareil photo ou accéder à la galerie de photos, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="f59f3-168">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="f59f3-169">Pour utiliser le microphone, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="f59f3-169">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="f59f3-170">Pour demander à l’utilisateur de partager un emplacement sur l’interface de carte, Teams mobile demande l’autorisation lorsque vous appelez `getLocation()` :</span><span class="sxs-lookup"><span data-stu-id="f59f3-170">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="f59f3-171">Bureau</span><span class="sxs-lookup"><span data-stu-id="f59f3-171">Desktop</span></span>](#tab/desktop)

   ![Invite d’autorisations d’appareil de bureau Onglets](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="f59f3-173">Mobile</span><span class="sxs-lookup"><span data-stu-id="f59f3-173">Mobile</span></span>](#tab/mobile)

   ![Invite d’autorisations d’appareil mobile Onglets](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="f59f3-175">Comportement des autorisations entre les sessions de connexion</span><span class="sxs-lookup"><span data-stu-id="f59f3-175">Permission behavior across login sessions</span></span>

<span data-ttu-id="f59f3-176">Les autorisations d’appareil sont stockées pour chaque session de connexion.</span><span class="sxs-lookup"><span data-stu-id="f59f3-176">Device permissions are stored for every login session.</span></span> <span data-ttu-id="f59f3-177">Cela signifie que si vous vous connectez à une autre instance de Teams, par exemple, sur un autre ordinateur, les autorisations de votre appareil à partir de vos sessions précédentes ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="f59f3-177">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="f59f3-178">Par conséquent, vous devez consentir à nouveau aux autorisations d’appareil pour la nouvelle session.</span><span class="sxs-lookup"><span data-stu-id="f59f3-178">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="f59f3-179">Cela signifie également que, si vous vous dé connectez à Teams ou que vous changez de client dans Teams, les autorisations de votre appareil sont supprimées de la session de connexion précédente.</span><span class="sxs-lookup"><span data-stu-id="f59f3-179">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="f59f3-180">Lorsque vous consentez aux autorisations natives de l’appareil, elle n’est valide que pour votre session _de_ connexion actuelle.</span><span class="sxs-lookup"><span data-stu-id="f59f3-180">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f59f3-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f59f3-181">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f59f3-182">Intégrer des fonctionnalités multimédias dans Teams</span><span class="sxs-lookup"><span data-stu-id="f59f3-182">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f59f3-183">Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="f59f3-183">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f59f3-184">Intégrer des fonctionnalités d’emplacement dans Teams</span><span class="sxs-lookup"><span data-stu-id="f59f3-184">Integrate location capabilities in Teams</span></span>](location-capability.md)
