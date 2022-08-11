---
title: Manifeste d’application Teams dans le Kit de ressources Teams pour Visual Studio
author: surbhigupta
description: Dans ce module, découvrez comment modifier, afficher un aperçu et personnaliser le manifeste d’application Teams dans l’environnement différent pour Visual Studio.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: c391df383c97638d3c8ff5944afab75db2400580
ms.sourcegitcommit: 52a11f7614c43172bc2d57401a60d569db5310a9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2022
ms.locfileid: "67291652"
---
# <a name="edit-teams-app-manifest-using-visual-studio"></a>Modifier le manifeste de l’application Teams à l’aide de Visual Studio

Le Kit de ressources Teams dans Visual Studio charge le manifeste à partir de configurations à partir `manifest.template.json` de `state.{env}.json` et `config.{env}.json` pendant l’approvisionnement et la préparation des dépendances d’application. Vous pouvez également créer une application Microsoft Teams dans le [portail des développeurs](https://dev.teams.microsoft.com/apps) avec le manifeste.

Après la génération de modèles automatiques, dans le fichier de modèle de manifeste sous `templates/appPackage` le dossier, `manifest.template.json` est partagé entre l’environnement local et l’environnement distant.

Dans le modèle de manifeste, sélectionnez Boîte **à outils** >  **Project** >  Teams **Ouvrir le fichier manifeste**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Ouvrir le fichier manifeste":::

### <a name="customize-app-manifest-in-teams-toolkit"></a>Personnaliser le manifeste d’application dans le Kit de ressources Teams

Il existe deux types d’espaces réservés dans `manifest.template.json`:

- `{{state.xx}}` est un espace réservé prédéfini, dont la valeur est résolue par le Kit de ressources Teams, définie dans `state.{env}.json`. Il est recommandé de ne pas modifier les valeurs dans `state.{env}.json`.
- `{{config.manifest.xx}}` est un espace réservé personnalisé dont la valeur est résolue à partir de `config.{env}.json`.

Vous pouvez ajouter un paramètre personnalisé en :

- Ajout d’un espace réservé avec `manifest.template.json` le modèle : `{{config.manifest.xx}}`.
- Ajout d’une valeur de configuration dans `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### <a name="preview-app-manifest-in-teams-toolkit"></a>Manifeste d’application en préversion dans le Kit de ressources Teams

Vous pouvez afficher un aperçu des valeurs dans le manifeste de l’application de deux manières :

- Lorsque vous pointez sur l’espace réservé dans `manifest.template.json`, les valeurs de **développement** et d’environnement **local** sont visibles.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Pointer sur l’espace réservé":::

- Vous pouvez également pointer sur la clé en plus de chaque espace réservé dans `manifest.template.json`, les mêmes valeurs pour le **développement** et l’environnement **local** peuvent être vues.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Pointer sur la touche à côté de l’espace réservé":::

   > [!NOTE]
   > Si l’environnement n’a pas été approvisionné ou que les dépendances de l’application Teams n’ont pas été préparées, cela indique que les valeurs de l’espace réservé n’ont pas été générées. Suivez les instructions à l’intérieur du pointage pour générer les valeurs correspondantes.

### <a name="preview-manifest-file"></a>Fichier manifeste d’aperçu

Vous pouvez afficher un aperçu du fichier manifeste en effectuant les étapes suivantes :

- Sélectionnez le menu Du **kit de ressources** **Project** >  Teams et **déclenchez Préparer les dépendances d’application Teams** ou **l’approvisionnement dans le cloud** qui génère la configuration pour l’application Teams locale ou distante.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Fichier manifeste d’aperçu":::

- Pour afficher un aperçu du manifeste avec du contenu réel, teams toolkit génère les fichiers manifeste en préversion, puis cliquez avec le bouton droit sur **manifest.template.json** sous le dossier **appPackage** . Sélectionnez **l’aperçu du fichier** >  manifeste **pour local** ou **pour Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Menu contextuel d’aperçu":::

Il existe deux autres façons d’afficher un aperçu du fichier manifeste :

- Sélectionnez **Project** > **Teams Toolkit** > **Zip App Package** , puis **For Local** ou **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Package d’application zip":::

- Vous pouvez également voir la même liste de menus sous Project > Teams Toolkit, si vous cliquez avec le bouton droit sur le nom de votre projet, puis sélectionnez **Teams Toolkit** sous **Explorateur de solutions**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="Liste des menus du Kit de ressources Teams de l’Explorateur de solutions":::

    > [!NOTE]
    >Dans ce scénario, le nom du projet est **MyTeamsApp1**.

### <a name="sync-local-changes-to-developer-portal"></a>Synchroniser les modifications locales avec Developer Portal

Vos modifications locales peuvent être synchronisées avec le portail des développeurs, une fois que vous avez prévisualisé le fichier manifeste. Sélectionnez le manifeste de mise à jour du **kit de ressources** >  **Project** >  Teams **dans le portail des développeurs Teams** ou le menu contextuel dans Explorateur de solutions.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Mettre à jour le manifeste dans le portail des développeurs Teams":::

> [!NOTE]
> Les modifications sont mises à jour vers le portail des développeurs Teams. Si vous avez des mises à jour manuelles dans le portail des développeurs, vous pouvez les remplacer. Dans la boîte de dialogue **Avertissement** , vous pouvez sélectionner **Remplacer et mettre à jour** ou **Annuler**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Avertissement de mise à jour":::

## <a name="see-also"></a>Voir aussi

- [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
- [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
