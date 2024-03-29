---
title: Personnaliser le manifeste d’application Teams dans le Kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez comment modifier, afficher un aperçu et personnaliser le manifeste d’application Teams dans un autre environnement.
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: e92e30cf30dd06dbbe3c513a79fe4b7ed7c4bc1a
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833099"
---
# <a name="customize-teams-app-manifest"></a>Personnaliser le manifeste de l’application Teams

Le manifeste de l’application Teams décrit comment votre application s’intègre au produit Microsoft Teams.

::: zone pivot="visual-studio-code"

## <a name="customize-teams-app-manifest-for-visual-studio-code"></a>Personnaliser le manifeste de l’application Teams pour Visual Studio Code

Le manifeste de l’application Teams décrit comment votre application s’intègre au produit Microsoft Teams. Pour plus d’informations sur le manifeste, consultez [Schéma de manifeste d’application pour Teams](../resources/schema/manifest-schema.md). Cette section traite des sujets suivants :

* [Afficher un aperçu du fichier manifeste dans l’environnement local](#preview-manifest-file-in-local-environment)
* [Afficher un aperçu du fichier manifeste dans un environnement distant](#preview-manifest-file-in-remote-environment)
* [Synchroniser les modifications locales avec Developer Portal](#sync-local-changes-to-developer-portal)
* [Personnaliser votre manifeste d’application Teams](#customize-your-teams-app-manifest)
* [Valider le manifeste](#validate-manifest)

Le fichier de modèle de manifeste `manifest.template.json` est disponible sous `templates/appPackage` dossier après la génération de modèles automatiques. Le fichier de modèle avec des espaces réservés et les valeurs réelles sont résolus par teams Toolkit à l’aide de fichiers sous `.fx/configs` et `.fx/states` pour différents environnements.

Pour afficher un aperçu du manifeste avec du contenu réel, le Kit de ressources Teams génère des fichiers manifeste d’aperçu sous le `build/appPackage` dossier :

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

Vous pouvez afficher un aperçu du fichier manifeste dans des environnements locaux et distants.

* [Afficher un aperçu du fichier manifeste dans l’environnement local](#preview-manifest-file-in-local-environment)
* [Afficher un aperçu du fichier manifeste dans un environnement distant](#preview-manifest-file-in-remote-environment)

## <a name="preview-manifest-file-in-local-environment"></a>Afficher un aperçu du fichier manifeste dans l’environnement local

Pour afficher un aperçu du fichier manifeste dans un environnement local, vous pouvez appuyer sur **F5** pour exécuter le débogage local. Il génère les paramètres locaux par défaut pour vous, puis le package d’application et l’aperçu du manifeste sont générés sous le dossier `build/appPackage`.

Vous pouvez également afficher un aperçu du fichier manifeste local par deux méthodes

* En utilisant l’option d’aperçu dans codelens
* À l’aide de **l’option de package de métadonnées Zip Teams**

Les étapes suivantes permettent d’afficher un aperçu du fichier manifeste local à l’aide de l’option d’aperçu dans codelens :

1. Sélectionnez **Aperçu** dans le codelens du `manifest.template.json` fichier.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Capture d’écran montrant l’aperçu dans le codelens du fichier manifeste.":::

1. Sélectionnez **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="La capture d’écran est un exemple montrant la sélection de local dans l’environnement.":::

Les étapes suivantes permettent d’afficher un aperçu du fichier manifeste local à l’aide de l’option **de package de métadonnées Zip Teams** :

1. Sélectionnez `manifest.template.json` fichier.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Capture d’écran montrant la sélection de manifest.template.json.":::

1. Sélectionnez l’icône Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: dans la barre d’outils Visual Studio Code.

1. Sélectionnez **Package de métadonnées Zip Teams** sous **DÉPLOIEMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Capture d’écran montrant la sélection du package de métadonnées Teams zip.":::

1. Sélectionnez **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="La capture d’écran est un exemple montrant la sélection de local dans l’environnement.":::

L’aperçu local s’affiche comme indiqué dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Capture d’écran est un exemple d’affichage de l’aperçu de local.":::

## <a name="preview-manifest-file-in-remote-environment"></a>Afficher un aperçu du fichier manifeste dans un environnement distant

Pour afficher un aperçu du fichier manifeste à l’aide de Visual Studio Code :

* Sélectionnez **Provisionner dans le cloud** sous **DÉVELOPPEMENT** dans l’extension Teams Toolkit
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="Capture d’écran montrant la sélection de l’approvisionnement dans la ressource cloud.":::

Pour afficher un aperçu du fichier manifeste à l’aide de la palette de commandes :

* Déclencher **Teams : provisionner dans le cloud** à partir de la palette de commandes.

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="Capture d’écran montrant l’approvisionnement d’une ressource cloud à l’aide de la palette de commandes.":::

Il génère la configuration de l’application Teams distante et génère le package et le manifeste en préversion sous `build/appPackage` le dossier .

Vous pouvez également afficher un aperçu du fichier manifeste par deux méthodes dans un environnement distant

* En utilisant l’option d’aperçu dans codelens
* À l’aide de **l’option de package de métadonnées Zip Teams**

Les étapes suivantes permettent d’afficher un aperçu du fichier manifeste à l’aide de l’option d’aperçu dans codelens :

1. Sélectionnez **Aperçu** dans le codelens du `manifest.template.json` fichier.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Capture d’écran est un exemple d’affichage de l’aperçu dans le codelens du fichier manifeste.":::

1. Sélectionnez votre environnement.

   > [!NOTE]
   > S’il existe plusieurs environnements, vous devez sélectionner l’environnement que vous souhaitez afficher en aperçu, comme illustré dans l’image :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="La capture d’écran est un exemple montrant l’ajout d’un environnement.":::

Les étapes suivantes permettent d’afficher un aperçu du fichier manifeste à l’aide de l’option **de package de métadonnées Zip Teams** dans un environnement distant :

1. Sélectionnez `manifest.template.json` fichier.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Capture d’écran montrant la sélection de manifest.template.json.":::

1. Sélectionnez l’icône Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: dans la barre d’outils Visual Studio Code.

1. Sélectionnez **Package de métadonnées Zip Teams** sous **DÉPLOIEMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Capture d’écran montrant la sélection du package de métadonnées Teams zip.":::

1. Sélectionnez votre environnement.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="La capture d’écran est un exemple montrant l’ajout d’un environnement.":::

   > [!NOTE]
   > S’il existe plusieurs environnements, vous devez sélectionner l’environnement que vous souhaitez afficher en aperçu, comme illustré dans l’image :

## <a name="sync-local-changes-to-developer-portal"></a>Synchroniser les modifications locales avec Developer Portal

Après avoir aperçu le fichier manifeste, vous pouvez synchroniser vos modifications locales avec le Portail des développeurs des manières suivantes :

> [!NOTE]
> Pour plus d’informations sur le Portail des développeurs, consultez [Portail des développeurs pour Teams](../concepts/build-and-test/teams-developer-portal.md).

1. Déployer le manifeste de l’application Teams.

   Vous pouvez déployer le manifeste d’application Teams de l’une des manières suivantes :

   * Accédez au `manifest.template.json` fichier, puis cliquez avec le bouton droit pour effectuer une sélection `Deploy Teams app manifest` dans le menu contextuel.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="La capture d’écran est un exemple montrant la sélection du manifeste de déploiement de l’application Teams.":::

   * Déclencher `Teams: Deploy Teams app manifest` à partir de la palette de commandes.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="Capture d’écran montrant le déploiement à partir de la palette de commandes.":::

2. Mettez à jour vers la plateforme Teams.

   Vous pouvez effectuer une mise à jour vers la plateforme Teams de l’une des manières suivantes :

   * Sélectionnez **Mettre à jour la plateforme Teams** dans le coin supérieur gauche de `manifest.{env}.json`.

   * Déclencher **Teams : mettre à jour le manifeste vers la plateforme Teams** dans la barre de menus de `manifest.{env}.json`.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Capture d’écran montrant la mise à jour de la plateforme Teams dans la barre de menus du manifeste.":::

Vous pouvez également déclencher **Teams : Mettre à jour le manifeste vers la plateforme Teams à** partir de la palette de commandes :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="Capture d’écran montrant la sélection de Teams : mettre à jour le manifeste vers la plateforme Teams à partir de la palette de commandes.":::

> [!NOTE]
> Déclencher à partir du codelens de l’éditeur ou de la barre de menus met à jour le fichier manifeste actuel vers la plateforme Teams. Le déclencheur à partir de la palette de commandes nécessite la sélection de l’environnement cible.

 Commande CLI :

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> La modification est mise à jour dans le portail de développement. Toutes les mises à jour manuelles dans le portail de développement sont remplacées.

Si le fichier manifeste est obsolète en raison d’une modification du fichier de configuration ou d’un changement de modèle, sélectionnez l’une des actions suivantes :

* **Préversion uniquement** : le fichier manifeste local est remplacé en fonction de la configuration actuelle.
* **Aperçu et mise à jour** : le fichier manifeste local est remplacé en fonction de la configuration actuelle et également mis à jour vers la plateforme Teams.
* **Annuler** : aucune action n’est effectuée.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="Capture d’écran est un exemple de montrant la navigation pour sélectionner les options d’aperçu uniquement, d’aperçu et de mise à jour et d’annulation lorsque le fichier manifeste est obsolète en raison de la modification de la configuration ou du modèle.":::

## <a name="customize-your-teams-app-manifest"></a>Personnaliser votre manifeste d’application Teams

Le kit de ressources Teams se compose des fichiers de modèles de manifeste suivants sous `manifest.template.json` dossier dans les environnements locaux et distants :

* `manifest.template.json`
* `templates/appPackage`

Pendant le débogage local ou l’approvisionnement, Teams Toolkit charge le manifeste à partir de `manifest.template.json`, avec les configurations de `state.{env}.json`, `config.{env}.json`et crée l’application Teams dans [le portail de développement](https://dev.teams.microsoft.com/apps).

### <a name="supported-placeholders-in-manifesttemplatejson"></a>Espaces réservés pris en charge dans manifest.template.json

La liste suivante fournit les espaces réservés pris en charge dans `manifest.template.json`:

* `{{state.xx}}` est un espace réservé prédéfini et sa valeur est résolue par la boîte à outils Teams, définie dans `state.{env}.json`. Veillez à ne pas modifier les valeurs dans `state.{env}.json`
* `{{config.manifest.xx}}` est un espace réservé personnalisé et sa valeur est résolue à partir de `config.{env}.json`

**Pour ajouter un paramètre personnalisé**

1. Ajoutez un paramètre personnalisé comme suit :</br>
   a. Ajoutez un espace réservé dans `manifest.template.json` avec le modèle `{{config.manifest.xx}}`.</br>
   b. Ajoutez une valeur de configuration dans `config.{env}.json`.

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. Vous pouvez accéder au fichier de configuration en sélectionnant l’un des espaces réservés de configuration **Accéder au fichier de configuration** ou **Afficher le fichier d’état** dans `manifest.template.json`.

### <a name="validate-manifest"></a>Valider le manifeste

Lors d’opérations telles que **le package de métadonnées Zip Teams**, Teams Toolkit valide le manifeste par rapport à son schéma. La liste suivante fournit différentes façons de valider le manifeste :

* Dans VSC, déclenchez `Teams: Validate manifest file` à partir de la palette de commandes :

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="Capture d’écran montrant le fichier manifeste de validation Teams à partir de la palette de commandes.":::

* Dans l’interface CLI, utilisez la commande :

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can go to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Screenshot is an example of showing preview values for local and dev environment.":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can go to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Screenshot is an example of showing the selection of an environment.":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Screenshot is an example of showing the preview values for all environments.":::

::: zone-end

::: zone pivot="visual-studio"

## Edit Teams app manifest using Visual Studio

Teams Toolkit in Visual Studio loads manifest from `manifest.template.json` with configurations from `state.{env}.json` and `config.{env}.json` while provisioning and preparing app dependencies. You can also create Microsoft Teams app in [Developer Portal](https://dev.teams.microsoft.com/apps) with the manifest.

After scaffolding, in the manifest template file under `templates/appPackage` folder,
`manifest.template.json` is shared between local and remote environment.

In the manifest template, select **Project** > **Teams Toolkit** > **Open Manifest File**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Screenshot is an example of showing the navigation to open manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png":::

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

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Screenshot is an example showing when you hover over placeholder, can view the values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png":::

* You can also hover over the key besides each placeholder in `manifest.template.json`, and you can see the same values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Screenshot is an example showing when you hover over key beside placeholder can view the same values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png":::

   > [!NOTE]
   > If the environment has not been provisioned, or the Teams app dependencies have not been prepared, it indicates that the values for placeholder have not been generated. Please follow the guidance inside hover to generate corresponding values.

### Preview manifest file

To preview the manifest file, you can sideload for local or deploy for Azure. You can preview the manifest file by performing the following step:

* Select **Project** > **Teams Toolkit** and trigger **Prepare Teams App Dependencies** or **Provision in the Cloud** that generates configuration for local or remote Teams app.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Screenshot is an example of showing preview manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png":::

There are two other ways to upload zip app package before you can preview manifest file:

1. From the list of menu select **Project** > **Teams Toolkit** > **Zip App Package**, and select **For Local** or **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Screenshot is an example of showing the navigation to zip app package for local and azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png":::

1. You can also upload zip app package from Solution Explorer, if you right-click on **MyTeamsApp1** and then select **Teams Toolkit** > **Zip App Package** > **For Local** or **For Azure**.

  > [!NOTE]
  > In this scenario the project name is **MyTeamsApp1**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="Screenshot is an example of showing the list of Teams toolkit menus from solution explorer." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png":::

Teams Toolkit generates the zip app package, and to preview manifest file content you can follow the step below:

* Right-click on **manifest.template.json** under **appPackage** folder, select **Preview Manifest File** > **For Local** or **For Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Screenshot is an example of showing the preview manifest menu for local and azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png":::

This displays the preview of the manifest file in Visual Studio.

### Sync local changes to Developer Portal

After you've previewed the manifest file in Visual Studio, you can now sync the local changes to the Developer Portal. Select **Project** > **Teams Toolkit** > **Update Manifest in Teams Developer Portal**, or context menu from Solution Explorer. You can now preview the manifest file in Developer Portal as a result of syncing the local changes.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Screenshot is an example of showing the navigation to update manifest in Teams developer portal." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png":::

The changes are updated to Teams Developer Portal.

> [!NOTE]
>
> * Select **Overwrite and update** or **Cancel** from the **Warning** dialog box to make any manual updates that can be overwritten in the Developer Portal.
> * When you create a Teams command bot using Visual Studio, two app IDs are registered in Azure Active Directory. You can identify the app IDs in the Developer Portal as **Application client ID** under Basic information and existing **Bot ID** under **App features**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Screenshot is an example of showing the update warning." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png":::

::: zone-end

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)
* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)
* [Deploy Teams app to the cloud using Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
