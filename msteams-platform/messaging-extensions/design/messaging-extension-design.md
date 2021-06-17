---
title: Conception de votre extension de messagerie
description: Découvrez comment concevoir une extension Teams messagerie et obtenir le kit Microsoft Teams’interface utilisateur.
keywords: 'Recommandations en matière de conception d’équipes : conseils sur les extensions de messagerie'
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: fd870d8e10ef74c36f8f6d145d48980f53e9303c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631041"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Conception de votre extension Microsoft Teams messagerie électronique

Les extensions de messagerie sont des raccourcis pour insérer du contenu d’application ou agir sur un message sans sortir de la conversation.
Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des extensions de messagerie dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions complètes sur la conception des extensions de messagerie, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le kit d’interface Microsoft Teams’interface utilisateur.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>Ajouter une extension de messagerie

Vous pouvez ajouter une extension de messagerie dans les contextes Teams suivants :

* À partir du magasin Teams de données.
* Dans un canal, une conversation ou une réunion (avant, pendant et après) près de la zone de composition. Il est intéressant de noter que si vous ajoutez une extension de messagerie à l’un de ces endroits, vous pouvez uniquement l’utiliser dans ce contexte.

L’exemple suivant montre comment ajouter une extension de messagerie dans un canal :

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="L’exemple montre comment ajouter une extension de messagerie près de la zone de composition dans un canal." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="L’exemple montre comment ajouter une extension de messagerie près de la zone de composition dans un canal mobile." border="false":::

---

## <a name="set-up-a-messaging-extension"></a>Configurer une extension de messagerie

L’authentification n’est pas obligatoire, mais si votre application ressemble à un outil de suivi des tickets, vous devrez peut-être que des personnes se connectent pour utiliser l’extension de messagerie.

Par souci de cohérence entre Teams applications, vous ne pouvez pas personnaliser l’écran de la signature. Si vous utilisez l’authentification unique(SSO), les utilisateurs sont automatiquement connectés.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="L’exemple illustre l’écran de configuration de l’extension de messagerie avec un bouton de signature." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="L’exemple illustre l’écran de configuration de l’extension de messagerie avec un bouton de connectez-vous sur mobile." border="false":::

---

## <a name="types-of-messaging-extensions"></a>Types d’extensions de messagerie

Les extensions de messagerie peuvent avoir des commandes de recherche, des commandes d’action ou les deux. Vos commandes dépendent des fonctionnalités de votre application et de la façon dont elles s’intègrent Teams cas d’utilisation.

### <a name="search-commands"></a>Commandes de recherche

Avec les commandes de recherche, les utilisateurs peuvent utiliser votre extension de messagerie pour trouver rapidement du contenu externe et les insérer dans un message. Les commandes de recherche sont généralement disponibles dans la zone de composition. Par exemple, vous pouvez commencer ou ajouter une discussion en partageant un élément de contenu, sans jamais quitter Teams.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="L’exemple montre une extension de messagerie basée sur la recherche lancée à partir de la zone de composition." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="Exemple d’une extension de messagerie basée sur la recherche lancée à partir de la zone de composition sur mobile." border="false":::

---

#### <a name="compose-box-layout-options"></a>Options de disposition de zone de composition

