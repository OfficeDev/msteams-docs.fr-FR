---
title: Conception de votre application personnelle
description: Découvrez comment concevoir une application personnelle Teams et obtenir le Kit d’interface utilisateur Microsoft Teams, créer des composants, tels que le tableau de bord, le formulaire, le tableau de tâches pour l’expérience Mobile et Bureau. Découvrez les meilleures pratiques pour le développement d’applications personnelles.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
keywords: Modèle de formulaire de tableau de bord iframe de l’onglet du bot de navigation web de l’application personnelle du kit d’interface utilisateur
ms.openlocfilehash: 51087d0f055130e822d837d9e78eda5b1b28966a
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111814"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Concevoir votre application personnelle pour Microsoft Teams

Une application personnelle peut être un bot, un espace de travail privé ou les deux. Parfois, il fonctionne comme un emplacement pour créer ou afficher du contenu, d’autres fois il offre à l’utilisateur une vue d’ensemble de tout ce qui lui appartient lorsque l’application a été configurée sous forme d’onglet dans plusieurs canaux.

Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer des applications personnelles dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception d’applications personnelles complètes, notamment des éléments que vous pouvez récupérer et modifier si nécessaire, dans le Kit d’interface utilisateur Microsoft Teams. Le kit d’interface utilisateur contient également des rubriques essentielles telles que l’accessibilité et le dimensionnement réactif qui ne sont pas abordés ici.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Ajouter une application personnelle

Les utilisateurs peuvent ajouter une application personnelle à partir du menu volant du magasin ou de l’application Teams en sélectionnant l’icône **Plus** sur le côté gauche de Teams (illustré dans l’exemple suivant).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="Exemple montre comment ajouter une application personnelle à partir du menu volant de l’application." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Utiliser une application personnelle (espace de travail privé)

Avec un espace de travail privé, les utilisateurs peuvent afficher le contenu de l’application qui leur est significatif dans un emplacement central sans quitter Teams.

(Remarque d’implémentation : l’espace de travail privé est basé sur [*l’onglet personnel*](../../build-your-first-app/build-personal-tab.md) fonctionnalité.)

