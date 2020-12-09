---
title: Conception de votre robot
description: Découvrez comment concevoir un bot de teams et obtenir le kit d’interface utilisateur Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605426"
---
# <a name="designing-your-microsoft-teams-bot"></a>Conception de votre robot Microsoft teams

Les robots sont des applications de conversation qui effectuent un ensemble spécifique de tâches. En fonction de <a href="https://dev.botframework.com/" target="_blank">Microsoft bot Framework</a>, les robots communiquent avec les utilisateurs, répondent à leurs questions et les signalent de manière proactive sur les modifications et les autres événements. Ils constituent un excellent moyen de communiquer.

Pour vous aider à concevoir votre application, les informations suivantes décrivent et illustrent la façon dont les utilisateurs peuvent ajouter, utiliser et gérer les robots dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur Microsoft teams

Vous trouverez des instructions de conception de robot plus complètes, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a>Ajouter un bot

Les robots sont disponibles dans les conversations, les canaux et les applications personnelles. Vous pouvez ajouter un bot de l’une des manières suivantes :

* À partir du magasin de Teams (AppSource).
* À l’aide du lanceur d’application en sélectionnant l’icône **plus** sur le côté gauche de teams.
* Avec une @mention dans la boîte de dialogue nouvelle conversation ou composition (l’exemple suivant montre comment effectuer cette opération dans une conversation de groupe).

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="Exemple montre comment ajouter un bot dans une conversation de groupe à l’aide d’une @mention." border="false":::

## <a name="introduce-a-bot"></a>Introduire un robot

Il est essentiel que votre bot s’introduit lui-même et décrit ce qu’il peut faire. Cet échange initial permet aux utilisateurs de comprendre ce qu’ils doivent faire avec le bot, de connaître les limites et, plus important encore, d’interagir avec eux.

### <a name="welcome-message-in-a-one-on-one-chat"></a>Message de bienvenue dans une conversation en un seul

Dans les contextes personnels, les messages d’accueil définissent le ton de votre robot. Le message inclut un message d’accueil, ce que le robot peut faire et quelques suggestions concernant la façon d’interagir (par exemple, « essayez de me demander... »). Dans la mesure du possible, ces suggestions doivent renvoyer des réponses stockées sans avoir à se connecter.

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="Exemple de présentation d’un bot dans une application personnelle." border="false":::

### <a name="introductions-in-group-chats-and-channels"></a>Introductions dans les conversations et les canaux de groupe

L’introduction de votre robot doit être légèrement différente dans les conversations et les canaux de groupe par rapport à un contexte personnel (par exemple, une application personnelle). En réalité, si vous avez entré une salle pleine de personnes ; vous vous présenterez vous-même au lieu de accueillir les personnes qui s’y trouvent déjà. Conpensez-vous à la conception de votre robot.

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="Exemple de présentation d’un bot dans un contexte collaboratif." border="false":::

### <a name="bot-authentication-with-single-sign-on"></a>Authentification de robot avec authentification unique

Lorsqu’une personne message un bot, vous pouvez être amené à utiliser toutes ses fonctionnalités. Vous pouvez simplifier le processus d’authentification à l’aide de l’authentification unique (SSO).

N’oubliez pas : dans le menu de commandes du bot (**que puis-je faire ?**), vous devez également fournir une commande pour vous déconnecter.

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="Exemple montre un bot avec un bouton de connexion." border="false":::

### <a name="tours"></a>Voyages

Vous pouvez inclure une visite guidée avec des messages de bienvenue et si le robot répond à une commande semblable à celle d’aide. Une visite guidée est la manière la plus efficace de décrire ce que votre robot peut faire. Le cas échéant, elles sont également idéales pour décrire les autres fonctionnalités de votre application (par exemple, inclure des captures d’écran de votre extension de messagerie).

> [!IMPORTANT]
> Les visites guidées doivent être accessibles sans avoir à se connecter.

#### <a name="one-on-one-chats"></a>Conversations en un seul

Dans une application personnelle, un carrousel peut fournir une vue d’ensemble efficace de votre bot et de toutes les autres fonctionnalités de votre application. Y compris les boutons les commandes autoriser les utilisateurs à essayer le robot sont encouragées (par exemple, **créer une tâche**).

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="Exemple illustre une visite guidée dans une conversation en un seul." border="false":::

#### <a name="channels-and-group-chats"></a>Canaux et conversations de groupe

