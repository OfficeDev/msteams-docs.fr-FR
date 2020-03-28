---
title: Demander des autorisations de périphérique pour votre onglet Microsoft teams
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui requièrent généralement le consentement de l’utilisateur
keywords: développement d’onglets teams
ms.openlocfilehash: e9dc6c6f177e3a87e2846bcb836cc38601c9a50e
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034035"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="d91ae-104">Demander des autorisations de périphérique pour votre onglet Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="d91ae-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="d91ae-105">Vous souhaiterez peut-être enrichir votre onglet avec des fonctionnalités qui nécessitent l’accès à des fonctionnalités d’appareil natives comme :</span><span class="sxs-lookup"><span data-stu-id="d91ae-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="d91ae-106">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="d91ae-106">Camera</span></span>
* <span data-ttu-id="d91ae-107">Micro</span><span class="sxs-lookup"><span data-stu-id="d91ae-107">Microphone</span></span>
* <span data-ttu-id="d91ae-108">Emplacement</span><span class="sxs-lookup"><span data-stu-id="d91ae-108">Location</span></span>
* <span data-ttu-id="d91ae-109">Notifications</span><span class="sxs-lookup"><span data-stu-id="d91ae-109">Notifications</span></span>

![Écran des paramètres d’autorisations des appareils](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
>
> <span data-ttu-id="d91ae-111">Les fonctionnalités d’appareil Native ne sont actuellement pas prises en charge pour les onglets sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="d91ae-111">Native device functionality is currently not supported for tabs on mobile clients.</span></span>
>
> <span data-ttu-id="d91ae-112">L’API de géolocalisation n’est actuellement pas entièrement prise en charge sur tous les clients de bureau.</span><span class="sxs-lookup"><span data-stu-id="d91ae-112">The geolocation API is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="d91ae-113">Autorisations de l’appareil</span><span class="sxs-lookup"><span data-stu-id="d91ae-113">Device permissions</span></span>

<span data-ttu-id="d91ae-114">L’accès aux autorisations de l’appareil d’un utilisateur vous permet de créer des expériences plus riches, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d91ae-114">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="d91ae-115">Enregistrer et partager des courtes vidéos</span><span class="sxs-lookup"><span data-stu-id="d91ae-115">Record and share short videos</span></span>
* <span data-ttu-id="d91ae-116">Enregistrez des mémos audio courts et enregistrez-les pour une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d91ae-116">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="d91ae-117">Utiliser les informations relatives à l’emplacement de l’utilisateur pour afficher les informations pertinentes</span><span class="sxs-lookup"><span data-stu-id="d91ae-117">Use user location information to display relevant information</span></span>

<span data-ttu-id="d91ae-118">Bien que l’accès à ces fonctionnalités soit standard dans la plupart des navigateurs Web modernes, vous devez informer teams des fonctionnalités que vous souhaitez utiliser en mettant à jour votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="d91ae-118">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="d91ae-119">Cela vous permettra de demander des autorisations, de la même façon que vous le feriez dans un navigateur, tandis que votre application est exécutée sur le client de bureau Teams.</span><span class="sxs-lookup"><span data-stu-id="d91ae-119">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="d91ae-120">Propriétés</span><span class="sxs-lookup"><span data-stu-id="d91ae-120">Properties</span></span>

<span data-ttu-id="d91ae-121">Mettez à jour votre `manifest.json` application en `devicePermissions` ajoutant et en spécifiant les cinq propriétés que vous souhaitez utiliser dans votre application :</span><span class="sxs-lookup"><span data-stu-id="d91ae-121">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="d91ae-122">Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement.</span><span class="sxs-lookup"><span data-stu-id="d91ae-122">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="d91ae-123">Propriété</span><span class="sxs-lookup"><span data-stu-id="d91ae-123">Property</span></span>      | <span data-ttu-id="d91ae-124">Description</span><span class="sxs-lookup"><span data-stu-id="d91ae-124">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="d91ae-125">media</span><span class="sxs-lookup"><span data-stu-id="d91ae-125">media</span></span>         | <span data-ttu-id="d91ae-126">autorisation d’utilisation de l’appareil photo, du microphone et des haut-parleurs</span><span class="sxs-lookup"><span data-stu-id="d91ae-126">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="d91ae-127">géolocalisation</span><span class="sxs-lookup"><span data-stu-id="d91ae-127">geolocation</span></span>   | <span data-ttu-id="d91ae-128">autorisation de retourner l’emplacement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d91ae-128">permission to return the user's location</span></span>      |
| <span data-ttu-id="d91ae-129">notifications</span><span class="sxs-lookup"><span data-stu-id="d91ae-129">notifications</span></span> | <span data-ttu-id="d91ae-130">autorisation d’envoyer les notifications de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d91ae-130">permission to send the user notifications</span></span>      |
| <span data-ttu-id="d91ae-131">midi</span><span class="sxs-lookup"><span data-stu-id="d91ae-131">midi</span></span>          | <span data-ttu-id="d91ae-132">autorisation d’envoyer et de recevoir des informations midi à partir d’un instrument musical numérique</span><span class="sxs-lookup"><span data-stu-id="d91ae-132">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="d91ae-133">openExternal</span><span class="sxs-lookup"><span data-stu-id="d91ae-133">openExternal</span></span>  | <span data-ttu-id="d91ae-134">autorisation d’ouvrir des liens dans des applications externes</span><span class="sxs-lookup"><span data-stu-id="d91ae-134">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="d91ae-135">Vérification des autorisations à partir de votre onglet</span><span class="sxs-lookup"><span data-stu-id="d91ae-135">Checking permissions from your tab</span></span>

<span data-ttu-id="d91ae-136">Une fois que vous `devicePermissions` avez ajouté à votre manifeste d’application, vous pouvez vérifier les autorisations à l’aide de l’API HTML5 « autorisations » sans générer d’invite.</span><span class="sxs-lookup"><span data-stu-id="d91ae-136">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="d91ae-137">Demander à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d91ae-137">Prompting the user</span></span>

<span data-ttu-id="d91ae-138">Pour afficher une invite permettant d’obtenir le consentement pour accéder aux autorisations des appareils, vous devez tirer parti de l’API HTML5 appropriée.</span><span class="sxs-lookup"><span data-stu-id="d91ae-138">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="d91ae-139">Par exemple, pour inviter l’utilisateur à accéder à sa caméra, vous devez appeler`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="d91ae-139">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="d91ae-140">La géolocalisation affiche une invite d’autorisation lorsque vous appelez`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="d91ae-140">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="d91ae-141">Les notifications invitent l’utilisateur lorsque vous appelez`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="d91ae-141">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Invite des autorisations des appareils de tabulation](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="d91ae-143">Comportement des autorisations entre les sessions de connexion</span><span class="sxs-lookup"><span data-stu-id="d91ae-143">Permission behavior across login sessions</span></span>

<span data-ttu-id="d91ae-144">Les autorisations natives des appareils sont stockées par session de connexion.</span><span class="sxs-lookup"><span data-stu-id="d91ae-144">Native device permissions are stored per login session.</span></span> <span data-ttu-id="d91ae-145">Cela signifie que si vous vous connectez à une autre instance de Teams (par exemple, sur un autre ordinateur), les autorisations de votre appareil pour vos sessions précédentes ne seront pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="d91ae-145">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="d91ae-146">Au lieu de cela, vous devrez redéfinir les autorisations des appareils pour la nouvelle session de connexion.</span><span class="sxs-lookup"><span data-stu-id="d91ae-146">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="d91ae-147">Cela signifie également que si vous vous déconnectez de Teams (ou que vous changez de locataire dans Teams), vos autorisations sur les appareils seront supprimées pour cette session précédente.</span><span class="sxs-lookup"><span data-stu-id="d91ae-147">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="d91ae-148">Gardez cela à l’esprit lorsque vous développez des autorisations d’appareil natives : les fonctionnalités natives que vous acceptez pour votre session de connexion _actuelle_ .</span><span class="sxs-lookup"><span data-stu-id="d91ae-148">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
