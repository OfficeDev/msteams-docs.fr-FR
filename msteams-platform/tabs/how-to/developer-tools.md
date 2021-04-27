---
title: DevTools pour les onglets Microsoft Teams
description: Décrit comment se rendre à DevTools lors de l'utilisation du client de bureau Microsoft Teams
localization_priority: Normal
ms.topic: how-to
keywords: devtools debug mobile chrome desktop client developer tools
ms.openlocfilehash: 663368c96f4c75953dde2ce1160314eca0917e2a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020372"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="756cf-104">DevTools pour les onglets Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="756cf-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="756cf-105">Lorsque Teams s'exécute dans un navigateur, il est facile d'accéder aux DevTools : F12 sur Windows ou Command-Option-I sur MacOS.</span><span class="sxs-lookup"><span data-stu-id="756cf-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="756cf-106">DevTools vous donne accès à :</span><span class="sxs-lookup"><span data-stu-id="756cf-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="756cf-107">Afficher les journaux de la console.</span><span class="sxs-lookup"><span data-stu-id="756cf-107">View console logs.</span></span>
1. <span data-ttu-id="756cf-108">Afficher ou modifier les requêtes HTML, CSS et réseau pendant l'utilisation.</span><span class="sxs-lookup"><span data-stu-id="756cf-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="756cf-109">Ajoutez des points d'arrêt à votre code JavaScript et effectuez un débogage interactif.</span><span class="sxs-lookup"><span data-stu-id="756cf-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="756cf-110">La fonctionnalité est disponible uniquement pour les clients de bureau et Android une fois l'aperçu **développeur** activé.</span><span class="sxs-lookup"><span data-stu-id="756cf-110">The feature is only available for desktop and Android clients after the **Developer Preview** has been enabled.</span></span> <span data-ttu-id="756cf-111">Pour plus d'informations, voir [Comment activer la prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="756cf-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-in-the-desktop"></a><span data-ttu-id="756cf-112">Accéder à DevTools dans le Bureau</span><span class="sxs-lookup"><span data-stu-id="756cf-112">Access DevTools in the Desktop</span></span>

<span data-ttu-id="756cf-113">Bien que la version web et la version de bureau de Teams soient presque identiques, il existe certaines différences concernant l'authentification.</span><span class="sxs-lookup"><span data-stu-id="756cf-113">While the web version and the desktop version of Teams are almost the same, there are some differences concerning authentication.</span></span> <span data-ttu-id="756cf-114">Parfois, la seule façon de déterminer ce qui se passe est d'utiliser DevTools.</span><span class="sxs-lookup"><span data-stu-id="756cf-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="756cf-115">Pour utiliser DevTools dans le client de bureau, vous devez :</span><span class="sxs-lookup"><span data-stu-id="756cf-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="756cf-116">Assurez-vous que vous avez activé la [prévisualisation pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="756cf-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="756cf-117">Ouvrez un onglet pour avoir quelque chose à inspecter avec DevTools.</span><span class="sxs-lookup"><span data-stu-id="756cf-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="756cf-118">Ouvrez DevTools de l'une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="756cf-118">Open the DevTools in one of the following ways:</span></span>
    * <span data-ttu-id="756cf-119">**Windows :** sélectionnez l'icône Teams dans le bac de bureau.</span><span class="sxs-lookup"><span data-stu-id="756cf-119">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="756cf-120">**macOS :** sélectionnez l'icône Teams dans la station d'accueil.</span><span class="sxs-lookup"><span data-stu-id="756cf-120">**macOS**: Select the Teams icon in the Dock.</span></span>
 
   <span data-ttu-id="756cf-121">L'image suivante montre DevTools inspectant un élément dans une boîte de dialogue de configuration d'onglet :</span><span class="sxs-lookup"><span data-stu-id="756cf-121">The following image shows DevTools inspecting an element in a tab configuration dialog:</span></span>

   ![Tab et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a><span data-ttu-id="756cf-123">Accéder à DevTools à partir d'un client Android</span><span class="sxs-lookup"><span data-stu-id="756cf-123">Access DevTools from an Android client</span></span>

<span data-ttu-id="756cf-124">Vous pouvez également activer devTools à partir du client Android Teams.</span><span class="sxs-lookup"><span data-stu-id="756cf-124">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="756cf-125">Pour activer DevTools, vous devez :</span><span class="sxs-lookup"><span data-stu-id="756cf-125">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="756cf-126">Activez la [prévisualisation pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="756cf-126">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="756cf-127">Connectez votre appareil à votre ordinateur de bureau et définissez votre appareil Android pour [le débogage à distance.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="756cf-127">Connect your device to your desktop computer, and set up your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="756cf-128">Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="756cf-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="756cf-129">Sélectionnez **Inspecter** sous l'onglet que vous souhaitez déboguer, comme dans l'image suivante :</span><span class="sxs-lookup"><span data-stu-id="756cf-129">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
