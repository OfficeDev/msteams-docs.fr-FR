---
title: 'TeamsFX : plusieurs environnements dans le Kit de ressources Teams'
author: surbhigupta
description: Dans ce module, découvrez le multi-environnement TeamsFX, par exemple, créez un environnement, sélectionnez l’environnement cible, etc.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 11/29/2021
ms.openlocfilehash: 4a4b67399b2ec7c78fa536b06ee7faa9bb352468
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616950"
---
# <a name="manage-multiple-environments"></a>Gérer plusieurs environnements

 Microsoft Teams Toolkit offre un moyen simple de créer et de gérer plusieurs environnements, de provisionner et de déployer des artefacts dans l’environnement cible de votre application Microsoft Teams.

 Vous pouvez effectuer les opérations suivantes avec plusieurs environnements :

1. **Test avant la production** : vous pouvez configurer plusieurs environnements tels que le développement, le test et la préproduction avant de publier une application Teams dans un environnement de production dans le cycle de vie du développement d’applications modernes.

2. **Gérer les comportements des applications dans différents environnements** : vous pouvez configurer différents comportements d’application pour plusieurs environnements, tels que l’activation de la télémétrie dans un environnement de production.

   > [!NOTE]
   > Vérifiez que la télémétrie est désactivée dans l’environnement de développement.

   > [!TIP]
   > Vérifiez que vous avez le projet d’application Teams dans Visual Studio Code.

## <a name="create-new-environment"></a>Créer un environnement

Une fois que vous avez créé un projet, Teams Toolkit configure par défaut :

* Un `local` environnement pour représenter la configuration de l’environnement de machine locale.
* Un `dev` environnement pour représenter la configuration de l’environnement distant ou cloud.

> [!NOTE]
> Chaque projet ne peut avoir qu’un seul environnement `local` mais plusieurs environnements distants.

**Ajouter un environnement distant** :

1. Sélectionnez le **Kit de ressources Teams** :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="dans la barre d’activité"::: de la barre d’activité.
2. Sélectionnez **+Teams : Créez un environnement** sous la section **ENVIRONNEMENT** , comme illustré dans l’image suivante :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="créer un environnement":::

> [!Note]
> Si vous avez plusieurs environnements, vous devez sélectionner un environnement existant pour créer le même environnement. La commande copie le contenu du fichier de et `azure.parameters.<newEnv>.json` à partir de `config.<newEnv>.json` l’environnement existant que vous avez sélectionné dans le nouvel environnement créé.

## <a name="target-environment"></a>Environnement cible

Vous pouvez sélectionner l’environnement cible. Le Kit de ressources Teams vous invite à sélectionner un environnement cible lorsque vous avez plusieurs environnements distants :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="ajouter des env":::

## <a name="project-folder-structure"></a>Structure des dossiers du projet

Après avoir créé le projet, vous pouvez afficher les dossiers et fichiers du projet sous **l’Explorateur** dans Visual Studio Code. Outre les codes personnalisés, le Kit de ressources Teams utilise certains fichiers pour gérer le `configs`, `states`et `templates` l’application. La liste suivante fournit des fichiers et décrit leur relation avec plusieurs environnements.

* `.fx/configs`: configure les fichiers que l’utilisateur peut personnaliser pour l’application Teams.
  * `config.<envName>.json`: fichier de configuration par environnement.
  * `azure.parameters.<envName>.json`: fichier de paramètres pour l’approvisionnement azure bicep par environnement.
  * `projectSettings.json`: paramètres de projet globaux qui s’appliquent à tous les environnements.
* `.fx/states`: Provisionner le résultat généré par le Kit de ressources Teams.
  * `state.<envName>.json`: provisionnez le fichier de sortie par environnement.
  * `<env>.userdata`: données utilisateur pour la sortie de provisionnement par environnement.
* `templates`
  * `appPackage`: fichiers de modèle de manifeste d’application.
  * `azure`: fichiers de modèle Bicep.

## <a name="customize-resource-provision"></a>Personnaliser l’approvisionnement des ressources

Teams Toolkit vous permet de modifier les fichiers de configuration et les fichiers de modèle pour personnaliser l’approvisionnement des ressources dans chaque environnement.

Le tableau suivant répertorie les scénarios courants pour l’approvisionnement personnalisé des ressources :

