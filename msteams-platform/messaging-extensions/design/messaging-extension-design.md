---
title: Conception de votre extension de messagerie
description: Découvrez comment concevoir une extension de messagerie Teams et obtenir le Kit d’interface utilisateur de Microsoft Teams.
keywords: équipes conception lignes directrices référence extension de la messagerie conseils meilleure pratique
author: heath-hamilton
localization_priority: Priority
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: 63bdbd0afbf2d0c4a3b7506330fb56e463a10169379c0674dd68496e3cc8de19
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57703310"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Conception de votre extension de messagerie Microsoft Teams

Les extensions de messagerie sont des raccourcis permettant d’insérer du contenu d’application ou agir sur un message sans quitter la conversation.
Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des extensions de messagerie dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions plus détaillées sur la conception de l’extension de messagerie, y compris les éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d’interface utilisateur de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>Ajouter une extension de messagerie

Vous pouvez ajouter une extension de messagerie dans les contextes Teams suivants :

* À partir de Teams Store.
* Dans un canal, une conversation ou une réunion (avant, pendant et après) près de la zone de rédaction. Il est important de noter que si vous ajoutez une extension de messagerie à l’un de ces emplacements, vous seul pouvez l’utiliser dans ce contexte.

L’exemple suivant montre comment ajouter une extension de messagerie dans un canal :

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="Exemple montrant comment ajouter une extension de messagerie près de la zone de rédaction dans un canal." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="Exemple montrant comment ajouter une extension de messagerie près de la zone de rédaction dans un canal sur un appareil mobile." border="false":::

---

## <a name="set-up-a-messaging-extension"></a>Configurer une extension de messagerie

L'authentification n'est pas obligatoire, mais si votre application est une sorte d'outil de suivi des tickets, il se peut que vous ayez besoin que les utilisateurs se connectent pour utiliser l'extension de messagerie.

Pour assurer la cohérence entre les applications Teams, vous ne pouvez pas personnaliser l’écran de connexion. Si vous utilisez l’authentification unique (SSO), les utilisateurs sont connectés automatiquement.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="Exemple présentant l'écran de configuration d'une extension de messagerie avec un bouton de connexion." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="Exemple présentant l'écran de configuration d'une extension de messagerie avec un bouton de connexion sur un appareil mobile." border="false":::

---

## <a name="types-of-messaging-extensions"></a>Types d’extensions de messagerie

Les extensions de messagerie peuvent avoir des commandes de recherche, des commandes d’action ou les deux. Vos commandes dépendent des fonctionnalités de votre application et de la façon dont elles s’intègrent aux cas d'utilisation Teams.

### <a name="search-commands"></a>Commandes de recherche

Avec les commandes de recherche, les utilisateurs peuvent recourir à votre extension de messagerie pour trouver rapidement du contenu externe et les insérer dans un message. Les commandes de recherche sont généralement disponibles dans la zone de rédaction. Par exemple, vous pouvez démarrer ou ajouter à une discussion en partageant un élément de contenu, sans jamais quitter Teams.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Exemple d'une extension de messagerie basée sur la recherche et lancée à partir de la zone de rédaction." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="Exemple d'une extension de messagerie basée sur la recherche et lancée à partir de la zone de rédaction sur un appareil mobile." border="false":::

---

#### <a name="compose-box-layout-options"></a>Options de disposition de la zone de rédaction

