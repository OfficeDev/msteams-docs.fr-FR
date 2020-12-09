---
title: Conception de votre extension de messagerie
description: Découvrez comment concevoir une extension de messagerie teams et obtenir le kit d’interface utilisateur Microsoft Teams.
keywords: recommandations pour la conception des équipes de référence des extensions de messagerie conseils
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ad628bdaa46058aed4acdcea1a224c7ebfe40f89
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604821"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Conception de votre extension de messagerie Microsoft teams

Les extensions de messagerie sont des raccourcis permettant d’insérer du contenu d’application ou d’agir sur un message sans quitter la conversation.

Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer les extensions de messagerie dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur Microsoft teams

Vous trouverez des instructions de conception de l’extension de messagerie complète, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>Ajouter une extension de messagerie

Vous pouvez ajouter une extension de messagerie dans les contextes de teams suivants :

* À partir du magasin de Teams (AppSource).
* Dans un canal, une conversation ou une réunion (avant, pendant et après) à proximité de la zone de composition. Il est important de noter si vous ajoutez une extension de messagerie à l’un de ces emplacements, vous seul pouvez l’utiliser dans ce contexte.

L’exemple suivant montre comment ajouter une extension de messagerie dans un canal.

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="Cet exemple montre comment ajouter une extension de messagerie à proximité de la zone de composition d’un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a>Configurer une extension de messagerie

L’authentification n’est pas obligatoire, mais si votre application est semblable à un outil de suivi des tickets, vous aurez peut-être besoin que des personnes se connectent pour utiliser l’extension de messagerie.

Pour assurer la cohérence entre les applications Teams, vous ne pouvez pas personnaliser l’écran de connexion. Si vous utilisez l’authentification unique (SSO), les utilisateurs se connectent automatiquement.

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="Exemple affiche l’écran de configuration de l’extension de messagerie avec un bouton de connexion." border="false":::

## <a name="types-of-messaging-extensions"></a>Types d’extensions de messagerie

Les extensions de messagerie peuvent être dotées de commandes de recherche, de commandes d’action ou des deux. Vos commandes dépendent des fonctionnalités de votre application et de la façon dont elles rentrent dans les cas d’utilisation de teams.

### <a name="search-commands"></a>Commandes de recherche

Grâce aux commandes de recherche, les utilisateurs peuvent utiliser votre extension de messagerie pour trouver rapidement du contenu externe et l’insérer dans un message. Les commandes de recherche sont généralement disponibles dans la zone de composition. Par exemple, vous pouvez commencer ou ajouter une discussion en partageant une partie de contenu, sans jamais quitter Teams.

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Exemple montre une extension de messagerie basée sur la recherche lancée à partir de la zone de composition." border="false":::

#### <a name="compose-box-layout-options"></a>Options de disposition de la zone de composition

