---
title: Créer des applications avec Microsoft teams Toolkit et Visual Studio
description: Commencer à créer des applications personnalisées directement dans Visual Studio à l’aide du kit de développement Microsoft teams
keywords: Kit de développement Visual Studio teams
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051710"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a>Créer des applications avec Microsoft teams Toolkit et Visual Studio

Le kit de développement Microsoft teams vous permet de créer des applications teams personnalisées directement dans l’environnement Visual Studio. Le kit de développement vous guide tout au long du processus et vous fournit tout ce dont vous avez besoin pour créer, déboguer et lancer votre application Teams.

## <a name="installing-the-teams-toolkit"></a>Installation du kit de développement teams

Microsoft teams Toolkit pour Visual Studio peut être téléchargé à partir de [Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement en tant qu’extension dans Visual Studio.

## <a name="using-the-toolkit"></a>Utilisation de la boîte à outils

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Configurer votre application](#configure-your-app)
- [Empaquetage de votre application](#package-your-app)
- [Exécuter votre application dans teams](#install-and-run-your-app-locally)
- [Valider votre application](#validate-your-app)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet teams

1. Créez un projet et sélectionnez le modèle Microsoft Terams Toolkit.
1. Vous arrivez à l’écran **Add Capabilities** pour configurer les propriétés de votre nouvelle application.
1. Cliquez sur le bouton **Terminer** pour terminer le processus de configuration.

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

1. Pour configurer votre application, accédez à la fenêtre d’extension de **Microsoft teams Toolkit** .
1. Sélectionnez **modifier le package d’application** pour afficher la page des détails de l' **application** .
1. La modification des champs de la page des détails de l’application met à jour le contenu de la manifest.jssur un fichier qui sera finalement envoyé dans le cadre du package d’application. [En savoir plus](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetage de votre application

Modification vous êtes la page de détails de l' **application** ou vous mettez à jour le **manifeste**, ou les fichiers **. env** dans le dossier **. Publish** de votre application généreront automatiquement votre fichier **Development.zip** . Vous devez inclure [deux icônes](../concepts/build-and-test/apps-package.md#icons) dans ce même dossier.

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

Dans le menu déroulant *configurations de solutions* , sélectionnez *déployer*. Appuyez sur le bouton *ISS Express + teams* . Teams se lance et la boîte de dialogue d’installation de l’application doit apparaître dans le client Teams.

## <a name="validate-your-app"></a>Valider votre application

La page **Validate** vous permet de vérifier votre package d’application avant d’envoyer votre application à AppSource. Téléchargez simplement le package de manifeste et l’outil de validation vérifiera votre application par rapport à tous les cas de test liés au manifeste. Pour chaque test ayant échoué, la description fournit un lien vers la documentation pour vous aider à résoudre l’erreur. Pour les tests difficiles à automatiser, la liste de **vérification préliminaire** décrit les 7 des cas de test ayant échoué les plus fréquents, ainsi que le lien vers une liste de contrôle d’envoi complète.

## <a name="publish-your-app-to-teams"></a>Publier votre application dans teams

Sur la page d’accueil de votre projet, vous pouvez charger votre application dans une équipe, envoyer votre application à votre magasin d’applications personnalisé d’entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source de l’application pour tous les utilisateurs de teams. Votre administrateur informatique examinera ces envois. Vous pouvez revenir à la page *publier* pour vérifier l’état de votre envoi et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. Il s’agit également de l’endroit où vous allez envoyer des mises à jour à votre application ou d’annuler les envois actuellement actifs.

> [!div class="nextstepaction"]
> [Étape suivante : maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
