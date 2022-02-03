---
title: Interface de ligne de commande TeamsFx
author: MuyangAmigo
description: Décrit l’interface de ligne de commande TeamsFx
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 45f5d58708b3ec7e452d864c6dfb6fcc79b4a48d
ms.sourcegitcommit: 58a24422bb04a529b6629a56803ed2efabc17cb1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2022
ms.locfileid: "62323182"
---
# <a name="teamsfx-library"></a>Bibliothèque TeamsFx

Microsoft Teams Framework (TeamsFx) est une bibliothèque encapsulant des fonctionnalités et des modèles d’intégration courants (comme l’accès simplifié à Microsoft Identity). Vous pouvez créer des applications pour Microsoft Teams avec une configuration nulle.

Voici la liste des principales fonctionnalités TeamsFx :

- **Collaboration TeamsFx : permet aux** développeurs et au propriétaire du projet d’inviter d’autres collaborateurs au projet TeamsFx. Vous pouvez collaborer pour déboguer et déployer un projet TeamsFx.

- **CLI TeamsFx** : il accélère Teams développement d’applications. Il permet également un scénario CI/CD dans lequel vous pouvez intégrer l’CLI dans des scripts pour l’automatisation.

- Kit de développement logiciel **(SDK) TeamsFx** : le Kit de développement logiciel (SDK) TeamsFx est la bibliothèque de code TeamsFx principale qui encapsule l’authentification simple pour le code côté client et côté serveur adapté aux développeurs Teams.


## <a name="teamsfx-command-line-interface"></a>Interface de ligne de commande TeamsFx

L’interface de ligne de commande TeamsFx est une interface de ligne de commande basée sur du texte qui accélère Teams développement d’applications. Il vise à fournir une expérience centrée sur le clavier tout en Teams applications. Il permet également un scénario CI/CD dans lequel vous pouvez intégrer l’CLI dans des scripts pour l’automatisation.

