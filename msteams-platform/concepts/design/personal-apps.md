---
title: Conception de votre application personnelle
description: Découvrez comment implémenter les instructions de conception, notamment les éléments d’interface utilisateur pour concevoir une application personnelle à l’aide du kit d’interface utilisateur Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 4646d47c5aa325291f060ea192dcc1705b414ac7
ms.sourcegitcommit: bd96080c78f25eb0a67ce176df5e255be348f7b1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/14/2022
ms.locfileid: "68575787"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Concevoir votre application personnelle pour Microsoft Teams

Une application personnelle peut être un bot, un espace de travail privé ou les deux. Parfois, il fonctionne comme un endroit pour créer ou afficher du contenu. Dans d’autres cas, il offre à l’utilisateur une vue d’ensemble de tout ce qui lui revenait lorsque l’application a été configurée en tant qu’onglet dans plusieurs canaux.

Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer des applications personnelles dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception d’applications personnelles complètes, notamment des éléments que vous pouvez récupérer et modifier si nécessaire, dans le Kit d’interface utilisateur Microsoft Teams. Le kit d’interface utilisateur contient également des rubriques essentielles telles que l’accessibilité et le dimensionnement réactif qui ne sont pas abordés ici.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Ajouter une application personnelle

Les utilisateurs peuvent ajouter une application personnelle à partir du menu volant du magasin ou de l’application Teams en sélectionnant l’icône **Plus** sur le côté gauche de Teams (illustré dans l’exemple suivant).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="Exemple montre comment ajouter une application personnelle à partir du menu volant de l’application.":::

## <a name="use-a-personal-app-private-workspace"></a>Utiliser une application personnelle (espace de travail privé)

Avec un espace de travail privé, les utilisateurs peuvent afficher le contenu de l’application qui leur est significatif dans un emplacement central sans quitter Teams.

(Remarque d’implémentation : l’espace de travail privé est basé sur [*l’onglet personnel*](../../tabs/how-to/create-personal-tab.md) fonctionnalité.)

### <a name="anatomy-personal-app-private-workspace"></a>Anatomie : application personnelle (espace de travail privé)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="Exemple montre l’anatomie des composants de l’onglet personnel.":::

|Compteur|Description|
|----------|-----------|
|A|**Attribution d’application** : nom de votre application.|
|B|**onglets**: fournit la navigation pour votre application personnelle.|
|C|**Menu Plus** : Inclut d’autres options et informations d’application.|
|D|**Navigation principale**: fournit la navigation à votre application à d’autres fonctionnalités principales de Teams.|

#### <a name="configure-and-add-multiple-actions-in-navbar"></a>**Configurer et ajouter plusieurs actions dans NavBar**

Vous pouvez ajouter plusieurs actions à la barre de navigation supérieure droite et créer un menu de dépassement pour les actions supplémentaires dans une application.

>[!NOTE]
> Un maximum de cinq actions peut être ajouté dans la barre de navigation, y compris le menu de dépassement de capacité.

:::image type="content" source="../../assets/images/overflow-menu-and-multiple-actionsoptions.png" alt-text="La capture d’écran est un exemple qui décrit le menu NavBar et Overflow.":::

Pour **configurer et ajouter plusieurs actions dans NavBar**, appelez [l’API setNavBarMenu](/javascript/api/@microsoft/teams-js/microsoftteams.menus?view=msteams-client-js-1.12.1&preserve-view=true) . et ajoutez la `displayMode enum` propriété à `MenuItem`. Définit `displayMode enum` l’affichage d’un menu dans la barre de navigation. La valeur par défaut est `displayMode enum` définie sur `ifRoom`.

En fonction des exigences et de l’espace disponibles dans navBar, définissez `displayMode enum` l’une des options suivantes.

* S’il y a de la place, définissez-le `ifRoom = 0` pour placer un élément dans la barre de navigation.
* S’il n’y a pas de place, définissez `overflowOnly = 1`, afin que cet élément soit toujours placé dans le menu de dépassement de capacité du NavBar, mais pas dans la barre de navigation.

Voici un exemple de configuration de NavBar avec un menu de dépassement de capacité pour plusieurs actions :

```typescript
const menuItems = [item1, item2, item3, item4, item5]
microsoftTeams.menus.setNavBarMenu(menuItems, (id: string) => {
  output(`Clicked ${id}`)
  return true;
})
```

