---
title: Personnaliser le manifeste d’application Teams dans le Kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez comment modifier, afficher un aperçu et personnaliser le manifeste d’application Teams dans l’environnement différent.
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 02bbcc86c769f8ebff87803b6a12bf882e214bf6
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780704"
---
# <a name="customize-teams-app-manifest"></a>Personnaliser le manifeste de l’application Teams

Le manifeste de l’application Teams décrit comment votre application s’intègre au produit Microsoft Teams.

::: zone pivot="visual-studio-code"

## <a name="customize-teams-app-manifest-for-visual-studio-code"></a>Personnaliser le manifeste de l’application Teams pour Visual Studio Code

Le manifeste de l’application Teams décrit comment votre application s’intègre au produit Microsoft Teams. Pour plus d’informations sur le manifeste, consultez [le schéma de manifeste d’application pour Teams](../resources/schema/manifest-schema.md). Cette section traite des sujets suivants :

* [Fichier manifeste d’aperçu dans un environnement local](#preview-manifest-file-in-local-environment)
* [Fichier manifeste d’aperçu dans un environnement distant](#preview-manifest-file-in-remote-environment)
* [Synchroniser les modifications locales avec Developer Portal](#sync-local-changes-to-developer-portal)
* [Personnaliser le manifeste de votre application Teams](#customize-your-teams-app-manifest)
* [Valider le manifeste](#validate-manifest)

Le fichier de modèle de manifeste `manifest.template.json` est disponible sous `templates/appPackage` dossier après la génération de modèles automatiques. Le fichier modèle avec des espaces réservés et les valeurs réelles sont résolus par le Kit de ressources Teams à l’aide de fichiers sous `.fx/configs` et `.fx/states` pour différents environnements.

Pour afficher un aperçu du manifeste avec du contenu réel, le Kit de ressources Teams génère un aperçu des fichiers manifeste sous le `build/appPackage` dossier :

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

## <a name="preview-manifest-file-in-local-environment"></a>Fichier manifeste d’aperçu dans un environnement local

Pour afficher un aperçu du fichier manifeste dans un environnement local, vous pouvez appuyer sur **F5** pour exécuter le débogage local. Il génère les paramètres locaux par défaut pour vous, puis le package d’application et l’aperçu du manifeste sont générés sous le dossier `build/appPackage`.

Vous pouvez également afficher un aperçu du fichier manifeste local par deux méthodes

* En utilisant l’option d’aperçu dans codelens
* En utilisant l’option **de package de métadonnées Zip Teams**

Les étapes suivantes permettent d’afficher un aperçu du fichier manifeste local à l’aide de l’option d’aperçu dans codelens :

1. Sélectionnez **Aperçu** dans le codelens du `manifest.template.json` fichier.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Aperçu":::

1. Sélectionnez **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="Sélectionner l’environnement1":::

Les étapes suivantes permettent d’afficher un aperçu du fichier manifeste local à l’aide de l’option de **package de métadonnées Zip Teams** :

1. Sélectionnez le `manifest.template.json` fichier.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Sélectionnez un manifeste.":::

1. Sélectionnez l’icône du Kit de ressources :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams dans la barre d’outils Visual Studio Code.

1. Sélectionnez **le package de métadonnées Zip Teams** sous **DEPLOYMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Sélectionner le package de métadonnées Teams":::

1. Sélectionnez **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="Sélectionner un environnement":::

L’aperçu local s’affiche comme indiqué dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Aperçu":::

## <a name="preview-manifest-file-in-remote-environment"></a>Fichier manifeste d’aperçu dans un environnement distant

Pour afficher un aperçu du fichier manifeste à l’aide de Visual Studio Code :

* Sélectionner **Provisionner dans le cloud** sous **DÉVELOPPEMENT** dans l’extension Teams Toolkit
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="Provisionner une ressource cloud":::

Pour afficher un aperçu du fichier manifeste à l’aide de la commande palatte :

* Déclencher **Teams : provisionner dans le cloud à** partir de la palette de commandes.

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="Provisionner une ressource cloud à l’aide de la commande palatte":::

Il génère la configuration de l’application Teams distante et génère le package et le manifeste d’aperçu sous le `build/appPackage` dossier.

Vous pouvez également afficher un aperçu du fichier manifeste par deux méthodes dans un environnement distant

* En utilisant l’option d’aperçu dans codelens
* En utilisant l’option **de package de métadonnées Zip Teams**

Les étapes suivantes permettent d’afficher un aperçu du fichier manifeste à l’aide de l’option d’aperçu dans codelens :

1. Sélectionnez **Aperçu** dans le codelens du `manifest.template.json` fichier.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Aperçu":::

1. Sélectionnez votre environnement.

   > [!NOTE]
   > S’il existe plusieurs environnements, vous devez sélectionner l’environnement que vous souhaitez afficher en aperçu, comme illustré dans l’image :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Ajouter env":::

Les étapes suivantes permettent d’afficher un aperçu du fichier manifeste à l’aide de l’option de **package de métadonnées Zip Teams** dans un environnement distant :

1. Sélectionnez le `manifest.template.json` fichier.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Sélectionnez un manifeste.":::

1. Sélectionnez l’icône du Kit de ressources :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams dans la barre d’outils Visual Studio Code.

1. Sélectionnez **le package de métadonnées Zip Teams** sous **DEPLOYMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Sélectionner le package de métadonnées Teams":::

1. Sélectionnez votre environnement.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Ajouter env":::

   > [!NOTE]
   > S’il existe plusieurs environnements, vous devez sélectionner l’environnement que vous souhaitez afficher en aperçu, comme illustré dans l’image :

## <a name="sync-local-changes-to-developer-portal"></a>Synchroniser les modifications locales avec Developer Portal

Après avoir prévisualisé le fichier manifeste, vous pouvez synchroniser vos modifications locales avec le portail des développeurs des manières suivantes :

> [!NOTE]
> Pour plus d’informations sur le portail des développeurs, consultez [Portail des développeurs pour Teams](../concepts/build-and-test/teams-developer-portal.md).

1. Déployer le manifeste de l’application Teams.

   Vous pouvez déployer le manifeste de l’application Teams de l’une des manières suivantes :

   * Accédez au `manifest.template.json` fichier, puis cliquez avec le bouton droit pour le sélectionner `Deploy Teams app manifest` dans le menu contextuel.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="Déployer le manifeste":::

   * Déclencher `Teams: Deploy Teams app manifest` à partir de la palette de commandes.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="Déployer à partir de la palette de commandes":::

2. Mise à jour vers la plateforme Teams.

   Vous pouvez effectuer une mise à jour vers la plateforme Teams de l’une des manières suivantes :

   * Sélectionnez **Mettre à jour vers la plateforme Teams** dans le coin supérieur gauche de `manifest.{env}.json`.

   * Déclencher **Teams : mettre à jour le manifeste vers la plateforme Teams** dans la barre de menus de `manifest.{env}.json`.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Mise à jour vers les équipes":::

Vous pouvez également déclencher **Teams : Mettre à jour le manifeste vers la plateforme Teams à** partir de la palette de commandes :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="arborescence":::

> [!NOTE]
> Le déclencheur à partir du codelens de l’éditeur ou de la barre de menus met à jour le fichier manifeste actuel vers la plateforme Teams. Le déclencheur à partir de la palette de commandes nécessite la sélection de l’environnement cible.

 Commande CLI :

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> La modification est mise à jour vers le portail de développement. Toutes les mises à jour manuelles dans le portail de développement sont remplacées.

Si le fichier manifeste est obsolète en raison d’un changement de fichier de configuration ou d’un changement de modèle, sélectionnez l’une des actions suivantes :

* **Aperçu uniquement** : le fichier manifeste local est remplacé en fonction de la configuration actuelle.
* **Aperçu et mise à jour** : le fichier manifeste local est remplacé en fonction de la configuration actuelle et également mis à jour vers la plateforme Teams.
* **Annuler** : aucune action n’est effectuée.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="Pre":::

## <a name="customize-your-teams-app-manifest"></a>Personnaliser le manifeste de votre application Teams

Le kit de ressources Teams se compose des fichiers de modèles de manifeste suivants sous `manifest.template.json` dossier dans les environnements locaux et distants :

* `manifest.template.json`
* `templates/appPackage`

Pendant le débogage ou l’approvisionnement local, Teams Toolkit charge le manifeste à partir de `manifest.template.json`, avec les configurations de `state.{env}.json`, `config.{env}.json`et crée l’application Teams dans le [portail de développement](https://dev.teams.microsoft.com/apps).

### <a name="supported-placeholders-in-manifesttemplatejson"></a>Espaces réservés pris en charge dans manifest.template.json

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

2. Vous pouvez accéder au fichier de configuration en sélectionnant l’un des espaces réservés de configuration **. Accédez au fichier de configuration** ou **affichez le fichier d’état** dans `manifest.template.json`.

### <a name="validate-manifest"></a>Valider le manifeste

Pendant les opérations telles que le **package de métadonnées Zip Teams**, Teams Toolkit valide le manifeste par rapport à son schéma. La liste suivante fournit différentes façons de valider le manifeste :

* Dans VSC, déclenchez `Teams: Validate manifest file` à partir de la palette de commandes :

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="Valider le fichier":::

* Dans CLI, utilisez la commande :

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Preview values":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Select your environment":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Preview all values":::

::: zone-end

::: zone pivot="visual-studio"

## Edit Teams app manifest using Visual Studio

Teams Toolkit in Visual Studio loads manifest from `manifest.template.json` with configurations from `state.{env}.json` and `config.{env}.json` while provisioning and preparing app dependencies. You can also create Microsoft Teams app in [Developer Portal](https://dev.teams.microsoft.com/apps) with the manifest.

After scaffolding, in the manifest template file under `templates/appPackage` folder,
`manifest.template.json` is shared between local and remote environment.

In the manifest template, select **Project** > **Teams Toolkit** > **Open Manifest File**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Open manifest file" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png":::

### Customize app manifest in Teams Toolkit

There are two types of placeholders in `manifest.template.json`:

* `{{state.xx}}` is pre-defined placeholder, whose value is resolved by Teams Toolkit, defined in `state.{env}.json`. It's recommended to not modify the values in `state.{env}.json`.
* `{{config.manifest.xx}}` is customized placeholder, whose value is resolved from `config.{env}.json`.

You can add a customized parameter by:

* Adding a placeholder in `manifest.template.json` with pattern: `{{config.manifest.xx}}`.
* Adding a config value in `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### Preview app manifest in Teams Toolkit

You can preview values in app manifest in two ways:

* When you hover over the placeholder in `manifest.template.json`, then you can see the values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Hover over placeholder" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png":::

* You can also hover over the key besides each placeholder in `manifest.template.json`, and you can see the same values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Hover over key beside placeholder" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png":::

   > [!NOTE]
   > If the environment has not been provisioned, or the Teams app dependencies have not been prepared, it indicates that the values for placeholder have not been generated. Please follow the guidance inside hover to generate corresponding values.

### Preview manifest file

To preview the manifest file, you can sideload for local or deploy for Azure. You can preview the manifest file by performing the following step:

* Select **Project** > **Teams Toolkit** and trigger **Prepare Teams App Dependencies** or **Provision in the Cloud** that generates configuration for local or remote Teams app.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Preview manifest file" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png":::

There are two other ways to upload zip app package before you can preview manifest file:

1. From the list of menu select **Project** > **Teams Toolkit** > **Zip App Package**, and select **For Local** or **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Zip app package" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png":::

1. You can also upload zip app package from Solution Explorer, if you right-click on **MyTeamsApp1** and then select **Teams Toolkit** > **Zip App Package** > **For Local** or **For Azure**.

  > [!NOTE]
  > In this scenario the project name is **MyTeamsApp1**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="List of Teams Toolkit menus from solution explorer" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png":::

Teams Toolkit generates the zip app package, and to preview manifest file content you can follow the step below:

* Right-click on **manifest.template.json** under **appPackage** folder, select **Preview Manifest File** > **For Local** or **For Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Preview context menu" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png":::

This displays the preview of the manifest file in Visual Studio.

### Sync local changes to Developer Portal

After you've previewed the manifest file in Visual Studio, you can now sync the local changes to the Developer Portal. Select **Project** > **Teams Toolkit** > **Update Manifest in Teams Developer Portal**, or context menu from Solution Explorer. You can now preview the manifest file in Developer Portal as a result of syncing the local changes.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Update manifest in teams developer portal" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png":::

> [!NOTE]
> The changes are updated to Teams Developer Portal. If you have some manual updates in Developer Portal, that can be overwritten. In the **Warning** dialog box you can select **Overwrite and update** or **Cancel**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Update warning" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png":::

::: zone-end

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)

* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)

* [Deploy Teams app to the cloud using Visual Studio](deploy-teams-app.md)
