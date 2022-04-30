---
title: Aperçu du manifeste de l’application Teams dans le kit de ressources Teams
author: zyxiaoyuer
description: Aperçu du manifeste de l’application Teams
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 91bc070d30136ce1f004676172594f26ca37dea5
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111870"
---
# <a name="preview-app-manifest-in-toolkit"></a>Aperçu du manifeste d’application dans le Kit de ressources

Le fichier de modèle de manifeste `manifest.template.json` est disponible sous `templates/appPackage` dossier après la génération de modèles automatiques. Le fichier modèle avec des espaces réservés et les valeurs réelles sont résolus par le Kit de ressources Teams à partir de fichiers sous `.fx/configs` et `.fx/states` pour différents environnements.

## <a name="prerequisite"></a>Conditions préalables

* Installez la [dernière version du kit de ressources Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Vérifiez que vous avez le projet d’application Teams dans Visual Studio Code.

## <a name="preview-manifest"></a>Aperçu du manifeste

Pour afficher un aperçu du manifeste avec du contenu réel, le Kit de ressources Teams génère un aperçu des fichiers manifeste sous le dossier `build/appPackage` :

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>Aperçu du fichier manifeste local

Pour afficher un aperçu du fichier manifeste de l’application Teams locale, vous pouvez appuyer sur **F5** pour exécuter le débogage local. Il génère les paramètres locaux par défaut pour vous, puis le package d’application et l’aperçu du manifeste sont générés sous le dossier `build/appPackage`.

Vous pouvez également afficher un aperçu du manifeste local en suivant les étapes suivantes :

1. Sélectionnez l’**aperçu** dans le codelens de fichier `manifest.template.json`, puis sélectionnez **locale**
2. Sélectionnez **Aperçu du manifeste de fichier** dans la barre de menus de fichier `manifest.template.json`
3. Sélectionnez le **Package de métadonnées Zip Teams** dans Treeview, puis sélectionnez **local**

L’aperçu local s’affiche comme indiqué dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Aperçu":::

### <a name="preview-manifest-in-remote-environment"></a>Afficher un aperçu du manifeste dans un environnement distant

Pour afficher un aperçu du fichier manifeste de l’application Teams distante, sélectionnez **Provisionner dans le cloud** dans **panneau de développement** l’arborescence d’extensions du Kit de ressources Teams, ou déclenchez **Teams : provisionner dans le cloud** à partir de la palette de commandes. Il génère la configuration de l’application Teams distante et génère le package et le manifeste d’aperçu sous le dossier `build/appPackage`.

Vous pouvez également afficher un aperçu du manifeste dans un environnement distant en suivant les étapes suivantes :

1. Sélectionnez l’**aperçu** dans le codelens du fichier `manifest.template.json`
2. Sélectionnez **Aperçu du manifeste de fichier** dans la barre de menus de fichier `manifest.template.json`
3. Sélectionnez le **Package de métadonnées Zip Teams** dans Treeview
4. Sélection de votre environnement

S’il existe plusieurs environnements, vous devez sélectionner l’environnement que vous souhaitez afficher en aperçu, comme illustré dans l’image :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Ajouter env":::

## <a name="sync-local-changes-to-developer-portal"></a>Synchroniser les modifications locales avec Developer Portal

Après avoir prévisualisé le fichier manifeste, vous pouvez synchroniser vos modifications locales avec Developer Portal en suivant les étapes suivantes :

1. Sélectionnez **Mettre à jour vers la plateforme Teams** dans le coin supérieur gauche de `manifest.{env}.json`
2. Sélectionnez **Teams : mettre à jour le manifeste vers la plateforme Teams** dans la barre de menus de `manifest.{env}.json`

 Vous pouvez également déclencher **Teams : mettre à jour le manifeste vers la plateforme Teams** à partir de la palette de commandes :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="arborescence":::

> [!NOTE]
> Déclencher à partir du codelens de l’éditeur ou du **titre** met à jour le fichier manifeste actuel sur la plateforme Teams. Le déclencheur à partir de la palette de commandes nécessite la sélection de l’environnement cible

  

Si le fichier manifeste est obsolète en raison d’une modification du fichier de configuration ou d’un changement de modèle, sélectionnez l’une des actions suivantes :

* **Aperçu uniquement**: le fichier manifeste local est remplacé en fonction de la configuration actuelle
* **aperçu et mise à jour**: le fichier manifeste local est remplacé en fonction de la configuration actuelle et également mis à jour vers la plateforme Teams
* **Annuler**: aucune action n’est effectuée

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="Pre":::



> [!NOTE]
> Les modifications sont mises à jour dans le portail de développement. Toutes les mises à jour manuelles dans le portail de développement sont remplacées.

## <a name="see-also"></a>Voir aussi

[Personnaliser le manifeste d’application Teams dans le kit de ressources Teams](TeamsFx-manifest-customization.md)
