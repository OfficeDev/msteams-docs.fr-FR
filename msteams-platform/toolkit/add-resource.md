---
title: Ajouter des ressources aux applications Teams
author: MuyangAmigo
description: Dans ce module, découvrez comment ajouter resources of Teams Toolkit, advantages, limitations and capabilities
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: fc58610802a51af19efc32e579566fbf5e36feca
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616517"
---
# <a name="add-cloud-resources-to-microsoft-teams-app"></a>Ajouter des ressources cloud à l’application Microsoft Teams

Teams Toolkit vous aide à provisionner les ressources cloud pour l’hébergement de votre application. Vous pouvez ajouter éventuellement les ressources cloud qui répondent à vos besoins de développement. L’avantage de l’ajout de ressources cloud supplémentaires dans TeamsFx est que vous pouvez générer automatiquement tous les fichiers de configuration et vous connecter à l’application Teams à l’aide du Kit de ressources Teams.

> [!NOTE]
> Si vous avez créé un projet d’onglet basé sur SPFx, vous ne pouvez pas ajouter de ressources cloud Azure.

## <a name="add-cloud-resources"></a>Ajouter des ressources cloud

Vous pouvez ajouter des ressources cloud selon les méthodes suivantes :

### <a name="to-add-cloud-resources-by-using-teams-toolkit-in-visual-studio-code"></a>Pour ajouter des ressources cloud à l’aide du Kit de ressources Teams dans Visual Studio Code

   1. Ouvrez **Visual Studio Code**.
   1. Sélectionnez **Teams Toolkit** dans la barre d’activité.
   1. Sélectionnez **Ajouter des fonctionnalités** sous **DÉVELOPPEMENT**.

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/select-feature-updated.png" alt-text="Ajouter une fonctionnalité à partir du Kit de ressources Teams":::

### <a name="to-add-cloud-resources-by-using-command-palette"></a>Pour ajouter des ressources cloud à l’aide de la palette de commandes

   1. Sélectionnez **Afficher** >  la **palette de commandes...** ou **Ctrl+Maj+P**.

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features.png" alt-text="Ajouter une fonctionnalité à partir de la palette de commandes":::

   1. Entrez **Teams : Ajouter des fonctionnalités**.
   1. Appuyez sur **Entrée**.

      :::image type="content" source="../assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features1.png" alt-text="Tapez ajouter une fonctionnalité et entrez":::

   1. Dans la fenêtre contextuelle, sélectionnez les **ressources cloud** à ajouter à votre projet.

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/updated-final-cloud.png" alt-text="Final":::

  > [!NOTE]
  > Vous devez provisionner pour chaque environnement, une fois que vous avez ajouté la ressource dans votre application Teams.

### <a name="add-cloud-resources-using-teamsfx-cli"></a>Ajouter des ressources cloud à l’aide de l’interface CLI TeamsFx

* Remplacez le répertoire par votre **répertoire du projet**.
* Le tableau suivant répertorie les fonctionnalités et les commandes requises :

  |Ressource cloud|Commande|
  |---------------|----------|
  | Fonction Azure|`teamsfx add azure-function`|
  | Base de données SQL Azure|`teamsfx add azure-sql`|
  | Gestion des API Azure|`teamsfx add azure-apim`|
  | Azure Key Vault|`teamsfx add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>Types de ressources cloud

Dans les scénarios suivants, TeamsFx s’intègre aux services Azure :

* [Azure Functions](/azure/azure-functions/functions-overview) : solution sans serveur pour répondre à vos exigences à la demande, telles que la création d’API web pour votre backend d’applications Teams.
* [Base de données SQL Azure](/azure/azure-sql/database/sql-database-paas-overview) : moteur de base de données PaaS (Platform-as-a-Service) qui vous sert de magasin de données d’applications Teams.
* [Gestion des API Azure](deploy.md) : une passerelle d’API peut être utilisée pour administrer les API créées pour les applications Teams et les publier pour les utiliser sur d’autres applications, telles que les applications Power.
* [Azure Key Vault](/azure/key-vault/general/overview) : protégez les clés de chiffrement et d’autres clés secrètes utilisées par les applications et les services cloud.

## <a name="changes-after-adding-cloud-resources"></a>Modifications après l’ajout de ressources cloud

Les modifications suivantes apparaissent après l’ajout de ressources dans votre projet :

* Nouveaux paramètres ajoutés à azure.parameter. {env}.json pour fournir les informations requises pour l’approvisionnement.
* Le nouveau contenu est inclus dans le modèle ARM sous `templates/azure`, sauf que les fichiers sont dans `templates/azure/teamsfx` le dossier pour l’ajout des ressources Azure.
* Les fichiers sous le dossier `templates/azure/teamsfx` sont régénérés pour garantir que la configuration requise de TeamsFx est à jour pour les ressources Azure ajoutées.
* `.fx/projectSettings.json` est mis à jour pour suivre les ressources disponibles dans votre projet.

Les modifications supplémentaires suivantes s’affichent après l’ajout de ressources dans votre projet :

|Ressources|Modifications|Description|
|---------------|---------------|-----------------------------|
|Azure Functions|Un code de modèle Azure Functions est ajouté dans un sous-dossier avec le chemin d’accès `yourProjectFolder/api`</br></br>`launch.json` et `task.json` sont mis à jour sous le dossier `.visual studio code`.| Inclut un modèle de déclencheur HTTP Hello World dans votre projet.</br></br> Inclut les scripts nécessaires pour Visual Studio Code à exécuter lorsque vous souhaitez déboguer votre application de manière locale.|
|Gestion des API Azure|Fichier de spécification d’API ouvert ajouté dans un sous-dossier avec le chemin d’accès `yourProjectFolder/openapi`|Définit votre API après la publication. Il s’agit du fichier de spécification de l’API.|

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Créer une application Teams](create-new-project.md)
* [Ajouter des fonctionnalités aux applications Teams](add-capability.md)
* [Déployer à partir du cloud](deploy.md)