### <a name="anatomy-personal-app-private-workspace"></a>Anatomie : application personnelle (espace de travail privé)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="Exemple montre l’anatomie des composants de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Attribution d’application** : nom de votre application.|
|B|**onglets**: fournit la navigation pour votre application personnelle.|
|C|**Plus de menu**: inclut des options et des informations supplémentaires sur l’application.|
|D|**Navigation principale**: fournit la navigation à votre application à d’autres fonctionnalités principales de Teams.|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="Exemple montre l’anatomie structurelle de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**onglets**: fournit la navigation pour votre application personnelle.|
|1|**affichage web** : affiche le contenu de votre application.|

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="Cet exemple montre l’anatomie des composants de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Attribution d’application** : logo et nom de votre application.|
|B|**onglets**: fournit la navigation pour votre application personnelle.|
|C|**Affichage contextuel** : fait passer le contenu de votre application d'une fenêtre parent à une fenêtre enfant autonome.|
|D|**Plus de menu**: inclut des options et des informations supplémentaires sur l’application. (Vous pouvez également créer **Paramètres** un onglet.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="Cet exemple montre l’anatomie structurelle de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**onglets**: fournit la navigation pour votre application personnelle.|
|1|**IFrame** : affiche le contenu de votre application.|

### <a name="design-with-ui-templates-and-advanced-components"></a>Concevoir avec des modèles d’interface utilisateur et des composants avancés

Utilisez l’un des modèles et composants Teams suivants pour vous aider à concevoir votre onglet personnel :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list) : les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.
* [Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board) : un tableau des tâches, parfois appelé « tableau kanban » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau de bord](../../concepts/design/design-teams-app-ui-templates.md#dashboard) : un tableau de bord est un espace contenant plusieurs cartes qui fournissent une vue d’ensemble de données ou de contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form) : les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state) : le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la connexion, les expériences de première exécution, les messages d’erreur et bien plus encore.
* [Navigation de gauche](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav) : Le composant navigation de gauche peut être utile si votre application personnelle nécessite une certaine navigation. En général, vous devez conserver la navigation au minimum.

## <a name="use-a-personal-app-bot"></a>Utiliser une application personnelle (bot)

Les applications personnelles peuvent inclure un bot pour les conversations individuelles et les notifications privées (par exemple, lorsqu’un collègue publie un commentaire sur la planche graphique). Les utilisateurs interagissent avec le bot dans un onglet que vous spécifiez.

### <a name="anatomy-personal-app-bot"></a>Anatomie : application personnelle (bot)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="Exemple montre l’anatomie du composant de bot personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**point d’entrée du bot**: point d’entrée permettant aux utilisateurs d’accéder à la fonctionnalité de bot dans votre application personnelle.|
|B|**bouton Précédent**: renvoie les utilisateurs à l’espace de travail privé.|
|C|**message bot**: les bots envoient souvent des messages et des notifications sous la forme d’une carte (par exemple, une carte adaptative).|
|D|**zone Compose**: champ d’entrée pour l’envoi de messages au bot.|

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="Exemple montre l’anatomie du composant de bot personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Onglet Bot** : par exemple, incluez un onglet **Chat** pour accéder aux conversations et aux notifications des robots.|
|B|**message bot**: les bots envoient souvent des messages et des notifications sous la forme d’une carte (par exemple, une carte adaptative).|
|C|**zone Compose**: champ d’entrée pour l’envoi de messages au bot.|

## <a name="manage-a-personal-tab"></a>Gérer un onglet personnel

Sur le côté gauche de Teams, les utilisateurs peuvent cliquer avec le bouton droit sur l’application personnelle pour épingler, supprimer et configurer d’autres options d’application.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="Exemple montre les options de gestion d’une application personnelle." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="tab-priority"></a>Priorité de tabulation

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>À faire : afficher le contenu le plus pertinent dans le premier onglet

Avec un dimensionnement réactif, les onglets à droite peuvent être tronqués ou hors vue.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="Exemple montre une application personnelle affichant le contenu le plus pertinent dans le premier onglet." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Ne pas : diriger avec du contenu ou des métadonnées secondaires

À l’instar d’une application web standard, la navigation par tabulation doit progresser dans un ordre qui vous aide à comprendre les principales fonctionnalités de votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Exemple montre une application personnelle avec un contenu ou des métadonnées secondaires." border="false":::

### <a name="tab-hierarchy"></a>Hiérarchie de tabulation

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>À faire : les onglets doivent être de hiérarchie égale et représenter des pages d’application clés

Vos onglets doivent catégoriser les principales fonctionnalités et le contenu de votre application. Avec un dimensionnement réactif, le contenu à droite peut être tronqué ou hors vue.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="Exemple montre une application personnelle avec des onglets de hiérarchie égale." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>Ne pas : inclure différents niveaux de hiérarchie

Votre contenu doit progresser dans un ordre logique qui aide les utilisateurs à le comprendre. Si vous avez deux onglets étroitement liés, envisagez de les combiner en un seul onglet.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="Exemple montre une application personnelle avec différents niveaux de hiérarchie." border="false":::

### <a name="first-run-experience"></a>Première expérience d’utilisation

#### <a name="do-include-a-first-run-experience"></a>À faire : inclure une expérience de première exécution

Il doit y avoir au moins un écran d’accueil la première fois que vous utilisez une application personnelle. Pour les bots, décrivez ce que votre bot peut faire et fournissez des actions rapides, telles qu’un bouton de connexion.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="exemple montre ce qu’il faut faire lors de la première exécution d’une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Un autre exemple montre ce qu’il faut faire lors de la première exécution d’une application personnelle." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>Ne pas : commencer avec un écran vide

Les utilisateurs peuvent être confondus si rien ne s’affiche la première fois qu’ils exécutent votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="exemple montre ce qu’il ne faut pas faire lors de la première exécution d’une application personnelle." border="false":::

### <a name="personalized-content"></a>Contenu personnalisé

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>À faire : agréger le contenu d’application pertinent pour un utilisateur

Qu’il s’agisse d’un onglet personnel ou d’un bot, affichez du contenu lié uniquement à l’activité d’un utilisateur dans votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="Exemple montre ce qu’il faut faire avec une application personnelle et du contenu personnalisé." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Un autre exemple montre ce qu’il faut faire avec une application personnelle et du contenu personnalisé." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>Ne pas : afficher du contenu non lié ou trop large

Dans les contextes personnels, n’affichez pas de contenu pour les équipes dont un utilisateur ne fait pas partie. Le contenu du bot personnel doit se concentrer sur l’individu et non sur un groupe.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="Exemple montre ce qu’il ne faut pas faire avec une application personnelle et du contenu personnalisé." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Un autre exemple montre ce qu’il ne faut pas faire avec une application personnelle et du contenu personnalisé." border="false":::

### <a name="complex-app-features"></a>Fonctionnalités d’application complexes

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>À faire : autoriser les utilisateurs à accéder à des fonctionnalités complexes dans un navigateur

Votre application doit se concentrer sur les tâches principales dans Teams, mais vous pouvez toujours afficher l’application autonome complète dans un navigateur.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="Exemple montre comment gérer des fonctionnalités d’application complexes avec une application personnelle." border="false":::

#### <a name="dont-include-your-entire-app"></a>Ne pas : inclure l’intégralité de votre application

Sauf si vous avez créé votre application spécifiquement pour Teams, vous disposez probablement de fonctionnalités qui n’ont pas de sens dans un outil de collaboration.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="Exemple montre comment ne pas gérer les fonctionnalités d’application complexes avec une application personnelle." border="false":::

## <a name="see-also"></a>Voir aussi

Ces autres instructions de conception peuvent vous aider en fonction de l’étendue de votre application personnelle :

* [Conception de votre onglet](../../tabs/design/tabs.md)
* [la conception de votre bot](../../bots/design/bots.md)