> [!NOTE]
> L’API `setNavBarMenu` ne contrôle pas le bouton **Actualiser** . Il s’affiche par défaut.

:::image type="content" source="../../assets/images/overflow-menu-and-multple-actions.png" alt-text="La capture d’écran est un exemple montrant la barre de navigation et plusieurs actions dans un menu de dépassement de capacité.":::

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="Exemple montre l’anatomie structurelle de l’onglet personnel.":::

|Compteur|Description|
|----------|-----------|
|A|**onglets**: fournit la navigation pour votre application personnelle.|
|1|**affichage web** : affiche le contenu de votre application.|

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="Cet exemple montre l’anatomie des composants de l’onglet personnel.":::

|Compteur|Description|
|----------|-----------|
|A|**Attribution d’application** : logo et nom de votre application.|
|B|**onglets**: fournit la navigation pour votre application personnelle.|
|C|**Affichage contextuel** : fait passer le contenu de votre application d'une fenêtre parent à une fenêtre enfant autonome.|
|D|**Menu Plus** : Inclut d’autres options et informations d’application. (Vous pouvez également créer **Paramètres** un onglet.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="Cet exemple montre l’anatomie structurelle de l’onglet personnel.":::

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

Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on artboard). Users interact with the bot in a tab you specify.

### <a name="anatomy-personal-app-bot"></a>Anatomie : application personnelle (bot)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="Exemple montre l’anatomie du composant de bot personnel.":::

|Compteur|Description|
|----------|-----------|
|A|**point d’entrée du bot**: point d’entrée permettant aux utilisateurs d’accéder à la fonctionnalité de bot dans votre application personnelle.|
|B|**bouton Précédent**: renvoie les utilisateurs à l’espace de travail privé.|
|C|**message bot**: les bots envoient souvent des messages et des notifications sous la forme d’une carte (par exemple, une carte adaptative).|
|D|**zone Compose**: champ d’entrée pour l’envoi de messages au bot.|

#### <a name="configure-back-button"></a>Bouton Configurer l’arrière

Lorsque vous sélectionnez le bouton Précédent dans une application Teams, vous revenez à la plateforme Teams sans naviguer à l’intérieur de l’application.

Pour naviguer dans l’application, configurez le bouton Précédent afin que lorsque vous sélectionnez le bouton Précédent, vous puissiez revenir aux étapes précédentes et naviguer dans l’application.

Pour **configurer le bouton Précédent**, appelez l’API [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true) , qui gère les fonctionnalités du bouton Précédent en fonction de l’une des conditions suivantes :

* Lorsque `registerBackButtonHandler` la valeur est définie `false`sur , le Kit de développement logiciel (SDK) JavaScript appelle l’API `navigateBack` et la plateforme Teams gère le bouton Précédent.
* Lorsque `registerBackButtonHandler` la valeur est définie `true`sur , l’application gère les fonctionnalités du bouton Précédent (vous pouvez revenir aux étapes précédentes et naviguer dans l’application), et la plateforme Teams n’effectue aucune autre action.

Voici un exemple de configuration du bouton Précédent :

```typescript
microsoftTeams.registerBackButtonHandler(() => {
  const selectOption = registerBackReturn.options[registerBackReturn.selectedIndex].value
  var isHandled = false
  if (selectOption == 'true') 
    isHandled = true;
  output(`onBack isHandled ${isHandled}`)
  return isHandled;
})
```

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="Exemple montre l’anatomie du composant de bot personnel.":::

|Compteur|Description|
|----------|-----------|
|A|**Onglet Bot** : par exemple, incluez un onglet **Chat** pour accéder aux conversations et aux notifications des robots.|
|B|**message bot**: les bots envoient souvent des messages et des notifications sous la forme d’une carte (par exemple, une carte adaptative).|
|C|**zone Compose**: champ d’entrée pour l’envoi de messages au bot.|

## <a name="manage-a-personal-tab"></a>Gérer un onglet personnel

Sur le côté gauche de Teams, les utilisateurs peuvent cliquer avec le bouton droit sur l’application personnelle pour épingler, supprimer et configurer d’autres options d’application.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="Exemple montre les options de gestion d’une application personnelle.":::

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="tab-priority"></a>Priorité de tabulation

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>À faire : afficher le contenu le plus pertinent dans le premier onglet

