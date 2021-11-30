---
title: Ajouter des ressources à vos applications Teams applications
author: MuyangAmigo
description: Décrit ajouter des ressources de Teams Shared Computer Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: dcaa4475db62be2cebbbe2b1b74e0bbbd7fb5398
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227706"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>Ajouter des ressources cloud à votre application Teams web

TeamsFx vous aide à mettre en service des ressources cloud pour l’hébergement de votre application. Vous pouvez également ajouter des ressources cloud adaptées à vos besoins de développement.

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Vous devez déjà avoir un projet Teams’application.

## <a name="add-cloud-resources-using-teams-toolkit"></a>Ajouter des ressources cloud à l’aide Teams Shared Computer Toolkit

> [!IMPORTANT]
> Vous devez mettre en service chaque environnement après avoir ajouté une ressource.

1. Ouvrez **Visual Studio Code**.
1. Sélectionnez **Teams Shared Computer Toolkit** dans le panneau gauche :

    ![Activer Teams Shared Computer Toolkit](./images/activate-teams-toolkit.png)

1. Dans le Teams Shared Computer Toolkit de la barre latérale, **sélectionnez Ajouter des ressources cloud**:

    ![Ajouter des ressources cloud](./images/add-cloud-resources.png)

    Vous pouvez également ouvrir la palette de commandes et entrer **Teams : Ajouter des ressources cloud**:
    
    > [!NOTE]
    > Suivez le même processus que celui déclenché à partir de l’arborescence :

    ![Autres ressources cloud](./images/alternate-cloud-resources.png)

1. Dans la fenêtre pop-up, sélectionnez les ressources cloud que vous souhaitez ajouter à Teams projet d’application :

     ![Sélectionner des ressources cloud](./images/select-cloud-resources.png)

1. Sélectionnez **OK**.

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>Ajouter des ressources cloud à l’aide de l’CLI TeamsFx dans la fenêtre de commande

1. Modifiez le répertoire vers le **répertoire de votre projet.**
1. Exécutez la commande pour ajouter différentes fonctionnalités.

Le tableau suivant décrit les ressources cloud et les commandes correspondantes pour les ajouter :

|Ressources cloud|Commande|
|---------------|----------|
| Fonction Azure|`teamsfx resource add azure-function --function-name your-func-name`|
| Base de données azure SQL données|`teamsfx resource add --function-name your-func-name`|
| Gestion des API Azure|`teamsfx resource add azure-apim`|

## <a name="what-cloud-resources-can-be-added"></a>Quelles ressources cloud peuvent être ajoutées

TeamsFx fournit des intégrations transparentes avec les services Azure qui sont courants dans les scénarios d’application suivants :

- [Fonctions Azure](/azure/azure-functions/functions-overview): solution sans serveur pour répondre à vos exigences à la demande, telles que la création d’API web pour votre serveur principal Teams applications.
- [Base SQL données](/azure/azure-sql/database/sql-database-paas-overview)Azure : moteur de base de données PaaS (Plateforme en tant que service) entièrement géré qui sert de magasin de données Teams applications.
- [Gestion des API Azure](/azure/azure-sql/database/sql-database-paas-overview): une passerelle API qui peut être utilisée pour administrer les API créées pour les applications Teams et les publier pour les consommer sur d’autres applications, telles que Power Apps.

## <a name="what-happens-when-you-add-resources"></a>Que se passe-t-il lorsque vous ajoutez des ressources ?

Les modifications suivantes sont apportées à votre projet lorsque vous ajoutez des ressources :

- De nouveaux paramètres peuvent être ajoutés à azure.parameter. {env}.json pour fournir les informations requises pour la mise en service.
- Le nouveau contenu est ajouté à ARM sous dossier (à l’exception des fichiers sous dossier) pour créer les `templates/azure` `templates/azure/teamsfx` ressources Azure ajoutées.
- Les fichiers sous dossier sont régénérés pour s’assurer que la configuration requise teamsFx est à jour pour `templates/azure/teamsfx` les ressources Azure ajoutées.
- `.fx/projectSettings.json` est mis à jour pour suivre les ressources présentes dans votre projet.

En attendant, il existe des modifications supplémentaires pour chaque type de ressource :

|Ressources ajoutées|Ce qui a changé|Pourquoi ces modifications sont-elles apportées ?|
|---------------|---------------|-----------------------------|
|Azure Functions|Un code de modèle Azure Functions est ajouté dans un sous-foldeur avec chemin d’accès `yourProjectFolder/api`</br></br>`launch.json` et `task.json` mis à jour sous le `.vscode` dossier.| Incluez un modèle de déclencheur Http Hello World dans votre projet.</br></br> Pour inclure les scripts nécessaires Visual Studio Code exécutés lorsque vous souhaitez déboguer votre application localement.|
|Gestion des API Azure|Fichier de spécification Open API ajouté dans un sous-dossier avec chemin d’accès `yourProjectFolder/openapi`|Il s’agit du fichier de spécification d’API qui définit votre API après la publication.|

## <a name="limitations"></a>Limites

- Vous ne pouvez ajouter qu’une seule Function App/Azure SQL Database/APIM Service à votre projet.
- Vous ne pouvez pas ajouter de ressources si votre projet ne contient pas d’application onglet.

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Mise en service des ressources cloud](provision.md)
