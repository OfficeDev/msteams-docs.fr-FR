---
title: Concevoir une boîte de dialogue en réunion
author: heath-hamilton
description: Découvrez comment concevoir efficacement une boîte de dialogue de réunion pour Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: f2ac0df3ce28293d9e3f61f45dd2d460dc01f2e9
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452672"
---
# <a name="design-an-in-meeting-dialog"></a>Concevoir une boîte de dialogue en réunion

Les boîtes de dialogue de réunion sont affichées à l’étape de réunion Teams. Elles requièrent l’attention, la confirmation ou l’interaction d’un utilisateur, mais elles sont subtiles et n’interrompent pas la réunion.

## <a name="use-cases"></a>Cas d’utilisation

Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (par exemple, l’organisateur de la réunion) qui peut souhaiter que les participants :

* Fournir des commentaires succincts
* Suivre une brève enquête ou sondage
* Soumettre des approbations
* Obtenir les rappels

## <a name="example"></a>Exemple

L’exemple suivant montre à quoi la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion. Comme vous pouvez le voir, le contenu et la tâche sont légers.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion.":::

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir le scénario complet (Figma)</a>

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir d’autres exemples d’utilisation (Figma)</a>

## <a name="anatomy"></a>Anatomie

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

1. **Icône de l’application**
1. **Nom de l'application**
1. **Chaîne d’action**
1. **Ignorer l’icône :** Ferme une seule boîte de dialogue. Toujours utiliser l’icône fermer en haut à droite au lieu d’une action dans le pied de page.
1. **WebView**: affiche tous les boutons et le contenu d’application tiers (les boutons standard teams sont recommandés).

### <a name="sizing"></a>Taille

Les boîtes de dialogue de réunion peuvent varier en fonction de la taille pour tenir compte de différents cas d’utilisation, mais vous devez toujours conserver les tailles de remplissage et de composant.

* **Height**: la hauteur de la boîte de dialogue est déterminée par le contenu dans le WebView. Le défilement vertical est pris en charge pour le contenu qui dépasse la hauteur maximale que vous spécifiez.
* **Width**: la largeur de WebView est une valeur absolue comprise dans la plage que vous spécifiez.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

## <a name="behavior"></a>Comportement

Voir comportement général de la boîte de dialogue de réunion, tel que REST, chargement, etc., dans <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.

### <a name="position"></a>Position

Les boîtes de dialogue de réunion sont alignées au centre de l’étape de réunion. Elles ne peuvent pas être déplacées et ne fonctionnent pas dans l’infrastructure des notifications au niveau du système de teams.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

### <a name="aggregation"></a>Aggregat

Une seule boîte de dialogue s’affiche à la fois, en empileant le classement du dernier au plus récent en bas. Une fois qu’une boîte de dialogue est résolue ou fermée, le suivant prend sa place.

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir un exemple (Figma)</a>

### <a name="scrolling"></a>Défilement

Le défilement se produit dans la partie WebView d’une boîte de dialogue de réunion. Souvenez-vous des éléments suivants à propos du défilement :

* Vous devez uniquement pouvoir faire défiler verticalement.
* Vous ne pouvez voir que le contenu auquel vous avez fait défiler (rien au-dessus ou en dessous).

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

### <a name="buttons"></a>Boutons

