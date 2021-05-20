---
title: Conception de votre onglet pour le bureau et le Web
description: Apprenez à concevoir un onglet Teams (bureau et web) et obtenez le kit d’interface utilisateur Microsoft Teams’interface utilisateur.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: baa17cd97ff4e2cad91615dced5c4e4cf5e533c8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566879"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a>Conception de votre onglet pour Microsoft Teams bureau et web

Un onglet est une grande toile pour votre contenu. Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les gens peuvent ajouter, utiliser et gérer les onglets dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous pouvez trouver des lignes directrices complètes de conception d’onglets, y compris des éléments que vous pouvez saisir et modifier au besoin, dans le kit d Microsoft Teams’interface utilisateur. La trousse d’interface utilisateur a également des sujets essentiels tels que l’accessibilité et le dimensionnement réactif qui ne sont pas couverts ici.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>Ajouter un onglet

Vous pouvez ajouter un onglet du magasin Teams (AppSource) ou dans l’un des contextes suivants :

* Conversation
* Canal
* Réunion (avant, pendant ou après la réunion)

L’exemple suivant montre comment un onglet est ajouté dans un canal :

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="Exemple montre un onglet ajouté dans un canal." border="false":::

## <a name="set-up-a-tab"></a>Configurer un onglet

Il y a un court processus de configuration pour ajouter une application en tant que canal, chat ou onglet de réunion. L’expérience dépend en grande partie de vous. Par exemple, vous pouvez avoir une description de la façon d’utiliser l’application et certains paramètres optionnels. Incluez une étape de dédentification ici si vous avez besoin d’authentifier les utilisateurs.

### <a name="tab-configuration-modal"></a>Configuration de l’onglet modal

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Exemple montre une configuration d’onglet modal." border="false":::

### <a name="anatomy-tab-configuration-modal"></a>Anatomie: Configuration de l’onglet modal

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Illustration affichant l’anatomie d’interface utilisateur d’un modal de configuration d’onglet." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Logo de l’application**: Logo de l’application en couleur de votre application.|
|2|**Nom de l’application**: Nom complet de votre application.|
|3|**iframe**: Espace réactif pour le contenu de votre application. Par exemple, paramètres d’onglet ou authentification.|
|4 |**À propos du** lien : Ouvre un dialogue montrant plus d’informations sur l’application, telles qu’une description complète, les autorisations requises par l’application et les liens vers votre politique de confidentialité et vos conditions de service.
|5 |**Bouton fermer**: Ferme le modale.|
|6 |**Aviser l’option membres** de l’équipe : Le modal vous demande si vous souhaitez créer un message permettant aux autres de savoir que vous avez ajouté un onglet.|
|7 |**Bouton arrière : Passe** à l’étape précédente en fonction de l’endroit où le dialogue s’est ouvert.|
|8 |**Enregistrer le bouton**: Termine la configuration de l’onglet.|

### <a name="tab-authentication-with-single-sign-on"></a>Authentification de l’onglet avec une seule inscription

Vous pouvez ajouter une étape dans laquelle les utilisateurs doivent d’abord se connecter avec leurs informations d’identification Microsoft. Cette méthode d’authentification est appelée simple connectement (SSO).

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Exemple montre un écran d’authentification d’onglet." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>Conception d’une configuration d’onglet avec des modèles d’interface utilisateur

