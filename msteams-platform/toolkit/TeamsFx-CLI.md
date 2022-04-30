---
title: Interface de ligne de commande TeamsFx
author: MuyangAmigo
description: Décrit l’interface de ligne de commande TeamsFx
ms.author: zhany
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ab9bad973d337d783c1de70c2ad8575a67d6cb6e
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111436"
---
# <a name="teamsfx-library"></a>Bibliothèque TeamsFx

Microsoft Teams Framework (TeamsFx) est une bibliothèque qui encapsule les fonctionnalités courantes et les modèles d’intégration (comme l’accès simplifié à Microsoft Identity). Vous pouvez créer des applications pour Microsoft Teams avec aucune configuration.

Voici une liste des principales fonctionnalités de TeamsFx :

* **Collaboration TeamsFx** : permet aux développeurs et au propriétaire du projet d’inviter d’autres collaborateurs au projet TeamsFx. Vous pouvez collaborer pour déboguer et déployer un projet TeamsFx.

* **Interface CLI TeamsFx** : elle accélère Teams développement d’applications. Il active également le scénario CI/CD dans lequel vous pouvez intégrer l’interface CLI dans des scripts pour l’automatisation.

* **TeamsFx SDK** : TeamsFx Software Development Kit (SDK) est la principale bibliothèque de code TeamsFx encapsulant une authentification simple pour le code côté client et côté serveur, adaptée aux développeurs Teams.

## <a name="teamsfx-command-line-interface"></a>Interface de ligne de commande TeamsFx

TeamsFx est une interface de ligne de commande textuelle qui accélère le développement d’applications Teams. Il vise à offrir une expérience centrée sur le clavier lors de la création d’applications Teams. Il active également le scénario CI/CD dans lequel vous pouvez intégrer l’interface CLI dans des scripts pour l’automatisation.

Pour plus d’informations, voir :

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
| `teamsfx new`| Création d’une nouvelle application Teams.|
| `teamsfx account`| Gérer les comptes de service cloud. Les services cloud pris en charge sont « Azure » et « Microsoft 365 ». |
| `teamsfx env` | Gérer des environnements. |
| `teamsfx capability`| Ajoutez de nouvelles fonctionnalités à l’application actuelle.|
| `teamsfx resource`  | Gérez les ressources dans l’application actuelle.|
| `teamsfx provision` | Provisionnez des ressources cloud dans l’application actuelle.|
| `teamsfx deploy` | Déployez l’application actuelle.  |
| `teamsfx package` | Créez votre application Teams dans un package pour la publication.|
| `teamsfx validate` | Valider l’application actuelle.|
| `teamsfx publish` | Publier l’application sur Teams.|
| `teamsfx preview` | Affichez un aperçu de l’application actuelle. |
| `teamsfx config`  | Gérer les données de configuration. |
| `teamsfx permission`| Collaborez avec d’autres développeurs dans le même projet.|

## `teamsfx new`

Par défaut, `teamsfx new` passe en mode interactif et vous guide tout au long du processus de création d’une nouvelle application Teams. Vous pouvez également utiliser le mode non interactif en définissant `--interactive` l’indicateur `false` sur.

| `teamsFx new` Commande | Description |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Créer une application à partir d’un modèle existant |
| `teamsfx new template list`     | Répertorier tous les modèles disponibles |

### <a name="parameters-for-teamsfx-new"></a>Paramètres pour `teamsfx new`

| Paramètre | Conditions requises | Description |
|:---------------- |:-------------|:-------------|
|`--app-name` | Oui| Nom de votre application Teams.|
|`--interactive`| Non | Sélectionnez les options de manière interactive. Les options sont `true` et `false` et la valeur par défaut est `true`.|
|`--capabilities`| Non| Choisissez des fonctionnalités Teams de l’application, les options multiples sont `tab`, `bot`, `messaging-extension` et `tab-spfx`. La valeur par défaut est `tab`.|
|`--programming-language`| Non| Langage de programmation du projet. Les options sont `javascript` ou `typescript` et la valeur par défaut est `javascript`.|
|`--folder`| Non | Répertoire de projet. Un sous-dossier avec le nom de votre application est créé sous ce répertoire. La valeur par défaut est `./`.|
|`--spfx-framework-type`| Non| Applicable si la capacité `Tab(SPfx)` est sélectionnée. Infrastructure frontale. Les options sont `none` et `react`, et la valeur par défaut est `none`.|
|`--spfx-web part-name`| Non | Applicable si la capacité `Tab(SPfx)` est sélectionnée. La valeur par défaut est « helloworld ».|
|`--spfx-web part-desp`| Non | Applicable si la capacité `Tab(SPfx)` est sélectionnée. La valeur par défaut est « description helloworld ». |
|`--azure-resources`| Non| Applicable si contient la fonctionnalité `tab`. Ajoutez des ressources Azure à votre projet. Les options multiples sont `sql` (Azure SQL Database) et `function` (Azure Functions). |

