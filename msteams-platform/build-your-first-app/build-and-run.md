---
title: 'Commencer : créer et exécuter votre première application'
author: heath-hamilton
description: Créez rapidement une application Microsoft Teams qui affiche un « Hello, World! » à l’aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093949"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>Créer et exécuter votre première application Microsoft Teams

Démarrez le développement de Microsoft Teams en construisant un onglet personnel qui affiche « Hello, World! ».
Créez et exécutez votre première application Teams en suivant les étapes suivantes :

## <a name="1-create-your-app-project"></a>1. Créer votre projet d’application

Utilisez la Shared Computer Toolkit Microsoft Teams Visual Studio Code pour configurer votre premier projet d’application. Créez votre projet d’application en suivant les étapes suivantes :

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.
1. Dans **l’écran Ajouter des fonctionnalités,** **sélectionnez Onglet,** puis **Suivant**.
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran montrant comment configurer votre projet d’application avec la Visual Studio Code Teams Shared Computer Toolkit.":::
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.)
1. Cochez uniquement **l’option Onglet** Personnel et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.

## <a name="2-understand-important-app-project-components"></a>2. Comprendre les composants importants d’un projet d’application

Une fois que le kit de ressources a configuré votre projet, vous avez les composants pour créer un onglet personnel de base pour Teams. Les répertoires et fichiers du projet s’affichent dans la zone Explorateur de Visual Studio Code.

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran montrant les fichiers de projet d’application pour un onglet personnel dans Visual Studio Code.":::

### <a name="app-scaffolding"></a>Échafaudage d’application

Le kit de ressources crée automatiquement la création de la forme dans le répertoire en fonction des fonctionnalités que vous avez ajoutées lors de `src` l’installation.

Si vous créez un onglet lors de l’installation, par exemple, le fichier dans le répertoire est important car il gère l’initialisation et le `App.js` `src/components` routage de votre application. Il appelle le [SDK client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.

### <a name="app-id"></a>ID de l’application

Configurez votre application avec App Studio à l’aide de l’ID d’application Teams. Recherchez l’ID dans `teamsAppId` l’objet, qui se trouve dans le fichier de votre `package.json` projet.

## <a name="3-build-and-run-your-app"></a>3. Créer et exécuter votre application

Créez et exécutez votre application localement pour gagner du temps. Ces informations sont également disponibles dans le kit de `README` ressources. Créez et exécutez votre application en suivant les étapes suivantes :

1. Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécutez `npm start` .

Une fois terminé, une compilation a **réussi !** dans le terminal. Votre application est en cours d’exécution sur `https://localhost:3000` .

## <a name="4-sideload-your-app-in-teams"></a>4. Chargement de version secondaire de votre application dans Teams

Votre application est prête à être testée dans Teams. Pour ce faire, vous devez avoir un compte de développement Microsoft 365 qui autorise le chargement de version de version d’application. Pour plus d’informations sur l’ouverture de compte, voir [le compte de développement Teams.](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account) 

> [!TIP]
> Recherchez les problèmes avant de recharger une version indépendante de votre application, à l’aide de la fonctionnalité de validation dans [App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)qui est incluse dans le kit de ressources. Corrigez les erreurs de chargement de version de l’application.

Chargez une version de votre application dans Teams en suivant les étapes suivantes :

> [!NOTE]
> Pour activer le chargement de version sideloading avant de charger une version de version de votre application dans Teams, suivez les étapes de l’étape Activer le chargement de version [de l’application.](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)

1. Sélectionnez **la touche F5** pour lancer un client web Teams dans Visual Studio Code.
1. Pour afficher le contenu de votre application dans Teams, spécifiez que l’endroit où votre application est en cours d’exécution ( `localhost` ) est digne de confiance :
   1. Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyez sur **F5**.
   1. Go to `https://localhost:3000/tab` and proceed to the page.
1. Revenir à Teams. Dans la boîte de dialogue, **sélectionnez Ajouter pour moi** pour installer votre application.
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Capture d’écran montrant un exemple d’application d’onglet personnel « Hello, World! » en cours d’exécution dans Teams.":::

🎉 félicitations ! Votre application s’exécute dans Teams.

## <a name="next-step"></a>Étape suivante

Développez l’onglet personnel que vous avez créé ou créez un autre type d’application Teams.

> [!div class="nextstepaction"]
> [Ajouter à votre onglet personnel](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [Créer un onglet de canal](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)