Vous disposez de certaines options pour afficher les résultats de recherche de l’extension de messagerie, notamment [liste et les vues de grille](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations montrant les options de disposition pour les résultats de recherche d’extension de messagerie." border="false":::

### <a name="action-commands"></a>Commandes d'action

Les commandes d’action permettent aux utilisateurs de déclencher des actions et de traiter des demandes dans des services externes dans Teams. Par exemple, si votre application assure le suivi des commandes, un utilisateur peut créer une nouvelle commande en utilisant le contenu du message d'un collègue, et ce, directement dans sa conversation.

Les extensions de messagerie basées sur des actions nécessitent souvent que les utilisateurs remplissent un formulaire ou un autre type de configuration au sein d’un modal. Vous pouvez créer ces expériences avec [modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="open-a-messaging-extension"></a>Ouvrir une extension de messagerie

La zone de rédaction et les messages ou publications sont les principaux contextes dans lesquels les utilisateurs utilisent des extensions de messagerie.

### <a name="from-the-compose-box"></a>À partir de la zone de rédaction

Une fois ajoutée, les utilisateurs peuvent ouvrir votre extension de messagerie en sélectionnant l'icône de votre application sous la zone de rédaction. Dans ces exemples, l’extension comporte des commandes de recherche et d’action.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="Exemple montrant comment ouvrir une extension de messagerie à partir de la zone de rédaction." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="Exemple montrant comment ouvrir une extension de messagerie à partir de la zone de rédaction sur un appareil mobile." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a>À partir d’un message de conversation ou d’un billet de canal

Une fois ajoutés, les utilisateurs peuvent sélectionner l’icône **Plus** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: dans le message de conversation ou le billet de canal pour rechercher les commandes d’action de votre extension. Votre extension peut être répertoriée sous **Plus d’actions** en fonction de l’utilisation.

> [!NOTE]
> La prise en charge d’autres actions à partir d’un message de conversation ou d’un billet de canal n’est pas disponible sur la plateforme mobile Microsoft Teams. 

#### <a name="chat-message"></a>Message de conversation

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="Exemple montrant comment ouvrir une extension de messagerie à partir d’un message de conversation." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="Exemple montrant comment ouvrir une extension de messagerie à partir d’un billet de conversation sur un appareil mobile." border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a>Utiliser une extension de messagerie

Les scénarios suivants montrent les principales façons dont les utilisateurs utilisent les extensions de messagerie.

### <a name="insert-content-into-a-message"></a>Insérer du contenu dans un message

**1. Sélectionner une extension de messagerie**. Les utilisateurs peuvent rechercher le contenu qu'ils veulent partager à partir de la zone de rédaction.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Exemple montrant un utilisateur recherchant du contenu à insérer à partir de la zone de rédaction." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="Exemple montrant un utilisateur recherchant du contenu à insérer à partir de la zone de rédaction sur un appareil mobile." border="false":::

---

**2. Insérer du contenu**. Une fois publiés, d’autres utilisateurs peuvent répondre ou sélectionner le contenu pour afficher plus d’informations dans votre application.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple montrant un utilisateur publiant du contenu dans une conversation de canal." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="Exemple montrant un utilisateur publiant du contenu dans une conversation de canal sur un appareil mobile." border="false":::

---

### <a name="take-action-on-a-message"></a>Effectuez des actions sur un message

**1. Sélectionner une extension de messagerie**. Votre application peut inclure une ou plusieurs commandes d’action.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Exemple montrant un utilisateur sélectionnant une commande d’action d’extension de messagerie." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="Exemple montrant un utilisateur sélectionnant une commande d’action d’extension de messagerie sur un appareil mobile." border="false":::

---

**2. Terminer l'action**. Votre application peut recevoir et traiter le contenu ou les données envoyés par l’action de message. Cela permet aux utilisateurs de rester dans leur conversation et, dans l’exemple suivant, de ne pas se soucier de la saisie d’informations directement dans votre application.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message sur un appareil mobile." border="false":::

---

### <a name="preview-links"></a>Liens d’aperçu

Les extensions de messagerie vous permettent également d’insérer des liens enrichis à partir d’une URL reconnue dans un message (cette fonctionnalité est appelée [lien en cours de déploiement](../../messaging-extensions/how-to/link-unfurling.md).)

**1. Coller un lien reconnu** dans la zone de rédaction.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Exemple montrant un utilisateur collant un lien dans la zone de rédaction." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="Exemple montrant un utilisateur collant un lien dans la zone de rédaction sur un appareil mobile." border="false":::

---

**2. Insérer du contenu**. Si votre application reconnaît l’URL dans la zone de rédaction, elle affiche le lien sous la forme d’une carte qui fournit un aperçu riche en contenu du contenu web. (Pour plus d’informations, consultez les [Instructions de conception de Cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md) .)

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="Exemple montrant comment l'URL, étant donné qu'elle est reconnue par votre application, inclut un contenu enrichi dans la zone de rédaction." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="Exemple montrant comment l'URL, étant donné qu'elle est reconnue par votre application, inclut un contenu enrichi dans la zone de rédaction sur un appareil mobile." border="false":::

---

## <a name="manage-a-messaging-extension"></a>Gérer une extension de messagerie

En cliquant avec le bouton droit sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de messagerie.

## <a name="anatomy"></a>Anatomie

### <a name="messaging-extension-in-the-compose-box"></a>Extension de messagerie dans la zone de rédaction

L’exemple suivant est une extension de messagerie ouverte à partir de la zone de rédaction.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'une extension de messagerie dans la zone de rédaction." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Logo de l’application** : icône couleur du logo de votre application.|
|2.|**Nom de l’application** : nom complet de votre application.|
|3|**Icône de menu Commandes d’action (facultatif)** : ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).
|4|**Zone de recherche** : permet aux utilisateurs de trouver le contenu de l’application qu’ils souhaitent insérer.|
|5|**Menu onglet (facultatif)** : fournit plusieurs catégories de contenu.|
|6|**Menu commandes d’action (facultatif)** : affiche la liste des commandes d’action (le cas échéant).|
|7|**Contenu de l’application** : principalement pour afficher les résultats de la recherche. L’exemple suivant utilise la disposition de liste (la disposition de la grille est une autre option).|
|8|**Logo de l’application** : icône contour du logo de votre application.|

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'une extension de messagerie dans la zone de rédaction sur un appareil mobile." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’application** : nom complet de votre application.|
|2.|**Icône de menu Commandes d’action (facultatif)** : ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).
|3|**Zone de recherche** : permet aux utilisateurs de trouver le contenu de l’application qu’ils souhaitent insérer.|
|4|**Menu onglet (facultatif)** : fournit plusieurs catégories de contenu.|
|5|**Menu commandes d’action (facultatif)** : affiche la liste des commandes d’action (le cas échéant).|
|6|**Contenu de l’application** : principalement pour afficher les résultats de la recherche.|

