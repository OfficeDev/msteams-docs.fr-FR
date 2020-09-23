---
title: Conception de cartes efficaces
description: Décrit les instructions de conception pour la création de cartes
keywords: instructions de conception teams fiches d’infrastructure de référence (cartes simplifiées)
ms.openlocfilehash: 4ec410820e0288d99dacb6944a8096f4f61b9d34
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209836"
---
# <a name="design-effective-cards"></a><span data-ttu-id="7d881-104">Conception de cartes efficaces</span><span class="sxs-lookup"><span data-stu-id="7d881-104">Design effective cards</span></span>

<span data-ttu-id="7d881-105">Les cartes sont des extraits de code actionnables, que vous pouvez ajouter à une conversation via un bot, un connecteur ou une application.</span><span class="sxs-lookup"><span data-stu-id="7d881-105">Cards are actionable snippets of content that you can add to a conversation through a bot, a connector, or app.</span></span> <span data-ttu-id="7d881-106">En utilisant du texte, des graphiques et des boutons, les cartes vous permettent de communiquer avec une audience.</span><span class="sxs-lookup"><span data-stu-id="7d881-106">Using text, graphics, and buttons, cards allow you to communicate with an audience.</span></span>

<span data-ttu-id="7d881-107">Notre infrastructure de cartes élimine le fardeau de concevoir une expérience utilisateur entièrement fonctionnelle.</span><span class="sxs-lookup"><span data-stu-id="7d881-107">Our card framework eliminates the burden of designing a fully functional UX.</span></span> <span data-ttu-id="7d881-108">Nous avons développé plusieurs types de cartes standard et chacun d’eux s’adapte à nos plateformes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="7d881-108">We developed several standard card types and each one fits within our supported platforms.</span></span> <span data-ttu-id="7d881-109">Cela signifie que la disposition est entièrement prise en charge, et vous n’avez pas besoin de développer des itérations de carte différentes sur les plateformes.</span><span class="sxs-lookup"><span data-stu-id="7d881-109">This means layout is completely taken care of, and you won’t need to develop different card iterations across platforms.</span></span> <span data-ttu-id="7d881-110">Au lieu de cela, vous pouvez vous concentrer sur la numérotation dans votre contenu.</span><span class="sxs-lookup"><span data-stu-id="7d881-110">Instead, you can focus on dialing in your content.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="7d881-111">Conseils</span><span class="sxs-lookup"><span data-stu-id="7d881-111">Guidelines</span></span>

<span data-ttu-id="7d881-112">Considérez une carte comme une réponse à une question d’utilisateur ou à un paramètre.</span><span class="sxs-lookup"><span data-stu-id="7d881-112">Think of a card as a response to a user question or a setting.</span></span> <span data-ttu-id="7d881-113">Une carte peut répondre à une question directe (par exemple, le nombre de bogues ouverts) ou à une condition (par exemple, « envoyer une liste de mes bogues ouverts à 9 am tous les jours »).</span><span class="sxs-lookup"><span data-stu-id="7d881-113">A card can respond to a direct question (like, “How many open bugs do I have?”) or to a condition (like, “Send a list of my open bugs at 9 am every day”).</span></span>

> [!TIP]
> <span data-ttu-id="7d881-114">En utilisant l’un de nos types de cartes standard, vous savez déjà que toutes vos réponses s’afficheront correctement sur chaque plateforme prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7d881-114">Using one of our standard card types means you’ll already know that all your responses will render nicely across each supported platform.</span></span>

<span data-ttu-id="7d881-115">Une carte peut inclure n’importe lequel des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7d881-115">A card could include any of the following elements:</span></span><br />

[!include[Card anatomy](~/includes/design/card-image-anatomy.html)]

