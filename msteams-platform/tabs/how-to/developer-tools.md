---
title: DevTools pour les onglets Microsoft Teams
description: Décrit comment se rendre à DevTools lors de l’utilisation du client de bureau Microsoft Teams
ms.topic: how-to
keywords: devtools debug mobile chrome desktop client developer tools
ms.openlocfilehash: 1c540c94adc080d9495097f8e3b427eeb14c56d8
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634740"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools pour les onglets Microsoft Teams

Lorsque Teams s’exécute dans un navigateur, il est facile d’accéder aux devTools : F12 sur Windows ou Command-Option-I sur MacOS. DevTools vous donne accès à :

1. Afficher les journaux de la console.
1. Afficher ou modifier les requêtes HTML, CSS et réseau pendant l’utilisation.
1. Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.

> [!NOTE]
> La fonctionnalité est disponible uniquement dans les clients de bureau et Android **une** fois la prévisualisation du développeur activée. Pour plus d’informations, voir [Comment activer la prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-in-the-desktop"></a>Accéder à DevTools dans le Bureau

Bien que la version web et la version de bureau de Teams soient presque identiques, il existe certaines différences en ce qui concerne l’authentification. Parfois, la seule façon de déterminer ce qui se passe est d’utiliser DevTools. Pour utiliser DevTools dans le client de bureau, vous devez :

1. Assurez-vous que vous avez activé la [prévisualisation pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)
1. Ouvrez un onglet pour avoir quelque chose à inspecter avec DevTools.
1. Ouvrez DevTools de l’une des manières suivantes :
    * **Windows :** sélectionnez l’icône Teams dans le bac de bureau.
    * **MacOS :** sélectionnez l’icône Teams dans la station d’accueil.
 
   L’image suivante montre DevTools inspectant un élément dans une boîte de dialogue de configuration d’onglet :

   ![Tab et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a>Accéder à DevTools à partir d’un client Android

Vous pouvez également activer devTools à partir du client Android Teams. Pour activer DevTools, vous devez :

1. Activez la [prévisualisation pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)
1. Connectez votre appareil à votre ordinateur de bureau et programmez votre appareil Android pour [le débogage à distance.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices` .
1. Sélectionnez **Inspecter** sous l’onglet que vous souhaitez déboguer, comme dans l’image suivante :

   ![Android DevTools](~/assets/images/android-devtools.png)
