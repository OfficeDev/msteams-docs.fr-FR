---
title: Onglets de conception pour ordinateur de bureau, web et mobile
description: Découvrez comment concevoir un onglet Teams pour ordinateur de bureau, web et mobile, et obtenir le kit d’interface utilisateur de Microsoft Teams. Découvrez la fonctionnalité et l’apparence de l’onglet, la création de l’authentification utilisateur, les notifications de tabulation et la liaison approfondie dans les onglets.
author: heath-hamilton
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
keywords: Discussion sur le thread de la vue basée sur le rôle de liaison approfondie de l’AUTHENTIFICATION unique de la configuration de l’onglet
ms.openlocfilehash: 42f5a76c0499b3f50d90608d1f08e701caa13984
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887921"
---
# <a name="design-your-tab-for-microsoft-teams"></a>Concevoir votre onglet pour Microsoft Teams

Un onglet est un espace de grande taille pour le contenu de votre application. Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment des utilisateurs peuvent ajouter, utiliser et gérer des onglets dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions plus détaillées sur la conception d’onglet, y compris les éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d’interface utilisateur de Microsoft Teams. Le kit d’interface utilisateur contient également des rubriques essentielles telles que l’accessibilité et le dimensionnement réactif qui ne sont pas abordés ici.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>Ajouter un onglet

Vous pouvez ajouter un onglet à partir du Store Teams (AppSource) ou dans l’un des contextes suivants :

* Conversation
* Canal
* Réunion (avant, pendant ou après la réunion)

### <a name="mobile"></a>Mobile

Les utilisateurs peuvent accéder aux onglets en sélectionnant le bouton **Plus** dans le canal (exemple ci-dessous) ou la conversation dans laquelle ils ont été ajoutés.

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="L’exemple illustre l’ajout d’un onglet mobile dans un canal." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

L’exemple suivant montre comment les utilisateurs peuvent ajouter un onglet dans un canal.

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="L’exemple montre l’ajout d’un onglet dans un canal." border="false":::

## <a name="set-up-a-tab"></a>Configurer un onglet

Il existe un bref processus de configuration pour ajouter une application en tant qu’onglet de canal, conversation ou de réunion. C’est en grande partie à vous de faire l’expérience. Par exemple, vous pouvez avoir une description de l’utilisation de l’application et de certains paramètres facultatifs. Incluez une étape de connexion ici si vous devez authentifier les utilisateurs.

### <a name="tab-configuration-dialog"></a>Boîte de dialogue de configuration d’onglet

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Exemple de configuration modale d’onglet." border="false":::

#### <a name="anatomy-tab-configuration-dialog"></a>Anatomie : boîte de dialogue de configuration d’onglet

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’une configuration modale d’onglet." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Logo d’application** : logo d’application en couleur complète de votre application.|
|2|**Nom de l’application** : nom complet de votre application.|
|3|**IFrame** : espace réactif pour le contenu de votre application (par exemple, authentification ou paramètres d’onglet).|
|4|**À propos du lien** : ouvre une boîte de dialogue affichant plus d’informations sur l’application, telles qu’une description complète, les autorisations requises par l’application et les liens vers votre politique de confidentialité et les conditions d’utilisation.|
|5|**Bouton Fermer** : ferme la boîte de dialogue.|
|6 |**Option Avertir les membres de l’équipe** : la boîte de dialogue demande aux utilisateurs s’ils souhaitent créer un billet pour informer d’autres utilisateurs qu’ils ont ajouté un onglet.|
|7 |**Bouton Précédent** : passe à l’étape précédente en fonction de l’endroit où la boîte de dialogue s’est ouverte.|
|8 |**Bouton Enregistrer** : termine la configuration de l’onglet.|

### <a name="tab-authentication-with-single-sign-on"></a>Authentification d’onglet avec l’authentification unique

Vous pouvez ajouter une étape dans laquelle les utilisateurs doivent d’abord se connecter avec leurs informations d’identification Microsoft. Cette méthode d’authentification est appelée authentification unique (SSO).

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Exemple d’écran d’authentification de l’onglet." border="false":::

### <a name="design-a-tab-setup-with-ui-templates"></a>Concevoir une configuration d’onglet avec des modèles d’interface utilisateur

