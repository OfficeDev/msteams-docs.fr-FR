---
title: 'TeamsFX : plusieurs environnements dans le Kit de ressources Teams'
author: MuyangAmigo
description: À propos du multi-environnement TeamsFX
ms.author: nintan
ms.localizationpriority: high
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: b9719add5036ae533ce6d7c395ab95a5905bcbb8
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111863"
---
# <a name="manage-multiple-environments"></a>Gérer plusieurs environnements

 Teams Toolkit offre un moyen simple de créer et de gérer plusieurs environnements, de provisionner et de déployer des artefacts dans l’environnement cible pour l’application Teams.

 Vous pouvez effectuer les opérations suivantes avec les différents environnements :

1. **Test avant le début de production** : vous pouvez configurer plusieurs environnements tels que le développement, le test et la préproduction avant de publier une application Teams dans un environnement de production dans le cycle de vie moderne du développement d’applications

2. **Gérer les comportements des applications dans différents environnements**: vous pouvez configurer différents comportements pour plusieurs environnements, tels que l’activation de la télémétrie dans un environnement de production, tout en la désactivant dans l’environnement de développement

## <a name="prerequisite"></a>Conditions préalables

* [Installer la dernière version d’Office](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Vérifiez que le projet d’application Teams est ouvert dans Microsoft Visual Studio code.

## <a name="create-a-new-environment"></a>Créez entièrement un nouveau environnement

Après avoir créé un projet, le Kit de ressources Teams crée par défaut :

* Un environnement `local` pour représenter les configurations de l’environnement d’ordinateur local
* Un environnement `dev` pour représenter les configurations d’environnement distant ou cloud

> [!NOTE]
> Chaque projet ne peut avoir qu’un seul environnement `local` mais plusieurs environnements distants.

**Pour ajouter un autre** d’environnement distant :

1. Sélectionnez l’icône **Teams** dans la barre latérale
2. Sélectionnez **+Teams : Créer un environnement** sous la section Environnement, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="créer":::

Si vous avez plusieurs environnements, vous devez sélectionner un environnement existant pour créer le même environnement. La commande copie le contenu du fichier de `config.<newEnv>.json` et `azure.parameters.<newEnv>.json` de l’environnement existant que vous avez sélectionné dans le nouvel environnement créé.

## <a name="select-target-environment"></a>Sélectionner l’environnement cible

Vous pouvez sélectionner l’environnement cible pour toutes les opérations liées à l’environnement. Le Kit de ressources vous invite et demande un environnement cible lorsque vous avez plusieurs environnements distants, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="ajouter des env":::

## <a name="project-folder-structure"></a>Structure des dossiers du projet

Après avoir créé le projet, vous pouvez afficher les dossiers et fichiers du projet dans la zone explorateur de Visual Studio Code. Outre les codes personnalisés, certains fichiers sont utilisés par le Kit de ressources Teams pour gérer la configuration, l’état et le modèle de l’application. La liste suivante fournit des fichiers et décrit leur relation avec plusieurs environnements.

* `.fx/configs` : configurer les fichiers que l’utilisateur peut personnaliser pour l’application Teams
  * `config.<envName>.json`: fichier de configuration pour chaque environnement 
  * `azure.parameters.<envName>.json`: par fichier de paramètres d’environnement pour l’approvisionnement d’Azure bicep
  * `projectSettings.json` : paramètres de projet globaux , qui s’appliquent à tous les environnements
* `.fx/states`: résultat de provisionnement généré par le Kit de ressources
  * `state.<envName>.json` : fichier de sortie de provisionnement par environnement
  * `<env>.userdata` : données utilisateur sensibles par environnement pour la sortie de provisionnement
* `templates`
  * `appPackage` : fichiers de modèle de manifeste d’application
  * `azure` : fichiers de modèle Bicep

## <a name="customize-resource-provision"></a>Personnaliser l’approvisionnement des ressources

Teams Toolkit vous permet de modifier les fichiers de configuration et les fichiers de modèle pour personnaliser l’approvisionnement des ressources dans chaque environnement.

Le tableau suivant répertorie les scénarios courants pour l’approvisionnement personnalisé des ressources :

| Scénarios | Emplacement| Description |
| --- | --- | --- |
| Personnaliser une ressource Azure | <ul> <li>Fichiers Bicep sous `templates/azure`</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [personnaliser les paramètres et modèles ARM](provision.md#customize-arm-parameters-and-templates) |
| Réutiliser l’application Azure AD existante pour l’application Teams | <ul> <li>`auth`section dans`.fx/config.<envName>.json`</li> </ul> |  [Utiliser une application Azure AD existante pour votre application Teams](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Réutiliser l’application Azure AD existante pour le bot | <ul> <li>`bot`section dans`.fx/config.<envName>.json`</li> </ul> | [Utiliser une application Azure AD existante pour votre bot](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Ignorer l’ajout d’un utilisateur lors de l’approvisionnement de SQL | <ul> <li>`skipAddingSqlUser`Propriété dans`.fx/config.<envName>.json`</li> </ul> | [Ignorer l’ajout d’un utilisateur pour la base de données SQL](provision.md#skip-adding-user-for-sql-database) |
| Personnaliser le manifeste de l’application | <ul> <li>`templates/manifest.template.json`</li> <li>`manifest`section dans`.fx/config.<envName>.json`</li>  </ul> | [Personnaliser le manifeste d’application Teams dans le kit de ressources Teams](TeamsFx-manifest-customization.md) |

## <a name="scenarios"></a>Scénarios

Il existe quatre scénarios pour personnaliser l’approvisionnement des ressources dans différents environnements.
<br>

<br><details>
<summary><b>scénario 1 : personnaliser le nom de l’application Teams pour différents </b> d’environnement</summary>

Vous pouvez définir le nom de l’application Teams sur `myapp(dev)` pour l’environnement par défaut `dev`  et `myapp(staging)` pour l’environnement intermédiaire `staging`.

Effectuez les étapes suivantes pour la personnalisation :

1. Ouvrez le fichier config `.fx/configs/config.dev.json`
2. Mettez à jour la propriété de *manifeste > appName >* court sur `myapp(dev)`

  Les mises à jour de `.fx/configs/config.dev.json` sont les suivantes :

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

3. Créez un environnement et nommez-le `staging` s’il n’existe pas
4. Ouvrez le fichier config `.fx/configs/config.staging.json`
5. Mettez à jour la même propriété `myapp(staging)`
6. Exécutez la commande d’approvisionnement sur `dev` et `staging` environnement pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande d’approvisionnement avec teams Toolkit, consultez [provisionnement](provision.md#provision-using-teams-toolkit)
</details>
<br>


<details>
<summary><b>scénario 2 : personnaliser la description de l’application Teams pour différents environnements</b></summary>

Dans ce scénario, vous allez apprendre à définir différentes descriptions d’application Teams pour les différents environnements :

* Pour l’environnement par défaut `dev`, la description est `my app description for dev`
* Pour l’environnement intermédiaire `staging`, la description est `my app description for staging`

Effectuez les étapes suivantes pour la personnalisation :

1. Ouvrez le fichier config `.fx/configs/config.dev.json`
2. Ajoutez une nouvelle propriété de *description > manifeste >* courte avec une valeur `my app description for dev`

  Les mises à jour de `.fx/configs/config.dev.json` sont les suivantes :

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

3. Créez un environnement et nommez-le `staging` s’il n’existe pas
4. Ouvrez le fichier config `.fx/configs/config.staging.json`
5. Ajoutez la même propriété à `my app description for staging`
6. Ouvrez le modèle de manifeste d’application Teams `templates/appPackage/manifest.template.json`
7. Mettez à jour la `description > short` de propriété pour utiliser la **variable** définie dans configurer des fichiers avec une syntaxe de mustache `{{config.manifest.description.short}}`
  
  Les mises à jour de `manifest.template.json` sont les suivantes :

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

8. Exécutez la commande provision sur `dev` et `staging` environnement pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande d’approvisionnement avec teams Toolkit, consultez [provisionnement](provision.md#provision-using-teams-toolkit)

</details>
<br>

<details>
<summary><b>scénario 3 : Personnaliser la description de l’application Teams pour tous les environnements</b></summary>

Dans ce scénario, vous allez apprendre à définir la description de l’application Teams sur `my app description` pour tous les environnements.

Comme le modèle de manifeste d’application Teams est partagé dans tous les environnements, nous pouvons mettre à jour la valeur de description qu’il contient pour notre cible :

1. Ouvrez le modèle de manifeste d’application Teams `templates/appPackage/manifest.template.json`
2. Mettez à jour la `description > short` de propriété avec **chaîne codée en dur**`my app description`
  
  Les mises à jour de `manifest.template.json` sont les suivantes :

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
 ```
3. Exécutez la commande d’approvisionnement sur **tous** les environnements pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande d’approvisionnement avec teams Toolkit, consultez [provisionnement](provision.md#provision-using-teams-toolkit)
<br></details>
<br>
<details>
<br><summary><b>scénario 4 : personnaliser les ressources Azure pour différents environnements</b></summary>
Vous pouvez personnaliser les ressources Azure pour chaque environnement, par exemple spécifier le nom de la fonction Azure, en modifiant l’environnement correspondant à fx/configs/azure.parameters. {env}.json. le fichier.

Pour plus d’informations sur les fichiers de paramètres et de modèles Bicep, consultez [provisionner des ressources cloud](provision.md)
</details> <br



## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Ajouter d’autres ressources cloud](add-resource.md)
* [Collaborer avec d’autres développeurs sur des projets Teams](TeamsFx-collaboration.md)