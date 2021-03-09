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
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a><span data-ttu-id="a6cba-103">Mettre à niveau Teams à l’aide du générateur Yeoman Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a6cba-103">Upgrade Teams using Microsoft Teams Yeoman generator</span></span>
<span data-ttu-id="a6cba-104">Ce didacticiel vous aide à mettre à niveau votre version actuelle de l’application Microsoft Teams vers la dernière version à l’aide du générateur Yeoman Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a6cba-104">This tutorial helps you to upgrade your current Microsoft Teams app version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

## <a name="get-current-version-of-teams"></a><span data-ttu-id="a6cba-105">Obtenir la version actuelle de Teams</span><span class="sxs-lookup"><span data-stu-id="a6cba-105">Get current version of Teams</span></span>
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a><span data-ttu-id="a6cba-106">Mettre à jour Teams</span><span class="sxs-lookup"><span data-stu-id="a6cba-106">Update Teams</span></span>
<span data-ttu-id="a6cba-107">La commande yo répertorie différentes options, allant de la création d’un projet à la mise à jour du générateur.</span><span class="sxs-lookup"><span data-stu-id="a6cba-107">The yo command lists out various options ranging from creating project to updating generator.</span></span> <span data-ttu-id="a6cba-108">Utilisez la commande suivante pour sélectionner le générateur de mise à jour :</span><span class="sxs-lookup"><span data-stu-id="a6cba-108">Use the following command to select update generator:</span></span>
```PowerShell
 yo
```

<span data-ttu-id="a6cba-109">Utilisez les touches de direction pour choisir **Update Generators**.</span><span class="sxs-lookup"><span data-stu-id="a6cba-109">Use the arrow keys to choose **Update Generators**.</span></span>
<span data-ttu-id="a6cba-110">![image de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span><span class="sxs-lookup"><span data-stu-id="a6cba-110">![image of YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span></span>

<span data-ttu-id="a6cba-111">La liste affiche tous les générateurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="a6cba-111">The list displays all the available generators.</span></span> <span data-ttu-id="a6cba-112">Pour sélectionner ou désélectionner la version de  Teams dans les options disponibles, utilisez la barre d’espace et choisissez un générateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="a6cba-112">To select or unselect Teams version from the available options, use the **space bar** and choose a specific generator.</span></span>
<span data-ttu-id="a6cba-113">![image de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span><span class="sxs-lookup"><span data-stu-id="a6cba-113">![image of UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span></span>

<span data-ttu-id="a6cba-114">L’installation de Teams prend quelques secondes à quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a6cba-114">It takes few seconds to minutes for Teams installation to complete.</span></span>

<span data-ttu-id="a6cba-115">Une fois l’installation terminée, utilisez la commande suivante pour vérifier la version installée :</span><span class="sxs-lookup"><span data-stu-id="a6cba-115">After the installation is complete, use the following command to check the installed version:</span></span>

```PowerShell
yo teams --version
```

![image de FindVersionAfterInstallation](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

<span data-ttu-id="a6cba-117">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="a6cba-117">Congrats!</span></span> <span data-ttu-id="a6cba-118">Vous avez mis à niveau Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a6cba-118">You have upgraded Microsoft Teams.</span></span>