1. <span data-ttu-id="7d881-116">**Texte**de l’enveloppe : idéal pour les messages de conversation.</span><span class="sxs-lookup"><span data-stu-id="7d881-116">**Envelope text**: Best used for chat messages.</span></span> <span data-ttu-id="7d881-117">Par exemple, si vous souhaitez qu’un bot indique : « Voici ce que j’ai trouvé ! »</span><span class="sxs-lookup"><span data-stu-id="7d881-117">For example, if you want a bot to say: “Here’s what I found!”</span></span> <span data-ttu-id="7d881-118">ou « heure de votre résumé d’informations 1:00 », ce message est mieux affiché dans le texte de l’enveloppe.</span><span class="sxs-lookup"><span data-stu-id="7d881-118">or “Time for your 1:00 news digest”, that message is best displayed in envelope text.</span></span>

   <span data-ttu-id="7d881-119">Le texte d’enveloppe est un excellent moyen d’injecter un peu de personnalité dans votre service, n’oubliez pas de le conserver relativement rapidement.</span><span class="sxs-lookup"><span data-stu-id="7d881-119">Envelope text is a great way to inject a little personality into your service—just remember to keep it relatively short.</span></span>

2. <span data-ttu-id="7d881-120">**Titre**: votre titre sera toujours le plus grand texte de votre carte.</span><span class="sxs-lookup"><span data-stu-id="7d881-120">**Title**: Your title will always be the largest text in your card.</span></span> <span data-ttu-id="7d881-121">Il sert également de « raccordement », donc essayez de conserver le titre Short, mémorable et facile à analyser.</span><span class="sxs-lookup"><span data-stu-id="7d881-121">It also serves as your “hook”, so try to keep the title short, memorable, and easy to scan.</span></span>

3. <span data-ttu-id="7d881-122">**Sous-titre**: idéal pour les attributions, les slogans ou comme directive secondaire.</span><span class="sxs-lookup"><span data-stu-id="7d881-122">**Subtitle**: Best used for attribution, taglines, or as a secondary directive.</span></span> <span data-ttu-id="7d881-123">Ce composant apparaît juste en dessous de votre titre.</span><span class="sxs-lookup"><span data-stu-id="7d881-123">This component appears just below your title.</span></span>

4. <span data-ttu-id="7d881-124">**Image**: les images s’ajustent à leur conteneur.</span><span class="sxs-lookup"><span data-stu-id="7d881-124">**Image**: Images scale to fit their container.</span></span> <span data-ttu-id="7d881-125">Les cartes héros ont une largeur maximale de 420px, les miniatures ont une largeur maximale de 100px et les affichages de liste uniquement pour des en mode Bureau.</span><span class="sxs-lookup"><span data-stu-id="7d881-125">Hero cards have a max width of 420px, thumbnails have a max width of 100px, and list views only allow for 32px in desktop mode.</span></span>

5. <span data-ttu-id="7d881-126">**Text**: idéal pour le texte brut dans le corps de votre carte.</span><span class="sxs-lookup"><span data-stu-id="7d881-126">**Text**: Best used for plain text in the body of your card.</span></span> <span data-ttu-id="7d881-127">Votre longueur maximale dépend du type de carte que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="7d881-127">Your max length depends on the card type you’ve selected.</span></span>

6. <span data-ttu-id="7d881-128">**Buttons**: idéal pour ouvrir des pages Web, des onglets ou du contenu de conversation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="7d881-128">**Buttons**: Best used to open web pages, tabs, or additional chat content.</span></span> <span data-ttu-id="7d881-129">Veillez à laisser le texte du bouton court et jusqu’au point.</span><span class="sxs-lookup"><span data-stu-id="7d881-129">Make sure to keep your button text short and to the point.</span></span>

   <span data-ttu-id="7d881-130">Vous pouvez inclure jusqu’à 6 boutons par carte, mais nous vous recommandons de suivre une philosophie « moins de plus » ici.</span><span class="sxs-lookup"><span data-stu-id="7d881-130">You can include up to 6 buttons per card, but we’d recommend following a ‘less is more’ philosophy here.</span></span>

7. <span data-ttu-id="7d881-131">**Appuyez sur région**: il s’agit de la région cliquable de votre carte.</span><span class="sxs-lookup"><span data-stu-id="7d881-131">**Tap region**: This is the clickable region of your card.</span></span> <span data-ttu-id="7d881-132">La plupart des utilisateurs veulent cliquer sur les images automatiquement, essayez de concevoir votre texte afin qu’ils sachent où ils doivent appuyer ou cliquer.</span><span class="sxs-lookup"><span data-stu-id="7d881-132">Most users will want to click on images automatically, so try and craft your text so they know where they should tap or click.</span></span>

