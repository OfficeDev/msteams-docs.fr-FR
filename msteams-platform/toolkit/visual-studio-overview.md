---
title: Créer des applications avec Microsoft teams Toolkit et Visual Studio
description: Commencer à créer des applications personnalisées directement dans Visual Studio à l’aide du kit de développement Microsoft teams
keywords: Kit de développement Visual Studio teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: a1221945659b2dd0f45bdd3a966d9b029ddcde09
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604486"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Créer des applications avec Team Toolkit et Visual Studio

Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio. Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="prerequisites"></a>Configuration requise

1. [Activer l’Aperçu pour les développeurs](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. Assurez-vous que le **<span>ASP.ne</span>T et le module de développement Web** a été ajouté à votre instance Visual Studio. Vous pouvez vérifier en suivant les étapes de la procédure [modifier Visual Studio en ajoutant ou en supprimant les charges de travail et](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) la documentation des composants.

![module asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, IIS (Internet Information Services) doit être installé dans votre environnement de développement. Visual Studio n’inclut pas les services Internet (IIS) et il n’est pas inclus dans la configuration par défaut de Windows 10, Windows 8 ou Windows 7 ; Toutefois, vous pouvez télécharger la dernière version à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=48264).

![Affichage de la page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Installer la boîte à outils teams

Microsoft teams Toolkit pour Visual Studio peut être téléchargé à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio.

## <a name="using-the-toolkit"></a>Utilisation de la boîte à outils

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Configurer votre application](#configure-your-app)
- [Empaquetage de votre application](#package-your-app)
- [Exécuter votre application dans teams](#install-and-run-your-app-locally)
- [Valider votre application](#validate-your-app)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet teams

1. Sélectionnez **créer un nouveau projet**.
1. Choisissez **application Microsoft teams** , puis cliquez sur **suivant**.
1. Vous arrivez à l’écran **configurer votre nouveau projet** , qui vous permet de choisir le **nom du projet**, son **emplacement** et le nom de la **solution**.
1. Activez la case à cocher **Placer la solution et le projet dans le même répertoire**.
1. Une fenêtre contextuelle intitulée ajouter des **fonctionnalités** vous permet de choisir une ou plusieurs fonctionnalités pour la configuration de votre projet.
1. Cliquez sur le bouton **suivant** pour terminer le processus de configuration.
1. Une fenêtre contextuelle intitulée ajouter des **fonctionnalités** vous permet de choisir les propriétés de chaque fonctionnalité sélectionnée.
1. Sélectionnez **Terminer** et vous serez sur la page d’accueil du **Kit Microsoft teams** .

## <a name="configure-your-app"></a>Configurer votre application

À son niveau principal, l’application teams adopte trois composants :

  1. Le client Microsoft Teams (Web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Serveur qui répond aux demandes de contenu qui s’affichent dans Teams, par exemple, le contenu de l’onglet HTML ou une carte de robot.
  1. Package d' [application](/concepts/build-and-test/apps-package.md) teams comprenant trois fichiers :

  > [!div class="checklist"]
  >
  > - La manifest.jssur
  > - Une [icône de couleur](../resources/schema/manifest-schema.md#icons) pour l’affichage de votre application dans le catalogue d’applications public ou d’organisation
 > - [Icône de plan](../resources/schema/manifest-schema.md#icons) pour l’affichage dans la barre d’activité de teams.

Lorsqu’une application est installée, le client teams analyse le fichier manifeste pour déterminer les informations nécessaires telles que le nom de votre application et l’URL où se trouvent les services.

> [!NOTE]
>Si vous ne l’avez pas déjà fait, vous devez vous connecter à votre compte Microsoft 365 ou pour poursuivre le processus de développement.
>
> Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire pour obtenir un abonnement au [programme de développement microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) . Elle est *gratuite* pendant 90 jours et se renouvelle en permanence tant que vous l’utiliserez pour l’activité de développement. Si vous disposez d’un abonnement Visual Studio *entreprise* ou *professionnel* , les deux programmes incluent un [abonnement de développeur](https://aka.ms/MyVisualStudioBenefits)gratuit Microsoft 365, actif pendant la durée de vie de votre abonnement Visual Studio. *Consultez la rubrique* [configurer un abonnement développeur Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).
>

### <a name="configuration-steps"></a>Étapes de configuration

1. Pour configurer votre application, dans la page d’accueil du kit de développement **Microsoft teams** , sélectionnez **modifier le package d’application** .
1. Dans le menu déroulant **My environnements** , sélectionnez **Development**.
1. Sur la page Détails de l' **application** , vous allez pouvoir modifier les champs de propriétés de votre application.
1. La modification des champs de la page des détails de l’application met à jour le contenu de la manifest.jssur un fichier qui sera finalement envoyé dans le cadre du package d’application. [En savoir plus](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetage de votre application

La modification de la page de détails de l' **application** ou la mise à jour du **manifeste**, ou des fichiers **. env** dans le dossier  **. Publish** de votre application, génère automatiquement votre fichier **Development.zip** . Le fichier Development.zip inclut trois fichiers obligatoires : le **manifest.jssur** et [deux icônes](../concepts/build-and-test/apps-package.md#app-icons).

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

1. Dans le menu déroulant **configurations de solutions** , sélectionnez **déployer**.

![Menu configurations de solutions](../assets/images/solution-configurations.png)

2. Sélectionnez le bouton **ISS Express + teams** .

1. Teams se lance et la boîte de dialogue d’installation de l’application doit apparaître dans le client Teams.

## <a name="validate-your-app"></a>Valider votre application

La page **Validate** vous permet de vérifier votre package d’application avant d’envoyer votre application à AppSource. Téléchargez simplement le package de manifeste et l’outil de validation vérifiera votre application par rapport à tous les cas de test liés au manifeste. Pour chaque test ayant échoué, la description fournit un lien vers la documentation pour vous aider à résoudre l’erreur. Pour les tests difficiles à automatiser, la liste de **vérification préliminaire** décrit les 7 des cas de test ayant échoué les plus fréquents, ainsi que le lien vers une liste de contrôle d’envoi complète.

## <a name="publish-your-app-to-teams"></a>Publier votre application dans teams

✔ Sur la page d’accueil de votre projet, vous pouvez charger votre application dans une équipe, envoyer votre application à votre magasin d’applications personnalisé d’entreprise pour les utilisateurs de votre organisation ou envoyer votre application à la source de l’application pour tous les utilisateurs de teams.

✔ Votre administrateur informatique examinera ces envois.

✔ Vous pouvez revenir à la page **publier** pour vérifier l’état de votre envoi et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. Il s’agit également de l’endroit où vous allez envoyer des mises à jour à votre application ou d’annuler les envois actuellement actifs.

> [!div class="nextstepaction"]
> [Étape suivante : maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