Les boutons de boîte de dialogue de réunion font partie du WebView ([voir quelques exemples](#best-practices)).

Contrairement aux composants similaires, les boîtes de dialogue de réunion sont rejetées lorsqu’un utilisateur sélectionne un bouton.

## <a name="components"></a>Composants

Les boîtes de dialogue de réunion sont créées principalement avec les <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">composants d’interface utilisateur suivants (Figma)</a>, qui sont basés sur le <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">système de conception Fluent</a>.

Composant | Conseils | Exemple
 - | - | -
Bouton | Les boutons principal et secondaire peuvent être de taille moyenne ou petite | Envoyer une réponse
Input | Champ pour une saisie utilisateur partielle. Le texte de l’étiquette peut inclure une icône  | Entrer des commentaires
Liste déroulante | Sélectionnez une ou plusieurs options dans une liste. Peut inclure des fonctionnalités de recherche et de sélection multiple | Choisir une langue
Contrôles de sélection | Utilisez des cases à cocher pour plusieurs choix ou cases d’option et pour basculer pour les choix uniques. Pour des sélections plus détaillées, utilisez un curseur | Vote dans un sondage
Alertes | Qu’il s’agisse d’un message urgent, d’un état d’erreur ou d’un avertissement, le message doit être court et n’interrompra pas la tâche actuelle de l’utilisateur. | Afficher un problème lors de l’envoi d’une réponse

## <a name="theming"></a>Thèmes

### <a name="colors"></a>Couleurs

Utilisez le <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">jeu de couleurs recommandé (Figma)</a> pour les arrière-plans, les avant-plans et les États de transport.

### <a name="typography"></a>Typographie

Utilisez les <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">tailles et épaisseurs de police recommandées (Figma)</a> pour les titres, le corps de texte et le texte de métadonnées.

## <a name="best-practices"></a>Meilleures pratiques

Tandis que les boîtes de dialogue de réunion peuvent faire des appels plus efficaces, ils peuvent également dérailiser les appels s’ils sont trop discrets. En règle générale, utilisez les boîtes de dialogue avec parcimonie et suivez ces meilleures pratiques.

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="do-keep-it-contained"></a>Do : conservez-le

Limitez le contenu de la boîte de dialogue de réunion à un seul écran pour permettre aux utilisateurs de se concentrer sur la réunion.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="dont-include-multiple-steps"></a>Ne pas inclure plusieurs étapes

Les boîtes de dialogue de réunion ne doivent pas obliger les utilisateurs à naviguer dans le contenu.

   :::column-end:::
:::row-end:::

### <a name="interactions"></a>Leurs

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-do.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-dont.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-do.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="do-limit-number-of-interactions"></a>Do : limiter le nombre d’interactions

Supprimer le contenu inutile qui ne permet pas aux utilisateurs d’effectuer une tâche rapidement. Si vous avez besoin d’interactions complexes, nous vous recommandons vivement d’afficher votre contenu à l’aide d’une seule colonne sous l’onglet dans la réunion.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>Ne pas faire : introduire des éléments inutiles

Il se peut que vous puissiez concevoir une seule boîte de dialogue de réunion avec plusieurs interactions, mais trop nombreuses peuvent gêner la réunion.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Disposition

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="do-use-single-column-layouts"></a>Do : utiliser des mises en page à une seule colonne

Étant donné que les boîtes de dialogue sont au centre de l’étape de la réunion, l’exécution de la tâche doit être rapide et simple pour éviter toute frustration des utilisateurs.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="dont-clutter-the-space"></a>Ne pas : emcombrer l’espace

Le contenu dense ou très structuré peut être gênant et écrasant, en particulier lors d’une réunion.

   :::column-end:::
:::row-end:::

### <a name="size"></a>Size

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="do-keep-it-consistent"></a>Do : conservez la cohérence

Ceci est important, car les boîtes de dialogue de réunion s’affichent toujours au même endroit.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="dont-always-fit-to-the-content"></a>Ne pas : toujours tenir dans le contenu

Il est possible que vous essayiez d’éviter le défilement horizontal, mais que plusieurs tailles de boîte de dialogue de réunion dans la même application constituent une expérience incohérente.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Contrôles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do : aligner à droite l’action principale

Nous vous recommandons de placer l’action la plus intense à l’emplacement le plus à droite.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>Ne pas : Left ou Center align actions

Cela diffère du modèle standard teams pour le positionnement du contrôle dans une boîte de dialogue et peut entrer en conflit avec une boîte de dialogue située en arrière-plan.

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a>Accessibilité

Pour plus d’informations sur l’accessibilité, voir <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.

## <a name="resources"></a>Ressources

* <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Fichiers Figma des extensions de réunion Microsoft teams</a>

## <a name="validate-your-design"></a>Valider votre conception

Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.

> [!div class="nextstepaction"]
> [Vérifier les instructions de validation de la conception](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
