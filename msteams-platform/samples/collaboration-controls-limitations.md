---
title: Limitations et problèmes connus dans l’application de contrôle Collaboration
author: surbhigupta
description: Dans ce module, découvrez les limitations et les problèmes connus dans l’application De contrôles de collaboration pour Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 6961b5fc51cc8aa2a2ad0620c8a8ef5032005f40
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179018"
---
# <a name="limitations-and-known-issues"></a>Limitations et problèmes connus

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

Voici les limitations des contrôles de collaboration :

* Les composants ne peuvent pas être utilisés dans les applications Canvas.
* Les composants prennent uniquement en charge les affichages d’onglets complets.

     :::image type="content" source="../assets/images/collaboration-control/tasks-tab.png" alt-text="tâches" border="true":::

* La vue sous-engrid sélectionnée n’est pas honorée. Toutes les tâches, réunions ou notes de l’enregistrement collaboratif s’affichent.

     :::image type="content" source="../assets/images/collaboration-control/subgrid-view.png" alt-text="vue subgrid" border= "true":::

* Les activités ajoutées au contrôle de chronologie n’apparaissent pas dans les composants, les tâches, les réunions et les notes créés dans les composants ne sont pas inclus dans le contrôle de chronologie.
* Les nouveaux enregistrements doivent être enregistrés avant d’accéder aux composants. Sinon, un écran vide s’affiche.
* Les composants n’héritent pas des thèmes du formulaire ou de l’application auquel ils sont ajoutés.
* La localisation est disponible uniquement lors de l’exécution de l’application dans Microsoft Teams.
* Le mode strict Microsoft Edge n’est pas pris en charge et les cookies intersites sont requis.

**Administration Center ne se met pas à jour lorsque l’installation ou la mise à niveau est terminée**

