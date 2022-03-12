---
title: Prévisualiser Teams manifeste de l’application dans Teams Shared Computer Toolkit
author: zyxiaoyuer
description: Aperçu du manifeste de l’application Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: aa80636a4fdb3c27d66bc08f9d308a009e183570
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453242"
---
# <a name="preview-teams-app-manifest-in-teams-toolkit"></a>Prévisualiser Teams manifeste de l’application dans Teams Shared Computer Toolkit

Après la échafaudage, les fichiers de modèles de manifeste disponibles sous dossier sont les suivants `templates/appPackage` :

* `manifest.local.template.json` - application d’équipes de débogage locale.
* `manifest.remote.template.json` - partagé entre tous les environnements distants.

Les fichiers de modèles constitués d’espaces réservé et les valeurs réelles de Teams Shared Computer Toolkit sont résolues dans les fichiers sous `.fx/configs` et `.fx/states`.

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Assurez-vous que Teams projet d’application est ouvert dans Visual Studio code.

## <a name="preview-manifest"></a>Manifeste d’aperçu

Pour afficher un aperçu du manifeste avec du contenu réel, Teams Shared Computer Toolkit génère des fichiers manifeste d’aperçu sous le `build/appPackage` dossier :

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>Afficher un aperçu du fichier manifeste local

Pour afficher un aperçu du fichier manifeste de l’application teams locale, vous devez appuyer sur **F5** pour exécuter le débogage local. Il génère les paramètres locaux par défaut pour vous, puis le package d’application et le manifeste d’aperçu sont générés sous **le dossier build/appPackage** .

Vous pouvez également afficher un aperçu du manifeste local en suivant les étapes ci-après :

1. **Sélectionnez Aperçu** dans les codelens du **fichier manifest.local.template.json**.
2. **Sélectionnez le fichier manifeste d’aperçu** dans la barre de menus du fichier **manifest.local.template.json**.
3. **Sélectionnez Zip Teams package de métadonnées** dans Treeview et **sélectionnez Local**.
L’aperçu local apparaît comme illustré dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-1.png" alt-text="Aperçu":::

### <a name="preview-manifest-in-remote-environment"></a>Prévisualiser le manifeste dans un environnement distant

Pour prévisualiser le fichier manifeste de l’application Teams distante, sélectionnez Provision **dans le cloud** dans le panneau DÉVELOPPEMENT de Teams Shared Computer Toolkit extension Treeview ou déclenchez **Teams :** mise en service dans le cloud à partir de la palette de commandes. Il génère la configuration de l’application Teams distante et génère le package et le manifeste d’aperçu sous **le dossier build/appPackage** .

Vous pouvez également afficher un aperçu du manifeste dans un environnement distant en suivant les étapes ci-après :

1. **Sélectionnez Aperçu** dans les codelens du **fichier manifest.remote.template.json**.
2. **Sélectionnez le fichier manifeste d’aperçu** dans la barre de menus du **fichier manifest.remote.template.json**.
3. **Sélectionnez Zip Teams package de métadonnées** dans Treeview.
4. Sélectionnez votre environnement.

S’il existe plusieurs environnements, vous devez sélectionner l’environnement que vous souhaitez afficher en aperçu, comme illustré dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Ajouter un env":::

## <a name="sync-local-changes-to-dev-portal"></a>Synchroniser les modifications locales sur le portail de développement

Après avoir prévisualisé le fichier manifeste, vous pouvez synchroniser vos modifications locales avec le portail de développement en suivant les étapes ci-après :

1. **Sélectionnez Mettre à jour Teams plateforme dans** le coin supérieur gauche de`manifest.{env}.json`
2. Select **Teams: Update manifest to Teams platform** at the menu bar of`manifest.{env}.json`

 Vous pouvez également déclencher Teams **: mettre à jour le manifeste sur Teams plateforme à** partir de la palette de commandes

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="arborescence":::

> [!NOTE]
> Le déclencheur à partir du codelens d’éditeur ou du titre met à jour le fichier manifeste actuel Teams plateforme. Le déclencheur à partir de la palette de commandes nécessite la sélection de l’environnement cible.

Si le fichier manifeste est obsolète en raison de la modification du fichier de configuration ou du modèle, assurez-vous de confirmer l’action suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="Pre":::

* **Aperçu uniquement** : le fichier manifeste local sera remplacé en fonction de la configuration actuelle
* **Aperçu et mise à jour** : le fichier manifeste local sera remplacé en fonction de la configuration actuelle et également mis à jour Teams plateforme
* **Annuler :** ne rien faire

> [!NOTE]
> Les modifications seront mises à jour sur le portail dev. Si vous avez des mises à jour manuelles dans le portail dev, elle sera écrasée.

## <a name="see-also"></a>Voir aussi

[Personnaliser Teams manifeste d’application dans Teams Shared Computer Toolkit](TeamsFx-manifest-customization.md)
