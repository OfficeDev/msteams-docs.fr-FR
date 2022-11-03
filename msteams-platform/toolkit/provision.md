---
title: Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud
author: MuyangAmigo
description: Dans ce module, découvrez comment provisionner des ressources cloud à l’aide du Kit de ressources Teams, créer des ressources et personnaliser l’approvisionnement des ressources
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 6c3e44de4d63911dff5481ab859019aea37559d1
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833197"
---
# <a name="provision-cloud-resources"></a>Provisionner des ressources cloud

TeamsFx s’intègre à Azure et Microsoft 365 cloud, ce qui vous permet de placer votre application dans Azure avec une seule commande. TeamsFx s’intègre à Azure Resource Manager qui vous permet de provisionner des ressources Azure, dont votre application a besoin pour l’approche du code.

::: zone pivot="visual-studio-code"

## <a name="provision-using-teams-toolkit-in-visual-studio-code"></a>Provisionner à l’aide du Kit de ressources Teams dans Visual Studio Code

L’approvisionnement est effectué avec une seule commande dans le Kit de ressources Teams pour Visual Studio Code ou l’interface CLI TeamsFx. Pour plus d’informations, consultez [Provisionner une application basée sur Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8).

## <a name="create-resources"></a>Créer des ressources

Lorsque vous déclenchez la commande de provisionnement dans Teams Shared Computer Toolkit ou TeamsFx CLI, vous pouvez obtenir les ressources suivantes :

* application Microsoft Azure Active Directory (Azure AD) sous votre locataire Microsoft 365.
* Inscription de l’application Teams sous la plateforme Teams de votre client Microsoft 365.
* Ressources Azure sous votre abonnement Azure sélectionné.

Lorsque vous créez un projet, vous pouvez utiliser toutes les ressources Azure. Le modèle ARM définit toutes les ressources Azure et permet de créer les ressources Azure nécessaires lors de l’approvisionnement. Lorsque vous [ajoutez une nouvelle ressource de fonctionnalité](./add-resource.md) à un projet existant, le modèle ARM mis à jour reflète la dernière modification.

