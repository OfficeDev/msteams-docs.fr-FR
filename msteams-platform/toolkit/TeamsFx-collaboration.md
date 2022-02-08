---
title: Collaborer sur des équipes TeamsFx Project l’aide Teams Shared Computer Toolkit
author: yanjiang
description: Collaborer sur des équipes TeamsFx Project l’aide Teams Shared Computer Toolkit
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>Collaborer sur Teams projet à l’aide Teams Shared Computer Toolkit

Plusieurs développeurs peuvent travailler ensemble pour déboguer, mettre en service et déployer pour le même projet TeamsFx, mais cela nécessite de définir manuellement les autorisations de Teams App et Azure AD App.Teams Shared Computer Toolkit prend en charge la fonctionnalité de collaboration pour permettre aux développeurs et au propriétaire du projet d’inviter d’autres développeurs ou collaborateurs au projet TeamsFx à déboguer,  et déployer le même projet TeamsFx.

## <a name="prerequisites"></a>Conditions préalables

* Conditions préalables pour le compte

    Pour mettre en service des ressources cloud, vous devez avoir les comptes suivants. Pour plus d’informations, voir, [préparer les comptes pour créer Teams application](accounts.md).

  * Abonnement Microsoft 365
  * Azure avec un abonnement valide

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Assurez-vous qu’un Teams d’application est ouvert dans Microsoft Visual Studio code.

## <a name="collaborate-with-other-developers"></a>Collaborer avec d’autres développeurs

La liste suivante nous guide pour comprendre le processus de collaboration et sa limitation :

### <a name="as-project-owner"></a>En tant que propriétaire du projet

> [!NOTE]
> Avant d’ajouter des collaborateurs pour un environnement, le propriétaire du [projet doit](provision.md) d’abord mettre en service le projet.

* Dans **la section ENVIRONNEMENT** sur Teams Shared Computer Toolkit, **sélectionnez des collaborateurs**. Il affiche les options Ajouter **une application Microsoft 365 Teams (avec Microsoft Azure Active Directory (Azure AD)** Et List **Microsoft 365 Teams App (avec Azure AD App) Propriétaires** comme illustré dans les images suivantes :

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="collaborateurs":::

* **Sélectionnez Ajouter Microsoft 365 Teams app (avec Azure AD App)** et ajoutez d’autres Microsoft 365 de messagerie de compte en tant que collaborateur. Le compte à ajouter doit se trouver sur le même client que le propriétaire du projet pour le débogage à distance, comme illustré dans l’image :

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add envi":::

* Pour afficher les collaborateurs dans l’environnement actuel, sélectionnez List **Microsoft 365 Teams App (avec Azure AD App),** puis les collaborateurs sont répertoriés dans le canal de sortie, comme illustré dans l’image suivante :

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="list":::

* Push the project to GitHub.

> [!NOTE]
> Le collaborateur nouvellement ajouté ne reçoit aucune notification. Project propriétaire doit avertir le collaborateur.

### <a name="as-project-collaborator"></a>En tant que collaborateur de projet

* Clonez le projet à partir GitHub.
* Connectez-vous Microsoft 365 compte.
* Connectez-vous au compte Azure, qui dispose de l’autorisation de collaborateur pour toutes les ressources Azure utilisées dans ce projet.
* Pour prévisualiser Teams application, déployez le projet à distance.
* Lancez à distance pour afficher un aperçu de l’Teams app.

Pour plus d’informations, [voir créer et exécuter votre application Teams dans un environnement distant](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch).

> [!NOTE]
> Les collaborateurs doivent se connecter à l’aide du compte ajouté par le propriétaire du projet, qui se trouve sous le même client avec le propriétaire du projet.

### <a name="limitation"></a>Restriction

Vous ne pouvez pas supprimer des collaborateurs directement de Teams Shared Computer Toolkit extension. Pour supprimer manuellement des collaborateurs, effectuez les étapes suivantes :

  1. Go to Teams Developer Portal and select your Teams app by name or app ID.
  2. Sélectionnez **Propriétaires** dans le panneau gauche.
  3. Sélectionnez et supprimez le collaborateur.
  4. Go to [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), select **App registration** from left panel, and find your Azure AD App.
  5. Sélectionnez **Propriétaires** dans le panneau gauche de la page Azure AD gestion des applications.
  6. Sélectionnez et supprimez le collaborateur.

> [!NOTE]
> * Le collaborateur ajouté à votre projet ne recevra aucune notification. Project propriétaire doit avertir le collaborateur hors connexion.
> * Les autorisations associées à Azure doivent être définies manuellement par l’administrateur d’abonnement Azure Microsoft Azure portail. Le compte Azure doit avoir un rôle de collaborateur pour l’abonnement afin que les développeurs peuvent collaborer pour mettre en service et déployer le projet TeamsFx.

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Déployer l’application Teams dans le cloud](deploy.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
