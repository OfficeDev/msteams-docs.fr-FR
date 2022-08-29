---
title: Utiliser le Kit de ressources Teams pour provisionner des ressources cloud à l’aide du Kit de ressources Teams pour Visual Studio
author: surbhigupta
description: Dans ce module, découvrez comment provisionner des ressources cloud à l’aide du Kit de ressources Teams. Également pour créer des ressources et personnaliser l’approvisionnement des ressources dans Visual Studio
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 7dfc5817fb8872a782b28c113c270a318e3d5078
ms.sourcegitcommit: 52a11f7614c43172bc2d57401a60d569db5310a9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2022
ms.locfileid: "67291688"
---
# <a name="provision-cloud-resources-using-visual-studio"></a>Provisionner des ressources cloud à l’aide de Visual Studio

TeamsFx s’intègre à Azure et au cloud Microsoft 365 qui vous permet de placer votre application dans Azure avec une seule commande. TeamsFx s’intègre à Azure Resource Manager qui vous permet de provisionner des ressources Azure. Pour l’approche du code, votre application a besoin des ressources cloud.

## <a name="prerequisites"></a>Conditions préalables

Voici la liste des outils dont vous avez besoin pour provisionner vos ressources cloud :

| &nbsp; | Installer | Pour l’utilisation... |
| --- | --- | --- |
| &nbsp; | **Obligatoire** | &nbsp; |
| &nbsp; | Visual Studio 2022 version 17.3 | Vous pouvez installer l’édition Entreprise de Visual Studio et installer la charge de travail « ASP.NET » et les outils de développement Microsoft Teams. |
| &nbsp; | [Compte de développeur Microsoft 365](https://developer.microsoft.com/en-us/microsoft-365/dev-program) | Accès au compte Teams avec les autorisations appropriées pour installer une application. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams pour collaborer avec toutes les personnes avec lesquelles vous travaillez via les applications pour les conversations, les réunions, les appels, le tout au même endroit. |
| &nbsp; | Toolkit Teams | Extension Visual Studio qui crée une structure de projet pour votre application. Utilisez la dernière version. |
| &nbsp; | [Compte Azure](https://portal.azure.com/) | Compte Azure avec un abonnement valide. |

## <a name="steps-to-provision-cloud-resources"></a>Étapes de provisionnement des ressources cloud

Les étapes suivantes vous aident à provisionner des ressources cloud à l’aide de Visual Studio :

### <a name="sign-in-to-your-microsoft-365-account"></a>Connectez-vous à votre compte Microsoft 365

1. Visual Studio 2022.
2. Ouvrez le projet d’application Microsoft Teams.
3. Sélectionnez **Projet**.
4. Sélectionnez **Teams Toolkit**.
5. Sélectionnez **Préparer les dépendances d’application Teams**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare-app-dependencies.png" alt-text="Préparer les dépendances d’application Teams":::

7. Sélectionnez **Se connecter...** pour vous connecter à votre compte Azure.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare1.png" alt-text="Se connecter à Microsoft 365":::

    > [!NOTE]
    > Si vous êtes déjà connecté, votre nom d’utilisateur s’affiche ou vous pouvez sélectionner la même option pour changer de compte.

8. Votre navigateur web par défaut s’ouvre pour vous permettre de vous [connecter](https://developer.microsoft.com/en-us/microsoft-365/dev-program) au compte.
9. Sélectionnez **Continuer** une fois que vous êtes connecté à votre compte.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-signin-M365.png" alt-text="Confirmer en sélectionnant Continuer":::

### <a name="sign-in-to-your-azure-account"></a>Connectez-vous à votre compte Azure

1. Ouvrez Visual Studio 2022.
2. Ouvrez le projet d’application Teams.
3. Sélectionnez **Projet**.
4. Sélectionnez **Teams Toolkit**.
5. Sélectionnez **Provisionner dans le cloud**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud.png" alt-text="Se connecter à un compte Azure":::

6. Sélectionnez **Se connecter...** pour vous connecter à votre compte Azure.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-start.png" alt-text="Connectez-vous à votre compte Azure":::

   > [!NOTE]
   > Si vous êtes déjà connecté, votre nom d’utilisateur s’affiche ou vous avez la possibilité de changer de compte.

7. Connectez-vous à un compte Azure à l’aide de vos informations d’identification. Le navigateur se ferme automatiquement.

### <a name="to-provision-cloud-resources"></a>Pour provisionner des ressources cloud

1. Après avoir ouvert votre projet dans Visual Studio, sélectionnez **Projet**
2. Sélectionner **Teams Toolkit**
3. Sélectionnez **Provisionner dans le cloud**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud1.png" alt-text="Provisionner dans le cloud":::

4. Dans la boîte de dialogue **approvisionnement** , vous pouvez voir la liste de tous les abonnements dans votre compte Azure.
5. Vous pouvez sélectionner ou créer un **groupe de ressources**.
6. Sélectionnez **Provision**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-select-subscription.png" alt-text="Sélectionner un groupe de ressources":::

7. La boîte de dialogue vous avertit que des frais peuvent être ajoutés en fonction de l’utilisation d’Azure. Sélectionnez **Provision**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-warning.png" alt-text="Avertissement de provisionnement":::

   Le processus d’approvisionnement de la création des ressources dans le cloud Azure peut prendre un certain temps.

8. Consultez la fenêtre de sortie du Kit de ressources Teams pour surveiller la progression.
9. Vous êtes invité une fois l’approvisionnement terminé. Sélectionnez **Afficher les ressources approvisionnées** pour afficher toutes les ressources qui ont été provisionnées.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-provision-success.png" alt-text="Afficher les ressources approvisionnées":::

### <a name="create-resources"></a>Créer des ressources

Lorsque vous déclenchez la commande de provisionnement dans Teams Toolkit ou TeamsFx CLI, vous pouvez créer les ressources suivantes :

* Microsoft Azure Active Directory application (Azure AD) sous votre locataire Microsoft 365.
* Inscription d’application Teams sous la plateforme Teams de votre locataire Microsoft 365.
* Ressources Azure sous votre abonnement Azure sélectionné.

Lorsque vous créez un projet, vous devez également créer des ressources Azure. Les modèles Azure Resource Manager (ARM) définissent toutes les ressources Azure et vous aident à créer les ressources Azure nécessaires lors de l’approvisionnement.

### <a name="create-resource-for-teams-tab-application"></a>Créer une ressource pour l’application onglet Teams

| Ressource | Objectif | Description |
| --- | --- | --- |
| Plan App Service | Héberge votre application web de l’onglet. | Non applicable |
| App Service | Héberge votre application d’onglet Blazor et votre serveur d’authentification simple qui permet d’accéder à d’autres services. | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |

### <a name="create-resources-for-teams-message-extension-application"></a>Créer des ressources pour l’application d’extension de message Teams

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot avec l’infrastructure de bot. | Connecte le bot à Teams. |
| App Service plan | Héberge votre application de bot web. | Non applicable |
| App Service | Héberge votre application bot. | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |

### <a name="create-resources-for-teams-command-bot-application"></a>Créer des ressources pour l’application de bot de commande Teams

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot avec l’infrastructure de bot. | Connecte le bot à Teams. |
| Plan App Service | Héberge votre application de bot web. | Non applicable |
| App Service | Héberge votre application bot. | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |

### <a name="create-resources-for-teams-notification-bot-with-http-trigger-web-api-server-application"></a>Créer des ressources pour le bot de notification Teams avec l’application de déclencheur HTTP (serveur d’API web)

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot avec l’infrastructure de bot. | Connecte le bot à Teams. |
| Plan App Service | Héberge votre application de bot web. | Non applicable |
| App Service | Hébergez votre application bot. | Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure. |
| Identité managée | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |

### <a name="create-resource-for-teams-notification-bot-with-http-trigger-azure-function-application"></a>Créer une ressource pour le bot de notification Teams avec l’application de déclencheur HTTP (fonction Azure)

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot avec l’infrastructure de bot. | Connecte le bot à Teams. |
| Gérer l’identité | Authentifie les demandes de service à service Azure. | Partagé entre différentes fonctionnalités et ressources. |
| Compte de stockage | Aide à créer une application de fonction. | Non applicable |
| Plan App Service | Héberge l’application de bot de fonction. | Non applicable |
| Application de la fonction | Héberge votre application bot. | - Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure.<br>-Ajoute une règle de partage de ressources cross-origin (CORS) pour autoriser les demandes provenant de votre application onglet.<br>- Ajoute un paramètre d’authentification qui autorise uniquement les demandes de votre application Teams.<br>- Ajoute les paramètres d’application requis par le Kit de développement logiciel (SDK) TeamsFx. |

### <a name="create-resource-for-teams-notification-bot-with-timer-trigger-azure-function-application"></a>Créer une ressource pour le bot de notification Teams avec une application de déclencheur de minuteur (fonction Azure)

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot avec l’infrastructure de bot. | Connecte le bot à Teams. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |
| Compte de stockage | Aide à créer une application de fonction. | Non applicable |
| Plan App Service | Héberge l’application de bot de fonction. | Non applicable |
| Application de la fonction | Héberge votre application bot. | - Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure.<br>-Ajoute une règle de partage de ressources cross-origin (CORS) pour autoriser les demandes provenant de votre application onglet.<br>- Ajoute un paramètre d’authentification qui autorise uniquement les demandes de votre application Teams.<br>- Ajoute les paramètres d’application requis par le Kit de développement logiciel (SDK) TeamsFx. |

### <a name="create-resources-for-teams-notification-bot-with-http-trigger--timer-trigger-azure-function-application"></a>Créer des ressources pour le bot de notification Teams avec l’application déclencheur HTTP + déclencheur de minuteur (fonction Azure)

| Ressource | Objectif | Description |
| --- | --- | --- |
| Bot Azure | Inscrit votre application en tant que bot avec l’infrastructure de bot. | Connecte le bot à Teams. |
| Gérer l’identité | Authentifier les demandes de service à service Azure. | Partage entre différentes fonctionnalités et ressources. |
| Compte de stockage | Aide à créer une application de fonction. | Non applicable |
| Plan App Service | Héberge l’application de bot de fonction. | Non applicable |
| Application de fonction | Héberge votre application bot. | - Ajoute l’identité affectée par l’utilisateur pour accéder à d’autres ressources Azure.<br>-Ajoute une règle de partage de ressources cross-origin (CORS) pour autoriser les demandes provenant de votre application onglet.<br>- Ajoute un paramètre d’authentification qui autorise uniquement les demandes de votre application Teams.<br>- Ajoute les paramètres d’application requis par le Kit de développement logiciel (SDK) TeamsFx. |

### <a name="manage-your-resources"></a>Gérer vos ressources

Vous pouvez vous connecter à [Portail Azure](https://portal.azure.com/) et gérer toutes les ressources créées par Teams Toolkit.

* Vous pouvez sélectionner un groupe de ressources dans la liste existante ou le nouveau groupe de ressources que vous avez créé.
* Vous pouvez voir les détails du groupe de ressources que vous avez sélectionné dans la section vue d’ensemble de la table des matières.

### <a name="customize-resource-provision"></a>Personnaliser l’approvisionnement des ressources

Teams Toolkit vous permet d’utiliser une infrastructure pour l’approche de code afin de définir les ressources Azure que vous souhaitez approvisionner. Vous pouvez modifier la configuration dans le Kit de ressources Teams en fonction de vos besoins.

Teams Toolkit utilise un modèle ARM pour définir des ressources Azure. Le modèle ARM est un ensemble de fichiers bicep qui définit l’infrastructure et la configuration de votre projet. Vous pouvez personnaliser les ressources Azure en modifiant le modèle ARM. Pour plus d’informations sur Intune, consultez ce [document biceps](/azure/azure-resource-manager/bicep).

L’approvisionnement avec ARM implique la modification des ensembles de fichiers, paramètres et modèles suivants :

* Fichiers de paramètre ARM (`azure.parameters.{your_env_name}.json`) situés dans un `.fx/configs` dossier, pour passer des paramètres aux modèles.
* Les fichiers de modèle ARM situés dans le `templates/azure` dossier contiennent les fichiers suivants :

| Fichier | Fonction | Autoriser la personnalisation des fichiers |
| --- | --- | --- |
| main.bicep | Indiquez un point d’entrée pour la ressource Azure. Disposition | Oui |
| provision.bicep | Créez et configurez des ressources Azure. | Oui |
| config.bicep | Ajoutez les configurations requises de TeamsFx aux ressources Azure. | Oui |
| provision/xxx.bicep | Créez et configurez chaque ressource Azure consommée par `provision.bicep`. | Oui |
| teamsfx/xxx.bicep | Ajoutez les configurations requises TeamsFx à chaque ressource Azure consommée par `config.bicep`.| Non |

> [!NOTE]
> Une fois que vous avez ajouté des ressources ou des fonctionnalités à votre projet, `teamsfx/xxx.bicep` elle est régénérée. Pour modifier les fichiers bicep, vous pouvez utiliser Git pour suivre vos modifications apportées aux `teamsfx/xxx.bicep` fichiers. Cela ne vous fait pas perdre de modifications lors de l’ajout de ressources ou de fonctionnalités à votre projet.

Les fichiers de modèle ARM utilisent des espaces réservés pour les paramètres. L’objectif des espaces réservés est de s’assurer que de nouvelles ressources peuvent être créées dans le nouvel environnement. Les valeurs réelles sont résolues à partir du `.fx/states/state.{env}.json` fichier.

### <a name="azure-ad-application-related-parameters"></a>Paramètres liés à l’application Azure AD

| Nom du paramètre | Détenteur de place de valeur par défaut | Signification du titulaire de place | Comment créer et personnaliser des applications ? |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | ID client d’application Azure AD de votre application créé lors de l’approvisionnement. | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | Clé secrète client d’application Azure AD de votre application créée lors de l’approvisionnement. | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | ID de locataire de l’application Azure AD de votre application. | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Hôte d’autorité OAuth de l’application Azure AD de votre application. | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | ID client de l’application Azure AD du bot créé lors de l’approvisionnement. | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secret client de l’application Azure AD du bot créé lors de l’approvisionnement. | [Personnaliser la valeur](#use-an-existing-azure-ad-app-for-your-bot) |

### <a name="reference-environment-variables-in-parameter-files"></a>Référencer des variables d’environnement dans des fichiers de paramètres

Lorsque la valeur est secrète, vous n’avez pas besoin de les coder en dur dans le fichier de paramètres. Les fichiers de paramètres prennent en charge le référencement des valeurs à partir de variables d’environnement. Vous pouvez utiliser cette syntaxe `{{$env.YOUR_ENV_VARIABLE_NAME}}` dans les valeurs de paramètres du Kit de ressources Teams pour résoudre à partir de la variable d’environnement actuelle.

L’exemple suivant lit la valeur du paramètre à `mySelfHostedDbConnectionString` partir de la variable `DB_CONNECTION_STRING`d’environnement :

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

### <a name="customize-arm-template-files"></a>Personnaliser les fichiers de modèle ARM

Si les modèles prédéfinis ne répondent pas aux besoins de votre application, vous pouvez personnaliser les modèles ARM sous `templates/azure` le dossier. Par exemple, vous pouvez personnaliser le modèle ARM pour créer des ressources Azure supplémentaires pour votre application. Vous devez avoir des connaissances de base du langage bicep, qui est utilisé pour créer un modèle ARM.

Pour vous assurer que l’outil TeamsFx fonctionne correctement, personnalisez le modèle ARM, qui répond aux exigences suivantes :

* Assurez-vous que la structure de dossiers et le nom de fichier restent inchangés. L’outil peut ajouter du nouveau contenu aux fichiers existants lorsque vous ajoutez d’autres ressources ou fonctionnalités à votre projet.
* Assurez-vous que le nom des paramètres générés automatiquement et ses noms de propriétés restent inchangés. Les paramètres générés automatiquement peuvent être utilisés lorsque vous ajoutez des ressources ou des fonctionnalités supplémentaires à votre projet.
* Assurez-vous que la sortie du modèle ARM généré automatiquement est également inchangée. Vous pouvez ajouter d’autres sorties au modèle ARM. La sortie est `.fx/states/state.{env}.json` et peut être utilisée dans d’autres fonctionnalités telles que le déploiement et la validation du fichier manifeste.

### <a name="customize-teams-app"></a>Personnaliser l’application Teams

Vous pouvez personnaliser votre bot ou l’application Teams en ajoutant des extraits de configuration pour utiliser une application Azure AD créée par vous. Vous pouvez effectuer les opérations suivantes :

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Utiliser une application Azure AD existante pour votre bot

Vous pouvez ajouter l’extrait `.fx/configs/config.{env}.json` de configuration suivant pour utiliser une application Azure AD créée par vous pour votre application Teams. Pour créer une application Azure AD, suivez le lien <https://aka.ms/teamsfx-existing-aad-doc>.

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
> Veillez à ne pas partager la même application Azure AD dans plusieurs environnements. Si vous n’êtes pas autorisé à mettre à jour l’application Azure AD, vous recevez un avertissement avec des instructions pour mettre à jour manuellement l’application Azure AD. Suivez ces instructions pour mettre à jour votre application Azure AD après l’approvisionnement.

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Utiliser une application Azure AD existante pour votre application Teams

Vous pouvez ajouter l’extrait de configuration suivant pour `.fx/configs/config.{env}.json` utiliser l’application Azure AD créée pour votre bot :

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Après avoir ajouté l’extrait de code, ajoutez votre clé secrète client à la variable d’environnement associée pour Teams Toolkit afin de résoudre la clé secrète client réelle lors de l’approvisionnement.

#### <a name="skip-adding-user-for-sql-database"></a>Ignorer l’ajout d’un utilisateur pour SQL base de données

Si vous obtenez une erreur d’autorisation insuffisante lorsque Teams Toolkit tente d’ajouter un utilisateur à la base de données SQL, vous pouvez ajouter l’extrait de configuration suivant pour `.fx/configs/config.{env}.json` ignorer l’ajout d’un utilisateur de base de données SQL :

```json
"skipAddingSqlUser": true
```

## <a name="see-also"></a>Voir aussi

* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
* [Modifier le manifeste de l’application Teams à l’aide de Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Déboguer l’application Teams localement pour Visual Studio](debug-teams-app-visual-studio.md)
