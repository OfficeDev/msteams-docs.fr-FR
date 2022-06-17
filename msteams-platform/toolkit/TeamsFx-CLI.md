---
title: Interface de ligne de commande TeamsFx
author: MuyangAmigo
description: Dans ce module, découvrez la bibliothèque TeamsFx, l’interface de ligne de commande TeamsFx, les commandes prises en charge et ses scénarios
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d269da398280f51a3225414f279a25fcd5d9d7cf
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142072"
---
# <a name="teamsfx-library"></a>Bibliothèque TeamsFx

Microsoft Teams Framework (TeamsFx) est une bibliothèque qui encapsule des fonctionnalités et des modèles d’intégration courants, tels que l’accès simplifié à Microsoft Identity. Vous pouvez créer des applications pour Microsoft Teams avec aucune configuration.

Voici une liste des principales fonctionnalités de TeamsFx :

* **Collaboration TeamsFx** : permet aux développeurs et au propriétaire du projet d’inviter d’autres collaborateurs au projet TeamsFx. Vous pouvez collaborer pour déboguer et déployer un projet TeamsFx.

* **Interface CLI TeamsFx** : accélère Teams développement d’applications. Il active également le scénario CI/CD dans lequel vous pouvez intégrer l’interface CLI dans des scripts pour l’automatisation.

* **Kit de développement logiciel (SDK) TeamsFx** : fournit l’accès à la base de données, telle que la bibliothèque de code TeamsFx principale contenant une authentification simple pour le code côté client et côté serveur adapté aux développeurs Teams.

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
| `teamsfx add`| Ajoute des fonctionnalités à votre application Teams.|
| `teamsfx account`| Gérer les comptes de service cloud. Les services cloud pris en charge sont « Azure » et « Microsoft 365 ». |
| `teamsfx env` | Gérer des environnements. |
| `teamsfx provision` | Provisionnez des ressources cloud dans l’application actuelle.|
| `teamsfx deploy` | Déployez l’application actuelle.  |
| `teamsfx package` | Créez votre application Teams dans un package pour la publication.|
| `teamsfx validate` | Valider l’application actuelle.|
| `teamsfx publish` | Publier l’application sur Teams.|
| `teamsfx preview` | Affichez un aperçu de l’application actuelle. |
| `teamsfx config`  | Gérer les données de configuration. |
| `teamsfx permission`| Collaborez avec d’autres développeurs dans le même projet.|

## `teamsfx new`

Par défaut, `teamsfx new` est en mode interactif et des guides pour créer une application Teams. Vous pouvez travailler en mode non interactif en définissant `--interactive` l’indicateur `false`sur .

| Command | Description |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Créer une application à partir d’un modèle existant |
| `teamsfx new template list`     | Répertorier tous les modèles disponibles |

### <a name="parameters-for-teamsfx-new"></a>Paramètres pour `teamsfx new`

| Paramètre | Conditions requises | Description |
|:---------------- |:-------------|:-------------|
|`--app-name` | Oui| Nom de votre application Teams.|
|`--interactive`| Non | Sélectionnez les options de manière interactive. Les options sont `true` et `false` et la valeur par défaut est `true`.|
|`--capabilities`| Non| Choisissez Teams fonctionnalités de l’application, les options sont `tab`: , `tab-non-sso`, `bot``tab-spfx`, `message-extension`, `command-bot``notification`, `sso-launch-page``search-app`. La valeur par défaut est `tab`.|
|`--programming-language`| Non| Langage de programmation du projet. Les options sont `javascript` ou `typescript` et la valeur par défaut est `javascript`.|
|`--folder`| Non | Répertoire de projet. Un sous-dossier avec le nom de votre application est créé sous ce répertoire. La valeur par défaut est `./`.|
|`--spfx-framework-type`| Non| Applicable si la capacité `SPFx tab` est sélectionnée. Infrastructure frontale. Les options sont `none`, `react` et `minimal`, et la valeur par défaut est `none`.|
|`--spfx-web part-name`| Non | Applicable si la capacité `SPFx tab` est sélectionnée. La valeur par défaut est « helloworld ».|
|`--bot-host-type-trigger`| Non | Applicable si la capacité `Notification bot` est sélectionnée. Les options sont `http-restify`, `http-functions`et `timer-functions`. La valeur par défaut est `http-restify`.|

### <a name="scenarios-for-teamsfx-new"></a>Scénarios pour `teamsfx new`

Vous pouvez utiliser le mode interactif pour créer une application Teams. La liste suivante fournit des scénarios de contrôle de tous les paramètres avec `teamsfx new`:

* Bot de notification déclenché par Http avec serveur restify

  ```bash
  teamsfx new --interactive false --capabilities "notification" --bot-host-type-trigger "http-restify" --programming-language "typescript" --folder "./" --app-name       MyAppName
  ```

* Teams bot de commande et de réponse

  ```bash
  teamsfx new --interactive false --capabilities "command-bot" --programming-language "typescript" --folder "./" --app-name myAppName
  ```

* Application d’onglet hébergée sur SPFx à l’aide de React

  ```bash
  teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
  ```

