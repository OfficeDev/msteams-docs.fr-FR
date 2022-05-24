---
title: manifeste d’application Teams dans Teams Toolkit
author: zyxiaoyuer
description: manifeste d’application Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: ebb6f7e66f09c3ebbc3834577f924f5a34bb8583
ms.sourcegitcommit: 264d3cc84d6eec4ab025cf86a7a6f4865f1aed07
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2022
ms.locfileid: "65653854"
---
# <a name="edit-teams-app-manifest"></a>Modifier Teams manifeste d’application

Le fichier de modèle de manifeste `manifest.template.json` est disponible sous `templates/appPackage` dossier après la génération de modèles automatiques. Le fichier de modèle avec des espaces réservés et les valeurs réelles sont résolus par Teams Toolkit à l’aide de fichiers sous `.fx/configs` et `.fx/states` pour différents environnements.

**Pour afficher un aperçu du manifeste avec du contenu réel, Teams Toolkit génère des fichiers manifeste en préversion sous le `build/appPackage` dossier** :

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

Vous pouvez afficher un aperçu du fichier manifeste dans des environnements locaux et distants.

* [Fichier manifeste d’aperçu dans un environnement local](#preview-manifest-file-in-local-environment)
* [Fichier manifeste d’aperçu dans un environnement distant](#preview-manifest-file-in-remote-environment)
 
### <a name="preview-manifest-file-in-local-environment"></a>Fichier manifeste d’aperçu dans un environnement local

Pour afficher un aperçu du fichier manifeste dans un environnement local, vous pouvez appuyer sur **F5** pour exécuter le débogage local. Il génère les paramètres locaux par défaut pour vous, puis le package d’application et l’aperçu du manifeste sont générés sous le dossier `build/appPackage`.

Vous pouvez également afficher un aperçu du fichier manifeste local en suivant les étapes suivantes :

1. Sélectionnez **Aperçu** dans le codelens du `manifest.template.json` fichier, puis sélectionnez **local**.
2. Sélectionnez **Le fichier manifeste d’aperçu** dans la barre de menus du `manifest.template.json` fichier.
3. Sélectionnez **Zip Teams package de métadonnées** dans Treeview, puis sélectionnez **local**.

L’aperçu local s’affiche comme indiqué dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Aperçu":::

### <a name="preview-manifest-file-in-remote-environment"></a>Fichier manifeste d’aperçu dans un environnement distant

**Pour afficher un aperçu du fichier manifeste dans un environnement distant**

* Sélectionnez **Provisionner dans le cloud** sous **DÉVELOPPEMENT** dans Teams extension toolkit ou 
* Déclencheur **Teams : provisionnement dans le cloud à** partir de la palette de commandes.
 
Il génère la configuration de l’application Teams distante et génère un package et un manifeste d’aperçu sous le `build/appPackage` dossier.

Vous pouvez également afficher un aperçu du fichier manifeste dans un environnement distant en procédant comme suit :

1. Sélectionnez **Aperçu** dans le codelens du `manifest.template.json` fichier.
2. Sélectionnez **Le fichier manifeste d’aperçu** dans la barre de menus du `manifest.template.json` fichier.
3. Sélectionnez **Zip Teams package de métadonnées** dans Treeview.
4. Sélectionnez votre environnement.

> [!NOTE]
> S’il existe plusieurs environnements, vous devez sélectionner l’environnement que vous souhaitez afficher en aperçu, comme illustré dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Ajouter env":::

## <a name="sync-local-changes-to-dev-portal"></a>Synchroniser les modifications locales dans le portail de développement

Après avoir prévisualisé le fichier manifeste, vous pouvez synchroniser vos modifications locales avec le portail de développement des manières suivantes :

1. Déployer Teams manifeste d’application

   Vous pouvez déployer Teams manifeste d’application de l’une des manières suivantes :

   * Accédez au `manifest.template.json` fichier, puis cliquez avec le bouton droit pour sélectionner `Deploy Teams app manifest` dans le menu contextuel

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="Déployer le manifeste":::

   * Déclencher `Teams: Deploy Teams app manifest` à partir de la palette de commandes

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="Déployer à partir de la palette de commandes":::

2. Mettre à jour vers la plateforme Teams

   Vous pouvez effectuer une mise à jour vers Teams plateforme de l’une des manières suivantes :

   * Sélectionnez **Mettre à jour pour Teams plateforme** dans le coin supérieur gauche de`manifest.{env}.json`

   * Déclencheur **Teams : mettre à jour le manifeste pour Teams plateforme** dans la barre de menus de`manifest.{env}.json`

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Mise à jour vers les équipes":::

Vous pouvez également déclencher **Teams : Mettre à jour le manifeste pour Teams plateforme à** partir de la palette de commandes :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="arborescence":::

> [!NOTE]
> Le déclencheur à partir du codelens de l’éditeur ou de la barre de menus met à jour le fichier manifeste actuel vers Teams plateforme. Le déclencheur à partir de la palette de commandes nécessite la sélection de l’environnement cible.

 Commande CLI :

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> La modification est mise à jour vers le portail de développement. Toutes les mises à jour manuelles dans le portail de développement sont remplacées.

Si le fichier manifeste est obsolète en raison d’une modification du fichier de configuration ou d’un changement de modèle, sélectionnez l’une des actions suivantes :

* **Aperçu uniquement**: le fichier manifeste local est remplacé en fonction de la configuration actuelle
* **aperçu et mise à jour**: le fichier manifeste local est remplacé en fonction de la configuration actuelle et également mis à jour vers la plateforme Teams
* **Annuler**: aucune action n’est effectuée

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="Pre" border="true":::


## <a name="customize-teams-app-manifest"></a>Personnaliser le manifeste de l’application Teams

Le kit de ressources Teams se compose des fichiers de modèles de manifeste suivants sous `manifest.template.json` dossier dans les environnements locaux et distants :

* `manifest.template.json`
* `templates/appPackage`


Pendant le débogage ou l’approvisionnement local, Teams Toolkit charge le manifeste à partir de `manifest.template.json`, avec les configurations de `state.{env}.json`, `config.{env}.json`et crée Teams application dans le [portail de développement](https://dev.teams.microsoft.com/apps).

## <a name="supported-placeholders-in-manifesttemplatejson"></a>Espaces réservés pris en charge dans manifest.template.json

La liste suivante fournit les espaces réservés pris en charge dans `manifest.template.json`:

* `{{state.xx}}` est un espace réservé prédéfini et sa valeur est résolue par la boîte à outils Teams, définie dans `state.{env}.json`. Veillez à ne pas modifier les valeurs dans `state.{env}.json`
* `{{config.manifest.xx}}` est un espace réservé personnalisé et sa valeur est résolue à partir de `config.{env}.json`

**Pour ajouter un paramètre personnalisé**

1. Ajoutez un paramètre personnalisé comme suit :</br>
   a. Ajoutez un espace réservé avec `manifest.template.json` le modèle `{{config.manifest.xx}}`.</br>
   b. Ajoutez une valeur de configuration dans `config.{env}.json`.

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. Vous pouvez accéder au fichier de configuration en sélectionnant l’un des espaces réservés de configuration **Go to config file** or **View the state file** in `manifest.template.json`.

### <a name="validate-manifest"></a>Valider le manifeste

Lors d’opérations telles que **zip Teams package de métadonnées**, Teams Toolkit valide le manifeste par rapport à son schéma. La liste suivante fournit différentes façons de valider le manifeste :

* Dans VSC, déclenchez `Teams: Validate manifest file` à partir de la palette de commandes :

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="Valider le fichier":::

* Dans CLI, utilisez la commande :

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## Codelenses and hovers

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Preview values":::

> [!NOTE] 
> Provision the environment or execute local debug to generate values for placeholders. 

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Select your environment":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Preview all values":::


## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md) 