### <a name="scenarios-for-teamsfx-new"></a>Scénarios pour `teamsfx new`

Vous pouvez utiliser le mode interactif pour créer une application Teams. Les scénarios de contrôle de tous les paramètres avec `teamsfx new` sont les suivants :

#### <a name="tab-app-hosted-on-spfx-using-react"></a>Application d’onglet hébergée sur SPFx à l’aide de React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>Application Teams en JavaScript avec onglet, capacités de bot et Azure Functions

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Application de l’onglet Teams avec Azure Functions et Azure SQL

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
| `teamsfx env list` | Lister tous les environnements. |

### <a name="scenarios-for-teamsfx-env"></a>Scénarios pour `teamsfx env`

Les scénarios pour `teamsfx env` sont les suivants :

#### <a name="create-a-new-environment"></a>Créez entièrement un nouveau environnement

Ajoutez un nouvel environnement en copiant depuis l’environnement de développement existant :

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Ajoutez de nouvelles fonctionnalités à l’application actuelle.

| `teamsFx capability` Commande  | Description |
|:----------------  |:-------------|
| `teamsfx capability add tab` | Ajouter un onglet  |
| `teamsfx capability add bot` | Ajouter un robot |
| `teamsfx capability add messaging-extension`| Ajouter l’extension de message |

> [!NOTE]
> Si votre projet inclut un bot, l’extension de message ne peut pas être ajoutée et s’applique vice versa. Vous pouvez inclure à la fois des extensions de bot et de message dans votre projet lors de la création d’un nouveau projet d’application Teams.

## `teamsfx resource`

Gérer les ressources dans l’application en cours. `<resource-type>` pris en charge sont : `azure-sql`, `azure-function` et `azure-apim` .

| `teamsFx resource` Commande  | Description |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Ajouter une ressource dans l’application actuelle.|
| `teamsfx resource show <resource-type>`      | Afficher les détails de configuration de la ressource. |
| `teamsfx resource list`      | Répertorier toutes les ressources de l’application en cours. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Paramètres pour `teamsfx resource add azure-function`

| Paramètre  | Conditions requises | Description |
|----------------  |-------------|-------------|
|`--function-name`| Oui | Indiquez un nom de fonction. La valeur par défaut est `getuserprofile`. |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Paramètres pour `teamsfx resource add azure-sql`

#### `--function-name`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--function-name`| Oui | Indiquez un nom de fonction. La valeur par défaut est `getuserprofile`. |

> [!NOTE]
> Le nom de la fonction est vérifié en tant que SQL et doit être accessible à partir de la charge de travail du serveur. Si votre projet ne contient pas de `Azure Functions`, créez-en un pour vous.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Paramètres pour `teamsfx resource add azure-apim`

> [!TIP]
> Les options prennent effet lorsque vous essayez d’utiliser une instance `APIM` existante. Par défaut, vous n’avez pas à spécifier d’options et cela crée une nouvelle instance au cours de l’étape `teamsfx provision`.

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--subscription`| Oui | Sélectionnez un abonnement Azure|
|`--apim-resource-group`| Oui| Nom du groupe de ressources. |
|`--apim-service-name`| Oui | Nom de l’instance du service de gestion des API. |
|`--function-name`| Oui | Indiquez un nom de fonction. La valeur par défaut est `getuserprofile`. |

> [!NOTE]
> `Azure API Management` a besoin pour fonctionner avec `Azure Functions`. Si votre projet ne contient pas de `Azure Functions`, vous pouvez en créer un.

## `teamsfx provision`

Provisionnez les ressources cloud dans l’application actuelle.

### <a name="parameters-for-teamsfx-provision"></a>Paramètres pour `teamsfx provision`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui| Sélectionnez un environnement pour le projet. |
|`--subscription`| Non | Spécifiez un ID d’abonnement Azure. |
|`--resource-group`| Non | Définissez le nom d’un groupe de ressources existant. |
|`--sql-admin-name`| Non | Applicable lorsqu’il y a une ressource SQL dans le projet. Nom d’administrateur de SQL.|
|`--sql-password`| Non| Applicable lorsqu’il y a une ressource SQL dans le projet. Mot de passe administrateur de SQL.|

## `teamsfx deploy`

Cette commande permet de déployer l’application en cours. Par défaut, il déploie l’intégralité du projet, mais il est également possible de déployer partiellement. Les options multiples sont `frontend-hosting`, `function`, `apim`, `teamsbot`, et `spfx`.

### <a name="parameters-for-teamsfx-deploy"></a>Paramètres pour `teamsfx deploy`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui| Sélectionnez un environnement existant pour le projet. |
|`--open-api-document`| Non | Applicable lorsqu’il y a une ressource APIM dans le projet. Le chemin d’accès au fichier de document API ouvert. |
|`--api-prefix`| Non | Applicable lorsqu’il y a une ressource APIM dans le projet. Le préfixe du nom de l’API. Le nom unique par défaut de l’API est `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| Non | Applicable lorsqu’il y a une ressource APIM dans le projet. La version d’API. |

