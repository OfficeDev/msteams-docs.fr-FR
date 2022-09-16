---
title: Créer une application Teams.
author: zyxiaoyuer
description: Dans ce module, découvrez comment créer une application Teams à l’aide du Kit de ressources Teams
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: e9f1d0cbfcc1de9ced3cd0bac6f26f9218aecd40
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2022
ms.locfileid: "67781139"
---
# <a name="create-a-new-teams-project"></a>Créer un projet Teams

Dans cette section, vous pouvez apprendre à créer un projet Teams à l’aide de Visual Studio Code et de Visual Studio.

::: zone pivot="visual-studio-code"

## <a name="create-a-new-teams-project-for-visual-studio-code"></a>Créer un projet Teams pour Visual Studio Code

Vous pouvez créer un projet Teams en sélectionnant **Créer une application Teams** dans le Kit de ressources Teams. Vous pouvez créer les types d’application suivants dans le Kit de ressources Teams :

| Type d’application | Définition |
| --- | --- |
| Application Teams de base | Les applications Teams de base sont des applications d’extension d’onglet, de bot ou de message que vous pouvez créer et personnaliser en fonction de vos besoins. |
| Application Teams basée sur un scénario | Les applications Teams basées sur des scénarios sont un bot de notification, un bot de commande, un onglet compatible SSO ou une application d’onglet SPFx, qui convient à un scénario particulier. Par exemple, le bot de notification convient uniquement pour envoyer une notification et n’est pas utilisé pour la conversation. |

## <a name="create-a-new-teams-app"></a>Créer une application Teams.

Les étapes de création d’une application Teams sont similaires pour tous les types d’application à l’exception de SPFx et du bot de notification. Les étapes suivantes vous aident à créer une application onglet :

**Pour créer une application**

1. Ouvrez Visual Studio Code.

1. Sélectionnez l’icône du Kit de ressources :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: Teams dans la barre de navigation de gauche.

1. Sélectionnez **Créer une application Teams**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. Vérifiez que **Tab** est sélectionné comme fonctionnalité de votre application.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-capabilities-tabapp.png" alt-text="Sélectionner la fonctionnalité d’application":::

1. Sélectionnez **JavaScript** comme langage de programmation.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-language-tab.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. Sélectionnez **dossier par défaut** pour stocker le dossier racine de votre projet à l’emplacement par défaut.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-default-location.png" alt-text="Sélectionner l’emplacement par défaut":::

   Les étapes suivantes vous guident pour modifier l’emplacement par défaut :

      1. Sélectionnez **Parcourir**.

          :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-browse.png" alt-text="Sélectionner rechercher le stockage":::

      1. Sélectionnez l’emplacement de l’espace de travail du projet.

      1. Sélectionnez **le dossier Sélectionner**.

          :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder.png" alt-text="select-folder pour le stockage":::

1. Entrez `helloworld` le nom de l’application. Veillez à utiliser uniquement des caractères alphanumériques. Ensuite, sélectionnez **Entrée**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/enter-name-tab1.png" alt-text="Capture d’écran montrant où entrer le nom de l’application.":::

1. Par défaut, le projet s’ouvre dans une nouvelle fenêtre dans les 10 secondes. Si vous souhaitez ouvrir dans la fenêtre active, sélectionnez **Ouvrir dans la fenêtre active**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/new-window-notification.png" alt-text="Nouvelle notification de fenêtre":::

   L’application onglet Teams est créée en quelques secondes.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/tap-app-created1.png" alt-text="Capture d’écran montrant l’application créée.":::

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

::: zone-end

::: zone pivot="visual-studio"

## <a name="create-new-teams-app-in-visual-studio"></a>Créer une application Teams dans Visual Studio

Teams Toolkit fournit des modèles d’application Microsoft Teams dans Visual Studio pour créer une application Teams.  Vous pouvez rechercher et sélectionner le modèle d’application Teams dont vous avez besoin lorsque vous créez un projet. Vous pouvez avoir des modèles d’application Teams pour la création :

* Application Tab
* Bot de commandes
* Bot de notification
* Application d’extension de message

## <a name="prerequisites"></a>Prerequisites

