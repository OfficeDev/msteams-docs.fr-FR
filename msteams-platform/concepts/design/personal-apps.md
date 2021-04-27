---
title: Conception de votre application personnelle
description: Découvrez comment concevoir une application personnelle Teams et obtenir le Kit d'interface utilisateur Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 8302f3768034014ef5a446effeee0603afe4a5f4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020757"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Conception de votre application personnelle pour Microsoft Teams

Une application personnelle peut être un bot, un espace de travail privé ou les deux. Parfois, il fonctionne comme un endroit pour créer ou afficher du contenu, d'autres fois, il offre à l'utilisateur une vue d'ensemble de tout ce qui lui est propre lorsque l'application a été configurée sous la forme d'un onglet dans plusieurs canaux.

Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des applications personnelles dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions complètes sur la conception d'applications personnelles, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d'interface utilisateur Microsoft Teams. Le kit d'interface utilisateur contient également des rubriques essentielles telles que l'accessibilité et le resserrement réactif qui ne sont pas abordés ici.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Ajouter une application personnelle

Vous pouvez ajouter une application personnelle à partir du magasin Teams (AppSource) ou du flyout de l'application en sélectionnant l'icône Plus sur le côté gauche de Teams (illustré dans l'exemple suivant). 

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="L'exemple montre comment ajouter une application personnelle à partir du flyout de l'application." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Utiliser une application personnelle (espace de travail privé)

Avec un espace de travail privé, vous pouvez afficher le contenu de l'application qui vous semble significatif dans un emplacement central sans quitter Teams.

(Remarque d'implémentation : l'espace de travail privé est basé sur la [*fonctionnalité d'onglet*](../../build-your-first-app/build-personal-tab.md) personnel.)

### <a name="anatomy-personal-app-private-workspace"></a>Anatomie : application personnelle (espace de travail privé)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="L'exemple montre l'anatomie des composants de l'onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Attribution de l'application**: nom et logo de votre application.|
|B|**Onglets :** fournit la navigation pour votre application personnelle. Par exemple, incluez un **onglet À** propos de ou **Aide.**|
|C|**Affichage popout :** pousse le contenu de votre application d'une fenêtre parent vers une fenêtre enfant autonome.|
|D|**Menu supplémentaire**: inclut des informations et options supplémentaires sur l'application. (Vous pouvez également définir **Paramètres en** onglet.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="L'exemple montre l'anatomie structurelle de l'onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Onglets :** fournit la navigation pour votre application personnelle.|
|1|**iframe**: affiche le contenu de votre application.|

### <a name="designing-with-ui-templates"></a>Conception avec des modèles d'interface utilisateur

Utilisez l'un des modèles d'interface utilisateur Teams suivants pour vous aider à concevoir votre onglet personnel :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d'agir sur une liste entière ou sur des éléments individuels.
* [Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l'état des éléments de travail ou des tickets.
* [Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d'ensemble des données ou du contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d'état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d'erreur, etc.
* [Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation. En règle générale, vous devez conserver la navigation par onglets au minimum.

## <a name="use-a-personal-app-bot"></a>Utiliser une application personnelle (bot)

Les applications personnelles peuvent inclure un bot pour les conversations un-à-un et des notifications privées (par exemple, lorsqu'un collègue publie un commentaire sur votre tableau de bord). Le bot est disponible dans un onglet que vous spécifiez.

### <a name="anatomy-personal-app-bot"></a>Anatomie : application personnelle (bot)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="L'exemple montre l'anatomie des composants personnels du bot." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Onglet Bot**: par exemple, incluez un onglet **Conversation** pour accéder aux conversations et notifications des bots.|
|B|**Message du bot**: les bots envoient souvent des messages et des notifications sous la forme d'une carte (par exemple, une carte adaptative).|
|C|**Zone de composition**: champ d'entrée pour l'envoi de messages au bot.|

## <a name="best-practices"></a>Meilleures pratiques

### <a name="tab-priority"></a>Priorité de l'onglet

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>À faire : afficher le contenu le plus pertinent dans le premier onglet

Avec le resserré réactif, les onglets de droite peuvent être tronqués ou en dehors de la vue.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="L'exemple illustre les meilleures pratiques d'une application personnelle." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>À ne pas faire : diriger avec du contenu ou des métadonnées secondaires

À l'exemple d'une application web standard, la navigation par onglets doit s'effectuer dans un ordre qui vous aide à prendre en compte les principales fonctionnalités de votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Exemple de meilleure pratique pour une application personnelle." border="false":::

### <a name="tab-hierarchy"></a>Hiérarchie d'onglets

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>À faire : les onglets doivent être de hiérarchie égale et représenter des pages d'application clés

Vos onglets doivent catégoriser les principales fonctionnalités et le contenu de votre application. Avec le resserré réactif, le contenu à droite peut être tronqué ou hors de vue.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="L'exemple illustre les meilleures pratiques d'application personnelle." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>À ne pas faire : inclure différents niveaux de hiérarchie

Votre contenu doit évoluer dans un ordre logique qui aide les utilisateurs à le comprendre. Si vous avez deux onglets qui sont étroitement liés, envisagez de les combiner en un seul onglet.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="L'exemple affiche les meilleures pratiques d'une application personnelle." border="false":::

### <a name="first-run-experience"></a>Première expérience d’utilisation

#### <a name="do-include-a-first-run-experience"></a>À faire : inclure une expérience de première expérience

Il doit y avoir au moins un écran d'accueil la première fois que vous utilisez une application personnelle. Pour les bots, décrivez ce que votre bot peut faire et fournissez des actions rapides, telles qu'un bouton de sign-in.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="Illustration shows a personal app best practice." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Illustration des meilleures pratiques d'une application personnelle." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>À ne pas faire : démarrer avec un écran vide

Les utilisateurs peuvent être confondus si rien ne s'affiche la première fois qu'ils exécutent votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="L'illustration affiche les meilleures pratiques d'une application personnelle." border="false":::

### <a name="personalized-content"></a>Contenu personnalisé

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>À faire : agréger le contenu d'application pertinent pour un utilisateur

Qu'il s'agit d'un onglet personnel ou d'un bot, affichez le contenu lié uniquement à l'activité d'un utilisateur dans votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="Cet exemple fournit une meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="L'exemple illustre les meilleures pratiques d'une application personnelle." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>À ne pas faire : afficher du contenu non lié ou trop large

Dans les contextes personnels, n'affichez pas de contenu pour les équipes dont un utilisateur ne fait pas partie. Le contenu du bot personnel doit se concentrer sur la personne, et non sur un groupe.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="La divulgation est un exemple de meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="L'exemple montre les meilleures pratiques d'une application personnelle." border="false":::

### <a name="complex-app-features"></a>Fonctionnalités d'application complexes

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>À faire : autoriser les utilisateurs à accéder à des fonctionnalités complexes dans un navigateur

Votre application doit se concentrer sur les tâches principales dans Teams, mais vous pouvez toujours afficher l'application autonome complète dans un navigateur.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="L'exemple montre les meilleures pratiques d'application personnelle." border="false":::

#### <a name="dont-include-your-entire-app"></a>À ne pas faire : inclure l'intégralité de votre application

Sauf si vous avez créé votre application spécifiquement pour Teams, vous disposez probablement de fonctionnalités qui n'ont pas de sens dans un outil de collaboration.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="L'illustration fournit les meilleures pratiques d'application personnelles." border="false":::

## <a name="manage-a-personal-tab"></a>Gérer un onglet personnel

Sur le côté gauche de Teams, les utilisateurs peuvent cliquer avec le bouton droit sur l'application personnelle pour épingler, supprimer et configurer d'autres options d'application.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="L'exemple montre les options de gestion d'une application personnelle." border="false":::

## <a name="learn-more"></a>En savoir plus

Ces autres recommandations de conception peuvent vous aider en fonction de l'étendue de votre application personnelle :

* [Conception de votre onglet](../../tabs/design/tabs.md)
* [Conception de votre bot](../../bots/design/bots.md)

## <a name="validate-your-design"></a>Valider votre conception

Si vous envisagez de publier votre application sur AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l'échec des applications lors de l'envoi.

> [!div class="nextstepaction"]
> [Vérifier les instructions de validation de la conception](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
