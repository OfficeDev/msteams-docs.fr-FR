---
title: Personnaliser Teams manifeste d’application dans Teams Shared Computer Toolkit
author: zyxiaoyuer
description: Personnaliser Teams manifeste de l’application
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 34b454f63eb900fce2f38748838ce46558835ac5
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228108"
---
# <a name="customize-teams-app-manifest-in-teams-toolkit"></a>Personnaliser Teams manifeste d’application dans Teams Shared Computer Toolkit

Teams Shared Computer Toolkit se compose de deux fichiers de modèles de manifeste sous `templates/appPackage` dossier :

- `manifest.local.template.json` - application d’équipes de débogage locale
- `manifest.remote.template.json` - partagé dans tous les environnements

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Un projet d’application Teams doit déjà être ouvert dans du code VS.

Pendant la mise en service, Teams Shared Computer Toolkit chargera le manifeste à partir `manifest.remote.template.json` de , combiné avec les configurations à partir de et `state.{env}.json` `config.{env}.json` . Il crée ensuite une application Teams dans [le portail de développement](https://dev.teams.microsoft.com/apps) avec ce manifeste.

Pendant le débogage local, Teams Shared Computer Toolkit charge le manifeste à partir `manifest.local.template.json` de , combiné avec les configurations à partir de `localSettings.json` . Il crée ensuite une application Teams dans [le portail de développement](https://dev.teams.microsoft.com/apps) avec ce manifeste.

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>Espace réservé pris en charge dans manifest.remote.template.json

- `{{state.xx}}`est un espace réservé prédéfiny dont la valeur est résolue par Teams Shared Computer Toolkit, défini dans `state.{env}.json` . Vous ne devez pas modifier les valeurs en état. {env}.json.
- `{{config.manifest.xx}}` est un espace réservé personnalisé dont la valeur est résolue à partir de `config.{env}.json` .
  - Vous pouvez ajouter un paramètre personnalisé en suivant :
    - Ajoutez un espace réservé dans manifest.remote.template.json avec le modèle : `{{config.manifest.xx}}`
    - Ajoutez une valeur de config dans la config. {env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    Outre chaque espace réservé de la `manifest.remote.template.json` config, il existe un `Go to config file` bouton. Vous pouvez accéder au fichier de configuration en le sélectionnant comme illustré dans l’image :

    ![go to config file](./images/gotoconfigfile.png)

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>Espace réservé pris en charge dans manifest.local.template.json

`{{localSettings.xx}}`est un espace réservé prédéfiny dont la valeur est résolue par Teams Shared Computer Toolkit, défini dans `localSettings.json` . Vous ne devez pas modifier les valeurs dans localSettings.json.

 > [!NOTE]
 > La personnalisation du manifeste local n’est pas suggérée.

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Prévisualiser Teams manifeste de l’application dans Teams Shared Computer Toolkit](TeamsFx-manifest-preview.md)
