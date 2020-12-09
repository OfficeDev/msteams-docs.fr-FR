---
title: Création d’un onglet pour le bureau et le Web
description: Découvrez comment concevoir un onglet Teams (de bureau et Web) et obtenir le kit d’interface utilisateur de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604670"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a>Conception de votre onglet pour le bureau et le Web Microsoft teams

Un onglet est un grand canevas pour le contenu qui facilite la collaboration. Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer des onglets dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur Microsoft teams

Vous trouverez des instructions détaillées sur la conception des onglets, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams. Le kit d’interface utilisateur comporte également des rubriques essentielles, telles que l’accessibilité et le dimensionnement réactif, qui ne sont pas abordées ici.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>Ajouter un onglet

Vous pouvez ajouter un onglet à partir du magasin Teams (AppSource) ou dans l’un des contextes suivants :

* Conversation
* Canal
* Réunion (avant, pendant ou après la réunion)

L’exemple suivant montre comment un onglet est ajouté dans un canal.

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="Exemple illustre l’ajout d’un onglet à un canal." border="false":::

## <a name="set-up-a-tab"></a>Configurer un onglet

Il existe un petit processus de configuration pour ajouter une application sous la forme d’un onglet canal, conversation ou réunion. L’expérience est largement à votre place. Par exemple, vous pouvez avoir une description de l’utilisation de l’application et de certains paramètres facultatifs. Incluez ici une étape de connexion si vous devez authentifier les utilisateurs.

### <a name="tab-configuration-modal"></a>Configuration de l’onglet modal

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Exemple montre une configuration d’onglet modale." border="false":::

### <a name="anatomy-tab-configuration-modal"></a>Anatomie : modal de configuration d’onglet

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’une configuration d’onglet modale." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Logo** de l’application : logo de l’application couleur complète de votre application.|
|2 |**Nom** de l’application : nom complet de votre application.|
|3 |**IFRAME**: espace réactif pour le contenu de votre application (par exemple, paramètres de tabulation ou authentification).|
|4 |**À propos de Link**: ouvre une boîte de dialogue affichant plus d’informations sur l’application, telle qu’une description complète, les autorisations requises par l’application, ainsi que des liens vers votre politique de confidentialité et les conditions de service.
|5 |**Bouton Fermer**: ferme le modal.|
|6 |**Option de notification des membres** de l’équipe : le modal vous demande si vous souhaitez créer un billet indiquant que vous avez ajouté un onglet.|
|7 |**Bouton précédent**: passe à l’étape précédente en fonction de l’emplacement de la boîte de dialogue ouverte.|
|8 |**Bouton enregistrer**: termine la configuration de l’onglet.|

### <a name="tab-authentication-with-single-sign-on"></a>Authentification de l’onglet avec authentification unique

Vous pouvez ajouter une étape dans laquelle les utilisateurs doivent d’abord se connecter avec leurs informations d’identification Microsoft. Cette méthode d’authentification est appelée authentification unique (SSO).

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Exemple affiche un écran d’authentification de tabulation." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>Conception d’une configuration d’onglet avec des modèles d’interface utilisateur

Utilisez l’un des modèles d’interface utilisateur teams suivants pour vous aider à concevoir votre configuration d’onglet :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.

## <a name="view-a-tab"></a>Afficher un onglet

Les onglets fournissent une expérience Web en plein écran dans Teams, qui vous permet d’afficher du contenu collaboratif, ainsi que des tableaux de tâches et des tableaux de bord, ainsi que des informations importantes.

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="Exemple affiche un onglet avec un tableau des tâches." border="false":::

### <a name="anatomy-tab"></a>Anatomie : Tab

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’un onglet." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom** de l’onglet : étiquette de navigation pour votre onglet.|
|2 |**Débordement d’onglets**: ouvre les actions d’onglet, telles que renommer et supprimer.|
|3 |**Conversation par onglets**: ouvre un fil de conversation sur la droite, ce qui permet aux utilisateurs de disposer d’une conversation en regard du contenu.|
|4 |**IFRAME**: affiche le contenu de votre onglet.

### <a name="designing-a-tab-with-ui-templates"></a>Création d’un onglet avec des modèles d’interface utilisateur

