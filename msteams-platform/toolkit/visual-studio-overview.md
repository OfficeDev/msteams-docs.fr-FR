---
title: Créez des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio
description: Obtenez commencé à construire d’excellentes applications personnalisées directement Visual Studio avec le Microsoft Teams Shared Computer Toolkit
keywords: équipes kit d’outils studio visuel
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: eb94a8de0355283344ebe890a6fa3a3050e243ea
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566550"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Créez des applications avec les Teams Shared Computer Toolkit et Visual Studio

Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio. Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="prerequisites"></a>Configuration requise

1. [Activer l’aperçu des développeurs](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).

1. Assurez-vous que **<span>le module ASP.NE</span>T et web a** été ajouté à votre instance Visual Studio web. Vous pouvez vérifier en suivant les étapes de la modification de la [Visual Studio en ajoutant ou en supprimant les charges de travail et la](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation des composants.

![module visuel de asp.net studio](../assets/images/visual-studio-web-dev-module.png)

3. Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, vous devrez faire installer IIS (Internet Information Services) dans votre environnement de développement. Visual Studio n’inclut pas IIS et il n’est pas inclus dans la configuration Windows 10, Windows 8 ou Windows 7; toutefois, vous pouvez télécharger la dernière version à partir du centre [de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=48264).

![Vue de la page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Installez le Teams Shared Computer Toolkit

Le Microsoft Teams Shared Computer Toolkit pour Visual Studio est disponible en téléchargement sur [le Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio.

## <a name="using-the-toolkit"></a>Utilisation de la boîte à outils

- [Mettre en place un nouveau projet](#set-up-a-new-teams-project)
- [Configurer votre application](#configure-your-app)
- [Emballez votre application](#package-your-app)
- [Exécutez votre application dans Teams](#install-and-run-your-app-locally)
- [Valider votre application](#validate-your-app)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Mettre en place un nouveau projet Teams projet

1. Sélectionnez **Créer un nouveau projet**.
1. Choisissez **Microsoft Teams appe et** sélectionnez **Suivant**.
1. Vous arriverez à **l’écran Configurer votre nouveau** projet où vous pouvez choisir le nom **Project,** **emplacement,** et le nom **de la solution**.
1. Cochez la case **labeled Place solution et projet dans le même répertoire**.
1. Une fenêtre contexturée étiquetée **Add Capabilities vous** permettra de choisir une ou plusieurs fonctionnalités pour la configuration de votre projet.
1. Sélectionnez **le bouton** Suivant pour compléter le processus de configuration.
1. Une fenêtre contexturée étiquetée **Add Capabilities** vous permettra de choisir les propriétés pour chaque capacité sélectionnée.
1. Sélectionnez **Finition** et vous atterrirez sur la page **Microsoft Teams Shared Computer Toolkit** de destination.

## <a name="configure-your-app"></a>Configurer votre application

À la base, l Teams apprateur de messagerie embrasse trois composantes :

  1. Le Microsoft Teams client (web, bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Un serveur qui répond aux demandes de contenu qui seront affichées en Teams, par exemple, le contenu de l’onglet HTML ou une carte adaptative bot .
  1. Un paquet Teams’application se compose de trois fichiers :

      > [!div class="checklist"]
      >
      > - Le manifest.jssur
      > - Une [icône couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications publiques ou organisation
      > - Une [icône de contour](../resources/schema/manifest-schema.md#icons) pour l’affichage sur la barre d Teams’activité.

Lorsqu’une application est installée, le client Teams parse le fichier manifeste pour déterminer les informations nécessaires comme le nom de votre application et l’URL où se trouvent les services.

> [!NOTE]
>Si vous ne l’avez pas déjà fait, vous devrez vous connecter à votre Microsoft 365 ou compte pour poursuivre le processus de développement.
>
> Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un [abonnement Microsoft 365 programme de développement.](https://developer.microsoft.com/microsoft-365/dev-program) Il est gratuit *pendant* 90 jours et sera continuellement renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement Visual Studio *Enterprise* *ou Professional,* les deux programmes incluent un abonnement gratuit de développeur [Microsoft 365,](https://aka.ms/MyVisualStudioBenefits)actif pour la durée de vie de votre abonnement Visual Studio abonnement. Pour plus d’informations, [voir Configurer un abonnement Microsoft 365 développeur .](/office/developer-program/office-365-developer-program-get-started)
>

### <a name="configuration-steps"></a>Étapes de configuration

1. Pour configurer votre application, sur la page **de Microsoft Teams Shared Computer Toolkit,** sélectionnez **Modifier le package de l’application**.
1. À partir du menu de drop-down **My Environments,** sélectionnez **développement**.
1. Vous atterrirez sur la page **de détails de** l’application où vous pourrez modifier les champs de propriété de votre application.
1. L’édition des champs dans la page détails de l’application met à jour le contenu des manifest.jsdans le fichier qui sera finalement expédié dans le cadre du paquet d’application. [En savoir plus](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Emballez votre application

La modification de la page **des détails** de l’application ou la **mise à** jour du manifeste, ou les fichiers **.env dans** le dossier  **.publish de** votre application **généreront automatiquementDevelopment.zip** fichier. Le Development.zip inclut trois fichiers requis : le **manifest.jset** [deux icônes](../concepts/build-and-test/apps-package.md#app-icons).

## <a name="install-and-run-your-app-locally"></a>Installez et exécutez votre application localement

1. À partir du menu **de dropdown configurations** de solution, **sélectionnez Déployer** comme indiqué dans l’image suivante :

    ![Menu configurations de solutions](../assets/images/solution-configurations.png)

2. Sélectionnez **le bouton IIS Express + Teams** + .

1. Teams lancera et le dialogue d’installation de l’application doit apparaître dans Teams client.

## <a name="validate-your-app"></a>Valider votre application

La page **Validate** vous permet de vérifier le package de votre application avant de soumettre votre application à AppSource. Il suffit de télécharger le paquet manifeste et l’outil de validation vérifiera votre application par rapport à tous les cas de test liés manifestes. Pour chaque test échoué, la description fournit un lien de documentation pour vous aider à corriger l’erreur. Pour les tests difficiles à automatiser, la liste de vérification préliminaire détaille 7 des cas de test échoués les plus courants ainsi qu’un lien vers une liste de vérification complète de la soumission. 

## <a name="publish-your-app-to-teams"></a>Publier votre application sur Teams

✔ Sur votre page d’accueil du projet, vous pouvez télécharger votre application à une équipe, soumettre votre application à votre app store personnalisé pour les utilisateurs de votre organisation, ou soumettre votre application à App Source pour tous les utilisateurs de Teams.

✔ votre administrateur informatique examinera ces soumissions.

✔ Vous pouvez revenir à la page **Publier** pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous viendront soumettre des mises à jour à votre application ou annuler toutes les soumissions actuellement actives.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Maintenir et soutenir votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
