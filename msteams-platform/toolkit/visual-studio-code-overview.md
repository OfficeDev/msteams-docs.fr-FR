---
title: Créer des applications avec Microsoft teams Toolkit et Visual Studio code
description: Commencer à créer des applications personnalisées directement dans Visual Studio code avec Microsoft teams Toolkit
keywords: Kit de développement Visual Studio Visual Studio teams
ms.openlocfilehash: 7b8a32c099d85bec2584da2b42dcf5a524ecddbc
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651662"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio-code"></a>Créer des applications avec Microsoft teams Toolkit et Visual Studio code

Le kit de développement Microsoft teams vous permet de créer des applications teams personnalisées directement dans l’environnement Visual Studio code. Le kit de développement vous guide tout au long du processus et vous fournit tout ce dont vous avez besoin pour créer, déboguer et lancer votre application Teams.

## <a name="installing-the-teams-toolkit"></a>Installation du kit de développement teams

Microsoft teams Toolkit for Visual Studio code peut être téléchargé à partir de [Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement en tant qu’extension dans Visual Studio code.

> [!TIP]
> Après l’installation, vous devriez voir la boîte à outils teams dans la barre d’activité code Visual Studio. Si ce n’est pas le cas, cliquez avec le bouton droit de la barre d’activité et sélectionnez **Microsoft teams** pour épingler la boîte à outils pour un accès facile.

## <a name="using-the-toolkit"></a>Utilisation de la boîte à outils

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Importer un projet existant](#import-an-existing-teams-app-project)
- [Configurer votre application](#configure-your-app)
- [Empaquetage de votre application](#package-your-app)
- [Exécuter votre application dans teams](#run-your-app-in-teams)
- [Valider votre application](#validate-your-app)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet teams

1. Créez un dossier/espace de travail pour votre projet dans votre environnement local.
1. Dans Visual Studio code, sélectionnez l’icône teams ![Icône Teams](../assets/icons/favicon-16x16.png) à partir de la barre d’activité sur le côté gauche de la fenêtre.
1. Sélectionnez **ouvrir la boîte à outils Microsoft teams** dans le menu de commandes.
1. Sélectionnez **créer une nouvelle application teams** dans le menu de commandes.
1. Lorsque vous y êtes invité, entrez le nom de l’espace de travail. Il sera utilisé à la fois comme nom du dossier dans lequel votre projet réside et comme nom par défaut de votre application.
1. Appuyez sur **entrée** pour accéder à l’écran **Add Capabilities** et configurer les propriétés de votre nouvelle application.
1. Cliquez sur le bouton **Terminer** pour terminer le processus de configuration.

## <a name="import-an-existing-teams-app-project"></a>Importer un projet d’application teams existant

1. Dans Visual Studio code, sélectionnez l’icône teams ![Icône Teams](../assets/icons/favicon-16x16.png) à partir de la barre d’activité sur le côté gauche de la fenêtre.
1. Sélectionnez **Importer un package d’application** dans le menu de commandes.
1. Choisissez votre fichier zip de [package d’application teams](../concepts/build-and-test/apps-package.md) existant.
1. Cliquez sur le bouton **Sélectionner un package de publication** . L’onglet Configuration de la boîte à outils doit maintenant être renseigné avec les détails de votre application.
1. Dans Visual Studio code, sélectionnez **fichier**  ->  **Ajouter un dossier à l’espace de travail** pour ajouter le répertoire de votre code source à l’espace de travail de code Visual Studio.

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

1. Pour configurer votre application, accédez à l’onglet **Microsoft teams Toolkit** dans Visual Studio code.
1. Sélectionnez **modifier le package d’application** pour afficher la page des détails de l' **application** .
1. La modification des champs de la page des détails de l’application met à jour le contenu de la manifest.jssur un fichier qui sera finalement envoyé dans le cadre du package d’application. [En savoir plus](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetage de votre application

Modification vous êtes la page de détails de l' **application** ou vous mettez à jour le **manifeste**, ou les fichiers **. env** dans le dossier  **. Publish** de votre application généreront automatiquement votre fichier **Development.zip** . Vous devez inclure [deux icônes](../concepts/build-and-test/apps-package.md#icons) dans ce même dossier.

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

Pour obtenir des instructions détaillées sur l’empaquetage et le test de votre application, reportez-vous à la page **Build and Run* content in your Project. En général, vous devez installer le serveur de votre application, le faire fonctionner, puis configurer une solution de tunneling afin que les équipes puissent accéder au contenu exécuté à partir de localhost.

## <a name="add-a-trusted-certificate-for-localhost"></a>Ajouter un certificat approuvé pour localhost

Si vous souhaitez déboguer votre application basée sur les onglets sur localhost à l’aide du protocole HTTPS, vous devrez ajouter un certificat pour localhost au `Trusted Root Certification Authorities` catalogue. Vous n’avez besoin d’effectuer cette étape qu’une seule fois par ordinateur.</br></br>

**Créez et installez un certificat approuvé :**
<details>
  <summary>Développer ici</summary>

* Création et exécution de votre application
  * Suivez le instuctions dans la section **Build and Run** de votre projet Lisez-moi afin qu’il soit pris en charge par https://localhost:3000/tab . En règle générale, cette opération implique l’exécution de `npm install` Then `npm start`
  * Accédez à https://localhost:3000/tab à partir de Google Chrome ou du chrome de bordure.

* Acquérir le certificat SSL :
  * Ouvrez la fenêtre outils de développement chrome ( `ctrl + shift + i`  /  `cmd + option + i` ).
  * Cliquez sur l' `Security` onglet
  * Cliquez sur activé `View certificate` et vous avez la possibilité de télécharger le certificat, soit en le faisant glisser sur votre bureau dans OS X, soit en cliquant sur l' `Details` onglet dans Windows et en cliquant sur `Copy to File…`
  * Nommez le fichier <*tout*>. cer et enregistrez-le dans un dossier qui ne requiert pas le consentement de l’administrateur pour effectuer une action d’écriture.
  
* Installer le certificat sur **Windows**
  * Sélectionnez l' `DER encoded binary X.509 (.CER)` option (la première) et enregistrez-la.
  * Double-cliquez sur le certificat et installez-le.
  * Opte `Local Machine`
  * Choisir `Place all certificates in the following store`
  * Opte `Trusted Root Certification Authorities`
  * Confirmer votre installation
  
* Installer le certificat **Mac OS X**
  * Sur OS X, ouvrez l’utilitaire Trousseau d’accès, puis sélectionnez `System` -le dans le menu de gauche. Cliquez sur l’icône de verrou pour activer les modifications.
  * Cliquez sur le bouton plus situé en bas pour ajouter un nouveau certificat, puis sélectionnez le `localhost.cer` fichier que vous avez déplacé vers le bureau. Cliquez `Always Trust` dans la boîte de dialogue qui s’affiche.
  * Après avoir ajouté le certificat au trousseau système, double-cliquez sur le certificat, puis développez la `Trust` section des détails du certificat. Sélectionnez `Always Trust` pour chaque option.

> [!IMPORTANT]
> Si vous recevez un avertissement de certificat de sécurité, accédez à https://localhost:3000/tab . Si le site n’est toujours pas approuvé, redémarrez votre ordinateur et localhost doit être accepté comme approuvé.
</details>

## <a name="run-your-app-in-teams"></a>Exécuter votre application dans teams
- Conditions préalables :
  - [Activer le mode Aperçu pour les développeurs teams](https://aka.ms/teams-toolkit-enable-devpreview)

1. Accédez à la barre d’activité sur le côté gauche de la fenêtre de code Visual Studio.
1. Sélectionnez l’icône **exécuter** pour afficher l’affichage **exécuter et déboguer** .
1. Vous pouvez également utiliser le raccourci clavier `Ctrl+Shift+D` .

## <a name="validate-your-app"></a>Valider votre application

La page **Validate** vous permet de vérifier votre package d’application avant d’envoyer votre application à AppSource. Téléchargez simplement le package de manifeste et l’outil de validation vérifiera votre application par rapport à tous les cas de test liés au manifeste. Pour chaque test ayant échoué, la description fournit un lien vers la documentation pour vous aider à résoudre l’erreur. Pour les tests difficiles à automatiser, la liste de **vérification préliminaire** décrit les 7 des cas de test ayant échoué les plus fréquents, ainsi que le lien vers une liste de contrôle d’envoi complète.

## <a name="publish-your-app-to-teams"></a>Publier votre application dans teams

Sur la page d’accueil de votre projet, vous pouvez charger votre application dans une équipe, envoyer votre application à votre magasin d’applications personnalisé d’entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source de l’application pour tous les utilisateurs de teams. Votre administrateur informatique examinera ces envois. Vous pouvez revenir à la page *publier* pour vérifier l’état de votre envoi et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. Il s’agit également de l’endroit où vous allez envoyer des mises à jour à votre application ou d’annuler les envois actuellement actifs.

> [!div class="nextstepaction"]
> [Étape suivante : maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
