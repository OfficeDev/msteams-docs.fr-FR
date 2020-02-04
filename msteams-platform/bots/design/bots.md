---
title: Instructions de conception pour les robots
description: Décrit les instructions pour la création de robots
keywords: Guide de conception des équipes
ms.openlocfilehash: f59a1e9c280f27567692b4d10341db79d05c3464
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673954"
---
# <a name="start-talking-with-bots"></a>Commencer à parler avec les robots

Les robots sont des applications de conversation qui effectuent un ensemble de tâches restreint ou spécifique. Elles vous permettent de communiquer avec les utilisateurs, de répondre à leurs questions et de les informer de manière proactive des modifications. Ils constituent un excellent moyen de communiquer.

---

## <a name="guidelines"></a>Conseils

### <a name="avatars"></a>Avatars

Les avatars de robots dans teams sont des hexagones, de sorte que les utilisateurs peuvent rapidement dire qu’ils parlent à un robot au lieu d’une personne. Vous allez soumettre votre avatar sous la forme d’un carré et nous le détourons. En ce qui concerne les avatars, nous vous recommandons de faire en sorte que les vôtres soient lisibles de 2 mètres et avec un contraste plus élevé.

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a>Boutons

Nous allons prendre en charge jusqu’à six boutons par carte. Soyez concis lorsque vous rédigez du texte de bouton et gardez à l’esprit que la plupart des boutons doivent uniquement traiter la tâche en cours.

### <a name="graphics"></a>Graphiques

Les graphiques sont un moyen efficace d’indiquer un récit, mais les conversations de robots ne nécessitent pas toutes des graphiques, c’est pourquoi vous pouvez les utiliser pour un impact maximal.

### <a name="responding-to-users-and-failing-gracefully"></a>Réponse aux utilisateurs et échec normal

Votre robot doit également pouvoir répondre à des éléments tels que « Bonjour », « aide » et « merci » tout en prenant en compte les fautes d’orthographe et d’familières courantes. Par exemple :

#### <a name="x2713-hello"></a>&#x2713; Hello

`Hi` `how are you` `howdy`

#### <a name="x2713-help"></a>Aide &#x2713;

`What do you do?` `How does this work?` `What the heck?`

#### <a name="x2713-thanks"></a>&#x2713; Merci

`Thank you` `thankyou` `thx`

Votre robot doit pouvoir gérer les types de requêtes et d’entrées suivants :

* **Questions reconnues**: il s’agit des questions les plus fréquemment posées par les utilisateurs.
* **Non-questions reconnues**: les requêtes sur les fonctionnalités non prises en charge, des éléments d’information aléatoires ou quand une personne souhaite traiter votre robot.
* **Questions non reconnues**: entrées inintelligibles (par exemple, comprises).

Exemples de personnalité et de types de réponse de robot :

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> Lors de l’écriture de votre script bot, posez-vous les questions suivantes : « mon entreprise sera-t-elle gênée si une réponse est capturée et partagée ? »

### <a name="understanding-what-users-are-trying-to-say"></a>Comprendre ce que les utilisateurs essaient de dire

#### <a name="use-a-thesaurus-for-synonyms"></a>Utilisation d’un dictionnaire des synonymes pour les synonymes

Lorsque vous utilisez des variantes de brainstorming, utilisez un dictionnaire des synonymes et obtenez des personnes sur autant d’arrière-plans que possible pour générer différentes interprétations de chaque requête.

#### <a name="make-use-of-telemetry-and-interviews"></a>Utilisation de la télémétrie et des entretiens

Découvrez ce que sont les utilisateurs et quels sont leurs intentions lors de l’interrogation de votre robot. Il s’agit d’un processus continu lorsque vous recevez des utilisateurs dans différents emplacements et types de sociétés. Vous pouvez affiner la reconnaissance de la langue et le mappage des intentions avec la prise en main du service intelligent ([Luis](/azure/cognitive-services/luis/what-is-luis)).

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a>À quelle fréquence devez-vous utiliser votre robot pour accéder à un utilisateur ?

