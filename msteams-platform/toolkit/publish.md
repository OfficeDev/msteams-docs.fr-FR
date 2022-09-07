---
title: Publier des applications Teams à l’aide du Kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez comment publier des applications Teams à l’aide du Kit de ressources Teams et publier dans une étendue ou une autorisation de chargement indépendant.
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6188072b2d4ca73aae4e7ea91715869d968a9b9c
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616728"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>Publier des applications Teams à l’aide du Kit de ressources Teams

Après avoir créé l’application, vous pouvez distribuer votre application à différentes étendues, telles qu’une personne, une équipe, une organisation ou n’importe qui. La distribution dépend de plusieurs facteurs tels que les besoins, les exigences métier et techniques, ainsi que votre objectif pour l’application. La distribution vers une étendue différente peut nécessiter un processus de révision différent. En général, plus l’étendue est grande, plus l’application doit passer en revue les problèmes de sécurité et de conformité.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish-flow.png" alt-text="flux de publication":::

Voici ce que vous allez apprendre dans cette section :

* [Publier sur une étendue individuelle ou charger une version test](#publish-to-individual-scope-or-sideload-permission)
* [Publier pour votre organisation](#publish-to-your-organization)
* [Publier dans le Microsoft Teams Store](#publish-to-microsoft-teams-store)

## <a name="prerequisites"></a>Configuration requise

* Veillez à créer votre [package d'application](~/concepts/build-and-test/apps-package.md) et [à le valider](https://dev.teams.microsoft.com/appvalidation.html) pour les erreurs.
* [Activez le téléchargement d'applications personnalisées](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) dans Teams.
* Assurez-vous que votre application est en cours d'exécution et accessible via HTTPS.
* Vérifiez que vous avez suivi l’ensemble des instructions de la publication de votre application dans le Microsoft Teams Store pour publier votre application.

## <a name="publish-to-individual-scope-or-sideload-permission"></a>Publier sur une étendue individuelle ou charger une version test

Vous pouvez ajouter une application personnalisée à Teams en chargeant un [package d’application](../concepts/build-and-test/apps-package.md) dans un fichier *.zip directement à une équipe ou dans un contexte personnel. L’ajout d’une application personnalisée en chargeant un package d’application est appelé chargement indépendant. Il vous permet de tester l’application lors du chargement dans Teams. Vous pouvez générer et tester l’application dans les scénarios suivants :

* Testez et déboguez une application localement.
* Créez une application pour vous-même, par exemple pour automatiser un flux de travail.
* Créez une application pour un petit ensemble d’utilisateurs, par exemple, votre groupe de travail.

Vous pouvez créer une application pour une utilisation interne uniquement et la partager avec votre équipe sans l’envoyer au catalogue d’applications Teams dans l’App Store Teams. Pour plus d’informations, consultez [Charger votre application dans Teams](../concepts/deploy-and-publish/apps-upload.md).

### <a name="to-build-your-app-to-zip-app-package-file"></a>Pour générer votre application dans un fichier de package d’application zip

Vous devez d’abord exécuter `Provision in the cloud` avant de générer le package d’application. Les étapes suivantes vous aident à créer le package d’application.

* Sélectionnez **le package de métadonnées Zip Teams** sous **DEPLOYMENT**.<br>
    Le package d’application généré se trouve dans `{your project folder}/build/appPackage/appPackage.{env}.zip`.

### <a name="to-upload-app-package"></a>Pour charger le package d’application

Effectuez les étapes suivantes pour charger le package d’application :

1. Dans le client Teams, sélectionnez **Applications** > **gérer vos applications** > **pour charger une application**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish1.png" alt-text="publier une application":::

   Une fenêtre de **chargement d’application s’affiche**.

2. Sélectionnez **Charger une application personnalisée**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/upload.png" alt-text="charger une application":::

   À présent, l’application est chargée de manière indépendante dans le client Teams et vous pouvez l’ajouter et l’afficher.

## <a name="publish-to-your-organization"></a>Publier pour votre organisation

Lorsque l’application est prête à être utilisée en production, vous pouvez l’envoyer à l’aide de l’API de soumission d’application Teams, appelée à partir de API Graph. L’API de soumission d’applications Teams est un environnement de développement intégré (IDE) tel que Microsoft Visual Studio Code installé avec le kit de ressources Teams. Les étapes suivantes vous aident à publier l’application dans votre organisation :

* [Publier à partir de Teams Toolkit](#publish-from-teams-toolkit)
* [Approuver sur Administration Center](#approve-on-admin-center)

### <a name="publish-from-teams-toolkit"></a>Publier à partir de Teams Toolkit

Les étapes suivantes vous aident à publier l’application à partir du Kit de ressources Teams :

1. Vous pouvez publier votre application Teams de l’une des manières suivantes :
     * Sélectionnez **Publier dans Teams** sous **DÉPLOIEMENT** dans l’arborescence du Kit de ressources Teams.
     * Entrez le déclencheur **Teams : Publier sur Teams à** partir de la palette de commandes.

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-publish.png" alt-text="Sélectionner Publier":::

2 Sélectionnez **Installer pour votre organisation**.

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/installforyourorganization.png" alt-text="Installer pour votre organisation":::

  À présent, l’application est correctement publiée sur le portail d’administration et vous voyez l’avis suivant :

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/confirm-publish.png" alt-text="Confirmer la publication":::

  L’application est désormais disponible dans le Centre d’administration **Gérer les applications** de Microsoft Teams, où vous et l’administrateur pouvez l’examiner et l’approuver.

  > [!NOTE]
  > L’application ne publie pas encore dans l’App Store de votre organisation. L’étape envoie l’application au Centre d’administration Microsoft Teams où vous pouvez l’approuver pour la publication dans l’App Store de votre organisation.

### <a name="approve-on-admin-center"></a>Approuver sur Administration Center

Le kit de ressources Teams pour Visual Studio Code s’appuie sur l’API de soumission d’applications Teams et vous permet d’automatiser le processus de soumission à approbation pour les applications personnalisées sur Teams.

  > [!NOTE]
  > Vérifiez que vous disposez d’un projet d’application Teams dans VS Code. En tant qu’administrateur, **Gérer les applications** dans le centre d’administration [Microsoft Teams](https://admin.teams.microsoft.com/policies/manage-apps) est l’endroit où vous pouvez afficher et gérer toutes les applications Teams pour votre organisation. Vous pouvez effectuer les activités suivantes dans le Centre d’administration :
  >
  > * Consultez l’état au niveau de l’organisation et les propriétés des applications.
  > * Approuvez ou chargez de nouvelles applications personnalisées dans l’App Store de votre organisation.
  > * Bloquez ou autorisez des applications au niveau de l’organisation.
  > * Ajoutez des applications à Teams.
  > * Acheter des services pour des applications tierces.
  > * Afficher les autorisations demandées par les applications.
  > * Accordez le consentement administrateur aux applications.
  > * [Gérer les paramètres d’application à l’échelle de l’organisation](https://admin.teams.microsoft.com/policies/manage-apps).

Les étapes suivantes vous aident à approuver à partir de Administration Center :

1. Sélectionnez **Accéder au portail d’administration**.

1. Sélectionnez l’icône :::image type="icon" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Showall.PNG"::: > application **Teams** > **Gérer les applications**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manage-apps.png" alt-text="Sélectionnez Gérer les applications":::

   Vous pouvez afficher toutes les applications Teams pour votre organisation.

   Dans le widget d’approbation en attente en haut de la page, vous savez quand une application personnalisée est soumise pour approbation. Dans le tableau, une application nouvellement soumise publie automatiquement l’état des applications soumises et bloquées. Vous pouvez trier la colonne d’état de publication dans l’ordre décroissant pour trouver l’application.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="Approbation":::

1. Sélectionnez le nom de l’application pour accéder à la page des détails de l’application. Sous l’onglet **À propos** , vous pouvez afficher des détails sur l’application, notamment la description, l’état et l’ID d’application.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="Application soumise":::

1. Sélectionnez la liste déroulante d’état et passez de **Soumis** à **Publier**.

   Après avoir publié l’application, l’état de publication devient publié et l’état devient automatiquement autorisé.

   Pour plus d’informations, consultez [Publier sur votre organisation](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json)

## <a name="publish-to-microsoft-teams-store"></a>Publier dans le Microsoft Teams Store

Vous pouvez distribuer votre application directement dans le Store au sein de Microsoft Teams et atteindre des millions d’utilisateurs dans le monde entier. Si votre application est également proposée dans le Store, vous pouvez atteindre instantanément les clients potentiels. Les applications publiées dans le magasin Teams sont également répertoriées automatiquement sur Microsoft AppSource, qui est la place de marché officielle pour Microsoft 365 applications et solutions.

Pour plus d’informations, consultez [Publier votre application sur le Microsoft Teams Store](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store).

## <a name="see-also"></a>Voir aussi

* [Distribuer votre application Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md)
* [Créer un package d’application Teams](../concepts/build-and-test/apps-package.md)
* [Préparer votre client Microsoft Office 365](../concepts/build-and-test/prepare-your-o365-tenant.md)
* [Publiez votre application dans le store Microsoft Teams.](../concepts/deploy-and-publish/appsource/publish.md)
* [Charger votre application dans Teams](../concepts/deploy-and-publish/apps-upload.md)
* [Gérer l’application Teams dans le Centre d’administration Microsoft Teams](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json)