## `teamsfx add`

Le tableau suivant répertorie les différentes fonctionnalités de votre application Teams ainsi que leur description.

| Command | Description |
|:----------------  |:-------------|
| `teamsfx add notification` | Envoyez une notification à Microsoft Teams via différents déclencheurs. |
| `teamsfx add command-and-response` | Répondez aux commandes simples dans Microsoft Teams conversation.|
| `teamsfx add sso-tab` | Teams pages web sensibles aux identités incorporées dans Microsoft Teams.|
| `teamsfx add tab` | Pages web Hello World incorporées dans Microsoft Teams.|
| `teamsfx add bot` | Hello World Chatbot pour exécuter des tâches simples et répétitives par utilisateur. |
| `teamsfx add message-extension` | Extension de message Hello World permettant des interactions via des boutons et des formulaires. |
| `teamsfx add azure-function`| Solution de calcul serverless basée sur les événements qui vous permet d’écrire moins de code. |
| `teamsfx add azure-apim` | Plateforme de gestion multicloud hybride pour les API dans tous les environnements.|
| `teamsfx add azure-sql` | Service de base de données relationnelle toujours à jour conçu pour le cloud. |
| `teamsfx add azure-keyvault` | Service cloud permettant de stocker et d’accéder en toute sécurité aux secrets. |
| `teamsfx add sso` | Développez une fonctionnalité de Sign-On unique pour Teams pages de lancement et la fonctionnalité Bot. |
| `teamsfx add api-connection [auth-type]` | Connecter à une API avec prise en charge de l’authentification à l’aide du Kit de développement logiciel (SDK) TeamsFx. |
| `teamsfx add cicd` | Ajoutez des flux de travail CI/CD pour GitHub, Azure DevOps ou Jenkins.|

## `teamsfx account`

Le tableau suivant répertorie les comptes de service cloud, tels qu’Azure et Microsoft 365.

| Command | Description |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Connectez-vous au service cloud sélectionné. Les options de service sont Microsoft 365 ou Azure. |
| `teamsfx account logout <service>`  | déconnectez-vous du service cloud sélectionné. Les options de service sont Microsoft 365 ou Azure. |
| `teamsfx account set --subscription` | Mettez à jour les paramètres du compte pour définir un ID d’abonnement. |

## `teamsfx env`

Le tableau suivant répertorie les différents environnements.

|  Command  | Description |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Ajoutez un nouvel environnement en copiant à partir de l’environnement spécifié. |
| `teamsfx env list` | Lister tous les environnements. |

### <a name="scenarios-for-teamsfx-env"></a>Scénarios pour `teamsfx env`

Créez un environnement en copiant à partir de l’environnement de développement existant :

```bash
teamsfx env add staging --env dev
```

## `teamsfx provision`

Provisionnez les ressources cloud dans l’application actuelle.

| `teamsFx provision` Commande | Description |
|:----------------  |:-------------|
| `teamsfx provision manifest` | Provisionnez une application Teams dans Teams portail des développeurs avec les informations correspondantes spécifiées dans le fichier manifeste donné. |

### <a name="parameters-for-teamsfx-provision"></a>Paramètres pour `teamsfx provision`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui| Sélectionnez un environnement pour le projet. |
|`--subscription`| Non | Spécifiez un ID d’abonnement Azure. |
|`--resource-group`| Non | Définissez le nom d’un groupe de ressources existant. |
|`--sql-admin-name`| Non | Applicable lorsqu’il y a SQL ressource dans le projet. Nom d’administrateur de SQL.|
|`--sql-password`| Non| Applicable lorsqu’il y a SQL ressource dans le projet. Mot de passe administrateur de SQL.|

## `teamsfx deploy`

Cette commande permet de déployer l’application en cours. Par défaut, il déploie l’intégralité du projet, mais il est également possible de déployer partiellement. Les options sont `frontend-hosting`, , `apim``function`, `bot``spfx`et `aad-manifest` `manifest`.

### <a name="parameters-for-teamsfx-deploy"></a>Paramètres pour `teamsfx deploy`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui| Sélectionnez un environnement existant pour le projet. |
|`--open-api-document`| Non | Applicable lorsqu’il existe une ressource APIM dans le projet. Le chemin d’accès au fichier de document API ouvert. |
|`--api-prefix`| Non | Applicable lorsqu’il existe une ressource APIM dans le projet. Le préfixe du nom de l’API. Le nom unique par défaut de l’API est `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| Non | Applicable lorsqu’il existe une ressource APIM dans le projet. La version d’API. |
|`--include-app-manifest`| Non | Indique s’il faut déployer le manifeste d’application sur Teams plateforme. Les options sont et `yes` `not`. La valeur par défaut est `no`. |
|`--include-aad-manifest`| Non | Indique s’il faut déployer un manifeste aad. Les options sont et `yes` `not`. La valeur par défaut est `no`. |

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
|`--m365-host`| Affichez un aperçu de l’application dans Teams, Outlook ou Office. Les options sont `teams`, `outlook` et `office`. La valeur par défaut est `teams`. |

### <a name="scenarios-for-teamsfx-preview"></a>Scénarios pour `teamsfx preview`

La liste suivante fournit les scénarios courants pour la préversion teamsfx :

* Prévisualisation

  Dépendances :

  * Node.js
  * Kit de développement logiciel .NET
  * Azure Functions Core Tools

  ```bash
  teamsfx preview --local
  teamsfx preview --local --browser chrome
  ```

* Préversion à distance

  ```bash
  teamsfx preview --remote
  teamsfx preview --remote --browser edge
  ```

  > [!NOTE]
  > Les journaux des services d’arrière-plan, tels que React, sont enregistrés au format `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Les données de configuration se trouve dans l’étendue de l’utilisateur ou dans l’étendue du projet.

