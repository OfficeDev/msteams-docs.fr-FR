---
title: Conception de votre extension de message
description: Découvrez comment concevoir une extension de message Teams et obtenir le Kit d’interface utilisateur Microsoft Teams. Décrit les conseils de conception d’équipes pour référencer les conseils sur les extensions de message
author: heath-hamilton
ms.localizationpriority: high
ms.author: surbhigupta
ms.topic: conceptual
ms.openlocfilehash: 2d3d31a0e59be22eb4f84bbdeb70897f4d584b83
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558750"
---
# <a name="designing-your-microsoft-teams-message-extension"></a>Conception de votre extension de message Microsoft Teams

Les extensions de message sont des raccourcis permettant d’insérer du contenu d’application ou d’agir sur un message sans quitter la conversation.
Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer des extensions de message dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions complètes de conception d’extension de message, y compris des éléments que vous pouvez récupérer et modifier si nécessaire, dans le Kit d’interface utilisateur Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-message-extension"></a>Ajouter une extension de message

Vous pouvez ajouter une extension de message dans les contextes Teams suivants :

* À partir de Teams Store.
* Dans un canal, une conversation ou une réunion (avant, pendant et après) près de la zone de rédaction. Il est important de noter que si vous ajoutez une extension de message à l’un de ces emplacements, vous seul pouvez l’utiliser dans ce contexte.

Les exemples suivants montrent comment ajouter une extension de message dans un canal.

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="L’exemple montre comment ajouter une extension de message près de la zone de composition dans un canal sur mobile.":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="L’exemple montre comment ajouter une extension de message près de la zone de composition dans un canal.":::

## <a name="set-up-a-message-extension"></a>Configurer une extension de message

L’authentification n’est pas obligatoire, mais si votre application ressemble à un outil de suivi des tickets, vous devrez peut-être vous connecter pour utiliser l’extension de message.

Pour assurer la cohérence entre les applications Teams, vous ne pouvez pas personnaliser l’écran de connexion. Si vous utilisez l’authentification unique (SSO), les utilisateurs sont connectés automatiquement.

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="L’exemple montre l’écran d’installation de l’extension de message avec un bouton de connexion sur mobile.":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="L’exemple montre l’écran d’installation de l’extension de message avec un bouton de connexion.":::

## <a name="types-of-message-extensions"></a>Types d’extensions de message

Les extensions de message peuvent avoir des commandes de recherche, des commandes d’action ou les deux. Vos commandes dépendent des fonctionnalités de votre application et de la façon dont elles s’intègrent aux cas d'utilisation Teams.

### <a name="search-commands"></a>Commandes de recherche

Avec les commandes de recherche, les utilisateurs peuvent utiliser votre extension de message pour rechercher rapidement du contenu externe et les insérer dans un message. Les commandes de recherche sont généralement disponibles dans la zone de rédaction. Par exemple, vous pouvez démarrer ou ajouter à une discussion en partageant un élément de contenu, sans jamais quitter Teams.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="L’exemple montre une extension de message basée sur la recherche lancée à partir de la zone de composition sur mobile.":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="L’exemple montre une extension de message basée sur la recherche lancée à partir de la zone de composition.":::

#### <a name="compose-box-layout-options"></a>Options de disposition de la zone de rédaction

