---
title: DevTools pour les onglets Microsoft Teams
description: Décrit comment se rendre à DevTools lors de l’utilisation du client de bureau Microsoft Teams
ms.topic: how-to
keywords: devtools debug mobile chrome desktop client developer tools
ms.openlocfilehash: 1bf7d246136a24316309ae144ac9552c5fd4f57d
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596272"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools pour les onglets Microsoft Teams

Lorsque Teams s’exécute dans un navigateur, il est facile d’accéder aux devTools : F12 (sur Windows) ou Command-Option-I (sur MacOS). DevTools vous donne accès à :

1. Afficher les journaux de la console.
1. Afficher/modifier les requêtes html, css et réseau pendant l’runtime.
1. Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.

La fonctionnalité est disponible uniquement dans les clients de bureau et Android une fois la prévisualisation du développeur activée. Pour plus d’informations, voir comment [activer la prévisualisation](~/resources/dev-preview/developer-preview-intro.md) du développeur.

## <a name="accessing-devtools-in-the-desktop"></a>Accès à DevTools dans le Bureau

Bien que la version web de Teams et la version de bureau des équipes soient presque identiques, il existe certaines différences, en particulier en ce qui concerne l’authentification. Parfois, le seul moyen de déterminer ce qui se passe est d’utiliser DevTools. Voici comment les obtenir à partir du client de bureau Teams. Pour utiliser DevTools dans le client de bureau :

1. Assurez-vous que vous avez activé la [prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md)
1. Ouvrez un onglet pour avoir quelque chose à inspecter avec DevTools.
1. Ouvrez DevTools de l’une des manières suivantes :
    * **Windows :** sélectionnez l’icône Teams dans le bac de bureau.
    * **macOS :** sélectionnez l’icône Teams dans la station d’accueil.

La capture d’écran suivante montre DevTools inspectant un élément dans une boîte de dialogue de configuration d’onglet :

![Tab et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Accès à DevTools à partir d’un client Android

Vous pouvez également activer devTools à partir du client Android Teams.

1. Assurez-vous que vous avez activé la [prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md)
1. Connecter votre appareil à votre ordinateur de bureau et configurer votre appareil Android pour [le débogage à distance](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices` .
1. Cliquez **sur Inspecter** sous l’onglet que vous souhaitez déboguer, comme dans la capture d’écran ci-dessous.

![Android DevTools](~/assets/images/android-devtools.png)
