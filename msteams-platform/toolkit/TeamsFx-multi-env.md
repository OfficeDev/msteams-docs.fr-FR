---
title: Plusieurs environnements TeamsFX dans Teams Shared Computer Toolkit
author: MuyangAmigo
description: À propos de TeamsFX multi-environnement
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 27172617db35126fb086d8691486e86c2946f0bd
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453585"
---
# <a name="manage-multiple-environments-in-teams-toolkit"></a>Gérer plusieurs environnements dans Teams Shared Computer Toolkit

 Teams Shared Computer Toolkit fournit un moyen simple pour créer et gérer plusieurs environnements, mettre en service et déployer des artefacts dans l’environnement cible pour Teams App.

 Avec plusieurs environnements, vous pouvez effectuer les choses suivantes :

1. **Test avant la production** : il est courant de configurer plusieurs environnements tels que le développement, le test et la mise en transit avant de publier une application Teams dans un environnement de production dans le cycle de vie de développement d’application moderne.

2. **Gérer les comportements** des applications dans différents environnements : vous pouvez définir différents comportements pour plusieurs environnements, tels que l’activer dans un environnement de production, mais le désactiver dans un environnement de développement.

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Assurez-vous que Teams projet d’application est ouvert dans Microsoft Visual Studio code.

## <a name="create-a-new-environment"></a>Créer un environnement

Après avoir créé un projet, Teams Shared Computer Toolkit par défaut crée :

* Un `local` environnement pour représenter les configurations de l’environnement d’ordinateur local.
* Un `dev` environnement pour représenter les configurations d’environnement distant ou cloud.

> [!NOTE]
> Chaque projet ne peut avoir qu’un `local` seul environnement, mais plusieurs environnements distants.

Pour ajouter un autre environnement distant, sélectionnez l’icône Teams dans la barre latérale, sélectionnez créer un environnement dans la section Sous Environnement, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="créer":::

> [!NOTE]
> Si vous avez plusieurs environnements existants, vous devez sélectionner un environnement existant pour créer le même environnement. La commande copie le contenu du fichier `config.<newEnv>.json` `azure.parameters.<newEnv>.json` de l’environnement existant que vous avez sélectionné vers le nouvel environnement en cours de création.

## <a name="select-target-environment"></a>Sélectionner l’environnement cible

Vous pouvez sélectionner l’environnement cible pour toutes les opérations liées à l’environnement. Le kit de ressources vous invite et demande un environnement cible lorsque vous avez plusieurs environnements distants, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="ajouter un env":::

## <a name="project-folder-structure"></a>Project structure de dossiers

Après avoir créé le projet, vous pouvez afficher les dossiers et les fichiers du projet dans la zone d’explorateur de Visual Studio Code. Outre les codes personnalisés, certains fichiers sont utilisés par les Teams Shared Computer Toolkit pour maintenir la config, l’état et le modèle de l’application. La liste suivante fournit des fichiers et décrit leur relation avec plusieurs environnements.

* `.fx/configs`: configurez les fichiers que l’utilisateur peut personnaliser pour l’Teams app.
  * `config.<envName>.json`: fichier de configuration par environnement.
  * `azure.parameters.<envName>.json`: fichier de paramètres par environnement pour la mise en service du bicep Azure.
  * `projectSettings.json`: paramètres de projet globaux, qui s’appliquent à tous les environnements.
  * `localSettings.json`: fichier de configuration de débogage local.
* `.fx/states`: résultat de la mise en service généré par le Shared Computer Toolkit.
  * `state.<envName>.json`: fichier de sortie de mise en service par environnement.
  * `<env>.userdata`: données utilisateur sensibles par environnement pour la sortie de mise en service.
* `templates`
  * `appPackage`: fichiers de modèles de manifeste d’application.
  * `azure`: fichiers de modèles biceps.

## <a name="customize-the-provision"></a>Personnaliser la mise en service

Teams Shared Computer Toolkit vous permet de modifier les fichiers de configuration et les fichiers modèles pour personnaliser la mise en service des ressources dans chaque environnement.

Le tableau suivant répertorie les scénarios courants pris en charge pour l’approvisionnement personnalisé et où personnaliser :

