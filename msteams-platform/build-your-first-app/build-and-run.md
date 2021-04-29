---
title: 'Commencer : créer et exécuter votre première application'
author: girliemac
description: Créez rapidement une application Microsoft Teams qui affiche un « Hello, World! » à l'aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068781"
---
# <a name="create-your-first-microsoft-teams-app"></a>Créer votre première application Microsoft Teams

Ce démarrage rapide vous apprend à créer et exécuter l'application Microsoft Teams qui affiche « Hello, World! »

## <a name="prerequisites"></a>Prerequisites

Avant de commencer, vous devez configurer [votre client](#set-up-your-teams-development-tenant) de développement Teams et installer [vos outils de développement Teams.](#install-your-development-tools)

### <a name="set-up-your-teams-development-tenant"></a>Configurer votre client de développement Teams

Un **client** est comme un conteneur pour une organisation. En termes teams, un client est l'endroit où les personnes de cette organisation discutent, partagent des fichiers et exécutent des réunions. En tant que développeur, vous avez besoin d'un client pour le chargement indépendant et le test des applications Teams que vous construisez.  

# <a name="do-not-have-a-tenant"></a>[N'avez pas de client](#tab/do-not-have-a-tenant)

Vous pouvez obtenir un compte de test Teams gratuit, qui inclut un client qui autorise le chargement de version test d'application, en rejoignant le programme pour les développeurs Microsoft 365. Le processus d'inscription prend environ deux minutes.

**Pour obtenir un client**

1. Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).
1. Sélectionnez **Rejoindre maintenant** et suivez les instructions à l'écran.
1. Dans l'écran d'accueil, **sélectionnez Configurer l'abonnement E5.**
1. Configurer votre compte de développeur Microsoft 365. 
   Une fois que vous avez terminé, l'écran suivant s'affiche :

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrire au programme pour les développeurs Microsoft 365.":::

1. Connectez-vous à Teams avec votre nouveau compte.
1. Dans le client Teams, sélectionnez **Applications.**
1. Vérifiez que vous pouvez voir l'option **Télécharger une application personnalisée.** Si c'est le cas, cela signifie que vous pouvez télécharger une version de version de chargement de version d'application.

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

# <a name="have-a-tenant"></a>[Avoir un client](#tab/have-a-tenant)

Si vous avez déjà un client, vérifiez si vous pouvez télécharger une version de version de chargement de version d'application dans Teams.

**Vérifier que vous pouvez télécharger une version de version de chargement de version de vos applications** 

1. Dans le client Teams, sélectionnez **Applications.** 
1.  Vérifiez que vous pouvez voir l'option **Télécharger une application personnalisée.** Si vous le faites, cela signifie que vous pouvez télécharger une version de version de chargement de version de version d'application. 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

---

### <a name="install-your-development-tools"></a>Installer vos outils de développement

Pour créer cette application, vous allez utiliser le Shared Computer Toolkit Teams pour Visual Studio code pour démarrer rapidement. Vous pouvez également créer des applications Teams avec n'importe quel de vos outils pré-utilisés. 

> [!NOTE]
> Teams affiche le contenu de l'application uniquement par le biais de connexions HTTPS. Pour déboguer certains types d'applications localement, comme un bot, vous allez apprendre à utiliser ngrok pour configurer un tunnel sécurisé entre Teams et votre application.
> 
> Les applications De Production Teams sont hébergées dans le cloud.

**Pour installer les outils Microsoft Teams**

