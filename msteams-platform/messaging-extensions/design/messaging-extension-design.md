---
title: Conception de votre extension de messagerie
description: Découvrez comment concevoir une extension de messagerie Teams et obtenir le kit d’interface Microsoft Teams’interface utilisateur.
keywords: les équipes conçoivent des lignes directrices sur les extensions de messagerie de référence conseils pratiques
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ed1f0f2eb2ce8d429a8a780bd2c4c4eb421d6d54
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566214"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Conception de votre extension Microsoft Teams messagerie

Les extensions de messagerie sont des raccourcis pour insérer du contenu d’application ou agir sur un message sans naviguer loin de la conversation.
Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les gens peuvent ajouter, utiliser et gérer les extensions de messagerie dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous pouvez trouver des lignes directrices complètes de conception d’extension de messagerie, y compris des éléments que vous pouvez saisir et modifier au besoin, dans le kit d Microsoft Teams’interface utilisateur.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>Ajouter une extension de messagerie

Vous pouvez ajouter une extension de messagerie dans les Teams suivants :

* À partir de Teams Store (AppSource).
* Dans un canal, chat ou réunion (avant, pendant et après) près de la boîte de composition. Il est intéressant de noter que si vous ajoutez une extension de messagerie dans l’un de ces endroits, vous seul pouvez l’utiliser dans ce contexte.

L’exemple suivant montre comment vous ajoutez une extension de messagerie dans un canal :

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="Exemple montre comment ajouter une extension de messagerie près de la boîte de composition dans un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a>Configurer une extension de messagerie

L’authentification n’est pas obligatoire, mais si votre application ressemble à un outil de suivi des billets, vous devrez peut-être que les gens se connectent pour utiliser l’extension de messagerie.

Pour plus de cohérence Teams les applications, vous ne pouvez pas personnaliser l’écran de dédisation. Si vous utilisez l’authentification unique de connect-on (SSO), les utilisateurs sont automatiquement connectés.

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="Exemple montre l’écran d’installation d’extension de messagerie avec un bouton de dédation." border="false":::

## <a name="types-of-messaging-extensions"></a>Types d’extensions de messagerie

Les extensions de messagerie peuvent avoir des commandes de recherche, des commandes d’action ou les deux. Vos commandes dépendent des fonctionnalités de votre application et de la façon dont celles-ci s’Teams les cas d’utilisation.

### <a name="search-commands"></a>Commandes de recherche

Avec les commandes de recherche, les gens peuvent utiliser votre extension de messagerie pour trouver rapidement du contenu externe et insérer dans un message. Les commandes de recherche sont généralement disponibles dans la boîte de composition. Par exemple, vous pouvez démarrer ou ajouter à une discussion en partageant un élément de contenu, sans jamais laisser Teams.

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Exemple montre une extension de messagerie basée sur la recherche lancée à partir de la boîte de composition." border="false":::

#### <a name="compose-box-layout-options"></a>Composer des options de mise en page de boîte

