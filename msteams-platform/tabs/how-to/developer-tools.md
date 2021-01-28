---
title: DevTools pour les onglets Microsoft Teams
description: Décrit comment se rendre à DevTools lors de l’utilisation du client de bureau Microsoft Teams
ms.topic: how-to
keywords: devtools debug mobile chrome desktop client developer tools
ms.openlocfilehash: 8f23a5d56faa00d40451d2bbeadde32f6a5d0f7f
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014578"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="70041-104">DevTools pour les onglets Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="70041-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="70041-105">Lorsque Teams s’exécute dans un navigateur, il est facile d’accéder aux devTools : F12 (sur Windows) ou Command-Option-I (sur MacOS).</span><span class="sxs-lookup"><span data-stu-id="70041-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="70041-106">DevTools vous donne accès à :</span><span class="sxs-lookup"><span data-stu-id="70041-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="70041-107">Afficher les journaux de la console.</span><span class="sxs-lookup"><span data-stu-id="70041-107">View console logs.</span></span>
1. <span data-ttu-id="70041-108">Afficher/modifier les requêtes html, css et réseau pendant l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="70041-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="70041-109">Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.</span><span class="sxs-lookup"><span data-stu-id="70041-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="70041-110">La fonctionnalité est disponible uniquement dans les clients de bureau et Android une fois la prévisualisation du développeur activée.</span><span class="sxs-lookup"><span data-stu-id="70041-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="70041-111">Pour plus d’informations, voir comment [activer la prévisualisation](~/resources/dev-preview/developer-preview-intro.md) du développeur.</span><span class="sxs-lookup"><span data-stu-id="70041-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="70041-112">Accès à DevTools dans le Bureau</span><span class="sxs-lookup"><span data-stu-id="70041-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="70041-113">Bien que la version web de Teams et la version de bureau des équipes soient presque identiques, il existe certaines différences, en particulier en ce qui concerne l’authentification.</span><span class="sxs-lookup"><span data-stu-id="70041-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="70041-114">Parfois, le seul moyen de déterminer ce qui se passe est d’utiliser DevTools.</span><span class="sxs-lookup"><span data-stu-id="70041-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="70041-115">Voici comment les obtenir à partir du client de bureau Teams.</span><span class="sxs-lookup"><span data-stu-id="70041-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="70041-116">Pour utiliser DevTools dans le client de bureau :</span><span class="sxs-lookup"><span data-stu-id="70041-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="70041-117">Assurez-vous que vous avez activé la [prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="70041-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="70041-118">Ouvrez un onglet pour avoir quelque chose à inspecter avec DevTools.</span><span class="sxs-lookup"><span data-stu-id="70041-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="70041-119">Ouvrez DevTools</span><span class="sxs-lookup"><span data-stu-id="70041-119">Open the DevTools</span></span>
    * <span data-ttu-id="70041-120">Sur Windows, vous ouvrez DevTools via l’icône Microsoft Teams dans le bac de bureau :</span><span class="sxs-lookup"><span data-stu-id="70041-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![Cliquez avec le bouton droit pour ouvrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="70041-122">Sur MacOS, cliquez sur l’icône Microsoft Teams dans la station d’accueil.</span><span class="sxs-lookup"><span data-stu-id="70041-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="70041-123">Voici à quoi ressemble un exemple d’onglet avec devTools ouvert et un élément sélectionné :</span><span class="sxs-lookup"><span data-stu-id="70041-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Tab et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="70041-125">Accès à DevTools à partir d’un client Android</span><span class="sxs-lookup"><span data-stu-id="70041-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="70041-126">Vous pouvez également activer devTools à partir du client Android Teams.</span><span class="sxs-lookup"><span data-stu-id="70041-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="70041-127">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="70041-127">To do so:</span></span>

1. <span data-ttu-id="70041-128">Assurez-vous que vous avez activé la [prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="70041-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="70041-129">Connecter votre appareil à votre ordinateur de bureau et configurer votre appareil Android pour [le débogage à distance](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="70041-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="70041-130">Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="70041-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="70041-131">Cliquez **sur Inspecter** sous l’onglet que vous souhaitez déboguer, comme dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="70041-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
