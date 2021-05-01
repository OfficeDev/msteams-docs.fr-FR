---
title: Conception de modules de tâches
author: heath-hamilton
description: Découvrez comment concevoir des modules de tâche pour Teams applications et obtenir Microsoft Teams kit d'interface utilisateur.
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 347ce42c41706f698e2f8897a0518aae0850a275
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101729"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Conception de modules de tâche pour votre application Microsoft Teams web

Vous pouvez créer des expériences popup modales dans votre application Teams avec des modules de tâche. Utilisez cette fonctionnalité pour afficher des informations et des médias enrichis ou effectuer une tâche complexe.

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="L'exemple montre un module de tâche." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception de module de tâche plus complètes, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d'interface Microsoft Teams'interface utilisateur.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>Ouvrir un module de tâche

Les modules de tâche peuvent être lancés à partir de pratiquement n'importe où dans votre application.

* **Onglet**: un module de tâche peut être lancé à partir de n'importe quel lien d'un onglet. À utiliser dans les scénarios où vous souhaitez que l'utilisateur se concentre sur une interaction.
* **Bot**: un module de tâche peut être lancé à partir d'un lien à l'intérieur d'un message de bot.
* **Carte adaptative**: un module de tâche peut être lancé à partir d'une carte adaptative (envoyée avec une extension de messagerie ou par un bot) lorsqu'un utilisateur sélectionne un bouton.
* **Extension de messagerie (commandes d'action)**: les extensions de messagerie vous permettent d'agir en particulier sur le contenu des messages. La sélection d'une action ouvre un module de tâche.
* **Extension de messagerie (contexte de la** zone de composition) : dans la zone de composition, vous pouvez concevoir une extension de messagerie pour ouvrir un module de tâche au lieu du volant classique. Réservez les modules de tâche pour les interactions complexes, telles que la réalisation d'un formulaire.

## <a name="anatomy"></a>Anatomie

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'un module de tâche." border="false":::

Les modules de tâche sont des surfaces très flexibles. Ils peuvent être créés avec des iframes, en tirant dans d'autres modèles d'interface utilisateur, pour héberger des expériences conçues par des partenaires. Il est préférable pour l'expérience la plus agréable.

Ils peuvent également être créés avec l'infrastructure [de](../../task-modules-and-cards/cards/design-effective-cards.md) carte adaptative, qui peut être un moyen plus simple et plus rapide d'exécuter des scénarios courants (tels que des formulaires).

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application**|
|2|**Nom de l'application**: nom complet de votre application.|
|3|**En-tête :** rendre les en-têtes clairs et concis. Décrivez la tâche que vous souhaitez que les utilisateurs terminent.
|4 |**Bouton Fermer :** permet aux utilisateurs de trouver le contenu d'application qu'ils souhaitent insérer.|
|5 |**iframe**: espace réactif qui héberge le contenu de votre application.|
|6 |**Actions (facultatives)**: boutons liés au contenu de votre application.|

## <a name="designing-with-ui-templates"></a>Conception avec des modèles d'interface utilisateur

Envisagez d'utiliser des modèles pour les dispositions courantes à l'intérieur de vos modules de tâche. Chacun d'eux est composé de composants plus petits pour créer une conception réactive et élégante qui peut être utilisée de manière personnalisée ou adaptée à votre scénario ou à votre apparence de marque.

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d'agir sur une liste entière ou sur des éléments individuels.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d'état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d'erreur, etc.

## <a name="examples"></a>Exemples

### <a name="list"></a>Répertorier

Les listes fonctionnent parfaitement dans un module de tâche, car elles sont faciles à analyser.

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Exemple de liste dans un module de tâche." border="false":::

### <a name="form"></a>Formulaire

Les modules de tâche sont un excellent endroit pour faire surface à des formulaires avec des entrées utilisateur séquentielles et une validation en ligne. Vous pouvez utiliser des cartes adaptatives pour incorporer des éléments de formulaire.

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Exemple de formulaire dans un module de tâche." border="false":::

### <a name="sign-in"></a>Se connecter

Créez un flux de signature ou d'inscription centré avec une série de modules de tâche, ce qui permet aux utilisateurs de se déplacer facilement à travers les étapes séquentielles.

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Exemple d'expérience de signature dans un module de tâche." border="false":::

### <a name="media"></a>Support

Incorporer du contenu multimédia dans un module de tâche pour une expérience d'affichage axée sur l'affichage.

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Exemple de contenu multimédia dans un module de tâche." border="false":::

### <a name="empty-state"></a>État vide

À utiliser pour les messages d'accueil, d'erreur et de réussite.

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Exemple d'état vide dans un module de tâche." border="false":::

### <a name="image-gallery"></a>Galerie d’images

Incorporer un carrousel de galerie dans un iFrame.

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Exemple de galerie d'images dans un module de tâche." border="false":::

### <a name="poll"></a>Sondage

Cet exemple montre les résultats des sondages lancés à partir d'une carte adaptative. Le sondage peut également être placé à l'intérieur d'un module de tâche.

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Exemple d'enquête dans un module de tâche." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d'application de qualité.

### <a name="usability"></a>Convivialité

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (un module de tâche à la fois)." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>À faire : utiliser un module de tâche à la fois

L'objectif est de concentrer l'utilisateur sur l'exécution d'une tâche après tout !

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (afficher une boîte de dialogue au-dessus d'un module de tâche)." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>À ne pas faire : faire apparaître une boîte de dialogue au-dessus d'un module de tâche

Cela crée une expérience utilisateur non recentrée et confuse.

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>Réactive

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (assurez-vous que le contenu est réactif)." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>À faire : assurez-vous que le contenu est réactif

Bien que les cartes adaptatives hébergées dans un module de tâche s'restituent bien sur les appareils mobiles, si vous choisissez d'utiliser un iframe pour héberger du contenu d'application, assurez-vous que l'interface utilisateur est réactive et fonctionne bien sur tous les appareils.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (n'utilisez pas de barres de défilement horizontales)." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a>À ne pas faire : utiliser des barres de défilement horizontales

Il est préférable de garder le contenu concentré et pas trop long. Si un défilement est nécessaire, faites défiler verticalement et non horizontalement.

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>Simplicité

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (restez bref)." border="false":::

#### <a name="do-keep-it-short"></a>Do: Keep it short

Vous pouvez facilement créer un Assistant en plusieurs étapes, mais cela ne signifie pas nécessairement que vous le devriez ! Un module de tâche multi-écran peut être problématique, car les messages entrants sont distrayants et tentant les utilisateurs de quitter. Si votre tâche est vraiment impliquée, pop out vers une page web complète au lieu d'un module de tâche.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (sans interactions longues)." border="false":::

#### <a name="dont-have-long-interactions"></a>À ne pas faire : avoir de longues interactions

Essayez de maintenir vos interactions courtes et au point.

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>Messages d’erreur

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (utiliser des messages d'erreur inline)." border="false":::

#### <a name="do-use-inline-error-messages"></a>À faire : utiliser les messages d'erreur inline

Consultez le modèle d'interface utilisateur de formulaires pour obtenir des instructions sur la gestion des erreurs en ligne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (placer des messages d'erreur dans des boîtes de dialogue)." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>À ne pas faire : placer des messages d’erreur dans des boîtes de dialogue

Ne pas faire apparaître de message d’erreur dans une boîte de dialogue au-dessus d’un module de tâche. Cela crée une expérience utilisateur confuse.

   :::column-end:::
:::row-end:::
