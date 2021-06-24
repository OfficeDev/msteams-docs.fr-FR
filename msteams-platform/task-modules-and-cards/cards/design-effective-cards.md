---
title: Conception de Cartes adaptatives pour votre application
description: Découvrez comment concevoir des Cartes adaptatives pour Teams et obtenir le Kit d’interface utilisateur de Microsoft Teams.
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8e56928da44e22006feb59715c8bdbf821ec4c42
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037655"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="79414-103">Conception de Cartes adaptatives pour votre application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="79414-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="79414-104">Une carte adaptative contient un corps libre d’éléments de carte et un ensemble facultatif d’actions.</span><span class="sxs-lookup"><span data-stu-id="79414-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="79414-105">Les cartes adaptatives sont des extraits de contenu exploitables que vous pouvez ajouter à une conversation par le biais d'un bot ou d'une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="79414-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="79414-106">À l’aide de texte, de graphiques et de boutons, ces cartes fournissent une communication enrichie à votre public.</span><span class="sxs-lookup"><span data-stu-id="79414-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="79414-107">L’infrastructure de carte adaptative est utilisée dans de nombreux produits Microsoft, y compris Teams.</span><span class="sxs-lookup"><span data-stu-id="79414-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="79414-108">Vous pouvez envoyer des cartes à l’intérieur des messages aux utilisateurs via des bots ou des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="79414-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="79414-109">Les utilisateurs peuvent également effectuer des actions sur les cartes lorsqu’ils sont présents.</span><span class="sxs-lookup"><span data-stu-id="79414-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Exemple de vue d’ensemble d’une carte adaptative." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="79414-111">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="79414-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="79414-112">Vous trouverez des instructions de conception plus complètes pour Cartes adaptatives dans Teams, y compris les éléments que vous pouvez récupérer et modifier en fonction des besoins, dans le Kit d’interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="79414-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="79414-113">Le kit d’interface utilisateur couvre également des sujets essentiels tels que le thème, l’accessibilité et le dimensionnement réactif.</span><span class="sxs-lookup"><span data-stu-id="79414-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="79414-114">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="79414-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="79414-115">Concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="79414-115">Adaptive Cards designer</span></span>

<span data-ttu-id="79414-116">Vous pouvez également commencer à concevoir vos Cartes adaptatives directement dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="79414-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="79414-117">Essayer le concepteur Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="79414-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="79414-118">Types de Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="79414-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="79414-119">Bannière</span><span class="sxs-lookup"><span data-stu-id="79414-119">Hero</span></span>

<span data-ttu-id="79414-120">Notre carte la plus grande.</span><span class="sxs-lookup"><span data-stu-id="79414-120">Our largest card.</span></span> <span data-ttu-id="79414-121">À utiliser pour partager des articles ou des scénarios dans lesquels une image indique la majeure partie de l’histoire.</span><span class="sxs-lookup"><span data-stu-id="79414-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-122">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Exemple montrant une carte de bannière de carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-124">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="Exemple montrant une carte de bannière de carte adaptative sur un appareil mobile." border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="79414-126">Miniature</span><span class="sxs-lookup"><span data-stu-id="79414-126">Thumbnail</span></span>

<span data-ttu-id="79414-127">Permet d’envoyer un message actionnable simple.</span><span class="sxs-lookup"><span data-stu-id="79414-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-128">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Exemple montrant une carte miniature de carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-130">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="Exemple montrant une carte miniature de carte adaptative sur un appareil mobile." border="false":::

---

### <a name="list"></a><span data-ttu-id="79414-132">Répertorier</span><span class="sxs-lookup"><span data-stu-id="79414-132">List</span></span>

<span data-ttu-id="79414-133">Utilisez-le dans les scénarios où vous souhaitez que l’utilisateur choisisse un élément dans une liste, mais que les éléments n’ont pas besoin de beaucoup d’explications.</span><span class="sxs-lookup"><span data-stu-id="79414-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-134">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Exemple montrant une carte de liste de carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-136">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="Exemple montrant une carte de liste de carte adaptative sur un appareil mobile." border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a><span data-ttu-id="79414-138">Médias</span><span class="sxs-lookup"><span data-stu-id="79414-138">Media</span></span>

<span data-ttu-id="79414-139">À utiliser lorsque vous souhaitez combiner du texte et des médias, tels que l'audio ou la vidéo.</span><span class="sxs-lookup"><span data-stu-id="79414-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-140">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Exemple montrant une carte média de carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-142">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="Exemple montrant une carte média de carte adaptative sur un appareil mobile." border="false":::

---

### <a name="people"></a><span data-ttu-id="79414-144">Personnes</span><span class="sxs-lookup"><span data-stu-id="79414-144">People</span></span>

<span data-ttu-id="79414-145">Meilleure utilisation lorsque vous communiquez efficacement les personnes impliquées dans une tâche.</span><span class="sxs-lookup"><span data-stu-id="79414-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-146">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Exemple montrant une carte de contacts de carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-148">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="Exemple montrant une carte de contacts de carte adaptative sur un appareil mobile." border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="79414-150">Ticket de demande</span><span class="sxs-lookup"><span data-stu-id="79414-150">Request ticket</span></span>

<span data-ttu-id="79414-151">Permet d’obtenir des entrées rapides d’un utilisateur pour créer automatiquement une tâche ou un ticket.</span><span class="sxs-lookup"><span data-stu-id="79414-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-152">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Exemple montrant une carte de ticket de demande de Carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-154">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="Exemple montrant une carte de ticket de demande de Carte adaptative sur un appareil mobile." border="false":::

---

### <a name="image-set"></a><span data-ttu-id="79414-156">Jeu d’images</span><span class="sxs-lookup"><span data-stu-id="79414-156">Image set</span></span>

