---
title: Demander des autorisations de périphérique pour votre onglet Microsoft teams
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui requièrent généralement le consentement de l’utilisateur
keywords: développement d’onglets teams
ms.openlocfilehash: e69c7540730307e62035c48ac64cd977419ea5f2
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434553"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="bd41b-104">Demander des autorisations de périphérique pour votre onglet Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="bd41b-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="bd41b-105">Vous souhaiterez peut-être enrichir votre onglet avec des fonctionnalités qui nécessitent l’accès à des fonctionnalités d’appareil natives comme :</span><span class="sxs-lookup"><span data-stu-id="bd41b-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="bd41b-106">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="bd41b-106">Camera</span></span>
> * <span data-ttu-id="bd41b-107">Micro</span><span class="sxs-lookup"><span data-stu-id="bd41b-107">Microphone</span></span>
> * <span data-ttu-id="bd41b-108">Emplacement</span><span class="sxs-lookup"><span data-stu-id="bd41b-108">Location</span></span>
> * <span data-ttu-id="bd41b-109">Notifications</span><span class="sxs-lookup"><span data-stu-id="bd41b-109">Notifications</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="bd41b-110">Actuellement, le client mobile teams prend en charge `camera` et `location` via les fonctionnalités de périphérique natives, et est disponible sur toutes les constructions d’application, y compris les onglets.</span><span class="sxs-lookup"><span data-stu-id="bd41b-110">Currently, Teams mobile client only supports `camera` and `location`  through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="bd41b-111">La prise en charge de `camera` la capture d’image est activée par l' [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-).</span><span class="sxs-lookup"><span data-stu-id="bd41b-111">Support for `camera` image capture is enabled by the [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-).</span></span>
> * <span data-ttu-id="bd41b-112">L' [**API de géolocalisation**](../../resources/schema/manifest-schema.md#devicepermissions) n’est actuellement pas entièrement prise en charge sur tous les clients de bureau.</span><span class="sxs-lookup"><span data-stu-id="bd41b-112">The [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="bd41b-113">Autorisations de l’appareil</span><span class="sxs-lookup"><span data-stu-id="bd41b-113">Device permissions</span></span>

<span data-ttu-id="bd41b-114">L’accès aux autorisations de l’appareil d’un utilisateur vous permet de créer des expériences plus riches, par exemple :</span><span class="sxs-lookup"><span data-stu-id="bd41b-114">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="bd41b-115">Enregistrer et partager des courtes vidéos</span><span class="sxs-lookup"><span data-stu-id="bd41b-115">Record and share short videos</span></span>
* <span data-ttu-id="bd41b-116">Enregistrez des mémos audio courts et enregistrez-les pour une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bd41b-116">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="bd41b-117">Utiliser les informations relatives à l’emplacement de l’utilisateur pour afficher les informations pertinentes</span><span class="sxs-lookup"><span data-stu-id="bd41b-117">Use user location information to display relevant information</span></span>

<span data-ttu-id="bd41b-118">Bien que l’accès à ces fonctionnalités soit standard dans la plupart des navigateurs Web modernes, vous devez informer teams des fonctionnalités que vous souhaitez utiliser en mettant à jour votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="bd41b-118">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="bd41b-119">Cela vous permettra de demander des autorisations, de la même façon que vous le feriez dans un navigateur, tandis que votre application est exécutée sur le client de bureau Teams.</span><span class="sxs-lookup"><span data-stu-id="bd41b-119">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="bd41b-120">Gérer les autorisations</span><span class="sxs-lookup"><span data-stu-id="bd41b-120">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="bd41b-121">Desktop</span><span class="sxs-lookup"><span data-stu-id="bd41b-121">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="bd41b-122">Ouvrez Teams.</span><span class="sxs-lookup"><span data-stu-id="bd41b-122">Open Teams.</span></span>
1. <span data-ttu-id="bd41b-123">Dans le coin supérieur droit de la fenêtre, sélectionnez l’icône de votre profil.</span><span class="sxs-lookup"><span data-stu-id="bd41b-123">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="bd41b-124">Sélectionnez **Settings**  ->  **autorisations** des paramètres dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="bd41b-124">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="bd41b-125">Choisissez les paramètres de votre choix.</span><span class="sxs-lookup"><span data-stu-id="bd41b-125">Choose your desired settings.</span></span>