Utilisez l’un des modèles d’interface utilisateur Teams suivants pour vous aider à concevoir votre expérience de configuration d’onglet :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list) : les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form) : les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state) : le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la connexion, les expériences de première exécution, les messages d’erreur et bien plus encore.

## <a name="view-a-tab"></a>Afficher un onglet

Les onglets offrent une expérience web en plein écran dans Teams où vous pouvez afficher du contenu collaboratif (tableaux de tâches et tableaux de bord, par exemple) et des informations importantes.

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="L’exemple montre un onglet mobile avec un tableau des tâches." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="L’exemple montre un onglet avec un tableau des tâches." border="false":::

### <a name="anatomy-tab"></a>Anatomie : onglet

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un onglet." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’onglet** : étiquette de navigation pour votre onglet.|
|2|**Conversation par onglet**: ouvre une conversation qui permet aux utilisateurs d’avoir une conversation à côté du contenu.|
|3|**affichage web** : affiche le contenu de votre application.|

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Cette illustration montre l’anatomie de l’interface utilisateur d’un onglet." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’onglet** : étiquette de navigation pour votre onglet.|
|2|**Dépassement d’onglet** : ouvre les actions d’onglet, telles que renommer et supprimer.|
|3|**Conversation par onglet** : ouvre une conversation à droite, ce qui permet aux utilisateurs d’avoir une conversation à côté du contenu.|
|4|**IFrame** : affiche le contenu de votre application.|

### <a name="design-a-tab-with-ui-templates-and-advanced-components"></a>Concevoir un onglet avec des modèles d’interface utilisateur et des composants avancés