Utilisez l’un des modèles d’interface Teams d’interface utilisateur suivants pour aider à concevoir votre expérience de configuration d’onglets :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): Les listes peuvent afficher des éléments connexes dans un format scannable et permettre aux utilisateurs de prendre des mesures sur une liste entière ou des éléments individuels.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): Les formulaires sont pour la collecte, la validation et la soumission structurée des entrées de l’utilisateur.
* [État vide :](../../concepts/design/design-teams-app-ui-templates.md#empty-state)Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la dé connecte, les expériences de première série, les messages d’erreur, et plus encore.

## <a name="view-a-tab"></a>Afficher un onglet

Les onglets offrent une expérience Web en plein écran dans les Teams où vous pouvez afficher du contenu collaboratif – tels que des tableaux de bord et des tableaux de bord – et des informations importantes.

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="Exemple montre un onglet avec un tableau de tâches." border="false":::

### <a name="anatomy-tab"></a>Anatomie: Onglet

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Illustration affichant l’anatomie d’interface utilisateur d’un onglet." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’onglet**: Étiquette de navigation pour votre onglet.|
|2|**Débordement d’onglets**: Ouvre les actions de l’onglet, telles que renommer et supprimer.|
|3|**Tab chat**: Ouvre un fil de chat sur la droite, permettant aux utilisateurs d’avoir une conversation à côté du contenu.|
|4 |**iframe**: Affiche le contenu de votre onglet.

### <a name="designing-a-tab-with-ui-templates"></a>Conception d’un onglet avec des modèles d’interface utilisateur

Utilisez l’un des modèles d Teams d’interface utilisateur suivants pour aider à concevoir votre expérience d’onglet :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): Les listes peuvent afficher des éléments connexes dans un format scannable et permettre aux utilisateurs de prendre des mesures sur une liste entière ou des éléments individuels.
* [Tableau de travail](../../concepts/design/design-teams-app-ui-templates.md#task-board): Un tableau de travail, parfois appelé planche kanban ou pistes de natation, est une collection de cartes souvent utilisées pour suivre l’état des articles de travail ou des billets.
* [Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : Un tableau de bord est une toile contenant plusieurs cartes qui donnent un aperçu des données ou du contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): Les formulaires sont pour la collecte, la validation et la soumission structurée des entrées de l’utilisateur.
* [État vide :](../../concepts/design/design-teams-app-ui-templates.md#empty-state)Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la dé connecte, les expériences de première série, les messages d’erreur, et plus encore.
* [Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)Le modèle de navigation gauche peut vous aider si votre onglet nécessite une certaine navigation. En général, vous devez garder un œil sur la navigation au minimum.

## <a name="use-a-tab-to-collaborate"></a>Utilisez un onglet pour collaborer

Les onglets facilitent les conversations sur le contenu dans un emplacement central.

### <a name="thread-discussion"></a>Discussion de fil

Les utilisateurs peuvent automatiquement publier sur un canal ou discuter une fois qu’ils ont ajouté un nouvel onglet. Cela permet non seulement d’aviser les membres de l’équipe du nouveau contenu et fournit un lien vers l’onglet, il permet aux gens de commencer à parler de l’onglet.

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="Exemple montre un onglet en cours de discussion dans un thread de canal." border="false":::

### <a name="side-by-side-discussion"></a>Discussion côte à côte

Les utilisateurs peuvent avoir une conversation ensuite tout en visualiser le contenu de l’onglet.

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="Exemple montre un onglet avec un chat ouvert sur le côté droit." border="false":::

### <a name="permissions-and-role-based-views"></a>Autorisations et vues basées sur les rôle

L’expérience de l’onglet peut être différente pour les utilisateurs en fonction de leurs autorisations. Par exemple, un utilisateur peut accéder à l’onglet sans avoir à se connecter. Un autre utilisateur, cependant, doit signer et verra un contenu légèrement différent.

## <a name="manage-a-tab"></a>Gérer un onglet

Vous pouvez inclure des options pour renommer, supprimer ou modifier un onglet.

### <a name="anatomy-tab-menu"></a>Anatomie: Menu onglet

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Illustration affichant l’anatomie d’interface utilisateur d’un menu d’onglet." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Paramètres**: (Facultatif) Permet aux utilisateurs de modifier les paramètres d’un onglet après son ajout.|
|2|**Renommer**: Permet aux utilisateurs de donner à l’onglet un nom plus significatif pour l’équipe.|
|3|**Supprimer**: Supprime l’onglet du canal, du chat ou de la réunion.|

## <a name="tab-notifications-and-deep-linking"></a>Notifications d’onglets et liaison profonde

Vous pouvez envoyer un message avec un lien profond vers votre onglet. Par exemple, une carte affiche un résumé des données de bogue qu’un utilisateur peut sélectionner pour voir l’ensemble du bogue dans un onglet. L’envoi de messages sur l’activité de l’onglet augmente la sensibilisation sans en informer explicitement tout le monde (c.-à-d. l’activité sans bruit). Vous pouvez également @mention utilisateurs spécifiques si nécessaire.

Informez les utilisateurs de l’activité de l’onglet de l’une des façons suivantes :

* **Bot**: Cette méthode est préférée surtout si le thread d’onglet est ciblé. La conversation filetée de l’onglet est déplacée en vue aussi récemment active. Cette méthode permet également une certaine sophistication dans la façon dont la notification est envoyée.
* **Message**: Un message apparaît dans le flux d’activité de l’utilisateur avec un [lien profond vers l’onglet](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).

## <a name="best-practices"></a>Bonnes pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité :

### <a name="collaboration"></a>Collaboration

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="L’illustration montre ce qu’il faut faire avec la conception de navigation d’onglet." border="false":::

#### <a name="do-facilitate-conversation"></a>Faire: Faciliter la conversation

Incluez le contenu et les composants dont les gens peuvent parler. S’il ne s’inscrit pas dans le contexte d’un chat, d’un canal ou d’une réunion, il n’a pas sa place dans votre onglet.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="Exemple montre ce qu’il ne faut pas faire avec la conception de navigation onglet." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>Ne pas : Traitez votre onglet comme n’importe quelle autre page Web

Un onglet n’est pas une page Web que quelqu’un peut afficher une fois. Un onglet doit afficher votre contenu le plus important et pertinent dont les gens ont besoin pour accomplir quelque chose ensemble.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Exemple montrant ce qu’il faut faire avec la conception de navigation d’onglet." border="false":::

#### <a name="do-limit-tasks-and-data"></a>Faire : Limiter les tâches et les données

Les onglets fonctionnent mieux lorsqu’ils répondent à des besoins spécifiques. Inclure un ensemble limité de tâches et de données pertinentes pour l’équipe ou le groupe.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de navigation d’onglet." border="false":::

#### <a name="dont-embed-your-entire-app"></a>Ne pas : Intégrir toute votre application

L’utilisation d’un onglet pour afficher une application entière avec navigation à plusieurs niveaux et interactions complexes conduit à une surcharge d’informations.

   :::column-end:::
:::row-end:::

### <a name="setup"></a>Configuration

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Illustration montrant ce qu’il faut faire avec la conception de configuration d’onglet." border="false":::

#### <a name="do-keep-it-simple"></a>Faire: Garder les choses simples

Si votre application nécessite une authentification, essayez d’intégrer microsoft single sign-on (SSO) pour une expérience de connexion plus transparente. En outre, ne comprennent que des informations essentielles et des étapes pour ajouter l’onglet.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de configuration d’onglet." border="false":::

#### <a name="dont-have-too-many-steps"></a>Ne pas: Avoir trop d’étapes

Supprimez toutes les étapes inutiles pour ajouter un onglet.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Illustration affichant ce qu’il faut faire avec le theming d’onglet." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Faire: Profitez de Teams de couleur

Chaque Teams a son propre schéma de couleurs. Pour gérer automatiquement les modifications de thème, <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">utilisez des jetons de couleur (interface utilisateur fluide)</a> dans votre conception.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec le theming d’onglet." border="false":::

#### <a name="dont-hard-code-color-values"></a>Ne pas : Valeurs de couleur de code dur

Si vous n’utilisez pas Teams jetons de couleur, vos créations seront moins évolutives et prennent plus de temps à gérer.

   :::column-end:::
:::row-end:::