|  Command  | Description |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Afficher la valeur de configuration de l’option |
| `teamsfx config set <option> <value>` | Mettre à jour la valeur de configuration de l’option |

### <a name="parameters-for-teamsfx-config"></a>Paramètres pour `teamsfx config`

| Paramètre  | Conditions requises | Description |
|:----------------  |:-------------|:-------------|
|`--env`| Oui | Sélectionnez un environnement existant pour le projet. |
|`--folder`| Non | Project répertoire utilisé pour obtenir ou définir la configuration du projet. La valeur par défaut est `./`. |
|`--global`| Non | Cope de configuration. Si la valeur est true, l’étendue est limitée à l’étendue utilisateur au lieu de l’étendue du projet. La valeur par défaut est `false`. À présent, les configurations globales prises en charge incluent `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools``validate-node`. |

### <a name="scenarios-for-teamsfx-config"></a>Scénarios pour `teamsfx config`

Les secrets du `.userdata` fichier sont chiffrés `teamsfx config` et peuvent vous aider à afficher ou à mettre à jour les valeurs requises.

* Arrêter l’envoi de données de télémétrie

  ```bash
  teamsfx config set telemetry off
  ```

* Désactiver le vérificateur d’environnement

  Il existe trois configurations pour activer ou désactiver Node.js, le Kit de développement logiciel (SDK) .NET et la validation Azure Functions Core Tools, et toutes sont activées par défaut. Vous pouvez définir la configuration sur « off » si vous n’avez pas besoin de la validation des dépendances et que vous souhaitez installer les dépendances par vous-même. Consultez les guides suivants :

  * [guide d’installationNode.js](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
  * [Guide d’installation du Kit de développement logiciel (SDK) .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
  * [Azure Functions Guide d’installation des outils principaux](<https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure>- functions-core-tools).

  Pour désactiver la validation du SDK .NET, vous pouvez utiliser la commande suivante :

  ```bash
  teamsfx config set validate-dotnet-sdk off
  ```

  Pour activer la validation du Kit de développement logiciel (SDK) .NET, vous pouvez utiliser la commande suivante :

  ```bash
  teamsfx config set validate-dotnet-sdk on
  ```

* Afficher toutes les configurations d’étendue utilisateur

  ```bash
  teamsfx config get -g
  ```

* Afficher toutes les configurations dans le projet

  Le secret est déchiffré automatiquement :

    ```bash
    teamsfx config get --env dev
    ```

* Mettre à jour la configuration du secret dans le projet

  ```bash
  teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
  ```

## `teamsfx permission`

L’interface CLI TeamsFx fournit des `teamsFx permission` commandes pour les scénarios de collaboration.

|  Commande | Description |
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

La liste suivante fournit les autorisations requises pour `TeamsFx` les projets :

* Accorder l’autorisation

  Le créateur du projet et les collaborateurs peuvent utiliser la commande `teamsfx permission grant` pour ajouter un nouveau collaborateur au projet :

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  Après avoir reçu l’autorisation requise, le créateur et les collaborateurs du projet peuvent partager le projet avec le nouveau collaborateur par GitHub, et le nouveau collaborateur peut avoir toutes les autorisations pour Microsoft 365 compte.

* Afficher l’état de l’autorisation

  Project créateur et collaborateurs peuvent utiliser `teamsfx permission status` la commande pour afficher Microsoft 365 autorisation de compte pour un env spécifique :

  ```bash
  teamsfx permission status --env dev
  ```

* Répertorier tous les collaborateurs

  Le créateur du projet et les collaborateurs peuvent utiliser la commande `teamsfx permission status` pour afficher tous les collaborateurs pour un environnement spécifique :

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

* Flux de travail E2E Collaboration dans CLI

  * En tant que créateur de projet :

    * Pour créer un onglet ou un projet de bot TeamsFx, puis sélectionnez Azure comme type d’hôte :

      ```bash
      teamsfx new --interactive false --app-name newapp --host-type azure
      ```

    * Pour vous connecter à Microsoft 365 compte et compte Azure :

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

  * En tant que collaborateur Project :

    * Clonez le projet à partir de GitHub.
    * Connectez-vous à Microsoft 365 compte. Vérifiez que le même compte Microsoft 365 est ajouté :

      ```bash
      teamsfx account login Microsoft 365
      ```

    * Connectez-vous au compte Azure avec l’autorisation contributeur pour toutes les ressources Azure.

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