Utilisez l’un des modèles d’interface utilisateur teams suivants pour vous aider à concevoir votre onglet :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.
* [Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board): un tableau des tâches, parfois appelé tableau kanban ou couloirs de natation, est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau](../../concepts/design/design-teams-app-ui-templates.md#dashboard)de bord : un tableau de bord est une zone de dessin contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.
* Navigation de [gauche](../../concepts/design/design-teams-app-ui-templates.md#left-nav): le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation. En règle générale, vous devez conserver la navigation par onglets au minimum.

## <a name="use-a-tab-to-collaborate"></a>Utiliser un onglet pour collaborer

Les onglets aident à faciliter les conversations sur le contenu à un emplacement central.

### <a name="thread-discussion"></a>Discussion de thread

Les utilisateurs peuvent automatiquement effectuer des publications sur un canal ou une conversation une fois qu’ils ont ajouté un nouvel onglet. Cette opération indique non seulement les membres de l’équipe du nouveau contenu et fournit un lien vers l’onglet, mais permet aux utilisateurs de commencer à parler de l’onglet.

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="Exemple montre un onglet discuté dans un thread de canal." border="false":::

### <a name="side-by-side-discussion"></a>Discussion côte à côte

Les utilisateurs peuvent avoir une conversation lors de l’affichage du contenu de l’onglet.

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="Exemple affiche un onglet avec une conversation ouverte sur le côté droit." border="false":::

### <a name="permissions-and-role-based-views"></a>Autorisations et vues basées sur les rôles

L’expérience utilisateur peut être différente pour les utilisateurs en fonction de leurs autorisations. Par exemple, un utilisateur peut accéder à l’onglet sans avoir à se connecter. Toutefois, un autre utilisateur doit se connecter et afficher un contenu légèrement différent.

## <a name="manage-a-tab"></a>Gérer un onglet

Vous pouvez inclure des options permettant de renommer, de supprimer ou de modifier un onglet.

### <a name="anatomy-tab-menu"></a>Anatomie : menu de l’onglet

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’un menu d’onglets." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Paramètres**: (facultatif) permet aux utilisateurs de modifier les paramètres d’un onglet après qu’il a été ajouté.|
|2 |**Rename**: permet aux utilisateurs d’attribuer un nom plus significatif à l’équipe.|
|3 |**Supprimer**: supprime l’onglet du canal, de la conversation ou de la réunion.|

## <a name="tab-notifications-and-deep-linking"></a>Notifications de tabulation et liens détaillés

Vous pouvez envoyer un message avec un lien détaillé vers votre onglet. Par exemple, une carte affiche un résumé des données de bogue qu’un utilisateur peut sélectionner pour afficher l’intégralité du bogue dans un onglet. L’envoi de messages sur l’activité des onglets augmente la sensibilisation sans notification explicite à tous les utilisateurs (c.-à-d., activité sans bruit). Vous pouvez également @mention des utilisateurs spécifiques, le cas échéant.

Avertissez les utilisateurs de l’activité des onglets de l’une des manières suivantes :

* **Bot**: cette méthode est préférée en particulier si le thread d’onglet est ciblé. La conversation de thème de l’onglet est déplacée vers le mode récemment actif. Cette méthode permet également une sophistication du mode d’envoi de la notification.
* **Message**: un message s’affiche dans le flux d’activités de l’utilisateur avec un [lien détaillé vers l’onglet](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).

## <a name="best-practices"></a>Meilleures pratiques

### <a name="collaboration"></a>Collaboration

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Illustration illustrant la marche à suivre pour la conception de la navigation par onglets." border="false":::

#### <a name="do-facilitate-conversation"></a>Do : faciliter la conversation

Inclure le contenu et les composants que les utilisateurs peuvent parler. S’il ne rentre pas dans le contexte d’une conversation, d’un canal ou d’une réunion, il n’appartient pas à votre onglet.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la navigation par onglet." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>Ne pas : traiter votre onglet comme n’importe quelle autre page Web

Un onglet n’est pas une page Web qui peut s’afficher une seule fois. Un onglet doit afficher votre contenu le plus important et pertinent dont les utilisateurs ont besoin pour effectuer une tâche conjointe.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Illustration illustrant la marche à suivre pour la conception de la navigation par onglets." border="false":::

#### <a name="do-limit-tasks-and-data"></a>Do : limiter les tâches et les données

Les onglets fonctionnent mieux lorsqu’ils répondent à des besoins spécifiques. Incluez un ensemble limité de tâches et de données pertinentes pour l’équipe ou le groupe.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la navigation par onglet." border="false":::

#### <a name="dont-embed-your-entire-app"></a>Ne pas : incorporer votre application entière

L’utilisation d’un onglet pour afficher une application entière avec une navigation à plusieurs niveaux et des interactions complexes entraîne une surcharge d’informations.

   :::column-end:::
:::row-end:::

### <a name="setup"></a>Configuration

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Illustration illustrant les actions à effectuer avec la conception de la configuration de l’onglet." border="false":::

#### <a name="do-keep-it-simple"></a>Do : restez simple

Si votre application requiert une authentification, essayez d’intégrer Microsoft Single Sign-On (SSO) pour une expérience de connexion plus transparente. En outre, n’incluez que les informations essentielles et les étapes à suivre pour ajouter l’onglet.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la configuration de l’onglet." border="false":::

#### <a name="dont-have-too-many-steps"></a>Ne pas faire : trop d’étapes

Supprimez toutes les étapes inutiles pour l’ajout d’un onglet.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Illustration illustrant la procédure d’affichage des onglets." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do : tirer parti des jetons de couleur teams

Chaque thème teams possède son propre jeu de couleurs. Pour gérer automatiquement les modifications de thème, utilisez des <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">jetons de couleur (IU Fluent)</a> dans votre conception.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Illustration illustrant ce qu’il ne faut pas faire avec des tabulations." border="false":::

#### <a name="dont-hard-code-color-values"></a>Ne pas : valeurs de couleur de code dur

Si vous n’utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prendre plus de temps à gérer.

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>Valider votre conception

Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.

> [!div class="nextstepaction"]
> [Vérifier les instructions de validation de la conception](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