> [!TIP]
> <span data-ttu-id="7d881-133">Il n’est pas nécessaire d’inclure chaque élément dans chaque carte que vous créez.</span><span class="sxs-lookup"><span data-stu-id="7d881-133">There’s no need to include every element in each card you create.</span></span> <span data-ttu-id="7d881-134">Laissez votre contenu dicter vos éléments.</span><span class="sxs-lookup"><span data-stu-id="7d881-134">Let your content dictate your elements.</span></span>

---

## <a name="types-of-cards"></a><span data-ttu-id="7d881-135">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="7d881-135">Types of cards</span></span>

### <a name="hero"></a><span data-ttu-id="7d881-136">Hero</span><span class="sxs-lookup"><span data-stu-id="7d881-136">Hero</span></span>

<span data-ttu-id="7d881-137">Notre plus grande carte.</span><span class="sxs-lookup"><span data-stu-id="7d881-137">Our largest card.</span></span> <span data-ttu-id="7d881-138">Idéal pour les articles, les descriptions longues ou les scénarios dans lesquels votre image indique la plus grande partie de l’histoire.</span><span class="sxs-lookup"><span data-stu-id="7d881-138">Best used for articles, long descriptions, or scenarios where your image is telling most of the story.</span></span>

[!include[Card anatomy](~/includes/design/card-image-hero.html)]

### <a name="thumbnail"></a><span data-ttu-id="7d881-139">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="7d881-139">Thumbnail</span></span>

<span data-ttu-id="7d881-140">Short et doux.</span><span class="sxs-lookup"><span data-stu-id="7d881-140">Short and sweet.</span></span> <span data-ttu-id="7d881-141">Ces cartes sont idéales pour des réponses courtes ou si vous souhaitez renvoyer plusieurs cartes en même temps afin que l’utilisateur puisse choisir parmi plusieurs options.</span><span class="sxs-lookup"><span data-stu-id="7d881-141">These cards are ideal for short answers, or if you want to return several cards at once so the user can choose from a bunch of options.</span></span> <span data-ttu-id="7d881-142">Nous pensons qu’il s’agit d’un excellent moyen de créer un lien profond vers un autre onglet ou un service Web.</span><span class="sxs-lookup"><span data-stu-id="7d881-142">We think these are a great way to deep link to another tab or a web service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-thumbnail.html)]

### <a name="sign-in"></a><span data-ttu-id="7d881-143">Connexion</span><span class="sxs-lookup"><span data-stu-id="7d881-143">Sign in</span></span>

<span data-ttu-id="7d881-144">Certains services exigent que les utilisateurs se connectent indépendamment de notre authentification.</span><span class="sxs-lookup"><span data-stu-id="7d881-144">Some services require users to sign in independently of our authentication.</span></span> <span data-ttu-id="7d881-145">Dans ce cas, vous devez présenter une carte de connexion avant que l’utilisateur ne puisse se connecter à votre service.</span><span class="sxs-lookup"><span data-stu-id="7d881-145">In that event, you would present a sign-in card before the user can connect to your service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-signin.html)]

> [!TIP]
> <span data-ttu-id="7d881-146">Limitez les occurrences d’une carte de connexion supplémentaire, car elles constituent une forte vitesse de ralentissement pour les nouveaux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7d881-146">Limit the occurrences of an additional sign-in card since they pose a significant speed bump for new users.</span></span>

---

## <a name="card-collections"></a><span data-ttu-id="7d881-147">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="7d881-147">Card collections</span></span>

<span data-ttu-id="7d881-148">Nous disposons également de types de cartes standard qui conviennent mieux lorsque vous souhaitez présenter plusieurs éléments de contenu en une seule fois ou en succession rapide.</span><span class="sxs-lookup"><span data-stu-id="7d881-148">We also have standard card types that are best used when you want to present several pieces of content at once or in quick succession.</span></span> <span data-ttu-id="7d881-149">À cet effet, nous disposons d’un carrousel, d’un résumé, d’une liste et de ce que nous appelons « fusion de bulles ».</span><span class="sxs-lookup"><span data-stu-id="7d881-149">For that purpose, we have a carousel, a digest, a list, and what we call a ‘bubble merge’.</span></span>

