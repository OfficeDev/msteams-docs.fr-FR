---
title: Conception de votre application avec des modèles d’interface utilisateur
author: heath-hamilton
description: Concevez votre application plus rapidement avec des composants d’interface utilisateur standardisés, des dispositions et des modèles couramment rencontrés dans Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: b4d244bbf78ac85042d5caf8ec84afe42e79b3c7
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911925"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur

Concevez votre application Microsoft Teams plus rapidement avec des modèles d’interface utilisateur. Les modèles sont un ensemble de composants Basés sur l’interface utilisateur Fluent qui fonctionnent dans les cas d’utilisation courants de Teams, ce qui vous donne plus de temps pour déterminer la meilleure expérience pour vos utilisateurs.

## <a name="getting-started-with-tools-and-samples"></a>Mise en place d’outils et d’exemples

Les ressources suivantes peuvent vous aider à concevoir et développer votre application à l’aide de modèles d’interface utilisateur.

### <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur Microsoft Teams

Récupérer des modèles d’interface utilisateur pour la conception de votre application à partir du Kit d’interface utilisateur Microsoft Teams, qui inclut également des informations complètes sur l’utilisation, l’anatomie, l’accessibilité et les meilleures pratiques.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Bibliothèque d’interface utilisateur Microsoft Teams

Affichez et testez des modèles d’interface utilisateur Teams individuels et des composants associés dans votre navigateur.

> [!div class="nextstepaction"]
> [Essayer la bibliothèque d’interface utilisateur (aire de jeu)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importez ces modèles et composants associés directement dans votre projet d’application Teams.

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque d’interface utilisateur (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Exemple d’application

Installez un exemple d’application pour voir l’apparence et le comportement des modèles d’interface utilisateur dans les contextes Teams.

> [!div class="nextstepaction"]
> [Obtenir l’exemple d’application (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a>Répertorier

Vous pouvez utiliser une liste pour afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="Exemple de modèle d’interface utilisateur de liste." border="false":::

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Afficher les données
* Actions contextuelles sur le contenu de l’application

## <a name="dashboard"></a>Tableau de bord

Un tableau de bord affiche différents types de contenu dans un emplacement central (application ou onglet personnel Teams). Les utilisateurs doivent pouvoir personnaliser au moins une partie de ce qu’ils voient sur un tableau de bord.

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="Exemple de modèle d’interface utilisateur de tableau de bord." border="false":::

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Analyser les données
* Mesures du rapport
* Organiser différentes informations au même endroit

## <a name="form"></a>Formulaire

Les formulaires sont utilisés pour collecter, valider et envoyer des entrées utilisateur de manière structurée. L’étiquetage clair et les regroupements logiques de champs d’entrée sont essentiels pour une bonne expérience utilisateur.

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="Exemple de modèle d’interface utilisateur de formulaire." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Connexion
* Profils utilisateur
* Paramètres
* Collection d’entrées utilisateur

## <a name="sign-in"></a>Connexion

Vous pouvez concevoir des flux de signature d’application pour différents contextes teams et fournisseurs d’identité. L’exemple suivant inclut l’authentification unique (SSO), que nous vous recommandons pour l’expérience d’authentification la plus simple.

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de la signature." border="false":::

### <a name="top-use-case"></a>Cas d’utilisation principaux

* Authentifier les utilisateurs

## <a name="task-board"></a>Tableau des tâches

Un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets. Il peut également être utilisé pour trier n’importe quel type de contenu en catégories. Vous pouvez modifier et déplacer les cartes entre les colonnes.

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="Exemple de modèle d’interface utilisateur du tableau des tâches." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Gestion de projet. Affectation de tâches et état de suivi
* Brainstorming. Ajout d’idées dans différentes catégories
* Exercices de tri. Organisation de n’importe quel type d’informations dans des compartiments

## <a name="data-visualization"></a>Visualisation de données

Vous pouvez utiliser différentes tailles de carte (unique, double et complète) pour empiler et organiser les visualisations de données sur la même page. Les cartes s’adaptent à la disposition des colonnes et remplissent des espaces vides.

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="Exemple de modèle d’interface utilisateur de visualisation de données." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Afficher des informations complexes
* Créer un tableau de bord

## <a name="wizard"></a>Assistant

Un Assistant guide un utilisateur à travers plusieurs écrans pour effectuer une tâche (par exemple, un processus d’installation).

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="Exemple de modèle d’interface utilisateur assistant." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Configuration
* Intégration
* Expériences de première expérience

## <a name="empty-state"></a>État vide

Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc. Il est très flexible : adaptez-le pour utiliser un, quelques-uns ou tous les composants de la conception suivante.

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide." border="false":::

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Connexion
* Messages de bienvenue et expériences de première expérience
* Messages de réussite
* Messages d’erreur

## <a name="notification-bar"></a>Barre de notification

Une barre de notification est une zone dédiée à l’affichage de messages brefs et importants qui ne nécessitent pas que l’utilisateur prenne des mesures immédiates. Des icônes et couleurs d’arrière-plan spécifiques sont associées à des types de messages spécifiques (voir ci-dessous).

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="Exemple de modèles de barre de notification." border="false":::

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Messages critiques, erreurs et avertissements
* Messages de réussite
* Messages d’information ou promotionnels

## <a name="left-nav"></a>Navigation gauche

Utilisez le navigation de gauche pour parcourir plusieurs pages dans votre onglet Teams. Dans l’exemple suivant, le navigation gauche se trouve entre la liste de canaux et le contenu de l’onglet.

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="Exemple de modèle de navigation gauche." border="false":::

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Parcourir plusieurs pages dans un onglet Teams
* Décomposer les applications complexes en plusieurs pages

## <a name="breadcrumb"></a>Barre de navigation

Les barre de navigation sont une aide à la navigation qui véhicule la hiérarchie de votre application. Ils aident les utilisateurs à comprendre comment la page qu’ils affichent s’intègre à l’expérience globale et offrent un accès en un clic aux niveaux supérieurs de cette hiérarchie.

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="Exemple de modèle de lacrumb." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Hiérarchie de communication
* Navigation

## <a name="toolbar"></a>Barre d'outils

Une barre d’outils est un conteneur permettant de grouper un ensemble de contrôles.

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="Exemple de modèle de barre d’outils." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Actions contextuelles sur le contenu de l’application
* Filtre contextuel et recherche
* Navigation et barre de navigation

## <a name="stage"></a>Phase

L’étape permet aux utilisateurs d’ouvrir une entité (par exemple, une image, un fichier ou un site web) dans Teams au lieu de l’ouvrir dans une autre application ou navigateur. Le cas d’utilisation principal de l’étape est l’affichage ; la surface ne doit pas être utilisée pour des interactions complexes.

(Remarque d’implémentation : créez votre étape à l’aide d’un [module de tâche de grande taille.)](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="Exemple de modèle d’étape." border="false":::

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Ouvrir une entité dans Teams au lieu d’une autre application ou navigateur
* Média à la une ou autre contenu
