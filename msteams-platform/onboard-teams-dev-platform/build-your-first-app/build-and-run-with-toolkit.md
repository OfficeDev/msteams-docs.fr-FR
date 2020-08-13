---
title: Créer et exécuter votre première application teams
author: heath-hamilton
description: Exécutez votre première application Microsoft Teams.
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651984"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Créer et exécuter votre première application Microsoft teams

Vous pouvez accéder directement au développement sur la plateforme Microsoft teams en générant et en exécutant rapidement une application de base.

> [!NOTE]
> Il est utile de posséder des connaissances pratiques sur JavaScript (en particulier REACT) lorsque vous suivez ces didacticiels.

## <a name="set-up-your-development-account"></a>Configurer votre compte de développement

Pour créer des applications pour Teams, vous avez besoin d’un compte teams qui autorise chargement (votre compte peut déjà fournir cette opération). Si ce n’est pas le cas, inscrivez-vous pour un abonnement développeur Microsoft 365 afin de pouvoir obtenir un client test.

1. Vérifiez si vous pouvez chargement des applications dans teams :
    1. Dans le client Teams, sélectionnez **applications**.
    1. Recherchez une option permettant de **Télécharger une application personnalisée**.
1. Si vous avez cette option, vous pouvez commencer à créer. Si ce n’est pas le cas, procédez comme suit :
    1. Inscrivez-vous pour un [abonnement développeur Microsoft 365](../doc-links/prepare-your-o365-tenant.md).
    1. [Activez l’application personnalisée chargement](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) pour votre compte de test.

## <a name="get-your-development-tools"></a>Obtenir vos outils de développement

Vous pouvez créer des applications teams avec vos outils préférés, mais voici ce dont vous avez besoin pour commencer rapidement avec Visual Studio code et Microsoft teams Toolkit.

1. Installez la dernière version de [Visual Studio code](https://code.visualstudio.com/download).
1. Dans Visual Studio code, sélectionnez **Extensions** ![ Visual Studio Toolkit View ](../doc-links/images/vs-code-extensions.png) sur la barre d’activité de gauche et Install the **Microsoft teams Toolkit**.
1. Installez [Node.js](https://nodejs.org/en/).

## <a name="create-an-app-project"></a>Créer un projet d’application

La boîte à outils Microsoft teams peut vous aider à configurer votre premier projet d’application.

1. Dans Visual Studio code, ouvrez la boîte à outils en sélectionnant l’icône Teams. ![icône teams](../doc-links/images/favicon-16x16.png) dans la barre d’activité de gauche.
1. Sélectionnez **créer une nouvelle application teams**.
1. Lorsque vous y êtes invité, entrez un nom pour votre application. Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet sur votre ordinateur local.
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.
1. Activez l’option **onglet personnel** , puis sélectionnez **Terminer** pour configurer votre projet.

![vue ajouter des onglets de la boîte à outils](../doc-links/images/toolkit-add-tabs.PNG)

Une fois terminé, vous disposez des composants d’échafaudage de l’application pour la création d’un onglet personnel.

## <a name="run-your-app"></a>Exécuter votre application

Suivez le `README.md` dans votre projet pour générer, exécuter et déployer votre application dans Teams. En règle générale, ces instructions vous aident à effectuer les opérations suivantes :

* Héberger votre application sur `localhost` .
* [Configurez un tunnel sécurisé avec ngrok](../doc-links/debug.md#locally-hosted) afin que les équipes puissent accéder à votre application. (Installer [ngrok](https://ngrok.com/download).)
* [Chargement votre application](../doc-links/apps-upload.md) dans le client teams à l’aide du `Development.zip` dans le `.publish` dossier.

Une fois que vous avez chargement votre application, elle doit ressembler à ce qui suit dans le client Teams.

![Onglet exemple Hello World](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a>Fichiers de projet d’application importants

Avec votre projet d’application et la configuration de la génération de modèles automatique, prenez le temps de comprendre certains des principaux fichiers que les développeurs d’applications teams utilisent.

### <a name="app-manifest-manifestjson"></a>Manifeste de l’application ( `manifest.json` )

Situé dans l' `.publish` annuaire, le manifeste de l’application est le point de départ de tout projet d’application. Le manifeste définit les attributs fondamentaux de votre application et pointe vers les ressources requises. Lorsque vous installez une application, teams analyse le manifeste pour comprendre comment afficher votre application dans le client.

Dans les didacticiels suivants, vous allez vous concentrer sur les sections du manifeste de l’application pour la création d’onglets de canaux et personnels.

### <a name="package-developmentzip"></a>Package ( `Development.zip` )

Dans l' `.publish` annuaire, vous avez également besoin du package d’application pour [chargement votre application](../../overview.md#how-can-you-share-your-teams-app) dans Teams. Il est également utilisé lors [de la publication dans le catalogue d’applications de votre organisation](../../overview.md#how-can-you-share-your-teams-app) ou [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).

Voici quelques détails sur les fichiers de package d’application :

|Nom|Type|Size|Emplacement du manifeste|Nom de fichier du Toolkit|
|---|---|:---:|:---:|-----|
|**Manifeste de l’application**|`.json`| — | — |`.publish/manifest.json`|
|**Logo couleur**|`.png`|192 &times; 192 pixels|`icon.color`|`.publish/color.png`|
|**Logo de plan**|`.png`|32 &times; 32 pixels|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a>Génération de modèles ( `src` )

Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.

Certains fichiers sont créés, quel que soit le type d’application dont vous disposez. Par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application. Plus important encore, il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../doc-links/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.

Pour plus d’informations sur la génération de modèles automatique dans les didacticiels, consultez la rubrique Création d’onglets personnels et de chaînes.

## <a name="next-step"></a>Étape suivante

🎉 Félicitations ! Vous avez une application teams en cours d’exécution. Cliquez sur le bouton suivant pour découvrir comment ajouter une fonctionnalité de monde réel.

> [!div class="nextstepaction"]
> [Créer un onglet personnel](add-personal-tab.md)
