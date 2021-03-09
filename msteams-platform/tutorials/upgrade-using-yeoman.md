---
title: Didacticiel - Mettre à niveau Teams à l’aide du générateur Yeoman Microsoft Teams
description: Découvrez comment utiliser le générateur Yeoman Microsoft Teams pour mettre à niveau Teams.
ms.topic: tutorial
ms.openlocfilehash: 0c52dd15703000a1c0f99ddd28401dd686e1b1bb
ms.sourcegitcommit: afe4bc0336663e496d03c52e4b206217c02fae63
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2021
ms.locfileid: "50528632"
---
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a>Mettre à niveau Teams à l’aide du générateur Yeoman Microsoft Teams
Ce didacticiel vous aide à mettre à niveau votre version actuelle de l’application Microsoft Teams vers la dernière version à l’aide du générateur Yeoman Microsoft Teams.

## <a name="get-current-version-of-teams"></a>Obtenir la version actuelle de Teams
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a>Mettre à jour Teams
La commande yo répertorie différentes options, allant de la création d’un projet à la mise à jour du générateur. Utilisez la commande suivante pour sélectionner le générateur de mise à jour :
```PowerShell
 yo
```

Utilisez les touches de direction pour choisir **Update Generators**.
![image de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

La liste affiche tous les générateurs disponibles. Pour sélectionner ou désélectionner la version de  Teams dans les options disponibles, utilisez la barre d’espace et choisissez un générateur spécifique.
![image de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)

L’installation de Teams prend quelques secondes à quelques minutes.

Une fois l’installation terminée, utilisez la commande suivante pour vérifier la version installée :

```PowerShell
yo teams --version
```

![image de FindVersionAfterInstallation](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

Félicitations ! Vous avez mis à niveau Microsoft Teams.

