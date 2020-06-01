---
title: Instructions de conception pour les robots
description: Décrit les instructions pour la création de robots
keywords: Guide de conception des équipes
ms.openlocfilehash: 731e36ac3437e22435ea6054ad359d0c6bc2ead3
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44453888"
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

### <a name="onboarding-users"></a>Utilisateurs d’intégration

Il est essentiel que les robots s’introduisent et envoient ce qu’ils peuvent faire aux utilisateurs. Cette *valeur* permet aux utilisateurs de comprendre ce qu’ils doivent faire avec le bot, où les limitations peuvent être, et, plus important encore, permet aux utilisateurs de tolérer l’interaction avec un ordinateur qui n’est pas aussi intuitif qu’une personne réelle. En outre, il accorde une autorisation pour les données utilisateur dans Exchange pour la valeur réelle fournie par le service.

#### <a name="welcome-messages"></a>Les messages de bienvenue

Les messages de bienvenue sont le meilleur moyen de définir le ton de votre robot et doivent être utilisés dans les scénarios personnels et d’équipe ou de groupe. Le message indique ce que fait le bot, ainsi que des méthodes courantes pour interagir avec lui. Utiliser des exemples de fonctionnalité spécifiques comme, «*essayez de demander....*» dans une liste à puces. Dans la mesure du possible, ces suggestions doivent renvoyer des réponses stockées. Il est essentiel que les exemples de fonctionnalités fonctionnent sans que les utilisateurs aient besoin de se connecter.

#### <a name="tours"></a>Voyages

Inclure un attribut de *visite guidée* avec des messages de bienvenue et des réponses à l’entrée utilisateur équivalente à «*aide*». Il s’agit de la méthode la plus efficace pour permettre aux utilisateurs de découvrir ce qu’un robot peut faire. Les carrousels dans les expériences un-à-un constituent un excellent moyen d’indiquer cette histoire et d' *essayer de créer* des boutons informatiques renvoyant à des exemples de réponses possibles. Les visites guidées sont également des emplacements très intéressants pour parler des autres fonctionnalités d’une application. Par exemple, vous pouvez inclure des captures d’écran des onglets extensions de messagerie et Teams.  Les utilisateurs ne doivent pas se connecter pour accéder à et utiliser une visite guidée.

Lorsque des visites guidées sont utilisées dans des scénarios d’équipe ou de groupe, elles doivent s’ouvrir dans un module de tâches afin de ne pas ajouter plus de bruit de carte aux conversations en cours entre les utilisateurs.

### <a name="responding-to-users-and-failing-gracefully"></a>Réponse aux utilisateurs et échec normal

Votre robot doit également pouvoir répondre à des éléments tels que «*Bonjour*», «*aide*» et «*Merci*», tout en prenant en compte les fautes d’orthographe courantes et familières. Par exemple :

#### <a name="x2713-hello"></a>&#x2713; Hello

`"Hi"`  `"How are you"`  `"Howdy"`

#### <a name="x2713-help"></a>Aide &#x2713;

`"What do you do?"`  `"How does this work?"`  `"What the heck?"`

#### <a name="x2713-thanks"></a>&#x2713; Merci

`"Thank you"`  `"Thankyou"`  `"Thx"`

Votre robot doit pouvoir gérer les types de requêtes et d’entrées suivants :

> [!div class="checklist"]
>
> * **Questions reconnues**. Il s’agit des questions de scénario les plus optimistes pour les utilisateurs.
> * **Non-questions reconnues**. Les requêtes relatives aux fonctionnalités non prises en charge et/ou aux entrées à inconvenances, non liées ou aléatoires.
> * **Questions non reconnues**: entrées ou entrées inintelligibles, sans signification ou sans sens.

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

Vous pouvez créer un lien vers un onglet à partir d’une carte. Si votre bot fournit une réponse qui nécessite quelques étapes supplémentaires, il peut créer un lien vers un onglet pour effectuer la tâche ou le flux. Par exemple, en réponse à la question suivante : « How do I Formating My iPhone ? », une réponse appropriée peut être une carte qui décrit les premières étapes et dispose d’un bouton permettant d' *afficher plus* , qui amène ensuite l’utilisateur à l’onglet d' *aide* du robot et des liens détaillés vers les instructions spécifiques.

### <a name="x2713-a-place-to-host-a-settings-page"></a>&#x2713; un emplacement d’hébergement d’une page de paramètres

Les robots doivent disposer d’un contrôle utilisateur. Pour de nombreux robots, il est autorisé par le biais d’une interface de conversation ; Toutefois, il est difficile de se souvenir de ces paramètres. Un onglet Paramètres permet d’afficher les paramètres des utilisateurs, d’autoriser les utilisateurs à les modifier tous en même temps, et peut également être un bon point de départ pour les comportements de robot personnalisés plus complexes.

