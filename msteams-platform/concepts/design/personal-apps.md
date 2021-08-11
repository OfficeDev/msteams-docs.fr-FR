---
title: Conception de votre application personnelle
description: Découvrez comment concevoir une application Teams et obtenir le kit Microsoft Teams’interface utilisateur.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 4a176f5c2b35ef21567d7d4096183f4ac503d98ad4adb905245a6dee570f5f99
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705748"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Conception de votre application personnelle pour Microsoft Teams

Une application personnelle peut être un bot, un espace de travail privé ou les deux. Parfois, il fonctionne comme un endroit pour créer ou afficher du contenu, d’autres fois il offre à l’utilisateur une vue d’ensemble de tout ce qui lui est propre lorsque l’application a été configurée sous la forme d’un onglet dans plusieurs canaux.

Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des applications personnelles dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions complètes sur la conception d’applications personnelles, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le kit Microsoft Teams’interface utilisateur. Le kit d’interface utilisateur contient également des rubriques essentielles telles que l’accessibilité et le resserrement réactif qui ne sont pas abordés ici.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Ajouter une application personnelle

Vous pouvez ajouter une application personnelle à partir du Teams store (AppSource)  ou du flyout de l’application en sélectionnant l’icône Plus sur le côté gauche de Teams (illustré dans l’exemple suivant).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="L’exemple montre comment ajouter une application personnelle à partir du volant de l’application." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Utiliser une application personnelle (espace de travail privé)

Avec un espace de travail privé, vous pouvez afficher le contenu de l’application qui vous semble significatif dans un emplacement central sans quitter Teams.

(Remarque d’implémentation : l’espace de travail privé est basé sur la [*fonctionnalité d’onglet*](../../build-your-first-app/build-personal-tab.md) personnel.)

