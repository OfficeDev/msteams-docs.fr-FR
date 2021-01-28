---
title: Demander des autorisations d’appareil pour votre onglet
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui nécessitent généralement le consentement de l’utilisateur
ms.topic: how-to
keywords: développement d’onglets teams
ms.openlocfilehash: a2893fb2905584eac4b398287d431f406c23b12b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014529"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="e67e4-104">Demander des autorisations d’appareil pour votre onglet Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e67e4-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="e67e4-105">Vous souhaitez peut-être enrichir votre onglet avec des fonctionnalités qui nécessitent l’accès aux fonctionnalités natives de l’appareil, telles que :</span><span class="sxs-lookup"><span data-stu-id="e67e4-105">You might want to enrich your tab with features that require access to native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="e67e4-106">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="e67e4-106">Camera</span></span>
> * <span data-ttu-id="e67e4-107">Microphone</span><span class="sxs-lookup"><span data-stu-id="e67e4-107">Microphone</span></span>
> * <span data-ttu-id="e67e4-108">Lieu</span><span class="sxs-lookup"><span data-stu-id="e67e4-108">Location</span></span>
> * <span data-ttu-id="e67e4-109">Notifications</span><span class="sxs-lookup"><span data-stu-id="e67e4-109">Notifications</span></span>

