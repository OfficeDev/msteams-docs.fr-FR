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
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools pour les onglets Microsoft Teams

Lorsque Teams s’exécute dans un navigateur, il est facile d’accéder aux devTools : F12 (sur Windows) ou Command-Option-I (sur MacOS). DevTools vous donne accès à :

1. Afficher les journaux de la console.
1. Afficher/modifier les requêtes html, css et réseau pendant l’utilisation.
1. Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.

La fonctionnalité est disponible uniquement dans les clients de bureau et Android une fois la prévisualisation du développeur activée. Pour plus d’informations, voir comment [activer la prévisualisation](~/resources/dev-preview/developer-preview-intro.md) du développeur.

## <a name="accessing-devtools-in-the-desktop"></a>Accès à DevTools dans le Bureau

Bien que la version web de Teams et la version de bureau des équipes soient presque identiques, il existe certaines différences, en particulier en ce qui concerne l’authentification. Parfois, le seul moyen de déterminer ce qui se passe est d’utiliser DevTools. Voici comment les obtenir à partir du client de bureau Teams. Pour utiliser DevTools dans le client de bureau :

1. Assurez-vous que vous avez activé la [prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md)
1. Ouvrez un onglet pour avoir quelque chose à inspecter avec DevTools.
1. Ouvrez DevTools
    * Sur Windows, vous ouvrez DevTools via l’icône Microsoft Teams dans le bac de bureau :

  ![Cliquez avec le bouton droit pour ouvrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * Sur MacOS, cliquez sur l’icône Microsoft Teams dans la station d’accueil.

Voici à quoi ressemble un exemple d’onglet avec devTools ouvert et un élément sélectionné :

![Tab et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Accès à DevTools à partir d’un client Android

Vous pouvez également activer devTools à partir du client Android Teams. Pour ce faire, procédez comme suit :

1. Assurez-vous que vous avez activé la [prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md)
1. Connecter votre appareil à votre ordinateur de bureau et configurer votre appareil Android pour [le débogage à distance](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices` .
1. Cliquez **sur Inspecter** sous l’onglet que vous souhaitez déboguer, comme dans la capture d’écran ci-dessous.

![Android DevTools](~/assets/images/android-devtools.png)