## `teamsfx validate`

Valider la candidature en cours. Cette commande valide le fichier manifeste de votre application.

### <a name="parameters-for-teamsfx-validate"></a>Paramètres pour `teamsfx validate`

`--env` : Sélectionnez un environnement existant pour le projet.

## `teamsfx publish`

Publier l’application sur Teams.

### <a name="parameters-for-teamsfx-publish"></a>Paramètres pour `teamsfx publish`

`--env` : Sélectionnez un environnement existant pour le projet.

## `teamsfx package`

Créez votre application Teams dans un package pour la publication.

## `teamsfx preview`

Prévisualisez l’application actuelle en local ou à distance.

### <a name="parameters-for-teamsfx-preview"></a>Paramètres pour `teamsfx preview`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--local`| Non | Prévisualisez l’application en local. `--local` est exclusif avec `--remote`. |
|`--remote`| Non | Prévisualisez l’application à distance. `--remote` est exclusif avec `--local`. |
|`--env`| Non | Sélectionnez un environnement existant pour le projet lorsque le paramètre `--remote` est ajouté. |
|`--folder`| Non | Répertoire racine du projet. La valeur par défaut est `./`. |
|`--browser`| Non | Le navigateur pour ouvrir le client Web Teams. Les options sont `chrome`, `edge` et `default` telles que le navigateur par défaut du système et la valeur est `default`. |
|`--browser-arg`| Non | Argument à transmettre au navigateur, nécessite --browser, peut être utilisé plusieurs fois, par exemple, --browser-args="--guest" |
|`--sharepoint-site`| Non | URL du site SharePoint, comme `{your-tenant-name}.sharepoint.com` pour l’aperçu à distance du projet SPFx. |

### <a name="scenarios-for-teamsfx-preview"></a>Scénarios pour `teamsfx preview`

#### <a name="local-preview"></a>Prévisualisation

Dépendances :