![Écran des paramètres de bureau des autorisations de périphérique](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="bd41b-127">Mobile</span><span class="sxs-lookup"><span data-stu-id="bd41b-127">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="bd41b-128">Ouvrez Teams.</span><span class="sxs-lookup"><span data-stu-id="bd41b-128">Open Teams.</span></span>
1. <span data-ttu-id="bd41b-129">Dans le coin supérieur gauche de l’écran, sélectionnez l’icône de menu &#9776;.</span><span class="sxs-lookup"><span data-stu-id="bd41b-129">In the upper left corner of the screen, select the &#9776; menu icon.</span></span>
1. <span data-ttu-id="bd41b-130">Sélectionnez **paramètres**  ->  **Devices**.</span><span class="sxs-lookup"><span data-stu-id="bd41b-130">Select **Settings** -> **Devices**.</span></span>
1. <span data-ttu-id="bd41b-131">Choisissez les paramètres de votre choix.</span><span class="sxs-lookup"><span data-stu-id="bd41b-131">Choose your desired settings.</span></span>

![Écran des paramètres mobiles des autorisations de l’appareil](../../assets/images/tabs/mobile-device-permissions-screen.png)

---

## <a name="properties"></a><span data-ttu-id="bd41b-133">Propriétés</span><span class="sxs-lookup"><span data-stu-id="bd41b-133">Properties</span></span>

<span data-ttu-id="bd41b-134">Mettez à jour votre application `manifest.json` en ajoutant `devicePermissions` et en spécifiant les cinq propriétés que vous souhaitez utiliser dans votre application :</span><span class="sxs-lookup"><span data-stu-id="bd41b-134">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

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
> <span data-ttu-id="bd41b-135">Le support est également utilisé pour les autorisations d’appareil photo dans mobile.</span><span class="sxs-lookup"><span data-stu-id="bd41b-135">Media is also used for camera permissions in mobile.</span></span>

<span data-ttu-id="bd41b-136">Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement.</span><span class="sxs-lookup"><span data-stu-id="bd41b-136">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="bd41b-137">Propriété</span><span class="sxs-lookup"><span data-stu-id="bd41b-137">Property</span></span>      | <span data-ttu-id="bd41b-138">Description</span><span class="sxs-lookup"><span data-stu-id="bd41b-138">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="bd41b-139">panne</span><span class="sxs-lookup"><span data-stu-id="bd41b-139">media</span></span>         | <span data-ttu-id="bd41b-140">autorisation d’utilisation de l’appareil photo, du microphone et des haut-parleurs</span><span class="sxs-lookup"><span data-stu-id="bd41b-140">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="bd41b-141">géolocalisation</span><span class="sxs-lookup"><span data-stu-id="bd41b-141">geolocation</span></span>   | <span data-ttu-id="bd41b-142">autorisation de retourner l’emplacement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="bd41b-142">permission to return the user's location</span></span>      |
| <span data-ttu-id="bd41b-143">notifications</span><span class="sxs-lookup"><span data-stu-id="bd41b-143">notifications</span></span> | <span data-ttu-id="bd41b-144">autorisation d’envoyer les notifications de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="bd41b-144">permission to send the user notifications</span></span>      |
| <span data-ttu-id="bd41b-145">midi</span><span class="sxs-lookup"><span data-stu-id="bd41b-145">midi</span></span>          | <span data-ttu-id="bd41b-146">autorisation d’envoyer et de recevoir des informations midi à partir d’un instrument musical numérique</span><span class="sxs-lookup"><span data-stu-id="bd41b-146">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="bd41b-147">openExternal</span><span class="sxs-lookup"><span data-stu-id="bd41b-147">openExternal</span></span>  | <span data-ttu-id="bd41b-148">autorisation d’ouvrir des liens dans des applications externes</span><span class="sxs-lookup"><span data-stu-id="bd41b-148">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="bd41b-149">Vérification des autorisations à partir de votre onglet</span><span class="sxs-lookup"><span data-stu-id="bd41b-149">Checking permissions from your tab</span></span>

<span data-ttu-id="bd41b-150">Une fois que vous avez ajouté `devicePermissions` à votre manifeste d’application, vous pouvez vérifier les autorisations à l’aide de l’API HTML5 « autorisations » sans générer d’invite.</span><span class="sxs-lookup"><span data-stu-id="bd41b-150">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="bd41b-151">Demander à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="bd41b-151">Prompting the user</span></span>

<span data-ttu-id="bd41b-152">Pour afficher une invite permettant d’obtenir le consentement pour accéder aux autorisations des appareils, vous devez tirer parti de l’API HTML5 ou teams appropriée.</span><span class="sxs-lookup"><span data-stu-id="bd41b-152">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> <span data-ttu-id="bd41b-153">Par exemple, pour inviter l’utilisateur à accéder à sa caméra, vous devez appeler`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="bd41b-153">For example, in order to prompt the user to access their camera you need to call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="bd41b-154">Pour utiliser l’appareil photo sur le bureau ou sur le Web, teams affiche une invite d’autorisation lorsque vous appelez getUserMedia</span><span class="sxs-lookup"><span data-stu-id="bd41b-154">To use camera on desktop or web, Teams will show a permission prompt when you call getUserMedia</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="bd41b-155">Pour capturer une image sur mobile, teams mobile demande des autorisations lorsqu’il est appelé captureImage ()</span><span class="sxs-lookup"><span data-stu-id="bd41b-155">To capture image on mobile, Teams mobile will ask for permission when called captureImage()</span></span>

```Typescript
function captureImage(callback: (error: SdkError, files: File[]) => void)
```

<span data-ttu-id="bd41b-156">Les notifications invitent l’utilisateur lorsque vous appelez`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="bd41b-156">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Invite des autorisations des appareils de tabulation](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="bd41b-158">Comportement des autorisations entre les sessions de connexion</span><span class="sxs-lookup"><span data-stu-id="bd41b-158">Permission behavior across login sessions</span></span>

<span data-ttu-id="bd41b-159">Les autorisations natives des appareils sont stockées par session de connexion.</span><span class="sxs-lookup"><span data-stu-id="bd41b-159">Native device permissions are stored per login session.</span></span> <span data-ttu-id="bd41b-160">Cela signifie que si vous vous connectez à une autre instance de Teams (par exemple, sur un autre ordinateur), les autorisations de votre appareil pour vos sessions précédentes ne seront pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="bd41b-160">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="bd41b-161">Au lieu de cela, vous devrez redéfinir les autorisations des appareils pour la nouvelle session de connexion.</span><span class="sxs-lookup"><span data-stu-id="bd41b-161">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="bd41b-162">Cela signifie également que si vous vous déconnectez de Teams (ou que vous changez de locataire dans Teams), vos autorisations sur les appareils seront supprimées pour cette session précédente.</span><span class="sxs-lookup"><span data-stu-id="bd41b-162">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="bd41b-163">Gardez cela à l’esprit lorsque vous développez des autorisations d’appareil natives : les fonctionnalités natives que vous acceptez pour votre session de connexion _actuelle_ .</span><span class="sxs-lookup"><span data-stu-id="bd41b-163">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