Vous disposez de certaines options pour afficher les résultats de la recherche d’extension de message, notamment la [liste et les vues de grille](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations montrant les options de disposition pour les résultats de recherche d’extension de message.":::

### <a name="action-commands"></a>Commandes d'action

Les commandes d’action permettent aux utilisateurs de déclencher des actions et de traiter des demandes dans des services externes dans Teams. Par exemple, si votre application assure le suivi des commandes, un utilisateur peut créer une nouvelle commande en utilisant le contenu du message d'un collègue, et ce, directement dans sa conversation.

Les extensions de message basées sur des actions nécessitent souvent que les utilisateurs remplissent un formulaire ou un autre type de configuration au sein d’un modal. Vous pouvez créer ces expériences avec [modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="open-a-message-extension"></a>Ouvrir une extension de message

La zone de composition et les messages ou les billets sont les principaux contextes dans lesquels les utilisateurs utilisent des extensions de message.

### <a name="from-the-compose-box"></a>À partir de la zone de rédaction

Une fois ajoutés, les utilisateurs peuvent ouvrir votre extension de message en sélectionnant l’icône de votre application sous la zone de composition. Dans ces exemples, l’extension comporte des commandes de recherche et d’action.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="L’exemple montre comment ouvrir une extension de message à partir de la zone de composition sur un appareil mobile.":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="L’exemple montre comment ouvrir une extension de message à partir de la zone de composition.":::

### <a name="from-a-chat-message-or-channel-post"></a>À partir d’un message de conversation ou d’un billet de canal

Une fois ajoutés, les utilisateurs peuvent sélectionner l’icône **Plus** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: dans le message de conversation ou le billet de canal pour rechercher les commandes d’action de votre extension. Votre extension peut être répertoriée sous **Plus d’actions** en fonction de l’utilisation.

#### <a name="chat-message"></a>Message de conversation

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="L’exemple montrant comment ouvrir une extension de messagerie à partir d’un message de conversation.":::

#### <a name="channel-post"></a>Billet de canal

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="L’exemple montre comment ouvrir une extension de message à partir d’un billet de canal sur mobile.":::

## <a name="use-a-message-extension"></a>Utiliser une extension de message

Les scénarios suivants montrent les principales façons dont les utilisateurs utilisent les extensions de message.

### <a name="insert-content-into-a-message"></a>Insérer du contenu dans un message

**1. Sélectionnez une extension de message**. Les utilisateurs peuvent rechercher le contenu qu’ils souhaitent partager à partir de la zone de composition.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="Exemple montrant un utilisateur recherchant du contenu à insérer à partir de la zone de rédaction sur un appareil mobile.":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Exemple montrant un utilisateur recherchant du contenu à insérer à partir de la zone de rédaction.":::

**2. Insérer le contenu**. Une fois publiés, d’autres utilisateurs peuvent répondre ou sélectionner le contenu pour afficher plus d’informations dans votre application.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="Exemple montrant un utilisateur publiant du contenu dans une conversation de canal sur un appareil mobile.":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple montrant un utilisateur publiant du contenu dans une conversation de canal.":::

### <a name="take-action-on-a-message"></a>Effectuez des actions sur un message

**1. Sélectionner une extension de message**. Votre application peut inclure une ou plusieurs commandes d’action.

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="L’exemple montre un utilisateur qui sélectionne une commande d’action d’extension de message.":::

**2. Terminer l'action**. Votre application peut recevoir et traiter le contenu ou les données envoyés par l’action de message. Les utilisateurs terminent l’action dans votre application tout en restant dans leur conversation.

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message.":::

### <a name="preview-links"></a>Liens d’aperçu

Les extensions de message vous permettent également d’insérer des liens enrichis à partir d’une URL reconnue dans un message (cette fonctionnalité est appelée [le déploiement de liens](../../messaging-extensions/how-to/link-unfurling.md).)

**1. Coller un lien reconnu** dans la zone de rédaction.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="Exemple montrant un utilisateur collant un lien dans la zone de rédaction sur un appareil mobile.":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Exemple montrant un utilisateur collant un lien dans la zone de rédaction.":::

**2. Insérer le contenu**. Si votre application reconnaît l’URL dans la zone de composition, elle affiche le lien sous la forme d’une carte qui fournit un aperçu riche en contenu du contenu web. (Pour plus d’informations, consultez les [Instructions de conception de cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md) .)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="Exemple montrant comment l'URL, étant donné qu'elle est reconnue par votre application, inclut un contenu enrichi dans la zone de rédaction sur un appareil mobile.":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="Exemple montrant comment l'URL, étant donné qu'elle est reconnue par votre application, inclut un contenu enrichi dans la zone de rédaction.":::

## <a name="manage-a-message-extension"></a>Gérer une extension de message

En cliquant avec le bouton droit sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de message.

## <a name="anatomy"></a>Anatomie

### <a name="message-extension-in-the-compose-box"></a>Extension de message dans la zone de composition

Les exemples suivants montrent une extension de message ouverte à partir de la zone de composition.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’une extension de message dans la zone de composition sur mobile.":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’application** : nom complet de votre application.|
|2|**Icône de menu Commandes d’action (facultatif)**: ouvre une liste de commandes d’action pour votre extension de message (si vous en spécifiez une).
|3|**Zone de recherche** : permet aux utilisateurs de trouver le contenu de l’application qu’ils souhaitent insérer.|
|4|**Menu onglet (facultatif)** : fournit plusieurs catégories de contenu.|
|5|**Menu commandes d’action (facultatif)** : affiche la liste des commandes d’action (le cas échéant).|
|6 |**Contenu de l’application** : principalement pour afficher les résultats de la recherche.|

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’une extension de message dans la zone de composition.":::

|Compteur|Description|
|----------|-----------|
|1|**Logo de l’application** : icône couleur du logo de votre application.|
|2.|**Nom de l’application** : nom complet de votre application.|
|3|**Icône de menu Commandes d’action (facultatif)**: ouvre une liste de commandes d’action pour votre extension de message (si vous en spécifiez une).
|4|**Zone de recherche** : permet aux utilisateurs de trouver le contenu de l’application qu’ils souhaitent insérer.|
|5|**Menu onglet (facultatif)** : fournit plusieurs catégories de contenu.|
|6 |**Menu commandes d’action (facultatif)** : affiche la liste des commandes d’action (le cas échéant).|
|7 |**Contenu de l’application** : principalement pour afficher les résultats de la recherche. L’exemple suivant utilise la disposition de liste (la disposition de la grille est une autre option).|
|8 |**Logo de l’application** : icône contour du logo de votre application.|

### <a name="message-extension-management-menu"></a>Menu de gestion des extensions de message

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un menu de gestion des extensions de message.":::

|Compteur|Description|
|----------|-----------|
|1|**Désépingler** : disponible si l’utilisateur a épinglé votre application.|
|2|**Supprimer** : supprime l’extension de message du canal, de la conversation ou de la réunion.|

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="setup-and-general-usage"></a>Configuration et utilisation générale

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple sur l’installation et l’utilisation générale.":::

#### <a name="do-integrate-with-single-sign-on"></a>À faire : intégrer avec l’authentification unique

L’authentification unique facilite, accélère et sécurise le processus de connexion. En outre, si un utilisateur s’est déjà connecté à votre application personnelle, il n’a’ pas besoin de se reconnecter pour accéder à l’extension de message.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple d’intégration avec l’authentification unique.":::

#### <a name="dont-take-users-away-from-the-conversation"></a>À ne pas faire : retirer les utilisateurs de la conversation

Les extensions de message sont des raccourcis censés réduire le changement de contexte. Par exemple, votre extension ne doit pas diriger les utilisateurs vers une page web en dehors de Teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-message-extension"></a>À faire : mettre en surbrillance votre extension de message

Les extensions de message ne sont pas toujours faciles à trouver. Incluez des captures d’écran de l’utilisation dans la page de détails de votre application. Si votre application inclut également un bot, vous pouvez inclure la documentation d’aide sur l’extension de message dans une visite guidée de bienvenue du bot.

### <a name="templating"></a>Création de modèles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple sur la création de modèles.":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>À faire : permettre à Teams de gérer une partie du travail de conception si possible

Si cela est pertinent pour vos cas d’usage, envisagez de créer une extension de message basée sur la recherche. Teams affiche ces types d’extensions avec un thème et une accessibilité intégrés.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple de gestion du travail de conception.":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>À ne pas faire : incorporer l’intégralité de votre application dans un module de tâche

Si votre extension de message nécessite des commandes d’action, gardez le module de tâche simple et affichez uniquement les composants nécessaires pour effectuer l’action.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple sur les thèmes.":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>À faire : tirer parti des jetons de couleur Teams

Chaque thème Teams a son propre modèle de couleurs. Pour gérer automatiquement les modifications de thème, utilisez <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">jetons de couleur (Fluent UI)</a> dans votre conception.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple sur les jetons de couleur.":::

#### <a name="dont-hard-code-color-values"></a>À ne pas faire : valeurs de couleur du code dur

Si vous n’utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prendront plus de temps à gérer.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple sur les actions.":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>À faire : inclure des commandes d’action qui ont du sens dans le contexte

Les actions de message doivent être liées à ce qu’un utilisateur examine. Par exemple, fournissez aux utilisateurs un raccourci pour créer un problème ou une tâche en utilisant le texte d'une publication.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple sur les commandes d’action.":::

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
