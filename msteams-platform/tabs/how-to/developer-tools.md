---
title: DevTools pour les onglets Microsoft Teams
description: Décrit comment se rendre à DevTools lors de l’utilisation du Microsoft Teams DevTools
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
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools pour les onglets Microsoft Teams

Lorsque Teams est en cours d’exécution dans un navigateur, il est facile d’accéder à DevTools : F12 sur Windows ou Command-Option-I sur MacOS. DevTools vous donne accès à :

1. Afficher les journaux de la console.
1. Afficher ou modifier les requêtes HTML, CSS et réseau pendant l’utilisation.
1. Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.

> [!NOTE]
> La fonctionnalité est disponible uniquement pour les clients de bureau et Android une fois l’aperçu **développeur** activé. Pour plus d’informations, voir [Comment activer la prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-on-the-desktop"></a>Accéder à DevTools sur le bureau

Bien que la version web et la version de bureau de Teams soient presque identiques, il existe certaines différences en ce qui concerne l’authentification. Parfois, la seule façon de déterminer ce qui se passe est d’utiliser DevTools. Pour utiliser DevTools dans le client de bureau, vous devez :

1. Assurez-vous que vous avez activé la [prévisualisation pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)
1. Ouvrez un onglet pour avoir quelque chose à inspecter avec DevTools.
1. Ouvrez DevTools de l’une des manières suivantes :
    * Sur Windows, ouvrez DevTools via l’icône Microsoft Teams dans le bac de bureau :<br>
  ![Cliquez avec le bouton droit pour ouvrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)
    * Sur MacOS, cliquez sur l’icône Microsoft Teams dans la station d’accueil.

L’exemple suivant montre que DevTools ouvre et inspecte une boîte de dialogue de configuration d’onglet :

   ![Tab et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-device"></a>Accéder à DevTools à partir d’un appareil Android

Vous pouvez également activer devTools à partir du client Teams Android. Pour activer DevTools, vous devez :

1. Activez la [prévisualisation pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)
1. Connecter votre appareil sur votre ordinateur de bureau et configurer votre appareil Android pour [le débogage à distance.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices` .
1. Sélectionnez **Inspecter** sous l’onglet que vous souhaitez déboguer, comme dans l’image suivante :

   ![Android DevTools](~/assets/images/android-devtools.png)
