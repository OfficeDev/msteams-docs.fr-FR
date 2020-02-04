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
# <a name="start-talking-with-bots"></a><span data-ttu-id="8ad9d-104">Commencer à parler avec les robots</span><span class="sxs-lookup"><span data-stu-id="8ad9d-104">Start talking with bots</span></span>

<span data-ttu-id="8ad9d-105">Les robots sont des applications de conversation qui effectuent un ensemble de tâches restreint ou spécifique.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-105">Bots are conversational apps that perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="8ad9d-106">Elles vous permettent de communiquer avec les utilisateurs, de répondre à leurs questions et de les informer de manière proactive des modifications.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-106">They give you an opportunity to communicate with users, respond to their questions, and proactively notify them about changes.</span></span> <span data-ttu-id="8ad9d-107">Ils constituent un excellent moyen de communiquer.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-107">They’re a great way to reach out.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="8ad9d-108">Conseils</span><span class="sxs-lookup"><span data-stu-id="8ad9d-108">Guidelines</span></span>

### <a name="avatars"></a><span data-ttu-id="8ad9d-109">Avatars</span><span class="sxs-lookup"><span data-stu-id="8ad9d-109">Avatars</span></span>

<span data-ttu-id="8ad9d-110">Les avatars de robots dans teams sont des hexagones, de sorte que les utilisateurs peuvent rapidement dire qu’ils parlent à un robot au lieu d’une personne.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-110">Bot avatars in Teams are shaped like hexagons so people can quickly tell that they’re talking to a bot instead of a person.</span></span> <span data-ttu-id="8ad9d-111">Vous allez soumettre votre avatar sous la forme d’un carré et nous le détourons.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-111">You’ll submit your avatar as a square and we’ll crop it for you.</span></span> <span data-ttu-id="8ad9d-112">En ce qui concerne les avatars, nous vous recommandons de faire en sorte que les vôtres soient lisibles de 2 mètres et avec un contraste plus élevé.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-112">When it comes to avatars, we recommend making yours legible from 2 feet away and using a higher contrast.</span></span>

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a><span data-ttu-id="8ad9d-113">Boutons</span><span class="sxs-lookup"><span data-stu-id="8ad9d-113">Buttons</span></span>

<span data-ttu-id="8ad9d-114">Nous allons prendre en charge jusqu’à six boutons par carte.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-114">We support up to six buttons per card.</span></span> <span data-ttu-id="8ad9d-115">Soyez concis lorsque vous rédigez du texte de bouton et gardez à l’esprit que la plupart des boutons doivent uniquement traiter la tâche en cours.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-115">Be concise when writing button text, and keep in mind that most buttons should only address the task at hand.</span></span>

### <a name="graphics"></a><span data-ttu-id="8ad9d-116">Graphiques</span><span class="sxs-lookup"><span data-stu-id="8ad9d-116">Graphics</span></span>

<span data-ttu-id="8ad9d-117">Les graphiques sont un moyen efficace d’indiquer un récit, mais les conversations de robots ne nécessitent pas toutes des graphiques, c’est pourquoi vous pouvez les utiliser pour un impact maximal.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-117">Graphics are a good way to tell a story, but not all bot conversations require graphics, so use them for maximum impact.</span></span>

### <a name="responding-to-users-and-failing-gracefully"></a><span data-ttu-id="8ad9d-118">Réponse aux utilisateurs et échec normal</span><span class="sxs-lookup"><span data-stu-id="8ad9d-118">Responding to users and failing gracefully</span></span>

<span data-ttu-id="8ad9d-119">Votre robot doit également pouvoir répondre à des éléments tels que « Bonjour », « aide » et « merci » tout en prenant en compte les fautes d’orthographe et d’familières courantes.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-119">Your bot should also be able to respond to things like 'Hi', 'Help', and 'Thanks' while taking common misspellings and colloquialisms into account.</span></span> <span data-ttu-id="8ad9d-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8ad9d-120">For example:</span></span>

#### <a name="x2713-hello"></a><span data-ttu-id="8ad9d-121">&#x2713; Hello</span><span class="sxs-lookup"><span data-stu-id="8ad9d-121">&#x2713; Hello</span></span>

<span data-ttu-id="8ad9d-122">`Hi` `how are you` `howdy`</span><span class="sxs-lookup"><span data-stu-id="8ad9d-122">`Hi` `how are you` `howdy`</span></span>

#### <a name="x2713-help"></a><span data-ttu-id="8ad9d-123">Aide &#x2713;</span><span class="sxs-lookup"><span data-stu-id="8ad9d-123">&#x2713; Help</span></span>