| &nbsp; | Installer | Pour l’utilisation... |
| --- | --- | --- |
| &nbsp; | **Obligatoire** | &nbsp; |
| &nbsp; | Visual Studio version 17.3 | Vous pouvez installer l’édition Entreprise de Visual Studio et installer la charge de travail « ASP.NET » et les outils de développement Microsoft Teams. |
| &nbsp; | Toolkit Teams | Extension Visual Studio qui crée une structure de projet pour votre application. Utilisez la dernière version. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams pour collaborer avec toutes les personnes avec lesquelles vous travaillez via les applications pour les conversations, les réunions, les appels, le tout au même endroit. |
 | &nbsp; | [Préparer votre client Microsoft Office 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Accès au compte Teams avec les autorisations appropriées pour installer une application. |

## <a name="create-a-new-teams-app"></a>Créer une application Teams.

Les étapes de création d’une application Teams sont similaires pour tous les types d’application, à l’exception du bot de notification. Les étapes suivantes vous aident à créer une application onglet :

1. Ouvrez Visual Studio.
1. Créez un projet à l’aide de l’une des deux options suivantes.

     :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1_1.png" alt-text="Créer un projet avec du code à partir de la prise en main":::

    * Sélectionnez **Créer un projet** sous **Prise en main** pour choisir le modèle de projet avec la génération de modèles de code.
    * Sélectionnez **Continuer sans code** pour créer un projet sans structure de code, puis sélectionnez **Fichier** > **nouveau** > **projet** dans Visual Studio.

        :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2_1.png" alt-text="Créer un projet à partir du menu fichier":::

   La fenêtre **Créer un projet** s’affiche.  

1. Entrez les équipes dans la zone de recherche et dans la liste, sélectionnez **Application Microsoft Teams** , puis **Suivant**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/visual-studio.png" alt-text="Rechercher et choisir l’application Microsoft Teams":::

   La fenêtre **Configurer votre nouveau projet** s’affiche.

     :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name_1.png" alt-text="Nommer votre application":::

    1. Entrez un nom approprié pour votre projet.

         > [!NOTE]
         > Le nom du projet que vous entrez est également automatiquement renseigné dans le nom de la **solution** . Si vous le souhaitez, vous pouvez modifier le nom de la solution sans affecter le nom du projet.

    1. Sélectionnez le chemin d’accès au dossier dans lequel vous souhaitez créer l’espace de travail du projet.
    1. Entrez un autre nom de solution, si vous le souhaitez.
    1. Si vous le souhaitez, cochez l’option permettant d’enregistrer le projet et la solution dans le même dossier. Pour ce didacticiel, vous n’avez pas besoin de cette option.
    1. Sélectionnez **Créer**.

   La fenêtre **Créer une application Teams** s’affiche.

1. Dans ce didacticiel, **Tab** est sélectionné pour créer une application Teams, puis **sélectionnez Créer**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type_3.png" alt-text="Sélectionner le type d’application Teams":::

   > [!NOTE]
   > Vous pouvez sélectionner le type d’application Teams requis pour votre projet.

   La **Začínáme** avec la fenêtre **Bienvenue dans le Kit de ressources Teams** s’affiche.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-getting-started-page.png" alt-text="Sélectionnez le kit de ressources teams Začínáme":::

### <a name="directory-structure"></a>Structure de répertoires

Teams Toolkit fournit tous les composants pour la création d’une application. Après avoir créé le projet, vous pouvez afficher les dossiers et fichiers du projet sous l’Explorateur.

* **Structure d’annuaires pour l’application Teams de base**

  :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project-solution-explorer_1.png" alt-text="Sélectionnez l’onglet Průzkumník řešení boîte à outils Teams":::

* **Structure d’annuaires pour l’application Teams basée sur un scénario**

  :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project-solution-explorer.png" alt-text="Sélectionnez le kit de ressources teams Průzkumník řešení":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Modèles d’application Teams dans le Kit de ressources Teams pour Visual Studio

Vous pouvez voir les modèles d’application Teams déjà renseignés dans le Kit de ressources Teams pour différents types d’application Teams. Le tableau suivant répertorie tous les modèles disponibles :

|Modèle d’application Teams  |Description  |
|---------|---------|
|Notification Bot     |L’application Bot de notification peut envoyer une notification à votre client Teams. Il existe plusieurs façons de déclencher la notification. Par exemple, déclenchez la notification par requête HTTP ou par heure. Vous pouvez également sélectionner une notification déclenchée en fonction de votre scénario métier.         |
|Bot de commandes     |Les utilisateurs peuvent taper une commande pour interagir avec le bot à l’aide de l’application Command Bot.         |
|Tab     |L’application Tab affiche une page web dans Teams et active l’authentification unique à l’aide d’un compte Teams.         |
|Message Extension     |L’application d’extension de message implémente des fonctionnalités simples telles que la création d’une carte adaptative, la recherche de packages De la pépite, le déploiement de liens pour le domaine « dev.botframework.com ».         |

> [!NOTE]
> Une fois le projet créé, le Kit de ressources Teams ouvre automatiquement la fenêtre **Prise en main** . Vous pouvez maintenant voir les instructions de la fenêtre **Prise en main** et découvrir les différentes fonctionnalités du Kit de ressources Teams.

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Créer une application Teams à l’aide de Blazor](../sbs-gs-blazorupdate.yml)
* [Créer une application Teams avec C# ou .NET](../sbs-gs-csharp.yml)
* [Prérequis pour tous les types d’environnement et création de votre application Teams](tools-prerequisites.md)
* [Préparer la création d’applications à l’aide de Microsoft Teams Toolkit](build-environments.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
