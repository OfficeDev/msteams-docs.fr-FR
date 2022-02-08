---
title: Ajouter des ressources à vos applications Teams applications
author: MuyangAmigo
description: Décrit ajouter des ressources de Teams Shared Computer Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# <a name="add-cloud-resources-to-your-teams-app"></a>Ajouter des ressources cloud à votre application Teams web

TeamsFx vous aide à mettre en service des ressources cloud pour l’hébergement de votre application. Vous pouvez également ajouter des ressources cloud adaptées à vos besoins de développement.

## <a name="prerequisite"></a>Conditions préalables

[Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Assurez-vous que vous Teams projet d’application dans Visual Studio Code.

## <a name="add-cloud-resources-using-teams-toolkit"></a>Ajouter des ressources cloud à l’aide Teams Shared Computer Toolkit

> [!IMPORTANT]
> Vous devez mettre en service chaque environnement après avoir ajouté une ressource.

1. **Ouvrez Microsoft Visual Studio Code**.
1. **Sélectionnez Teams Shared Computer Toolkit** dans le volet gauche.
1. Dans le Teams Shared Computer Toolkit barre latérale, **sélectionnez Ajouter des ressources cloud** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="Ajouter des ressources":::

   Vous pouvez également ouvrir la palette de commandes et entrer **Teams : Ajouter des ressources cloud** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="ajouter des ressources cloud":::

1. Dans la fenêtre pop-up, sélectionnez les ressources cloud que vous souhaitez ajouter à Teams projet d’application :

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="add":::

1. Sélectionnez **OK**.

Les ressources sélectionnées sont correctement ajoutées à votre projet.

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>Ajouter des ressources cloud à l’aide de l’CLI TeamsFx dans la fenêtre de commande

1. Modifiez le répertoire de **votre projet**.
1. Exécutez la commande suivante pour ajouter différentes ressources dans votre projet :

|Ressource cloud|Commande|
|---------------|----------|
| Fonction Azure|`teamsfx resource add azure-function --function-name your-func-name`|
| Base de données azure SQL données|`teamsfx resource add --function-name your-func-name`|
| Gestion des API Azure|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Types de ressources cloud

TeamsFx s’intègre aux services Azure pour les scénarios suivants :

- [Fonctions Azure :](/azure/azure-functions/functions-overview) une solution sans serveur pour répondre à vos exigences à la demande, telles que la création d’API web pour votre serveur principal Teams applications.
- [Base SQL données](/azure/azure-sql/database/sql-database-paas-overview) Azure : moteur de base de données PaaS (platform as a service) qui sert de magasin de données Teams applications.
- [Gestion des API Azure](/azure/azure-sql/database/sql-database-paas-overview) : une passerelle API qui peut être utilisée pour administrer les API créées pour les applications Teams et les publier pour les utiliser sur d’autres applications, telles que les applications Power.
- [Coffre de clés Azure](/azure/key-vault/general/overview) : protéger les clés de chiffrement et d’autres secrets utilisés par les applications et services cloud.

## <a name="add-cloud-resources"></a>Ajouter des ressources cloud

Après avoir ajouté une ressource, les modifications apportées à votre projet sont les suivantes :

- De nouveaux paramètres peuvent être ajoutés à azure.parameter. {env}.json pour fournir les informations requises pour la mise en service.
- Le nouveau contenu est ajouté à ARM sous dossier `templates/azure` `templates/azure/teamsfx` à l’exception des fichiers sous dossier pour créer les ressources Azure ajoutées.
- Les fichiers sous le `templates/azure/teamsfx` dossier sont régénérés pour s’assurer que la configuration requise teamsFx est à jour pour les ressources Azure ajoutées.
- `.fx/projectSettings.json` est mis à jour pour suivre les ressources présentes dans votre projet.

Après avoir ajouté des ressources, les modifications supplémentaires apportées à votre projet sont les suivantes :

|Ressources|Modifications|Description|
|---------------|---------------|-----------------------------|
|Fonctions Azure|Un code de modèle de fonctions Azure est ajouté dans un sous-foldeur avec chemin d’accès `yourProjectFolder/api`</br></br>`launch.json` et `task.json` mis à jour sous le `.visual studio code` dossier.| Inclut un modèle de déclencheur Http Hello World dans votre projet.</br></br> Inclut les scripts nécessaires Visual Studio Code à exécuter lorsque vous souhaitez déboguer votre application localement.|
|Gestion des API Azure|Fichier de spécification d’API ouvert ajouté dans un sous-dossier avec chemin d’accès `yourProjectFolder/openapi`|Définit votre API après la publication, il s’agit du fichier de spécification d’API.|

## <a name="limitation"></a>Restriction

Vous ne pouvez pas ajouter de ressources si vous avez créé un SPFx d’onglets.

## <a name="see-also"></a>Voir aussi

[Provisionner des ressources cloud](provision.md)