### <a name="anatomy-personal-app-private-workspace"></a>Anatomie : application personnelle (espace de travail privé)

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="L’exemple montre l’anatomie des composants de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Attribution de l’application**: nom et logo de votre application.|
|B|**Onglets :** fournit la navigation pour votre application personnelle.|
|C|**Affichage popout :** pousse le contenu de votre application d’une fenêtre parent vers une fenêtre enfant autonome.|
|D|**Menu supplémentaire**: inclut des informations et options d’application supplémentaires. (Vous pouvez également Paramètres **un** onglet.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Onglets :** fournit la navigation pour votre application personnelle.|
|1|**iframe**: affiche le contenu de votre application.|

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="L’exemple montre l’anatomie des composants de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Attribution de l’application**: nom de votre application.|
|B|**Onglets :** fournit la navigation pour votre application personnelle.|
|C|**Menu supplémentaire**: inclut des informations et options d’application supplémentaires.|
|D|**Navigation principale**: fournit la navigation vers les autres fonctionnalités principales Teams votre application.|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle de l’onglet personnel." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Onglets :** fournit la navigation pour votre application personnelle.|
|1|**webview**: affiche le contenu de votre application.|

---

### <a name="designing-with-ui-templates-and-advanced-components"></a>Conception avec des modèles d’interface utilisateur et des composants avancés

Utilisez l’un des Teams et composants suivants pour vous aider à concevoir votre onglet personnel :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.
* [Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.
* [Navigation gauche](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): le composant de navigation gauche peut vous aider si votre application personnelle nécessite une navigation. En règle générale, vous devez conserver la navigation au minimum.

## <a name="use-a-personal-app-bot"></a>Utiliser une application personnelle (bot)

Les applications personnelles peuvent inclure un bot pour les conversations un-à-un et des notifications privées (par exemple, lorsqu’un collègue publie un commentaire sur votre tableau de bord). Le bot est disponible dans un onglet que vous spécifiez.

### <a name="anatomy-personal-app-bot"></a>Anatomie : application personnelle (bot)

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="L’exemple montre l’anatomie des composants personnels du bot." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Onglet Bot**: par exemple, incluez un onglet **Conversation** pour accéder aux conversations et notifications des bots.|
|B|**Message du bot**: les bots envoient souvent des messages et des notifications sous la forme d’une carte (par exemple, une carte adaptative).|
|C|**Zone de composition**: champ d’entrée pour l’envoi de messages au bot.|

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="L’exemple montre l’anatomie des composants personnels du bot." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**Point d’entrée du bot**: point d’entrée pour que les utilisateurs accèdent à la fonctionnalité bot dans votre application personnelle.|
|B|**Bouton Retour :** permet aux utilisateurs de revenir à l’espace de travail privé.|
|C|**Message du bot**: les bots envoient souvent des messages et des notifications sous la forme d’une carte (par exemple, une carte adaptative).|
|D|**Zone de composition**: champ d’entrée pour l’envoi de messages au bot.|

---

## <a name="manage-a-personal-tab"></a>Gérer un onglet personnel

Sur le côté gauche du Teams, les utilisateurs peuvent cliquer avec le bouton droit sur l’application personnelle pour épingler, supprimer et configurer d’autres options d’application.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="L’exemple montre les options de gestion d’une application personnelle." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="tab-priority"></a>Priorité de l’onglet

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>À faire : afficher le contenu le plus pertinent dans le premier onglet

Avec le resserré réactif, les onglets de droite peuvent être tronqués ou en dehors de la vue.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="L’exemple montre une application personnelle affichant le contenu le plus pertinent dans le premier onglet." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>À ne pas faire : diriger avec du contenu ou des métadonnées secondaires

À l’exemple d’une application web standard, la navigation par onglets doit s’effectuer dans un ordre qui vous aide à prendre en compte les principales fonctionnalités de votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="L’exemple montre une application personnelle en tête avec du contenu ou des métadonnées secondaires." border="false":::

### <a name="tab-hierarchy"></a>Hiérarchie d’onglets

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>À faire : les onglets doivent être de hiérarchie égale et représenter des pages d’application clés

Vos onglets doivent catégoriser les principales fonctionnalités et le contenu de votre application. Avec le resserré réactif, le contenu à droite peut être tronqué ou hors de vue.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="L’exemple montre une application personnelle avec des onglets de hiérarchie égale." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>À ne pas faire : inclure différents niveaux de hiérarchie

Votre contenu doit évoluer dans un ordre logique qui aide les utilisateurs à le comprendre. Si vous avez deux onglets qui sont étroitement liés, envisagez de les combiner en un seul onglet.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="L’exemple montre une application personnelle avec différents niveaux de hiérarchie." border="false":::

### <a name="first-run-experience"></a>Première expérience d’utilisation

#### <a name="do-include-a-first-run-experience"></a>À faire : inclure une expérience de première expérience

Il doit y avoir au moins un écran d’accueil la première fois que vous utilisez une application personnelle. Pour les bots, décrivez ce que votre bot peut faire et fournissez des actions rapides, telles qu’un bouton de sign-in.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="L’exemple montre comment faire lors de la première expérience de première application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Un autre exemple montre comment faire lors de la première expérience de première application personnelle." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>À ne pas faire : démarrer avec un écran vide

Les utilisateurs peuvent être confondus si rien ne s’affiche la première fois qu’ils exécutent votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="L’exemple montre ce qu’il ne faut pas faire lors de la première expérience de première application personnelle." border="false":::

### <a name="personalized-content"></a>Contenu personnalisé

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>À faire : agréger le contenu d’application pertinent pour un utilisateur

Qu’il s’agit d’un onglet personnel ou d’un bot, affichez le contenu lié uniquement à l’activité d’un utilisateur dans votre application.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="L’exemple montre comment faire avec une application personnelle et du contenu personnalisé." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Un autre exemple montre comment faire avec une application personnelle et du contenu personnalisé." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>À ne pas faire : afficher du contenu non lié ou trop large

Dans les contextes personnels, n’affichez pas de contenu pour les équipes dont un utilisateur ne fait pas partie. Le contenu du bot personnel doit se concentrer sur la personne, et non sur un groupe.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="L’exemple montre ce qu’il ne faut pas faire avec une application personnelle et du contenu personnalisé." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Un autre exemple montre ce qu’il ne faut pas faire avec une application personnelle et du contenu personnalisé." border="false":::

### <a name="complex-app-features"></a>Fonctionnalités d’application complexes

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>À faire : autoriser les utilisateurs à accéder à des fonctionnalités complexes dans un navigateur

Votre application doit se concentrer sur les tâches principales dans Teams, mais vous pouvez toujours afficher l’application autonome complète dans un navigateur.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="L’exemple montre comment gérer des fonctionnalités d’application complexes avec une application personnelle." border="false":::

#### <a name="dont-include-your-entire-app"></a>À ne pas faire : inclure l’intégralité de votre application

Sauf si vous avez créé votre application spécifiquement Teams, vous disposez probablement de fonctionnalités qui n’ont pas de sens dans un outil de collaboration.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="L’exemple montre comment ne pas gérer des fonctionnalités d’application complexes avec une application personnelle." border="false":::

## <a name="see-also"></a>Voir aussi

Ces autres recommandations de conception peuvent vous aider en fonction de l’étendue de votre application personnelle :

* [Conception de votre onglet](../../tabs/design/tabs.md)
* [Conception de votre bot](../../bots/design/bots.md)
