---
title: Conception de modules de tâches
author: heath-hamilton
description: Dans ce module, découvrez comment concevoir des modules de tâches pour vos applications Teams et obtenez le Kit d’interface utilisateur Microsoft Teams.
ms.localizationpriority: high
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 07dd0457d49b167226da2fa10e91d87e6f674b6f
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035267"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Conception de modules de tâches pour votre application Microsoft Teams

Vous pouvez créer des expériences contextuelles modales dans votre application Teams avec des modules de tâches. Utilisez cette fonctionnalité pour afficher des informations et des médias enrichis ou effectuer une tâche complexe.

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="L’exemple montre un module de tâches.":::

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions plus détaillées sur la conception de modules de tâches, y compris les éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d’interface utilisateur de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>Ouvrir un module de tâches

Les modules de tâches peuvent être lancés à partir de pratiquement n’importe où dans votre application.

* **Onglet** : un module de tâches peut être lancé à partir de n’importe quel lien d’un onglet. À utiliser dans les scénarios où vous souhaitez que l’utilisateur se concentre sur une interaction.
* **Bot** : un module de tâches peut être lancé à partir d’un lien à l’intérieur d’un message de bot.
* **Carte adaptative** : un module de tâches peut être lancé à partir d’une carte adaptative (envoyée avec une extension de messagerie ou par un bot) lorsqu’un utilisateur sélectionne un bouton.
* **Extension de messagerie (commandes d’action)**  : les extensions de messagerie vous permettent d’agir en particulier sur le contenu des messages. La sélection d’une option ouvre un module de tâches.
* **Extension de messagerie (contexte de la zone de rédaction)**  : dans la zone de rédaction, vous pouvez concevoir une extension de messagerie pour ouvrir un module de tâches au lieu du menu volant classique. Réservez les modules de tâches pour des interactions complexes, telles qu’un formulaire à remplir.

## <a name="anatomy"></a>Anatomie

Les modules de tâches fournissent une surface flexible pour les expériences d’application hébergée. Ils sont créés à l’aide d’un IFrame (bureau) ou d’une vue web (mobile), afin que vous puissiez concevoir des modules de tâches avec nos modèles d’interface utilisateur (recommandés) ou à partir de zéro.

Ils peuvent également être créés avec l’infrastructure de [Cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md), ce qui peut être un moyen plus simple et plus rapide de faciliter des scénarios courants (tels que les formulaires).

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/task-module/mobile-task-module-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un module de tâches sur mobile.":::

|Compteur|Description|
|----------|-----------|
|1|**En-tête** : rendre les en-têtes clairs et concis. Décrivez la tâche que vous souhaitez que les utilisateurs effectuent.
|2|**Nom de l’application** : nom complet de votre application.|
|3|**Bouton Fermer** : ferme le module de tâches. Ne pas appliquer de modifications non enregistrées dans le contenu de l’application.|
|4|**affichage web** : espace réactif qui héberge le contenu de votre application.|
|5|**Actions (facultatives)**  : boutons liés au contenu de votre application.|

### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un module de tâches.":::

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application**|
|2|**Nom de l’application** : nom complet de votre application.|
|3|**En-tête** : rendre les en-têtes clairs et concis. Décrivez la tâche que vous souhaitez que les utilisateurs effectuent.
|4|**Bouton Fermer** : ferme le module de tâches. Ne pas appliquer de modifications non enregistrées dans le contenu de l’application.|
|5|**IFrame** : espace réactif qui héberge le contenu de votre application.|
|6|**Actions (facultatives)**  : boutons liés au contenu de votre application.|

## <a name="designing-with-ui-templates"></a>Conception avec des modèles d’interface utilisateur

Envisagez l’utilisation de modèles pour des dispositions courantes dans vos modules de tâches. Chacun d’eux est constitué de composants plus petits pour créer une conception réactive et élégante qui peut être utilisée de manière prête à l’emploi ou personnalisée à votre scénario ou à l’apparence de votre marque.

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list) : les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form) : les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state) : le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la connexion, les expériences de première exécution, les messages d’erreur et bien plus encore.

## <a name="examples"></a>Exemples

### <a name="list"></a>Liste

Les listes fonctionnent parfaitement dans un module de tâches, car elles sont faciles à analyser.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/task-module/mobile-list.png" alt-text="Exemple de liste dans un module de tâches sur un mobile.":::

#### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Exemple de liste dans un module de tâches.":::

### <a name="form"></a>Formulaire

Les modules de tâches sont un excellent emplacement pour afficher des formulaires avec des entrées utilisateur séquentielles et une validation en ligne. Vous pouvez utiliser des cartes adaptatives pour incorporer des éléments de formulaire.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/task-module/mobile-form.png" alt-text="Exemple de formulaire dans un module de tâches sur un mobile.":::

#### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/form.png" alt-text="Exemple de formulaire dans un module de tâches.":::

### <a name="sign-in"></a>Connexion

Créez une ouverture de session prioritaire ou un flux de connexion avec une série de modules de tâches, ce qui permet aux utilisateurs de se déplacer facilement dans les étapes séquentielles.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/task-module/mobile-sign-in.png" alt-text="Exemple d’expérience d’ouverture de session dans un module de tâches sur mobile.":::

#### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Exemple d’expérience de signature dans un module de tâches.":::

### <a name="media"></a>Élément multimédias

Incorporez du contenu multimédia dans un module de tâches pour une expérience d’affichage ciblée.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/task-module/mobile-media.png" alt-text="Exemple de contenu multimédia dans un module de tâches sur un mobile.":::

#### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Exemple de contenu multimédia dans un module de tâches.":::

### <a name="empty-state"></a>État vide

À utiliser pour les messages d’accueil, d’erreur et de réussite.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/task-module/mobile-empty-state.png" alt-text="Exemple d’état vide dans un module de tâches sur un mobile.":::

#### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Exemple d’état vide dans un module de tâches.":::

### <a name="image-gallery"></a>Bibliothèque d'images

Incorporez un carrousel de bibliothèque dans un IFrame (bureau) ou un affichage web (mobile).

##### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/task-module/mobile-image-gallery.png" alt-text="Exemple de bibliothèque d'images dans un module de tâches sur un mobile.":::

##### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Exemple de bibliothèque d'images dans un module de tâches.":::

### <a name="poll"></a>Sondage

Cet exemple montre les résultats de sondages lancés à partir d’une carte adaptative. Le sondage peut également être placé à l’intérieur d’un module de tâches.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/task-module/mobile-poll.png" alt-text="Exemple de sondage dans un module de tâches sur un mobile.":::

#### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Exemple de sondage dans un module de tâches.":::

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="usability"></a>Facilité d’utilisation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâches (un module de tâches à la fois).":::

#### <a name="do-use-one-task-module-at-a-time"></a>À faire : utiliser un module de tâches à la fois

L’objectif est de concentrer l’utilisateur sur l’exécution d’une tâche après tout !

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâches (afficher une boîte de dialogue au-dessus d’un module de tâches).":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>À ne pas faire : afficher une boîte de dialogue au-dessus d’un module de tâches

Cela crée une expérience utilisateur non ciblée et confuse.

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>Réactif

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Exemple montrant une meilleure pratique de module de tâches (vérifiez que le contenu est réactif).":::

#### <a name="do-make-sure-the-content-is-responsive"></a>À faire : vérifier que le contenu est réactif

Bien que les cartes adaptatives hébergées dans un module de tâches autorisent un bon rendu sur les appareils mobiles, si vous choisissez d’utiliser un IFrame pour héberger du contenu d’application, vérifiez que l’interface utilisateur est réactive et fonctionne bien sur tous les appareils.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâches (n’utilisez pas de barres de défilement horizontales).":::

#### <a name="dont-use-horizontal-scroll-bars"></a>À ne pas faire : utiliser des barres de défilement horizontales

Il est préférable de garder le contenu ciblé et pas trop long. Si un défilement est nécessaire, faites défiler verticalement et non horizontalement.

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>Simplicité

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâches (restez concis).":::

#### <a name="do-keep-it-short"></a>À faire : rester concis

Vous pouvez facilement créer un Assistant en plusieurs étapes, mais cela ne signifie pas nécessairement que vous devez le faire ! Un module de tâches à plusieurs écrans peut être problématique, car les messages entrants sont distrayants et les utilisateurs peuvent être tentés de quitter. Si votre tâche est vraiment compliquée, ouvrez une page web complète au lieu d’un module de tâches.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâches (sans interactions longues).":::

#### <a name="dont-have-long-interactions"></a>À ne pas faire : avoir de longues interactions

Essayez de maintenir vos interactions courtes et directes.

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>Messages d’erreur

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâches (utiliser des messages d’erreur en ligne).":::

#### <a name="do-use-inline-error-messages"></a>À faire : utiliser les messages d’erreur en ligne

Consultez le modèle d’interface utilisateur de formulaires pour obtenir des instructions sur la gestion des erreurs en ligne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâches (placer des messages d’erreur dans des boîtes de dialogue).":::

#### <a name="dont-put-error-messages-in-dialogs"></a>À ne pas faire : placer des messages d’erreur dans des boîtes de dialogue

Ne pas afficher de message d’erreur dans une boîte de dialogue au-dessus d’un module de tâches. Cela crée une expérience déconcertante.

   :::column-end:::
:::row-end:::
