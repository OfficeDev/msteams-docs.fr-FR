---
title: Onglets DevTools pour Microsoft teams
description: Décrit comment accéder au DevTools lors de l’utilisation du client de bureau Microsoft teams
keywords: devtools débogage des outils de développement mobile chrome de bureau
ms.openlocfilehash: 6c8ac15caf64c979b23155be847e8791988486e6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673787"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="7df86-104">Onglets DevTools pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="7df86-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="7df86-105">Lorsque teams est exécuté dans un navigateur, il est facile d’accéder à DevTools : F12 (sous Windows) ou commande-I (sur MacOS).</span><span class="sxs-lookup"><span data-stu-id="7df86-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="7df86-106">Le DevTools vous donne accès aux éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7df86-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="7df86-107">Afficher les journaux de console.</span><span class="sxs-lookup"><span data-stu-id="7df86-107">View console logs.</span></span>
1. <span data-ttu-id="7df86-108">Afficher/modifier les demandes html, CSS et réseau au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="7df86-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="7df86-109">Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.</span><span class="sxs-lookup"><span data-stu-id="7df86-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="7df86-110">La fonctionnalité est disponible uniquement dans les clients de bureau et Android une fois l’aperçu de développeur activé.</span><span class="sxs-lookup"><span data-stu-id="7df86-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="7df86-111">Pour plus d’informations, voir [Comment activer l’aperçu](~/resources/dev-preview/developer-preview-intro.md) pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="7df86-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="7df86-112">Accès à DevTools dans le Bureau</span><span class="sxs-lookup"><span data-stu-id="7df86-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="7df86-113">Bien que la version Web de teams et la version de bureau de teams soient presque identiques, il existe certaines différences, notamment en ce qui concerne l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7df86-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="7df86-114">Parfois, le seul moyen de déterminer ce qui se passe est d’utiliser le DevTools.</span><span class="sxs-lookup"><span data-stu-id="7df86-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="7df86-115">Voici comment y accéder à partir du client de bureau Teams.</span><span class="sxs-lookup"><span data-stu-id="7df86-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="7df86-116">Pour utiliser DevTools dans le client de bureau, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7df86-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="7df86-117">Vérifiez que vous avez activé la préversion pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="7df86-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="7df86-118">Ouvrez un onglet pour effectuer une inspection avec le DevTools.</span><span class="sxs-lookup"><span data-stu-id="7df86-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="7df86-119">Ouvrez le DevTools</span><span class="sxs-lookup"><span data-stu-id="7df86-119">Open the DevTools</span></span>
    * <span data-ttu-id="7df86-120">Sous Windows, vous ouvrez DevTools via l’icône Microsoft teams dans le bac de bureau :</span><span class="sxs-lookup"><span data-stu-id="7df86-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![Cliquez avec le bouton droit pour ouvrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="7df86-122">Sur MacOS, cliquez sur l’icône Microsoft teams dans le Dock.</span><span class="sxs-lookup"><span data-stu-id="7df86-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="7df86-123">Voici à quoi ressemble un exemple d’onglet avec le DevTools ouvert et un élément sélectionné :</span><span class="sxs-lookup"><span data-stu-id="7df86-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Onglet et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="7df86-125">Accès à DevTools à partir d’un client Android</span><span class="sxs-lookup"><span data-stu-id="7df86-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="7df86-126">Vous pouvez également activer l’DevTools à partir du client Android Teams.</span><span class="sxs-lookup"><span data-stu-id="7df86-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="7df86-127">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7df86-127">To do so:</span></span>

1. <span data-ttu-id="7df86-128">Vérifiez que vous avez activé la préversion pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="7df86-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="7df86-129">Connectez votre appareil à votre ordinateur de bureau et configurez votre appareil Android pour le [débogage à distance](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="7df86-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="7df86-130">Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices`.</span><span class="sxs-lookup"><span data-stu-id="7df86-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="7df86-131">Cliquez sur **inspecter** sous l’onglet que vous souhaitez déboguer, comme dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7df86-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![DevTools Android](~/assets/images/android-devtools.png)
