---
title: Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud
author: MuyangAmigo
description: Mise en service des ressources cloud
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: c8899131876533fdd64913fb6790cff9f258e8f5
ms.sourcegitcommit: aede47694894d281f6b725083bc0b46ab0e4846d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2021
ms.locfileid: "61591784"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud

TeamsFx offre une intégration transparente avec Azure et Microsoft 365 cloud qui vous permet de placer votre application dans Azure avec une seule commande. TeamsFx s’intègre à Azure Resource Manager qui vous permet de mettre en service de façon déclarative des ressources Azure dont votre application a besoin en utilisant l’infrastructure comme approche de code.  

## <a name="prerequisites"></a>Configuration requise

* Conditions préalables pour le compte

    Pour mettre en service des ressources cloud, vous devez avoir les comptes suivants avec les autorisations appropriées. Pour plus d’informations, voir [préparer les comptes pour créer Teams’application.](accounts.md)
    * Microsoft 365
    * Azure avec un abonnement valide

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Un projet d’application Teams doit déjà être ouvert dans du code VS.

## <a name="provision-using-teams-toolkit"></a>Approvisionnement à l’aide Teams Shared Computer Toolkit

L’approvisionnement est effectué avec une seule commande Teams Shared Computer Toolkit pour Visual Studio Code ou l’CLI TeamsFx comme suit :

[Mise en service d’une application azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)

## <a name="resource-creation"></a>Création de ressources

Lorsque vous déclenchez une commande de mise en service dans Teams Shared Computer Toolkit ou l’CLI TeamsFx, vous pouvez obtenir les ressources suivantes :

* AAD application sous votre client Microsoft 365 client
* Teams’inscription d’application sous la plateforme Microsoft 365 de votre client Teams client
* Ressources Azure sous votre abonnement Azure sélectionné

Lorsque vous créez un projet, vous obtenez toutes les ressources Azure à créer. Le modèle ARM définit toutes les ressources Azure et permet de créer les ressources Azure requises lors de la mise en service. Lorsque vous [ajoutez une nouvelle fonctionnalité/ressource](./add-resource.md) à un projet existant, le modèle ARM mise à jour reflète la dernière modification.

