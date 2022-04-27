---
title: Ajouter des fonctionnalités à vos applications Teams
author: MuyangAmigo
description: Décrit l’ajout de fonctionnalités de Teams Shared Computer Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9d2e3d559bd9d561e3afae8b0db9544ab2ad86cc
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073530"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Ajouter des fonctionnalités à vos applications Teams

Pendant le développement d’applications, vous pouvez créer une application Teams avec Teams fonctionnalité d’application. Le tableau suivant répertorie les fonctionnalités d’application Teams :

|**Fonctionnalité**|**Description**|
|--------|-------------|
| Onglets |  Les onglets sont des balises HTML simples qui pointent vers des domaines déclarés dans le manifeste de l’application. Vous pouvez ajouter des onglets dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel|
| Bots |  Les bots aident à interagir avec votre service web via du texte, des cartes interactives et des modules de tâches|
| Extensions de messagerie | Les extensions de messagerie permettent d’interagir avec votre service web via des boutons et des formulaires dans le client Microsoft Teams|

## <a name="prerequisite"></a>Conditions préalables

* [Installer la dernière version d’Office](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Vérifiez que vous avez Teams projet d’application ouvert dans VS Code.

## <a name="limitations"></a>Limites

Les limitations de TeamsFx lors de l’ajout de fonctionnalités supplémentaires sont les suivantes :

* Vous pouvez ajouter des onglets jusqu’à 16 instances
* Vous pouvez ajouter un bot et une extension de messagerie pour une instance chacune
## <a name="add-capabilities"></a>Ajouter des fonctionnalités

> [!Note]
> Vous devez effectuer la configuration pour chaque environnement, une fois que vous avez ajouté des fonctionnalités à votre application Teams.
* Vous pouvez ajouter des fonctionnalités à l’aide de Teams Shared Computer Toolkit dans Visual Studio Code
    1. Ouvrir **Microsoft Visual Studio Code**
    1. Sélectionnez **Teams Shared Computer Toolkit** dans le volet gauche
    1. Sélectionner **Ajouter des fonctionnalités**

        :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="fonctionnalités":::

*   Vous pouvez également ouvrir la palette de commandes et entrer Teams : Ajouter des fonctionnalités :

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="Autres fonctionnalités":::


    1. Dans la fenêtre contextuelle, sélectionnez les fonctionnalités à inclure dans votre projet :

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

    2. Sélectionner **OK**

Les fonctionnalités sélectionnées sont correctement ajoutées à votre projet. Le Teams Shared Computer Toolkit générer du code source pour les fonctionnalités nouvellement ajoutées

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>Ajouter des fonctionnalités à l’aide de l’interface CLI TeamsFx dans la fenêtre de commande

1. Remplacer le répertoire par le **répertoire** de votre projet
1. Exécutez la commande suivante pour ajouter différentes fonctionnalités à votre projet :

   |Fonctionnalité et scénario| Commande|
   |-----------------------|----------|
   |Pour ajouter un onglet|`teamsfx capability add tab`|
   |Pour ajouter un bot|`teamsfx capability add bot`|
   |Pour ajouter une extension de messagerie|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities"></a>Fonctionnalités prises en charge

Outre les fonctionnalités déjà disponibles pour votre application Teams, vous pouvez choisir d’ajouter différentes fonctionnalités à votre application Teams. Le tableau suivant fournit les différentes fonctionnalités d’application Teams :

|Fonctionnalités existantes|Autres fonctionnalités prises en charge|
|--------------------|--------------------|
|Onglets avec SPFx|Aucun|
|Onglets avec Azure|Bot et extension de messagerie|
|Bot|Onglets|
|Extension de la messagerie|Onglets et bot|
|Onglets et bot|Onglets et extension de message|
|Onglets et extension de messagerie|Onglets et bot|
|Onglets, bot et extension de messagerie|Onglets|
|Onglets |Bot et extension de message|

## <a name="add-bot-tab-and-messaging-extension"></a>Ajouter le bot, l’onglet et l’extension de messagerie

Après avoir ajouté un bot et une extension de messagerie, les modifications apportées à votre projet sont les suivantes :

* Un code de modèle de bot est ajouté dans un sous-dossier avec chemin d’accès `yourProjectFolder/bot`. Cela inclut un modèle d’application de bot **Hello World** dans votre projet
* `launch.json`et `task.json` sous `.vscode` le dossier sont mis à jour, ce qui inclut les scripts nécessaires pour Visual Studio Code, et est exécuté lorsque vous souhaitez déboguer votre application localement
* `manifest.template.json`Le fichier sous `templates/appPackage` dossier est mis à jour, qui inclut les informations relatives au bot dans le fichier manifeste qui représente votre application dans la plateforme Teams. Les modifications sont les suivantes :
  * ID de votre bot
  * Étendues de votre bot
  * Commandes auxquelles l’application de bot Hello World peut répondre
* Les fichiers sous `templates/azure/teamsfx` sont mis à jour et `templates/azure/provision/xxx`les fichiers .bicep sont régénérés
* Les fichiers sous `.fx/config` sont régénérés, ce qui garantit que votre projet est défini avec les configurations appropriées pour la fonctionnalité nouvellement ajoutée

Après l’ajout de l’onglet, les modifications apportées à votre projet sont les suivantes :

* Un code de modèle d’onglet front-end est ajouté dans un sous-dossier avec chemin d’accès `yourProjectFolder/tab`, qui inclut un modèle d’application d’onglet **Hello World** dans votre projet
* `launch.json`et `task.json` sous `.vscode` le dossier sont mis à jour, ce qui inclut les scripts nécessaires pour Visual Studio Code, et est exécuté lorsque vous souhaitez déboguer votre application localement
* `manifest.template.json`Le fichier sous `templates/appPackage` dossier est mis à jour, qui inclut des informations relatives aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams. Les modifications sont les suivantes :
  * Onglets configurables et statiques
  * Étendues des onglets
* Les fichiers sous `templates/azure/teamsfx` seront mis à jour et `templates/azure/provision/xxx`le fichier .bicep régénéré
* Le fichier sous `.fx/config` est régénéré, ce qui garantit que votre projet est défini avec les configurations appropriées pour la fonctionnalité nouvellement ajoutée



## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Créer un projet Teams](create-new-project.md)
