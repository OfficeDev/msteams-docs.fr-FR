---
title: Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud
author: MuyangAmigo
description: Provisionner des ressources cloud
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6ab903ab731e3fe90161d2873f0ca8be5ed284fa
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757457"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud

TeamsFx s’intègre à Azure et Microsoft 365 cloud, ce qui vous permet de placer votre application dans Azure avec une seule commande. TeamsFx s’intègre à Azure Resource Manager qui vous permet de provisionner des ressources Azure, dont votre application a besoin pour l’approche du code.  

## <a name="prerequisites"></a>Configuration requise

* Prérequis du compte Pour provisionner des ressources cloud, vous devez disposer des comptes suivants :

  * Microsoft 365 compte avec un abonnement valide.
  * Azure avec un abonnement valide.
  Pour plus d’informations, consultez [comment préparer des comptes pour la création d’Teams application](accounts.md).

* [Installez le Kit de ressources Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Vérifiez que vous avez Teams projet d’application ouvert dans VS Code.

## <a name="provision-using-teams-toolkit"></a>Provisionner à l’aide de Teams Shared Computer Toolkit

L’approvisionnement est effectué avec une seule commande dans Teams Shared Computer Toolkit pour Visual Studio Code ou TeamsFx CLI comme suit :

[Provisionner une application basée sur Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

## <a name="resource-creation"></a>Création de ressources

Lorsque vous déclenchez la commande de provisionnement dans Teams Shared Computer Toolkit ou TeamsFx CLI, vous pouvez obtenir les ressources suivantes :

* Microsoft Azure Active Directory application (Azure AD) sous votre locataire Microsoft 365.
* Teams inscription d’application sous la plateforme Teams de votre locataire Microsoft 365.
* Ressources Azure sous votre abonnement Azure sélectionné.

Lorsque vous créez un projet, vous pouvez utiliser toutes les ressources Azure. Le modèle ARM définit toutes les ressources Azure et permet de créer les ressources Azure nécessaires lors de l’approvisionnement. Lorsque vous [ajoutez une nouvelle ressource de fonctionnalité](./add-resource.md) à un projet existant, le modèle ARM mis à jour reflète la dernière modification.

> [!NOTE]
> Les services Azure entraînent des coûts dans votre abonnement. Pour plus d’informations sur l’estimation des coûts, consultez [la calculatrice de prix](https://azure.microsoft.com/pricing/calculator/).

### <a name="resource-creation-for-teams-tab-application"></a>Création de ressources pour l’onglet de l’application Teams

|Ressource|Objectif|Description |
|----------|--------------------------------|-----|
| Stockage Azure | Héberger votre application onglet | Active la fonction d'application web statique pour héberger votre application d'onglet. |
| Plan App Service pour l’authentification simple | Héberger l’application web de l’authentification simple |Non applicable |
| Application web pour l’authentification simple | Héberger un serveur d’authentification simple pour accéder à d’autres services dans votre application monopage | Ajoute une identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

### <a name="resource-creation-for-teams-bot-or-message-extension-application"></a>Création de ressources pour Teams application d’extension de bot ou de message

|Ressource|Objectif| Description |
|----------|--------------------------------|-----|
| Service de bot Azure | Inscrit votre application en tant que bot avec l’infrastructure de bot. | Connecte le bot à Teams. |
| Plan App Service pour le bot | Héberger l’application web du bot |Non applicable |
| Application web pour bot | Héberger votre application bot | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. <br /> Ajoute les paramètres d’application requis par le [Kit de développement logiciel (SDK) TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

### <a name="resource-creation-for-azure-functions-in-the-project"></a>Création de ressources pour Azure Functions dans le projet

|Ressource|Objectif| Description|
|----------|--------------------------------|-----|
| Plan App Service pour l’application de fonction | Héberger l’application de fonction |Non applicable |
| Application de la fonction | Héberger vos API Azure Functions | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. <br /> Ajoute une règle de partage des ressources d'origine croisée (CORS) pour autoriser les requêtes provenant de votre application d'onglet. <br /> Ajoute un paramètre d’authentification qui autorise uniquement les demandes de votre application Teams. <br /> Ajoute les paramètres d’application requis par le [Kit de développement logiciel (SDK) TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx). |
| Stockage Azure pour l’application de fonction | Requis pour créer une application de fonction |Non applicable|
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

### <a name="resource-creation-for-azure-sql-in-the-project"></a>Création de ressources pour Azure SQL dans le projet

|Ressource|Objectif | Description |
|----------|--------------------------------|-----|
| Azure SQL et SQL Server | Héberger l’instance de base de données Azure SQL | Permet à tous les services Azure d’accéder au serveur. |
| Base de données Azure SQL | Stocker des données pour votre application | Octroie à l’utilisateur l’autorisation d’identité, de lecture ou d’écriture attribuée à la base de données. |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

### <a name="resource-creation-for-azure-api-management-in-the-project"></a>Création de ressources pour Azure Gestion des API dans le projet

|Ressource|Objectif|
|----------|--------------------------------|
| Application Azure AD pour le service de gestion des API | Autorise les API d’accès Microsoft Power Platform gérées par le service de gestion des API. |
| Service de gestion des API | Gérer vos API hébergées dans l’application de fonction |
| Produit de gestion des API | Regrouper vos API, définir les conditions d’utilisation et les stratégies d’exécution |
| Serveur OAuth de gestion des API | Permet à Microsoft Power Platform d’accéder à vos API hébergées dans l’application de fonction. |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure |

### <a name="resources-created-when-including-azure-key-vault-in-the-project"></a>Ressources créées lors de l’inclusion d’Azure Key Vault dans le projet

|Ressources|Objectif de cette ressource|
|----------|--------------------------------|
| Azure Key Vault | Gérer les secrets (par exemple, Azure AD secret client d’application) utilisés par d’autres services Azure |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure |

## <a name="customize-resource-provision"></a>Personnaliser l’approvisionnement des ressources

Teams Shared Computer Toolkit vous permet d’utiliser une infrastructure comme approche de code pour définir les ressources Azure que vous souhaitez approvisionner et la façon dont vous souhaitez configurer. L’outil utilise un modèle ARM pour définir des ressources Azure. Le modèle ARM est un ensemble de fichiers bicep qui définit l’infrastructure et la configuration de votre projet. Vous pouvez personnaliser les ressources Azure en modifiant le modèle ARM. Pour plus d’informations sur Intune, consultez ce [document biceps](/azure/azure-resource-manager/bicep).

L’approvisionnement avec ARM implique la modification des ensembles de fichiers, paramètres et modèles suivants :

* Fichiers de paramètre ARM (`azure.parameters.{your_env_name}.json`) situés dans le `.fx/configs` dossier, pour passer des paramètres aux modèles
* Fichiers de modèle ARM situés dans `templates/azure`, ce dossier contient les fichiers suivants :

| Fichier | Fonction | Autoriser la personnalisation des fichiers |
| --- | --- | --- |
| main.bicep | Fournir un point d’entrée pour l’approvisionnement de ressources Azure | Oui |
| provision.bicep | Créer et configurer des ressources Azure | Oui |
| config.bicep | Ajouter les configurations requises TeamsFx aux ressources Azure | Oui |
| provision/xxx.bicep | Créer et configurer chaque ressource Azure consommée par `provision.bicep` | Oui |
| teamsfx/xxx.bicep | Ajouter les configurations requises TeamsFx à chaque ressource Azure consommée par `config.bicep`| Non |

> [!NOTE]
> Lorsque vous ajoutez des ressources ou des fonctionnalités à votre projet, `teamsfx/xxx.bicep` qui seront régénérées, vous ne pouvez pas personnaliser la même chose. Pour modifier les fichiers bicep, vous pouvez utiliser Git pour suivre vos modifications apportées aux `teamsfx/xxx.bicep` fichiers, ce qui vous permet de ne pas perdre les modifications lors de l’ajout de ressources ou de fonctionnalités.

### <a name="customize-arm-parameters-and-templates"></a>Personnaliser les paramètres et modèles ARM

Vous pouvez personnaliser les ressources Azure en personnalisant les fichiers de paramètres et en personnalisant les fichiers bicep.

#### <a name="customize-arm-template-parameter-files"></a>Personnaliser les fichiers de paramètres du modèle ARM

Le kit de ressources fournit un ensemble de paramètres prédéfinis pour personnaliser les ressources Azure. Les fichiers de paramètres se trouvent dans `.fx/configs/azure.parameters.{env}.json` et tous les paramètres disponibles sont définis dans la `provisionParameters` propriété. Il est recommandé de personnaliser les fichiers de paramètres si les paramètres prédéfinis satisfont à vos besoins.

Le tableau suivant fournit la liste des paramètres prédéfinis disponibles :

| Nom du paramètre | Valeur par défaut | Ce qui peut être personnalisé par le paramètre. | Contraintes de valeur |
| --- | --- | --- | --- |
| resourceBaseName | Généré automatiquement pour chaque environnement | Nom par défaut pour toutes les ressources | 2 à 20 lettres minuscules et chiffres |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | Nom du plan App Service d’authentification simple | 1 à 40 caractères alphanumériques et traits d’union |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | Nom de l’application web d’authentification simple | 2 à 60 caractères alphanumériques et traits d’union <br /> Impossible de démarrer ou de se terminer par un trait d’union |
| simpleAuthSku | F1 | Référence SKU d’un plan App Service d’authentification simple | Non applicable |
| frontendHostingStorageName | Onglet ${resourceBaseName} | Nom du compte de stockage d’hébergement frontal | 3-24 lettres minuscules et chiffres |
| frontendHostingStorageSku | StandardLRS | Référence SKU du compte de stockage d’hébergement front-end |[Références SKU disponibles](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep)|
| functionServerfarmsName | ${resourceBaseName}api | Nom du plan de service des applications de fonction | 1 à 40 caractères alphanumériques et traits d’union |
| functionServerfarmsSku | Y1 | Référence SKU du plan de service des applications de fonction | Non applicable|
| functionAppName | ${resourceBaseName}api | Nom de l’application de fonction | 2 à 60 caractères alphanumériques et traits d’union <br /> Impossible de démarrer ou de se terminer par un trait d’union |
| functionStorageName | ${resourceBaseName}api | Nom du compte de stockage de l’application de fonction | 3-24 lettres minuscules et chiffres |
| functionStorageSku | StandardLRS | Référence SKU du compte de stockage de l’application de fonction | [Références SKU disponibles](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep) |
| botServiceName | ${resourceBaseName} | Nom du service de bot Azure | 2-64 caractères alphanumériques, traits de soulignement, point et traits d’union <br /> Commencer par alphanumérique |
| botServiceSku | F0 | SKU du service Azure bot | [SKU disponibles](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep) |
| botDisplayName | ${resourceBaseName} | Nom complet de votre bot | 1 à 42 caractères |
| botServerfarmsName | ${resourceBaseName}bot | Nom du plan App Service du bot | 1 à 40 caractères alphanumériques et traits d’union |
| botWebAppName | ${resourceBaseName}bot | Nom de l’application web du bot | 2 à 60 caractères alphanumériques et traits d’union <br /> Impossible de démarrer ou de se terminer par un trait d’union |
| botWebAppSKU | F1 | SKU du plan Bot App Service | Non applicable |
| userAssignedIdentityName | ${resourceBaseName} | Nom de l’identité affectée par l’utilisateur | 3-128 caractères alphanumériques, traits d’union et traits de soulignement <br /> Commencer par une lettre ou un numéro |
| sqlServerName | ${resourceBaseName} | Nom du serveur Azure SQL | 1 à 63 lettres minuscules, chiffres et traits d’union <br /> Impossible de démarrer ou de se terminer par un trait d’union |
| sqlDatabaseName | ${resourceBaseName} | Nom de Azure SQL base de données | 1-128 caractères, ne peut pas utiliser <>*%&:\/? ou caractères de contrôle <br /> Ne peut pas se terminer par un point ou un espace. |
| sqlDatabaseSku | De base | SKU de base de données Azure SQL | Non applicable  |
| apimServiceName | ${resourceBaseName} | Nom du service APIM | 1-50 caractères alphanumériques et traits d’union <br /> Commencez par la lettre et terminez par alphanumérique. |
| apimServiceSku | Modèle de consommation | SKU du service APIM | [Références SKU disponibles](/azure/templates/microsoft.apimanagement/service?tabs=bicep) |
| apimProductName | ${resourceBaseName} | Nom du produit APIM | 1-80 alphanumériques et traits d’union <br /> Commencez par la lettre et terminez par alphanumérique. |
| apimOauthServerName | ${resourceBaseName} | Nom du serveur OAuth APIM | 1-80 alphanumériques et traits d’union <br /> Commencez par la lettre et terminez par alphanumérique. |
| keyVaultSkuName | standard | Nom de la référence SKU d’Azure Key Vault Service| |

Dans le même temps, les paramètres suivants sont disponibles avec des valeurs renseignées pendant l’approvisionnement. L’objectif de ces espaces réservés est de nous assurer que nous pouvons créer de nouvelles ressources pour vous dans un nouvel environnement. Les valeurs réelles sont résolues à partir de `.fx/states/state.{env}.json`.

##### <a name="azure-ad-application-related-parameters"></a>Paramètres Azure AD liés à l’application

| Nom du paramètre | Détenteur de place de valeur par défaut | Signification du titulaire de place | Comment créer et personnaliser des applications ? |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | ID client d’application Azure AD de votre application créé lors de l’approvisionnement | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | Clé secrète client Azure AD de votre application créée lors de l’approvisionnement | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | ID de locataire de l’application Azure AD de votre application | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Hôte d’autorité OAuth de l’application Azure AD de votre application | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | ID client de l’application Azure AD bot créé lors de l’approvisionnement | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secret client de l’application Azure AD du bot créé lors de l’approvisionnement | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-bot) |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | ID client d’application Azure AD APIM créé lors de l’approvisionnement | Supprimer l’espace réservé et remplir la valeur réelle |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | Clé secrète client d’application Azure AD APIM créée lors de l’approvisionnement | Supprimer l’espace réservé et remplir la valeur réelle |

##### <a name="azure-resource-related-parameters"></a>Paramètres liés aux ressources Azure

| Nom du paramètre | Détenteur de place de valeur par défaut | Signification du titulaire de place | Comment créer et personnaliser des applications ? |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Compte d'administrateur Azure SQL Server que vous avez fourni lors de l'approvisionnement | Supprimer l’espace réservé et remplir la valeur réelle |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Le mot de passe de l'administrateur du serveur SQL Azure que vous avez fourni lors de la mise à disposition. | Supprimer l’espace réservé et remplir la valeur réelle |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | E-mail de l’éditeur d’APIM, la valeur par défaut est votre compte Azure | Supprimer l’espace réservé et remplir la valeur réelle |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | Nom de l’éditeur d’APIM, la valeur par défaut est votre compte Azure | Supprimer l’espace réservé et remplir la valeur réelle |

#### <a name="referencing-environment-variables-in-parameter-files"></a>Référencement de variables d’environnement dans des fichiers de paramètres

Si vous ne souhaitez pas coder en dur les valeurs dans les fichiers de paramètres, par exemple, lorsque la valeur est un secret. Les fichiers de paramètres prennent en charge le référencement des valeurs à partir de variables d’environnement. Vous pouvez utiliser la syntaxe `{{$env.YOUR_ENV_VARIABLE_NAME}}` dans les valeurs de paramètre de l’outil pour résoudre à partir de la variable d’environnement actuelle.

L’exemple suivant lit la valeur du paramètre à `mySelfHostedDbConnectionString` partir de la variable `DB_CONNECTION_STRING`d’environnement :

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>Personnaliser les fichiers de modèle ARM

Si les modèles prédéfinis ne répondent pas aux exigences de votre application, vous pouvez personnaliser les modèles ARM sous le `templates/azure` dossier. Par exemple, vous pouvez personnaliser le modèle ARM pour créer des ressources Azure supplémentaires pour votre application. Vous devez avoir des connaissances de base du langage bicep, qui est utilisé pour créer un modèle ARM. Vous pouvez commencer à utiliser bicep dans la [documentation bicep](/azure/azure-resource-manager/bicep/).

> [!NOTE]
> Le modèle ARM est partagé par tous les environnements. Vous pouvez utiliser le [déploiement conditionnel](/azure/azure-resource-manager/bicep/conditional-resource-deployment) si le comportement de provisionnement varie d’un environnement à l’autre.

Pour vous assurer que l’outil TeamsFx fonctionne correctement, veillez à personnaliser le modèle ARM, qui répond aux exigences suivantes. Si vous utilisez un autre outil pour un développement ultérieur, vous pouvez ignorer ces exigences.

* Conservez la structure des dossiers et le nom de fichier inchangés. L’outil peut ajouter du nouveau contenu à des fichiers existants lorsque vous ajoutez des ressources ou des fonctionnalités supplémentaires à votre projet.
* Conservez le nom des paramètres générés automatiquement ainsi que les noms de propriétés inchangés. Les paramètres générés automatiquement peuvent être utilisés lorsque vous ajoutez des ressources ou des fonctionnalités supplémentaires à votre projet.
* Conservez inchangée la sortie du modèle ARM généré automatiquement. Vous pouvez ajouter des sorties supplémentaires au modèle ARM. La sortie est `.fx/states/state.{env}.json` et peut être utilisée dans d’autres fonctionnalités telles que le déploiement, la validation du fichier manifeste.

### <a name="customization-scenarios"></a>Scénarios de personnalisation

Vous pouvez créer un abonnement pour les scénarios suivants :

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Utiliser une application Azure AD existante pour votre bot

Vous pouvez ajouter l’extrait de configuration suivant au `.fx/configs/config.{env}.json` fichier pour utiliser une application Azure AD créée par vous-même pour votre application Teams. Pour créer une application Azure AD, consultez <https://aka.ms/teamsfx-existing-aad-doc>.

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Après avoir ajouté l’extrait de code, ajoutez votre secret à la variable d’environnement associée afin que l’outil puisse résoudre le secret réel pendant l’approvisionnement.

> [!NOTE]
> Veillez à ne pas partager la même application Azure AD dans plusieurs environnements. Si vous n’êtes pas autorisé à mettre à jour l’application Azure AD, vous pouvez recevoir un avertissement avec des instructions sur la façon de mettre à jour manuellement l’application Azure AD. Suivez les instructions pour mettre à jour votre application Azure AD après l’approvisionnement.

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Utiliser une application Azure AD existante pour votre application Teams

Vous pouvez ajouter l’extrait de configuration suivant au `.fx/configs/config.{env}.json` fichier pour utiliser une application Azure AD créée par vous-même pour votre bot :

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Après avoir ajouté l’extrait de code précédent, ajoutez votre secret à la variable d’environnement associée pour que l’outil résolvent le secret réel pendant l’approvisionnement.

#### <a name="skip-adding-user-for-sql-database"></a>Ignorer l’ajout d’un utilisateur pour SQL base de données

Si l’erreur d’autorisation est insuffisante lorsque l’outil tente d’ajouter un utilisateur à SQL base de données, vous pouvez ajouter l’extrait de configuration suivant au `.fx/configs/config.{env}.json` fichier pour ignorer l’ajout de SQL utilisateur de base de données :

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Spécification du nom de l’instance Function App

Vous pouvez utiliser `contosoteamsappapi` l’instance d’application de fonction au lieu d’utiliser le nom par défaut.

> [!NOTE]
> Si vous avez déjà approvisionné l’environnement, la spécification du nom peut créer une instance d’application de fonction pour vous, au lieu de renommer l’instance créée précédemment.

Les étapes suivantes seront :

1. Ouvert `.fx/configs/azure.parameters.{env}.json` pour votre environnement actuel
2. Ajoutez une nouvelle propriété `functionAppName` à la valeur du paramètre `provisionParameters`.
3. Entrez `contosoteamsappapi` comme valeur de `functionAppName`.
4. Le fichier de paramètre final s’affiche dans l’extrait de code suivant :

    ```json
    {
        "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "provisionParameters": {
            "value": {
                "functionAppName": "contosoteamsappapi"
                ...
                }
            }
        }
    }
    ```

### <a name="scenerio"></a>Scenario

Pour ajouter d’autres ressources ou stockage Azure à l’application :

Prenons le scénario suivant : vous souhaitez ajouter le stockage Azure à votre serveur principal de fonction Azure pour stocker les données blob. Il n’existe aucun flux automatique pour mettre à jour le modèle bicep avec la prise en charge du stockage Azure. Toutefois, vous pouvez modifier le fichier bicep et ajouter la ressource. Les étapes sont les suivantes :

1. Créer un projet d’onglet Microsoft Teams
2. Ajoutez une fonction au projet. Pour plus d’informations, consultez [ajouter des ressources](./add-resource.md).
3. Déclarez le nouveau compte de stockage dans le modèle ARM. Vous pouvez déclarer la ressource `templates/azure/provision/function.bicep` directement. Vous êtes libre de déclarer les ressources à d’autres endroits.

    `````````bicep
    var applicationStorageAccountName = 'myapp${uniqueString(resourceGroup().id)}'
    resource applicationStorageAccount 'Microsoft.Storage/storageAccounts@2021-06-01' = {
        name: applicationStorageAccountName
        location: resourceGroup().location
        kind: 'Storage'
        sku: {
            name: 'Standard_LRS'
        }
    }
    `````````

4. Mettez à jour les paramètres de l’application de fonction Azure avec la chaîne de connexion de stockage Azure dans `templates/azure/provision/function.bicep`. Ajoutez l’extrait de code suivant au `functionApp` tableau de la `appSettings` ressource :

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. Vous pouvez mettre à jour votre fonction avec des liaisons de sortie de stockage Azure.

## <a name="faq"></a>FAQ

<br>

<details>

<summary><b>Procédure de dépannage ?</b></summary>

Si vous obtenez des erreurs avec Teams Shared Computer Toolkit dans Visual Studio Code, vous pouvez sélectionner **Obtenir de l’aide** dans la notification d’erreur pour accéder au document associé. Si vous utilisez l’interface CLI TeamsFx, un lien hypertexte à la fin du message d’erreur pointe vers la documentation d’aide. Vous pouvez également consulter directement la [documentation d’aide sur l’approvisionnement](https://aka.ms/teamsfx-arm-help) .

<br>

</details>

<details>

<summary><b>Comment puis-je basculer vers un autre abonnement Azure lors de l’approvisionnement ?</b></summary>

1. Basculez l’abonnement dans le compte actuel ou déconnectez-vous et sélectionnez un nouvel abonnement.
2. Si vous avez déjà approvisionné l’environnement actuel, vous devez créer un environnement et effectuer l’approvisionnement, car ARM ne prend pas en charge le déplacement des ressources.
3. Si vous n’avez pas approvisionné l’environnement actuel, vous pouvez déclencher l’approvisionnement directement.

<br>

</details>

<details>

<summary><b>Comment puis-je modifier le groupe de ressources lors de l’approvisionnement ?</b></summary>

Avant l’approvisionnement, l’outil vous demande si vous souhaitez créer un groupe de ressources ou en utiliser un existant. Vous pouvez fournir un nouveau nom de groupe de ressources ou en choisir un existant dans cette étape.

<br>

</details>

<details>

<summary><b>Comment puis-je provisionner une application basée sur Sharepoint ?</b></summary>

Vous pouvez suivre [l’approvisionnement SharePoint application basée sur](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4).

> [!NOTE]
> Actuellement, la création Teams application avec sharepoint framework avec Teams Shared Computer Toolkit n’a pas d’intégration directe avec Azure. Le contenu de la documentation ne s’applique pas aux applications basées sur SPFx.

<br>

</details>

## <a name="see-also"></a>Voir aussi

* [Déployer l’application Teams dans le cloud](deploy.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
* [Collaborer avec d’autres développeurs sur des projets Teams](TeamsFx-collaboration.md)