<span data-ttu-id="8ad9d-124">`What do you do?` `How does this work?` `What the heck?`</span><span class="sxs-lookup"><span data-stu-id="8ad9d-124">`What do you do?` `How does this work?` `What the heck?`</span></span>

#### <a name="x2713-thanks"></a><span data-ttu-id="8ad9d-125">&#x2713; Merci</span><span class="sxs-lookup"><span data-stu-id="8ad9d-125">&#x2713; Thanks</span></span>

<span data-ttu-id="8ad9d-126">`Thank you` `thankyou` `thx`</span><span class="sxs-lookup"><span data-stu-id="8ad9d-126">`Thank you` `thankyou` `thx`</span></span>

<span data-ttu-id="8ad9d-127">Votre robot doit pouvoir gérer les types de requêtes et d’entrées suivants :</span><span class="sxs-lookup"><span data-stu-id="8ad9d-127">Your bot should be able to handle the following types of queries and inputs:</span></span>

* <span data-ttu-id="8ad9d-128">**Questions reconnues**: il s’agit des questions les plus fréquemment posées par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-128">**Recognized questions**: These are the “best case scenario” questions you’d anticipate from users.</span></span>
* <span data-ttu-id="8ad9d-129">**Non-questions reconnues**: les requêtes sur les fonctionnalités non prises en charge, des éléments d’information aléatoires ou quand une personne souhaite traiter votre robot.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-129">**Recognized non-questions**: Queries about unsupported functionality, random pieces of information, or when someone wants to curse at your bot.</span></span>
* <span data-ttu-id="8ad9d-130">**Questions non reconnues**: entrées inintelligibles (par exemple, comprises).</span><span class="sxs-lookup"><span data-stu-id="8ad9d-130">**Unrecognized questions**: Unintelligible inputs (i.e., gibberish).</span></span>

<span data-ttu-id="8ad9d-131">Exemples de personnalité et de types de réponse de robot :</span><span class="sxs-lookup"><span data-stu-id="8ad9d-131">Examples of bot personality and response types:</span></span>

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> <span data-ttu-id="8ad9d-132">Lors de l’écriture de votre script bot, posez-vous les questions suivantes : « mon entreprise sera-t-elle gênée si une réponse est capturée et partagée ? »</span><span class="sxs-lookup"><span data-stu-id="8ad9d-132">When writing your bot script, ask yourself: “Will my company be embarrassed if a response is screen captured and shared?”</span></span>

### <a name="understanding-what-users-are-trying-to-say"></a><span data-ttu-id="8ad9d-133">Comprendre ce que les utilisateurs essaient de dire</span><span class="sxs-lookup"><span data-stu-id="8ad9d-133">Understanding what users are trying to say</span></span>

#### <a name="use-a-thesaurus-for-synonyms"></a><span data-ttu-id="8ad9d-134">Utilisation d’un dictionnaire des synonymes pour les synonymes</span><span class="sxs-lookup"><span data-stu-id="8ad9d-134">Use a thesaurus for synonyms</span></span>

<span data-ttu-id="8ad9d-135">Lorsque vous utilisez des variantes de brainstorming, utilisez un dictionnaire des synonymes et obtenez des personnes sur autant d’arrière-plans que possible pour générer différentes interprétations de chaque requête.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-135">When brainstorming variants, use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of each query.</span></span>

#### <a name="make-use-of-telemetry-and-interviews"></a><span data-ttu-id="8ad9d-136">Utilisation de la télémétrie et des entretiens</span><span class="sxs-lookup"><span data-stu-id="8ad9d-136">Make use of telemetry and interviews</span></span>

<span data-ttu-id="8ad9d-137">Découvrez ce que sont les utilisateurs et quels sont leurs intentions lors de l’interrogation de votre robot.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-137">Find out what users are saying and what was their intent when querying your bot.</span></span> <span data-ttu-id="8ad9d-138">Il s’agit d’un processus continu lorsque vous recevez des utilisateurs dans différents emplacements et types de sociétés.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-138">This will be an ongoing process as you get users in different locations and types of companies.</span></span> <span data-ttu-id="8ad9d-139">Vous pouvez affiner la reconnaissance de la langue et le mappage des intentions avec la prise en main du service intelligent ([Luis](/azure/cognitive-services/luis/what-is-luis)).</span><span class="sxs-lookup"><span data-stu-id="8ad9d-139">You can fine-tune language recognition and intent mapping with Language Understanding Intelligent Service ([LUIS](/azure/cognitive-services/luis/what-is-luis)).</span></span>

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a><span data-ttu-id="8ad9d-140">À quelle fréquence devez-vous utiliser votre robot pour accéder à un utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="8ad9d-140">How often should you use your bot to reach out to a user?</span></span>