Pour plus d’informations, reportez-vous aux rubriques suivantes :
* [Code source](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli) 
* [Package (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>Prise en main

Installez `teamsfx-cli` à partir de `npm` et exécutez `teamsfx -h` pour vérifier toutes les commandes disponibles :

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>Commandes prises en charge

| Command | Description |
|----------------|-------------|
| `teamsfx new`| Créez une Teams application.|
| `teamsfx account`| Gérer les comptes de service cloud. Les services cloud pris en charge sont « Azure » et « Microsoft 365 ». |
| `teamsfx env` | Gérer les environnements. |
| `teamsfx capability`| Ajoutez de nouvelles fonctionnalités à l’application actuelle.|
| `teamsfx resource`  | Gérer les ressources dans l’application actuelle.|
| `teamsfx provision` | Mise en service des ressources cloud dans l’application actuelle.|
| `teamsfx deploy` | Déployez l’application actuelle.  |
| `teamsfx package` | Créez votre Teams dans un package pour la publication.|
| `teamsfx validate` | Validez l’application actuelle.|
| `teamsfx publish` | Publiez l’application sur Teams.|
| `teamsfx preview` | Afficher un aperçu de l’application actuelle. |
| `teamsfx config`  | Gérer les données de configuration. |
| `teamsfx permission`| Collaborez avec d’autres développeurs dans le même projet.|

## `teamsfx new`

Par défaut, passe `teamsfx new` en mode interactif et vous guide tout au long du processus de création d’Teams application. Vous pouvez également utiliser le mode non interactif en réglage de `--interactive` l’indicateur sur `false`.

| `teamsFx new` Commande | Description |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Créer une application à partir d’un modèle existant |
| `teamsfx new template list`     | Liste de tous les modèles disponibles |

### <a name="parameters-for-teamsfx-new"></a>Paramètres pour `teamsfx new`

| Paramètre | Conditions requises | Description |
|:---------------- |:-------------|:-------------|
|`--app-name` | Oui| Nom de votre application Teams application.|
|`--interactive`| Non | Sélectionnez les options de manière interactive. Les options sont et `true` la `false` valeur par défaut est `true`.|
|`--capabilities`| Non| Choisissez Teams fonctionnalités de l’application, les options multiples sont `tab`, `bot`et `tab-spfx``messaging-extension` . La valeur par défaut est `tab`.|
|`--programming-language`| Non| Langage de programmation pour le projet. Les options sont ou `javascript` et `typescript` la valeur par défaut est `javascript`.|
|`--folder`| Non | Project répertoire. Un sous-dossier avec le nom de votre application est créé sous ce répertoire. La valeur par défaut est `./`.|
|`--spfx-framework-type`| Non| Applicable si `Tab(SPfx)` la fonctionnalité est sélectionnée. Infrastructure frontale. Les options sont `none` et `react`, et la valeur par défaut est `none`.|
|`--spfx-web part-name`| Non | Applicable si `Tab(SPfx)` la fonctionnalité est sélectionnée. La valeur par défaut est « helloworld ».|
|`--spfx-web part-desp`| Non | Applicable si `Tab(SPfx)` la fonctionnalité est sélectionnée. La valeur par défaut est « helloworld description ». |
|`--azure-resources`| Non| Applicable si contient la `tab` fonctionnalité. Ajoutez des ressources Azure à votre projet. Les options multiples `sql` sont (Azure SQL Database) et `function` (Fonctions Azure). |

### <a name="scenarios-for-teamsfx-new"></a>Scénarios pour `teamsfx new`

Vous pouvez utiliser le mode interactif pour créer une Teams application. Les scénarios de contrôle de tous les paramètres avec `teamsfx new` sont les suivants :

#### <a name="tab-app-hosted-on-spfx-using-react"></a>Application d’onglet hébergée SPFx l’aide React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>Teams application en JavaScript avec onglet, fonctionnalités de bot et fonctions Azure

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Teams’onglet avec fonctions Azure et Azure SQL

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

Gérer les comptes de service cloud. Les services cloud pris en charge sont `Azure` et `Microsoft 365`.

| `teamsFx account` Commande | Description |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Connectez-vous au service cloud sélectionné. |
| `teamsfx account logout <service>`  | déconnectez-vous du service cloud sélectionné. |
| `teamsfx account set --subscription` | Mettez à jour les paramètres du compte pour définir un ID d’abonnement. |

## `teamsfx env`

Gérer les environnements.

| `teamsfx env` Commande  | Description |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Ajoutez un nouvel environnement en copiant à partir de l’environnement spécifié. |
| `teamsfx env list` | Liste de tous les environnements. |

### <a name="scenarios-for-teamsfx-env"></a>Scénarios pour `teamsfx env`

Les scénarios sont les `teamsfx env` suivants :

#### <a name="create-a-new-environment"></a>Créer un environnement

Ajoutez un nouvel environnement en copiant à partir de l’environnement dev existant :

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Ajoutez de nouvelles fonctionnalités à l’application actuelle.

| `teamsFx capability` Commande  | Description |
|:----------------  |:-------------|
| `teamsfx capability add tab` | Ajouter un onglet  |
| `teamsfx capability add bot` | Ajouter un bot |
| `teamsfx capability add messaging-extension`| Ajouter une extension de messagerie |

> [!NOTE]
> Si votre projet inclut un bot, l’extension de messagerie ne peut pas être ajoutée et elle s’applique vice versa. Vous pouvez inclure des extensions de bot et de messagerie dans votre projet lors de la création d’Teams projet d’application.

## `teamsfx resource`

Gérer les ressources dans l’application actuelle. Pris `<resource-type>` en charge : `azure-sql`et `azure-apim` `azure-function` .

| `teamsFx resource` Commande  | Description |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Ajoutez une ressource à l’application actuelle.|
| `teamsfx resource show <resource-type>`      | Afficher les détails de configuration de la ressource. |
| `teamsfx resource list`      | Liste de toutes les ressources dans l’application actuelle. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Paramètres pour `teamsfx resource add azure-function`

| Paramètre  | Conditions requises | Description |
|----------------  |-------------|-------------|
|`--function-name`| Oui | Fournissez un nom de fonction. La valeur par défaut est `getuserprofile`. |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Paramètres pour `teamsfx resource add azure-sql`

#### `--function-name`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--function-name`| Oui | Fournissez un nom de fonction. La valeur par défaut est `getuserprofile`. |

> [!NOTE]
> Le nom de la fonction est vérifié comme SQL et doit être accessible à partir de la charge de travail du serveur. Si votre projet ne contient pas `Azure Functions`, créez-en un pour vous.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Paramètres pour `teamsfx resource add azure-apim`

> [!TIP]
> Les options prennent effet lorsque vous essayez d’utiliser une `APIM` instance existante. Par défaut, vous n’avez pas besoin de spécifier d’options et il crée une nouvelle instance au cours de l’étape `teamsfx provision` .

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--subscription`| Oui | Sélectionner un abonnement Azure|
|`--apim-resource-group`| Oui| Nom du groupe de ressources. |
|`--apim-service-name`| Oui | Nom de l’instance du service de gestion des API. |
|`--function-name`| Oui | Fournissez un nom de fonction. La valeur par défaut est `getuserprofile`. |

> [!NOTE]
> `Azure API Management` doit fonctionner avec `Azure Functions`. Si votre projet ne contient pas `Azure Functions`, vous pouvez en créer un.

## `teamsfx provision`

Mise en service des ressources cloud dans l’application actuelle.

### <a name="parameters-for-teamsfx-provision"></a>Paramètres pour `teamsfx provision`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui| Sélectionnez un environnement pour le projet. |
|`--subscription`| Non | Spécifiez un ID d’abonnement Azure. |
|`--resource-group`| Non | Définissez le nom d’un groupe de ressources existant. |
|`--sql-admin-name`| Non | Applicable lorsqu’il existe SQL ressource dans le projet. Nom d’administrateur SQL.|
|`--sql-password`| Non| Applicable lorsqu’il existe SQL ressource dans le projet. Mot de passe d’administrateur SQL.|

## `teamsfx deploy`

Cette commande est utilisée pour déployer l’application actuelle. Par défaut, il déploie l’intégralité du projet, mais il est également possible de le déployer partiellement. Les options multiples `frontend-hosting`sont , `function`et `teamsbot``apim``spfx`.

### <a name="parameters-for-teamsfx-deploy"></a>Paramètres pour `teamsfx deploy`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui| Sélectionnez un environnement existant pour le projet. |
|`--open-api-document`| Non | Applicable lorsqu’il existe une ressource APIM dans le projet. Chemin d’accès au fichier de document api ouvert. |
|`--api-prefix`| Non | Applicable lorsqu’il existe une ressource APIM dans le projet. Préfixe de nom d’API. Le nom unique par défaut de l’API est `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| Non | Applicable lorsqu’il existe une ressource APIM dans le projet. Version de l’API. |

## `teamsfx validate`

Valider l’application actuelle. Cette commande valide le fichier manifeste de votre application.

### <a name="parameters-for-teamsfx-validate"></a>Paramètres pour `teamsfx validate`

`--env`: sélectionnez un environnement existant pour le projet.

## `teamsfx publish`

Publiez l’application sur Teams.

### <a name="parameters-for-teamsfx-publish"></a>Paramètres pour `teamsfx publish`

`--env`: sélectionnez un environnement existant pour le projet.

## `teamsfx package`

Créez votre Teams dans un package pour la publication.

## `teamsfx preview`

Afficher un aperçu de l’application actuelle à partir d’un emplacement local ou distant.

### <a name="parameters-for-teamsfx-preview"></a>Paramètres pour `teamsfx preview`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--local`| Non | Afficher un aperçu de l’application en local. `--local` est exclusif avec `--remote`. |
|`--remote`| Non | Afficher un aperçu de l’application à partir d’une application distante. `--remote` est exclusif avec `--local`. |
|`--env`| Non | Sélectionnez un environnement existant pour le projet lorsque le paramètre `--remote` est appended. |
|`--folder`| Non | Project répertoire racine. La valeur par défaut est `./`. |
|`--browser`| Non | Navigateur pour ouvrir Teams client web. Les options sont `chrome`, et `default` `edge` telles que le navigateur par défaut du système et la valeur est `default`. |
|`--browser-arg`| Non | Argument à transmettre au navigateur, nécessite --browser, peut être utilisé plusieurs fois, par exemple, --browser-args= »--guest » |
|`--sharepoint-site`| Non | SharePoint URL du site, `{your-tenant-name}.sharepoint.com` par exemple pour SPFx prévisualisation à distance du projet. |

### <a name="scenarios-for-teamsfx-preview"></a>Scénarios pour `teamsfx preview`

#### <a name="local-preview"></a>Aperçu local

Dépendances :

- Node.js
- Kit de développement logiciel .NET
- Outils azure Functions Core

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Aperçu à distance

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> Les journaux des services d’arrière-plan, tels que React sont enregistrés dans `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Gérez les données de configuration dans l’étendue utilisateur ou dans l’étendue du projet.

| `teamsfx config` Commande  | Description |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Afficher la valeur de configuration de l’option |
| `teamsfx config set <option> <value>` | Mettre à jour la valeur de configuration de l’option |

### <a name="parameters-for-teamsfx-config"></a>Paramètres pour `teamsfx config`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui | Sélectionnez un environnement existant pour le projet. |
|`--folder`| Non | Project répertoire. Il est utilisé pour obtenir ou définir la configuration du projet. La valeur par défaut est `./`. |
|`--global`| Non | Fin de la configuration. Si c’est le cas, l’étendue est limitée à l’étendue utilisateur au lieu de l’étendue du projet. La valeur par défaut est `false`. Actuellement, les configurations globales prise en charge incluent `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools`. `validate-node` |

### <a name="scenerios-for-teamsfx-config"></a>Scenerios pour `teamsfx config`

Les secrets du `.userdata` fichier sont chiffrés et `teamsfx config` peuvent vous aider à afficher ou à mettre à jour les valeurs.

#### <a name="stop-sending-telemetry-data"></a>Arrêter l’envoi de données de télémétrie

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Désactiver l’vérification de l’environnement

Il existe trois configurations pour activer ou désactiver Node.js, la validation du SDK .NET et des outils principaux des fonctions Azure, et toutes sont activées par défaut. Vous pouvez définir la configuration sur « off » si vous n’avez pas besoin de la validation des dépendances et que vous souhaitez installer les dépendances par vous-même. Consultez les guides suivants :
* [Node.js'installation](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [Guide d’installation du SDK .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk) 
* [Guide d’installation des outils azure Functions Core](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools).

Pour désactiver la validation du SDK .NET, vous pouvez utiliser la commande suivante :

```bash
teamsfx config set validate-dotnet-sdk off
```

Pour activer la validation du SDK .NET, vous pouvez utiliser la commande suivante :

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Afficher toute la configuration de l’étendue utilisateur

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Afficher toute la configuration dans le projet

La clé secrète est déchiffrée automatiquement :

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Mettre à jour la configuration secrète dans le projet

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

L’CLI TeamsFx fournit des `teamsFx permission` commandes pour un scénario de collaboration.

| `teamsFx permission` command | Description |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Accordez l’autorisation au compte Microsoft 365 du collaborateur pour le projet d’un environnement spécifié. |
| `teamsfx permission status` | Afficher l’état des autorisations pour le projet |

### <a name="parameters-for-teamsfx-permission-grant"></a>Paramètres pour `teamsfx permission grant`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui | Fournissez le nom de l’env. |
|`--email`| Oui | Fournissez l’adresse Microsoft 365 de messagerie du collaborateur. Assurez-vous que le compte du collaborateur se trouve dans le même client avec le créateur. |

### <a name="parameters-for-teamsfx-permission-status"></a>Paramètres pour `teamsfx permission status`

| Paramètre | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui | Fournissez le nom de l’env. |
|`--list-all-collaborators` | Non | Avec cet indicateur, Teams Shared Computer Toolkit CLI imprime tous les collaborateurs de ce projet. |

### <a name="scenarios-for-teamsfx-permission"></a>Scénarios pour `teamsfx permission`

Les autorisations pour les `TeamsFx` projets sont les suivantes :

#### <a name="grant-permission"></a>Accorder l’autorisation

Project créateurs et collaborateurs peuvent utiliser la `teamsfx permission grant` commande pour ajouter un nouveau collaborateur au projet :

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

Après avoir reçu l’autorisation requise, le créateur et les collaborateurs du projet peuvent partager le projet avec le nouveau collaborateur par GitHub, et le nouveau collaborateur peut avoir toutes les autorisations pour Microsoft 365 compte.

#### <a name="show-permission-status"></a>Afficher l’état des autorisations

Project créateurs et collaborateurs `teamsfx permission status` peuvent utiliser la commande pour afficher son Microsoft 365 de compte pour un env spécifique :

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Liste de tous les collaborateurs

Project créateurs et collaborateurs `teamsfx permission status` peuvent utiliser la commande pour afficher tous les collaborateurs pour un env spécifique :

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Flux de travail de collaboration E2E dans CLI

En tant que créateur de projet :

- Pour créer un nouvel onglet TeamsFx ou un projet de bot, sélectionnez Azure comme type d’hôte :

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

- Pour vous connecter à Microsoft 365 compte Azure et à un compte Azure :

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

- Pour mettre en service votre projet :

  ```bash
  teamsfx provision
  ```

- Pour afficher les collaborateurs :

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

- Pour ajouter un autre compte en tant que collaborateur. Assurez-vous que le compte ajouté se trouve sous le même client :

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="autorisation":::

- Pour pousser votre projet à l’GitHub

En tant que collaborateur Project :

- Clonez le projet à partir GitHub.
- Connectez-vous Microsoft 365 compte. Assurez-vous que le même Microsoft 365 compte est ajouté :

  ```bash
  teamsfx account login Microsoft 365
  ```

- Connectez-vous au compte Azure avec l’autorisation de collaborateur pour toutes les ressources Azure.

  ```bash
  teamsfx account login azure
  ```

- Vérifiez l’état de l’autorisation. Vous devez avoir l’autorisation propriétaire du projet :

  ```bash
  teamsfx permission status --env dev
  ```
  ![état de l’autorisation](./images/permission-status.png)

- Mettez à jour le code de l’onglet et déployez le projet à distance.
- Lancez à distance et le projet doit fonctionner comme il se doit.

## <a name="see-also"></a>Voir aussi

* [SDK TeamsFx pour TypeScript ou JavaScript](TeamsFx-SDK.md)
* [Gérer plusieurs environnements dans Teams Shared Computer Toolkit](TeamsFx-multi-env.md)
* [Collaborer sur Teams projet à l’aide Teams Shared Computer Toolkit](TeamsFx-collaboration.md)
 