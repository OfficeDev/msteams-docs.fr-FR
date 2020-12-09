---
title: Conception de votre application personnelle
description: Découvrez comment concevoir une application personnelle teams et obtenir le kit d’interface utilisateur Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604989"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Conception de votre application personnelle pour Microsoft teams

Une application personnelle peut être un bot, un espace de travail privé ou les deux. Parfois, il fonctionne comme un emplacement de création ou d’affichage de contenu, d’autres fois qu’il offre à l’utilisateur un aperçu de tous ses éléments lorsque l’application a été configurée sous la forme d’un onglet dans plusieurs canaux.

Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer des applications personnelles dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur Microsoft teams

Vous trouverez des instructions de conception d’applications personnelles complètes, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams. Le kit d’interface utilisateur comporte également des rubriques essentielles, telles que l’accessibilité et le dimensionnement réactif, qui ne sont pas abordées ici.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Ajouter une application personnelle

Vous pouvez ajouter une application personnelle à partir du magasin de Teams (AppSource) ou le menu volant d’application en sélectionnant l’icône **plus** sur le côté gauche de Teams (illustré dans l’exemple ci-dessous).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="Exemple montre comment ajouter une application personnelle à partir de la fenêtre mobile d’application." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Utiliser une application personnelle (espace de travail privé)

Avec un espace de travail privé, vous pouvez afficher le contenu de l’application qui est significatif pour vous dans un emplacement central sans quitter Teams.

(Mise en œuvre Remarque : l’espace de travail privé est basé sur les fonctionnalités de l' [*onglet personnel*](../../build-your-first-app/build-personal-tab.md) .)

### <a name="anatomy-personal-app-private-workspace"></a>Anatomie : application personnelle (espace de travail privé)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="Exemple illustre l’anatomie du composant de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Attribution d’application**: logo et nom de votre application.|
|B|**Onglets**: permet de naviguer dans votre application personnelle. Par exemple, inclure un onglet **à propos** de ou **d’aide** .|
|C|**Vue contextuelle**: envoie le contenu de votre application d’une fenêtre parente à une fenêtre enfant autonome.|
|D|**Autres menus**: inclut des informations et des options d’application supplémentaires. (Vous pouvez également définir les **paramètres** d’un onglet.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Onglets**: permet de naviguer dans votre application personnelle.|
|1 |**IFRAME**: affiche le contenu de votre application.|

### <a name="designing-with-ui-templates"></a>Conception avec des modèles d’interface utilisateur

Utilisez l’un des modèles d’interface utilisateur teams suivants pour vous aider à concevoir votre onglet personnel :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.
* [Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board): un tableau des tâches, parfois appelé tableau kanban ou couloirs de natation, est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau](../../concepts/design/design-teams-app-ui-templates.md#dashboard)de bord : un tableau de bord est une zone de dessin contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.
* Navigation de [gauche](../../concepts/design/design-teams-app-ui-templates.md#left-nav): le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation. En règle générale, vous devez conserver la navigation par onglets au minimum.

## <a name="use-a-personal-app-bot"></a>Utiliser une application personnelle (bot)

Les applications personnelles peuvent inclure un bot pour les conversations et les notifications privées en un seul (par exemple, lorsqu’un collègue envoie un commentaire sur votre planche graphique). Le bot est disponible sous un onglet que vous spécifiez.

### <a name="anatomy-personal-app-bot"></a>Anatomie : application personnelle (bot)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="Exemple illustre l’anatomie du composant bot personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Onglet bot**: par exemple, inclure un onglet de **conversation** pour accéder aux conversations et notifications du robot.|
|B|**Message bot**: les robots envoient souvent des messages et des notifications sous la forme d’une carte (telle qu’une carte adaptative).|
|C|**Zone de composition**: champ d’entrée pour l’envoi de messages au bot.|

## <a name="best-practices"></a>Meilleures pratiques

### <a name="tab-priority"></a>Priorité de l’onglet

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Do : afficher le contenu le plus pertinent dans le premier onglet

Avec un dimensionnement réactif, les onglets à droite peuvent être tronqués ou en dehors de l’affichage.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Ne pas : utiliser le contenu secondaire ou les métadonnées

À l’instar d’une application Web standard, la navigation à onglet doit progresser dans un ordre qui permet de mieux appréhender les fonctionnalités principales de votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

### <a name="tab-hierarchy"></a>Hiérarchie d’onglets

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Do : les onglets doivent être de même hiérarchie et représenter les pages d’application clés

Vos onglets doivent catégoriser les principales fonctionnalités et le contenu de votre application. Avec un dimensionnement réactif, le contenu à droite peut être tronqué ou inactif.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>Ne pas inclure différents niveaux de hiérarchie

Votre contenu doit progresser dans un ordre logique qui permet aux utilisateurs de le détecter. Si vous avez deux onglets étroitement liés, envisagez de les combiner en un seul onglet.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

### <a name="first-run-experience"></a>Première expérience d’utilisation

#### <a name="do-include-a-first-run-experience"></a>Do : inclure une expérience de première exécution

Il doit y avoir au moins un écran d’accueil la première fois que vous utilisez une application personnelle. Pour les robots, décrivez ce que votre robot peut faire et fournissez des actions rapides, telles qu’un bouton de connexion.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>Ne pas : Démarrer avec un écran vide

Les utilisateurs peuvent être confondus si rien ne s’affiche la première fois qu’ils exécutent votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

### <a name="personalized-content"></a>Contenu personnalisé

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Do : agréger le contenu d’application pertinent pour un utilisateur

Qu’il s’agisse d’un onglet personnel ou d’un bot, affiche le contenu associé uniquement à l’activité d’un utilisateur dans votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>Ne pas : afficher le contenu non lié ou trop large

Dans les contextes personnels, n’affichez pas de contenu pour les équipes auxquelles l’utilisateur ne fait pas partie. Le contenu de la bot doit se concentrer sur le individu, pas sur un groupe.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

### <a name="complex-app-features"></a>Fonctionnalités d’application complexes

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Do : autoriser les utilisateurs à accéder aux fonctionnalités complexes dans un navigateur

Votre application doit se concentrer sur les tâches principales dans Teams, mais vous pouvez toujours afficher l’application autonome complète dans un navigateur.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-include-your-entire-app"></a>Ne pas inclure votre application entière

Sauf si vous avez créé votre application spécifiquement pour Teams, vous disposez probablement de fonctionnalités qui n’ont pas de sens dans un outil de collaboration.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

## <a name="manage-a-personal-tab"></a>Gérer un onglet personnel

Sur le côté gauche de teams, les utilisateurs peuvent cliquer avec le bouton droit sur l’application personnelle pour épingler, supprimer et configurer d’autres options d’application.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="Exemple affiche des options de gestion d’une application personnelle." border="false":::

## <a name="learn-more"></a>En savoir plus

Ces autres instructions de conception peuvent vous aider en fonction de l’étendue de votre application personnelle :

* [Création de votre onglet](../../tabs/design/tabs.md)
* [Conception de votre robot](../../bots/design/bots.md)

## <a name="validate-your-design"></a>Valider votre conception

Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.

> [!div class="nextstepaction"]
> [Vérifier les instructions de validation de la conception](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
