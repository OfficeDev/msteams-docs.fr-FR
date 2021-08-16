---
title: Conception de votre bot
description: Découvrez comment concevoir un bot Teams et obtenir le Kit d’interface utilisateur de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: ea0392868b06653657beff60b157070eaef7f4ba
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345647"
---
# <a name="designing-your-microsoft-teams-bot"></a>Conception de votre bot Microsoft Teams

Les bots sont des applications de conversation qui effectuent un ensemble spécifique de tâches. Basés sur <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, les bots communiquent avec les utilisateurs, répondent à leurs questions et informent les utilisateurs de façon proactive en cas de modifications et d’autres événements. C’est un excellent moyen de les joindre.

> [!IMPORTANT]
> Actuellement, les bots sont disponibles dans Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), mais pas dans les GCC-High et le département de la Défense (DOD).

Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des bots dans Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions plus détaillées sur la conception du bot, y compris les éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d’interface utilisateur de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a>Ajouter un bot

Les bots sont disponibles dans les conversations, les canaux et les applications personnelles.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

Les utilisateurs peuvent ajouter un bot de l’une des manières suivantes :

* À partir de Teams Store.
* Utilisez le menu volant de l’application en sélectionnant l’icône **Plus** sur le côté gauche de Teams.
* Avec un @mention dans la nouvelle conversation ou zone de rédaction (l’exemple suivant montre comment faire dans une conversation de groupe).

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="L’exemple montre comment ajouter un bot dans une conversation de groupe à l’aide de @mention." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

Les utilisateurs peuvent accéder aux bots qui ont été ajoutés sur le bureau à l'@mention.

:::image type="content" source="../../assets/images/bots/mobile-access-bot-chat-at-mention.png" alt-text="L’exemple montre comment accéder à un bot mobile dans une conversation de groupe à l’aide d’une @mention." border="false":::

---

## <a name="introduce-a-bot"></a>Présentation d’un bot

Il est essentiel que votre bot se présente et décrive ce qu'il peut faire. Cet échange initial permet aux utilisateurs de comprendre ce qu’il faut faire avec le bot, de connaître ses limites et, surtout, de se mettre à l’interaction avec.

### <a name="welcome-message-in-a-one-on-one-chat"></a>Message de bienvenue dans une conversation à deux

En contexte personnel, les messages d’accueil définissent le ton de votre bot. Le message inclut un message d’accueil, ce que le bot peut faire et quelques suggestions pour l’interaction. Par exemple, « Essayez de me demander ... ». Si possible, ces suggestions doivent renvoyer les réponses stockées sans avoir à se connecter.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="L'exemple montre l'introduction d'un bot dans une application personnelle." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-personal-welcome.png" alt-text="Exemple d’introduction d’un bot dans une application personnelle sur un appareil mobile." border="false":::

---

### <a name="welcome-message-in-channels-and-group-chats"></a>Message de bienvenue dans les canaux et les conversations de groupe

L’introduction de votre bot doit être légèrement différente dans les canaux et les conversations de groupe par rapport à un espace personnel (comme une application personnelle). Dans la vie réelle, si vous entrez dans une salle pleine de gens, vous vous présenterez au lieu de souhaiter la bienvenue à tous ceux qui sont déjà là. Portez cette réflexion dans votre conception bot.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="L'exemple montre l'introduction d'un bot dans un contexte de collaboration." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-group-welcome.png" alt-text="Exemple d’introduction d’un bot dans un contexte de collaboration sur mobile." border="false":::

---

### <a name="bot-authentication-with-single-sign-on"></a>Authentification bot avec authentification unique

Lorsqu'une personne envoie un message à un bot, il peut être nécessaire de se connecter pour utiliser toutes ses fonctionnalités. Vous pouvez simplifier le processus d'authentification à l'aide de l'authentification unique (SSO).

N’oubliez pas : dans le menu de commandes du bot (**Que puis-je faire ?**), vous devez également fournir une commande pour vous sortir.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="L'exemple montre un bot avec un bouton de connexion." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-sso-example.png" alt-text="L’exemple montre un bot avec un bouton de sign-in sur mobile." border="false":::

---

### <a name="tours"></a>Visites guidées

Vous pouvez inclure une visite guidée avec des messages d’accueil et si le bot répond à une commande telle qu’une « aide ». Une visite guidée est le moyen le plus efficace de décrire ce que peut faire votre bot. Le cas échéant, ils sont également parfaits pour décrire les autres fonctionnalités de votre application. Par exemple, incluez des captures d’écran de votre extension de messagerie.

> [!IMPORTANT]
> Les visites guidées doivent être accessibles sans avoir à se connecter.

#### <a name="one-on-one-chats"></a>Conversations à deux

