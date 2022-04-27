---
title: Aperçu du manifeste d’application Teams dans Teams Shared Computer Toolkit
author: zyxiaoyuer
description: Aperçu du manifeste de l’application Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 57dc719f872d502beded14c30a09d72c27ee74c3
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073280"
---
# <a name="preview-app-manifest-in-toolkit"></a>Aperçu du manifeste de l’application dans Shared Computer Toolkit

Le fichier `manifest.template.json` de modèle de manifeste est disponible sous dossier `templates/appPackage` après la génération de modèles automatiques. Le fichier modèle avec des espaces réservés et les valeurs réelles sont résolus par Teams Shared Computer Toolkit des fichiers sous `.fx/configs` et `.fx/states` pour différents environnements.

## <a name="prerequisite"></a>Conditions préalables

* Installer la [dernière version de Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Vérifiez que Teams projet d’application est ouvert dans Visual Studio code.

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

### <a name="preview-local-manifest-file"></a>Aperçu du fichier manifeste local

Pour afficher un aperçu du fichier manifeste de l’application Teams locale, vous pouvez appuyer sur **F5** pour exécuter le débogage local. Il génère les paramètres locaux par défaut pour vous, puis le package d’application et la préversion des builds de manifeste sous le `build/appPackage` dossier.

Vous pouvez également afficher un aperçu du manifeste local en suivant les étapes suivantes :

1. Sélectionnez **Aperçu** dans le codelens du `manifest.template.json` fichier et sélectionnez **local**
2. Sélectionner **un fichier manifeste d’aperçu** dans la barre de menus du `manifest.template.json` fichier
3. Sélectionnez **zip Teams package de métadonnées** dans Treeview, puis sélectionnez **local**

L’aperçu local s’affiche comme indiqué dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Aperçu":::

### <a name="preview-manifest-in-remote-environment"></a>Afficher un aperçu du manifeste dans un environnement distant

Pour afficher un aperçu du fichier manifeste de l’application Teams distante, sélectionnez **Provisionner dans le cloud dans le** panneau **DÉVELOPPEMENT** de Teams Shared Computer Toolkit extension Treeview, ou déclenchez **Teams : Approvisionner dans le cloud à** partir de la palette de commandes. Il génère la configuration pour l’application Teams distante et génère le package et l’aperçu du manifeste sous le `build/appPackage` dossier.

Vous pouvez également afficher un aperçu du manifeste dans un environnement distant en suivant les étapes suivantes :

1. Sélectionner **Aperçu** dans le codelens du `manifest.template.json` fichier
2. Sélectionner **un fichier manifeste d’aperçu** dans la barre de menus du `manifest.template.json` fichier
3. Sélectionner **le package de métadonnées Zip Teams** dans Treeview
4. Sélectionner votre environnement

S’il existe plusieurs environnements, vous devez sélectionner l’environnement que vous souhaitez afficher en préversion, comme illustré dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Ajouter env":::

## <a name="sync-local-changes-to-developer-portal"></a>Synchroniser les modifications locales dans le portail des développeurs

Après avoir prévisualisé le fichier manifeste, vous pouvez synchroniser vos modifications locales avec le portail des développeurs en suivant les étapes suivantes :

1. Sélectionnez **Mettre à jour pour Teams plateforme** dans le coin supérieur gauche de`manifest.{env}.json`
2. Sélectionnez **Teams : Mettre à jour le manifeste pour Teams plateforme** dans la barre de menus de`manifest.{env}.json`

 Vous pouvez également déclencher **Teams : Mettre à jour le manifeste pour Teams plateforme à** partir de la palette de commandes :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="arborescence":::

> [!NOTE]
> Le déclencheur à partir du codelens de l’éditeur ou du **titre** met à jour le fichier manifeste actuel vers Teams plateforme. Le déclencheur à partir de la palette de commandes nécessite la sélection de l’environnement cible

  

Si le fichier manifeste est obsolète en raison d’un changement de fichier de configuration ou d’un changement de modèle, sélectionnez l’une des actions suivantes :

* **Aperçu uniquement** : le fichier manifeste local est remplacé en fonction de la configuration actuelle
* **Aperçu et mise à jour** : le fichier manifeste local est remplacé en fonction de la configuration actuelle et mis à jour vers Teams plateforme
* **Annuler** : aucune action n’est effectuée

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="Pre":::



> [!NOTE]
> Les modifications sont mises à jour dans le portail de développement. Toutes les mises à jour manuelles dans le portail de développement sont remplacées.

## <a name="see-also"></a>Voir aussi

[Personnaliser Teams manifeste d’application dans Teams Shared Computer Toolkit](TeamsFx-manifest-customization.md)
