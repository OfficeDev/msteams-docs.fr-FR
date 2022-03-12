---
title: Ajouter des fonctionnalités à vos applications Teams applications
author: MuyangAmigo
description: Décrit l’ajout de fonctionnalités de Teams Shared Computer Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 246a871c26b0194d74e7d1fc8a3cb8be64d55fe6
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453235"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Ajouter des fonctionnalités à vos applications Teams applications

Vous pouvez créer une application Teams avec l’une des fonctionnalités Teams’application. Pendant le développement d’applications, vous pouvez utiliser Teams Shared Computer Toolkit pour ajouter d’autres fonctionnalités à votre Teams application. Le tableau suivant répertorie les fonctionnalités Teams’application :

|**Fonctionnalité**|**Description**|
|--------|-------------|
| Onglets |  Les onglets sont des balises HTML simples qui pointent vers des domaines déclarés dans le manifeste de l’application. Vous pouvez ajouter des onglets dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel.|
| Bots |  Les bots permettent d’interagir avec votre service web via du texte, des cartes interactives et des modules de tâche.|
| Extensions de messagerie | Les extensions de messagerie permettent d’interagir avec votre service web par le biais de boutons et de formulaires dans Microsoft Teams client.|

## <a name="prerequisite"></a>Conditions préalables

[Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Assurez-vous que Teams projet d’application est ouvert dans du code VS.

## <a name="add-capabilities-using-teams-toolkit"></a>Ajouter des fonctionnalités à l’aide Teams Shared Computer Toolkit

> [!IMPORTANT]
> Vous devez effectuer une mise en service pour chaque environnement une fois que vous avez ajouté des fonctionnalités à votre Teams appl.

1. **Ouvrez Microsoft Visual Studio Code**.
1. Sélectionnez **Teams Shared Computer Toolkit** dans le panneau gauche.
1. **Sélectionnez Ajouter des fonctionnalités** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="fonctionnalités":::

   Vous pouvez également ouvrir la palette de commandes et entrer **Teams : Ajouter des fonctionnalités** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="Autres fonctionnalités":::

1. Dans la fenêtre pop-up, sélectionnez les fonctionnalités à inclure dans votre projet :

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

1. Sélectionnez **OK**.

Les fonctionnalités sélectionnées sont correctement ajoutées à votre projet. Le Teams Shared Computer Toolkit code source pour les fonctionnalités nouvellement ajoutées.

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>Ajouter des fonctionnalités à l’aide de l’CLI TeamsFx dans la fenêtre de commande

1. Modifiez le répertoire de **votre projet**.
1. Exécutez la commande suivante pour ajouter différentes fonctionnalités à votre projet :

   |Fonctionnalité et scénario| Commande|
   |-----------------------|----------|
   |Pour ajouter un onglet|`teamsfx capability add tab`|
   |Pour ajouter un bot|`teamsfx capability add bot`|
   |Pour ajouter une extension de messagerie|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities-matrix"></a>Matrice des fonctionnalités prise en charge

Outre les fonctionnalités que votre application Teams a déjà, vous pouvez choisir d’ajouter différentes fonctionnalités à votre Teams application. Le tableau suivant fournit les différentes fonctionnalités Teams’application :

|Fonctionnalités existantes|D’autres fonctionnalités prise en charge peuvent être ajoutées|
|--------------------|--------------------|
|Onglets avec SPFx|Aucun|
|Onglets avec Azure|Bot et extension de messagerie|
|Bot|Onglets|
|Extension de la messagerie|Onglets et bot|
|Onglets et bot|Onglets et extension de message|
|Onglets et extension de messagerie|Onglets et bot|
|Onglets, bot et extension de messagerie|Onglets|
|Onglets |Bot et extension de message|

## <a name="add-capabilities"></a>Ajouter des fonctionnalités

Après avoir ajouté un bot et une extension de messagerie, les modifications apportées à votre projet sont les suivantes :

* Un code de modèle de bot est ajouté dans un sous-foldeur avec le chemin d’accès `yourProjectFolder/bot`. Cela inclut un **modèle d’application bot Hello World** dans votre projet.
* `launch.json`et `task.json` sous `.vscode` le dossier sont mis à jour, ce qui inclut les scripts nécessaires pour Visual Studio Code, et est exécuté lorsque vous souhaitez déboguer votre application localement.
* `manifest.remote.template.json`et `manifest.local.template.json` le fichier sous `templates/appPackage` dossier est mis à jour, ce qui inclut les informations relatives au bot dans le fichier manifeste qui représente votre application dans la plateforme Teams web. Les modifications sont les suivantes :
  * ID de votre bot.
  * Étendues de votre bot.
  * Commandes à qui l’application bot Hello World peut répondre.
* Les fichiers sous `templates/azure/teamsfx` seront mis à jour et `templates/azure/provision/xxx`le fichier .bicep sera régénéré.
* Les fichiers sous `.fx/config` sont régénérés, ce qui garantit que votre projet est définie avec les configurations qui vous sont données pour la fonctionnalité nouvellement ajoutée.

Une fois l’onglet ajouté, les modifications apportées à votre projet sont les suivantes :

* Un code `yourProjectFolder/tab`de modèle d’onglet frontal est ajouté dans un sous-dossier avec le chemin d’accès, qui inclut un modèle d’application d’onglet **Hello World** dans votre projet.
* `launch.json`et `task.json` sous `.vscode` le dossier sont mis à jour, ce qui inclut les scripts nécessaires pour Visual Studio Code, et est exécuté lorsque vous souhaitez déboguer votre application localement.
* `manifest.remote.template.json`et `manifest.local.template.json` le fichier sous `templates/appPackage` le dossier est mis à jour, ce qui inclut des informations relatives aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams, les modifications sont les suivantes :
  * Onglets configurables et statiques.
  * Étendues des onglets.
* Les fichiers sous `templates/azure/teamsfx` seront mis à jour et `templates/azure/provision/xxx`le fichier .bicep sera régénéré.
* Le fichier sous `.fx/config` est régénéré, ce qui garantit que votre projet est bien définie avec les configurations pour la fonctionnalité nouvellement ajoutée.

## <a name="limitations"></a>Limites

Les limitations à TeamsFx lors de l’ajout de fonctionnalités sont les suivantes :

* Vous pouvez ajouter jusqu’à 16 instances d’onglets.
* Vous pouvez ajouter un bot et une extension de messagerie pour une instance chacune.

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Créer un projet Teams projet](create-new-project.md)