Certaines options s’offrent à vous pour afficher les résultats de recherche d’extension de messagerie, y compris les affichages liste [et grille.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations montrant les options de disposition pour les résultats de recherche d’extension de messagerie." border="false":::

### <a name="action-commands"></a>Commandes d'action

Les commandes d’action permettent aux utilisateurs de déclencher des actions et de traiter des demandes dans des services externes Teams. Par exemple, si votre application suit les commandes, un utilisateur peut créer une commande à l’aide du contenu du message d’un collègue directement dans sa conversation.

Les extensions de messagerie basées sur une action nécessitent fréquemment que les utilisateurs remplissent un formulaire ou tout autre type de configuration dans une configuration modale. Vous pouvez créer ces expériences avec [des modules de tâche.](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="open-a-messaging-extension"></a>Ouvrir une extension de messagerie

La zone de composition et les messages ou publications sont les principaux contextes dans lequel les personnes utilisent les extensions de messagerie.

### <a name="from-the-compose-box"></a>À partir de la zone de composition

Une fois ajouté, les utilisateurs peuvent ouvrir votre extension de messagerie en sélectionnant l’icône de votre application sous la zone de composition. Dans ces exemples, l’extension dispose de commandes de recherche et d’action.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="L’exemple montre comment ouvrir une extension de messagerie à partir de la zone de composition." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="L’exemple montre comment ouvrir une extension de messagerie à partir de la zone de composition sur un appareil mobile." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a>À partir d’un message de conversation ou d’un billet de canal

Une fois ajoutés, les utilisateurs peuvent sélectionner l’icône **Plus** dans le message de conversation ou le billet de canal pour trouver les commandes :::image type="icon" source="../../assets/icons/teams-client-more.png"::: d’action de votre extension. Votre extension peut être répertoriée sous **Plus d’actions** basées sur l’utilisation.

> [!NOTE]
> La prise en charge d’autres actions à partir d’un message de conversation ou d’un billet de canal n’est pas disponible Microsoft Teams plateforme mobile. 

#### <a name="chat-message"></a>Message de conversation

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="L’exemple montre comment ouvrir une extension de messagerie à partir d’un message de conversation." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="L’exemple montre comment ouvrir une extension de messagerie à partir d’un billet de conversation sur mobile." border="false":::

---

#### Channel post

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false":::

---

## <a name="use-a-messaging-extension"></a>Utiliser une extension de messagerie

Les scénarios suivants montrent les principales façons dont les personnes utilisent les extensions de messagerie.

### <a name="insert-content-into-a-message"></a>Insérer du contenu dans un message

**1. Sélectionnez une extension de messagerie.** Les utilisateurs peuvent rechercher le contenu qu’ils souhaitent partager à partir de la zone de composition.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Exemple : un utilisateur recherche le contenu à insérer à partir de la zone de composition." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="Exemple : un utilisateur recherche du contenu à insérer à partir de la zone de composition sur un appareil mobile." border="false":::

---

**2. Insérer du contenu**. Une fois publié, d’autres personnes peuvent répondre ou sélectionner le contenu pour voir plus d’informations dans votre application.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple : un utilisateur publie du contenu dans une conversation de canal." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="Exemple : un utilisateur publie du contenu dans une conversation de canal sur mobile." border="false":::

---

### <a name="take-action-on-a-message"></a>Prendre des mesures sur un message

**1. Sélectionnez une extension de messagerie.** Votre application peut inclure une ou plusieurs commandes d’action.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Exemple : un utilisateur sélectionne une commande d’action d’extension de messagerie." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="Exemple : un utilisateur sélectionne une commande d’action d’extension de messagerie sur un appareil mobile." border="false":::

---

**2. Terminez l’action.** Votre application peut recevoir et traiter tout contenu ou toute donnée envoyé par l’action de message. Cela permet aux utilisateurs de rester dans leur conversation et, dans l’exemple suivant, de ne pas se soucier d’entrer des informations directement dans votre application.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message sur un appareil mobile." border="false":::

---

### <a name="preview-links"></a>Liens d’aperçu

Les extensions de messagerie vous permettent également d’insérer des liens enrichis à partir d’une URL reconnue dans un message (cette fonctionnalité est appelée déploiement de [lien).)](../../messaging-extensions/how-to/link-unfurling.md)

**1. Collez un lien reconnu dans** la zone de composition.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="L’exemple montre un utilisateur qui a passé un lien dans le cadre de l’exemple." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="L’exemple montre un utilisateur qui a passé un lien dans la zone de l’appareil mobile." border="false":::

---

**2. Insérer du contenu**. Si votre application reconnaît l’URL dans la zone de composition, elle affiche le lien sous la mesure d’une carte qui fournit un aperçu enrichi de contenu du contenu web. (Pour plus [d’informations, voir](../../task-modules-and-cards/cards/design-effective-cards.md) les recommandations en matière de conception des cartes adaptatives.)

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="L’exemple montre comment l’URL, car elle est reconnue par votre application, inclut du contenu enrichi dans la zone de composition." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="L’exemple montre comment l’URL, car elle est reconnue par votre application, inclut du contenu enrichi dans la zone de composition sur mobile." border="false":::

---

## <a name="manage-a-messaging-extension"></a>Gérer une extension de messagerie

En cliquant avec le bouton droit sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de messagerie.

## <a name="anatomy"></a>Anatomie

### <a name="messaging-extension-in-the-compose-box"></a>Extension de messagerie dans la zone de composition

L’exemple suivant est une extension de messagerie ouverte à partir de la zone de composition.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’une extension de messagerie dans la zone de composition." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Logo de l’application**: icône couleur du logo de votre application.|
|2|**Nom de l’application**: nom complet de votre application.|
|3|**Icône de menu Commandes d’action (facultatif)**: ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).
|4 |**Zone de recherche**: permet aux utilisateurs de trouver le contenu d’application qu’ils souhaitent insérer.|
|5 |**Menu Onglet (facultatif)**: fournit plusieurs catégories de contenu.|
|6 |**Menu commandes d’action (facultatif)**: affiche la liste des commandes d’action (si vous en spécifiez une).|
|7 |**Contenu de l’application**: principalement pour afficher les résultats de recherche. L’exemple ci-dessous utilise la disposition de liste (la disposition de grille est une autre option).|
|8 |**Logo de l’application**: icône de plan du logo de votre application.|

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’une extension de messagerie dans la zone de composition sur mobile." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’application**: nom complet de votre application.|
|2|**Icône de menu Commandes d’action (facultatif)**: ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).
|3|**Zone de recherche**: permet aux utilisateurs de trouver le contenu d’application qu’ils souhaitent insérer.|
|4 |**Menu Onglet (facultatif)**: fournit plusieurs catégories de contenu.|
|5 |**Menu commandes d’action (facultatif)**: affiche la liste des commandes d’action (si vous en spécifiez une).|
|6 |**Contenu de l’application**: principalement pour afficher les résultats de recherche.|