Utilisez l’un des composants et modèles Teams suivants pour vous aider à concevoir votre expérience d’onglet :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list) : les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.
* [Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board) : un tableau des tâches, parfois appelé « tableau kanban » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau de bord](../../concepts/design/design-teams-app-ui-templates.md#dashboard) : un tableau de bord est un espace contenant plusieurs cartes qui fournissent une vue d’ensemble de données ou de contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form) : les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state) : le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la connexion, les expériences de première exécution, les messages d’erreur et bien plus encore.
* [Navigation gauche](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav) : le composant de navigation gauche peut vous aider si votre onglet nécessite une navigation. En règle générale, vous devez conserver la navigation par onglets au minimum.

## <a name="use-a-tab-to-collaborate"></a>Utiliser un onglet pour collaborer

Les onglets facilitent les conversations relatives à un contenu dans un emplacement central.

### <a name="thread-discussion"></a>Conversation de thread

Les utilisateurs peuvent publier automatiquement sur un canal ou une conversation une fois qu’ils ont ajouté un nouvel onglet. Non seulement cela leur permet d’informer les membres de l’équipe du nouveau contenu et de fournir un lien vers l’onglet, mais les utilisateurs peuvent également commencer à discuter de l’onglet.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="L’exemple montre un onglet mobile abordé dans un thread de canal." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="L’exemple montre un onglet étant évoqué dans un thread de canal." border="false":::

### <a name="tab-chat"></a>Conversation par onglets

Les utilisateurs peuvent avoir une conversation en regard du contenu de l’onglet qu’ils affichent. Sur un ordinateur de bureau, la conversation s’ouvre sur le côté du contenu de l’application.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="L’exemple montre un onglet mobile avec une zone de conversation en contexte." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="L’exemple montre un onglet avec une conversation ouverte sur le côté droit." border="false":::

### <a name="permissions-and-role-based-views"></a>Autorisations et affichages en fonction du rôle

L’expérience d’onglet peut être différente pour les utilisateurs en fonction de leurs autorisations. Par exemple, un utilisateur peut accéder à l’onglet sans avoir à se connecter. Toutefois, un autre utilisateur doit se connecter et afficher un contenu légèrement différent.

## <a name="manage-a-tab"></a>Gérer un onglet

Vous pouvez inclure des options pour renommer, supprimer ou modifier un onglet.

### <a name="anatomy-tab-menu"></a>Anatomie : menu d’onglet

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un menu onglet mobile." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Ouvrir dans le navigateur** : ouvre l’application dans le navigateur par défaut de l’appareil.|
|2|**Lien Copier** : les utilisateurs peuvent copier et partager un lien vers l’onglet.|
|3|**Paramètres** : (Facultatif) Modifier les paramètres d’un onglet après son ajout.|
|4|**Renommer** : les utilisateurs peuvent donner à l’onglet un nom significatif pour le canal, la conversation ou la réunion.|
|5|**Supprimer** : supprime l’onglet du canal, de la conversation ou de la réunion.|

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un menu d’onglet." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Paramètres** : (Facultatif) Permet aux utilisateurs de modifier les paramètres d’un onglet après son ajout.|
|2|**Renommer** : les utilisateurs peuvent donner à l’onglet un nom significatif pour le canal, la conversation ou la réunion.|
|3|**Supprimer** : supprime l’onglet du canal, de la conversation ou de la réunion.|

## <a name="tab-notifications-and-deep-linking"></a>Notifications d’onglet et liaison approfondie

Vous pouvez envoyer un message avec un lien profond vers votre onglet. Par exemple, une carte affiche un résumé des données de bogue qu’un utilisateur peut sélectionner pour voir l’intégralité du bogue dans un onglet. L’envoi de messages sur l’activité de l’onglet augmente la sensibilisation sans avertir explicitement tout le monde (c’est-à-dire, activité sans bruit). Vous pouvez également @mentionner des utilisateurs spécifiques si nécessaire.

Informez les utilisateurs de l’activité de l’onglet de l’une des manières suivantes :

* **Bot** : cette méthode est préférée, en particulier si le thread d’onglet est ciblé. La conversation à thread de l’onglet est déplacée en tant que conversation récemment active. Cette méthode permet également une certaine complexité dans la façon dont la notification est envoyée.
* **Message** : un message s’affiche dans le flux d’activités de l’utilisateur avec un [lien profond vers l’onglet](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité :

### <a name="collaboration"></a>Collaboration

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Illustration montrant comment procéder avec la conception de navigation d’onglet." border="false":::

#### <a name="do-facilitate-conversation"></a>À faire : faciliter la conversation

Incluez le contenu et les composants dont les utilisateurs peuvent parler. S’ils ne s’intègrent pas dans le contexte d’une conversation, d’un canal ou d’une réunion, ils n’appartiennent pas à votre onglet.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="L’exemple montre ce qu’il ne faut pas faire avec la conception de navigation par onglets." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>À ne pas faire : traiter votre onglet comme n’importe quelle autre page web

Un onglet n’est pas une page web que quelqu’un peut afficher une seule fois. Un onglet doit afficher le contenu le plus important et pertinent dont les utilisateurs ont besoin pour accomplir quelque chose ensemble.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Exemple montrant comment procéder avec la conception de navigation par onglets." border="false":::

#### <a name="do-limit-tasks-and-data"></a>À faire : limiter les tâches et les données

Les onglets fonctionnent mieux lorsqu’ils s’adressent à des besoins spécifiques. Incluez un ensemble limité de tâches et de données pertinentes pour l’équipe ou le groupe.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de navigation par onglets." border="false":::

#### <a name="dont-embed-your-entire-app"></a>À ne pas faire : incorporer l’intégralité de votre application

L’utilisation d’un onglet pour afficher l’ensemble d’une application avec une navigation à plusieurs niveaux et des interactions complexes entraîne une surcharge d’informations.

   :::column-end:::
:::row-end:::

### <a name="setup"></a>Configuration

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Illustration montrant ce qu’il faut faire avec la conception de la configuration de l’onglet." border="false":::

#### <a name="do-keep-it-simple"></a>À faire : rester simple

Si votre application nécessite une authentification, essayez d’intégrer l’authentification unique (SSO) Microsoft pour une expérience d’authentification plus transparente. En outre, incluez uniquement les informations essentielles et les étapes à suivre pour ajouter l’onglet.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la configuration de l’onglet." border="false":::

#### <a name="dont-have-too-many-steps"></a>À ne pas faire : trop d’étapes

Supprimez les étapes inutiles pour ajouter un onglet.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Illustration montrant ce qu’il faut faire avec les thèmes d’onglet." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>À faire : tirer parti des jetons de couleur Teams

Chaque thème Teams a son propre modèle de couleurs. Pour gérer automatiquement les modifications de thème, utilisez <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">jetons de couleur (Fluent UI)</a> dans votre conception.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec les onglets." border="false":::

#### <a name="dont-hard-code-color-values"></a>À ne pas faire : valeurs de couleur du code en dur

Si vous n’utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prendront plus de temps à gérer.

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>Voir aussi

[Modifications des marges de l’onglet](~/resources/removing-tab-margins.md)