#### <a name="x2713-when-a-state-has-changed"></a><span data-ttu-id="8ad9d-141">&#x2713; quand un État a changé</span><span class="sxs-lookup"><span data-stu-id="8ad9d-141">&#x2713; When a state has changed</span></span>

<span data-ttu-id="8ad9d-142">Par exemple, si une affectation est marquée comme étant complète, lorsqu’un bogue change, lorsque le nouveau réseau social est disponible ou lorsqu’une interrogation a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-142">For example, if an assignment is marked as complete, when a bug changes, when new social media is available, or when a poll has been completed.</span></span>

#### <a name="x2713-when-the-timing-is-right"></a><span data-ttu-id="8ad9d-143">&#x2713; lorsque le minutage est correct</span><span class="sxs-lookup"><span data-stu-id="8ad9d-143">&#x2713; When the timing is right</span></span>

<span data-ttu-id="8ad9d-144">Votre robot peut agir comme un condensé quotidien, envoyant une notification à l’utilisateur ou au canal à une fréquence spécifique.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-144">Your bot can act like a daily digest, sending a notification to the user or channel at a specific frequency.</span></span>

<span data-ttu-id="8ad9d-145">Laissez l’utilisateur dans le contrôle.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-145">Leave the user in control.</span></span> <span data-ttu-id="8ad9d-146">Fournissez des paramètres de notification qui incluent la fréquence et la priorité.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-146">Provide notification settings that include frequency and priority.</span></span>

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a><span data-ttu-id="8ad9d-147">Utilisation des onglets</span><span class="sxs-lookup"><span data-stu-id="8ad9d-147">Using tabs</span></span>

<span data-ttu-id="8ad9d-148">Les onglets rendent votre bot plus fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-148">Tabs make your bot much more functional.</span></span> <span data-ttu-id="8ad9d-149">Avec les onglets, vous pouvez créer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8ad9d-149">With tabs, you can create the following:</span></span>

### <a name="x2713-a-place-to-host-standing-queries"></a><span data-ttu-id="8ad9d-150">&#x2713; un emplacement pour héberger les requêtes permanentes</span><span class="sxs-lookup"><span data-stu-id="8ad9d-150">&#x2713; A place to host standing queries</span></span>

<span data-ttu-id="8ad9d-151">Dans les conversations personnelles entre un bot et une seule personne, les onglets peuvent contenir des informations et des listes propres à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-151">In personal conversations between a bot and a single person, tabs can house user-specific information and lists.</span></span> <span data-ttu-id="8ad9d-152">Ils sont également un excellent emplacement pour gérer les réponses des robots aux questions fréquemment posées (FAQ), de sorte que les utilisateurs n’ont pas besoin de se demander.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-152">They’re also a good place to maintain bot responses to frequently-asked questions (FAQs) — so users don’t need to keep asking.</span></span>

### <a name="x2713-a-place-to-finish-a-conversation"></a><span data-ttu-id="8ad9d-153">&#x2713; un emplacement pour terminer une conversation</span><span class="sxs-lookup"><span data-stu-id="8ad9d-153">&#x2713; A place to finish a conversation</span></span>

<span data-ttu-id="8ad9d-154">Vous pouvez créer un lien vers un onglet à partir d’une carte.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-154">You can link to a tab from a card.</span></span> <span data-ttu-id="8ad9d-155">Si votre bot fournit une réponse qui nécessite quelques étapes supplémentaires, il peut créer un lien vers un onglet pour effectuer la tâche ou le flux.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-155">If your bot provides an answer that requires a few more steps, it can link to a tab to complete the task or flow.</span></span>

### <a name="x2713-a-place-to-provide-some-help"></a><span data-ttu-id="8ad9d-156">&#x2713; un emplacement pour fournir de l’aide</span><span class="sxs-lookup"><span data-stu-id="8ad9d-156">&#x2713; A place to provide some help</span></span>

<span data-ttu-id="8ad9d-157">Ajoutez un onglet qui informe les utilisateurs sur la façon de communiquer avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-157">Add a tab that educates users about how to communicate with your bot.</span></span> <span data-ttu-id="8ad9d-158">Vous pouvez fournir un contexte pour ce qu’il fait ou des questions fréquemment posées.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-158">You can provide some context for what it does or FAQs.</span></span>