> [!NOTE]
> <span data-ttu-id="e67e4-110">Pour intégrer des fonctionnalités d’appareil photo et d’image dans votre application mobile Microsoft Teams, voir fonctionnalités d’appareil photo et [d’image dans Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="e67e4-110">To integrate camera and image capabilities within your Microsoft Teams mobile app, see [Camera and image capabilities in Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="e67e4-111">Pour l’instant, le client mobile Teams prend uniquement en charge l’accès aux fonctionnalités d’appareils natifs, ainsi qu’aux fonctionnalités de l’appareil natif, et il est disponible sur toutes les constructions d’application, y compris `camera` `gallery` les `mic` `location` onglets.</span><span class="sxs-lookup"><span data-stu-id="e67e4-111">At present, Teams mobile client only supports access to `camera`, `gallery`, `mic`, and `location` through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="e67e4-112">Prise en `camera` charge de , et est activée par le biais de `gallery` `mic` [**l’API selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="e67e4-112">Support for `camera`, `gallery`, and `mic` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="e67e4-113">Pour une capture d’image unique, vous pouvez utiliser [**l’API captureImage.**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e67e4-113">For single image capture you may use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span></span>
> * <span data-ttu-id="e67e4-114">La prise `location` en charge est activée via [**l’API getLocation.**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e67e4-114">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="e67e4-115">Il est recommandé d’utiliser cette API comme API de [**géolocalisation**](../../resources/schema/manifest-schema.md#devicepermissions) n’est actuellement pas entièrement prise en charge sur tous les clients de bureau.</span><span class="sxs-lookup"><span data-stu-id="e67e4-115">It's recommended you use this API as [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="e67e4-116">Autorisations de l’appareil</span><span class="sxs-lookup"><span data-stu-id="e67e4-116">Device permissions</span></span>

<span data-ttu-id="e67e4-117">L’accès aux autorisations d’appareil d’un utilisateur vous permet de créer des expériences beaucoup plus riches, par exemple :</span><span class="sxs-lookup"><span data-stu-id="e67e4-117">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="e67e4-118">Enregistrer et partager de courtes vidéos</span><span class="sxs-lookup"><span data-stu-id="e67e4-118">Record and share short videos</span></span>
* <span data-ttu-id="e67e4-119">Enregistrez de courtes mémos audio et enregistrez-les pour plus tard</span><span class="sxs-lookup"><span data-stu-id="e67e4-119">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="e67e4-120">Utiliser les informations d’emplacement de l’utilisateur pour afficher les informations pertinentes</span><span class="sxs-lookup"><span data-stu-id="e67e4-120">Use user location information to display relevant information</span></span>

<span data-ttu-id="e67e4-121">Bien que l’accès à ces fonctionnalités soit standard dans la plupart des navigateurs web modernes, vous devez faire savoir à Teams les fonctionnalités que vous souhaitez utiliser en mettant à jour votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="e67e4-121">While access to these features is standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="e67e4-122">Cela vous permettra de demander des autorisations, comme vous le feriez dans un navigateur, pendant que votre application est en cours d’exécution sur le client de bureau Teams.</span><span class="sxs-lookup"><span data-stu-id="e67e4-122">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="e67e4-123">Gérer les autorisations</span><span class="sxs-lookup"><span data-stu-id="e67e4-123">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e67e4-124">Desktop</span><span class="sxs-lookup"><span data-stu-id="e67e4-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="e67e4-125">Ouvrez Teams.</span><span class="sxs-lookup"><span data-stu-id="e67e4-125">Open Teams.</span></span>
1. <span data-ttu-id="e67e4-126">Dans le coin supérieur droit de la fenêtre, sélectionnez l’icône de votre profil.</span><span class="sxs-lookup"><span data-stu-id="e67e4-126">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="e67e4-127">Sélectionnez **Les**  ->  **autorisations des paramètres** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="e67e4-127">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="e67e4-128">Choisissez les paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="e67e4-128">Choose your desired settings.</span></span>

![Écran des paramètres de bureau des autorisations d’appareil](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="e67e4-130">Mobile</span><span class="sxs-lookup"><span data-stu-id="e67e4-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="e67e4-131">Ouvrez Teams.</span><span class="sxs-lookup"><span data-stu-id="e67e4-131">Open Teams.</span></span>
1. <span data-ttu-id="e67e4-132">Go to **Settings**  ->  **App Permissions**.</span><span class="sxs-lookup"><span data-stu-id="e67e4-132">Go to **Settings** -> **App Permissions**.</span></span>
1. <span data-ttu-id="e67e4-133">Sélectionnez l’application dont vous avez besoin pour choisir les paramètres.</span><span class="sxs-lookup"><span data-stu-id="e67e4-133">Select the app you need to choose settings for.</span></span>
1. <span data-ttu-id="e67e4-134">Choisissez les paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="e67e4-134">Choose your desired settings.</span></span>

![Écran des paramètres mobiles des autorisations d’appareil](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a><span data-ttu-id="e67e4-136">Propriétés</span><span class="sxs-lookup"><span data-stu-id="e67e4-136">Properties</span></span>

<span data-ttu-id="e67e4-137">Mettez à jour les propriétés de votre application en ajoutant et en spécifiant les cinq propriétés que vous souhaitez `manifest.json` utiliser dans votre application `devicePermissions` :</span><span class="sxs-lookup"><span data-stu-id="e67e4-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

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
> <span data-ttu-id="e67e4-138">Le média est également utilisé pour les autorisations d’appareil photo sur mobile.</span><span class="sxs-lookup"><span data-stu-id="e67e4-138">Media is also used for camera permissions on mobile.</span></span>

<span data-ttu-id="e67e4-139">Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement :</span><span class="sxs-lookup"><span data-stu-id="e67e4-139">Each property will allow you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="e67e4-140">Propriété</span><span class="sxs-lookup"><span data-stu-id="e67e4-140">Property</span></span>      | <span data-ttu-id="e67e4-141">Description</span><span class="sxs-lookup"><span data-stu-id="e67e4-141">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="e67e4-142">media</span><span class="sxs-lookup"><span data-stu-id="e67e4-142">media</span></span>         | <span data-ttu-id="e67e4-143">autorisation d’utiliser la caméra, le microphone, les haut-parleurs et l’accès à la galerie multimédia</span><span class="sxs-lookup"><span data-stu-id="e67e4-143">permission to use the camera, microphone, speakers, and access media gallery</span></span> |
| <span data-ttu-id="e67e4-144">géolocalisation</span><span class="sxs-lookup"><span data-stu-id="e67e4-144">geolocation</span></span>   | <span data-ttu-id="e67e4-145">autorisation de renvoyer l’emplacement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e67e4-145">permission to return the user's location</span></span>      |
| <span data-ttu-id="e67e4-146">notifications</span><span class="sxs-lookup"><span data-stu-id="e67e4-146">notifications</span></span> | <span data-ttu-id="e67e4-147">autorisation d’envoyer des notifications à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e67e4-147">permission to send the user notifications</span></span>      |
| <span data-ttu-id="e67e4-148">midi</span><span class="sxs-lookup"><span data-stu-id="e67e4-148">midi</span></span>          | <span data-ttu-id="e67e4-149">autorisation d’envoyer et de recevoir des informations midi à partir d’un instrument de musique numérique</span><span class="sxs-lookup"><span data-stu-id="e67e4-149">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="e67e4-150">openExternal</span><span class="sxs-lookup"><span data-stu-id="e67e4-150">openExternal</span></span>  | <span data-ttu-id="e67e4-151">autorisation d’ouvrir des liens dans des applications externes</span><span class="sxs-lookup"><span data-stu-id="e67e4-151">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="e67e4-152">Vérification des autorisations à partir de votre onglet</span><span class="sxs-lookup"><span data-stu-id="e67e4-152">Checking permissions from your tab</span></span>

<span data-ttu-id="e67e4-153">Une fois que vous avez ajouté le manifeste de votre application, vous pouvez vérifier les autorisations à l’aide de l’API HTML5 « autorisations » sans provoquer `devicePermissions` d’invite.</span><span class="sxs-lookup"><span data-stu-id="e67e4-153">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="e67e4-154">Invite de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e67e4-154">Prompting the user</span></span>

<span data-ttu-id="e67e4-155">Pour afficher une invite pour obtenir l’autorisation d’accéder aux autorisations d’appareil, vous devez utiliser l’API HTML5 ou Teams appropriée.</span><span class="sxs-lookup"><span data-stu-id="e67e4-155">To show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> 

<span data-ttu-id="e67e4-156">Par exemple, pour demander à l’utilisateur d’accéder à son emplacement, vous devez appeler `getCurrentPosition` :</span><span class="sxs-lookup"><span data-stu-id="e67e4-156">For example, to prompt the user to access their location you need to call `getCurrentPosition`:</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="e67e4-157">Pour utiliser l’appareil photo sur ordinateur de bureau ou web, Teams affiche une invite d’autorisation lorsque vous appelez `getUserMedia` :</span><span class="sxs-lookup"><span data-stu-id="e67e4-157">To use the camera on desktop or web, Teams will show a permission prompt when you call `getUserMedia`:</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="e67e4-158">Pour capturer l’image sur un appareil mobile, Teams mobile vous demandera l’autorisation lorsque vous appelez `captureImage()` :</span><span class="sxs-lookup"><span data-stu-id="e67e4-158">To capture the image on mobile, Teams mobile will ask for permission when you call `captureImage()`:</span></span>

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

<span data-ttu-id="e67e4-159">Les notifications inviteront l’utilisateur à appeler `requestPermission` :</span><span class="sxs-lookup"><span data-stu-id="e67e4-159">Notifications will prompt the user when you call `requestPermission`:</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

<span data-ttu-id="e67e4-160">Pour utiliser l’appareil photo ou accéder à la galerie de photos, Teams Mobile demande l’autorisation lorsque vous appelez `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="e67e4-160">To use camera or access photo gallery, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="e67e4-161">Pour utiliser le micro, Teams mobile demande l’autorisation lorsque vous appelez `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="e67e4-161">To use mic, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="e67e4-162">Pour demander à l’utilisateur de partager un emplacement sur l’interface de carte, Teams mobile demandera l’autorisation lorsque vous appelez `getLocation()` :</span><span class="sxs-lookup"><span data-stu-id="e67e4-162">To prompt user to share location on map interface, Teams mobile will ask permission when you call `getLocation()`:</span></span>

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[<span data-ttu-id="e67e4-163">Desktop</span><span class="sxs-lookup"><span data-stu-id="e67e4-163">Desktop</span></span>](#tab/desktop)

![Invite d’autorisations d’appareil de bureau Onglets](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="e67e4-165">Mobile</span><span class="sxs-lookup"><span data-stu-id="e67e4-165">Mobile</span></span>](#tab/mobile)

![Invite d’autorisations d’appareil mobile Onglets](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="e67e4-167">Comportement des autorisations entre les sessions de connexion</span><span class="sxs-lookup"><span data-stu-id="e67e4-167">Permission behavior across login sessions</span></span>

<span data-ttu-id="e67e4-168">Les autorisations d’appareil natives sont stockées pour chaque session de connexion.</span><span class="sxs-lookup"><span data-stu-id="e67e4-168">Native device permissions are stored for every login session.</span></span> <span data-ttu-id="e67e4-169">Cela signifie que si vous vous connectez à une autre instance de Teams (par exemple, sur un autre ordinateur), les autorisations de votre appareil à partir de vos sessions précédentes ne seront pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="e67e4-169">It means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="e67e4-170">Au lieu de cela, vous devrez consentir à nouveau aux autorisations d’appareil pour la nouvelle session de connexion.</span><span class="sxs-lookup"><span data-stu-id="e67e4-170">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="e67e4-171">Cela signifie également que, si vous vous déconnectez de Teams (ou que vous changez de client dans Teams), les autorisations de votre appareil seront supprimées pour cette session de connexion précédente.</span><span class="sxs-lookup"><span data-stu-id="e67e4-171">It also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="e67e4-172">Gardez ceci à l’esprit lorsque vous développez des autorisations d’appareil natives : les fonctionnalités natives que vous consentez sont uniquement pour votre session _de_ connexion actuelle.</span><span class="sxs-lookup"><span data-stu-id="e67e4-172">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
