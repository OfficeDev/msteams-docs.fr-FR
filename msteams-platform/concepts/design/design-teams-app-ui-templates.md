---
title: Conception de votre application avec des modèles d’interface utilisateur
author: heath-hamilton
description: Apprenez à concevoir votre application plus rapidement avec des composants, des dispositions et des modèles d’interface utilisateur standardisés couramment vus dans Microsoft Teams.
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: d6323baf20c733eaddc1e8797a56d63effc45eab
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142898"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur

Concevez votre application Microsoft Teams plus rapidement avec des modèles d’interface utilisateur. Les modèles sont une collection de Fluent composants basés sur l’interface utilisateur qui fonctionnent sur des cas d’utilisation courants Teams, ce qui vous donne plus de temps pour déterminer la meilleure expérience pour vos utilisateurs.

## <a name="getting-started-with-tools-and-samples"></a>Prise en main des outils et des exemples

Les ressources suivantes peuvent vous aider à concevoir et développer votre application à l’aide de modèles d’interface utilisateur.

### <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Récupérez des modèles d’interface utilisateur pour la conception de votre application à partir du kit d’interface utilisateur Microsoft Teams, qui inclut également des informations détaillées sur l’utilisation, l’anatomie, l’accessibilité et les meilleures pratiques.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Bibliothèque d’interface utilisateur Microsoft Teams

Affichez et testez des modèles d’interface utilisateur Teams individuels et des composants associés dans votre navigateur.