### <a name="x2713-a-place-to-provide-some-help"></a>&#x2713; un emplacement pour fournir de l’aide

Ajoutez un onglet qui informe les utilisateurs sur la façon de communiquer avec votre robot. Vous pouvez fournir un contexte pour ce qu’il fait ou des questions fréquemment posées.

![Fourniture d’aide](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> L’incorporation de parties de votre site dans un onglet permettra aux utilisateurs de maintenir le contexte d’une conversation quand ils utilisent votre service. Il supprime la nécessité de lancer votre service dans un navigateur et de basculer entre les applications.

---

## <a name="bots-in-channels"></a>Bots dans les canaux

L’appel d’un bot dans un canal peut être effectué par `@mention` . La boîte de dialogue bot doit être unique dans les canaux et les groupes, ainsi que dans les scénarios un-à-un et il est généralement judicieux de prendre en compte les différentes approches. Cela est particulièrement vrai dans les cas suivants :

### <a name="sensitive-data-sent-by-a-bot"></a>Données sensibles envoyées par un bot

Tandis que les utilisateurs d’une équipe peuvent être connus du service, les rôles d’utilisateur réels ne le peuvent pas. Cela signifie que, par exemple, dans un scénario d’éducation impliquant intimidation, les informations de contact parent et étudiant ne sont pas partagées dans un paramètre d’équipe. Au lieu de cela, le message du robot peut être « deux incidents de intimidation s’est produit aujourd’hui », ainsi qu’un bouton pour afficher les détails.

Lancement des détails dans une page Web, ou un module de tâches peut demander des informations d’identification de l’utilisateur ou effectuer une requête sur un index pour les rôles d’utilisateur associés aux comptes AAD. Dans ces deux options, les données se trouvent dans une étendue d’affichage privée et aucune fuite de données ne se produira. Si les mêmes données sont envoyées dans une conversation un-à-un entre un utilisateur et le bot, les données ne sont visibles que par l’utilisateur dans ce contexte et, par conséquent, sûres dans le message de robot. Le fait de prendre les utilisateurs d’un canal à une conversation un-à-un doit être évité Toutefois, car la navigation forcée est très perturbante.

### <a name="sending-cards-as-a-response-to-interactions"></a>Envoi de cartes en guise de réponse aux interactions

Lors de l’envoi d’une carte de carrousel en réponse à une *visite guidée* dans une conversation un-à-un est parfaitement acceptable, le même modèle peut produire des dizaines ou des centaines de *carrousels de tour* dans un canal actif avec un grand nombre d’utilisateurs. Pour éviter ce, les cartes secondaires doivent être hébergées dans un module de tâches. Ce modèle permet aux utilisateurs de consigner le canal, de nettoyer le canal en trop de réponses de robot et peut éventuellement prendre en compte différents rôles d’utilisateur lors de l’affichage de la *visite guidée* .

## <a name="useful-tips"></a>Conseils utiles

### <a name="x2713-remember-bots-arent-assistants"></a>&#x2713; n’oubliez pas que les robots ne sont pas des assistants

Contrairement aux agents, par exemple, Cortana, les robots agissent en tant que spécialistes.

### <a name="x2713-discourage-chitchat"></a>&#x2713; dissuader ChitChat

À moins que votre robot ne soit conçu pour la conversation, Découvrez comment rediriger ChitChat vers l’achèvement de la tâche.

### <a name="x2713-introduce-some-personality"></a>&#x2713; introduire une personnalité

Conservez votre personnalité de robot en fonction de la voix de votre produit. Imaginez votre robot comme parlant pour votre entreprise.

### <a name="x2713-maintain-tone"></a>&#x2713; conserver la tonalité

Déterminez si vous voulez que votre ton soit convivial et clair, « uniquement les faits » ou Super excentrique.

### <a name="x2713-encourage-easy-task-flow"></a>&#x2713; encourager le flux de tâches facile

Prendre en charge les interactions à rotation multiple tout en continuant à répondre aux questions entièrement formulées. L’anticipation de l’étape suivante permettra aux utilisateurs d’utiliser beaucoup plus facilement les flux de tâches.

Si un utilisateur effectue plusieurs étapes pour effectuer une tâche, autorisez-le à le faire tout au long de chaque étape, mais terminez-le en lui permettant de suggérer un chemin plus rapide. Par exemple, si un utilisateur a pris plusieurs tentatives de conversation pour définir une réunion (en spécifiant d’abord une réunion, puis en spécifiant l’heure, puis en indiquant le jour), terminez la conversation avec la suggestion suivante : la prochaine fois, essayez de confirmer si vous pouvez planifier une réunion avec Bob à 1:00 demain.