Vous disposez de plusieurs options pour afficher les résultats de recherche d’extension de messagerie, y compris les [affichages de liste et de grille](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations illustrant les options de disposition pour les résultats de recherche de l’extension de messagerie." border="false":::

### <a name="action-commands"></a>Commandes d’action

Les commandes d’action permettent aux utilisateurs de déclencher des actions et de traiter des demandes dans des services externes au sein de teams. Par exemple, si votre application suit les commandes, un utilisateur peut créer une nouvelle commande en utilisant le contenu du message d’un collègue de droite à l’intérieur de la conversation.

Les extensions de messagerie basées sur les actions nécessitent fréquemment que les utilisateurs exécutent un formulaire ou un autre type de configuration dans un modal. Vous pouvez créer ces expériences avec des [modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="open-a-messaging-extension"></a>Ouverture d’une extension de messagerie

La zone de composition et les messages/publications sont les contextes principaux dans lesquels les utilisateurs utilisent les extensions de messagerie.

### <a name="from-the-compose-box"></a>De la zone de composition

Une fois ajoutés, les utilisateurs peuvent ouvrir votre extension de messagerie en sélectionnant l’icône de votre application sous la zone de composition. Dans cet exemple, l’extension est dotée de commandes de recherche et d’action.

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir de la zone de composition." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a>À partir d’un message de conversation ou d’un billet de canal

Une fois ajoutés, les utilisateurs peuvent sélectionner l’icône **plus** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: sur le message de conversation ou le billet de canal pour trouver les commandes d’action de votre extension. Votre extension peut être indiquée sous **autres actions** en fonction de l’utilisation.

#### <a name="chat-message"></a>Message de conversation

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir d’un message de conversation." border="false":::

#### <a name="channel-post"></a>Billet de canal

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir d’un billet de canal." border="false":::

## <a name="use-a-messaging-extension"></a>Utiliser une extension de messagerie

Les scénarios suivants montrent les principales façons dont les utilisateurs utilisent les extensions de messagerie.

### <a name="insert-content-into-a-message"></a>Insérer du contenu dans un message

**1. Sélectionnez une extension de messagerie**. Les utilisateurs peuvent rechercher le contenu qu’ils souhaitent partager à partir de la zone de composition.

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Cet exemple montre comment afficher un utilisateur qui recherche du contenu à insérer à partir de la zone de composition." border="false":::

**2. Insérez du contenu**. Une fois publiés, les autres utilisateurs peuvent répondre ou sélectionner le contenu pour afficher plus d’informations dans votre application.

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple affiche un utilisateur publiant du contenu dans une conversation de canal." border="false":::

### <a name="take-action-on-a-message"></a>Effectuer une action sur un message

**1. Sélectionnez une extension de messagerie**. Votre application peut inclure une ou plusieurs commandes d’action.

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Exemple montre un utilisateur sélectionnant une commande action d’extension de messagerie." border="false":::

**2. Terminez l’action**. Votre application peut recevoir et traiter tout contenu ou données envoyé par l’action de message. Cela permet aux utilisateurs de rester dans leur conversation et, dans l’exemple suivant, de ne pas se soucier de saisir directement des informations dans votre application.

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Cet exemple montre comment afficher un utilisateur qui recherche du contenu à insérer à partir de la zone de composition." border="false":::

### <a name="preview-links"></a>Aperçu des liens

Les extensions de messagerie vous permettent également d’insérer des liens enrichis à partir d’une URL reconnue dans un message (cette fonctionnalité est appelée [Link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)

**1. collez un lien reconnu** dans la zone de composition.

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Exemple montre comment un utilisateur colle un lien dans la zone compost." border="false":::

**2. Insérez du contenu**. Si votre application reconnaît l’URL dans la zone de composition, elle affiche le lien sous la forme d’une carte qui fournit un aperçu riche en contenu du contenu Web. (Pour plus d’informations, consultez la rubrique [instructions de conception des cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md) .)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="Cet exemple montre comment l’URL, telle qu’elle est reconnue par votre application, inclut du contenu enrichi dans la zone de composition." border="false":::

## <a name="manage-a-messaging-extension"></a>Gérer une extension de messagerie

En cliquant avec le bouton droit sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de messagerie.

## <a name="anatomy"></a>Anatomie

### <a name="messaging-extension-in-the-compose-box"></a>Extension de messagerie dans la zone de composition

L’exemple suivant est une extension de messagerie ouverte à partir de la zone de composition.

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’une extension de messagerie dans la zone de composition." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Logo** de l’application : icône de couleur du logo de votre application.|
|2 |**Nom** de l’application : nom complet de votre application.|
|3 |**Icône de menu commandes d’action (facultatif)**: ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).
|4 |**Zone de recherche**: permet aux utilisateurs de trouver le contenu d’application qu’ils souhaitent insérer.|
|5 |**Menu de l’onglet (facultatif)**: fournit plusieurs catégories de contenu.|
|6 |**Menu commandes d’action (facultatif)**: affiche la liste des commandes d’action (si vous en spécifiez une).|
|7 |**Contenu** de l’application : principalement pour afficher les résultats de la recherche. Cet exemple utilise la mise en forme de liste (la disposition grille est une autre option).|
|8 |**Logo** de l’application : icône de plan du logo de votre application.|

### <a name="messaging-extension-management-menu"></a>Menu gestion des extensions de messagerie

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’un menu de gestion des extensions de messagerie." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Détacher**: disponible si l’utilisateur a épinglé votre application.|
|2 |**Remove**: supprime l’extension de messagerie du canal, de la conversation ou de la réunion.|

## <a name="best-practices"></a>Meilleures pratiques

### <a name="setup-and-general-usage"></a>Configuration et utilisation générale

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>Do : intégration avec l’authentification unique

SSO rend le processus de connexion plus facile, plus rapide et plus sécurisé. En outre, si un utilisateur s’est déjà connecté à votre application personnelle, il n’a pas besoin de se connecter à nouveau pour accéder à l’extension de messagerie.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>Ne pas : empêcher les utilisateurs de participer à la conversation

Les extensions de messagerie sont des raccourcis qui sont supposés réduire le changement de contexte. Votre extension ne doit pas, par exemple, diriger les utilisateurs vers une page Web en dehors de teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Do : mettez en surbrillance votre extension de messagerie

Les extensions de messagerie ne sont pas toujours faciles à trouver. Incluez des captures d’écran expliquant comment l’utiliser dans la page de détails de votre application. Si votre application inclut également un bot, vous pouvez inclure la documentation d’aide sur les extensions de messagerie dans une présentation de robot.

### <a name="templating"></a>Création

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Do : Permettez à teams de gérer une partie du travail de conception si cela est possible

Si cela est utile pour vos cas d’utilisation, envisagez de créer une extension de messagerie basée sur la recherche. Teams affiche ces types d’extensions avec des thèmes et une accessibilité intégrés.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>Ne pas : incorporer l’intégralité de votre application dans un module de tâches

Si votre extension de messagerie nécessite des commandes d’action, conservez le module de tâches simple et Affichez uniquement les composants requis pour effectuer l’action.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do : tirer parti des jetons de couleur teams

Chaque thème teams possède son propre jeu de couleurs. Pour gérer automatiquement les modifications de thème, utilisez des <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">jetons de couleur (IU Fluent)</a> dans votre conception.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="dont-hard-code-color-values"></a>Ne pas : valeurs de couleur de code dur

Si vous n’utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prendre plus de temps à gérer.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Do : inclure des commandes d’action qui ont un sens dans le contexte

Les actions de message doivent être liées à ce qu’un utilisateur examine. Par exemple, fournissez aux utilisateurs un raccourci pour la création d’un problème ou d’un élément de travail à l’aide du texte dans la publication d’une personne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>Ne pas : inclure les commandes d’actions qui ne sont pas contextuelles

Une action de message pour **afficher votre tableau de bord** semblerait probablement déconnectée de la plupart des conversations.

   :::column-end:::
:::row-end:::

### <a name="searches"></a>Recherches

#### <a name="do-show-search-results-while-typing"></a>Do : afficher les résultats de la recherche lors de la saisie

Fournissez les suggestions de résultats de recherche pendant que les utilisateurs tapent. Ils peuvent trouver le contenu dont ils ont besoin plus rapidement avec un minimum de caractères.

#### <a name="dont-require-users-to-submit-a-query"></a>Ne pas : exiger que les utilisateurs envoient une requête

Vous pouvez faire en sorte que les utilisateurs appuient sur une touche ou sélectionnent un bouton pour envoyer des requêtes à votre application. Bien que cela puisse être plus facile sur votre service d’application, il se peut que les utilisateurs ne voient pas les résultats de recherche en temps réel lorsqu’ils sont tapés.

#### <a name="do-consider-zero-term-queries"></a>Do : prendre en compte les requêtes à zéro terme

Par exemple, avant qu’un utilisateur n’écrit quoi que ce soit dans la zone de recherche, affichez ce qu’il a consulté en dernier sur votre application. Il est possible qu’ils souhaitent insérer ce contenu dans leur conversation.

## <a name="validate-your-design"></a>Valider votre conception

Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.

> [!div class="nextstepaction"]
> [Vérifier les instructions de validation de la conception](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
