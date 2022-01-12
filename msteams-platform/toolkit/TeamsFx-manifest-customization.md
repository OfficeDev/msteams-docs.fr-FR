---
title: Personnaliser Teams manifeste d’application dans Teams Shared Computer Toolkit
author: zyxiaoyuer
description: Personnaliser le manifeste de l’application Teams
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d9f2ea49ece8728101a738129e45dd8155887ebc
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768076"
---
# <a name="customize-app-manifest-in-teams-toolkit"></a>Personnaliser le manifeste de l’application dans Teams Shared Computer Toolkit

Teams Shared Computer Toolkit se compose des fichiers de modèles de manifeste suivants sous `templates/appPackage` le dossier :

- `manifest.local.template.json` - application d’équipes de débogage locale
- `manifest.remote.template.json` - partagé dans tous les environnements

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Assurez-vous que Teams projet d’application est ouvert dans VS Code.

Pendant la configuration, Teams Shared Computer Toolkit charge le manifeste à partir de , combiné avec les configurations à partir de et, et crée une application `manifest.remote.template.json` teams dans le portail de `state.{env}.json` `config.{env}.json` [développement](https://dev.teams.microsoft.com/apps).

Pendant le débogage local, Teams Shared Computer Toolkit charge le manifeste à partir de , combiné avec les configurations de , et crée une application teams dans le `manifest.local.template.json` `localSettings.json` portail de [développement.](https://dev.teams.microsoft.com/apps)

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>Espace réservé pris en charge dans manifest.remote.template.json

- `{{state.xx}}`est un espace réservé prédéfiny dont la valeur est résolue par Teams Shared Computer Toolkit, défini dans `state.{env}.json` . Veillez à ne pas modifier les valeurs à l’état. {env}.json.
- `{{config.manifest.xx}}` est un espace réservé personnalisé dont la valeur est résolue à partir de `config.{env}.json` .
  - Vous pouvez ajouter un paramètre personnalisé comme suit :
    - Ajoutez un espace réservé dans manifest.remote.template.json avec le modèle : `{{config.manifest.xx}}`
    - Ajoutez une valeur de config dans la config. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    Outre chaque espace réservé de la `manifest.remote.template.json` config, il existe un `Go to config file` . Vous pouvez accéder au fichier de configuration en le sélectionnant.

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>Espace réservé pris en charge dans manifest.local.template.json

`{{localSettings.xx}}`est un espace réservé prédéfiny dont la valeur est résolue par Teams Shared Computer Toolkit, défini dans `localSettings.json` . Veillez à ne pas modifier les valeurs dans localSettings.json.

 > [!NOTE]
 > Veillez à ne pas personnaliser le manifeste local.

## <a name="see-also"></a>Voir aussi

[Prévisualiser Teams manifeste de l’application dans Teams Shared Computer Toolkit](TeamsFx-manifest-preview.md)