1. Installez [Node.js](https://nodejs.org/en/).
1. Si vous prévoyez de créer un bot ou une extension de messagerie, installez [ngrok](https://ngrok.com/download) et exposez votre [localhost sur Internet](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)à l'aide de ngrok .
1. Installez la dernière version de [Visual Studio Code](https://code.visualstudio.com/download). 
   
   > [!NOTE]
   > Le kit de ressources ne prend pas en charge les versions antérieures Visual Studio Code.

1. Dans la barre d'activité de gauche, sélectionnez **Extensions.** :::image type="icon" source="../assets/icons/vs-code-extensions.png":::
1. Dans **Microsoft Teams Shared Computer Toolkit,** sélectionnez **Installer.**

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Illustration montrant où, dans Visual Studio Code, vous pouvez installer l'extension Shared Computer Toolkit Microsoft Teams.":::

## <a name="1-create-your-app-project"></a>1. Créer votre projet d'application

1. Ouvrez Visual Studio Code.
1. Sélectionnez **Microsoft Teams Shared Computer Toolkit** créer une application :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Teams.**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Capture d'écran montrant comment créer votre projet d'application avec la Visual Studio Code Teams Shared Computer Toolkit.":::
   
1. Connectez-vous avec votre compte de développement Microsoft 365. Soit celui que vous avez créé, soit le compte que vous avez déjà qui autorise le chargement d'une version de l'application.
1. Dans **l'écran Sélectionner un** projet, sélectionnez **Application** personnelle et **sélectionnez JS** (JavaScript) > **Suivant**.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Capture d'écran montrant comment configurer votre projet d'application avec la Visual Studio Code Teams Shared Computer Toolkit.":::

1. Entrez un nom pour votre application Teams.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Screenshot showing how to add a name to your app project with the Visual Studio Code Teams Toolkit.":::

1. Sélectionnez **Terminer**. 
   Votre projet est maintenant configuré. 

## <a name="2-understand-your-app-project-components"></a>2. Comprendre les composants de votre projet d'application

Une fois que le kit de ressources a configuré votre projet d'application, vous avez les composants pour créer votre « Hello, World! » Application Teams. Les répertoires et fichiers du projet se trouvent dans l'Explorateur Visual Studio code. 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Screenshot showing the scaffolding in your app project with the Visual Studio Code Teams Toolkit.":::

Le kit de ressources crée automatiquement la création de la création de lacafé d'application dans le répertoire en fonction des fonctionnalités que vous avez ajoutées `src` lors de l'installation. Étant donné que vous avez créé un onglet lors de l'installation, le fichier dans le répertoire gère l'initialisation et le `App.js` `src/components` routage de votre application. Le fichier appelle également le SDK client JavaScript Microsoft Teams pour établir la communication entre votre application et Teams. 

## <a name="3-build-and-run-your-app"></a>3. Créer et exécuter votre application

Créez et exécutez votre application localement pour gagner du temps. 

**Pour créer et exécuter votre application**

1. Dans Visual Studio code, sélectionnez **Afficher le**  >  **terminal.**
1. Exécutez `npm install` .
1. Exécutez `npm start` .
  
  Une **compilation réussie !** s'affiche dans le terminal. Votre application est désormais en cours d'exécution sur votre localhost sur `https://localhost:3000` . 

## <a name="4-sideload-your-app-in-teams"></a>4. Chargement de version secondaire de votre application dans Teams

Le chargement de version d'évaluation est le processus d'installation d'une application dans Teams qui n'a pas été approuvée par votre administrateur ou Microsoft. Le chargement de version test est courant lors du test et du débogage des applications Teams.

Par défaut, Teams n'autorise pas le chargement de version de l'application. Vous pouvez modifier ce paramètre dans le Centre d'administration Teams.

**Pour activer le chargement de version d'application dans Teams**

1. Connectez-vous au [Centre d'administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d'identification d'administrateur.  
1. Sélectionnez **Afficher toutes les**  >  **équipes.** 

   ![image du menu centre d'administration](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > L'apparition de l'option **Teams** peut prendre jusqu'à 24 heures. 

1. Go to **Teams apps**  >  **Setup policies**  >  **Global** (Org-wide default).

   ![activer l'affichage sideload](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. Activer le **basculement d'applications personnalisées** de chargement.

1. Sélectionnez **Enregistrer** pour enregistrer les modifications.

   Votre client test autorise désormais le chargement de version test de l'application personnalisée.

   > [!Note]
   > Vérifiez les problèmes avant de décharger votre application à l'aide de la fonctionnalité de validation dans App Studio, qui est incluse dans le kit de ressources. Corrigez les erreurs de chargement de version de l'application.


### <a name="sideload-your-app"></a>Chargement de version secondaire de votre application

1. Dans Visual Studio Code, ouvrez le Shared Computer Toolkit Teams.
1. Go to **App Studio**.  
1. Sélectionnez **Tester et distribuer l'installation.**  >  

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Screenshot showing how to sideload your app to Teams client with the Visual Studio Code Teams Toolkit.":::

**Alternativement**

1. Sélectionnez la **touche F5** pour ouvrir la fenêtre du navigateur à installer. Cela permet d'ignorer le processus d'installation dans **App Studio** et d'installer Teams dans votre navigateur.
1. Dans la boîte de dialogue d'installation, **sélectionnez Ajouter** pour installer votre application dans Teams.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="Screenshot showing how to sideload your app to Teams client.":::

   > [!Note]
   > App Studio est également disponible en tant qu'application autonome pour le client Teams.

### <a name="troubleshoot-sideloading-issues"></a>Résoudre les problèmes de chargement de version secondaire

**Échec de l'installation**

Si le message d'erreur s'affiche lors de l'installation de votre application, vérifiez que les informations de `Manifest parsing has failed` l'application sont entrées correctement.

**Pour vérifier les informations de l'application**

* Dans la Shared Computer Toolkit Teams, allez aux détails de **l'application App Studio** et vérifiez que toutes les informations requises sont  >   entrées correctement.
*  Si vous avez modifié manuellement le fichier, vérifiez que le JSON est bien défini dans l'outil manifeste de `manifest.json` l'application dans  App Studio.

**Contenu de l'onglet non affiché**

Vérifiez que votre application est en cours d'exécution. Si ce n'est pas le cas, allez sur le terminal et exécutez `npm start` .

## <a name="see-also"></a>Voir aussi

* [Préparer votre client Microsoft Office 365](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [Choix d'une configuration pour tester et déboguer votre application Microsoft Teams](../concepts/build-and-test/debug.md)
* [Création d'onglets et d'autres expériences hébergées avec le SDK client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md)
* [Préparer la soumission d'AppSource](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Développez rapidement des applications avec App Studio pour Microsoft Teams](../concepts/build-and-test/app-studio-overview.md)
* [Créer un onglet de canal](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet personnel pour Microsoft Teams](../build-your-first-app/build-personal-tab.md)
