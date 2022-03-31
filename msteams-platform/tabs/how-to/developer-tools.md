---
title: DevTools pour les onglets Microsoft Teams
description: Décrit comment se rendre à DevTools lors de l’utilisation du client de bureau Microsoft Teams et du débogage
ms.localizationpriority: medium
ms.topic: how-to
keywords: Devtools debug mobile chrome desktop client developer tools tab
ms.openlocfilehash: bec7b94b1db2492de9eaaa38ff62c0783c972f6e
ms.sourcegitcommit: d9daad3d5818d5774911b96fdc7bde45b04c9908
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2022
ms.locfileid: "64511225"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools pour les onglets Microsoft Teams

Lorsque Teams est en cours d’exécution dans un navigateur, il est facile d’accéder à DevTools : F12 sur Windows ou Command-Option-I sur MacOS. DevTools vous donne accès à :

1. Afficher les journaux de la console.
1. Afficher ou modifier les demandes HTML, CSS et réseau pendant l’utilisation.
1. Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.

> [!NOTE]
> La fonctionnalité est disponible uniquement pour les clients de bureau et Android une fois l’aperçu **développeur activé** . Pour plus d’informations, [voir Comment faire activer la prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-on-the-desktop"></a>Accéder à DevTools sur le bureau

Bien que la version web et la version de bureau de Teams sont presque identiques, il existe certaines différences en ce qui concerne l’authentification. Parfois, le seul moyen de déterminer ce qui se passe est d’utiliser les DevTools. Pour utiliser DevTools dans le client de bureau, vous devez :

1. Assurez-vous que vous avez activé la [prévisualisation pour les développeurs](~/resources/dev-preview/developer-preview-intro.md).
1. Ouvrez un onglet pour avoir quelque chose à inspecter avec DevTools.
1. Ouvrez DevTools de l’une des manières suivantes :
    * Sur Windows, vous ouvrez DevTools via l’icône Microsoft Teams dans le bac de bureau.

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * Sur MacOS, sélectionnez l’icône Microsoft Teams dans la station d’accueil.

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

L’exemple suivant montre que DevTools ouvre et inspecte une boîte de dialogue de configuration d’onglet :

   [![Tab et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>Accéder à DevTools à partir d’un appareil Android

Vous pouvez également activer DevTools à partir du client Teams Android. Pour activer DevTools, vous devez :

1. Activez la [prévisualisation du développeur](~/resources/dev-preview/developer-preview-intro.md).
1. Connecter votre appareil sur votre ordinateur de bureau et configurer votre appareil Android pour [le débogage à distance](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).
1. Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices`.
1. **Sélectionnez Inspecter** sous l’onglet que vous souhaitez déboguer, comme dans l’image suivante :

   ![Android DevTools](~/assets/images/android-devtools.png)