Dans une application personnelle, un carrousel peut fournir une vue d’ensemble efficace de votre bot et de toutes les autres fonctionnalités de votre application. Il est vivement encouragé d’inclure des boutons pour que les utilisateurs essaient les commandes de bot. Par exemple, **créez une tâche.**

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="L'exemple montre une visite guidée d'un bot dans une conversation à deux." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-personal.png" alt-text="Exemple d’une visite guidée de bot dans une conversation un-à-un sur mobile." border="false":::

---

#### <a name="channels-and-group-chats"></a>Canaux et conversations de groupe

Dans les canaux et conversations de groupe, une visite guidée doit s’ouvrir dans un modal (également appelé [module de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) de sorte qu’elle n’interrompe pas les conversations en cours. Cela vous permet également d’implémenter des affichages basés sur les rôles pour votre visite guidée.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="L'exemple montre une visite guidée d'un bot dans un canal." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-channel.png" alt-text="Exemple de visite guidée d’un bot dans un canal mobile." border="false":::

---

## <a name="chat-with-a-bot"></a>Discuter avec un robot

Les bots s’intègrent directement dans l’infrastructure de messagerie de l’équipe. Les utilisateurs peuvent discuter avec un bot pour trouver une réponse à leurs questions ou taper des commandes pour que le bot effectue un ensemble de tâches étroit ou spécifique. Les bots peuvent informer les utilisateurs des modifications ou mises à jour apportées à votre application par conversation instantanée.

### <a name="chat-with-a-bot-in-different-contexts"></a>Discuter avec un bot dans différents contextes

Vous pouvez utiliser des bots dans les contextes suivants :

* **Applications personnelles** : dans une application personnelle, un bot possède un onglet de conversation dédié.
* **Conversation à deux** : un utilisateur peut démarrer une conversation privée avec un bot. C’est la même expérience que l’utilisation d’un bot dans une application personnelle.
* **Conversation de groupe** : les utilisateurs peuvent interagir avec un bot dans une conversation de groupe en @mentionnant le bot.
* **Canal** : les utilisateurs peuvent interagir avec un bot dans un canal. en @mentionnant nom du bot dans la zone de rédaction. N’oubliez pas que, dans ce contexte, le bot est disponible pour l’ensemble de l’équipe, pas seulement pour le canal.

### <a name="anatomy"></a>Anatomie

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="L’exemple montre la forme structurelle d’un bot." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom et icône de l’application**|
|2|**Onglet Conversation** : ouvre l’espace pour discuter avec votre bot (applicable uniquement aux applications personnelles).|
|3 |**Onglets Personnalisé** : ouvre le contenu lié à votre application.|
|4 |**Onglet À propos** : affiche des informations de base sur votre application.|
|5 |**Bulle de conversation** : les conversations bot utilisent le cadre de stratégie de messagerie Teams.|
|6 |**Carte adaptative**: si les réponses de votre bot incluent des cartes adaptatives, la carte prend toute la largeur de la bulle de conversation.|
|7 |**Menu de commandes** : affiche les commandes standard de votre bot (définies par vous).|

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’un bot mobile." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom et icône de l’application**|
|2|**Onglet Conversation** : ouvre l’espace pour discuter avec votre bot (applicable uniquement aux applications personnelles).|
|3 |**Onglets Personnalisé** : ouvre le contenu lié à votre application.|
|4 |**Bulle de conversation** : les conversations bot utilisent le cadre de stratégie de messagerie Teams.|
|5 |**Carte adaptative**: si les réponses de votre bot incluent des cartes adaptatives, la carte prend toute la largeur de la bulle de conversation.|

---

### <a name="command-menu"></a>Menu de commandes

Le menu de commandes fournit la liste des mots ou phrases à qui votre robot doit toujours répondre. Le menu de commande s'affiche au-dessus de la zone de rédaction lorsqu'une personne converse avec un bot. Lorsqu’une commande est sélectionnée, elle est insérée dans un message.

La liste des commandes doit être brève. Le menu est destiné à mettre en évidence les principales fonctionnalités de votre bot. Gardez également les commandes concises. Par exemple, vous pouvez créer une commande appelée **Aide** au lieu d’une commande **Pouvez-vous m’aider** ?
Le menu de commandes doit toujours être disponible quel que soit l’état de la conversation.

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="L'exemple montre le menu de commandes d'un bot." border="false":::

## <a name="understand-what-people-are-saying"></a>Comprendre ce que les gens disent

Utilisez un dictionnaire des synonymes et demandez à des personnes issues d'horizons aussi différents que possible de vous aider à générer différentes interprétations de requêtes standard.

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Illustration montrant comment un bot peut interpréter « Bonjour »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Illustration montrant comment un bot peut interpréter « Aide »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Illustration montrant comment un bot peut interpréter « Merci »." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a>Extraire l’intention et les données des messages

Concevez votre bot pour reconnaître l'intention, c'est-à-dire ce que quelqu'un attend d'un bot en réponse à un message ou une requête. L'intention classe un message ou une requête comme une action unique avec un ou plusieurs objets de données affectés par l'action. 

Les exemples suivants décrivent l’intention et les données de l’utilisateur dans les messages envoyés aux bots :

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Exemple montrant que dans la phrase « Réserver un vol pour Seattle », l’intention de l’utilisateur est « réserver un vol » et les données sont « Seattle »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Exemple montrant que dans la phrase « Quand le magasin est-il ouvert » l’intention de l’utilisateur est « quand » et les données sont « ouvert »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Exemple montrant que dans la phrase « Planifier une réunion à 13h avec Bob dans Distribution », l’intention de l’utilisateur est « planifier une réunion » et les données sont « 13h » et « Bob dans Distribution »." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a>Analyser et améliorer

Découvrez les dires des utilisateurs en discutant avec votre bot. Il s’agit d’un processus itératif continu à mesure que votre base d’utilisateurs s’agrandit à différents emplacements et organisation. Vous pouvez affiner la reconnaissance linguistique et le mappage d’intention de votre bot avec Microsoft Language Understanding (LUIS).

* [Comprendre LUIS](/azure/cognitive-services/luis/artificial-intelligence) : découvrez comment LUIS utilise l’intelligence artificielle pour fournir une compréhension du langage naturel (NLU) aux données de votre application.
* [Intégration à LUIS](https://www.luis.ai/) : ajoutez des fonctionnalités de langage naturel à votre bot sans le processus complexe de création de modèles d’apprentissage automatique.

## <a name="use-cases"></a>Cas d’utilisation

### <a name="simple-queries"></a>Requêtes simples

Les bots peuvent fournir une correspondance exacte à une requête ou à un groupe de correspondances associées pour vous aider à mettre fin à l’ambiguïté. Pour les correspondances associées, groupez le contenu à l’aide d’une carte de liste.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="L'exemple montre une interaction de requête simple avec un bot." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-simple-query.png" alt-text="L’exemple illustre une interaction de requête simple avec un bot sur un appareil mobile." border="false":::

---

### <a name="multi-turn-interactions"></a>Interactions à plusieurs tour

Si votre bot peut prendre en charge les demandes complètes et les questions, il doit également être en mesure de gérer les interactions à plusieurs tour. L'anticipation des étapes suivantes possibles permet aux personnes d'effectuer un flux de tâches plus facilement (plutôt que d'attendre d'elles qu'elles rédigent une demande complète).

Dans les exemples suivants, le bot répond à chaque message avec des options pour ce que vous souhaitez faire ensuite.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="L'exemple montre une interaction à plusieurs tours avec un bot." border="false":::


# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-multi-turn.png" alt-text="L’exemple illustre une interaction à plusieurs tour avec un bot sur mobile." border="false":::


---

### <a name="reach-out-to-users"></a>Contacter les utilisateurs

Grâce à une messagerie proactive, votre robot peut agir comme un résumé qui envoie des notifications pertinentes à une personne, une conversation de groupe ou un canal à une fréquence spécifique. Un bot peut envoyer un message lorsqu’un élément a changé dans un document ou qu’un élément de travail est fermé.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

Dans l’exemple suivant, l’utilisateur reçoit une notification toast qu’un bot les a envoyés dans un autre canal.

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="L’exemple montre le toast d’un bot qui a envoyer un message de façon proactive à un utilisateur d’un autre canal." border="false":::

Dans ce canal, l’utilisateur peut lire son message à partir du bot.

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="L'exemple montre l'utilisateur regardant le message proactif du bot." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

Dans l’exemple suivant, l’utilisateur reçoit une notification qu’un bot les a envoyés dans un autre canal.

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message-toast.png" alt-text="L’exemple montre un toast d’un bot qui messagerie de manière proactive un utilisateur à partir d’un autre canal sur mobile." border="false":::

Dans ce canal, l’utilisateur peut lire son message à partir du bot.

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message.png" alt-text="L’exemple montre l’utilisateur regardant le message proactif du bot sur un appareil mobile." border="false":::

---

### <a name="use-tabs-with-bots"></a>Utiliser des onglets avec des bots

Dans les applications personnelles, un onglet peut compléter ce que votre bot peut faire. Par exemple, si votre bot peut créer des éléments de travail, il peut être agréable d’afficher tous ces éléments dans un emplacement central au sein d’un onglet. En savoir plus sur la [création d’onglets](../../tabs/design/tabs.md).

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="L'exemple montre comment un onglet peut aider à organiser le contenu d'un bot." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-with-tab.png" alt-text="Un exemple montre comment un onglet peut aider à organiser le contenu du bot sur mobile." border="false":::

---

## <a name="manage-a-bot"></a>Gérer un bot

Les utilisateurs doivent pouvoir modifier les paramètres d’un bot. Vous pouvez fournir cette fonctionnalité avec des commandes bot, mais il est généralement plus efficace d’inclure tous les paramètres dans un [module de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (comme illustré dans l’exemple suivant).

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="L'exemple montre un module de tâches permettant de configurer les paramètres d'un bot." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="content"></a>Contenu

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Exemple montrant une meilleure pratique de bot pour établir un personnage clair." border="false":::

#### <a name="do-establish-a-clear-persona"></a>À faire : établir un personnage clair

Le ton de votre bot est-il amical et léger, « juste les faits », ou plus excentrique ? Comment doit-il répondre dans différents scénarios ? La planification et la documentation du personnage de votre bot facilitent l’écriture des réponses qui semblent naturelles et cohérentes.

En savoir plus sur l’écriture pour les bots dans <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">kit d’interface utilisateur de Microsoft Teams (Figma).</a>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Exemple montrant comment transmettre clairement ce que votre bot peut faire." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a>À faire : communiquer clairement ce que votre bot peut faire

Les messages de bienvenue et les visites guidées aident les personnes à comprendre ce qu’elles peuvent faire avec votre bot.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Exemple montrant qu’il ne faut pas masquer les fonctionnalités de votre bot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a>À ne pas faire : masquer les fonctionnalités de votre bot

Les premières impressions sont importantes. Les personnes seront probablement confuses ou méfiantes lorsqu'elles verront un message de connexion indéfini.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="L’exemple montrant votre bot doit reconnaître les questions non posées." border="false":::

#### <a name="do-recognize-non-questions"></a>À faire : reconnaître les questions non posées

Votre bot doit pouvoir répondre à des messages tels que « Bonjour », « Aide » et « Merci », tout en tenant compte des fautes d'orthographe et des expressions familières courantes.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Exemple montrant que vous devez éviter les réponses inttér es aux messages de bot simples." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a>À ne pas faire : manquer les opportunités de satisfaction

Certaines personnes s'attendent à ce que les conversations se déroulent naturellement, comme avec une personne réelle. Essayez d'éviter les réponses maladroites à des messages simples.

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a>Résolution des problèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="L’exemple de bots doit aider les utilisateurs à comprendre comment les utiliser." border="false":::

#### <a name="do-provide-help"></a>À faire : fournir de l’aide

Si votre bot ne peut pas répondre à une demande, fournissez à l’utilisateur les moyens de s’informer sur l’interaction avec votre bot.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Exemple montrant que votre bot ne doit pas être un groupe d’utilisateurs." border="false":::

#### <a name="dont-leave-users-stranded"></a>À ne pas faire : laisser les utilisateurs bloqués

Les personnes vont rapidement abandonner votre robot s’ils ne peuvent pas résoudre les problèmes.

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a>Interactions complexes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Exemple montrant que vous pouvez utiliser des modules de tâche ou des onglets avec votre bot pour des interactions complexes." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a>A faire : utiliser des modules ou des onglets de tâches

Si votre bot fournit une réponse qui nécessite quelques étapes supplémentaires, vous pouvez lier un module de tâches ou un onglet pour terminer la tâche ou le flux.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Exemple montrant comment votre bot doit éviter les interactions à plusieurs tour." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a>À ne pas faire : rendre les interactions à plusieurs tour fastidieuses

Une conversation approfondie pour accomplir une seule tâche est lente et trop complexe. Le développeur doit également prendre en compte les modifications apportées aux états (par exemple, le délai d’annulation de la conversation ou l’envoi d’un message « Annuler »).

   :::column-end:::
:::row-end:::

### <a name="privacy"></a>Confidentialité

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Exemple montrant comment les bots doivent uniquement afficher des informations privées dans un contexte personnel." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a>À faire : afficher uniquement les informations sensibles dans un contexte personnel

Si votre bot se trouve dans une conversation ou un canal de groupe, nous vous recommandons de diriger les utilisateurs vers un emplacement privé (tel qu’un module de tâches, un onglet ou un navigateur) pour afficher les informations sensibles.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Exemple montrant comment les bots ne doivent pas révéler d’informations sensibles à un groupe ou à des personnes." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a>À ne pas faire : certains contenus ne sont pas destinés à être vus par tout le monde

Votre bot ne doit pas révéler d’informations sensibles à un groupe de personnes.

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>Voir aussi

Ces autres instructions peuvent vous aider dans la conception de votre bot :

* [Conception de votre application personnelle](../../concepts/design/personal-apps.md)
* [Conception de cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md)
* [Conception de modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