Avec un dimensionnement réactif, les onglets à droite peuvent être tronqués ou hors vue.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="Exemple montre une application personnelle affichant le contenu le plus pertinent dans le premier onglet.":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Ne pas : diriger avec du contenu ou des métadonnées secondaires

À l’instar d’une application web standard, la navigation par tabulation doit progresser dans un ordre qui vous aide à comprendre les principales fonctionnalités de votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Exemple montre une application personnelle avec un contenu ou des métadonnées secondaires.":::

### <a name="tab-hierarchy"></a>Hiérarchie de tabulation

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>À faire : les onglets doivent être de hiérarchie égale et représenter des pages d’application clés

Vos onglets doivent catégoriser les principales fonctionnalités et le contenu de votre application. Avec un dimensionnement réactif, le contenu à droite peut être tronqué ou hors vue.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="Exemple montre une application personnelle avec des onglets de hiérarchie égale.":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>Ne pas : inclure différents niveaux de hiérarchie

Votre contenu doit progresser dans un ordre logique qui aide les utilisateurs à le comprendre. Si vous avez deux onglets étroitement liés, envisagez de les combiner en un seul onglet.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="Exemple montre une application personnelle avec différents niveaux de hiérarchie.":::

### <a name="first-run-experience"></a>Première expérience d’utilisation

#### <a name="do-include-a-first-run-experience"></a>À faire : inclure une expérience de première exécution

Il doit y avoir au moins un écran d’accueil la première fois que vous utilisez une application personnelle. Pour les bots, décrivez ce que votre bot peut faire et fournissez des actions rapides, telles qu’un bouton de connexion.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="exemple montre ce qu’il faut faire lors de la première exécution d’une application personnelle.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Un autre exemple montre ce qu’il faut faire lors de la première exécution d’une application personnelle.":::

#### <a name="dont-start-with-a-blank-screen"></a>Ne pas : commencer avec un écran vide

Les utilisateurs peuvent être confondus si rien ne s’affiche la première fois qu’ils exécutent votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="exemple montre ce qu’il ne faut pas faire lors de la première exécution d’une application personnelle.":::

### <a name="personalized-content"></a>Contenu personnalisé

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>À faire : agréger le contenu d’application pertinent pour un utilisateur

Qu’il s’agisse d’un onglet personnel ou d’un bot, affichez du contenu lié uniquement à l’activité d’un utilisateur dans votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="Exemple montre ce qu’il faut faire avec une application personnelle et du contenu personnalisé.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Un autre exemple montre ce qu’il faut faire avec une application personnelle et du contenu personnalisé.":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>Ne pas : afficher du contenu non lié ou trop large

Dans les contextes personnels, n’affichez pas de contenu pour les équipes dont un utilisateur ne fait pas partie. Le contenu du bot personnel doit se concentrer sur l’individu et non sur un groupe.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="Exemple montre ce qu’il ne faut pas faire avec une application personnelle et du contenu personnalisé.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Un autre exemple montre ce qu’il ne faut pas faire avec une application personnelle et du contenu personnalisé.":::

### <a name="complex-app-features"></a>Fonctionnalités d’application complexes

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>À faire : autoriser les utilisateurs à accéder à des fonctionnalités complexes dans un navigateur

Votre application doit se concentrer sur les tâches principales dans Teams, mais vous pouvez toujours afficher l’application autonome complète dans un navigateur.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="Exemple montre comment gérer des fonctionnalités d’application complexes avec une application personnelle.":::

#### <a name="dont-include-your-entire-app"></a>Ne pas : inclure l’intégralité de votre application

Sauf si vous avez créé votre application spécifiquement pour Teams, vous disposez probablement de fonctionnalités qui n’ont pas de sens dans un outil de collaboration.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="Exemple montre comment ne pas gérer les fonctionnalités d’application complexes avec une application personnelle.":::

## <a name="see-also"></a>Voir aussi

Ces autres instructions de conception peuvent vous aider en fonction de l’étendue de votre application personnelle :

* [Conception de votre onglet](../../tabs/design/tabs.md)
* [Conception de votre bot](../../bots/design/bots.md)
* [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true)
* [DisplayMode, énumération](/javascript/api/@microsoft/teams-js/menus.displaymode?view=msteams-client-js-latest&preserve-view=true)