### <a name="carousel"></a><span data-ttu-id="7d881-150">Carrousel</span><span class="sxs-lookup"><span data-stu-id="7d881-150">Carousel</span></span>

<span data-ttu-id="7d881-151">Idéal pour les articles, les achats et la navigation à l’aide de cartes.</span><span class="sxs-lookup"><span data-stu-id="7d881-151">Best used for articles, shopping, and browsing through cards.</span></span>

[!include[Card anatomy](~/includes/design/card-image-carousel.html)]

> [!TIP]
> <span data-ttu-id="7d881-152">Le Carrousel sera la hauteur maximale de votre carte principale.</span><span class="sxs-lookup"><span data-stu-id="7d881-152">The carousel will be the max height of your largest card.</span></span> <span data-ttu-id="7d881-153">Nous vous recommandons d’utiliser le même type de carte et les mêmes champs de contenu dans.</span><span class="sxs-lookup"><span data-stu-id="7d881-153">We recommend using the same card type and content fields throughout.</span></span>

### <a name="digest"></a><span data-ttu-id="7d881-154">Digest</span><span class="sxs-lookup"><span data-stu-id="7d881-154">Digest</span></span>

<span data-ttu-id="7d881-155">Idéal pour les actualités, les résumés et chaque fois que vous souhaitez que l’utilisateur affiche plusieurs cartes à la fois.</span><span class="sxs-lookup"><span data-stu-id="7d881-155">Best used for news, digests, and whenever you want the user to view multiple cards at once.</span></span> <span data-ttu-id="7d881-156">Nous vous recommandons d’utiliser des cartes miniatures pour les résumés.</span><span class="sxs-lookup"><span data-stu-id="7d881-156">We recommend using thumbnail cards for digests.</span></span>

[!include[Card anatomy](~/includes/design/card-image-digest.html)]

### <a name="lists"></a><span data-ttu-id="7d881-157">Listes</span><span class="sxs-lookup"><span data-stu-id="7d881-157">Lists</span></span>

<span data-ttu-id="7d881-158">Les listes sont un excellent moyen de présenter un ensemble d’objets balayables dans un scénario de sélection.</span><span class="sxs-lookup"><span data-stu-id="7d881-158">Lists are a great way to present a scannable set of objects in a “pick one of these” scenario.</span></span> <span data-ttu-id="7d881-159">Les listes sont recommandées pour les éléments qui n’ont pas besoin d’une grande quantité d’explications.</span><span class="sxs-lookup"><span data-stu-id="7d881-159">Lists are best used for items that don’t need a lot of explanation.</span></span>

[!include[Card anatomy](~/includes/design/card-image-list.html)]

### <a name="bubble-merge"></a><span data-ttu-id="7d881-160">Fusion de bulles</span><span class="sxs-lookup"><span data-stu-id="7d881-160">Bubble merge</span></span>

<span data-ttu-id="7d881-161">Certains effets intéressants peuvent être atteints en envoyant rapidement un héros et plusieurs miniatures.</span><span class="sxs-lookup"><span data-stu-id="7d881-161">Some interesting effects can be achieved by sending one hero and several thumbnails in quick succession.</span></span> <span data-ttu-id="7d881-162">Nous vous recommandons d’utiliser cette approche lorsque vous souhaitez traiter un résultat principal, mais seulement quelques éléments connexes.</span><span class="sxs-lookup"><span data-stu-id="7d881-162">We recommend this approach when you want to serve a main result but include a few more related items.</span></span>

[!include[Card anatomy](~/includes/design/card-image-bubble-merge.html)]

---

## <a name="best-practices"></a><span data-ttu-id="7d881-163">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="7d881-163">Best practices</span></span>

### <a name="keep-the-noise-down"></a><span data-ttu-id="7d881-164">Maintenir le bruit inactif</span><span class="sxs-lookup"><span data-stu-id="7d881-164">Keep the noise down</span></span>

<span data-ttu-id="7d881-165">Il est facile d’envoyer plusieurs cartes dans une conversation, mais une fois que les cartes sortent de l’affichage, elles deviennent moins utiles.</span><span class="sxs-lookup"><span data-stu-id="7d881-165">It’s easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="7d881-166">Essayez de vous limiter aux notions fondamentales.</span><span class="sxs-lookup"><span data-stu-id="7d881-166">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="7d881-167">Cela est particulièrement vrai dans un canal où les utilisateurs ont moins de tolérance pour ce qu’ils perçoivent comme « bruit ».</span><span class="sxs-lookup"><span data-stu-id="7d881-167">This is especially true in a channel where users have less tolerance for what they perceive as “noise”.</span></span>