![Fourniture d’aide](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> <span data-ttu-id="8ad9d-160">L’incorporation de parties de votre site dans un onglet permet à quelqu’un de gérer le contexte d’une conversation quand il utilise votre service.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-160">Embedding parts of your site in a tab will help someone maintain the context of a conversation as they use your service.</span></span> <span data-ttu-id="8ad9d-161">Il supprime la nécessité de lancer votre service dans un navigateur et de basculer entre les applications.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-161">It removes the need to launch your service in a browser and switch back and forth between apps.</span></span>

---

## <a name="best-practices"></a><span data-ttu-id="8ad9d-162">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="8ad9d-162">Best practices</span></span>

### <a name="x2713-bots-arent-assistants"></a><span data-ttu-id="8ad9d-163">Les robots &#x2713; ne sont pas des assistants</span><span class="sxs-lookup"><span data-stu-id="8ad9d-163">&#x2713; Bots aren’t assistants</span></span>

<span data-ttu-id="8ad9d-164">Contrairement aux agents, par exemple, Cortana, les robots agissent en tant que spécialistes.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-164">Unlike agents, e.g., Cortana, bots act as specialists.</span></span>

### <a name="x2713-discourage-chitchat"></a><span data-ttu-id="8ad9d-165">&#x2713; dissuader ChitChat</span><span class="sxs-lookup"><span data-stu-id="8ad9d-165">&#x2713; Discourage chitchat</span></span>

<span data-ttu-id="8ad9d-166">À moins que votre robot ne soit conçu pour la conversation, Découvrez comment rediriger ChitChat vers l’achèvement de la tâche.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-166">Unless your bot is built for conversation, find ways to redirect chitchat toward task completion.</span></span>

### <a name="x2713-introduce-some-personality"></a><span data-ttu-id="8ad9d-167">&#x2713; introduire une personnalité</span><span class="sxs-lookup"><span data-stu-id="8ad9d-167">&#x2713; Introduce some personality</span></span>

<span data-ttu-id="8ad9d-168">Conservez votre personnalité de robot en fonction de la voix de votre produit.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-168">Keep your bot personality consistent with the voice of your product.</span></span> <span data-ttu-id="8ad9d-169">Imaginez votre robot comme parlant pour votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-169">Think of your bot as speaking for your company.</span></span>

### <a name="x2713-maintain-tone"></a><span data-ttu-id="8ad9d-170">&#x2713; conserver la tonalité</span><span class="sxs-lookup"><span data-stu-id="8ad9d-170">&#x2713; Maintain tone</span></span>

<span data-ttu-id="8ad9d-171">Déterminez si vous voulez que votre ton soit convivial et clair, « uniquement les faits » ou Super excentrique.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-171">Determine whether you want your tone to be friendly and light, “just the facts”, or super quirky.</span></span>

### <a name="x2713-encourage-easy-task-flow"></a><span data-ttu-id="8ad9d-172">&#x2713; encourager le flux de tâches facile</span><span class="sxs-lookup"><span data-stu-id="8ad9d-172">&#x2713; Encourage easy task flow</span></span>

<span data-ttu-id="8ad9d-173">Prendre en charge les interactions à rotation multiple tout en continuant à répondre aux questions entièrement formulées.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-173">Support multi-turn interactions while still allowing for fully formed questions.</span></span> <span data-ttu-id="8ad9d-174">L’anticipation de l’étape suivante permettra aux utilisateurs d’utiliser beaucoup plus facilement les flux de tâches.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-174">Anticipating the next step will help users get through task flows much easier.</span></span>

<span data-ttu-id="8ad9d-175">Si un utilisateur effectue plusieurs étapes pour effectuer une tâche, autorisez-le à le faire tout au long de chaque étape, mais terminez-le en lui permettant de suggérer un chemin plus rapide.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-175">If a user takes several steps to complete a task, allow your bot to take them through each step, but finish by having it suggest a quicker path.</span></span> <span data-ttu-id="8ad9d-176">Par exemple, si un utilisateur a pris plusieurs tentatives de conversation pour définir une réunion (en commençant par spécifier une réunion, puis en spécifiant l’heure, puis en indiquant le jour), terminez la conversation avec la suggestion suivante : prochaine fois, essayez de vous demander si vous possibilité de planifier une réunion avec Bob à 1:00 demain.</span><span class="sxs-lookup"><span data-stu-id="8ad9d-176">For example, if a user has taken several conversational turns to set a meeting (by first specifying a meeting, then identifying with whom, then stating the time, then stating the day), finish the conversation with the following suggestion: Next time, try asking if you can ‘schedule a meeting with Bob at 1:00 tomorrow’.</span></span>