| Scénarios | Emplacement| Description |
| --- | --- | --- |
| Personnaliser la ressource Azure | <ul> <li>Fichiers biceps sous `templates/azure`.</li> <li>`.fx/azure.parameters.<envName>.json`.</li></ul> | [Personnalisez ARM paramètres et modèles.](provision.md#customize-arm-parameters-and-templates) |
| Réutiliser une application Azure AD existante pour Teams application | <ul> <li>`auth` section in`.fx/config.<envName>.json`.</li> </ul> |  [Utilisez une application Azure AD existante pour votre application Teams existante](provision.md#use-an-existing-azure-ad-app-for-your-teams-app). |
| Réutiliser une application Azure AD existante pour le bot | <ul> <li>`bot` section in`.fx/config.<envName>.json`.</li> </ul> | [Utilisez une application Azure AD existante pour votre bot](provision.md#use-an-existing-azure-ad-app-for-your-bot). |
| Ignorer l’ajout d’utilisateurs lors de l’SQL | <ul> <li>`skipAddingSqlUser``.fx/config.<envName>.json`in.</li> </ul> | [Ignorez l’ajout d’utilisateurs SQL base de données.](provision.md#skip-adding-user-for-sql-database) |
| Personnaliser le manifeste de l’application | <ul> <li>`templates/manifest.remote.template.json`.</li> <li>`manifest` section in`.fx/config.<envName>.json`.</li>  </ul> | [Personnalisez Teams manifeste de l’application dans Teams Shared Computer Toolkit](TeamsFx-manifest-customization.md). |

## <a name="scenarios"></a>Scénarios

### <a name="scenario-1-customize-teams-app-name-for-different-environment"></a>Scénario 1 : personnaliser Teams’application pour un environnement différent

Vous pouvez définir le nom Teams’application `myapp(dev)` pour l’environnement par `dev` défaut et `myapp(staging)` pour l’environnement de transit`staging`.

Effectuez les étapes suivantes pour la personnalisation :

* 1. Ouvrez le fichier de config `.fx/configs/config.dev.json`.
* 2. Mettre à jour la propriété du *manifeste > appName > court* à `myapp(dev)`

  Les mises à jour sont les `.fx/configs/config.dev.json` suivantes :

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          "appName": {
              "short": "myapp(dev)"
              ...
          }
      }
      ...
  }
  ```

* 3. Créez un environnement et nommez-le `staging` s’il n’existe pas.
* 4. Ouvrez le fichier de config `.fx/configs/config.staging.json`.
* 5. Mettre à jour la même propriété `myapp(staging)`.
* 6. Exécutez la commande de mise en service sur `dev` et l’environnement `staging` pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande de mise en service Teams Shared Computer Toolkit, consultez [la mise en service](provision.md#provision-using-teams-toolkit).

### <a name="scenario-2-customize-teams-app-description-for-different-environment"></a>Scénario 2 : personnaliser Teams description de l’application pour un environnement différent

Dans ce scénario, vous allez apprendre à définir différentes descriptions Teams’application pour différents environnements :

* Pour l’environnement par défaut `dev`, la description sera `my app description for dev`;
* Pour l’environnement de transit `staging`, la description sera `my app description for staging`;

Effectuez les étapes suivantes pour la personnalisation :

* 1. Ouvrez le fichier de config `.fx/configs/config.dev.json`.
* 2. Ajoutez une nouvelle propriété de *manifeste > description > courte* avec la valeur `my app description for dev`.

  Les mises à jour sont les `.fx/configs/config.dev.json` suivantes :

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          ...
          "description": {
              "short": "`my app description for dev"
              ...
          }
      }
      ...
  }
  ```

* 3. Créez un environnement et nommez-le `staging` s’il n’existe pas.
* 4. Ouvrez le fichier de config `.fx/configs/config.staging.json`.
* 5. Ajoutez la même propriété à `my app description for staging`.
* 6. Ouvrez Teams de manifeste d’application pour une application distante`templates/appPackage/manifest.remote.template.json`.
* 7. Mettez à jour la propriété `description > short` pour utiliser la **variable** définie dans la configuration des fichiers avec la syntaxe `{{config.manifest.description.short}}`de mustache .
  
  Les mises à jour sont les `manifest.remote.template.json` suivantes :

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "{{config.manifest.description.short}}", 
      ...
    },
    ...
  }
  ```

* 8. Exécutez la commande de mise en service sur `dev` et l’environnement `staging` pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande de mise en service Teams Shared Computer Toolkit, consultez [la mise en service](provision.md#provision-using-teams-toolkit).

### <a name="scenario-3-customize-teams-app-description-for-all-environments"></a>Scénario 3 : personnaliser la description Teams’application pour tous les environnements

Dans ce scénario, vous allez apprendre à définir la description de Teams application pour `my app description` tous les environnements.

Comme le Teams de manifeste d’application est partagé dans tous les environnements, nous pouvons mettre à jour la valeur de description dans celui-ci pour notre cible :

* 1. Ouvrez Teams de manifeste d’application pour une application distante`templates/appPackage/manifest.remote.template.json`.
* 2. Mettez à jour la propriété `description > short` **avec une chaîne codée en dur**`my app description`.
  
  Les mises à jour sont les `manifest.remote.template.json` suivantes :

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "my app description",
      ...
    },
    ...
  }

* 3. Run provision command against **all** environment to update the app name in remote environments. To run provision command with Teams Toolkit, see [provision](provision.md#provision-using-teams-toolkit).

### Scenario 4: customize Azure resources for different environment

You can customize Azure resources for each environment, for example specify Azure Function name, by editing the environment corresponding to `.fx/configs/azure.parameters.{env}.json` file.

For more information on Bicep template and parameter files, see [provision cloud resources](provision.md)

## See also

* [Provision cloud resources](provision.md)
* [Add more cloud resources](add-resource.md)
* [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)