| Scénarios | Emplacement| Description |
| --- | --- | --- |
| Personnaliser une ressource Azure |Fichiers Bicep sous `templates/azure` `.fx/azure.parameters.<envName>.json` | [personnaliser les paramètres et modèles ARM](provision.md#customize-arm-template-files) |
| Réutiliser l’application Azure AD existante pour l’application Teams | `auth`section dans`.fx/config.<envName>.json`|  [Utiliser une application Azure AD existante pour votre application Teams](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| Réutiliser l’application Azure AD existante pour le bot |`bot`section dans`.fx/config.<envName>.json`| [Utiliser une application Azure AD existante pour votre bot](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| Ignorer l’ajout d’un utilisateur lors de l’approvisionnement de SQL |`skipAddingSqlUser`Propriété dans`.fx/config.<envName>.json`| [Ignorer l’ajout d’un utilisateur pour la base de données SQL](provision.md#skip-adding-user-for-sql-database) |
| Personnaliser le manifeste de l’application |`templates/manifest.template.json` fichier sous `manifest` la section dans `.fx/config.<envName>.json`| [Aperçu du manifeste d’application dans le Kit de ressources](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>Scénarios

Vous pouvez voir les scénarios suivants pour personnaliser l’approvisionnement des ressources dans différents environnements.
<br>

<br><details>
<summary><b>Scénario 1 : Personnaliser le nom de l’application Teams pour un environnement différent </b></summary>

Vous pouvez définir le nom de l’application Teams pour `myapp(dev)` l’environnement `dev` par défaut et `myapp(staging)` pour l’environnement `staging`intermédiaire.

Étapes de personnalisation :

1. Ouvrez le fichier `.fx/configs/config.dev.json`de configuration.
2. Mettez à jour la propriété de **`manifest`** > **`appName`** > **short** sur **`myapp(dev)`**.

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

3. Vous pouvez créer un environnement et le nommer s’il `staging` n’existe pas.
4. Ouvrez le fichier `.fx/configs/config.staging.json`de configuration.
5. Mettez à jour la même propriété `myapp(staging)`.
6. Vous pouvez maintenant exécuter la commande de provisionnement sur `dev` et `staging` l’environnement pour mettre à jour le nom de l’application dans les environnements distants. Pour exécuter la commande de provisionnement avec le Kit de ressources Teams, consultez [provisionner](provision.md#provision-using-teams-toolkit).

</details>

<details>
<summary><b>scénario 2 : personnaliser la description de l’application Teams pour différents environnements</b></summary>

Vous pouvez définir différentes descriptions d’application Teams pour les différents environnements :

* Pour l’environnement `dev`par défaut, la description est `my app description for dev`.
* Pour l’environnement `staging`intermédiaire, la description est `my app description for staging`.

Étapes de personnalisation :

1. Ouvrez le fichier `.fx/configs/config.dev.json`de configuration.
2. Ajouter une nouvelle propriété de avec la **`manifest`** > **`short`** > **`description`** valeur .**`my app description for dev`**

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

3. Créez un environnement et nommez-le `staging` s’il n’existe pas.
4. Ouvrez le fichier `.fx/configs/config.staging.json`de configuration.
5. Ajoutez la même propriété à `my app description for staging`.
6. Ouvrez le modèle `templates/appPackage/manifest.template.json`de manifeste d’application Teams.
7. Mettez à jour la propriété **`description`** > **`short`** pour utiliser la **variable** définie dans configurer les fichiers avec la syntaxe **`{{config.manifest.description.short}}`** de la moustache.
  
  Les mises à jour sont les `manifest.template.json` suivantes :

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

8. Vous pouvez maintenant exécuter la commande de provisionnement sur `dev` et `staging` l’environnement pour mettre à jour le nom de l’application dans les environnements distants.

</details>

<details>
<summary><b>scénario 3 : Personnaliser la description de l’application Teams pour tous les environnements</b></summary>

Vous pouvez définir la description de l’application `my app description` Teams pour tous les environnements.

Comme le modèle de manifeste d’application Teams est partagé dans tous les environnements, nous pouvons mettre à jour la valeur de description qu’il contient pour notre cible :

1. Ouvrez le modèle `templates/appPackage/manifest.template.json`de manifeste d’application Teams.
2. Mettez à jour la propriété **`description`** > **`short`** avec une chaîne **`my app description`** codée en dur.
  
  Les mises à jour sont les `manifest.template.json` suivantes :

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

3. Vous pouvez maintenant exécuter la commande de provisionnement sur **tout l’environnement** pour mettre à jour le nom de l’application dans les environnements distants.

</details>

<details>
<br><summary><b>Scénario 4 : Personnaliser les ressources Azure pour différents environnements</b></summary>

Vous pouvez personnaliser les ressources Azure pour chaque environnement, par exemple modifier l’environnement correspondant à fx/configs/azure.parameters. Fichier {env}.json pour spécifier le nom de la fonction Azure.

Pour plus d’informations sur les fichiers de modèles et de paramètres Bicep, consultez [provisionner des ressources cloud](provision.md).
</details>
</br>

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Ajouter d’autres ressources cloud](add-resource.md)
* [Collaborer avec d’autres développeurs sur des projets Teams](TeamsFx-collaboration.md)
* [Tester le comportement de l’application dans un environnement différent](test-app-behavior.md)
