---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans le Teams et obtenir le kit d’interface Microsoft Teams’interface utilisateur.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 0a888c333305e9caafcd0bac0e5549bf08ead424
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566025"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Concevoir votre extension Microsoft Teams réunion

Vous pouvez créer des applications pour rendre les réunions plus productives. Par exemple, demandez aux gens de remplir un sondage lors d’un appel ou d’envoyer un rappel rapide qui n’interrompt pas le déroulement de la réunion.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous pouvez trouver des lignes directrices de conception plus complètes, y compris des éléments que vous pouvez saisir et modifier au besoin, dans le kit d Microsoft Teams’interface utilisateur.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Ajouter une extension de réunion

Vous pouvez ajouter une extension de réunion avant et pendant les réunions. Vous pouvez également ajouter une application pour une réunion spécifique directement à partir du Teams store (AppSource).

### <a name="add-before-a-meeting"></a>Ajouter avant une réunion

Dans les détails de la réunion, **sélectionnez Ajouter un onglet +** pour ouvrir le flyout de l’application et trouver des applications optimisées pour les réunions.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a>Ajouter lors d’une réunion

Lors d’une réunion, **sélectionnez** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Ajouter une application et** choisissez l’application que vous souhaitez.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Exemple montre comment ajouter une extension de réunion lors d’une réunion." border="false":::

## <a name="before-a-meeting"></a>Avant une réunion

Avant votre réunion, vous pouvez ajouter du contenu dans l’onglet. L’exemple suivant montre un projet de question de sondage à laquelle les gens répondront pendant l’appel.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="Exemple montre comment app contenu dans les détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomie: Onglet Réunion (avant et après les réunions)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="Exemple montre l’anatomie structurale d’un onglet de réunion avant et après une réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’onglet**: Étiquette de navigation pour votre onglet.|
|2|**Débordement d’onglets**: Ouvre les actions de l’onglet, telles que renommer et supprimer.|
|3|**iframe**: Affiche le contenu de votre application.|

### <a name="designing-with-ui-templates"></a>Conception avec des modèles d’interface utilisateur

