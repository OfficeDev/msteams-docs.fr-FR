---
title: Créer et exécuter un « Hello, World ! » Application Teams
author: heath-hamilton
description: Créez et exécutez votre première application Microsoft Teams, un onglet personnel qui affiche « Hello, World ! ».
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 244a899670f71b9446c8c3d3e404c9fd7c7b510c
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237831"
---
# <a name="build-a-hello-world-teams-app"></a>Créer un « Hello, World! » Application Teams

Vous pouvez accéder directement au développement de la plateforme Microsoft teams en créant un onglet personnel qui affiche « Hello, World ! ».

## <a name="1-create-your-app-project"></a>1. créer votre projet d’application

Utilisez la boîte à outils Microsoft teams dans Visual Studio code pour configurer votre premier projet d’application.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran indiquant comment configurer votre projet d’application avec Visual Studio code teams Toolkit.":::
1. Activez l’option **onglet personnel** et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.

## <a name="2-understand-important-app-project-components"></a>2. comprendre les composants importants du projet d’application

Une fois que le kit d’outils configure votre projet, vous disposez des composants permettant de créer un onglet personnel de base pour Teams. Les répertoires et les fichiers du projet sont affichés dans la zone Explorateur de Visual Studio code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran illustrant les fichiers de projet d’application pour un onglet personnel dans Visual Studio code.":::

Nous allons prendre quelques instants pour comprendre quelques-uns des principaux fichiers que les développeurs d’applications teams utilisent.

### <a name="app-manifest-manifestjson"></a>Manifeste de l’application ( `manifest.json` )

Situé dans l' `.publish` annuaire, le manifeste de l’application est le point de départ de tout projet d’application. Le manifeste définit les attributs fondamentaux de votre application et pointe vers les ressources requises. Lorsque vous installez une application, teams analyse le manifeste pour comprendre comment afficher votre application dans le client.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.

Si vous créez un onglet pendant l’installation, par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application. Il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.

### <a name="app-package-developmentzip"></a>Package d’application ( `Development.zip` )

Situé dans l' `.publish` annuaire, vous avez besoin du package d’application pour [chargement votre application](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) dans Teams. Le package est également utilisé lors [de la publication dans le catalogue d’applications de votre organisation](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) ou [AppSource](../concepts/deploy-and-publish/appsource/publish.md).

Voici quelques détails sur les fichiers de package d’application :

|Nom|Type|Size|Emplacement du manifeste|Nom de fichier du Toolkit|
|---|---|:---:|:---:|-----|
|**Manifeste de l’application**|`.json`| — | — |`.publish/manifest.json`|
|**Logo couleur**|`.png`|192 &times; 192 pixels|`icon.color`|`.publish/color.png`|
|**Logo de plan**|`.png`|32 &times; 32 pixels|`icon.outline`|`.publish/outline.png`|

## <a name="3-run-your-app"></a>3. exécuter votre application

Pour des raisons de temps, vous allez créer et exécuter votre application localement.

(Ces informations sont également disponibles dans la boîte à outils `README` .)

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` . Une fois terminé, une **compilation est effectuée.** message dans le terminal.
1. Ouvrez un navigateur et accédez à `https://localhost:3000` la page Web vierge intitulée **Microsoft teams**. (Ne vous inquiétez pas que vous ne pouvez pas voir le contenu sur la page.)<br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Capture d’écran illustrant l’apparence de votre application en cours d’exécution dans un navigateur.":::

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a>4. configurer un tunnel sécurisé pour votre application

Votre application est en cours d’exécution sur votre serveur Web local. Pour exécuter votre application dans Teams, vous devez faire en sorte qu’elle soit `localhost` accessible via HTTPS.

Installez [ngrok](https://ngrok.com/download) si vous ne l’avez pas encore fait. Lorsque vous exécutez cet outil, vous créez deux URL globalement disponibles qui pointent vers votre serveur Web local ( `http://localhost:3000` ). Vous avez besoin de l’URL de transfert qui commence par `HTTPS` .

1. Ouvrez un nouveau terminal et exécutez `ngrok http 3000` .
1. Copiez l’URL HTTPs que vous avez fournie (Voir l’exemple ci-dessous).
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Capture d’écran illustrant un terminal avec ngrok en cours d’exécution.":::
1. Dans votre `.publish` répertoire, ouvrez `Development.env` .
1. Remplacez la `baseUrl0` valeur par l’URL copiée. (Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ba5.ngrok.io` .)

Le manifeste de votre application pointe maintenant vers l’emplacement où vous hébergez l’application.

## <a name="5-sideload-your-app-in-teams"></a>5. chargement de votre application dans teams

Une fois que votre application est en cours d’exécution et accessible via HTTPs, vous êtes prêt à la télécharger vers Teams.

> [!TIP]
> Avant de chargement votre application, vérifiez les problèmes à l’aide de la [fonctionnalité de validation de la boîte à outils](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool). Les erreurs doivent être résolues pour chargement l’application.

1. Connectez-vous au client teams avec votre compte qui autorise l’application chargement. (Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)
1. Sélectionnez **applications**, puis **Télécharger une application personnalisée**.
1. Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` . Une installation modale d’installation s’affiche.
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Capture d’écran illustrant un exemple d’installation de l’application teams modale.":::
1. Sélectionnez **Ajouter** pour installer votre application.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Capture d’écran illustrant un exemple d’application d’onglet personnelle « Hello, World ! » en cours d’exécution dans Teams.":::

🎉 Félicitations ! Votre application est en cours d’exécution dans Teams.

## <a name="next-step"></a>Étape suivante

Développez l’onglet personnel que vous venez de créer ou créez un autre type d’application Teams.

> [!div class="nextstepaction"]
> [Ajouter à votre onglet personnel](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Créer un onglet de canal](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)
