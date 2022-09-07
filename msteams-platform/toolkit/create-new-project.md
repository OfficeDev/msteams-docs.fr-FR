---
title: Créer une application Teams.
author: zyxiaoyuer
description: Dans ce module, découvrez comment créer une application Teams à l’aide du Kit de ressources Teams
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: e64daa0c3288f97286177e814204404522a6d6b9
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616599"
---
# <a name="create-a-new-teams-project"></a>Créer un projet Teams

Vous pouvez créer un projet Teams en sélectionnant **Créer une application Teams** dans le Kit de ressources Teams. Vous pouvez créer les types d’application suivants dans le Kit de ressources Teams :

| Type d’application | Définition |
| --- | --- |
| Application Teams de base | Les applications Teams de base sont des applications d’extension d’onglet, de bot ou de message que vous pouvez créer et personnaliser en fonction de vos besoins. |
| Application Teams basée sur un scénario | Les applications Teams basées sur des scénarios sont un bot de notification, un bot de commande, un onglet compatible SSO ou une application d’onglet SPFx, qui convient à un scénario particulier. Par exemple, le bot de notification convient uniquement pour envoyer une notification et n’est pas utilisé pour la conversation. |

## <a name="create-a-new-teams-app"></a>Créer une application Teams.

Les étapes de création d’une application Teams sont similaires pour tous les types d’application à l’exception de SPFx et du bot de notification. Les étapes suivantes vous aident à créer une application onglet :

**Pour créer une application**

1. Ouvrez Visual Studio Code.
1. Sélectionnez l’icône du Kit de ressources :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams.
1. Sélectionnez **Créer une application Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-teams-app.png" alt-text="Barre latérale du kit de ressources Teams":::

1. Sélectionnez **Créer une application Teams** pour créer une application à l’aide du Kit de ressources Teams.

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-create-app.png" alt-text="Créer une application":::

1. Pour ce didacticiel, sélectionnez **Tab** comme fonctionnalité de création de votre application.

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-tabapp1.png" alt-text="Sélectionner la fonctionnalité d’application":::

   > [!NOTE]
   > Vous pouvez sélectionner n’importe quel type de fonctionnalité en fonction de vos besoins.

1. Sélectionnez **JavaScript** comme langage de programmation.

    :::image type="content" source="../assets/images/teams-toolkit-v2/select-language-tab.png" alt-text="Capture d’écran montrant comment sélectionner le langage de programmation":::

1. Sélectionnez l’emplacement de l’espace de travail du projet et **sélectionnez Dossier**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder1.png" alt-text="select-folder":::

1. Pour ce didacticiel, entrez `helloworld` le nom de l’application. Ensuite, sélectionnez **Entrée**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/enter-name-tab.png" alt-text="Capture d’écran montrant où entrer le nom de l’application":::

   > [!NOTE]
   > Vous pouvez entrer votre propre nom d’application pour d’autres fonctionnalités et vous assurer d’utiliser uniquement des caractères alphanumériques.

   L’application onglet Teams est créée en quelques secondes.

    :::image type="content" source="../assets/images/teams-toolkit-v2/tap-app-created1.png" alt-text="Capture d’écran montrant l’application créée":::

### <a name="directory-structure-for-different-app-types"></a>Structure de répertoires pour différents types d’applications

Teams Toolkit fournit tous les composants pour la création d’une application. Après avoir créé le projet, vous pouvez afficher les dossiers et fichiers du projet sous **l’Explorateur**.

<br>
<details>
<summary><b>Structure d’annuaires pour l’application Teams de base</b></summary>

Vous avez trois types différents d’application Teams de base et la structure d’annuaires ressemble à tous les types d’applications. L’exemple suivant montre une structure de répertoire d’application onglet Teams de base :

| Nom du dossier | Sommaire |
| --- | --- |
| `.fx/configs` | Fichiers de configuration que l’utilisateur peut personnaliser pour l’application Teams. |
| - `.fx/configs/config.<envName>.json` | Fichier de configuration pour chaque environnement. |
| - `.fx/configs/azure.parameters.<envName>.json` | Fichier de paramètres pour l’approvisionnement Azure BICEP pour chaque environnement. |
| - `.fx/configs/projectSettings.json` | Paramètres de projet globaux qui s’appliquent à tous les environnements. |
| `tabs` | Code de la fonctionnalité Tab nécessaire au moment de l’exécution, comme l’avis de confidentialité, les conditions d’utilisation et les onglets de configuration. |
| - `tabs/src/index.jsx` | Point d’entrée de l’application frontale, où le composant principal de l’application est affiché avec `ReactDOM.render()` |
| - `tabs/src/components/App.jsx` | Code permettant de gérer le routage d’URL dans l’application. Il appelle le [Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) pour établir une communication entre votre application et Teams. |
| - `tabs/src/components/Tab.jsx` | Code pour implémenter l’interface utilisateur de votre application. |
| - `tabs/src/components/TabConfig.jsx` | Code pour implémenter l’interface utilisateur qui configure votre application. |
| `templates/appPackage` | Fichiers de modèle de manifeste d’application et icônes d’application : color.png et outline.png. |
| - `templates/appPackage/manifest.template.json` | Manifeste d’application pour l’exécution de l’application dans un environnement local ou distant.  |
| `templates/azure` | Fichiers de modèle BICEP |