Utilisez l’un des modèles d Teams d’interface utilisateur suivants pour aider à concevoir votre onglet réunion :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): Les listes peuvent afficher des éléments connexes dans un format scannable et permettre aux utilisateurs de prendre des mesures sur une liste entière ou des éléments individuels.
* [Tableau de travail](../../concepts/design/design-teams-app-ui-templates.md#task-board): Un tableau de travail, parfois appelé planche kanban ou pistes de natation, est une collection de cartes souvent utilisées pour suivre l’état des articles de travail ou des billets.
* [Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : Un tableau de bord est une toile contenant plusieurs cartes qui donnent un aperçu des données ou du contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): Les formulaires sont pour la collecte, la validation et la soumission structurée des entrées de l’utilisateur.
* [État vide :](../../concepts/design/design-teams-app-ui-templates.md#empty-state)Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la dé connecte, les expériences de première série, les messages d’erreur, et plus encore.
* [Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)Le modèle de navigation gauche peut vous aider si votre onglet nécessite une certaine navigation. En général, vous devez garder un œil sur la navigation au minimum.

## <a name="use-an-in-meeting-tab"></a>Utiliser un onglet en réunion

L’onglet en réunion est une toile pour augmenter la collaboration pendant les réunions. Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de l’étape de la réunion grâce à des vues partagées ou basées sur des rôle.

### <a name="use-cases"></a>Cas d’utilisation

Les gens peuvent utiliser l’onglet en réunion pour :

* Fournir une rétroaction détaillée. Par exemple, évaluez un candidat à un emploi.
* Créez un sondage, un sondage ou un élément de tâche pour les participants à la réunion.
* Affichez les notes pertinentes à la réunion. Par exemple, des informations sur un responsable commercial.

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Exemple montre comment vous pouvez présenter le contenu du sondage dans un onglet en réunion." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomie: Onglet en réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="Exemple montre l’anatomie structurale d’un onglet en réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application (sélectionnée)**: logo transparent de l’application de 16 pixels.|
|2|**Nom de l'application**|
|3|**En-tête**: Inclut le nom de votre application.|
|4 |**Bouton fermer**: Rejette l’onglet. Utilisez toujours l’icône de fermeture supérieure-droite au lieu d’une action dans le pied.|
|5 |**Barre de notification**: Les alertes d’erreur s’affichent directement sous l’en-tête et font baisser le contenu de l’iframe de 20 pixels.|
|6 |**iframe**: Affiche le contenu de votre application.|

### <a name="spacing"></a>Espacement

Optimisez votre onglet en réunion pour vous adapter de bord en bord dans la zone iframe de 280 pixels de large. Il y a 20 pixels de rembourrage sur les côtés gauche et droit de l’iframe et entre l’en-tête de l’onglet. L’iframe est saigné au fond de l’onglet.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Exemple montre les dimensions d’espacement des onglets en réunion." border="false":::

### <a name="scrolling"></a>défilement

Le contenu iframe doit défiler verticalement. Vous ne pouvez voir que le contenu sur quoi vous avez fait défiler (rien au-dessus ou au-dessous). La barre de défilement fait partie du contenu iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Exemple montre comment l’onglet en réunion défile." border="false":::

### <a name="navigation"></a>Navigation

Pour les scénarios avec des couches de navigation ou un contenu lourd, nous vous recommandons de permettre aux utilisateurs de naviguer vers une couche secondaire. Les utilisateurs doivent pouvoir revenir à la couche précédente.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple montre la navigation en réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Utiliser un dialogue en réunion

Les dialogues en réunion s’affichent sur Teams étape de la réunion. Ils nécessitent l’attention, la confirmation ou l’interaction d’un utilisateur, mais sont subtils et n’interrompent pas la réunion. Vous devez les utiliser avec parcimonie et pour des scénarios qui sont légers et axés sur les tâches.

### <a name="use-cases"></a>Cas d’utilisation

Les dialogues en réunion sont déclenchés par un utilisateur (tel que l’organisateur de la réunion) qui peut vouloir que les participants :

* Fournir de brèves commentaires
* Faites un court sondage ou un sondage
* Soumettre les approbations
* Obtenez des rappels

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Exemple montre comment vous pouvez utiliser un dialogue en réunion." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomie: Dialogue en réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="Exemple montre l’anatomie structurelle d’un dialogue en réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**En-tête**: Inclut l’icône d’application, le nom, la chaîne d’action et l’icône proche.|
|2|**iframe**: Affiche le contenu de votre application.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomie : En-tête de dialogue en réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Exemple montre l’anatomie structurale d’un en-tête de dialogue en réunion." border="false":::

Il existe deux variantes d’en-tête. Dans la mesure du possible, utilisez la variante avec l’avatar pour renforcer que le dialogue vient d’une personne.

|Compteur|Description|
|----------|-----------|
|1|**Avatar**: Personne qui initie le dialogue en réunion.|
|2|**Icône de l’application**|
|3|**Nom de l'application**|
|4 |**Bouton fermer**: Rejette le dialogue.|
|5 |**Chaîne d’action**: Décrit généralement qui a initié le dialogue.|

### <a name="responsive-behavior"></a>Comportement réactif

Les dialogues en réunion peuvent varier en taille pour tenir compte de différents scénarios. Assurez-vous de maintenir le rembourrage et la taille des composants.

* **Largeur**: Vous pouvez spécifier la largeur de l’iframe du dialogue n’importe où dans la plage de taille prise en charge.
* **Hauteur**: Vous pouvez spécifier la hauteur de l’iframe du dialogue n’importe où dans la plage de taille prise en charge. Vous pouvez également permettre aux utilisateurs de faire défiler verticalement si le contenu de votre application dépasse la hauteur maximale.

Pour implémenter, spécifiez la largeur et la hauteur à l’aide de [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) la clé.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple montre le dialogue en réunion. Largeur: Min--280 pixels (248 pixels iframe). Max---460 pixels (428 pixels iframe). Hauteur: 300 pixels (iframe)." border="false":::

## <a name="after-a-meeting"></a>Après une réunion

Vous pouvez revenir à une réunion après sa fin et afficher le contenu de l’application. Dans cet exemple, l’organisateur de la réunion peut examiner les résultats du sondage dans **l’onglet Contoso.** (Note : Du point de vue de la conception, il n’y a pas de différence entre l’expérience de l’onglet avant et après la réunion.)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="Exemple d’illustration montre un onglet post-réunion." border="false":::

## <a name="best-practices"></a>Bonnes pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="interactions"></a>Interactions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple montrant comment limiter le nombre d’interactions." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Faire : Limiter le nombre d’interactions

Pour les dialogues en réunion, supprimez le contenu inutile qui n’aide pas les utilisateurs à accomplir quelque chose rapidement.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple montrant comment ne pas introduire d’éléments inutiles." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>Ne pas : Introduire des éléments inutiles

Un seul dialogue en réunion avec plusieurs interactions peut détourner l’attention de l’appel.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Disposition

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple montrant comment vous devez utiliser une mise en page de dialogue à colonne unique." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>Faire : Utiliser une mise en page de dialogue à colonne unique

Étant donné que les dialogues sont au centre de l’étape de la réunion, l’achèvement des tâches doit être rapide et simple pour éviter la frustration des utilisateurs.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple montrant que vous ne devriez pas encombrer l’espace d’une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a>Ne pas : encombrer l’espace

Le contenu dense ou trop structuré peut être distrayant et accablant, surtout lors d’une réunion.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montrant une mise en page d’onglet à colonne unique." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>Faire : Utilisez une mise en page d’onglet à colonne unique

Compte tenu de la nature étroite de l’onglet en réunion, nous vous recommandons fortement d’afficher le contenu dans une seule colonne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple montrant un onglet avec plusieurs colonnes." border="false":::

#### <a name="dont-use-multiple-columns"></a>Ne pas : Utilisez plusieurs colonnes

En raison de l’espace limité de l’onglet en réunion, les dispositions avec plus d’une colonne ne sont pas recommandées.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Contrôles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Exemple montrant comment aligner à droite les contrôles primaires." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Faire: Droit aligner l’action primaire

Nous vous recommandons de positionner l’action la plus lourde visuellement à l’endroit le plus approprié.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple montrant comment vous ne devriez pas laisser aligner les contrôles primaires." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>Ne pas : La gauche ou le centre alignent les actions

Cela s’écarte de la norme Teams modèle de contrôle dans un dialogue et peut entrer en conflit avec un dialogue derrière le haut.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Faire défiler

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple montrant le défilement vertical dans un onglet en réunion." border="false":::

#### <a name="do-scroll-vertically"></a>Faire: Faire défiler verticalement

Les utilisateurs s’attendent à un défilement vertical Teams (et ailleurs).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple montrant le défilement horizontal dans un onglet en réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a>Ne pas : Faites défiler horizontalement

Le défilement horizontal n’est pas un comportement attendu dans Teams. D’autres toiles de l’environnement de réunion défilent verticalement.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Flux de travail

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple montrant un scénario complexe dans un onglet en réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Faire : Scénarios complexes de surface dans l’onglet en réunion

Si votre application comprend plusieurs tâches, nous vous recommandons fortement d’utiliser un onglet en réunion avec une mise en page à colonne unique.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple montrant des scénarios complexes dans un dialogue en réunion." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>Ne pas : Rendre les dialogues en réunion complexes

Les dialogues en réunion sont destinés à de brèves interactions.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montrant une extension de réunion avec le thème sombre." border="false":::

#### <a name="do-use-teams-color-tokens"></a>Faire: Utilisez Teams de couleur

Teams réunions sont optimisées pour le mode sombre afin de réduire le bruit visuel et cognitif afin que les utilisateurs puissent se concentrer sur la discussion et le contenu partagé. En savoir plus sur <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">l’utilisation de jetons de couleur (interface utilisateur couramment)</a>.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montrant une extension de réunion avec un thème par défaut (lumière)." border="false":::

#### <a name="dont-hard-code-hex-values"></a>Ne pas: Valeurs hex code dur

Si vous n’utilisez pas Teams jetons de couleur, vos créations seront moins évolutives et prennent plus de temps à gérer.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple montrant une extension de réunion avec un bouton arrière." border="false":::

#### <a name="do-have-a-back-button"></a>Faire: Avoir un bouton arrière

Si vous avez plus d’une couche de navigation dans un onglet en réunion, les utilisateurs doivent être en mesure de revenir à leurs vues précédentes.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple montrant une extension de réunion avec deux boutons de rejet." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>Ne pas: Inclure un autre bouton de rejet

Fournir une option pour fermer le contenu de l’onglet en réunion peut causer des problèmes car il ya déjà un bouton dans l’en-tête pour rejeter l’onglet en réunion lui-même.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montrant des modalités (ou modules de tâches) dans un onglet en réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Attention : Évitez les modalités dans l’onglet en réunion

Les modules modaux (également connus sous le nom de modules de tâches) dans l’onglet en réunion déjà étroit peuvent envelopper et obscurcir le contenu.

   :::column-end:::
:::row-end:::
