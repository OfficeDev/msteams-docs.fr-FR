---
title: Demander des autorisations de périphérique pour votre onglet Microsoft teams
description: Comment mettre à jour le manifeste de votre application afin de demander l’accès aux fonctionnalités natives qui requièrent généralement le consentement de l’utilisateur
keywords: développement d’onglets teams
ms.openlocfilehash: 454466ff17ecf275f6ae6c7413df8e117335f3c8
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673540"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="10774-104">Demander des autorisations de périphérique pour votre onglet Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="10774-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="10774-105">Vous souhaiterez peut-être enrichir votre onglet avec des fonctionnalités qui nécessitent l’accès à des fonctionnalités d’appareil natives comme :</span><span class="sxs-lookup"><span data-stu-id="10774-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="10774-106">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="10774-106">Camera</span></span>
* <span data-ttu-id="10774-107">Micro</span><span class="sxs-lookup"><span data-stu-id="10774-107">Microphone</span></span>
* <span data-ttu-id="10774-108">L’emplacement</span><span class="sxs-lookup"><span data-stu-id="10774-108">Location</span></span>
* <span data-ttu-id="10774-109">Notifications</span><span class="sxs-lookup"><span data-stu-id="10774-109">Notifications</span></span>

![Écran des paramètres d’autorisations des appareils](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> <span data-ttu-id="10774-111">La fonctionnalité d’appareil Native n’est actuellement pas prise en charge pour les onglets sur les clients mobiles, mais la prise en charge complète sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="10774-111">Native device functionality is currently not supported for tabs on mobile clients but full support is coming soon.</span></span> <span data-ttu-id="10774-112">Pour vous préparer à ce changement, suivez les [instructions pour les onglets sur mobile](~/tabs/design/tabs-mobile.md) lors de la création des onglets.</span><span class="sxs-lookup"><span data-stu-id="10774-112">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="10774-113">Les applications personnelles (onglets statiques) sont actuellement disponibles dans l’Aperçu pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="10774-113">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="10774-114">Lorsque la prise en charge complète des onglets est publiée :</span><span class="sxs-lookup"><span data-stu-id="10774-114">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="10774-115">Tous les onglets seront toujours disponibles sur mobile</span><span class="sxs-lookup"><span data-stu-id="10774-115">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="10774-116">Votre `contentUrl` **sera chargé dans le client teams mobile**.</span><span class="sxs-lookup"><span data-stu-id="10774-116">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="10774-117">Pour les onglets canal/groupe, les utilisateurs peuvent toujours ouvrir l’onglet dans un navigateur `websiteUrl`distinct via votre `contentUrl` , mais votre sera chargé en premier.</span><span class="sxs-lookup"><span data-stu-id="10774-117">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>  

## <a name="device-permissions"></a><span data-ttu-id="10774-118">Autorisations de l’appareil</span><span class="sxs-lookup"><span data-stu-id="10774-118">Device permissions</span></span>

<span data-ttu-id="10774-119">L’accès aux autorisations de l’appareil d’un utilisateur vous permet de créer des expériences plus riches, par exemple :</span><span class="sxs-lookup"><span data-stu-id="10774-119">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="10774-120">Enregistrer et partager des courtes vidéos</span><span class="sxs-lookup"><span data-stu-id="10774-120">Record and share short videos</span></span>
* <span data-ttu-id="10774-121">Enregistrez des mémos audio courts et enregistrez-les pour une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="10774-121">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="10774-122">Utiliser les informations relatives à l’emplacement de l’utilisateur pour afficher les informations pertinentes</span><span class="sxs-lookup"><span data-stu-id="10774-122">Use user location information to display relevant information</span></span>

<span data-ttu-id="10774-123">Bien que l’accès à ces fonctionnalités soit standard dans la plupart des navigateurs Web modernes, vous devez informer teams des fonctionnalités que vous souhaitez utiliser en mettant à jour votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="10774-123">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="10774-124">Cela vous permettra de demander des autorisations, de la même façon que vous le feriez dans un navigateur, tandis que votre application est exécutée sur le client de bureau Teams.</span><span class="sxs-lookup"><span data-stu-id="10774-124">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="10774-125">Propriétés</span><span class="sxs-lookup"><span data-stu-id="10774-125">Properties</span></span>

<span data-ttu-id="10774-126">Mettez à jour votre `manifest.json` application en `devicePermissions` ajoutant et en spécifiant les cinq propriétés que vous souhaitez utiliser dans votre application :</span><span class="sxs-lookup"><span data-stu-id="10774-126">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="10774-127">Chaque propriété vous permet d’inviter l’utilisateur à demander son consentement.</span><span class="sxs-lookup"><span data-stu-id="10774-127">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="10774-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="10774-128">Property</span></span>      | <span data-ttu-id="10774-129">Description</span><span class="sxs-lookup"><span data-stu-id="10774-129">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="10774-130">panne</span><span class="sxs-lookup"><span data-stu-id="10774-130">media</span></span>         | <span data-ttu-id="10774-131">autorisation d’utilisation de l’appareil photo, du microphone et des haut-parleurs</span><span class="sxs-lookup"><span data-stu-id="10774-131">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="10774-132">géolocalisation</span><span class="sxs-lookup"><span data-stu-id="10774-132">geolocation</span></span>   | <span data-ttu-id="10774-133">autorisation de retourner l’emplacement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="10774-133">permission to return the user's location</span></span>      |
| <span data-ttu-id="10774-134">notifications</span><span class="sxs-lookup"><span data-stu-id="10774-134">notifications</span></span> | <span data-ttu-id="10774-135">autorisation d’envoyer les notifications de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="10774-135">permission to send the user notifications</span></span>      |
| <span data-ttu-id="10774-136">midi</span><span class="sxs-lookup"><span data-stu-id="10774-136">midi</span></span>          | <span data-ttu-id="10774-137">autorisation d’envoyer et de recevoir des informations midi à partir d’un instrument musical numérique</span><span class="sxs-lookup"><span data-stu-id="10774-137">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="10774-138">openExternal</span><span class="sxs-lookup"><span data-stu-id="10774-138">openExternal</span></span>  | <span data-ttu-id="10774-139">autorisation d’ouvrir des liens dans des applications externes</span><span class="sxs-lookup"><span data-stu-id="10774-139">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="10774-140">Vérification des autorisations à partir de votre onglet</span><span class="sxs-lookup"><span data-stu-id="10774-140">Checking permissions from your tab</span></span>

<span data-ttu-id="10774-141">Une fois que vous `devicePermissions` avez ajouté à votre manifeste d’application, vous pouvez vérifier les autorisations à l’aide de l’API HTML5 « autorisations » sans générer d’invite.</span><span class="sxs-lookup"><span data-stu-id="10774-141">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="10774-142">Demander à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="10774-142">Prompting the user</span></span>

<span data-ttu-id="10774-143">Pour afficher une invite permettant d’obtenir le consentement pour accéder aux autorisations des appareils, vous devez tirer parti de l’API HTML5 appropriée.</span><span class="sxs-lookup"><span data-stu-id="10774-143">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="10774-144">Par exemple, pour inviter l’utilisateur à accéder à sa caméra, vous devez appeler`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="10774-144">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="10774-145">La géolocalisation affiche une invite d’autorisation lorsque vous appelez`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="10774-145">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="10774-146">Les notifications invitent l’utilisateur lorsque vous appelez`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="10774-146">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Invite des autorisations des appareils de tabulation](~/assets/images/tabs/device-permissions-prompt.png)