> [!NOTE]
> Azure services incur costs in your subscription, you can refer to [pricing calculator](https://azure.microsoft.com/pricing/calculator/) to understand an estimate.

### <a name="resource-creation-for-teams-tab-application"></a>Création de ressources pour l Teams’onglet

|Ressources|Objectif de cette ressource| Remarques |
|----------|--------------------------------|-----|
| Stockage Azure | Héberger votre application d’onglet | Permet à la fonctionnalité d’application web statique d’héberger votre application Onglet |
| App Service Plan for Simple Auth | Héberger l’application web d’th simple | |
| Application web pour th simple | Héberger un serveur d’th simple qui vous permet d’accéder à d’autres services dans votre application à page unique | Ajoute l’identité attribuée à l’utilisateur pour faciliter l’accès à d’autres ressources Azure |
| Identité attribuée à l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

### <a name="resources-created-for-teams-bot-or-messaging-extension-application"></a>Ressources créées pour Teams application Bot ou Extension de messagerie

|Ressources|Objectif de cette ressource| Remarques |
|----------|--------------------------------|-----|
| Azure Bot Service | Enregistre votre application en tant que bot avec Bot Framework | Connecte le bot à Teams |
| Plan de service d’application pour bot | Héberger l’application web du bot | |
| Application web pour bot | Héberger votre application de bot | Ajoute l’identité attribuée à l’utilisateur pour faciliter l’accès à d’autres ressources Azure. <br /> Ajoute les paramètres d’application requis par [le SDK TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Identité attribuée à l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

### <a name="resources-created-when-including-azure-functions-in-the-project"></a>Ressources créées lors de l’inclure à des fonctions Azure dans le projet

|Ressources|Objectif de cette ressource| Remarques |
|----------|--------------------------------|-----|
| Plan du service d’application pour function app | Héberger l’application de fonction | |
| Function App | Héberger vos API de fonctions Azure | Ajoute l’identité attribuée à l’utilisateur pour faciliter l’accès à d’autres ressources Azure. <br /> Ajoute une règle CORS pour autoriser les demandes à partir de votre application d’onglet <br /> Ajoute un paramètre d’authentification qui autorise uniquement les demandes provenant de votre Teams application. <br /> Ajoute les paramètres d’application requis par [le SDK TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| stockage Azure pour Function App | Obligatoire lors de la création de Function App | |
| Identité attribuée à l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

### <a name="resources-created-when-including-azure-sql-in-the-project"></a>Ressources créées lors de l’SQL Azure dans le projet

|Ressources|Objectif de cette ressource| Remarques |
|----------|--------------------------------|-----|
| Azure SQL Server | Héberger l’instance Azure SQL Database instance | Permet à tous les services Azure d’accéder au serveur |
| Base de données Azure SQL | Stocker des données pour votre application | Accorde à l’utilisateur une autorisation de lecture/écriture sur la base de données |
| Identité attribuée à l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

### <a name="resources-created-when-including-azure-api-management-in-the-project"></a>Ressources créées lors de l’inclure à la gestion des API Azure dans le projet

|Ressources|Objectif de cette ressource|
|----------|--------------------------------|
| Azure Active Directory application de gestion des API | Permet aux API d’accès microsoft Power Platform gérées par le service de gestion des API |
| Service de gestion des API | Gérer vos API hébergées dans Function App |
| Produit de gestion des API | Grouper vos API, définir les conditions d’utilisation et les stratégies d’utilisation |
| Gestion des API OAuth Server | Permet à Microsoft Power Platform d’accéder à vos API hébergées dans Function App |
| Identité attribuée à l’utilisateur | Authentifier les demandes de service à service Azure |

## <a name="customize-resource-provision"></a>Personnaliser la mise en service des ressources

Teams Shared Computer Toolkit vous permet d’utiliser une infrastructure comme approche de code pour définir les ressources Azure que vous souhaitez mettre en service et la façon dont vous souhaitez les configurer. Les outils utilisent ARM modèle pour définir des ressources Azure. Le ARM est un ensemble de fichiers biceps qui définit l’infrastructure et la configuration de votre projet. Vous pouvez personnaliser les ressources Azure créées en modifiant ARM modèle. Pour plus d’informations, [voir le document bicep.](/azure/azure-resource-manager/bicep.md) La mise en service ARM implique la modification des deux jeux de fichiers, paramètres et modèles suivants :

* ARM fichiers de paramètres ( ) se trouvent dans le dossier, pour transmettre des `azure.parameters.{your_env_name}.json` `.fx/configs` paramètres à des modèles.
* ARM de modèles situés à `templates/azure` l’emplacement , ce dossier contient les fichiers suivants :

| Fichier | Que fait-il ? | Autoriser la personnalisation |
| --- | --- | --- |
| main.bicep | Fournir un point d’entrée pour la mise en service des ressources Azure | Oui |
| provision.bicep | Créer et config des ressources Azure | Oui |
| config.bicep | Ajouter des configurations teamsFx requises aux ressources Azure | Oui |
| provision/xxx.bicep | créer et configer chaque ressource Azure consommée par `provision.bicep` | Oui |
| teamsfx/xxx.bicep | Ajouter les configurations requises TeamsFx à chaque ressource Azure consommée par `config.bicep`| Non |

> [!NOTE]
> lorsque vous ajoutez des ressources ou des fonctionnalités à votre projet, `teamsfx/xxx.bicep` elle est régénérée. C’est pourquoi il est marqué comme non personnalisable. Si vous avez vraiment besoin de modifier ces fichiers biceps, nous vous recommandons d’utiliser Git pour suivre vos modifications apportées aux fichiers afin de ne pas perdre vos modifications lors de l’ajout de ressources ou `teamsfx/xxx.bicep` de fonctionnalités.

### <a name="customize-arm-parameters-and-templates"></a>Personnaliser ARM paramètres et modèles

Vous pouvez personnaliser les ressources Azure en personnalisant les fichiers de paramètres et en personnalisant les fichiers biceps.

#### <a name="customize-arm-template-parameter-files"></a>Personnaliser ARM fichiers de paramètres de modèle

Le kit de ressources fournit un ensemble de paramètres prédéfinits pour vous aider à personnaliser les ressources Azure. Les fichiers de paramètres se trouvent à l’emplacement et tous les `.fx/configs/azure.parameters.{env}.json` paramètres disponibles sont définis dans la `provisionParameters` propriété. Il est préférable de personnaliser les fichiers de paramètres si les paramètres prédéfincis sont satisfaits à vos besoins.

Voici une liste des paramètres prédéfincis disponibles :

| Nom du paramètre | Valeur par défaut | Ce qui peut être personnalisé par le paramètre | Contraintes de valeur |
| --- | --- | --- | --- |
| resourceBaseName | Généré automatiquement pour chaque environnement | Nom par défaut de toutes les ressources | 2 à 20 lettres minuscules et chiffres |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | Nom du plan de service d’th d’th simple | 1 à 40 alphanumériques et tirets |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | Nom de Simple Auth Web App | 2 à 60 alphanumériques et tirets <br /> Impossible de commencer ou de se terminer par un trait d’union |
| simpleAuthSku | F1 | Référence (SKU) du plan de service d’th d’th simple |  |
| frontendHostingStorageName | Onglet ${resourceBaseName}. | Nom du compte d’Stockage frontal | 3 à 24 lettres minuscules et chiffres |
| frontendHostingStorageSku | Standard_LRS | Référence (SKU) du compte Stockage frontal | Reportez-vous [à cette page](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch) pour les références SSO disponibles |
| functionServerfarmsName | ${resourceBaseName}api | Nom du plan de service d’application de Function App | 1 à 40 alphanumériques et tirets |
| functionServerfarmsSku | Y1 | Référence (SKU) du plan de service d’application de l’application FUnction |
| functionAppName | ${resourceBaseName}api | Nom de l’application de fonction | 2 à 60 alphanumériques et tirets <br /> Impossible de commencer ou de se terminer par un trait d’union |
| functionStorageName | ${resourceBaseName}api | Nom du compte Stockage Function App | 3 à 24 lettres minuscules et chiffres |
| functionStorageSku | Standard_LRS | Référence (SKU) du compte Stockage Function App | Reportez-vous [à cette page](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch=pr-en-us-4713)pour les références SSO disponibles |
| botServiceName | ${resourceBaseName} | Nom du service Azure Bot | 2 à 64 caractères alphanumériques, traits de soulignement, point et traits d’union <br /> Commencer par alphanumérique |
| botServiceSku | F0 | Référence (SKU) du service Azure Bot | Reportez-vous [à cette page](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep&branch) pour les références SSO disponibles |
| botDisplayName | ${resourceBaseName} | Nom d’affichage de votre bot | 1 à 42 caractères |
| botServerfarmsName | ${resourceBaseName}bot | Nom du plan de service d’application du bot | 1 à 40 alphanumériques et tirets |
| botWebAppName | ${resourceBaseName}bot | Nom de l’application web du bot | 2 à 60 alphanumériques et tirets <br /> Impossible de commencer ou de se terminer par un trait d’union |
| botWebAppSKU | F1 | Référence (SKU) du plan de service Bot App |  |
| userAssignedIdentityName | ${resourceBaseName} | Nom de l’identité attribuée à l’utilisateur | 3 à 128 caractères alphanumériques, tirets et traits de soulignement <br /> Commencer par une lettre ou un numéro |
| sqlServerName | ${resourceBaseName} | Nom d’Azure SQL Server | 1 à 63 lettres minuscules, chiffres et tirets <br /> Impossible de commencer ou de se terminer par un trait d’union |
| sqlDatabaseName | ${resourceBaseName} | Nom du Azure SQL Database | 1 à 128 caractères, ne peut pas utiliser <>*%&: \/ ? ou des caractères de contrôle <br /> Ne peut pas se terminer par un point ou un espace |
| sqlDatabaseSku | De base | Référence (SKU) de Azure SQL Database |  |
| apimServiceName | ${resourceBaseName} | Nom du service APIM | 1 à 50 alphanumériques et tirets <br /> Commencer par une lettre et terminer par alphanumérique |
| apimServiceSku | Consommation | Référence (SKU) du service APIM | Reportez-vous [à cette page](/azure/templates/microsoft.apimanagement/service?tabs=bicep&branch)pour les références SSO disponibles |
| apimProductName | ${resourceBaseName} | Nom du produit APIM | 1 à 80 alphanumériques et tirets <br /> Commencer par une lettre et terminer par alphanumérique |
| apimOauthServerName | ${resourceBaseName} | Nom du serveur OAuth APIM | 1 à 80 alphanumériques et tirets <br /> Commencer par une lettre et terminer par alphanumérique |

En attendant, les paramètres suivants sont disponibles avec les valeurs remplies pendant la mise en service. L’objectif de ces espaces réservé est de nous assurer que nous pouvons créer de nouvelles ressources pour vous lorsque vous avez créé un nouvel environnement. Les valeurs réelles sont résolues à partir de `.fx/states/state.{env}.json` .

##### <a name="aad-application-related-parameters"></a>AAD paramètres liés à l’application

| Nom du paramètre | Titulaire d’une place de valeur par défaut | Signification du titulaire de la place | Comment personnaliser |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | ID client de votre application AAD créé lors de la mise en service | [Reportez-vous à cette section](#use-an-existing-aad-app-for-your-teams-app) pour personnaliser la valeur |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | La secret client de votre application AAD créé lors de la mise en service | [Reportez-vous à cette section](#use-an-existing-aad-app-for-your-teams-app) pour personnaliser la valeur |
| Microsoft 365TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | ID de locataire de l’application AAD application | [Reportez-vous à cette section](#use-an-existing-aad-app-for-your-teams-app) pour personnaliser la valeur |
| Microsoft 365 OauthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Hôte d’autorité OAuth de l’application AAD application | [Reportez-vous à cette section](#use-an-existing-aad-app-for-your-teams-app) pour personnaliser la valeur |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | ID client AAD’application du bot créé lors de la mise en service | [Reportez-vous à cette section](#use-an-existing-aad-app-for-your-bot) pour personnaliser la valeur |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secret client de l’AAD du bot créé lors de la mise en service | [Reportez-vous à cette section](#use-an-existing-aad-app-for-your-bot) pour personnaliser la valeur |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | ID client de l’AAD APIM créé lors de la mise en service | Supprimer l’espace réservé et remplir la valeur réelle |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | La secret client de l’AAD APIM créée lors de la mise en service | Supprimer l’espace réservé et remplir la valeur réelle |

##### <a name="azure-resource-related-parameters"></a>Paramètres liés aux ressources Azure

| Nom du paramètre | Titulaire d’une place de valeur par défaut | Signification du titulaire de la place | Comment personnaliser |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Compte d’administrateur SQL Server Azure que vous avez fourni lors de la mise en service | Supprimer l’espace réservé et remplir la valeur réelle |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Mot de passe SQL Server administrateur Azure que vous avez fourni lors de la mise en service | Supprimer l’espace réservé et remplir la valeur réelle |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | Courrier électronique de l’éditeur de l’APIM, la valeur par défaut est votre compte Azure | Supprimer l’espace réservé et remplir la valeur réelle |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | Nom d’éditeur de l’APIM, la valeur par défaut est votre compte Azure | Supprimer l’espace réservé et remplir la valeur réelle |

#### <a name="referencing-environment-variables-in-parameter-files"></a>Référencement de variables d’environnement dans des fichiers de paramètres

Il peut se peut que vous ne vouliez pas coder en dur les valeurs dans les fichiers de paramètres. Par exemple, lorsque la valeur est un secret. Les fichiers de paramètres peuvent référencer les valeurs des variables d’environnement. Vous pouvez utiliser la syntaxe dans les valeurs de paramètre pour indiquer à l’outil que la valeur doit être résolue à partir de `{{$env.YOUR_ENV_VARIABLE_NAME}}` la variable d’environnement actuelle.

L’exemple suivant lit la valeur du `mySelfHostedDbConnectionString` paramètre à partir de la variable d’environnement `DB_CONNECTION_STRING` :

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>Personnaliser les ARM modèles de fichiers

Si les modèles prédéfincis ne répondent pas aux exigences de votre application, vous pouvez personnaliser les modèles ARM sous `templates/azure` dossier. Par exemple, vous pouvez personnaliser le modèle ARM pour créer des ressources Azure supplémentaires pour votre application. Il s’agit d’un scénario avancé qui nécessite une connaissance de base du langage bicep utilisé pour ARM modèle. Vous pouvez commencer à utiliser le biceps à [l’occasion de la documentation sur le bicep.](/azure/azure-resource-manager/bicep/?branch)
> [!NOTE]
> Le ARM est partagé par tous les environnements. Vous pouvez utiliser le [déploiement conditionnel](/azure/azure-resource-manager/bicep/conditional-resource-deployment?branch) si le comportement de mise en service est divers d’un environnement à l’autre.

Pour vous assurer que les fonctions d’outils TeamsFx fonctionnent correctement, assurez-vous que votre modèle personnalisé ARM répond aux exigences suivantes. Si vous utilisez d’autres outils pour le développement, vous pouvez ignorer ces exigences.

* Conservez la structure du dossier et le nom de fichier inchangés. L’outil peut ajouter un nouveau contenu à des fichiers existants lorsque vous ajoutez des ressources/fonctionnalités supplémentaires à votre projet.
* Conservez le nom des paramètres générés automatiquement ainsi que les noms de ses propriétés inchangés. Les paramètres générés automatiquement peuvent être utilisés lorsque vous ajoutez des ressources/fonctionnalités supplémentaires à votre projet.
* Conservez la sortie du modèle ARM généré automatiquement inchangée. Vous pouvez ajouter des sorties supplémentaires à ARM modèle. La sortie sera persistante et utilisée dans d’autres fonctionnalités telles que déployer, valider le fichier `.fx/states/state.{env}.json` manifeste, etc.

### <a name="customization-scenarios"></a>Scénarios de personnalisation

Voici quelques scénarios courants que vous pouvez personnaliser le comportement de la mise en service.

#### <a name="use-an-existing-aad-app-for-your-teams-app"></a>Utiliser une application AAD existante pour votre Teams de messagerie

Vous pouvez ajouter l’extrait de configuration suivant au fichier pour utiliser une application AAD créée par vous-même pour `.fx/configs/config.{env}.json` Teams application. Pour créer une application AAD, voir <https://aka.ms/teamsfx-existing-aad-doc> .

```json
"auth": {
    "clientId": "<your AAD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your AAD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Après avoir ajouté l’extrait de code ci-dessus, ajoutez votre clé secrète à la variable d’environnement associée afin que les outils peuvent résoudre la clé secrète réelle lors de la mise en service.

> [!NOTE]
> Vous ne devez pas partager une application AAD dans plusieurs environnements. Si vous n’êtes pas autorisé à mettre à jour l’application AAD, vous recevez un avertissement avec des instructions sur la mise à jour manuelle de l’AAD’application. Suivez les instructions pour mettre à jour votre application AAD après la mise en service.

#### <a name="use-an-existing-aad-app-for-your-bot"></a>Utiliser une application AAD existante pour votre bot

Vous pouvez ajouter l’extrait de configuration suivant au fichier pour utiliser une application `.fx/configs/config.{env}.json` AAD créée par vous-même pour votre bot.

```json
"bot": {
    "appId": "<your AAD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Après avoir ajouté l’extrait de code ci-dessus, ajoutez votre clé secrète à la variable d’environnement associée afin que les outils peuvent résoudre la clé secrète réelle lors de la mise en service.

> [!NOTE]
> Vous ne devez pas partager une application AAD dans plusieurs environnements.

#### <a name="skip-adding-user-for-sql-database"></a>Ignorer l’ajout d’utilisateurs SQL base de données

Parfois, vous risquez d’obtenir une erreur d’autorisation insuffisante lorsque l’outil tente d’ajouter un utilisateur à SQL base de données. Vous pouvez ajouter l’extrait de configuration suivant au fichier pour `.fx/configs/config.{env}.json` ignorer l’ajout SQL de base de données.

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Spécification du nom de l’instance function app

Dans cet exemple, je vais spécifier un autre nom pour `contosoteamsappapi` l’instance function app au lieu d’utiliser le nom par défaut.

> [!NOTE]
> Si vous avez déjà mis en service l’environnement, le fait de spécifier le nom crée une nouvelle instance function app pour vous, au lieu de renommer l’instance créée précédemment.

Les étapes suivantes sont les suivantes :

1. Ouvrez `.fx/configs/azure.parameters.{env}.json` pour votre environnement actuel.
2. Ajoutez une nouvelle propriété `functionAppName` à la valeur du paramètre `provisionParameters` .
3. Remplir « contosoteamsappapi » comme valeur de `functionAppName`
4. Le fichier de paramètres final s’affiche comme suit :

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

### <a name="scenerio"></a>Scenerio 

**Pour ajouter d’autres ressources Azure (stockage Azure) à l’application**

Envisagez le scénario, vous souhaitez ajouter des stockage Azure à votre système d’accès de base de fonction Azure pour stocker des données blob. Il n’existe pas de flux automatique pour mettre à jour le modèle bicep avec stockage Azure prise en charge. Toutefois, vous pouvez modifier le fichier biceps et ajouter la ressource. Les étapes sont les suivantes :

1. Créer un projet d’onglet
2. Ajoutez une fonction au projet. Vous pouvez visiter [Ajouter des ressources pour](./add-resource.md) en savoir plus sur l’ajout de ressources.
3. Déclarez le nouveau compte Stockage dans ARM modèle. Pour simplifier, nous déclarerons la ressource `templates/azure/provision/function.bicep` directement. Vous êtes libre de déclarer les ressources à d’autres endroits.

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

4. Mettez à jour l’application de Paramètres Azure avec stockage Azure de connexion dans , qui est le même `templates/azure/provision/function.bicep` fichier à l’étape 3. Ajoutez l’extrait de code suivant `functionApp` au tableau de `appSettings` ressources.

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. Vous pouvez maintenant mettre à jour votre fonction avec stockage Azure de sortie.

## <a name="faq"></a>FAQ

<br>

<details>

<summary><b>Comment résoudre les problèmes ?</b></summary>

Si vous avez rencontré des erreurs Teams Shared Computer Toolkit dans Visual Studio Code, vous pouvez cliquer sur le bouton de la notification d’erreur pour accéder à la documentation `Get Help` d’aide associée. Si vous utilisez l’CLI TeamsFx, un lien hypertexte à la fin du message d’erreur pointe vers le document d’aide. Vous pouvez également afficher directement la [documentation d’aide](https://aka.ms/teamsfx-arm-help) relative à la mise en service.

<br>

</details>

<details>

<summary><b>Comment puis-je basculer vers un autre abonnement Azure lors de l’approvisionnement ?</b></summary>

1. Changez d’abonnement dans le compte actuel ou déconnectez-vous, puis sélectionnez un nouvel abonnement.
2. Si vous avez déjà mis en service l’environnement actuel, vous devez créer un nouvel environnement et effectuer l’approvisionnement, car ARM ne prend pas en charge le déplacement de ressources.
3. Si vous n’avez pas provisioné l’environnement actuel, vous pouvez déclencher l’approvisionnement directement.

<br>

</details>

<details>

<summary><b>Comment puis-je modifier le groupe de ressources lors de l’approvisionnement ?</b></summary>

Avant la mise en service, l’outil vous demande si vous souhaitez créer un groupe de ressources ou utiliser un groupe existant. Vous pouvez fournir un nouveau nom de groupe de ressources ou en choisir un existant dans cette étape.

<br>

</details>

<details>

<summary><b>Comment puis-je SharePoint une application basée sur un système ?</b></summary>

Vous pouvez suivre [l’SharePoint pour mettre](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch) en service SharePoint’application basée sur la mise en service.

> [!NOTE]
> Actuellement, la création de Teams App avec SharePoint Framework à l’aide de Teams Shared Computer Toolkit n’a pas d’intégration directe avec Azure, le contenu de ce document ne s’applique pas SPFx applications basées sur des applications.


<br>

</details>

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Déployer Teams application dans le cloud](deploy.md)

> [!div class="nextstepaction"]
> [Gérer plusieurs environnements](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [Collaborer avec d’autres développeurs sur Teams projet](TeamsFx-collaboration.md)
