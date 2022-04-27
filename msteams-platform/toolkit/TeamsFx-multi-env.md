---
title: Plusieurs environnements TeamsFX dans Teams Shared Computer Toolkit
author: MuyangAmigo
description: À propos du multi-environnement TeamsFX
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 194c31d02424d08080dca981bb9fe6d963d0a416
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073082"
---
# <a name="manage-multiple-environments"></a>Gérer plusieurs environnements

 Teams Shared Computer Toolkit offre un moyen simple de créer et de gérer plusieurs environnements, de provisionner et de déployer des artefacts dans l’environnement cible pour Teams App.

 Vous pouvez effectuer les opérations suivantes avec les différents environnements :

1. **Test avant la production** : vous pouvez configurer plusieurs environnements tels que le développement, le test et la préproduction avant de publier une application Teams dans un environnement de production dans le cycle de vie du développement d’applications modernes

2. **Gérer les comportements d’application dans différents environnements** : vous pouvez configurer différents comportements pour plusieurs environnements, tels que l’activation de la télémétrie dans un environnement de production, mais la désactiver dans l’environnement de développement

## <a name="prerequisite"></a>Conditions préalables

* [Installer la dernière version d’Office](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Vérifiez que Teams projet d’application est ouvert dans Microsoft Visual Studio code.

## <a name="create-a-new-environment"></a>Créer un environnement

Après avoir créé un projet, Teams Shared Computer Toolkit crée par défaut :

* Un `local` environnement pour représenter les configurations d’environnement de machine locale
* Un `dev` environnement pour représenter les configurations d’environnement distant ou cloud

> [!NOTE]
> Chaque projet ne peut avoir qu’un `local` seul environnement, mais plusieurs environnements distants.

**Pour ajouter un autre environnement distant** :

1. Sélectionnez l’icône **Teams** dans la barre latérale
2. Sélectionnez **+Teams : Créez un environnement** dans la section Environnement, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="créer":::

Si vous avez plusieurs environnements, vous devez sélectionner un environnement existant pour créer le même environnement. La commande copie le contenu du fichier de et `azure.parameters.<newEnv>.json` à partir de `config.<newEnv>.json` l’environnement existant que vous avez sélectionné dans le nouvel environnement créé.

## <a name="select-target-environment"></a>Sélectionner l’environnement cible

Vous pouvez sélectionner l’environnement cible pour toutes les opérations liées à l’environnement. Le Shared Computer Toolkit invite et demande un environnement cible lorsque vous avez plusieurs environnements distants, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add env":::

## <a name="project-folder-structure"></a>structure de dossiers Project

Après avoir créé le projet, vous pouvez afficher les dossiers et fichiers du projet dans la zone Explorateur de Visual Studio Code. Outre les codes personnalisés, certains fichiers sont utilisés par Teams Shared Computer Toolkit pour gérer la configuration, l’état et le modèle de l’application. La liste suivante fournit des fichiers et décrit leur relation avec plusieurs environnements.

* `.fx/configs`: configurer des fichiers que l’utilisateur peut personnaliser pour l’application Teams
  * `config.<envName>.json`: fichier de configuration pour chaque environnement 
  * `azure.parameters.<envName>.json`: fichier de paramètres par environnement pour l’approvisionnement Azure bicep
  * `projectSettings.json`: paramètres de projet globaux, qui s’appliquent à tous les environnements
* `.fx/states`: résultat de provisionnement généré par le Shared Computer Toolkit
  * `state.<envName>.json`: fichier de sortie de provisionnement par environnement
  * `<env>.userdata`: données utilisateur sensibles à l’environnement pour la sortie de provisionnement
* `templates`
  * `appPackage`: fichiers de modèle de manifeste d’application
  * `azure`: fichiers de modèle Bicep

## <a name="customize-resource-provision"></a>Personnaliser l’approvisionnement des ressources

Teams Shared Computer Toolkit vous permet de modifier les fichiers de configuration et les fichiers de modèle pour personnaliser l’approvisionnement des ressources dans chaque environnement.

Le tableau suivant répertorie les scénarios courants de provisionnement de ressources personnalisés :

| Scénarios | Emplacement| Description |
| --- | --- | --- |
| Personnaliser une ressource Azure | <ul> <li>Fichiers Bicep sous `templates/azure`</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [Personnaliser les paramètres et modèles ARM](provision.md#customize-arm-parameters-and-templates) |
| Réutiliser l’application Azure AD existante pour Teams application | <ul> <li>`auth` section dans`.fx/config.<envName>.json`</li> </ul> |  [Utiliser une application Azure AD existante pour votre application Teams](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Réutiliser l’application Azure AD existante pour le bot | <ul> <li>`bot` section dans`.fx/config.<envName>.json`</li> </ul> | [Utiliser une application Azure AD existante pour votre bot](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Ignorer l’ajout d’un utilisateur lors de l’approvisionnement de SQL | <ul> <li>`skipAddingSqlUser` propriété dans`.fx/config.<envName>.json`</li> </ul> | [Ignorer l’ajout d’un utilisateur pour SQL base de données](provision.md#skip-adding-user-for-sql-database) |
| Personnaliser le manifeste de l’application | <ul> <li>`templates/manifest.template.json`</li> <li>`manifest` section dans `.fx/config.<envName>.json`</li>  </ul> | [Personnaliser Teams manifeste d’application dans Teams Shared Computer Toolkit](TeamsFx-manifest-customization.md) |

## <a name="scenarios"></a>Scénarios

Il existe quatre scénarios pour personnaliser l’approvisionnement des ressources dans différents environnements.
<br>

<br><details>
<summary><b>Scénario 1 : Personnaliser Teams nom de l’application pour différents environnements</b></summary>

Vous pouvez définir le nom de l’application Teams pour `myapp(dev)` l’environnement `dev` par défaut et `myapp(staging)` pour l’environnement `staging`intermédiaire.

Effectuez les étapes suivantes pour la personnalisation :

1. Ouvrir le fichier de configuration `.fx/configs/config.dev.json`
2. Mettez à jour la propriété du *manifeste > appName > en bref* pour `myapp(dev)`

  Les mises à jour sont `.fx/configs/config.dev.json` les suivantes :

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

3. Créer un environnement et le nommer `staging` s’il n’existe pas
4. Ouvrir le fichier de configuration `.fx/configs/config.staging.json`
5. Mettre à jour la même propriété `myapp(staging)`
6. Exécutez la commande d’approvisionnement sur `dev` et `staging` l’environnement pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande provision avec Teams Shared Computer Toolkit, consultez [provisionner](provision.md#provision-using-teams-toolkit)
</details>
<br>


<details>
<summary><b>Scénario 2 : Personnaliser Teams description de l’application pour différents environnements</b></summary>

Dans ce scénario, vous allez apprendre à définir différentes descriptions d’application Teams pour les différents environnements :

* Pour l’environnement `dev`par défaut, la description est `my app description for dev`
* Pour l’environnement `staging`intermédiaire, la description est `my app description for staging`

Effectuez les étapes suivantes pour la personnalisation :

1. Ouvrir le fichier de configuration `.fx/configs/config.dev.json`
2. Ajouter une nouvelle propriété du *manifeste > description > abrégé* avec valeur `my app description for dev`

  Les mises à jour sont `.fx/configs/config.dev.json` les suivantes :

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

3. Créer un environnement et le nommer `staging` s’il n’existe pas
4. Ouvrir le fichier de configuration `.fx/configs/config.staging.json`
5. Ajouter la même propriété à `my app description for staging`
6. Ouvrir Teams modèle de manifeste d’application`templates/appPackage/manifest.template.json`
7. Mettre à jour la propriété `description > short` pour utiliser la **variable** définie dans configurer des fichiers avec la syntaxe de la moustache `{{config.manifest.description.short}}`
  
  Les mises à jour sont `manifest.template.json` les suivantes :

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

8. Exécutez la commande `dev` de provisionnement et `staging` l’environnement pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande provision avec Teams Shared Computer Toolkit, consultez [provisionner](provision.md#provision-using-teams-toolkit)

</details>
<br>

<details>
<summary><b>Scénario 3 : Personnaliser Teams description de l’application pour tous les environnements</b></summary>

Dans ce scénario, vous allez apprendre à définir la description de Teams application `my app description` pour tous les environnements.

Comme le modèle de manifeste d’application Teams est partagé dans tous les environnements, nous pouvons mettre à jour la valeur de description pour notre cible :

1. Ouvrir Teams modèle de manifeste d’application`templates/appPackage/manifest.template.json`
2. Mettre à jour la propriété `description > short` avec une **chaîne codée en dur** `my app description`
  
  Les mises à jour sont `manifest.template.json` les suivantes :

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
3. Exécutez la commande de **provisionnement sur tous les** environnements pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande provision avec Teams Shared Computer Toolkit, consultez [provisionner](provision.md#provision-using-teams-toolkit)
<br></details>
<br>
<details>
<br><summary><b>Scénario 4 : personnaliser les ressources Azure pour différents environnements</b></summary>
Vous pouvez personnaliser les ressources Azure pour chaque environnement, par exemple spécifier le nom de la fonction Azure, en modifiant l’environnement correspondant à fx/configs/azure.parameters. {env}.json. Fichier.

Pour plus d’informations sur les fichiers de modèles et de paramètres Bicep, consultez [provisionner des ressources](provision.md)
</details> cloud <br



## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Ajouter d’autres ressources cloud](add-resource.md)
* [Collaborer avec d’autres développeurs sur des projets Teams](TeamsFx-collaboration.md)