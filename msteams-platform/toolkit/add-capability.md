---
title: Ajouter des fonctionnalités à vos applications Teams applications
author: MuyangAmigo
description: Décrit l’ajout de fonctionnalités de Teams Shared Computer Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f5563b16646b66795b9451eebc865879294dfd98
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227935"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Ajouter des fonctionnalités à vos applications Teams applications

Vous pouvez commencer à créer une application Teams avec l’une Teams fonctionnalités de l’application. Pendant le développement d’applications, vous pouvez utiliser Teams Shared Computer Toolkit pour ajouter de manière flexible d’autres fonctionnalités à votre Teams application. Le tableau suivant décrit les fonctionnalités Teams’application :

|**Fonctionnalité**|**Description**|
|--------|-------------|
| Onglets |  Les onglets sont des balises HTML simples qui pointent vers des domaines déclarés dans le manifeste de l’application. Vous pouvez ajouter des onglets dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel.|
| Bots |  Les bots permettent d’interagir avec votre service web via du texte, des cartes interactives et des modules de tâche.|
| Extensions de messagerie | Les extensions de messagerie permettent d’interagir avec votre service web par le biais de boutons et de formulaires dans Microsoft Teams client.|

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Un projet d’application Teams doit déjà être ouvert dans du code VS.

## <a name="add-capabilities-using-teams-toolkit"></a>Ajouter des fonctionnalités à l’aide Teams Shared Computer Toolkit

> [!IMPORTANT]
> Vous devez effectuer une mise en service pour chaque environnement une fois que vous avez ajouté des fonctionnalités à votre Teams application.

1. Sélectionnez **Teams Shared Computer Toolkit** dans le panneau gauche :

    ![Activer Teams Shared Computer Toolkit](./images/activate-teams-toolkit.png)
  
1. Sélectionnez **Ajouter des fonctionnalités**:

    ![Ajouter des fonctionnalités](./images/add-capabilities.png)

      Vous pouvez également ouvrir la palette de commandes et entrer **Teams : Ajouter des fonctionnalités**: 
      
      > [!NOTE]
      > Il s’agit d’un déclencheur équivalent à celui de l’arborescence.

    ![Autres fonctionnalités d’ajout](./images/alternate-capabilities.png)

1. Dans la fenêtre pop-up, sélectionnez les fonctionnalités à inclure dans votre projet :

    ![Sélectionner des fonctionnalités](./images/select-capabilities.png)

1. Sélectionnez **OK**.

Les fonctionnalités sélectionnées sont correctement ajoutées à votre projet. Le Teams Shared Computer Toolkit code source pour les fonctionnalités nouvellement ajoutées.

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>Ajouter des fonctionnalités à l’aide de l’CLI TeamsFx dans la fenêtre de commande

1. Modifiez le répertoire vers le **répertoire de votre projet.**
1. Exécutez la commande suivante pour ajouter différentes fonctionnalités à votre projet :

   |Fonctionnalité et scénario| Commande|
   |-----------------------|----------|
   |Pour ajouter un onglet|`teamsfx capability add tab`|
   |Pour ajouter un bot|`teamsfx capability add bot`|
   |Pour ajouter une extension de messagerie|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities-matrix"></a>Matrice des fonctionnalités prise en charge

Outre les fonctionnalités que votre application Teams a déjà, vous pouvez choisir d’ajouter différentes fonctionnalités à votre application Teams web. Le tableau suivant fournit différentes fonctionnalités d’Teams d’application : 

|Fonctionnalités existantes|D’autres fonctionnalités peuvent être ajoutées|
|--------------------|--------------------|
|Onglets avec SPFx|Aucun|
|Onglets avec Azure|Bots et extensions de messagerie|
|Bots|Onglets|
|Extensions de messagerie|Onglets|
|Onglets et bots|Aucun|
|Onglets et extensions de messagerie|Aucun|
|Onglets, bots et extensions de messagerie|Aucun|

## <a name="what-happens-when-you-add-capabilities"></a>Que se passe-t-il lorsque vous ajoutez des fonctionnalités ?

Après avoir ajouté le bot et l’extension de messagerie, les modifications suivantes dans votre projet sont les suivantes :

- Un code de modèle de bot est ajouté dans un sous-foldeur avec le chemin `yourProjectFolder/bot` d’accès. Cela inclut un modèle d’application bot « Hello World » dans votre projet.
- `launch.json` et `task.json` sous le dossier sont mis à `.vscode` jour. Cela inclut les scripts nécessaires Visual Studio Code est exécuté lorsque vous souhaitez déboguer votre application localement. 
- `manifest.remote.template.json` et `manifest.local.template.json` le fichier sous le dossier sont mis à `templates/appPackage` jour. Cela inclut les informations relatives au bot dans le fichier manifeste qui représente votre application dans la plateforme Teams web. La modification inclut :
  - ID de votre bot.
  - Étendues de votre bot.
  - Commandes à qui l’application bot Hello World peut répondre.
- Les fichiers sous seront mis à jour et les `templates/azure/teamsfx` modèles/azure/provision/xxx.bicep seront régénérés.
- Le fichier sous `.fx/config` est régénéré. Cela garantit l’ensemble de votre projet avec des configurations de qualité pour les fonctionnalités nouvellement ajoutées.

Une fois l’onglet ajouté, les modifications suivantes dans votre projet sont les suivantes :

- Un code de modèle d’onglet frontal est ajouté dans un sous-foldeur avec le chemin `yourProjectFolder/tab` d’accès. Cela inclut un modèle d’application d’onglet « Hello World » dans votre projet.
- `launch.json` et `task.json` sous le dossier sont mis à `.vscode` jour. Cela inclut les scripts nécessaires Visual Studio Code est exécuté lorsque vous souhaitez déboguer votre application localement. 
- `manifest.remote.template.json` et `manifest.local.template.json` le fichier sous le dossier sont mis à `templates/appPackage` jour. Cela inclut les informations relatives aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams, les modifications sont les suivantes :
  - Onglets configurables et statiques.
  - Étendues des onglets.
- Les fichiers sous seront mis à jour et les `templates/azure/teamsfx` modèles/azure/provision/xxx.bicep seront régénérés.
- Le fichier sous `.fx/config` est régénéré. Cela garantit l’ensemble de votre projet avec des configurations de qualité pour les fonctionnalités nouvellement ajoutées.

## <a name="limitations"></a>Limites

Actuellement, il existe des limitations avec TeamsFx lors de l’ajout de fonctionnalités. Les limitations sont les suivantes :

- Chaque fonctionnalité de projet plusieurs fois
- Toute fonctionnalité si vous démarrez avec une application Tab avec SPFx
- Autres fonctionnalités de bot si votre projet contient une extension de messagerie
- Extension de messagerie supplémentaire si votre projet contient un bot.

> [!NOTE]
> Si vous souhaitez inclure des fonctionnalités de bot et d’extension de messagerie, sélectionnez-les en même temps. Vous pouvez les ajouter lorsque vous créez un projet ou une application onglet.

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Mise en service des ressources cloud](provision.md)

> [!div class="nextstepaction"]
> [Créer un projet Teams projet](create-new-project.md)
