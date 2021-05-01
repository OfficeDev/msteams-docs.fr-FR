---
title: DevTools pour les onglets Microsoft Teams
description: Décrit comment se rendre à DevTools lors de l'utilisation du Microsoft Teams DevTools
localization_priority: Normal
ms.topic: how-to
keywords: devtools debug mobile chrome desktop client developer tools
ms.openlocfilehash: 70c9a2bab94ceb97e8dcd5cf5cdb98261d037f74
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101827"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="6c9a8-104">DevTools pour les onglets Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6c9a8-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="6c9a8-105">Lorsque Teams est en cours d'exécution dans un navigateur, il est facile d'accéder à DevTools : F12 sur Windows ou Command-Option-I sur MacOS.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="6c9a8-106">DevTools vous donne accès à :</span><span class="sxs-lookup"><span data-stu-id="6c9a8-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="6c9a8-107">Afficher les journaux de la console.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-107">View console logs.</span></span>
1. <span data-ttu-id="6c9a8-108">Afficher ou modifier les requêtes HTML, CSS et réseau pendant l'utilisation.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="6c9a8-109">Ajoutez des points d'arrêt à votre code JavaScript et effectuez un débogage interactif.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="6c9a8-110">La fonctionnalité est disponible uniquement pour les clients de bureau et Android une fois l'aperçu **développeur** activé.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-110">The feature is only available for desktop and Android clients after the **Developer Preview** has been enabled.</span></span> <span data-ttu-id="6c9a8-111">Pour plus d'informations, voir [Comment activer la prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6c9a8-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-on-the-desktop"></a><span data-ttu-id="6c9a8-112">Accéder à DevTools sur le bureau</span><span class="sxs-lookup"><span data-stu-id="6c9a8-112">Access DevTools on the desktop</span></span>

<span data-ttu-id="6c9a8-113">Bien que la version web et la version de bureau de Teams soient presque identiques, il existe certaines différences en ce qui concerne l'authentification.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-113">While the web version and the desktop version of Teams are almost the same, there are some differences concerning authentication.</span></span> <span data-ttu-id="6c9a8-114">Parfois, la seule façon de déterminer ce qui se passe est d'utiliser DevTools.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="6c9a8-115">Pour utiliser DevTools dans le client de bureau, vous devez :</span><span class="sxs-lookup"><span data-stu-id="6c9a8-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="6c9a8-116">Assurez-vous que vous avez activé la [prévisualisation pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="6c9a8-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="6c9a8-117">Ouvrez un onglet pour avoir quelque chose à inspecter avec DevTools.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="6c9a8-118">Ouvrez DevTools de l'une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c9a8-118">Open the DevTools one of the following ways:</span></span>
    * <span data-ttu-id="6c9a8-119">Sur Windows, ouvrez DevTools via l'icône Microsoft Teams dans le bac de bureau :</span><span class="sxs-lookup"><span data-stu-id="6c9a8-119">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span><br>
  <span data-ttu-id="6c9a8-120">![Cliquez avec le bouton droit pour ouvrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span><span class="sxs-lookup"><span data-stu-id="6c9a8-120">![Right-click to open DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span></span>
    * <span data-ttu-id="6c9a8-121">Sur MacOS, cliquez sur l'icône Microsoft Teams dans la station d'accueil.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-121">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="6c9a8-122">L'exemple suivant montre que DevTools ouvre et inspecte une boîte de dialogue de configuration d'onglet :</span><span class="sxs-lookup"><span data-stu-id="6c9a8-122">The following example shows DevTools open and inspecting a tab configuration dialog:</span></span>

   ![Tab et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-device"></a><span data-ttu-id="6c9a8-124">Accéder à DevTools à partir d'un appareil Android</span><span class="sxs-lookup"><span data-stu-id="6c9a8-124">Access DevTools from an Android device</span></span>

<span data-ttu-id="6c9a8-125">Vous pouvez également activer devTools à partir du client Teams Android.</span><span class="sxs-lookup"><span data-stu-id="6c9a8-125">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="6c9a8-126">Pour activer DevTools, vous devez :</span><span class="sxs-lookup"><span data-stu-id="6c9a8-126">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="6c9a8-127">Activez la [prévisualisation pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="6c9a8-127">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="6c9a8-128">Connecter votre appareil sur votre ordinateur de bureau et configurer votre appareil Android pour [le débogage à distance.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="6c9a8-128">Connect your device to your desktop computer, and set up your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="6c9a8-129">Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="6c9a8-129">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="6c9a8-130">Sélectionnez **Inspecter** sous l'onglet que vous souhaitez déboguer, comme dans l'image suivante :</span><span class="sxs-lookup"><span data-stu-id="6c9a8-130">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