### <a name="test-on-mobile"></a><span data-ttu-id="7d881-168">Test sur mobile</span><span class="sxs-lookup"><span data-stu-id="7d881-168">Test on mobile</span></span>

<span data-ttu-id="7d881-169">Les environnements mobiles sont limités en espace et en bande passante, donc soyez vigilant lorsque vous incluez des images surdimensionnées et des ensembles de données volumineux dans des listes et des carrousels.</span><span class="sxs-lookup"><span data-stu-id="7d881-169">Mobile environments are space- and bandwidth-constrained, so be cautious about including oversized images and large data sets in lists and carousels.</span></span> <span data-ttu-id="7d881-170">En outre, les largeurs de titre et les longueurs de texte seront tronquées sur mobile, ce qui est une autre chose de garder un oeil.</span><span class="sxs-lookup"><span data-stu-id="7d881-170">Also, title widths and text lengths will truncate on mobile, so that’s another thing to keep an eye on.</span></span>

### <a name="check-your-graphics"></a><span data-ttu-id="7d881-171">Vérifier vos graphismes</span><span class="sxs-lookup"><span data-stu-id="7d881-171">Check your graphics</span></span>

<span data-ttu-id="7d881-172">Les graphiques sont redimensionnés, donc veillez à les afficher sur toutes les plateformes.</span><span class="sxs-lookup"><span data-stu-id="7d881-172">Graphics are going to scale, so be sure to preview them on all platforms.</span></span>

### <a name="avoid-including-text-in-a-graphic"></a><span data-ttu-id="7d881-173">Éviter d’inclure du texte dans un graphisme</span><span class="sxs-lookup"><span data-stu-id="7d881-173">Avoid including text in a graphic</span></span>

<span data-ttu-id="7d881-174">Tout ce qui doit être lu par un utilisateur doit être inclus dans un champ de texte.</span><span class="sxs-lookup"><span data-stu-id="7d881-174">Anything that needs to be read by a user should be included in a text field.</span></span> <span data-ttu-id="7d881-175">Une fois qu’une image est redimensionnée dynamiquement, le texte que vous ajoutez à un graphique peut devenir inintelligible.</span><span class="sxs-lookup"><span data-stu-id="7d881-175">Once an image is dynamically scaled, any text you add to a graphic may become unintelligible.</span></span>

### <a name="use-mentions-if-you-want-the-attention-of-specific-users"></a><span data-ttu-id="7d881-176">Utiliser des mentions pour attirer l’attention des utilisateurs spécifiques</span><span class="sxs-lookup"><span data-stu-id="7d881-176">Use mentions if you want the attention of specific users</span></span>

> [!NOTE]
> <span data-ttu-id="7d881-177">Mentionner la prise en charge des cartes est actuellement prise en charge en version préliminaire pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="7d881-177">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="7d881-178">Les mentions sont un excellent moyen d’avertir des utilisateurs spécifiques dans une conversation d’équipe ou de groupe.</span><span class="sxs-lookup"><span data-stu-id="7d881-178">Mentions are a great way to notify specific users in a Team or group chat.</span></span> <span data-ttu-id="7d881-179">Vous pouvez inclure une mention dans la carte dans des scénarios, comme une tâche qui est affectée à un utilisateur ou la fourniture d’un Félicitations à un coéquipier.</span><span class="sxs-lookup"><span data-stu-id="7d881-179">You can include a mention in card in scenarios like, a task thats assigned to a user or giving Kudos to a teammate.</span></span> <span data-ttu-id="7d881-180">Découvrez comment inclure des mentions dans les cartes dans la [page de mise en forme](~/task-modules-and-cards/cards/cards-format.md)de la carte.</span><span class="sxs-lookup"><span data-stu-id="7d881-180">Learn how to include mentions in cards in the [card formatting page](~/task-modules-and-cards/cards/cards-format.md).</span></span> 
