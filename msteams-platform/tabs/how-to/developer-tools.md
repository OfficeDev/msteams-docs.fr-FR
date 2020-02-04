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
# <a name="devtools-for-microsoft-teams-tabs"></a>Onglets DevTools pour Microsoft teams

Lorsque teams est exécuté dans un navigateur, il est facile d’accéder à DevTools : F12 (sous Windows) ou commande-I (sur MacOS). Le DevTools vous donne accès aux éléments suivants :

1. Afficher les journaux de console.
1. Afficher/modifier les demandes html, CSS et réseau au moment de l’exécution.
1. Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.

La fonctionnalité est disponible uniquement dans les clients de bureau et Android une fois l’aperçu de développeur activé. Pour plus d’informations, voir [Comment activer l’aperçu](~/resources/dev-preview/developer-preview-intro.md) pour les développeurs.

## <a name="accessing-devtools-in-the-desktop"></a>Accès à DevTools dans le Bureau

Bien que la version Web de teams et la version de bureau de teams soient presque identiques, il existe certaines différences, notamment en ce qui concerne l’authentification. Parfois, le seul moyen de déterminer ce qui se passe est d’utiliser le DevTools. Voici comment y accéder à partir du client de bureau Teams. Pour utiliser DevTools dans le client de bureau, procédez comme suit :

1. Vérifiez que vous avez activé la préversion pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md)
1. Ouvrez un onglet pour effectuer une inspection avec le DevTools.
1. Ouvrez le DevTools
    * Sous Windows, vous ouvrez DevTools via l’icône Microsoft teams dans le bac de bureau :

  ![Cliquez avec le bouton droit pour ouvrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * Sur MacOS, cliquez sur l’icône Microsoft teams dans le Dock.

Voici à quoi ressemble un exemple d’onglet avec le DevTools ouvert et un élément sélectionné :

![Onglet et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Accès à DevTools à partir d’un client Android

Vous pouvez également activer l’DevTools à partir du client Android Teams. Pour ce faire, procédez comme suit :

1. Vérifiez que vous avez activé la préversion pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md)
1. Connectez votre appareil à votre ordinateur de bureau et configurez votre appareil Android pour le [débogage à distance](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices`.
1. Cliquez sur **inspecter** sous l’onglet que vous souhaitez déboguer, comme dans la capture d’écran ci-dessous.

![DevTools Android](~/assets/images/android-devtools.png)