> [!NOTE]
> Si vous disposez d’un bot ou d’une application d’extension de message, des dossiers pertinents sont ajoutés à la structure de répertoires.

Pour en savoir plus sur la structure de répertoires de différents types d’application Teams de base, consultez le tableau suivant :

| Type d’application | Liens |
| --- | --- |
| Pour l’application onglet | [Créer votre première application d’onglet à l’aide de JavaScript](../sbs-gs-javascript.yml) |
| Pour l’application bot | [Créer votre première application de bot à l’aide de JavaScript](../sbs-gs-bot.yml) |
| Pour l’application d’extension de message | [Créer votre première application d’extension de message à l’aide de JavaScript](../sbs-gs-msgext.yml) |

</details>
<br>
<details>
<summary><b>Structure d’annuaires pour l’application Teams basée sur un scénario</b></summary>

Vous disposez de quatre types différents d’applications Teams basées sur des scénarios et la structure d’annuaires est similaire pour tous les types d’applications. L’exemple suivant montre une structure de répertoire d’application Teams basée sur un scénario :

Le nouveau dossier de projet contient le contenu suivant :

| Nom du dossier | Sommaire |
| --- | --- |
| `.fx` | Paramètres, configuration et informations d’environnement au niveau du projet |
| `.vscode` | Fichiers de code VS pour le débogage local |
| `bot` | Code source du bot |
| `templates` | Modèles pour le manifeste d’application Teams et les ressources Azure correspondantes |

Implémentation de notification principale dans le dossier **du bot** et contient :

| Nom de fichier | Sommaire |
| --- | --- |
| `src/adaptiveCards/` | Modèles pour la carte adaptative  |
| `src/internal/` | Code d’initialisation généré pour la fonctionnalité de notification |
| `src/index.*s` | Point d’entrée pour gérer les messages du bot et envoyer des notifications |
| `.gitignore` | Fichier pour exclure des fichiers locaux du projet de bot |
| `package.json` | Fichier de package npm pour le projet de bot |

> [!NOTE]
> Si vous disposez d’un bot de commandes, d’un onglet SSO ou d’une application d’onglet SPFx, des dossiers pertinents sont ajoutés à la structure de répertoires.

Pour en savoir plus sur la structure d’annuaires de différents types d’applications Teams basées sur des scénarios, consultez le tableau suivant :

| Type d’application | Liens |
| --- | --- |
| Pour l’application de bot de notification | [Envoyer une notification à Teams](../sbs-gs-notificationbot.yml) |
| Pour l’application de bot de commande | [Générer un bot de commandes](../sbs-gs-commandbot.yml) |
| Pour l’application d’onglet SPFx | [Créer une application Teams avec SPFx](../sbs-gs-spfx.yml) |

</details>
<br>
<details>
<summary><b>Structure d’annuaires pour l’application multi-fonctionnalités</b></summary>

Vous pouvez ajouter d’autres fonctionnalités à votre application Teams existante à l’aide d’ajouter des fonctionnalités. Par exemple, si vous ajoutez une application bot à l’application onglet existante, Teams Toolkit ajoute le dossier du bot avec des fichiers et du code pertinents.

L’image suivante montre la structure de répertoire de l’application tabulation :

   :::image type="content" source="../assets/images/teams-toolkit-v2/tabapp-directory.png" alt-text="Structure du répertoire de l’application Tab":::

L’image suivante montre la structure de répertoire de l’application onglet avec la fonctionnalité de bot :

   :::image type="content" source="../assets/images/teams-toolkit-v2/tab-app-with-bot-app.png" alt-text="Tab app with bot app directory structure":::

</details>

## <a name="see-also"></a>Voir aussi

* [Créer une application Teams à l’aide de Blazor](../sbs-gs-blazorupdate.yml)
* [Créer une application Teams avec C# ou .NET](../sbs-gs-csharp.yml)
* [Prérequis pour tous les types d’environnement et création de votre application Teams](tools-prerequisites.md)
* [Préparer la création d’applications à l’aide de Microsoft Teams Toolkit](build-environments.md)
