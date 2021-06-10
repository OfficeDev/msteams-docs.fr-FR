---
title: Conception de votre application avec des modèles d’interface utilisateur
author: heath-hamilton
description: Concevez votre application plus rapidement avec des composants d’interface utilisateur, des dispositions et des modèles standardisés fréquemment visibles dans Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 5026554070396dcc55390496b6754961e8e037bc
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644815"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur

Concevez votre application Microsoft Teams plus rapidement avec des modèles d’interface utilisateur. Les modèles sont une collection de composants fluent basés sur l’interface utilisateur qui fonctionnent dans les cas d’utilisation courants Teams, ce qui vous donne plus de temps pour déterminer la meilleure expérience pour vos utilisateurs.

## <a name="getting-started-with-tools-and-samples"></a>Mise en place des outils et des exemples

Les ressources suivantes peuvent vous aider à concevoir et développer votre application à l’aide de modèles d’interface utilisateur.

### <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Récupérer des modèles d’interface utilisateur pour la conception de votre application à partir du kit d’interface utilisateur Microsoft Teams, qui inclut également des informations complètes sur l’utilisation, l’anatomie, l’accessibilité et les meilleures pratiques.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams Bibliothèque d’interface utilisateur

Affichez et testez les Teams d’interface utilisateur et les composants associés dans votre navigateur.

> [!div class="nextstepaction"]
> [Essayer la bibliothèque d’interface utilisateur (aire de jeu)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importez ces modèles et composants associés directement dans Teams projet d’application.

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque d’interface utilisateur (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Exemple d’application

Installez un exemple d’application pour voir l’apparence et le comportement des modèles d’interface utilisateur Teams contextes.

> [!div class="nextstepaction"]
> [Obtenir l’exemple d’application (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a>Tableau de bord

Un tableau de bord affiche différents types de contenu dans un emplacement central (Teams application ou onglet personnel). Les utilisateurs doivent pouvoir personnaliser au moins une partie de ce qu’ils voient sur un tableau de bord.

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Analyser les données
* Mesures du rapport
* Organiser différentes informations au même endroit

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="L’exemple montre un modèle d’interface utilisateur de tableau de bord sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="L’exemple montre un modèle d’interface utilisateur de tableau de bord sur mobile." border="false":::

---

## <a name="data-visualization"></a>Visualisation de données

Vous pouvez utiliser différentes tailles de carte (unique, double et complète) pour empiler et organiser les visualisations de données sur la même page. Les cartes s’adaptent à la disposition des colonnes et remplissent des espaces vides.

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Afficher des informations complexes
* Créer un tableau de bord

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="L’exemple illustre un modèle d’interface utilisateur de visualisation de données sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="L’exemple montre un modèle d’interface utilisateur de visualisation de données sur un appareil mobile." border="false":::

---

## <a name="empty-state"></a>État vide

Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc. Il est très flexible : adaptez-le pour utiliser un, quelques-uns ou tous les composants de la conception suivante.

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Se connecter
* Messages de bienvenue et expériences de première expérience
* Messages de réussite
* Messages d’erreur

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide sur mobile." border="false":::

---

## <a name="filter"></a>Filtre

Un filtre vous permet de réduire les informations que vous voyez en fonction des critères sélectionnés. Vous pouvez inclure des filtres avec des tableaux, des listes, des cartes et d’autres composants qui organisent le contenu.

### <a name="top-use-cases"></a>Principaux cas d’utilisation

Organisation du contenu dans :

* Listes
* Tables
* Tableaux de bord
* Visualisation de données

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="Exemple de modèle de filtre." border="false":::

## <a name="form"></a>Formulaire

Les formulaires sont utilisés pour collecter, valider et envoyer des entrées utilisateur de manière structurée. Effacer l’étiquetage et les regroupements logiques de champs d’entrée sont essentiels pour une bonne expérience utilisateur.

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Se connecter
* Profils utilisateur
* Paramètres
* Collection d’entrées utilisateur

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="L’exemple montre un modèle d’interface utilisateur de formulaire sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="L’exemple montre un modèle d’interface utilisateur de formulaire sur mobile." border="false":::

---

## <a name="list"></a>Répertorier

Vous pouvez utiliser une liste pour afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Afficher les données
* Actions contextuelles sur le contenu de l’application

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="L’exemple montre un modèle d’interface utilisateur de liste sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="L’exemple montre un modèle d’interface utilisateur de liste sur mobile." border="false":::

---

## <a name="sign-in"></a>Se connecter

Vous pouvez concevoir des flux de Teams d’application pour différents contextes et fournisseurs d’identité. L’exemple suivant inclut l’authentification unique (SSO), que nous recommandons pour l’expérience d’authentification la plus simple.

### <a name="top-use-case"></a>Cas d’utilisation principaux

* Authentifier les utilisateurs

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de la signature sur le bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de la signature sur un appareil mobile." border="false":::

---

## <a name="settings"></a>Paramètres

Paramètres sont les écrans où les utilisateurs peuvent configurer leurs préférences avec votre application. (Remarque : Paramètres est un conteneur pour les [composants d’interface utilisateur de base.)](~/concepts/design/design-teams-app-basic-ui-components.md)

### <a name="top-use-case"></a>Cas d’utilisation principaux

* Gérer les fonctionnalités de l’application

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="L’exemple montre un modèle de paramètres." border="false":::

## <a name="task-board"></a>Tableau des tâches

Un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets. Il peut également être utilisé pour trier n’importe quel type de contenu en catégories. Vous pouvez modifier et déplacer les cartes entre les colonnes.

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Gestion de projet. Affectation de tâches et état de suivi
* Brainstorming. Ajout d’idées dans différentes catégories
* Exercices de tri. Organisation de n’importe quel type d’informations dans des compartiments

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="L’exemple montre un modèle d’interface utilisateur du tableau des tâches sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="L’exemple montre un modèle d’interface utilisateur du tableau des tâches sur mobile." border="false":::

---

## <a name="wizard"></a>Assistant

Un Assistant guide un utilisateur à travers plusieurs écrans pour effectuer une tâche (par exemple, un processus d’installation).

### <a name="top-use-cases"></a>Principaux cas d’utilisation

* Configuration
* Intégration
* Expériences de première expérience

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="Un exemple illustre un modèle d’interface utilisateur d’Assistant sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’assistant sur mobile." border="false":::

---
