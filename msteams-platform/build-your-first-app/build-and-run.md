---
title: Prise en main-créer et exécuter votre première application
author: heath-hamilton
description: Créez rapidement une application Microsoft teams qui affiche un « Hello, World ! ». message à l’aide de Microsoft teams Toolkit.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931775"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Créer et exécuter votre première application Microsoft teams

Vous pouvez accéder directement au développement Microsoft teams en créant un onglet personnel qui affiche « Hello, World ! ».

## <a name="1-create-your-app-project"></a>1. créer votre projet d’application

Utilisez la boîte à outils Microsoft teams dans Visual Studio code pour configurer votre premier projet d’application.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran indiquant comment configurer votre projet d’application avec Visual Studio code teams Toolkit.":::
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Activez uniquement l’option **onglet personnel** et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.

## <a name="2-understand-important-app-project-components"></a>2. comprendre les composants importants du projet d’application

Une fois que le kit d’outils configure votre projet, vous disposez des composants permettant de créer un onglet personnel de base pour Teams. Les répertoires et les fichiers du projet sont affichés dans la zone Explorateur de Visual Studio code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran illustrant les fichiers de projet d’application pour un onglet personnel dans Visual Studio code.":::

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.

Si vous créez un onglet pendant l’installation, par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application. Il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.

### <a name="app-id"></a>ID de l’application

L’ID d’application de teams est nécessaire pour configurer votre application avec App Studio. Vous pouvez trouver l’ID dans l' `teamsAppId` objet, qui se trouve dans le fichier de votre projet `package.json` .

## <a name="3-build-and-run-your-app"></a>3. générez et exécutez votre application

Pour des raisons de temps, vous allez créer et exécuter votre application localement.

(Ces informations sont également disponibles dans la boîte à outils `README` .)

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` .

Une fois terminé, une **compilation est effectuée.** message dans le terminal. Votre application est en cours d’exécution sur `https://localhost:3000` .

## <a name="4-sideload-your-app-in-teams"></a>4. chargement de votre application dans teams

Votre application est prête à être testée dans Teams. Pour ce faire, vous devez disposer d’un compte qui autorise l’application chargement. (Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)

> [!TIP]
> Avant de chargement votre application, vérifiez les problèmes à l’aide de la [fonctionnalité de validation dans App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), qui est incluse dans la boîte à outils. Les erreurs doivent être résolues pour chargement l’application.

1. Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.
1. Pour afficher le contenu de votre application dans Teams, spécifiez le lieu de fiabilité de votre application ( `localhost` ).
   1. Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyé sur **F5**.
   1. Accédez à `https://localhost:3000/tab` la page et passez à la page.
1. Revenir à Teams. Dans la boîte de dialogue, sélectionnez **Ajouter pour moi** pour installer votre application.
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