Vous avez quelques options pour afficher les résultats de recherche d’extension de messagerie, y compris les vues [de liste et de grille.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations montrant les options de mise en page pour les résultats de recherche d’extension de messagerie." border="false":::

### <a name="action-commands"></a>Commandes d'action

Les commandes d’action permettent aux gens de déclencher des actions et de traiter les demandes dans les services externes Teams. Par exemple, si votre application suit les commandes, un utilisateur peut créer une nouvelle commande en utilisant le contenu du message d’un collègue à partir de l’intérieur de son chat.

Les extensions de messagerie basées sur l’action exigent fréquemment que les utilisateurs remplissent un formulaire ou un autre type de configuration dans un module. Vous pouvez créer ces expériences avec des [modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="open-a-messaging-extension"></a>Ouvrez une extension de messagerie

La boîte de composition et les messages ou messages sont les principaux contextes où les gens utilisent des extensions de messagerie.

### <a name="from-the-compose-box"></a>De la boîte à composer

Une fois ajouté, les utilisateurs peuvent ouvrir votre extension de messagerie en sélectionnant l’icône de votre application sous la boîte de composition. Dans cet exemple, l’extension a des commandes de recherche et d’action :

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir de la boîte de composition." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a>À partir d’un message de chat ou d’un message de canal

Une fois ajouté,  les utilisateurs peuvent sélectionner :::image type="icon" source="../../assets/icons/teams-client-more.png"::: l’icône Plus sur le message de chat ou le message de canal pour trouver les commandes d’action de votre extension. Votre extension peut être répertoriée sous Plus **d’actions basées** sur l’utilisation.

> [!NOTE]
> La prise en charge d’un plus grand nombre d’actions à partir d’un message de chat ou d’une publication de canal n’est pas disponible Microsoft Teams la plate-forme mobile. 

#### <a name="chat-message"></a>Message de conversation

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir d’un message de chat." border="false":::

#### <a name="channel-post"></a>Poste de canal

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir d’un poste de canal." border="false":::

## <a name="use-a-messaging-extension"></a>Utiliser une extension de messagerie

Les scénarios suivants montrent les principales façons dont les gens utilisent les extensions de messagerie.

### <a name="insert-content-into-a-message"></a>Insérer du contenu dans un message

**1. Sélectionnez une extension de messagerie**. Les utilisateurs peuvent rechercher le contenu qu’ils souhaitent partager à partir de la boîte de composition.

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Exemple montre un utilisateur à la recherche de contenu à insérer à partir de la boîte de composition." border="false":::

**2. Insérer le contenu**. Une fois affiché, d’autres peuvent répondre ou sélectionner le contenu pour voir plus d’informations dans votre application.

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple montre un utilisateur affichant du contenu dans une conversation de canal." border="false":::

### <a name="take-action-on-a-message"></a>Agir sur un message

**1. Sélectionnez une extension de messagerie**. Votre application peut inclure une ou plusieurs commandes d’action.

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Exemple montre un utilisateur sélectionnant une commande d’action d’extension de messagerie." border="false":::

**2. Terminer l’action**. Votre application peut recevoir et traiter tout contenu ou données envoyés par l’action de message. Cela permet aux utilisateurs de rester dans leur conversation et, l’exemple suivant, de ne pas s’inquiéter d’entrer des informations directement dans votre application.

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message." border="false":::

### <a name="preview-links"></a>Liens d’aperçu

Les extensions de messagerie vous permettent également d’insérer des liens riches à partir d’une URL reconnue dans un message (cette fonctionnalité [est appelée lien de déploiement](../../messaging-extensions/how-to/link-unfurling.md).)

**1. Coller un lien reconnu dans** la boîte de composition.

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Exemple montre un utilisateur qui a passé un lien dans la boîte de compost." border="false":::

**2. Insérer le contenu**. Si votre application reconnaît l’URL dans la boîte de composition, elle rend le lien comme une carte qui fournit un aperçu riche en contenu du contenu Web. (Voir les lignes [directrices de conception des cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md) pour plus d’informations.)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="Exemple montre comment l’URL, puisqu’elle est reconnue par votre application, inclut un contenu riche dans la boîte de composition." border="false":::

## <a name="manage-a-messaging-extension"></a>Gérer une extension de messagerie

En cliquant à droite sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de messagerie.

## <a name="anatomy"></a>Anatomie

### <a name="messaging-extension-in-the-compose-box"></a>Extension de messagerie dans la boîte de composition

L’exemple suivant est une extension de messagerie ouverte à partir de la boîte de composition.

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration montrant l’anatomie d’interface utilisateur d’une extension de messagerie dans la boîte de composition." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Logo de l’application**: Icône couleur du logo de votre application.|
|2|**Nom de l’application**: Nom complet de votre application.|
|3|**Icône de menu commandes d’action (facultatif)**: Ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).
|4 |**Boîte de recherche**: Permet aux utilisateurs de trouver le contenu de l’application qu’ils souhaitent insérer.|
|5 |**Menu onglet (facultatif)**: Fournit plusieurs catégories de contenu.|
|6 |**Menu commandes d’action (facultatif)**: Affiche la liste des commandes d’action (si vous en spécifiez).|
|7 |**Contenu de l’application**: Principalement pour afficher les résultats de recherche. L’exemple ici est l’utilisation de la mise en page de liste (mise en page de grille est une autre option).|
|8 |**Logo de l’application**: Icône de contour du logo de votre application.|

### <a name="messaging-extension-management-menu"></a>Menu de gestion d’extension de messagerie

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration affichant l’anatomie d’interface utilisateur d’un menu de gestion d’extension de messagerie." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Unpin**: Disponible si l’utilisateur a épinglé votre application.|
|2|**Supprimer**: Supprime l’extension de messagerie du canal, du chat ou de la réunion.|

## <a name="best-practices"></a>Bonnes pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="setup-and-general-usage"></a>Configuration et utilisation générale

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple sur la configuration et l’utilisation générale." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>Faire: Intégrer avec un seul signe sur

SSO facilite, accélère et sécurise le processus de connexion. En outre, si un utilisateur s’est déjà connecté à votre application personnelle, il n’a pas à se connecter à nouveau pour accéder à l’extension de messagerie.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple sur l’intégration avec un seul signe." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>Ne pas : Éloignez les utilisateurs de la conversation

Les extensions de messagerie sont des raccourcis qui sont censés réduire la commutation de contexte. Votre extension ne doit pas, par exemple, diriger les utilisateurs vers une page Web en dehors de Teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Faire: Mettre en surbrillance votre extension de messagerie

Les extensions de messagerie ne sont pas toujours faciles à trouver. Incluez des captures d’écran de la façon de l’utiliser dans votre page de détails d’application. Si votre application inclut également un bot, vous pouvez inclure la documentation d’aide d’extension de messagerie dans une visite de bienvenue de bot.

### <a name="templating"></a>Templating (templating)

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple sur templating." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Faire: Laissez-Teams gérer une partie du travail de conception si possible

Si cela est logique pour vos cas d’utilisation, envisagez de créer une extension de messagerie basée sur la recherche. Teams rend ces types d’extensions avec le sur lent et l’accessibilité intégrés.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple sur le travail de conception de manipulation." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>Ne pas : Intégrer toute votre application dans un module de tâches

Si votre extension de messagerie nécessite des commandes d’action, gardez le module de tâches simple et affichez uniquement les composants nécessaires pour compléter l’action.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple sur le sujet." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Faire: Profitez de Teams de couleur

Chaque Teams a son propre schéma de couleurs. Pour gérer automatiquement les modifications de thème, <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">utilisez des jetons de couleur (interface utilisateur fluide)</a> dans votre conception.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple sur les jetons de couleur." border="false":::

#### <a name="dont-hard-code-color-values"></a>Ne pas : Valeurs de couleur de code dur

Si vous n’utilisez pas Teams jetons de couleur, vos créations seront moins évolutives et prennent plus de temps à gérer.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple sur les actions." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Faire : Inclure des commandes d’action qui ont du sens dans leur contexte

Les actions de message doivent se rapporter à ce qu’un utilisateur regarde. Par exemple, fournissez aux utilisateurs un raccourci pour créer un problème ou un élément de travail en utilisant le texte dans la publication de quelqu’un.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple sur les commandes d’action." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>Ne pas : Inclure des commandes d’actions qui ne sont pas contextuelles

Une action de message pour **afficher votre tableau de** bord semble probablement déconnectée de la plupart des conversations.

   :::column-end:::
:::row-end:::

### <a name="searches"></a>Recherches

#### <a name="do-show-search-results-while-typing"></a>Faire: Afficher les résultats de recherche tout en tapant

Fournissez les résultats de recherche suggérés pendant que les utilisateurs tapent. Ils peuvent trouver le contenu dont ils ont besoin plus rapidement avec un minimum de caractères.

#### <a name="dont-require-users-to-submit-a-query"></a>Ne pas : Exiger des utilisateurs qu’ils soumettent une requête

Vous pouvez faire appuyer sur une clé par les utilisateurs ou sélectionner un bouton pour envoyer des requêtes à votre application. Bien que cela puisse être plus facile sur votre service de services d’application, les gens peuvent être confus qu’ils ne voient pas les résultats de recherche en temps réel comme ils tapent.

#### <a name="do-consider-zero-term-queries"></a>Faire : Considérez les requêtes à durée zéro

Par exemple, avant qu’un utilisateur n’écrive quoi que ce soit dans la boîte de recherche, affichez ce qu’il a vu pour la dernière fois sur votre application. Il est possible qu’ils veuillent insérer ce contenu dans leur conversation.