#### <a name="x2713-when-a-state-has-changed"></a>&#x2713; quand un État a changé

Par exemple, si une affectation est marquée comme étant complète, lorsqu’un bogue change, lorsque le nouveau réseau social est disponible ou lorsqu’une interrogation a été effectuée.

#### <a name="x2713-when-the-timing-is-right"></a>&#x2713; lorsque le minutage est correct

Votre robot peut agir comme un condensé quotidien, envoyant une notification à l’utilisateur ou au canal à une fréquence spécifique.

Laissez l’utilisateur dans le contrôle. Fournissez des paramètres de notification qui incluent la fréquence et la priorité.

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a>Utilisation des onglets

Les onglets rendent votre bot plus fonctionnel. Avec les onglets, vous pouvez créer les éléments suivants :

### <a name="x2713-a-place-to-host-standing-queries"></a>&#x2713; un emplacement pour héberger les requêtes permanentes

Dans les conversations personnelles entre un bot et une seule personne, les onglets peuvent contenir des informations et des listes propres à l’utilisateur. Ils sont également un excellent emplacement pour gérer les réponses des robots aux questions fréquemment posées (FAQ), de sorte que les utilisateurs n’ont pas besoin de se demander.

### <a name="x2713-a-place-to-finish-a-conversation"></a>&#x2713; un emplacement pour terminer une conversation

Vous pouvez créer un lien vers un onglet à partir d’une carte. Si votre bot fournit une réponse qui nécessite quelques étapes supplémentaires, il peut créer un lien vers un onglet pour effectuer la tâche ou le flux.

### <a name="x2713-a-place-to-provide-some-help"></a>&#x2713; un emplacement pour fournir de l’aide

Ajoutez un onglet qui informe les utilisateurs sur la façon de communiquer avec votre robot. Vous pouvez fournir un contexte pour ce qu’il fait ou des questions fréquemment posées.

![Fourniture d’aide](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> L’incorporation de parties de votre site dans un onglet permet à quelqu’un de gérer le contexte d’une conversation quand il utilise votre service. Il supprime la nécessité de lancer votre service dans un navigateur et de basculer entre les applications.

---

## <a name="best-practices"></a>Meilleures pratiques

### <a name="x2713-bots-arent-assistants"></a>Les robots &#x2713; ne sont pas des assistants

Contrairement aux agents, par exemple, Cortana, les robots agissent en tant que spécialistes.

### <a name="x2713-discourage-chitchat"></a>&#x2713; dissuader ChitChat

À moins que votre robot ne soit conçu pour la conversation, Découvrez comment rediriger ChitChat vers l’achèvement de la tâche.

### <a name="x2713-introduce-some-personality"></a>&#x2713; introduire une personnalité

Conservez votre personnalité de robot en fonction de la voix de votre produit. Imaginez votre robot comme parlant pour votre entreprise.

### <a name="x2713-maintain-tone"></a>&#x2713; conserver la tonalité

Déterminez si vous voulez que votre ton soit convivial et clair, « uniquement les faits » ou Super excentrique.

### <a name="x2713-encourage-easy-task-flow"></a>&#x2713; encourager le flux de tâches facile

Prendre en charge les interactions à rotation multiple tout en continuant à répondre aux questions entièrement formulées. L’anticipation de l’étape suivante permettra aux utilisateurs d’utiliser beaucoup plus facilement les flux de tâches.

Si un utilisateur effectue plusieurs étapes pour effectuer une tâche, autorisez-le à le faire tout au long de chaque étape, mais terminez-le en lui permettant de suggérer un chemin plus rapide. Par exemple, si un utilisateur a pris plusieurs tentatives de conversation pour définir une réunion (en commençant par spécifier une réunion, puis en spécifiant l’heure, puis en indiquant le jour), terminez la conversation avec la suggestion suivante : prochaine fois, essayez de vous demander si vous possibilité de planifier une réunion avec Bob à 1:00 demain.