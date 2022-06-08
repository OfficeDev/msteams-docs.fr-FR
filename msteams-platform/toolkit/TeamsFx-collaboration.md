---
title: Collaborer sur TeamsFx Project à l’aide du Kit de ressources Teams
author: yanjiang
description: Collaborer sur TeamsFx Project à l’aide du Kit de ressources Teams
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: be36cf1af9741d65d66ede498f5ac2fff31df148
ms.sourcegitcommit: ff31cbe4840191f004d8fc61dd4fd93d35fcaecb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2022
ms.locfileid: "65938869"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>Collaborer sur un projet Teams à l'aide de Teams Toolkit

Plusieurs développeurs peuvent collaborer pour déboguer, approvisionner et déployer pour le même projet TeamsFx, mais cela nécessite de définir manuellement les autorisations appropriées de l’application Teams et de l’application Microsoft Azure Active Directory (Azure AD). Teams Toolkit prend en charge la fonctionnalité de collaboration pour permettre aux développeurs et au propriétaire du projet d’inviter d’autres développeurs ou collaborateurs au projet TeamsFx à déboguer, approvisionner et déployer le même projet TeamsFx.

## <a name="prerequisites"></a>Conditions préalables

* Abonnement Microsoft 365
* Azure avec un abonnement valide
  
  Pour plus d’informations sur les différents comptes, consultez [préparer des comptes pour créer une application Teams](accounts.md).

* [Installer Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+

> [!TIP]
> Vérifiez qu’un projet d’application Teams est ouvert dans Visual Studio Code.

## <a name="collaborate-with-other-developers"></a>Collaborer avec d’autres développeurs

Les listes suivantes nous guident pour comprendre le processus de collaboration et ses limitations :

* En tant que propriétaire du projet

  > [!NOTE]
  > Avant d’ajouter des collaborateurs pour un environnement, le propriétaire du projet doit [d’abord provisionner](provision.md) le projet.

  1. Dans la section **ENVIRONNEMENT** du Kit de ressources Teams, sélectionnez **des collaborateurs**. Il affiche les options **Ajouter des propriétaires d’application Microsoft 365 Teams (avec application Azure AD)** et **répertorier les propriétaires d’applications Microsoft 365 Teams (avec l’application Azure AD),** comme illustré dans les images suivantes :

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="Collaborateurs":::

  2. Sélectionnez **Ajouter des propriétaires d’application Microsoft 365 Teams (avec l’application Azure AD)** et ajoutez une autre adresse e-mail de compte Microsoft 365 en tant que collaborateur. Le compte à ajouter doit se trouver sur le même locataire que le propriétaire du projet pour le débogage à distance, comme illustré dans l’image :

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add envi":::

  3. Pour afficher les collaborateurs dans l’environnement actuel, sélectionnez **Répertorier les propriétaires d’applications Microsoft 365 Teams (avec l’application Azure AD),** puis les collaborateurs sont répertoriés dans le canal de sortie, comme illustré dans l’image suivante :

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="liste":::

  4. Envoyer (push) le projet à GitHub

     > [!NOTE]
     > Les collaborateurs nouvellement ajoutés ne reçoivent aucune notification. Le propriétaire du projet doit notifier le collaborateur.

* En tant que collaborateur de projet

  1. Clonez le projet à partir de GitHub.
  2. Connectez-vous au compte Microsoft 365.
  3. Connectez-vous au compte Azure. Il dispose de l’autorisation de contributeur pour toutes les ressources Azure, qui sont utilisées dans le projet.
  4. Pour afficher un aperçu de votre application Teams, déployez le projet à distance.
  5. Lancez à distance pour avoir un aperçu de l’application Teams.

     > [!NOTE]
     > Les collaborateurs doivent se connecter à l’aide du compte que le propriétaire du projet ajoute sous le même locataire avec le propriétaire du projet. Pour plus d’informations, consultez [générer et exécuter votre application Teams dans un environnement distant](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch).

### <a name="limitations"></a>Limites

Si vous souhaitez supprimer des collaborateurs de l’extension Teams Toolkit, vous devez les supprimer manuellement, car vous ne pouvez pas les supprimer directement. Effectuez les étapes suivantes pour supprimer manuellement les collaborateurs :

* Utilisation du portail des développeurs

  * Accédez au [portail des développeurs Teams](https://dev.teams.microsoft.com/home) et sélectionnez votre application Teams par nom ou ID d’application
  * Sélectionner **Propriétaires** dans le volet gauche
  * Sélectionner et supprimer le collaborateur

* Utilisation d’Azure Active Directory

  * Accédez à [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), sélectionnez **Inscription d’application** dans le volet gauche et recherchez votre application Azure AD
  * Sélectionner **Propriétaires** dans le volet gauche de la page de gestion des applications Azure AD
  * Sélectionner et supprimer le collaborateur

   > [!NOTE]
   >
   > * Le collaborateur ajouté à votre projet ne reçoit aucune notification. Le propriétaire du projet doit informer le collaborateur hors connexion.
   > * Les autorisations associées à Azure doivent être définies manuellement par l’administrateur d’abonnement Azure sur le portail Azure. Le compte Azure doit avoir un rôle de contributeur pour l’abonnement afin que les développeurs puissent collaborer pour approvisionner et déployer le projet TeamsFx.

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Déployer l’application Teams dans le cloud](deploy.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
