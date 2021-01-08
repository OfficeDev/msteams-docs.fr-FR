---
title: Demander des autorisations de périphérique pour votre onglet Microsoft teams
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui requièrent généralement le consentement de l’utilisateur
keywords: développement d’onglets teams
ms.openlocfilehash: 6be183d2610616f3bd3bdf32554976322193c132
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731978"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="f76a7-104">Demander des autorisations de périphérique pour votre onglet Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="f76a7-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="f76a7-105">Vous voudrez peut-être enrichir votre onglet avec des fonctionnalités qui nécessitent un accès à des fonctionnalités d’appareil natives, telles que :</span><span class="sxs-lookup"><span data-stu-id="f76a7-105">You might want to enrich your tab with features that require access to native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="f76a7-106">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="f76a7-106">Camera</span></span>
> * <span data-ttu-id="f76a7-107">Micro</span><span class="sxs-lookup"><span data-stu-id="f76a7-107">Microphone</span></span>
> * <span data-ttu-id="f76a7-108">Emplacement</span><span class="sxs-lookup"><span data-stu-id="f76a7-108">Location</span></span>
> * <span data-ttu-id="f76a7-109">Notifications</span><span class="sxs-lookup"><span data-stu-id="f76a7-109">Notifications</span></span>

[!Note] <span data-ttu-id="f76a7-110">Pour intégrer les capacités de l’appareil photo et de l’image dans votre application mobile Microsoft Teams, reportez-vous à la rubrique [fonctionnalités de l’appareil photo](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="f76a7-110">To integrate camera and image capabilities within your Microsoft Teams mobile app, refer [Camera and image capabilities in Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="f76a7-111">Pour le moment, le client mobile teams prend uniquement en charge l’accès aux fonctionnalités de l’appareil,, `camera` `gallery` `mic` et `location` via les fonctionnalités natives, et est disponible sur toutes les constructions d’applications, y compris les onglets.</span><span class="sxs-lookup"><span data-stu-id="f76a7-111">At present, Teams mobile client only supports access to `camera`, `gallery`, `mic`, and `location` through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="f76a7-112">La prise en charge de `camera` , de `gallery` et de `mic` est activée via l' [**API selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f76a7-112">Support for `camera`, `gallery`, and `mic` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="f76a7-113">Pour la capture d’image unique, vous pouvez utiliser l' [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f76a7-113">For single image capture you may use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span></span>
> * <span data-ttu-id="f76a7-114">La prise en charge de `location` est activée via l' [**API GetLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f76a7-114">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="f76a7-115">Il est recommandé d’utiliser cette API car l' [**API de géolocalisation**](../../resources/schema/manifest-schema.md#devicepermissions) n’est pas entièrement prise en charge sur tous les clients de bureau.</span><span class="sxs-lookup"><span data-stu-id="f76a7-115">It's recommended you use this API as [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="f76a7-116">Autorisations de l’appareil</span><span class="sxs-lookup"><span data-stu-id="f76a7-116">Device permissions</span></span>

<span data-ttu-id="f76a7-117">L’accès aux autorisations de l’appareil d’un utilisateur vous permet de créer des expériences plus riches, par exemple :</span><span class="sxs-lookup"><span data-stu-id="f76a7-117">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="f76a7-118">Enregistrer et partager des courtes vidéos</span><span class="sxs-lookup"><span data-stu-id="f76a7-118">Record and share short videos</span></span>
* <span data-ttu-id="f76a7-119">Enregistrez des mémos audio courts et enregistrez-les pour une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f76a7-119">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="f76a7-120">Utiliser les informations relatives à l’emplacement de l’utilisateur pour afficher les informations pertinentes</span><span class="sxs-lookup"><span data-stu-id="f76a7-120">Use user location information to display relevant information</span></span>

<span data-ttu-id="f76a7-121">Bien que l’accès à ces fonctionnalités soit standard dans la plupart des navigateurs Web modernes, vous devez informer teams des fonctionnalités que vous souhaitez utiliser en mettant à jour votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="f76a7-121">While access to these features is standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="f76a7-122">Cela vous permettra de demander des autorisations, de la même façon que vous le feriez dans un navigateur, tandis que votre application est exécutée sur le client de bureau Teams.</span><span class="sxs-lookup"><span data-stu-id="f76a7-122">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="f76a7-123">Gérer les autorisations</span><span class="sxs-lookup"><span data-stu-id="f76a7-123">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f76a7-124">Desktop</span><span class="sxs-lookup"><span data-stu-id="f76a7-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="f76a7-125">Ouvrez Teams.</span><span class="sxs-lookup"><span data-stu-id="f76a7-125">Open Teams.</span></span>
1. <span data-ttu-id="f76a7-126">Dans le coin supérieur droit de la fenêtre, sélectionnez l’icône de votre profil.</span><span class="sxs-lookup"><span data-stu-id="f76a7-126">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="f76a7-127">Sélectionnez   ->  **autorisations** des paramètres dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="f76a7-127">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="f76a7-128">Choisissez les paramètres de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f76a7-128">Choose your desired settings.</span></span>

![Écran des paramètres de bureau des autorisations de périphérique](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="f76a7-130">Mobile</span><span class="sxs-lookup"><span data-stu-id="f76a7-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="f76a7-131">Ouvrez Teams.</span><span class="sxs-lookup"><span data-stu-id="f76a7-131">Open Teams.</span></span>
1. <span data-ttu-id="f76a7-132">Accédez à **paramètres**  ->  **app permissions**.</span><span class="sxs-lookup"><span data-stu-id="f76a7-132">Go to **Settings** -> **App Permissions**.</span></span>
1. <span data-ttu-id="f76a7-133">Sélectionnez l’application pour laquelle vous devez choisir des paramètres.</span><span class="sxs-lookup"><span data-stu-id="f76a7-133">Select the app you need to choose settings for.</span></span>
1. <span data-ttu-id="f76a7-134">Choisissez les paramètres de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f76a7-134">Choose your desired settings.</span></span>

![Écran des paramètres mobiles des autorisations de l’appareil](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a><span data-ttu-id="f76a7-136">Propriétés</span><span class="sxs-lookup"><span data-stu-id="f76a7-136">Properties</span></span>

<span data-ttu-id="f76a7-137">Mettez à jour votre application `manifest.json` en ajoutant `devicePermissions` et en spécifiant les cinq propriétés que vous souhaitez utiliser dans votre application :</span><span class="sxs-lookup"><span data-stu-id="f76a7-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```
> [!Note]
>
> <span data-ttu-id="f76a7-138">Le support est également utilisé pour les autorisations d’appareil photo sur mobile.</span><span class="sxs-lookup"><span data-stu-id="f76a7-138">Media is also used for camera permissions on mobile.</span></span>

<span data-ttu-id="f76a7-139">Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement :</span><span class="sxs-lookup"><span data-stu-id="f76a7-139">Each property will allow you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="f76a7-140">Propriété</span><span class="sxs-lookup"><span data-stu-id="f76a7-140">Property</span></span>      | <span data-ttu-id="f76a7-141">Description</span><span class="sxs-lookup"><span data-stu-id="f76a7-141">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="f76a7-142">panne</span><span class="sxs-lookup"><span data-stu-id="f76a7-142">media</span></span>         | <span data-ttu-id="f76a7-143">autorisation d’utilisation de l’appareil photo, du microphone, des haut-parleurs et de la Galerie multimédia Access</span><span class="sxs-lookup"><span data-stu-id="f76a7-143">permission to use the camera, microphone, speakers, and access media gallery</span></span> |
| <span data-ttu-id="f76a7-144">géolocalisation</span><span class="sxs-lookup"><span data-stu-id="f76a7-144">geolocation</span></span>   | <span data-ttu-id="f76a7-145">autorisation de retourner l’emplacement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f76a7-145">permission to return the user's location</span></span>      |
| <span data-ttu-id="f76a7-146">notifications</span><span class="sxs-lookup"><span data-stu-id="f76a7-146">notifications</span></span> | <span data-ttu-id="f76a7-147">autorisation d’envoyer les notifications de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f76a7-147">permission to send the user notifications</span></span>      |
| <span data-ttu-id="f76a7-148">midi</span><span class="sxs-lookup"><span data-stu-id="f76a7-148">midi</span></span>          | <span data-ttu-id="f76a7-149">autorisation d’envoyer et de recevoir des informations midi à partir d’un instrument musical numérique</span><span class="sxs-lookup"><span data-stu-id="f76a7-149">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="f76a7-150">openExternal</span><span class="sxs-lookup"><span data-stu-id="f76a7-150">openExternal</span></span>  | <span data-ttu-id="f76a7-151">autorisation d’ouvrir des liens dans des applications externes</span><span class="sxs-lookup"><span data-stu-id="f76a7-151">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="f76a7-152">Vérification des autorisations à partir de votre onglet</span><span class="sxs-lookup"><span data-stu-id="f76a7-152">Checking permissions from your tab</span></span>

<span data-ttu-id="f76a7-153">Une fois que vous avez ajouté `devicePermissions` à votre manifeste d’application, vous pouvez vérifier les autorisations à l’aide de l’API HTML5 « autorisations » sans générer d’invite.</span><span class="sxs-lookup"><span data-stu-id="f76a7-153">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="f76a7-154">Demander à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f76a7-154">Prompting the user</span></span>

<span data-ttu-id="f76a7-155">Pour afficher une invite permettant d’obtenir le consentement pour accéder aux autorisations des appareils, vous devez tirer parti de l’API HTML5 ou teams appropriée.</span><span class="sxs-lookup"><span data-stu-id="f76a7-155">To show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> 

<span data-ttu-id="f76a7-156">Par exemple, pour inviter l’utilisateur à accéder à son emplacement, vous devez appeler `getCurrentPosition` :</span><span class="sxs-lookup"><span data-stu-id="f76a7-156">For example, to prompt the user to access their location you need to call `getCurrentPosition`:</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="f76a7-157">Pour utiliser l’appareil photo sur un ordinateur de bureau ou sur le Web, teams affiche une invite d’autorisation lorsque vous appelez `getUserMedia` :</span><span class="sxs-lookup"><span data-stu-id="f76a7-157">To use the camera on desktop or web, Teams will show a permission prompt when you call `getUserMedia`:</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="f76a7-158">Pour capturer l’image sur mobile, teams mobile vous demande des autorisations lors de l’appel `captureImage()` :</span><span class="sxs-lookup"><span data-stu-id="f76a7-158">To capture the image on mobile, Teams mobile will ask for permission when you call `captureImage()`:</span></span>

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

<span data-ttu-id="f76a7-159">Les notifications invitent l’utilisateur à appeler les `requestPermission` éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f76a7-159">Notifications will prompt the user when you call `requestPermission`:</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

<span data-ttu-id="f76a7-160">Pour utiliser l’appareil photo ou la Galerie de photos Access, teams mobile demande des autorisations lorsque vous appelez `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="f76a7-160">To use camera or access photo gallery, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="f76a7-161">Pour utiliser le micro, teams mobile demande des autorisations lorsque vous appelez `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="f76a7-161">To use mic, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="f76a7-162">Pour inviter l’utilisateur à partager son emplacement sur l’interface de carte, teams mobile demande l’autorisation lorsque vous appelez `getLocation()` :</span><span class="sxs-lookup"><span data-stu-id="f76a7-162">To prompt user to share location on map interface, Teams mobile will ask permission when you call `getLocation()`:</span></span>

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[<span data-ttu-id="f76a7-163">Desktop</span><span class="sxs-lookup"><span data-stu-id="f76a7-163">Desktop</span></span>](#tab/desktop)

![Invite des autorisations des appareils de bureau des onglets](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="f76a7-165">Mobile</span><span class="sxs-lookup"><span data-stu-id="f76a7-165">Mobile</span></span>](#tab/mobile)

![Invite des autorisations de l’appareil mobile onglets](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="f76a7-167">Comportement des autorisations entre les sessions de connexion</span><span class="sxs-lookup"><span data-stu-id="f76a7-167">Permission behavior across login sessions</span></span>

<span data-ttu-id="f76a7-168">Les autorisations d’appareil Native sont stockées pour chaque session de connexion.</span><span class="sxs-lookup"><span data-stu-id="f76a7-168">Native device permissions are stored for every login session.</span></span> <span data-ttu-id="f76a7-169">Cela signifie que si vous vous connectez à une autre instance de Teams (par exemple, sur un autre ordinateur), les autorisations de votre appareil pour vos sessions précédentes ne seront pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="f76a7-169">It means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="f76a7-170">Au lieu de cela, vous devrez redéfinir les autorisations des appareils pour la nouvelle session de connexion.</span><span class="sxs-lookup"><span data-stu-id="f76a7-170">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="f76a7-171">Cela signifie également que si vous vous déconnectez de Teams (ou que vous changez de locataire dans Teams), vos autorisations sur les appareils seront supprimées pour cette session précédente.</span><span class="sxs-lookup"><span data-stu-id="f76a7-171">It also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="f76a7-172">Gardez cela à l’esprit lorsque vous développez des autorisations d’appareil natives : les fonctionnalités natives que vous acceptez pour votre session de connexion _actuelle_ .</span><span class="sxs-lookup"><span data-stu-id="f76a7-172">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
