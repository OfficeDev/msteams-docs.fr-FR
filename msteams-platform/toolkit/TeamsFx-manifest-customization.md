---
title: Personnaliser Teams manifeste d’application dans Teams Shared Computer Toolkit
author: zyxiaoyuer
description: Personnaliser le manifeste de l’application Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: de85674891a53c1e87b43ae1d472daf35716c348
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073539"
---
# <a name="customize-app-manifest-in-toolkit"></a>Personnaliser le manifeste de l’application dans Shared Computer Toolkit

Teams Shared Computer Toolkit se compose des fichiers de modèle de manifeste suivants sous `manifest.template.json` un dossier dans des environnements locaux et distants :

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>Conditions préalables

* [Installer la dernière version d’Office](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> Vérifiez que Teams projet d’application est ouvert dans Visual Studio Code.

Pendant le débogage ou l’approvisionnement local, Teams Shared Computer Toolkit charge le manifeste à partir de `manifest.template.json`, avec les configurations de `state.{env}.json`, `config.{env}.json`et crée l’application Teams dans le [portail de développement](https://dev.teams.microsoft.com/apps).


## <a name="placeholders-supported-in-manifesttemplatejson"></a>Espaces réservés pris en charge dans manifest.template.json

* `{{state.xx}}`est un espace réservé prédéfini et sa valeur est résolue par Teams Shared Computer Toolkit, défini dans `state.{env}.json`. Veillez à ne pas modifier les valeurs dans l’état. {env}.json
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

   2. Vous pouvez accéder au fichier de configuration en sélectionnant l’un des espaces réservés de configuration **Go to config file** or **View the state file** in `manifest.template.json`

## <a name="see-also"></a>Voir aussi

[Aperçu du manifeste d’application Teams dans Teams Shared Computer Toolkit](TeamsFx-manifest-preview.md)
