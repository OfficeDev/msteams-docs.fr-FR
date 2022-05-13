---
title: Ajouter des ressources à vos applications Teams
author: MuyangAmigo
description: Décrit l’ajout de ressources du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 50cd3de693f70fd0c8414408bd6f4e6d3332d544
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2022
ms.locfileid: "65297204"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>Ajouter des ressources cloud à votre application Teams

TeamsFx vous permet d’approvisionner des ressources cloud pour l’hébergement de votre application. Vous pouvez également ajouter, de manière facultative, des ressources cloud qui s’adaptent à vos besoins de développement.

## <a name="prerequisite"></a>Conditions préalables

[Installez le Kit de ressources Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Vérifiez que vous avez le projet d’application Teams dans Visual Studio Code.

## <a name="add-cloud-resources-using-teams-toolkit"></a>Ajouter des ressources cloud à l’aide du Kit de ressources Teams

> [!IMPORTANT]
> Vous devez approvisionner chaque environnement après l’ajout d’une ressource.

1. Ouvrez **Microsoft Visual Studio Code**.
1. Sélectionnez **Kit de ressources Teams** dans le volet gauche.
1. Dans le panneau Kit de ressources Teams de la barre latérale, sélectionnez **Ajouter des ressources cloud** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="Ajouter des ressources":::

   Vous pouvez également ouvrir la palette de commandes et entrer **Teams : Ajouter des ressources cloud** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="ajouter des ressources cloud":::

1. Dans la fenêtre contextuelle, sélectionnez les ressources cloud à ajouter à votre projet d’application Teams :

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="ajouter":::

1. Sélectionnez **OK**.

Les ressources sélectionnées sont correctement ajoutées à votre projet.

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>Ajouter des ressources cloud à l’aide de l’Interface de ligne de commande Azure (CLI) TeamsFx dans la fenêtre de commande

1. Remplacez le répertoire par votre **répertoire du projet**.
1. Exécutez la commande suivante pour ajouter diverses ressources dans votre projet :

|Ressource cloud|Commande|
|---------------|----------|
| Fonction Azure|`teamsfx resource add azure-function --function-name your-func-name`|
| Base de données SQL Azure|`teamsfx resource add --function-name your-func-name`|
| Gestion des API Azure|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Types de ressources cloud

TeamsFx s’intègre aux services Azure pour les scénarios suivants :

- [Azure Functions](/azure/azure-functions/functions-overview) : solution sans serveur pour répondre à vos exigences à la demande, telles que la création d’API web pour votre backend d’applications Teams.
- [Base de données SQL Azure](/azure/azure-sql/database/sql-database-paas-overview) : moteur de base de données PaaS (Platform-as-a-Service) qui vous sert de magasin de données d’applications Teams.
- [Gestion des API Azure](deploy.md) : passerelle d’API pouvant être utilisée pour gérer les API créées pour les applications Teams et les publier pour les utiliser sur d’autres applications, telles que les applications Power.
- [Azure Key Vault](/azure/key-vault/general/overview) : protégez les clés de chiffrement et d’autres clés secrètes utilisées par les applications et les services cloud.

## <a name="add-cloud-resources"></a>Ajouter des ressources cloud

Après l’ajout de ressources, les modifications apportées à votre projet sont les suivantes :

- De nouveaux paramètres peuvent être ajoutés à azure.parameter.{env}.json pour fournir les informations requises pour l’approvisionnement.
- Le nouveau contenu est ajouté au modèle ARM sous le dossier `templates/azure`, à l’exception des fichiers sous le dossier `templates/azure/teamsfx` pour créer les ressources Azure ajoutées.
- Les fichiers sous le dossier `templates/azure/teamsfx` sont régénérés pour garantir que la configuration requise de TeamsFx est à jour pour les ressources Azure ajoutées.
- `.fx/projectSettings.json` est mis à jour pour suivre les ressources présentes dans votre projet.

Après avoir ajouté des ressources, les modifications supplémentaires apportées à votre projet sont les suivantes :

|Ressources|Modifications|Description|
|---------------|---------------|-----------------------------|
|Azure Functions|Un code de modèle Azure Functions est ajouté dans un sous-dossier avec le chemin d’accès `yourProjectFolder/api`</br></br>`launch.json` et `task.json` sont mis à jour sous le dossier `.visual studio code`.| Inclut un modèle de déclencheur HTTP Hello World dans votre projet.</br></br> Inclut les scripts nécessaires pour Visual Studio Code à exécuter lorsque vous souhaitez déboguer votre application de manière locale.|
|Gestion des API Azure|Fichier de spécification d’API ouvert ajouté dans un sous-dossier avec le chemin d’accès `yourProjectFolder/openapi`|Définit votre API après la publication. Il s’agit du fichier de spécification de l’API.|

## <a name="limitation"></a>Restriction

Vous ne pouvez pas ajouter de ressources si vous avez créé un projet d’onglet basé sur SPFx.

## <a name="see-also"></a>Voir aussi

[Provisionner des ressources cloud](provision.md)