---

### <a name="messaging-extension-management-menu"></a>Menu gestion des extensions de messagerie

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un menu de gestion des extensions de messagerie." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Unpin**: disponible si l’utilisateur a épinglé votre application.|
|2|**Supprimer**: supprime l’extension de messagerie du canal, de la conversation ou de la réunion.|

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="setup-and-general-usage"></a>Configuration et utilisation générale

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple sur l’installation et l’utilisation générale." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>À faire : intégrer avec l' sign-on unique

SSO facilite, accélère et sécurisation le processus de se connecte. En outre, si un utilisateur s’est déjà inscrit à votre application personnelle, il n’a pas besoin de se connecter à nouveau pour accéder à l’extension de messagerie.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple d’intégration à l' sign-on unique." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>À ne pas faire : éloignez les utilisateurs de la conversation

Les extensions de messagerie sont des raccourcis supposés réduire le changement de contexte. Votre extension ne doit pas, par exemple, diriger les utilisateurs vers une page web en dehors Teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>À faire : mettre en surbrillation votre extension de messagerie

Les extensions de messagerie ne sont pas toujours faciles à trouver. Incluez des captures d’écran de son utilisation dans la page de détails de votre application. Si votre application inclut également un bot, vous pouvez inclure la documentation d’aide sur l’extension de messagerie dans une visite guidée du bot.

### <a name="templating"></a>Templating

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple de modèle." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>À faire : laissez Teams gérer une partie du travail de conception si possible

Si cela est utile pour vos cas d’utilisation, envisagez de créer une extension de messagerie basée sur la recherche. Teams restituer ces types d’extensions avec des modèles intégrés et une accessibilité.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple de gestion du travail de conception." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>À ne pas faire : incorporer l’intégralité de votre application dans un module de tâche

Si votre extension de messagerie nécessite des commandes d’action, maintenez le module de tâche simple et affichez uniquement les composants requis pour effectuer l’action.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple sur les themings." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>À faire : tirer parti des jetons Teams couleur

Chaque Teams thème possède son propre modèle de couleurs. Pour gérer automatiquement les modifications de thème, utilisez des jetons <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">de couleur (interface</a> utilisateur Fluent) dans votre conception.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple sur les jetons de couleur." border="false":::

#### <a name="dont-hard-code-color-values"></a>À ne pas faire : valeurs de couleur de code dur

Si vous n’utilisez pas Teams couleur, vos conceptions seront moins évolutives et prenons plus de temps à gérer.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple sur les actions." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>À faire : inclure des commandes d’action qui ont du sens dans le contexte

Les actions de message doivent être liées à ce qu’un utilisateur regarde. Par exemple, fournissez aux utilisateurs un raccourci pour créer un problème ou un élément de travail à l’aide du texte dans le billet d’une personne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple sur les commandes d’action." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>À ne pas faire : inclure des commandes d’actions qui ne sont pas contextuelles

Une action de message pour **afficher votre tableau de** bord semble probablement déconnectée de la plupart des conversations.

   :::column-end:::
:::row-end:::

### <a name="searches"></a>Recherches

#### <a name="do-show-search-results-while-typing"></a>À faire : afficher les résultats de la recherche lors de la saisie

Fournissez des résultats de recherche suggérés pendant que les utilisateurs tapent. Ils peuvent trouver le contenu dont ils ont besoin plus rapidement avec un nombre minimal de caractères.

#### <a name="dont-require-users-to-submit-a-query"></a>À ne pas faire : exiger que les utilisateurs soumettent une requête

Vous pouvez faire en sorte que les utilisateurs appuient sur une touche ou sélectionnent un bouton pour envoyer des requêtes à votre application. Bien que cela puisse être plus facile sur votre service de services d’application, il se peut que les personnes ne voient pas les résultats de recherche en temps réel lorsqu’elles tapent.

#### <a name="do-consider-zero-term-queries"></a>À faire : envisagez les requêtes à terme zéro

Par exemple, avant qu’un utilisateur n’écrive quoi que ce soit dans la zone de recherche, affichez ce qu’il a affiché pour la dernière fois sur votre application. Il est possible qu’ils souhaitent insérer ce contenu dans leur conversation.