> [!div class="nextstepaction"]
> [Essayer la bibliothèque d’interface utilisateur (terrain de jeu)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importez ces modèles et composants associés directement dans votre projet d’application Teams.

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque d’interface utilisateur (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Exemple d’application

Installez un exemple d’application pour voir à quoi ressemblent les modèles d’interface utilisateur et se comportent dans Teams contextes.

> [!div class="nextstepaction"]
> [Obtenir l'application d'exemple (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="calendar"></a>Calendrier

Dans Teams, un calendrier est l’endroit où un utilisateur affiche, planifie et gère les événements à venir et passés pour lui-même ou un groupe.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Planifier des réunions et des événements
* Obtenir des rappels de réunions et d’événements à venir
* Afficher les planifications

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/desktop-calendar.png" alt-text="L’exemple montre un modèle d’interface utilisateur de calendrier sur le bureau." border="false":::

## <a name="dashboard"></a>Tableau de bord

Un tableau de bord affiche différents types de contenu dans un emplacement central (par exemple, une application ou un onglet Teams personnel). Les utilisateurs doivent être en mesure de personnaliser au moins une partie de ce qu’ils voient sur un tableau de bord.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Analyser les données
* Métriques de rapport
* Organiser différentes informations à un seul endroit

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="Exemple montrant un modèle d’interface utilisateur de tableau de bord sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="Exemple montrant un modèle d’interface utilisateur de tableau de bord sur le bureau." border="false":::

## <a name="data-visualization"></a>Visualisation de données

Vous pouvez utiliser différentes tailles de carte (unique, double et complète) pour empiler et organiser des visualisations de données sur la même page. Les cartes sont mises à l’échelle pour s’adapter à la disposition des colonnes et remplir des espaces vides.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Afficher des informations complexes
* Créer un tableau de bord

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="Exemple montrant un modèle d’interface utilisateur de visualisation des données sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="L’exemple montre un modèle d’interface utilisateur de visualisation des données sur le bureau." border="false":::

## <a name="empty-state"></a>État vide

Le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment la connexion, les expériences de première exécution, les messages d’erreur, etc. Il est très flexible: adaptez-le pour utiliser un, quelques-uns ou tous les composants de la conception suivante.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Se connecter
* Messages d’accueil et expériences de première exécution
* Messages de réussite
* Messages d’erreur

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="L’exemple montre un modèle d’interface utilisateur d’état vide sur le bureau." border="false":::

## <a name="filter"></a>Filtre

Un filtre vous permet de réduire les informations que vous voyez en fonction des critères sélectionnés. Vous pouvez inclure des filtres avec des tables, des listes, des cartes et d’autres composants qui organisent le contenu.

### <a name="top-use-cases"></a>Principaux cas d’usage

Organisation du contenu dans :

* Listes
* Tables
* Tableaux de bord
* Visualisation de données

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="L’exemple montre un modèle de filtre." border="false":::

## <a name="form"></a>Formulaire

Les formulaires sont utilisés pour collecter, valider et envoyer des entrées utilisateur de manière structurée. L’étiquetage clair et les regroupements logiques de champs d’entrée sont essentiels pour une bonne expérience utilisateur.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Se connecter
* Profils utilisateur
* Paramètres
* Collection d’entrées utilisateur

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="L’exemple montre un modèle d’interface utilisateur de formulaire sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/form.png" alt-text="L’exemple montre un modèle d’interface utilisateur de formulaire sur le bureau." border="false":::

## <a name="list"></a>Liste

Vous pouvez utiliser une liste pour afficher les éléments associés dans un formatcannable et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Afficher les données
* Actions contextuelles sur le contenu de l’application

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="L’exemple montre un modèle d’interface utilisateur de liste sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="L’exemple montre un modèle d’interface utilisateur de liste sur le bureau." border="false":::

## <a name="sign-in"></a>Se connecter

Vous pouvez concevoir des flux de connexion d’application pour différents contextes Teams et fournisseurs d’identité. L’exemple suivant inclut l’authentification unique (SSO), que nous recommandons pour l’expérience d’authentification la plus simple.

### <a name="top-use-case"></a>Cas d’usage supérieur

* Authentifier les utilisateurs

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de connexion sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="L’exemple montre un modèle d’interface utilisateur de connexion sur le bureau." border="false":::

## <a name="settings"></a>Paramètres

Paramètres écrans permettent aux utilisateurs de configurer leurs préférences avec votre application. (Remarque : Paramètres est un conteneur pour [les composants d’interface utilisateur de base](~/concepts/design/design-teams-app-basic-ui-components.md).)

### <a name="top-use-case"></a>Cas d’usage supérieur

* Gérer les fonctionnalités de l’application

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="L’exemple montre un modèle de paramètres." border="false":::

## <a name="task-board"></a>Tableau des tâches

Un tableau de tâches, parfois appelé tableau kanban ou couloirs de nage, est une collection de cartes souvent utilisées pour suivre l’état des articles de travail ou des billets. Il peut également être utilisé pour trier n’importe quel type de contenu en catégories. Vous pouvez modifier et déplacer les cartes entre les colonnes.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Gestion de projet. Affectation de tâches et état du suivi.
* Brainstorming. Ajout d’idées dans différentes catégories.
* Exercices de tri. Organiser n’importe quel type d’informations en compartiments.

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="Exemple montrant un modèle d’interface utilisateur de tableau des tâches sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="L’exemple montre un modèle d’interface utilisateur de tableau des tâches sur le bureau." border="false":::

## <a name="wizard"></a>Assistant

Un Assistant guide un utilisateur à travers plusieurs écrans pour effectuer une tâche (par exemple, un processus d’installation).

### <a name="top-use-cases"></a>Principaux cas d’usage

* Configuration
* Intégration
* Expériences de première exécution

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="Exemple montrant un modèle d’interface utilisateur de l’Assistant sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="Exemple montrant un modèle d’interface utilisateur de l’Assistant sur le bureau." border="false":::

## <a name="see-also"></a>Voir aussi

* [Concevoir votre application avec des composants d’interface utilisateur Fluent de base](~/concepts/design/design-teams-app-basic-ui-components.md)
* [Conception de votre application Microsoft Teams avec des composants d’interface utilisateur avancés](~/concepts/design/design-teams-app-advanced-ui-components.md)
* [Formatez vos messages robots.](~/bots/how-to/format-your-bot-messages.md)