Lorsque vous suivez les étapes d’installation des [contrôles Collaboration](~/samples/install-collaboration-control.md), vous êtes redirigé vers le Centre d’administration Power Platform. Une bannière s’affiche au démarrage de l’installation, mais elle n’est pas mise à jour à la fin de l’installation. L’état est répertorié pendant l’installation et, une fois l’installation terminée, il peut disparaître de la liste. Vous pouvez afficher la liste des solutions pour [https://make.powerapps.com/](https://make.preview.powerapps.com/) vérifier que l’installation est terminée.

**Afficher pendant l’installation :** :::image type="content" source="../assets/images/collaboration-control/view-during-installation.png" alt-text="afficher pendant l’installation" border="true":::

**Afficher après l’installation :** :::image type="content" source="../assets/images/collaboration-control/view-after-installation.png" alt-text="afficher après l’installation" border="true":::

Lors de la mise à niveau des contrôles vers une version ultérieure, la même bannière de démarrage de l’installation s’affiche, mais l’état du contrôle reste installé même une fois la mise à niveau terminée. Vous pouvez vérifier que la mise à niveau est terminée en vérifiant la liste des solutions dans [https://make.powerapps.com/](https://make.preview.powerapps.com/)laquelle elle doit prendre environ 15 minutes.

Vous pouvez également voir dans l’historique des solutions spécifiques que la version ultérieure a été installée, puis que la version précédente a été supprimée : :::image type="content" source="../assets/images/collaboration-control/history.png" alt-text="Vérification de l’historique" border="true":::

## <a name="bookings-meetings"></a>Réservations de réunions

Le contrôle Réunions prend en charge une réunion sur une lors de l’utilisation de Bookings pour interagir avec des utilisateurs extérieurs à votre organisation. Une à plusieurs réunions ne sont pas prises en charge à l’heure actuelle à l’aide de contrôles collaboration.

**L’état du participant à la réunion est incorrect**

Lorsqu’un participant participe à une réunion, son état de réponse peut ne pas s’afficher correctement dans l’affichage de l’ordre du jour et dans les détails de la réunion. La sélection du bouton Refuser peut également renvoyer un message d’erreur à l’écran.

## <a name="tasks"></a>Tâches

**Tâches : Le texte « clair » de filtre n’est pas traduit**

Le texte du bouton « Effacer » affiché sur le filtre Tâches n’est pas traduit.

**Tâches : le menu contextuel grille s’affiche rogné**

Quand, la grille Tâches est remplie par un petit nombre de tâches, le menu contextuel de la grille peut apparaître rogné et nécessiter l’utilisation de barres de défilement.

**Tâches : le filtre de recherche par mot clé utilise l’opérateur « BeginsWith » pour les tâches « Guest »**

Lorsque vous recherchez des tâches à l’aide du filtre de texte par mot clé, les tâches « Invité » sont retournées à l’aide de l’opérateur « BeginsWith ». Les tâches « Membre » sont retournées à l’aide de l’opérateur « Contains ».

## <a name="files"></a>Fichiers

Lors de la navigation dans le dossier Archive après l’archivage des fichiers, les utilisateurs peuvent rencontrer des dossiers d’archivage en double.  La navigation entre le ou les dossiers d’archivage et la vue principale des fichiers résout le problème et les fichiers archivés ne seront pas supprimés.

## <a name="controls"></a>Contrôles

**Échec de l’enregistrement des contrôles**

Si un contrôle ne parvient pas à enregistrer une tâche ou une réunion, la cause probable est un ID de groupe ou un ID de canal mal configuré.  

Solution 1 : Vérifiez que les ID sont corrects et que les paramètres ont été appliqués conformément à l’exercice de paramètres.  

Solution 2 : Essayez de vous assurer que l’environnement Power Apps et l’environnement Teams se trouvent sur le même locataire.  

**Échec du chargement des contrôles ou affichage d’une erreur**

Si les contrôles ne parviennent pas à se charger ou à afficher une erreur, il peut s’agir d’un problème temporaire.

Exemple :

:::image type="content" source="../assets/images/collaboration-control/sync-fail.png" alt-text="échec de la synchronisation des contrôles":::

Cela s’affiche dans le journal de la console comme suit :

:::image type="content" source="../assets/images/collaboration-control/control-fail.png" alt-text="échec du contrôle" border="true":::

Solution : actualisez votre navigateur ou, dans l’application Teams, rechargez l’onglet.

Si vous souhaitez modifier le nom, l’icône ou la description de l’application après son chargement dans Teams, consultez [personnaliser l’apparence des applications](/MicrosoftTeams/customize-apps#customize-details-of-an-app)

## <a name="error-logging"></a>Enregistrement des erreurs

Les contrôles fournissent les méthodes suivantes pour déboguer votre application.

1. **Journalisation du suivi** des événements de plug-in lorsqu’une API est appelée. Ces informations sont stockées dans votre environnement Dataverse.

    1. Pour activer la journalisation des traces, procédez comme suit dans [la journalisation et le suivi](/power-apps/developer/data-platform/logging-tracing?WT.mc_id=email).

1. **Journalisation du navigateur** pour les contrôles d’interface utilisateur. Il s’agit de la journalisation de la console standard.

    1. Il est pris en charge lors de l’utilisation d’un navigateur pour exécuter l’application Gestionnaire de collaboration via Power Platform et teams web.
    1. Dans l’onglet console, vous pouvez rechercher des erreurs à l’aide du message d’erreur Gestionnaire de collaboration ou à la recherche de noms de contrôle Gestionnaire de collaboration tels que Tâches.

> [!TIP]
> Si une erreur se produit dans un client de bureau Teams, essayez de répliquer dans le web Teams pour capturer le journal des erreurs.

## <a name="faq"></a>FAQ

<br>

<details>

<summary><b>Que sont les contrôles collaboration (préversion) ?</b></summary>

Les contrôles de collaboration (préversion) vous permettent d’ajouter des fonctionnalités Microsoft 365 à vos applications personnalisées métier Power Apps pour simplifier les flux de travail utilisateur lors de la collaboration sur des processus métier dans Teams ou Power Apps.

<br>

</details>

<br>

<details>

<summary><b>Quel est l’avantage des contrôles collaboration (préversion) pour les créateurs ?</b></summary>

Avec ces nouveaux contrôles, vous pouvez en tant que créateur glisser-déplacer des contrôles qui permettent à Microsoft 365 Collaboration d’accéder à votre application.

<br>

</details>

<br>

<details>

<summary><b>Quel est l’avantage des contrôles collaboration (préversion) pour les utilisateurs ?</b></summary>

Vos utilisateurs peuvent constater des gains de productivité et rester dans leur flux en collaborant sur des approbations, des fichiers, des réunions, des notes et des tâches sans quitter le contexte de votre application.

<br>

</details>

<br>

<details>

<summary><b>Comment faire accéder aux contrôles collaboration (préversion) ?</b></summary>

Demandez à votre administrateur Power Platform d’installer les contrôles d’AppSource vers votre environnement Power Apps.

<br>

</details>

<br>

<details>

<summary><b>Comment faire ajouter les contrôles à une application basée sur des modèles ?</b></summary>

Accédez au Concepteur de formulaires et faites glisser les contrôles du volet Composant vers un formulaire.

<br>

</details>
