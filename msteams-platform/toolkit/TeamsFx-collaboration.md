---
title: Collaborer sur TeamsFx Project à l’aide du Kit de ressources Teams
author: surbhigupta
description: Dans cet article, découvrez comment collaborer sur TeamsFx Project à l’aide de Teams Toolkit et collaborer avec d’autres développeurs.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 90ccd073e45649f715751e81835747bfb95d7806
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616839"
---
# <a name="collaborate-on-teams-project-using-microsoft-teams-toolkit"></a>Collaborer sur un projet Teams à l’aide de Microsoft Teams Toolkit

Plusieurs développeurs peuvent collaborer pour déboguer, provisionner et déployer pour le même projet TeamsFx, mais cela nécessite de définir manuellement les autorisations appropriées de Teams App et Microsoft Azure Active Directory (Azure AD). Teams Toolkit prend en charge la fonctionnalité de collaboration pour permettre aux développeurs et au propriétaire du projet d’inviter d’autres développeurs ou collaborateurs au projet TeamsFx à déboguer, approvisionner et déployer le même projet TeamsFx.

## <a name="collaborate-with-other-developers"></a>Collaborer avec d’autres développeurs

Les sections suivantes nous guident pour comprendre le processus de collaboration en tant que propriétaire ou collaborateur du projet :

### <a name="as-project-owner"></a>En tant que propriétaire du projet

  > [!NOTE]
  > Avant d’ajouter des collaborateurs pour un environnement, le propriétaire du projet doit [d’abord provisionner](provision.md) le projet.

  1. Sélectionnez **Teams Toolkit** dans la barre d’activité.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-teams-toolkit.png" alt-text="Sélectionner le kit de ressources Teams dans la barre d’activités":::

  1. Dans la section **ENVIRONNEMENT** , sélectionnez collaborateurs, qui s’affiche sous la forme de l’option **1** **Ajouter des propriétaires d’applications Microsoft 365 Teams (avec l’application Azure AD)** et **2** **Répertorier les propriétaires d’applications Microsoft 365 Teams (avec l’application Azure AD),** comme illustré dans l’image suivante :

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="Collaborateurs":::

  2. Sélectionnez **Ajouter des propriétaires d’application Microsoft 365 Teams (avec l’application Azure AD)** et ajoutez une autre adresse e-mail de compte Microsoft 365 en tant que collaborateur. Le compte à ajouter doit se trouver sur le même locataire que le propriétaire du projet pour le débogage à distance, comme illustré dans l’image :

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add-owner.png" alt-text="Ajouter le propriétaire du projet":::

  3. Pour afficher les collaborateurs dans l’environnement actuel, sélectionnez **Répertorier les propriétaires d’applications Microsoft 365 Teams (avec l’application Azure AD),** puis vous pouvez voir les collaborateurs répertoriés dans le canal de sortie, comme illustré dans l’image suivante :

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="list":::

  4. Envoyez (push) le projet à GitHub.

     > [!NOTE]
     > Les collaborateurs nouvellement ajoutés ne reçoivent aucune notification. Le propriétaire du projet doit notifier le collaborateur.

### <a name="as-project-collaborator"></a>En tant que collaborateur de projet

  1. Clonez le projet à partir de GitHub.
  2. Connectez-vous au compte Microsoft 365.
  3. Connectez-vous au compte Azure. Il dispose de l’autorisation de contributeur pour toutes les ressources Azure, qui sont utilisées dans le projet.
  4. Pour afficher un aperçu de votre application Teams, déployez le projet à distance.
  5. Lancez à distance pour avoir un aperçu de l’application Teams.

     > [!NOTE]
     > Les collaborateurs doivent se connecter à l’aide du compte que le propriétaire du projet ajoute sous le même locataire avec le propriétaire du projet. Pour plus d’informations, consultez [générer et exécuter votre application Teams dans un environnement distant](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch).

## <a name="remove-collaborators"></a>Supprimer des collaborateurs

Si vous souhaitez supprimer des collaborateurs de l’extension Teams Toolkit, vous devez les supprimer manuellement, car vous ne pouvez pas les supprimer directement. Effectuez les étapes suivantes pour supprimer manuellement les collaborateurs :

* Utilisation du portail des développeurs

  * Accédez au [portail des développeurs Teams](https://dev.teams.microsoft.com/home) et sélectionnez votre application Teams par nom ou ID d’application.
  * Sélectionnez **Propriétaires** dans le volet gauche.
  * Sélectionnez et supprimez le collaborateur.

* Utilisation d’Azure Active Directory

  * Accédez à [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), sélectionnez **Inscription d’application** dans le volet gauche et recherchez votre application Azure AD.
  * Sélectionnez **Propriétaires** dans le volet gauche de la page de gestion des applications Azure AD.
  * Sélectionnez et supprimez le collaborateur.

    > [!NOTE]
    >
    > * Le collaborateur ajouté à votre projet ne reçoit aucune notification. Le propriétaire du projet doit informer le collaborateur hors connexion.
    > * Les autorisations associées à Azure doivent être définies manuellement par l’administrateur d’abonnement Azure sur Portail Azure.
    > * Le compte Azure doit avoir un rôle de contributeur pour l’abonnement afin que les développeurs puissent collaborer pour approvisionner et déployer le projet TeamsFx.

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Déployer l’application Teams dans le cloud](deploy.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