---

### <a name="messaging-extension-management-menu"></a>Menu de gestion des extensions de messagerie

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'un menu de gestion des extensions de messagerie." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Désépingler** : disponible si l’utilisateur a épinglé votre application.|
|2.|**Supprimer** : supprime l’extension de messagerie du canal, de la conversation ou de la réunion.|

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="setup-and-general-usage"></a>Configuration et utilisation générale

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple sur l’installation et l’utilisation générale." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>À faire : intégrer avec l’authentification unique

L’authentification unique facilite, accélère et sécurise le processus de connexion. En outre, si un utilisateur s’est déjà connecté à votre application personnelle, il n’a pas besoin de ’ se reconnecter pour accéder à l’extension de messagerie.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple d’intégration avec l’authentification unique." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>À ne pas faire : retirer les utilisateurs de la conversation

Les extensions de messagerie sont des raccourcis censés réduire le changement de contexte. Par exemple, votre extension ne doit pas diriger les utilisateurs vers une page web en dehors de Teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>À faire : mettre en surbrillance votre extension de messagerie

Les extensions de messagerie ne sont pas toujours faciles à trouver. Incluez des captures d’écran de l’utilisation dans la page de détails de votre application. Si votre application inclut également un bot, vous pouvez inclure la documentation d’aide de l’extension de messagerie dans une visite guidée de bienvenue du bot.

### <a name="templating"></a>Création de modèles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple sur la création de modèles." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>À faire : permettre à Teams de gérer une partie du travail de conception si possible

Si cela s'avère utile pour vos cas d'utilisation, envisagez de créer une extension de messagerie basée sur la recherche. Teams affiche ces types d’extensions avec un thème et une accessibilité intégrés.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple de gestion du travail de conception." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>À ne pas faire : incorporer l’intégralité de votre application dans un module de tâche

Si votre extension de messagerie nécessite des commandes d’action, conservez le module de tâche simple et affichez uniquement les composants nécessaires à l’exécution de l’action.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple sur les thèmes." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>À faire : tirer parti des jetons de couleur Teams

Chaque thème Teams a son propre modèle de couleurs. Pour gérer automatiquement les modifications de thème, utilisez <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">jetons de couleur (Fluent UI)</a> dans votre conception.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple sur les jetons de couleur." border="false":::

#### <a name="dont-hard-code-color-values"></a>À ne pas faire : valeurs de couleur du code dur

Si vous n’utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prendront plus de temps à gérer.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple sur les actions." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>À faire : inclure des commandes d’action qui ont du sens dans le contexte

Les actions de message doivent être liées à ce qu’un utilisateur examine. Par exemple, fournissez aux utilisateurs un raccourci pour créer un problème ou une tâche en utilisant le texte d'une publication.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple sur les commandes d’action." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>À ne pas faire : inclure des commandes d’actions qui ne sont pas contextuelles

Une action de message pour **Afficher votre tableau de bord** semble probablement déconnectée de la plupart des conversations.

   :::column-end:::
:::row-end:::

### <a name="searches"></a>Recherches

#### <a name="do-show-search-results-while-typing"></a>À faire : afficher les résultats de la recherche lors de la saisie

Fournissez des résultats de recherche suggérés pendant que les utilisateurs tapent. Ils peuvent trouver le contenu dont ils ont besoin plus rapidement avec un minimum de caractères.

#### <a name="dont-require-users-to-submit-a-query"></a>À ne pas faire : demander aux utilisateurs de soumettre une requête

Vous pouvez faire en sorte que les utilisateurs appuient sur une touche ou sélectionnent un bouton pour envoyer des requêtes à votre application. Bien que cela puisse être plus facile pour votre service de services d'applications, les utilisateurs peuvent être déconcertés par le fait qu'ils ne voient pas les résultats de recherche en temps réel au fur et à mesure qu'ils tapent.

#### <a name="do-consider-zero-term-queries"></a>À faire : prendre en compte les requêtes sans terme

Par exemple, avant qu’un utilisateur n’écrive quoi que ce soit dans la zone de recherche, affichez ce qu’il a affiché pour la dernière fois sur votre application. Il est possible qu'ils veuillent insérer ce contenu dans leur conversation.