* Node.js
* Kit de développement logiciel .NET
* Azure Functions Core Tools

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Préversion à distance

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> Les journaux des services d’arrière-plan, tels que React, sont enregistrés au format `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Gérez les données de configuration soit dans la portée de l’utilisateur, soit dans la portée du projet.

| `teamsfx config` Commande  | Description |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Afficher la valeur de configuration de l’option |
| `teamsfx config set <option> <value>` | Mettre à jour la valeur de configuration de l’option |

### <a name="parameters-for-teamsfx-config"></a>Paramètres pour `teamsfx config`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui | Sélectionnez un environnement existant pour le projet. |
|`--folder`| Non | Répertoire de projet. Ceci est utilisé pour obtenir ou définir la configuration du projet. La valeur par défaut est `./`. |
|`--global`| Non | Cope de configuration. Si cela est vrai, la portée est limitée à la portée de l’utilisateur au lieu de la portée du projet. La valeur par défaut est `false`. Actuellement, les configurations globales prises en charge incluent `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools`, `validate-node`. |

### <a name="scenerios-for-teamsfx-config"></a>Scenerios pour `teamsfx config`

Les secrets du `.userdata` fichier sont cryptés `teamsfx config` et peuvent vous aider à afficher ou à mettre à jour les valeurs.

#### <a name="stop-sending-telemetry-data"></a>Arrêter l’envoi de données de télémétrie

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Désactiver le vérificateur d’environnement

Il existe trois configurations pour activer ou désactiver Node.js, le Kit de développement logiciel (SDK) .NET et la validation Azure Functions Core Tools, et toutes sont activées par défaut. Vous pouvez définir la configuration sur « off » si vous n’avez pas besoin de la validation des dépendances et que vous souhaitez installer les dépendances par vous-même. Consultez les guides suivants :

* [guide d’installationNode.js](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [Guide d’installation du Kit de développement logiciel (SDK) .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [guide d’installation de Azure Functions Core Tools](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools).

Pour désactiver la validation du SDK .NET, vous pouvez utiliser la commande suivante :

```bash
teamsfx config set validate-dotnet-sdk off
```

Pour activer la validation du Kit de développement logiciel (SDK) .NET, vous pouvez utiliser la commande suivante :

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Afficher toutes les configurations d’étendue utilisateur

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Afficher toutes les configurations dans le projet

Le secret est déchiffré automatiquement :

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Mettre à jour la configuration du secret dans le projet

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

L’interface CLI TeamsFx fournit des `teamsFx permission` commandes pour le scénario de collaboration.

| `teamsFx permission` commande | Description |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Accordez l’autorisation au compte Microsoft 365 collaborateur pour le projet d’un environnement spécifié. |
| `teamsfx permission status` | Afficher l’état des autorisations pour le projet |

### <a name="parameters-for-teamsfx-permission-grant"></a>Paramètres pour `teamsfx permission grant`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui | Indiquez le nom de l’environnement. |
|`--email`| Oui | Indiquez l’adresse e-mail Microsoft 365 du collaborateur. Vérifiez que le compte du collaborateur se trouve dans le même locataire que le créateur. |

### <a name="parameters-for-teamsfx-permission-status"></a>Paramètres pour `teamsfx permission status`

| Paramètre | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui | Indiquez le nom de l’environnement. |
|`--list-all-collaborators` | Non | Avec cet indicateur, Teams Shared Computer Toolkit CLI imprime tous les collaborateurs de ce projet. |

### <a name="scenarios-for-teamsfx-permission"></a>Scénarios pour `teamsfx permission`

Les autorisations pour les projets `TeamsFx` sont les suivantes :

#### <a name="grant-permission"></a>Accorder l’autorisation

Le créateur du projet et les collaborateurs peuvent utiliser la commande `teamsfx permission grant` pour ajouter un nouveau collaborateur au projet :

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

Après avoir reçu l’autorisation requise, le créateur du projet et les collaborateurs peuvent partager le projet avec le nouveau collaborateur par GitHub, et le nouveau collaborateur peut avoir toutes les autorisations pour le compte Microsoft 365.

#### <a name="show-permission-status"></a>Afficher l’état de l’autorisation

Le créateur du projet et les collaborateurs peuvent utiliser la commande `teamsfx permission status` pour afficher l’autorisation de son compte Microsoft 365 pour un environnement spécifique :

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Répertorier tous les collaborateurs

Le créateur du projet et les collaborateurs peuvent utiliser la commande `teamsfx permission status` pour afficher tous les collaborateurs pour un environnement spécifique :

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Flux de travail E2E Collaboration dans CLI

En tant que créateur de projet :

* Pour créer un onglet ou un projet de bot TeamsFx, puis sélectionnez Azure comme type d’hôte :

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

* Pour vous connecter au compte Microsoft 365 et compte Azure :

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

* Pour provisionner votre projet :

  ```bash
  teamsfx provision
  ```

* Pour afficher les collaborateurs :

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

* Pour ajouter un autre compte en tant que collaborateur. Vérifiez que le compte ajouté se trouve sous le même locataire :

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="autorisation":::

* Pour pousser votre projet vers GitHub

En tant que collaborateur Project :

* Clonez le projet à partir de GitHub.
* Connectez-vous au compte Microsoft 365. Vérifiez que le même compte Microsoft 365 est ajouté :

  ```bash
  teamsfx account login Microsoft 365
  ```

* Connectez-vous au compte Azure avec l’autorisation de contributeur pour toutes les ressources Azure.

  ```bash
  teamsfx account login azure
  ```

* Vérifiez l’état des autorisations. Vous devez disposer des autorisations de propriétaire du projet :

  ```bash
  teamsfx permission status --env dev
  ```

  ![état de l’autorisation](./images/permission-status.png)

* Mettez à jour le code d’onglet et déployez le projet à distance.
* Lancez à distance et le projet doit fonctionner correctement.

## <a name="see-also"></a>Voir aussi

* [SDK TeamsFx pour TypeScript ou JavaScript](TeamsFx-SDK.md)
* [Gérer plusieurs environnements dans Teams Shared Computer Toolkit](TeamsFx-multi-env.md)
* [Collaborer sur un projet Teams à l'aide de Teams Toolkit](TeamsFx-collaboration.md)
* [Vue d’ensemble du Kit de ressources Teams](teams-toolkit-fundamentals.md)
