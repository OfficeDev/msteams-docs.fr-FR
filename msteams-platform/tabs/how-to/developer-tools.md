---
title: DevTools pour les onglets Microsoft Teams
description: Décrit comment accéder à DevTools lors de l’utilisation du client de bureau Microsoft Teams et du débogage
ms.localizationpriority: medium
ms.topic: how-to
keywords: onglet outils de développeur du client de bureau chrome mobile de débogage devtools
ms.openlocfilehash: c4601711948df798bda6b7d4940b5436c66f8c97
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757478"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools pour les onglets Microsoft Teams

Quand Teams s’exécute dans un navigateur, il est facile d’accéder aux DevTools : F12 du navigateur sur Windows ou Command-Option-I sur MacOS. DevTools vous donne accès à :

1. Afficher les journaux de la console.
1. Affichez ou modifiez les requêtes HTML, CSS et réseau pendant le runtime.
1. Ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif.

> [!NOTE]
> La fonctionnalité est disponible uniquement pour les clients de bureau et Android après l’activation de la **Version préliminaire pour développeurs**. Pour plus d’informations, consultez [Comment activer la version préliminaire pour les développeurs](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-on-the-desktop"></a>Accéder à DevTools sur le bureau

Bien que la version web et la version de bureau de Teams soient presque les mêmes, il existe des différences relatives à l’authentification. Utiliser DevTools est parfois la seule façon de savoir ce qui se passe. Pour utiliser DevTools dans le client de bureau, vous devez :

1. Vérifier que vous avez activé la [Version préliminaire pour développeurs](~/resources/dev-preview/developer-preview-intro.md).
1. Ouvrir un onglet pour que vous ayez un élément à inspecter avec DevTools.
1. Ouvrez DevTools de l’une des manières suivantes :
    * Sur Windows, vous ouvrez DevTools via l’icône Microsoft Teams dans la barre d’état du bureau.

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * Sur MacOS, sélectionnez l’icône Microsoft Teams dans le Dock.

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

L’exemple suivant montre DevTools ouvert et inspectant une boîte de dialogue de configuration d’onglet :

   [![Onglet et DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>Accéder à DevTools à partir d’un appareil Android

Vous pouvez également activer DevTools à partir du client Android Teams. Pour activer DevTools, vous devez :

1. Activer la [version préliminaire pour développeurs](~/resources/dev-preview/developer-preview-intro.md).
1. Connecter votre appareil sur votre ordinateur de bureau, puis configurez votre appareil Android pour le [débogage à distance](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).
1. Dans votre navigateur Chrome, ouvrez `chrome://inspect/#devices`.
1. Sélectionnez **Inspecter** sous l’onglet à déboguer, comme dans l’image suivante :

   ![DevTools pour Android](~/assets/images/android-devtools.png)