<span data-ttu-id="79414-157">Permet d’envoyer plusieurs miniatures d’image.</span><span class="sxs-lookup"><span data-stu-id="79414-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-158">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Exemple montrant une carte de jeu d’image de Carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-160">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="Exemple montrant une carte de jeu d’image de Carte adaptative sur un appareil mobile." border="false":::

---

### <a name="action-set"></a><span data-ttu-id="79414-162">Jeu d’actions</span><span class="sxs-lookup"><span data-stu-id="79414-162">Action set</span></span>

<span data-ttu-id="79414-163">Utilisez cette option lorsque vous souhaitez que l’utilisateur sélectionne un bouton, puis recueille d'autres entrées utilisateur sur la même carte.</span><span class="sxs-lookup"><span data-stu-id="79414-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-164">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Exemple montrant une carte de jeu d’action de Carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-166">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="Exemple montrant une carte de jeu d’action de Carte adaptative sur un appareil mobile." border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="79414-168">Ensemble de choix</span><span class="sxs-lookup"><span data-stu-id="79414-168">Choice set</span></span>

<span data-ttu-id="79414-169">Permet de collecter plusieurs entrées de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79414-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-170">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Exemple montrant une carte d’ensemble de choix de Carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-172">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="Exemple montrant une carte d’ensemble de choix de Carte adaptative sur un appareil mobile." border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="79414-174">Anatomie</span><span class="sxs-lookup"><span data-stu-id="79414-174">Anatomy</span></span>

<span data-ttu-id="79414-175">Les cartes adaptatives ont une grande flexibilité.</span><span class="sxs-lookup"><span data-stu-id="79414-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="79414-176">Mais au minimum, nous vous suggérons vivement d’inclure les composants suivants dans chaque carte.</span><span class="sxs-lookup"><span data-stu-id="79414-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="79414-177">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="79414-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Exemple illustrant l'anatomie de la Carte adaptative." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="79414-179">Mobile</span><span class="sxs-lookup"><span data-stu-id="79414-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="Exemple illustrant l'anatomie de la Carte adaptative sur un appareil mobile." border="false":::

---

|<span data-ttu-id="79414-181">Compteur</span><span class="sxs-lookup"><span data-stu-id="79414-181">Counter</span></span>|<span data-ttu-id="79414-182">Description</span><span class="sxs-lookup"><span data-stu-id="79414-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="79414-183">A</span><span class="sxs-lookup"><span data-stu-id="79414-183">A</span></span>|<span data-ttu-id="79414-184">**En-tête** : rendez vos en-têtes clairs et concis.</span><span class="sxs-lookup"><span data-stu-id="79414-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="79414-185">B</span><span class="sxs-lookup"><span data-stu-id="79414-185">B</span></span>|<span data-ttu-id="79414-186">**Copie du corps** : transmettez des détails trop longs ou pas assez importants pour être inclus dans l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="79414-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="79414-187">C</span><span class="sxs-lookup"><span data-stu-id="79414-187">C</span></span>|<span data-ttu-id="79414-188">**Actions principales** : il est recommandé d’inclure entre 1 et 3 actions principales.</span><span class="sxs-lookup"><span data-stu-id="79414-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="79414-189">Un groupe peut comporter jusqu’à six.</span><span class="sxs-lookup"><span data-stu-id="79414-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="79414-190">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="79414-190">Best practices</span></span>

<span data-ttu-id="79414-191">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="79414-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="79414-192">Actions principales et secondaires</span><span class="sxs-lookup"><span data-stu-id="79414-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Meilleure pratique concernant la façon dont vous ne devez inclure qu’un petit jeu d’actions sur une carte adaptative." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="79414-194">À faire : utiliser jusqu’à six actions principales</span><span class="sxs-lookup"><span data-stu-id="79414-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="79414-195">Bien que Cartes adaptatives puisse prendre en charge six actions principales, la plupart des cartes n’en ont pas besoin.</span><span class="sxs-lookup"><span data-stu-id="79414-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="79414-196">Les actions doivent être claires, concises et directes.</span><span class="sxs-lookup"><span data-stu-id="79414-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="79414-197">Moins, c’est plus.</span><span class="sxs-lookup"><span data-stu-id="79414-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Meilleure pratique pour ne pas surcharger les utilisateurs avec un trop grand nombre d’actions sur une carte adaptative." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="79414-199">À ne pas faire : utiliser plus de six actions principales</span><span class="sxs-lookup"><span data-stu-id="79414-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="79414-200">Les cartes adaptatives doivent présenter un contenu rapide et exploitable.</span><span class="sxs-lookup"><span data-stu-id="79414-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="79414-201">Un trop grand nombre d’actions peut surcharger un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79414-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="79414-202">Fréquence</span><span class="sxs-lookup"><span data-stu-id="79414-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Meilleure pratique concernant la fréquence des cartes adaptatives." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="79414-204">À faire : être concis</span><span class="sxs-lookup"><span data-stu-id="79414-204">Do: Be concise</span></span>

<span data-ttu-id="79414-205">Il est facile d’envoyer plusieurs cartes dans une conversation, mais une fois que les cartes défilent hors de l’affichage, elles deviennent moins utiles.</span><span class="sxs-lookup"><span data-stu-id="79414-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="79414-206">Essayez de vous limiter à l’essentiel.</span><span class="sxs-lookup"><span data-stu-id="79414-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="79414-207">Cela est particulièrement vrai dans un canal où les utilisateurs ont moins de tolérance pour ce qu’ils considèrent comme du « bruit ».</span><span class="sxs-lookup"><span data-stu-id="79414-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
