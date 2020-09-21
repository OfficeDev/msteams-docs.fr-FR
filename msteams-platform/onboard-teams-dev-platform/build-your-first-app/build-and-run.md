---
title: Créer et exécuter une application de première équipe
author: heath-hamilton
ms.author: lajanuar
description: Exécutez votre première application Microsoft Teams.
ms.date: 08/31/2020
ms.topic: quickstart
ms.openlocfilehash: 441b70480d9c177e9c6140342df8c9ea29494a29
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964655"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Créer et exécuter votre première application Microsoft teams

Vous pouvez accéder directement au développement sur la plateforme Microsoft teams en créant et en exécutant rapidement un onglet personnel de base.

## <a name="create-your-app-project"></a>Créer votre projet d’application

Utilisez la boîte à outils Microsoft teams dans Visual Studio code pour configurer votre premier projet d’application.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
:::image type="content" source="../doc-links/images/create-teams-app.png" alt-text="image de l’application de création de teams":::
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.
:::image type="content" source="../doc-links/images/choose-tab.png" alt-text="vue de l’image de l’application de création de teams":::
1. Activez l’option **onglet personnel** et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.

## <a name="understand-important-app-project-components"></a>Comprendre les composants importants du projet d’application

Une fois que le kit d’outils configure votre projet, vous disposez des composants permettant de créer un onglet personnel de base pour Teams. Les répertoires et les fichiers du projet sont affichés dans la zone Explorateur de Visual Studio code.

:::image type="content" source="../doc-links/images/app-project-files.png" alt-text="Fichiers de projet d’application dans Visual Studio code.":::

Nous allons prendre le temps de comprendre certains des principaux fichiers que les développeurs d’applications teams utilisent.

### <a name="app-manifest-manifestjson"></a>Manifeste de l’application ( `manifest.json` )

Situé dans l' `.publish` annuaire, le manifeste de l’application est le point de départ de tout projet d’application. Le manifeste définit les attributs fondamentaux de votre application et pointe vers les ressources requises. Lorsque vous installez une application, teams analyse le manifeste pour comprendre comment afficher votre application dans le client.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.

Si vous créez un onglet pendant l’installation, par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application. Il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.

### <a name="app-package-developmentzip"></a>Package d’application ( `Development.zip` )

Situé dans l' `.publish` annuaire, vous avez besoin du package d’application pour [chargement votre application](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) dans Teams. Le package est également utilisé lors [de la publication dans le catalogue d’applications de votre organisation](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) ou [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).

Voici quelques détails sur les fichiers de package d’application :

|Nom|Type|Size|Emplacement du manifeste|Nom de fichier du Toolkit|
|---|---|:---:|:---:|-----|
|**Manifeste de l’application**|`.json`| — | — |`.publish/manifest.json`|
|**Logo couleur**|`.png`|192 &times; 192 pixels|`icon.color`|`.publish/color.png`|
|**Logo de plan**|`.png`|32 &times; 32 pixels|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a>Exécuter votre application

Pour des raisons de temps, vous allez créer et exécuter votre application localement. Les applications teams de teams sont hébergées dans le Cloud.

(Ces informations sont également disponibles dans la boîte à outils `README` .)

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` . Une fois terminé, une **compilation est effectuée.** message dans le terminal.
1. Ouvrez un navigateur et accédez à `https://localhost:3000` la page Web vierge intitulée **Microsoft teams**. (Ne vous inquiétez pas que vous ne pouvez pas voir le contenu sur la page.)<br/>
   :::image type="content" source="../doc-links/images/local-host-tab.png" alt-text="Affichage de l’application dans un navigateur.":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a>Configurer un tunnel sécurisé pour votre application

Votre application est en cours d’exécution sur votre serveur Web local. Pour exécuter votre application dans Teams, vous devez faire en sorte qu’elle soit `localhost` accessible via HTTPS.

Installez [ngrok](https://ngrok.com/download) si vous ne l’avez pas encore fait. Lorsque vous exécutez cet outil, vous créez deux URL globalement disponibles qui pointent vers votre serveur Web local ( `http://localhost:3000` ). Vous avez besoin de l’URL de transfert qui commence par `HTTPS` .

1. Ouvrez un nouveau terminal et exécutez `ngrok http 3000` .
1. Copiez l’URL HTTPs que vous avez fournie (Voir l’exemple ci-dessous).
:::image type="content" source="../doc-links/images/ngrok-running.png" alt-text="image en cours d’exécution ngrok":::
1. Dans votre `.publish` répertoire, ouvrez `Development.env` .
1. Remplacez la `baseUrl0` valeur par l’URL copiée. (Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ba5.ngrok.io` .)

Le manifeste de votre application pointe maintenant vers l’emplacement où vous hébergez l’application.

## <a name="sideload-your-app-in-teams"></a>Chargement de votre application dans teams

Une fois que votre application est en cours d’exécution et accessible via HTTPs, vous êtes prêt à la télécharger vers Teams.

> [!TIP]
> Avant de chargement votre application, vérifiez les problèmes à l’aide de la [fonctionnalité de validation de la boîte à outils](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool). Les erreurs doivent être résolues pour chargement l’application.

1. Connectez-vous au client teams avec votre compte qui autorise l’application chargement. (Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/building-real-world-app.md#set-up-your-development-account).)
1. Sélectionnez **applications**, puis **Télécharger une application personnalisée**.
1. Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` . Affichage modal d’installation.
:::image type="content" source="../doc-links/images/add-teams-app.png" alt-text="Ajouter une application teams":::
1. Sélectionnez **Ajouter** pour installer votre application.
:::image type="content" source="../doc-links/images/tab-running.png" alt-text="Capture d’écran illustrant un exemple Hello, World ! application dans Teams.":::

🎉 Félicitations ! Votre application est en cours d’exécution dans Teams.

## <a name="next-step"></a>Étape suivante

Développez l’onglet personnel que vous venez de créer ou créez un autre type d’application Teams.

> [!div class="nextstepaction"]
> [Ajouter à votre onglet personnel](../build-your-first-app/add-personal-tab.md)
> [!div class="nextstepaction"]
> [Onglet créer un canal](../build-your-first-app/add-channel-tab.md)
> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/add-bot.md)