> [!NOTE]
> Les services Azure entraînent des coûts dans votre abonnement. Pour plus d’informations sur l’estimation des coûts, consultez [la calculatrice de prix](https://azure.microsoft.com/pricing/calculator/).

La liste suivante montre la création de ressources pour différents types d’application et de ressources Azure :
<br>

<details>
<summary><b>Création de ressources pour l’onglet de l’application Teams</b></summary>

|Ressource|Objectif|Description |
|----------|--------------------------------|-----|
| Stockage Azure | Héberger votre application onglet | Active la fonction d'application web statique pour héberger votre application d'onglet. |
| Plan App Service pour l’authentification simple | Héberger l’application web de l’authentification simple |Non applicable |
| Application web pour l’authentification simple | Héberger un serveur d’authentification simple pour accéder à d’autres services dans votre application monopage | Ajoute une identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

</details>
<br>

<details>
<summary><b>Création de ressources pour Teams application d’extension de bot ou de message</b></summary>

|Ressource|Objectif| Description |
|----------|--------------------------------|-----|
| Service de bot Azure | Inscrit votre application en tant que bot avec l’infrastructure de bot. | Connecte le bot à Teams. |
| Plan App Service pour le bot | Héberger l’application web du bot |Non applicable |
| Application web pour bot | Héberger votre application bot | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. <br /> Ajoute les paramètres d’application requis par le [Kit de développement logiciel (SDK) TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

</details>
<br>

<details>
<summary><b>Création de ressources pour Azure Functions dans le projet</b></summary>

|Ressource|Objectif| Description|
|----------|--------------------------------|-----|
| Plan App Service pour l’application de fonction | Héberger l’application de fonction |Non applicable |
| Application de la fonction | Héberger vos API Azure Functions | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. <br /> Ajoute une règle de partage des ressources d'origine croisée (CORS) pour autoriser les requêtes provenant de votre application d'onglet. <br /> Ajoute un paramètre d’authentification qui autorise uniquement les demandes de votre application Teams. <br /> Ajoute les paramètres d’application requis par le [Kit de développement logiciel (SDK) TeamsFx](https://www.npmjs.com/package/@microsoft/teamsfx). |
| Stockage Azure pour l’application de fonction | Requis pour créer une application de fonction |Non applicable|
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

</details>
<br>

<details>
<summary><b>Création de ressources pour Azure SQL dans le projet</b></summary>

|Ressource|Objectif | Description |
|----------|--------------------------------|-----|
| Azure SQL et SQL Server | Héberger l’instance de base de données Azure SQL | Permet à tous les services Azure d’accéder au serveur. |
| Base de données Azure SQL | Stocker des données pour votre application | Octroie à l’utilisateur l’autorisation d’identité, de lecture ou d’écriture attribuée à la base de données. |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure | Partagé entre différentes fonctionnalités et ressources |

</details>
<br>

<details>
<summary><b>Création de ressources pour Azure Gestion des API dans le projet</b></summary>

|Ressource|Objectif|
|----------|--------------------------------|
| Application Azure AD pour le service de gestion des API | Autorise les API d’accès Microsoft Power Platform gérées par le service de gestion des API. |
| Service de gestion des API | Gérer vos API hébergées dans l’application de fonction |
| Produit de gestion des API | Regrouper vos API, définir les conditions d’utilisation et les stratégies d’exécution |
| Serveur OAuth de gestion des API | Permet à Microsoft Power Platform d’accéder à vos API hébergées dans l’application de fonction. |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure |

</details>
<br>

<details>
<summary><b>Ressources créées lors de l’inclusion d’Azure Key Vault dans le projet</b></summary>

|Ressources|Objectif de cette ressource|
|----------|--------------------------------|
| Azure Key Vault | Gérer les secrets (par exemple, Azure AD secret client d’application) utilisés par d’autres services Azure |
| Identité affectée par l’utilisateur | Authentifier les demandes de service à service Azure |

</details>
<br>

## <a name="customize-resource-provision"></a>Personnaliser l’approvisionnement des ressources

Teams Toolkit vous permet d’utiliser une approche de l’infrastructure en tant que code pour définir les ressources Azure que vous souhaitez approvisionner et la façon dont vous souhaitez configurer. L’outil utilise un modèle ARM pour définir des ressources Azure. Le modèle ARM est un ensemble de fichiers bicep qui définit l’infrastructure et la configuration de votre projet. Vous pouvez personnaliser les ressources Azure en modifiant le modèle ARM. Pour plus d’informations sur Intune, consultez ce [document biceps](/azure/azure-resource-manager/bicep).

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

### <a name="azure-ad-parameters"></a>Paramètres Azure AD

Les fichiers de modèle ARM utilisent des espaces réservés pour les paramètres. L’objectif de ces espaces réservés est de garantir la création de nouvelles ressources pour vous dans un nouvel environnement. Les valeurs réelles sont résolues à partir de `.fx/states/state.{env}.json`.

Il existe deux types de paramètres tels que les paramètres liés à l’application Azure AD et les paramètres liés aux ressources Azure.

##### <a name="azure-ad-application-related-parameters"></a>Paramètres Azure AD liés à l’application

| Nom du paramètre | Détenteur de place de valeur par défaut | Signification du titulaire de place | Comment créer et personnaliser des applications ? |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | ID client d’application Azure AD de votre application créé lors de l’approvisionnement | [Utiliser une application Azure AD existante pour votre bot](#use-an-existing-azure-ad-app-for-your-bot) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | Clé secrète client Azure AD de votre application créée lors de l’approvisionnement | [Utiliser une application Azure AD existante pour votre application Teams](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | ID de locataire de l’application Azure AD de votre application | [Utiliser une application Azure AD existante pour votre application Teams](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Hôte d’autorité OAuth de l’application Azure AD de votre application | [Utiliser une application Azure AD existante pour votre application Teams](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | ID client de l’application Azure AD bot créé lors de l’approvisionnement | [Utiliser une application Azure AD existante pour votre bot](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secret client de l’application Azure AD du bot créé lors de l’approvisionnement | [Utiliser une application Azure AD existante pour votre bot](#use-an-existing-azure-ad-app-for-your-bot) |

##### <a name="azure-resource-related-parameters"></a>Paramètres liés aux ressources Azure

| Nom du paramètre | Détenteur de place de valeur par défaut | Signification du titulaire de place | Comment créer et personnaliser des applications ? |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Compte d'administrateur Azure SQL Server que vous avez fourni lors de l'approvisionnement | Supprimer l’espace réservé et remplir la valeur réelle |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Le mot de passe de l'administrateur du serveur SQL Azure que vous avez fourni lors de la mise à disposition. | Supprimer l’espace réservé et remplir la valeur réelle |

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

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Utiliser une application Azure AD existante pour votre application Teams

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

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Utiliser une application Azure AD existante pour votre bot

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
2. Ajoutez une nouvelle propriété, par exemple, `functionAppName` sous la `provisionParameters` section .
3. Entrez la valeur , `functionAppName`par exemple `contosoteamsappapi`.
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

Pour ajouter d’autres ressources ou stockage Azure à l’application :

Prenons l’exemple du scénario suivant :

Vous souhaitez ajouter le stockage Azure à votre back-end de fonction Azure pour stocker des données d’objet blob. Il n’existe aucun flux automatique pour mettre à jour le modèle bicep avec la prise en charge du stockage Azure. Toutefois, vous pouvez modifier le fichier bicep et ajouter la ressource. Les étapes sont les suivantes :

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

::: zone-end

::: zone pivot="visual-studio"

## <a name="provision-using-teams-toolkit-in-visual-studio"></a>Provisionner à l’aide de Teams Toolkit dans Visual Studio

Les étapes suivantes vous aident à provisionner des ressources cloud à l’aide de Visual Studio :

### <a name="sign-in-to-your-microsoft-365-account"></a>Connectez-vous à votre compte Microsoft 365

1. Ouvrez Visual Studio 2022.
1. Ouvrez le projet d’application Microsoft Teams.
1. Sélectionnez **Project** > **Teams Toolkit** > **Préparer les dépendances d’application Teams**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare-app-dependencies1.png" alt-text="Préparer les dépendances des applications Teams":::

1. Sélectionnez **Se connecter** pour vous connecter à votre compte Azure.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare1.png" alt-text="Se connecter à Microsoft 365":::

    > [!NOTE]
    > Si vous êtes déjà connecté, votre nom d’utilisateur s’affiche ou vous pouvez le sélectionner pour changer de compte.

1. Votre navigateur web par défaut s’ouvre pour vous permettre de vous [connecter](https://developer.microsoft.com/en-us/microsoft-365/dev-program) au compte.

1. Sélectionnez **Continuer** une fois que vous êtes connecté à votre compte.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-signin-M365.png" alt-text="Confirmer en sélectionnant Continuer":::

### <a name="sign-in-to-your-azure-account"></a>Connectez-vous à votre compte Azure

1. Ouvrez Visual Studio 2022.
1. Ouvrez le projet d’application Teams.
1. Sélectionnez **Provisionner le****kit de ressources** >  Project  >  Teams **dans le cloud**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud2.png" alt-text="Se connecter au compte Azure":::

1. Sélectionnez **Se connecter...** pour vous connecter à votre compte Azure.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-start.png" alt-text="Connectez-vous à votre compte Azure":::

   > [!NOTE]
   > Si vous êtes déjà connecté, votre nom d’utilisateur s’affiche ou vous avez la possibilité de changer de compte.

   Une fois connecté à votre compte Azure à l’aide de vos informations d’identification, le navigateur se ferme automatiquement.

### <a name="to-provision-cloud-resources"></a>Pour provisionner des ressources cloud

Après avoir ouvert votre projet dans Visual Studio :

1. Sélectionnez **Provisionner le****kit de ressources** >  Project  >  Teams **dans le cloud**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud2.png" alt-text="Provisionner dans le cloud":::

   La fenêtre **Provisionner** s’affiche.

1. Entrez les détails suivants pour provisionner vos ressources.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-select-subscription1.png" alt-text="Sélectionner un groupe de ressources":::

   1. Sélectionnez votre **nom d’abonnement** dans la liste déroulante.
   1. Sélectionnez votre **groupe de ressources** dans la liste déroulante.
   1. Sélectionnez votre **Région** dans la liste déroulante.

      > [!NOTE]
      > Vous pouvez créer un groupe de ressources en sélectionnant **Nouveau**.

   1. Sélectionnez **Provisionner**.

1. La boîte de dialogue s’affiche, indiquant que des frais peuvent être ajoutés en fonction de l’utilisation d’Azure. Sélectionnez **Provisionner**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-warning.png" alt-text="Avertissement de provisionnement":::

   Le processus d’approvisionnement crée des ressources dans le cloud Azure. Vous pouvez surveiller la progression en observant la fenêtre de sortie du Kit de ressources Teams.

1. Vous êtes invité une fois l’approvisionnement terminé. Sélectionnez **Afficher les ressources approvisionnées** pour afficher toutes les ressources qui ont été approvisionnées.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-provision-success.png" alt-text="Afficher les ressources approvisionnées":::

## <a name="create-resources"></a>Créer des ressources

Lorsque vous déclenchez une commande d’approvisionnement dans Teams Toolkit ou l’interface CLI TeamsFx, vous pouvez créer les ressources suivantes :

* application Microsoft Azure Active Directory (Azure AD) sous votre locataire Microsoft 365.
* Inscription de l’application Teams sous la plateforme Teams de votre client Microsoft 365.
* Ressources Azure sous votre abonnement Azure sélectionné.

Lorsque vous créez un projet, vous devez également créer des ressources Azure. Les modèles Azure Resource Manager (ARM) définissent toutes les ressources Azure et vous aident à créer les ressources Azure nécessaires lors de l’approvisionnement.

La liste suivante montre la création de ressources pour différents types d’application et de ressources Azure :
<br>

<details>
<summary><b>Création de ressources pour l’onglet de l’application Teams</b></summary>

| Ressource | Objectif | Description |
| --- | --- | --- |
| Plan App Service | Héberge votre application web de l’onglet . | Non applicable |
| Service d’application | Héberge votre application d’onglet Blazor et votre serveur d’authentification simple qui vous permet d’accéder à d’autres services. | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |

</details>
<br>

<details>
<summary><b>Création de ressources pour l’application d’extension de message Teams</b></summary>

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot auprès de l’infrastructure de bot. | Connecte le bot à Teams. |
| plan App Service | Héberge votre application de bot web. | Non applicable |
| App Service | Héberge votre application de bot. | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |

</details>
<br>

<details>
<summary><b>Création de ressources pour l’application de bot de commande Teams</b></summary>

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot auprès de l’infrastructure de bot. | Connecte le bot à Teams. |
| Plan App Service | Héberge votre application de bot web. | Non applicable |
| Service d’application | Héberge votre application de bot. | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |

</details>
<br>

<details>
<summary><b>Création de ressources pour le bot de notification Teams avec l’application déclencheur HTTP (serveur d’API web)</b></summary>

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot auprès de l’infrastructure de bot. | Connecte le bot à Teams. |
| Plan App Service | Héberge votre application de bot web. | Non applicable |
| Service d’application | Hébergez votre application de bot. | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Identité managée | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |

</details>
<br>

<details>
<summary><b>Création de ressources pour le bot de notification Teams avec l’application déclencheur HTTP (fonction Azure)</b></summary>

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot auprès de l’infrastructure de bot. | Connecte le bot à Teams. |
| Gérer l’identité | Authentifie les demandes de service à service Azure. | Partagé entre différentes fonctionnalités et ressources. |
| Compte de stockage | Permet de créer une application de fonction. | Non applicable |
| Plan App Service | Héberge l’application de bot de fonction. | Non applicable |
| Application de la fonction | Héberge votre application de bot. | -Ajoute une identité affectée par l’utilisateur pour accéder à d’autres ressources Azure.<br>-Ajoute la règle CORS (Cross-Origin Resource Sharing) pour autoriser les demandes de votre application d’onglet.<br>-Ajoute un paramètre d’authentification qui autorise uniquement les demandes de votre application Teams.<br>-Ajoute les paramètres d’application requis par le Kit de développement logiciel (SDK) TeamsFx. |

</details>
<br>

<details>
<summary><b>Création de ressources pour le bot de notification Teams avec l’application de déclencheur de minuteur (fonction Azure)</b></summary>

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot auprès de l’infrastructure de bot. | Connecte le bot à Teams. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |
| Compte de stockage | Permet de créer une application de fonction. | Non applicable |
| Plan App Service | Héberge l’application de bot de fonction. | Non applicable |
| Application de la fonction | Héberge votre application de bot. | -Ajoute une identité affectée par l’utilisateur pour accéder à d’autres ressources Azure.<br>-Ajoute la règle CORS (Cross-Origin Resource Sharing) pour autoriser les demandes de votre application d’onglet.<br>-Ajoute un paramètre d’authentification qui autorise uniquement les demandes de votre application Teams.<br>-Ajoute les paramètres d’application requis par le Kit de développement logiciel (SDK) TeamsFx. |

</details>
<br>

<details>
<summary><b>Création de ressources pour le bot de notification Teams avec l’application déclencheur HTTP + déclencheur de minuteur (fonction Azure)</b></summary>

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot auprès de l’infrastructure de bot. | Connecte le bot à Teams. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |
| Compte de stockage | Permet de créer une application de fonction. | Non applicable |
| Plan App Service | Héberge l’application de bot de fonction. | Non applicable |
| Application de fonction | Héberge votre application de bot. | -Ajoute une identité affectée par l’utilisateur pour accéder à d’autres ressources Azure.<br>-Ajoute la règle CORS (Cross-Origin Resource Sharing) pour autoriser les demandes de votre application d’onglet.<br>-Ajoute un paramètre d’authentification qui autorise uniquement les demandes de votre application Teams.<br>-Ajoute les paramètres d’application requis par le Kit de développement logiciel (SDK) TeamsFx. |

</details>
<br>

### <a name="manage-your-resources"></a>Gérer vos ressources

Vous pouvez vous connecter à [Portail Azure](https://portal.azure.com/) et gérer toutes les ressources créées par teams Toolkit.

* Vous pouvez sélectionner un groupe de ressources dans la liste existante ou le nouveau groupe de ressources que vous avez créé.
* Vous pouvez voir les détails du groupe de ressources que vous avez sélectionné dans la section Vue d’ensemble de la table des matières.

## <a name="customize-resource-provision"></a>Personnaliser l’approvisionnement des ressources

Teams Toolkit vous permet d’utiliser une infrastructure pour l’approche du code afin de définir les ressources Azure que vous souhaitez approvisionner. Vous pouvez modifier la configuration dans teams Toolkit en fonction de vos besoins.

Teams Toolkit utilise un modèle ARM pour définir des ressources Azure. Le modèle ARM est un ensemble de fichiers bicep qui définit l’infrastructure et la configuration de votre projet. Vous pouvez personnaliser les ressources Azure en modifiant le modèle ARM. Pour plus d’informations sur Intune, consultez ce [document biceps](/azure/azure-resource-manager/bicep).

L’approvisionnement avec ARM implique la modification des ensembles de fichiers, paramètres et modèles suivants :

* Fichiers de paramètres ARM (`azure.parameters.{your_env_name}.json`) situés dans le `.fx/configs` dossier, pour passer des paramètres aux modèles.
* Les fichiers de modèle ARM situés dans le `templates/azure` dossier contiennent les fichiers suivants :

| Fichier | Fonction | Autoriser la personnalisation des fichiers |
| --- | --- | --- |
| main.bicep | Fournissez le point d’entrée pour la ressource Azure. Disposition | Oui |
| provision.bicep | Créez et configurez des ressources Azure. | Oui |
| config.bicep | Ajoutez les configurations requises TeamsFx aux ressources Azure. | Oui |
| provision/xxx.bicep | Créez et configurez chaque ressource Azure consommée par `provision.bicep`. | Oui |
| teamsfx/xxx.bicep | Ajoutez les configurations requises TeamsFx à chaque ressource Azure consommée par `config.bicep`.| Non |

> [!NOTE]
> Une fois que vous avez ajouté des ressources ou des fonctionnalités à votre projet, `teamsfx/xxx.bicep` est régénéré. Pour modifier les fichiers bicep, vous pouvez utiliser Git pour suivre vos modifications apportées aux `teamsfx/xxx.bicep` fichiers. Cela ne vous fait perdre aucune modification lors de l’ajout de ressources ou de fonctionnalités à votre projet.

Les fichiers de modèle ARM utilisent des espaces réservés pour les paramètres. L’objectif des espaces réservés est de s’assurer que de nouvelles ressources peuvent être créées dans le nouvel environnement. Les valeurs réelles sont résolues à partir du `.fx/states/state.{env}.json` fichier.

### <a name="azure-ad-application-related-parameters"></a>Paramètres liés à l’application Azure AD

| Nom du paramètre | Détenteur de place de valeur par défaut | Signification du titulaire de place | Comment créer et personnaliser des applications ? |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | ID client d’application Azure AD de votre application créé lors de l’approvisionnement. | [Utiliser une application Azure AD existante pour votre application Teams](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | Clé secrète client de l’application Azure AD de votre application créée lors de l’approvisionnement. | [Utiliser une application Azure AD existante pour votre application Teams](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | ID de locataire de l’application Azure AD de votre application. | [Utiliser une application Azure AD existante pour votre application Teams](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Hôte d’autorité OAuth de l’application Azure AD de votre application. | [Utiliser une application Azure AD existante pour votre application Teams](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | ID client d’application Azure AD du bot créé lors de l’approvisionnement. | [Utiliser une application Azure AD existante pour votre bot](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Clé secrète client de l’application Azure AD du bot créée lors de l’approvisionnement. | [Utiliser une application Azure AD existante pour votre bot](#use-an-existing-azure-ad-app-for-your-bot) |

### <a name="reference-environment-variables-in-parameter-files"></a>Référencer des variables d’environnement dans des fichiers de paramètres

Lorsque la valeur est secrète, vous n’avez pas besoin de les coder en dur dans le fichier de paramètres. Les fichiers de paramètres prennent en charge le référencement des valeurs à partir de variables d’environnement. Vous pouvez utiliser cette syntaxe `{{$env.YOUR_ENV_VARIABLE_NAME}}` dans les valeurs de paramètre du Kit de ressources Teams à résoudre à partir de la variable d’environnement actuelle.

L’exemple suivant lit la valeur du paramètre à `mySelfHostedDbConnectionString` partir de la variable `DB_CONNECTION_STRING`d’environnement :

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

### <a name="customize-arm-template-files"></a>Personnaliser les fichiers de modèle ARM

Si les modèles prédéfinis ne répondent pas aux besoins de votre application, vous pouvez personnaliser les modèles ARM sous `templates/azure` le dossier . Par exemple, vous pouvez personnaliser le modèle ARM afin de créer des ressources Azure supplémentaires pour votre application. Vous devez avoir des connaissances de base du langage bicep, qui est utilisé pour créer un modèle ARM.

Pour vous assurer que l’outil TeamsFx fonctionne correctement, personnalisez le modèle ARM, qui répond aux exigences suivantes :

* Assurez-vous que la structure de dossiers et le nom de fichier restent inchangés. L’outil peut ajouter du nouveau contenu aux fichiers existants lorsque vous ajoutez des ressources ou des fonctionnalités supplémentaires à votre projet.
* Assurez-vous que le nom des paramètres générés automatiquement et ses noms de propriétés restent en surplomb. Les paramètres générés automatiquement peuvent être utilisés lorsque vous ajoutez des ressources ou des fonctionnalités supplémentaires à votre projet.
* Vérifiez que la sortie du modèle ARM généré automatiquement est également inchangée. Vous pouvez ajouter d’autres sorties au modèle ARM. La sortie est `.fx/states/state.{env}.json` et peut être utilisée dans d’autres fonctionnalités telles que déployer et valider un fichier manifeste.

### <a name="customize-teams-app"></a>Personnaliser l’application Teams

Vous pouvez personnaliser votre bot ou l’application Teams en ajoutant des extraits de configuration pour utiliser une application Azure AD que vous avez créée. Vous pouvez effectuer les opérations suivantes :

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Utiliser une application Azure AD existante pour votre application Teams

Vous pouvez ajouter l’extrait de configuration `.fx/configs/config.{env}.json` suivant pour utiliser une application Azure AD que vous avez créée pour votre application Teams. Pour créer une application Azure AD, suivez le lien <https://aka.ms/teamsfx-existing-aad-doc>.

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Après avoir ajouté l’extrait de code, ajoutez votre clé secrète client à la variable d’environnement associée afin que teams Toolkit puisse résoudre la clé secrète client réelle lors de l’approvisionnement.

> [!NOTE]
> Veillez à ne pas partager la même application Azure AD dans plusieurs environnements. Si vous n’êtes pas autorisé à mettre à jour l’application Azure AD, vous recevez un avertissement contenant des instructions pour mettre à jour manuellement l’application Azure AD. Suivez ces instructions pour mettre à jour votre application Azure AD après l’approvisionnement.

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Utiliser une application Azure AD existante pour votre bot

Vous pouvez ajouter l’extrait de code de configuration suivant à afin d’utiliser `.fx/configs/config.{env}.json` l’application Azure AD créée pour votre bot :

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Après avoir ajouté l’extrait de code, ajoutez votre clé secrète client à la variable d’environnement associée pour teams Toolkit afin de résoudre la clé secrète client réelle lors de l’approvisionnement.

#### <a name="skip-adding-user-for-sql-database"></a>Ignorer l’ajout d’un utilisateur pour SQL base de données

Si vous obtenez une erreur d’autorisation insuffisante lorsque Teams Toolkit tente d’ajouter un utilisateur à la base de données SQL, vous pouvez ajouter l’extrait de code de configuration suivant à `.fx/configs/config.{env}.json` pour ignorer l’ajout d’un utilisateur de base de données SQL :

```json
"skipAddingSqlUser": true
```

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Déployer l’application Teams dans le cloud](deploy.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
* [Collaborer avec d’autres développeurs sur des projets Teams](TeamsFx-collaboration.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
* [Modifier le manifeste de l’application Teams à l’aide de Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Déboguer l’application Teams localement pour Visual Studio](debug-local.md#debug-your-teams-app-locally-using-visual-studio)
