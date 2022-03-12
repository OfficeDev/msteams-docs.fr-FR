---
title: Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio avec le Microsoft Teams Shared Computer Toolkit. Découvrez comment configurer votre application dans Visual Studio, valider votre application et la publier à partir de Visual Studio portail de développement.
keywords: boîte à outils visual studio teams
ms.localizationpriority: medium
ms.topic: overview
ms.date: 1/13/2022
ms.author: johmil
ms.openlocfilehash: c34f1113cd4da5f1b416dba6bc950b3588accecf
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453429"
---
# <a name="teams-toolkit-for-visual-studio"></a>Extension de kit de ressources Teams pour Visual Studio

Créez, testez et développez des Teams à l’intérieur de votre IDE.

L’extension de Teams Shared Computer Toolkit pour Visual Studio facilite la création de projets pour Teams, la configuration automatique des applications dans le portail de développement Teams, l’utilisation et le débogage dans Teams, la configuration de l’hébergement cloud et l’utilisation de [TeamsFx](https://github.com/OfficeDev/teamsfx) à partir de votre IDE.

## <a name="install-teams-toolkit-for-visual-studio"></a>Installer Teams Shared Computer Toolkit pour Visual Studio

>[!NOTE]
> En tant que condition préalable, veillez à utiliser Visual Studio 2022 17.1 Preview 2 ou version plus nouvelle pour suivre les instructions ci-dessous.

1. Si vous avez déjà Visual Studio 2022 17.1 Preview 2, passez à l’étape suivante. Dans le cas [contraire, installez Visual Studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/).
2. Ouvrez le Visual Studio Installer.
3. **Sélectionnez Modifier** pour votre installation VS 2022 Preview existante.
4. Sélectionnez la **charge ASP.NET charge de travail de développement web**.
5. À droite, développez la section **ASP.NET développement web** et sélectionnez Microsoft Teams **outils** de développement dans la liste facultative des composants.
6. **Sélectionnez Installer** **ou Modifier** dans le Visual Studio Installer pour terminer le processus d’installation.

![Sélection des outils Microsoft Teams de développement dans le programme Visual Studio installer.) installé.](images/teams-development-tools-vs-installer.png)

## <a name="get-started-quickly-with-a-new-project"></a>Mise en place rapide d’un nouveau projet

Teams Shared Computer Toolkit modèles de projet fournissent l’ensemble du code, des fichiers et de la configuration dont vous avez besoin pour prendre en Teams projet d’application.

Le Microsoft Teams de projet Application vous permet de spécifier un compte Microsoft 365 requis pour inscrire et configurer automatiquement votre nouvelle application Teams client.

> [!NOTE]
> Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement [Microsoft 365 programme pour les développeurs](https://developer.microsoft.com/microsoft-365/dev-program). Il est gratuit pendant 90 jours et renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement Visual Studio Enterprise ou Professional, les deux programmes incluent un abonnement Microsoft 365 [développeur gratuit,](https://aka.ms/MyVisualStudioBenefits) actif pendant toute la durée de Visual Studio abonnement. Pour plus d’informations, [voir configurer un abonnement Microsoft 365 développeur.](/office/developer-program/office-365-developer-program-get-started)

1. Lancez Visual Studio 2022.
1. Dans la fenêtre de démarrage, choisissez **Créer un projet**.
1. Dans la **zone Rechercher des modèles**, entrez Microsoft Teams App.
1. Sélectionnez le **Microsoft Teams d’application** et sélectionnez **Suivant**.
1. Dans la **fenêtre Configurer votre nouveau projet**, tapez ou entrez _HelloTeams_ dans la **Project nom**. Ensuite, sélectionnez **Créer**.
1. Dans la **fenêtre Créer une application Teams**, choisissez ou connectez-vous à un compte Microsoft 365 à l’aide du sélecteur **de comptes**. Ensuite, sélectionnez **Créer**.

![Création d’un Microsoft Teams d’application dans Visual Studio.](images/teams-toolkit-vs-new-project.png)

Visual Studio ouvre votre nouveau projet et Teams Shared Computer Toolkit vous configurera le nouveau projet dans Teams Portail du développeur. Le projet est ajouté pour l’organisation Teams liée au compte Microsoft 365 que vous avez choisi dans les étapes ci-dessus et crée une nouvelle Azure Active Directory inscription. Cela est nécessaire pour que l’application s’exécute Teams.

## <a name="run-and-debug-your-app-in-teams"></a>Exécuter et déboguer votre application dans Teams

Vous pouvez lancer votre projet d’application s’exécutant localement à partir Visual Studio.

1. Ouvrez ou [créez un Teams d’application.](#get-started-quickly-with-a-new-project)
2. **Appuyez sur F5** ou **sélectionnez Déboguer > démarrer le débogage** dans Visual Studio.

Visual Studio lancez votre projet Teams’application dans un navigateur et démarrez le débogage.

## <a name="host-your-teams-app-in-the-cloud-and-preview-it"></a>Héberger votre application Teams dans le cloud et la prévisualiser

Vous pouvez créer et configurer automatiquement des ressources cloud pour l’hébergement de votre application dans Azure à l’aide Teams Shared Computer Toolkit.

1. Sélectionnez l **Project > Teams Shared Computer Toolkit > approvisionnement dans le menu Cloud**.
2. Dans la fenêtre Sélectionner votre abonnement, choisissez l’abonnement Azure avec qui vous souhaitez créer des ressources.

Teams Shared Computer Toolkit créer des ressources Azure dans cet abonnement, mais aucun code n’est déployé au cours de cette étape. Pour déployer votre projet sur ces nouvelles ressources :

1. Sélectionnez le **Project > Teams Shared Computer Toolkit > déployer dans le menu Cloud**.

## <a name="preview-your-app-running-from-cloud-resources"></a>Afficher un aperçu de l’exécution de votre application à partir des ressources cloud

Vous pouvez exécuter votre application dans un navigateur à l’aide des ressources distantes pour vérifier que tout fonctionne. Il n’est pas encore possible de déboguer pendant ce scénario.

1. Sélectionnez le **menu Project > Teams Shared Computer Toolkit > aperçu Teams’application**.

Votre application s’ouvre dans un navigateur et utilise les ressources créées par les étapes de mise en service et de déploiement.

## <a name="publish-your-app-to-teams"></a>Publier votre application sur Teams

Dans le [portail du développeur Teams](https://dev.teams.microsoft.com/home), vous pouvez télécharger votre application vers une équipe, soumettre votre application au magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source de l’application pour tous les Teams utilisateurs.

- Votre administrateur informatique examine ces envois.
- Vous pouvez revenir **à la page** Publier pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous pouvez soumettre des mises à jour à votre application ou annuler les soumissions actives.
