---
title: Conception de votre application avec des modèles d’interface utilisateur
author: heath-hamilton
description: Concevez votre application plus rapidement avec des composants d’interface utilisateur normalisés, des mises en page et des motifs couramment observés dans Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 0cd5c6c4525e340f9aa53a78749211783880225a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566018"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur

Concevez votre application Microsoft Teams plus rapidement avec des modèles d’interface utilisateur. Les modèles sont une collection de composants fluent basés sur l’interface utilisateur qui fonctionnent dans des cas d’utilisation de Teams communs, vous donnant plus de temps pour trouver la meilleure expérience pour vos utilisateurs.

## <a name="getting-started-with-tools-and-samples"></a>Commencer avec des outils et des échantillons

Les ressources suivantes peuvent vous aider à concevoir et développer votre application à l’aide de modèles d’interface utilisateur.

### <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Prenez des modèles d’interface utilisateur pour la conception de votre application à partir de la trousse d’interface utilisateur Microsoft Teams, qui comprend également des informations détaillées sur l’utilisation, l’anatomie, l’accessibilité et les meilleures pratiques.

> [!div class="nextstepaction"]
> [Obtenez le kit d’interface utilisateur (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams Bibliothèque d’interface utilisateur

Visualisez et testez les Teams d’interface utilisateur et les composants connexes de votre navigateur.

> [!div class="nextstepaction"]
> [Essayez la bibliothèque d’interface utilisateur (aire de jeux)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importez ces modèles et composants connexes directement dans votre projet d Teams appe.

> [!div class="nextstepaction"]
> [Obtenez la bibliothèque d’interface utilisateur (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Exemple d’application

Installez une application d’exemple pour voir à quoi ressemblent et se comportent les modèles d’interface utilisateur Teams contextes.

> [!div class="nextstepaction"]
> [Obtenez l’exemple d’application (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a>Répertorier

Vous pouvez utiliser une liste pour afficher des éléments connexes dans un format scannable et permettre aux utilisateurs de prendre des mesures sur une liste entière ou des éléments individuels.

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="Exemple montre un modèle d’interface utilisateur de liste." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Afficher les données
* Actions contextuelles sur le contenu de l’application

## <a name="dashboard"></a>Tableau de bord

Un tableau de bord affiche différents types de contenu dans un emplacement central (Teams ou onglet personnel). Les utilisateurs devraient être en mesure de personnaliser au moins une partie de ce qu’ils voient sur un tableau de bord.

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="Exemple montre un modèle d’interface utilisateur de tableau de bord." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Analyser les données
* Indicateurs de rapport
* Organiser différentes informations en un seul endroit

## <a name="form"></a>Formulaire

Les formulaires sont utilisés pour recueillir, valider et soumettre les commentaires des utilisateurs de manière structurée. L’étiquetage clair et les regroupements logiques de champs d’entrée sont essentiels pour une bonne expérience utilisateur.

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="Exemple montre un modèle d’interface utilisateur de formulaire." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Se connecter
* Profils utilisateur
* Paramètres
* Collecte d’entrées utilisateur

## <a name="sign-in"></a>Se connecter

Vous pouvez concevoir des flux de connecte d’applications pour différents Teams et fournisseurs d’identité. L’exemple suivant inclut une seule inscription (SSO), que nous recommandons pour l’expérience d’authentification la plus simple.

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="Exemple montre un signe dans le modèle d’interface utilisateur." border="false":::

### <a name="top-use-case"></a>Cas d’utilisation supérieure

* Authentifier les utilisateurs

## <a name="task-board"></a>Tableau de travail

Un tableau de travail, parfois appelé un conseil kanban ou des voies de baignade, est une collection de cartes souvent utilisées pour suivre l’état des articles de travail ou des billets. Il peut également être utilisé pour trier n’importe quel type de contenu en catégories. Vous pouvez modifier et déplacer les cartes entre les colonnes.

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="Exemple montre un modèle d’interface utilisateur du tableau de tâches." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Project : Attribution des tâches et statut de suivi.
* Remue-méninges : Ajout d’idées dans différentes catégories.
* Exercices de tri : Organiser n’importe quel type d’information en seaux.

## <a name="data-visualization"></a>Visualisation de données

Vous pouvez utiliser différentes tailles de carte (simple, double et complète) pour empiler et organiser des visualisations de données sur la même page. L’échelle des cartes pour s’adapter à la disposition de la colonne et remplir les espaces vides.

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="Exemple montre un modèle d’interface utilisateur de visualisation de données." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Afficher des informations complexes
* Créer un tableau de bord

## <a name="wizard"></a>Assistant

Un assistant guide un utilisateur à travers plusieurs écrans pour accomplir une tâche (comme un processus d’installation).

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="Exemple montre un modèle d’interface utilisateur assistant." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Configuration
* Intégration
* Expériences de première manche

## <a name="empty-state"></a>État vide

Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la dé connecte, les expériences de première série, les messages d’erreur, et plus encore. Il est très flexible : adaptez-le pour utiliser un, quelques-uns ou tous les composants de la conception suivante.

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="Exemple montre un modèle d’interface utilisateur à l’état vide." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Se connecter
* Messages de bienvenue et expériences de première série
* Messages de réussite
* Messages d’erreur

## <a name="notification-bar"></a>Barre de notification

Une barre de notification est un espace dédié à l’affichage d’un message bref et important qui n’oblige pas l’utilisateur à prendre des mesures immédiates. Des couleurs et des icônes d’arrière-plan spécifiques sont associées à des types spécifiques de messages (voir ci-dessous).

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="Exemple montre les modèles de barre de notification." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Messages critiques, erreurs et avertissements
* Messages de réussite
* Messages d’information ou promotionnels

## <a name="left-nav"></a>Navigation gauche

Utilisez la navigation gauche pour parcourir plusieurs pages dans votre onglet Teams gauche. Dans l’exemple suivant, la navigation de gauche se situe entre la liste des canaux et le contenu de l’onglet.

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="Exemple montre un modèle de navigation gauche." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Parcourez plusieurs pages dans un onglet Teams’utilisateur.
* Décomposez les applications complexes en plusieurs pages.

## <a name="breadcrumb"></a>Barre de navigation

La chapelure est une aide à la navigation qui transmet la hiérarchie de votre application. Ils aident les utilisateurs à comprendre comment la page qu’ils consultent s’inscrit dans l’expérience globale et permettent un accès en un clic à des niveaux plus élevés dans cette hiérarchie.

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="Exemple montre un modèle de chapelure." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Communiquer la hiérarchie
* Navigation

## <a name="toolbar"></a>Barre d'outils

Une barre d’outils est un conteneur pour regrouper un ensemble de contrôles.

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="Exemple montre un modèle de barre d’outils." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Actions contextuelles sur le contenu de l’application
* Filtre contextuel et trouver
* Navigation et chapelure

## <a name="stage"></a>Phase

Stage offre aux utilisateurs un moyen d’ouvrir une entité , comme une image, un fichier ou un site Web - en Teams au lieu de l’ouvrir dans une autre application ou navigateur. Le cas d’utilisation primaire de l’étape est le visionnement ; la surface ne doit pas être utilisée pour des interactions complexes.

(Note de mise en œuvre : Construisez votre étape à l’aide d’un [grand module de](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)tâches.)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="Exemple montre un modèle d’étape." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation supérieure

* Ouvrez une entité dans Teams au lieu d’une autre application ou navigateur.
* Braquez les projecteurs sur les médias ou d’autres contenus.