Dans les canaux et les conversations de groupe, une visite guidée doit s’ouvrir dans un module modal (également appelé « [module de tâche](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) » pour ne pas interrompre les conversations en cours. Cela vous donne également la possibilité d’implémenter des vues basées sur les rôles pour votre visite guidée.

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="Exemple illustre une visite guidée dans un canal." border="false":::

## <a name="chat-with-a-bot"></a>Conversation avec un bot

Les robots s’intègrent directement à l’infrastructure de messagerie de l’équipe. Les utilisateurs peuvent discuter avec un bot pour obtenir des réponses à leurs questions ou taper des commandes pour que le robot effectue un ensemble de tâches restreint ou spécifique. Les robots peuvent avertir de manière proactive les utilisateurs concernant les modifications ou les mises à jour de votre application via une conversation.

### <a name="chat-with-a-bot-in-different-contexts"></a>Conversation avec un bot dans différents contextes

Vous pouvez utiliser les robots dans les contextes suivants :

* **Applications personnelles**: dans une application personnelle, un bot a un onglet de conversation dédié.
* **Conversation en un seul**: un utilisateur peut lancer une conversation privée avec un bot. Il s’agit de la même expérience que l’utilisation d’un bot dans une application personnelle.
* **Group chat**: les personnes peuvent interagir avec un bot dans une conversation de groupe en @mentioning le bot.
* **Canal**: les personnes peuvent interagir avec un bot dans un canal. en @mentioning le nom du bot dans la zone de composition. N’oubliez pas que dans ce contexte, le bot est disponible pour l’ensemble de l’équipe, pas seulement pour le canal.

### <a name="anatomy"></a>Anatomie

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’un bot." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom et icône de l’application**|
|2 |**Onglet conversation**: ouvre l’espace pour parler avec votre bot (applicable uniquement aux applications personnelles).|
|3 |**Onglets personnalisés**: ouvre un autre contenu lié à votre application.|
|4 |**À propos** de l’onglet : affiche des informations de base sur votre application.|
|5 |**Bulle de conversation**: les conversations de robots utilisent l’infrastructure de messagerie Teams.|
|6 |**Carte adaptative**: si les réponses de votre robot incluent des cartes adaptatives, la carte occupe toute la largeur de la bulle de conversation.|
|7 |**Menu de commandes**: affiche les commandes standard de votre robot (que vous avez définie).

### <a name="command-menu"></a>Menu de commandes

Le menu de commandes fournit une liste de mots ou d’expressions auxquelles votre bot doit toujours répondre. Le menu de commandes s’affiche au-dessus de la zone de composition lorsqu’une personne est contourne d’un bot. Lorsqu’une commande est sélectionnée, elle est insérée dans un message.

La liste des commandes doit être brève. Le menu est destiné uniquement à mettre en évidence les principales fonctionnalités de votre robot. Conservez les commandes de manière concise. Par exemple, créez une commande appelée **aide** au lieu de **pouvez-vous m’aider**?
Le menu de commandes doit toujours être disponible indépendamment de l’état de la conversation.

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="Exemple de menu de commandes d’un bot." border="false":::

## <a name="understand-what-people-are-saying"></a>Comprendre ce que les utilisateurs disent

Utilisez un dictionnaire des synonymes et obtenez des personnes d’autres arrière-plans, autant que possible, pour vous aider à générer différentes interprétations des requêtes standard.

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Illustration illustrant la façon dont un bot peut interpréter’Hello'." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Illustration illustrant la façon dont un bot peut interpréter’help'." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Illustration illustrant la façon dont un bot peut interpréter’thanks'." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a>Extraire les intentions et les données des messages

Concevez votre robot pour qu’il reconnaisse l’intention, ce qui capture la réponse d’un bot à un message ou à une requête. L’intention classe un message ou une requête en tant qu’action unique avec un ou plusieurs objets de données qui sont affectés par l’action. 

Les exemples suivants décrivent l’intention de l’utilisateur et les données contenues dans les messages envoyés aux robots.

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Exemple illustrant dans la phrase « réserver un vol à Seattle », l’intention de l’utilisateur est « réserver un vol » et les données sont « Paris »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Exemple d’affichage dans la phrase « quand le magasin est ouvert », l’intention de l’utilisateur est « quand » et les données sont « ouvertes »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Exemple illustrant la phrase « planifier une réunion à 13h00 avec Bob en distribution », l’intention de l’utilisateur est « planifier une réunion » et les données « 13h00 » et « Bob en distribution »." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a>Analyser et améliorer

Découvrez ce que les utilisateurs disent lorsque vous discutez avec votre robot. Il s’agit d’un processus continu et itératif à mesure que votre base d’utilisateurs se développe à différents emplacements et développées. Vous pouvez régler le mappage de reconnaissance et d’intention de langue de votre robot avec Microsoft Language mémorandum (LUIS).

* [Comprendre Luis](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Découvrez comment Luis utilise ai pour fournir une compréhension de langage naturel (NLU) à vos données d’application.
* [Intégration avec Luis](https://www.luis.ai/): ajoutez des fonctionnalités de langage naturel à votre bot sans le processus complexe de création de modèles d’apprentissage automatique.

## <a name="use-cases"></a>Cas d'utilisation

### <a name="simple-queries"></a>Requêtes simples

Les robots peuvent fournir une correspondance exacte à une requête ou à un groupe de correspondances associées pour faciliter la désambiguïsation. Pour les correspondances associées, groupez le contenu à l’aide d’une carte de liste.

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="Exemple illustre une interaction de requête simple avec un bot." border="false":::

### <a name="multi-turn-interactions"></a>Interactions multi-tournage

Bien que votre robot puisse prendre en charge des demandes et des questions complètes, il doit également être en mesure de gérer les interactions à tour de rôle. En anticipant les étapes suivantes possibles, il est plus facile pour les utilisateurs d’effectuer un flux de tâches complet (au lieu de s’attendre à créer une requête complète).

Dans l’exemple suivant, le bot répond à chaque message avec des options pour ce qui peut être le plus utile.

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="Exemple illustre une interaction à tournage multiple avec un bot." border="false":::

### <a name="reach-out-to-users"></a>Contacter des utilisateurs

Avec la messagerie proactive, votre robot peut agir comme un Digest qui envoie des notifications pertinentes à un individu, une conversation de groupe ou un canal à une fréquence spécifique. Un bot peut envoyer un message lorsqu’un élément a été modifié dans un document ou qu’un élément de travail est fermé.

Dans l’exemple suivant, un utilisateur obtient une notification de Toast qu’un bot a messageé dans un autre canal.

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="L’exemple montre un toast d’un bot à la messagerie proactive d’un utilisateur à partir d’un autre canal." border="false":::

Dans ce canal, l’utilisateur peut lire son message à partir du bot.

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="Exemple montre comment l’utilisateur examine le message proactif du bot." border="false":::

### <a name="use-tabs-with-bots"></a>Utiliser des onglets avec des robots

Un onglet peut faciliter l’utilisation de votre robot. Par exemple, si votre bot peut créer des éléments de travail, il serait intéressant d’afficher tous ces éléments dans un emplacement central à l’intérieur d’un onglet. En savoir plus sur la [conception des onglets](../../tabs/design/tabs.md).

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="Cet exemple montre comment un onglet peut vous aider à organiser le contenu de la robots." border="false":::

## <a name="manage-a-bot"></a>Gérer un bot

Les utilisateurs doivent être en mesure de modifier les paramètres d’un bot. Vous pouvez fournir cette fonctionnalité avec les commandes bot, mais il est généralement plus efficace d’inclure tous les paramètres dans un [module de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (comme illustré dans l’exemple suivant).

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="Exemple de module de tâche permettant de configurer les paramètres d’un bot." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

### <a name="content"></a>Contenu

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-establish-a-clear-persona"></a>Do : établir un personnage clair

Est-ce que le ton est convivial et clair, « juste les faits » ou Super-excentrique ? Comment doit-il répondre dans différents scénarios ? La planification et la documentation du personnage de votre robot facilitent l’écriture de réponses apparemment naturelles et cohésives.

Pour en savoir plus sur la rédaction de robots, consultez le <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Kit d’interface utilisateur Microsoft Teams (Figma).</a>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a>Do : transmettez clairement ce que votre robot peut faire

Les messages de bienvenue et les visites aident les utilisateurs à comprendre ce qu’ils peuvent faire avec votre robot.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a>Ne pas : obscurcir les fonctionnalités de votre robot

Premières impressions. Il se peut que des personnes soient confondues ou suspectes lors de la présentation d’un message de connexion nondescript.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-recognize-non-questions"></a>Do : reconnaître les non-questions

Votre robot doit pouvoir répondre aux messages tels que « HI », « aide » et « Merci », tout en tenant compte également des fautes d’orthographe courantes et familières.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a>Ne manquez pas les occasions de vous faire plaisir

Certaines personnes attendent que les conversations se déplacent naturellement comme elles le ferait avec une personne réelle. Essayez d’éviter des réponses encombrantes aux messages simples.

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a>Résolution des problèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-provide-help"></a>Do : fournir de l’aide

Si votre bot ne peut pas répondre à une demande, demandez à un utilisateur de se former de l’interaction avec votre robot.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-leave-users-stranded"></a>Ne pas : laisser les utilisateurs bloqués

Les utilisateurs abandonneront rapidement votre robot s’ils ne peuvent pas résoudre les problèmes.

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a>Interactions complexes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a>Do : utiliser des onglets ou des modules de tâches

Si votre bot fournit une réponse qui nécessite quelques étapes supplémentaires, vous pouvez créer un lien vers un onglet ou un module de tâches pour effectuer la tâche ou le flux.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a>N’effectuez pas les interactions fastidieux

Une conversation complète pour effectuer une tâche unique est lente et excessivement complexe. Le développeur doit également tenir compte des modifications d’État (par exemple, le délai d’expiration de conversation ou l’envoi d’un message d’annulation).

   :::column-end:::
:::row-end:::

### <a name="privacy"></a>Confidentialité

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a>Do : afficher uniquement les informations sensibles dans un contexte personnel

Si votre bot se trouve dans un canal ou une conversation de groupe, nous vous recommandons de diriger les utilisateurs vers un emplacement privé (par exemple, un module de tâches, un onglet ou un navigateur) pour afficher les informations sensibles.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a>Ne pas : certains contenus ne sont pas destinés à être vus par tout le monde

Votre bot ne doit pas révéler d’informations sensibles à un groupe de personnes.

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a>En savoir plus

Ces autres instructions peuvent vous aider dans votre conception de robot :

* [Conception de votre application personnelle](../../concepts/design/personal-apps.md)
* [Conception de cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md)
* [Création de modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a>Valider votre conception

Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.

> [!div class="nextstepaction"]
> [Vérifier les instructions de validation de la conception](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
