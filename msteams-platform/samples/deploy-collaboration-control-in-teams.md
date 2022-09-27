---
title: Déployer une application avec des contrôles collaboration dans Microsoft Teams
author: surbhigupta
description: Dans ce module, découvrez comment déployer votre application avec le contrôle Collaboration dans Microsoft Teams et comment permettre à d’autres utilisateurs d’utiliser votre application.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 75a2aa9d09247ac152c31df02f2bb8d4fb507619
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027304"
---
# <a name="deploy-collaboration-controls-to-microsoft-teams"></a>Déployer des contrôles collaboration dans Microsoft Teams

Les contrôles de collaboration fonctionnent actuellement mieux dans Microsoft Teams. Vous pouvez créer une application qui peut être incorporée dans l’application Teams sous la forme d’une application personnelle et d’une application onglet.

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

## <a name="configure-the-app-for-teams"></a>Configurer l’application pour Teams

L’application que vous avez créée dans [créer une application pilotée par modèle](~/samples/app-with-collaboration-controls.md#create-a-model-driven-application) n’a qu’un seul volet gauche et il n’existe aucune commande complexe. Ainsi, avant d’ajouter votre application dans Teams, vous pouvez masquer le volet gauche et rendre l’affichage d’en-tête plus compréhensible.

> [!NOTE]
> N’activez pas les étapes suivantes si vous souhaitez afficher le volet gauche et l’en-tête à haute densité à vos utilisateurs.

Pour ce faire, nous allons utiliser les nouveaux paramètres de **l’application** Power Apps.

1. Accédez à **Solutions** dans le volet gauche.

1. Accédez au bas de votre liste de solutions et sélectionnez **Solution par défaut**.

1. Recherchez et sélectionnez **définition de paramètre**.

     :::image type="content" source="../assets/images/collaboration-control/settings-defnition.png" alt-text="Définition de paramètre":::

1. Recherchez et **sélectionnez Masquer la barre de navigation** dans la liste des définitions de paramètres. Cela masque le volet gauche de votre application.

     :::image type="content" source="../assets/images/collaboration-control/hide-the-nav-bar.png" alt-text="Masquer la barre de navigation":::

1. En bas à droite de votre application dans le volet d’édition, une section intitulée **Définir les valeurs de l’application** s’affiche. Si vous avez créé votre application à l’aide du concepteur d’applications moderne, votre application apparaît dans la liste. Sélectionnez **Nouvelle valeur d’application** sous votre application.

1. Remplacez la valeur **non** par **Oui.**

     :::image type="content" source="../assets/images/collaboration-control/value-to-yes.png" alt-text="Remplacer la valeur par oui":::

1. Sélectionnez **Enregistrer.**

1. Recherchez et sélectionnez **l’en-tête de page à haute densité d’application** dans la liste des définitions de paramètres, puis répétez le processus.

     :::image type="content" source="../assets/images/collaboration-control/density-page-header.png" alt-text="En-tête de page densité":::

1. **Sélectionnez Revenir aux solutions**.

     :::image type="content" source="../assets/images/collaboration-control/default-solution.png" alt-text="Solution par défaut":::

1. Sélectionnez **Publier toutes les personnalisations** pour publier tout le travail que vous avez effectué.

     :::image type="content" source="../assets/images/collaboration-control/publish-cusomization.png" alt-text="Publier toutes les personnalisations":::

## <a name="add-the-app-to-microsoft-teams-app-catalog"></a>Ajouter l’application au catalogue d’applications Microsoft Teams

À mesure que les paramètres sont définis, vous pouvez maintenant ajouter l’application à Microsoft Teams. Pour commencer, accédez à la page **Applications** dans le portail Power Apps maker, recherchez l’application que vous avez créée, puis sélectionnez ellipse **...**.

Pour ajouter l’application à Teams, **sélectionnez Ajouter à Teams**.

:::image type="content" source="../assets/images/collaboration-control/add-to-teams.png" alt-text="Ajouter à Teams":::

La sélection **d’Ajouter à Teams** ouvre une boîte de dialogue dans laquelle vous pouvez consulter les détails et sélectionner **Télécharger l’application**, ce qui enregistre le manifeste de l’application Microsoft Teams sur votre appareil.

:::image type="content" source="../assets/images/collaboration-control/colab-manager-inspection.png" alt-text="La capture d’écran est un exemple montrant l’inspection du gestionnaire de collaboration":::

Pour charger votre application dans Teams, consultez [charger votre application dans Team](~/concepts/deploy-and-publish/apps-upload.md).

## <a name="enable-others-to-use-your-application"></a>Permettre à d’autres utilisateurs d’utiliser votre application

Les éléments suivants sont nécessaires pour permettre aux utilisateurs d’exécuter les applications Gestionnaire de collaboration déployées créées à l’aide des contrôles collaboration :

* Créer une équipe de collaboration
* Ajouter des membres à l’équipe
* Créer un rôle de sécurité
* Attribuer des rôles de sécurité aux membres de l’équipe

### <a name="create-a-collaboration-team"></a>Créer une équipe de collaboration

1. Connectez-vous au [Centre d’administration Power Platform](https://admin.powerplatform.microsoft.com/environments).

     1. Sélectionnez l’environnement dans lequel l’application est déployée.
     1. Sélectionnez **Les autorisations Utilisateurs** +  des  > **paramètres**.
     1. Sélectionnez **Teams**.

1. Sélectionnez le bouton **+ Créer une équipe** en haut de la page.

1. Ajoutez tous les champs requis :
     1. **Nom de l’équipe :** Vérifiez que le nom est unique au sein de l’unité commerciale.
     1. **Description:** Entrez une description de l’équipe.
     1. **Unité commerciale :** Sélectionnez une unité commerciale dans la liste déroulante.
     1. **Administrateur:** Recherchez l’utilisateur au sein de votre organisation que vous souhaitez affecter en tant qu’administrateur en entrant des caractères.
     1. **Type d’équipe :** Sélectionnez le type d’équipe. Les étapes suivantes supposent que vous avez sélectionné Propriétaire dans la liste déroulante. Les autres types d’équipe (équipe Microsoft 365 et équipe Microsoft Azure Active Directory) remplissent automatiquement les membres de l’équipe à partir d’Azure Active Directory.

         :::image type="content" source="../assets/images/collaboration-control/new-team.png" alt-text="Nouvelle équipe":::

     1. Veillez à noter le nom de l’équipe. Vous en aurez besoin ultérieurement pour affecter cette équipe en tant que propriétaire d’un enregistrement.

     1. Sélectionnez **Suivant.**

### <a name="add-members-to-the-team"></a>Ajouter des membres à l’équipe

> [!NOTE]
> L’ajout de membres à l’équipe n’est pas nécessaire si votre type d’équipe est Azure Active Directory ou Microsoft 365.

1. Sélectionnez une équipe, puis **sélectionnez Gérer les membres de l’équipe**.

1. Pour ajouter de nouveaux membres d’équipe, sélectionnez **+ Ajouter des membres d’équipe** et choisissez les utilisateurs de votre organisation à ajouter.

     :::image type="content" source="../assets/images/collaboration-control/add-team-members.png" alt-text="La capture d’écran décrit comment ajouter des membres de l’équipe":::

1. Pour supprimer un membre de l’équipe, sélectionnez l’utilisateur, puis **choisissez Supprimer**.

### <a name="create-a-security-role"></a>Créer un rôle de sécurité

1. Sélectionnez **Paramètres Autorisations** > **utilisateur** +  dans l’environnement dans lequel l’application est déployée.

1. Sélectionnez **Rôles de sécurité**.

     :::image type="content" source="../assets/images/collaboration-control/users-permission.png" alt-text="Autorisation des utilisateurs":::

1. Sélectionnez **Le nouveau rôle** en haut à gauche de la page, qui ouvre maintenant une nouvelle page.

1. Sous **l’onglet Détails**, indiquez un nom pour votre rôle de sécurité.

1. Accédez à l’onglet **Entités personnalisées** .

     1. Accordez des autorisations d’organisation (cercle vert complet) pour chacune des entités de collaboration, **carte** de collaboration, **métadonnées de collaboration** et **racine de collaboration**.

         :::image type="content" source="../assets/images/collaboration-control/collab-map.png" alt-text="Carte de collaboration":::

1. Sélectionnez **Enregistrer** et **fermer**.

### <a name="assign-security-roles"></a>Attribuer des rôles de sécurité

1. Sélectionnez **Paramètres Autorisations** > **utilisateur** +  dans l’environnement dans lequel l’application est déployée.

1. Sélectionnez **Teams**, puis l’équipe que vous avez créée dans [créer une équipe de collaboration](#create-a-collaboration-team).

1. Choisissez **Gérer les rôles de sécurité** dans l’en-tête.

     :::image type="content" source="../assets/images/collaboration-control/edit-team.png" alt-text="Modifier l’équipe":::

1. Sélectionnez les rôles [créés dans un rôle de sécurité](#create-a-security-role).

1. Sélectionnez **Enregistrer**.

Pour plus d’informations sur les privilèges de rôle, consultez [configurer la sécurité des utilisateurs dans un environnement](/power-platform/admin/database-security).
