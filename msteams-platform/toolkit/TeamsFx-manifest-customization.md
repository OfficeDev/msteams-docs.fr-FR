---
title: Personnaliser le manifeste d’application Teams dans le Kit de ressources Teams
author: zyxiaoyuer
description: Personnaliser le manifeste de l’application Teams
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 28a06da170ee52e4340aa3d401d39ad08f58e2ba
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110259"
---
# <a name="customize-app-manifest-in-toolkit"></a>Personnaliser le manifeste d’application dans le Kit de ressources

Le kit de ressources Teams se compose des fichiers de modèles de manifeste suivants sous `manifest.template.json` dossier dans les environnements locaux et distants :

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>Conditions préalables

* [Installer la dernière version d’Office](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Vérifiez que vous avez le projet d’application Teams dans Visual Studio Code.

Pendant le débogage ou l’approvisionnement local, le kit de ressources Teams charge le manifeste à partir de `manifest.template.json` avec les configurations de `state.{env}.json`, `config.{env}.json`, et crée l’application Teams dans [Portail de développement](https://dev.teams.microsoft.com/apps).


## <a name="placeholders-supported-in-manifesttemplatejson"></a>Espaces réservés pris en charge dans manifest.template.json

* `{{state.xx}}` est un espace réservé prédéfini et sa valeur est résolue par la boîte à outils Teams, définie dans `state.{env}.json`. Veillez à ne pas modifier les valeurs dans l’état. {env}.json
* `{{config.manifest.xx}}` est un espace réservé personnalisé et sa valeur est résolue à partir de `config.{env}.json`

  1. Vous pouvez ajouter un paramètre personnalisé comme suit :
      1. Ajoutez un espace réservé dans manifest.template.json avec le modèle : `{{config.manifest.xx}}`
      2. Ajoutez une valeur de configuration dans la configuration. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. Vous pouvez accéder au fichier de configuration en sélectionnant l’un des espaces réservés de configuration **Accéder au fichier de configuration** ou **Afficher le fichier d’état** dans `manifest.template.json`

## <a name="see-also"></a>Voir aussi

[Aperçu du manifeste de l’application Teams dans le kit de ressources Teams](TeamsFx-manifest-preview.md)
