---
title: Création de modules de tâches
author: heath-hamilton
description: Découvrez comment concevoir des modules de tâches pour les applications teams et obtenir le kit d’interface utilisateur Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 41584ecf58ca7718290e58e5845549e4579dac64
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606198"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Conception de modules de tâches pour votre application Microsoft teams

Vous pouvez créer des expériences de menu contextuel modal dans votre application de teams avec des modules de tâches. Utilisez cette fonctionnalité pour afficher des informations et des médias enrichis ou effectuer une tâche complexe.

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="Exemple de module de tâche." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur Microsoft teams

Vous trouverez des instructions de conception de module de tâches plus complètes, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>Ouvrir un module de tâches

Les modules de tâches peuvent être lancés à partir de quasiment n’importe où dans votre application.

* **Onglet**: un module de tâches peut être lancé à partir de n’importe quel lien dans un onglet ou un IFRAME. À utiliser dans les scénarios dans lesquels vous souhaitez que l’utilisateur se focalise sur une interaction.
* **Bot**: un module de tâche peut être lancé à partir d’un lien à l’intérieur d’un message de robot.
* **Carte adaptative**: un module de tâches peut être lancé à partir d’une carte adaptative (envoyée avec une extension de messagerie ou un bot) lorsqu’un utilisateur sélectionne un bouton.
* **Extension de messagerie (commandes action)**: les extensions de messagerie vous permettent d’effectuer une action particulière sur le contenu des messages. La sélection d’une action ouvre un module de tâches.
* **Extension de messagerie (contexte de la zone de composition)**: dans la zone de composition, vous pouvez concevoir une extension de messagerie pour ouvrir un module de tâches au lieu du menu volant standard. Réservez les modules de tâche pour les interactions complexes, comme la réalisation d’un formulaire.

## <a name="anatomy"></a>Anatomie

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’un module de tâches." border="false":::

Les modules de tâches sont des surfaces très flexibles. Ils peuvent être créés avec des IFRAMES, en extrayant d’autres modèles de l’interface utilisateur, pour héberger des expériences créées par des partenaires. Cette approche est recommandée pour l’expérience la plus soignée.

Elles peuvent également être créées à l’aide de l’infrastructure de [carte adaptative](../../task-modules-and-cards/cards/design-effective-cards.md) , qui peut être plus simple et plus rapide pour exécuter des scénarios courants (tels que des formulaires).

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application**|
|2 |**Nom** de l’application : nom complet de votre application.|
|3 |**En-tête**: rendez les en-têtes claires et concise. Décrivez la tâche que les utilisateurs doivent effectuer.
|4 |**Bouton Fermer**: permet aux utilisateurs de rechercher le contenu d’application qu’ils souhaitent insérer.|
|5 |**IFRAME**: espace réactif qui héberge le contenu de votre application.|
|6 |**Actions (facultatif)**: boutons liés au contenu de votre application.|

## <a name="designing-with-ui-templates"></a>Conception avec des modèles d’interface utilisateur

Envisagez d’utiliser des modèles pour des dispositions courantes à l’intérieur de vos modules de tâches. Chacune d’entre elles est composée de plus petits composants pour créer une conception élégante et réactive pouvant être utilisée ou personnalisée pour votre scénario ou avec l’apparence de votre marque.

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.

## <a name="examples"></a>Exemples

### <a name="list"></a>Répertorier

Les listes fonctionnent parfaitement dans un module de tâches, car elles sont faciles à analyser.

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Exemple de liste dans un module de tâches." border="false":::

### <a name="form"></a>Formulaire

Les modules de tâches constituent un excellent point de vue des formulaires avec des entrées utilisateur et une validation en ligne séquentielles. Vous pouvez utiliser des cartes adaptatives pour incorporer des éléments de formulaire.

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Exemple de formulaire dans un module de tâches." border="false":::

### <a name="sign-in"></a>Se connecter

Créez une connexion ciblée ou un flux d’inscription avec une série de modules de tâches, ce qui permet aux utilisateurs de se déplacer facilement via des étapes séquentielles.

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Exemple d’expérience de connexion dans un module de tâches." border="false":::

### <a name="media"></a>Multimédia

Incorporer du contenu multimédia dans un module de tâches pour une expérience de visualisation ciblée.

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Exemple de contenu multimédia dans un module de tâches." border="false":::

### <a name="empty-state"></a>État vide

À utiliser pour les messages d’accueil, d’erreur et de réussite.

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Exemple d’état vide dans un module de tâches." border="false":::

### <a name="image-gallery"></a>Galerie d’images

Incorporer un carrousel de galerie dans un IFRAME.

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Exemple de Galerie d’images dans un module de tâches." border="false":::

### <a name="poll"></a>Temporisateur

Cet exemple montre les résultats de la requête lancés à partir d’une carte adaptative.

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Exemple d’interrogation dans un module de tâches." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

### <a name="usability"></a>Facilement

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>Do : utiliser un module de tâche à la fois

L’objectif est de concentrer l’utilisateur sur la réalisation d’une tâche après tout !

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>Ne pas : dépiler une boîte de dialogue par-dessus un module de tâches

Cela crée une expérience utilisateur non ciblée et confuse.

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>Réactive

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>Do : Assurez-vous que le contenu est réactif

Alors que les cartes adaptatives hébergées dans un module de tâches s’affichent correctement sur les appareils mobiles, si vous choisissez d’utiliser un IFRAME pour héberger le contenu de l’application, assurez-vous que l’interface utilisateur est réactive et fonctionne bien sur les appareils.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="dont-use-horizontal-scrollbars"></a>Ne pas : utiliser des barres de défilement horizontales

Il est recommandé de conserver le contenu axé sur le contenu et pas trop long. Si un défilement est nécessaire, faites défiler verticalement et pas horizontalement.

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>Simplification

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="do-keep-it-short"></a>Do : conservez-le short

Vous pouvez facilement créer un assistant à plusieurs étapes, mais cela ne signifie pas nécessairement que vous devez le faire ! Un module de tâches à écrans multiples peut être problématique, car les messages entrants sont gênants et les utilisateurs tentant de quitter. Si votre tâche est réellement impliquée, affichez-la sur une page Web complète au lieu d’un module de tâches.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="dont-do-long-interactions"></a>Ne pas : effectuer des interactions longues

Essayez de conserver vos interactions courtes et jusqu’au point.

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>Messages d’erreur

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="do-use-inline-error-messages"></a>Do : utiliser des messages d’erreur incorporés

Consultez le modèle d’interface utilisateur formulaires pour obtenir des instructions sur la gestion des erreurs Inline.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>Ne pas : placer les messages d’erreur dans les boîtes de dialogue

Ne pas afficher un message d’erreur dans une boîte de dialogue en haut d’un module de tâches. Il crée une expérience utilisateur confuse.

   :::column-end:::
:::row-end:::
