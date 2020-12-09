---
title: Conception de cartes adaptatives pour votre application
description: Découvrez comment concevoir des cartes adaptatives pour teams et obtenir le kit d’interface utilisateur Microsoft Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604521"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="c96a4-103">Conception de cartes adaptatives pour votre application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="c96a4-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="c96a4-104">Une carte adaptative contient un corps de forme libre des éléments de carte et un ensemble facultatif d’actions.</span><span class="sxs-lookup"><span data-stu-id="c96a4-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="c96a4-105">Les cartes adaptatives sont des extraits de code actionnables, que vous pouvez ajouter à une conversation via un bot ou une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="c96a4-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="c96a4-106">À l’aide de texte, de graphiques et de boutons, ces cartes fournissent une meilleure communication à votre public.</span><span class="sxs-lookup"><span data-stu-id="c96a4-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="c96a4-107">La structure de carte adaptative est utilisée dans de nombreux produits Microsoft, y compris Teams.</span><span class="sxs-lookup"><span data-stu-id="c96a4-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="c96a4-108">Vous pouvez envoyer des cartes à l’intérieur des messages à des utilisateurs via des robots ou des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="c96a4-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="c96a4-109">Les utilisateurs peuvent effectuer des actions sur les cartes lorsqu’elles sont présentes.</span><span class="sxs-lookup"><span data-stu-id="c96a4-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Exemple de carte adaptative." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="c96a4-111">Kit d’interface utilisateur Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="c96a4-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="c96a4-112">Vous trouverez des instructions de conception plus complètes pour les cartes adaptatives dans Teams, y compris les éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c96a4-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="c96a4-113">Le kit d’interface utilisateur aborde également les sujets essentiels tels que les thèmes, l’accessibilité et le dimensionnement réactif.</span><span class="sxs-lookup"><span data-stu-id="c96a4-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c96a4-114">Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="c96a4-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="c96a4-115">Concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="c96a4-115">Adaptive Cards designer</span></span>

<span data-ttu-id="c96a4-116">Vous pouvez également commencer à concevoir vos cartes adaptatives directement dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="c96a4-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c96a4-117">Essayer le concepteur de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="c96a4-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="c96a4-118">Types de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="c96a4-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="c96a4-119">Hero</span><span class="sxs-lookup"><span data-stu-id="c96a4-119">Hero</span></span>

<span data-ttu-id="c96a4-120">Notre plus grande carte.</span><span class="sxs-lookup"><span data-stu-id="c96a4-120">Our largest card.</span></span> <span data-ttu-id="c96a4-121">À utiliser pour partager des articles ou des scénarios dans lesquels une image indique la plus grande partie de l’histoire.</span><span class="sxs-lookup"><span data-stu-id="c96a4-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="thumbnail"></a><span data-ttu-id="c96a4-123">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="c96a4-123">Thumbnail</span></span>

<span data-ttu-id="c96a4-124">Permet d’envoyer un message actionnable simple.</span><span class="sxs-lookup"><span data-stu-id="c96a4-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="list"></a><span data-ttu-id="c96a4-126">Répertorier</span><span class="sxs-lookup"><span data-stu-id="c96a4-126">List</span></span>

<span data-ttu-id="c96a4-127">À utiliser dans les scénarios dans lesquels vous souhaitez que l’utilisateur sélectionne un élément dans une liste, mais les éléments n’ont pas besoin de beaucoup d’explications.</span><span class="sxs-lookup"><span data-stu-id="c96a4-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="digest"></a><span data-ttu-id="c96a4-129">Digest</span><span class="sxs-lookup"><span data-stu-id="c96a4-129">Digest</span></span>

<span data-ttu-id="c96a4-130">À utiliser pour les résumés d’actualité et les billets d’arrondi.</span><span class="sxs-lookup"><span data-stu-id="c96a4-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="c96a4-131">Remarque : nous vous recommandons d’utiliser la carte miniature pour une seule mise à jour ou un seul élément d’actualité.</span><span class="sxs-lookup"><span data-stu-id="c96a4-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="media"></a><span data-ttu-id="c96a4-133">Multimédia</span><span class="sxs-lookup"><span data-stu-id="c96a4-133">Media</span></span>

<span data-ttu-id="c96a4-134">À utiliser lorsque vous souhaitez combiner du texte et des médias, comme audio ou vidéo.</span><span class="sxs-lookup"><span data-stu-id="c96a4-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="people"></a><span data-ttu-id="c96a4-136">Contacts</span><span class="sxs-lookup"><span data-stu-id="c96a4-136">People</span></span>

<span data-ttu-id="c96a4-137">Idéal pour transmettre efficacement les personnes impliquées dans une tâche.</span><span class="sxs-lookup"><span data-stu-id="c96a4-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="request-ticket"></a><span data-ttu-id="c96a4-139">Demander un ticket</span><span class="sxs-lookup"><span data-stu-id="c96a4-139">Request ticket</span></span>

<span data-ttu-id="c96a4-140">Utilisez pour obtenir des entrées rapides d’un utilisateur afin de créer automatiquement une tâche ou un ticket.</span><span class="sxs-lookup"><span data-stu-id="c96a4-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="imageset"></a><span data-ttu-id="c96a4-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="c96a4-142">ImageSet</span></span>

<span data-ttu-id="c96a4-143">Permet d’envoyer plusieurs miniatures d’image.</span><span class="sxs-lookup"><span data-stu-id="c96a4-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="actionset"></a><span data-ttu-id="c96a4-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="c96a4-145">ActionSet</span></span>

<span data-ttu-id="c96a4-146">Utilisez cette option lorsque vous souhaitez que l’utilisateur sélectionne un bouton, puis recueille une entrée utilisateur supplémentaire à partir de la même carte.</span><span class="sxs-lookup"><span data-stu-id="c96a4-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="choiceset"></a><span data-ttu-id="c96a4-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="c96a4-148">ChoiceSet</span></span>

<span data-ttu-id="c96a4-149">Permet de collecter plusieurs entrées de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c96a4-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Exemple de carte adaptative." border="false":::

## <a name="anatomy"></a><span data-ttu-id="c96a4-151">Anatomie</span><span class="sxs-lookup"><span data-stu-id="c96a4-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’une carte adaptative." border="false":::

<span data-ttu-id="c96a4-153">Les cartes adaptatives offrent une grande flexibilité.</span><span class="sxs-lookup"><span data-stu-id="c96a4-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="c96a4-154">Au minimum, nous vous suggérons vivement d’inclure les composants suivants dans chaque carte :</span><span class="sxs-lookup"><span data-stu-id="c96a4-154">But at a minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="c96a4-155">Compteur</span><span class="sxs-lookup"><span data-stu-id="c96a4-155">Counter</span></span>|<span data-ttu-id="c96a4-156">Description</span><span class="sxs-lookup"><span data-stu-id="c96a4-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c96a4-157">A</span><span class="sxs-lookup"><span data-stu-id="c96a4-157">A</span></span>|<span data-ttu-id="c96a4-158">**En-tête**: rendez les en-têtes claires et concises, mais descriptives.</span><span class="sxs-lookup"><span data-stu-id="c96a4-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="c96a4-159">B</span><span class="sxs-lookup"><span data-stu-id="c96a4-159">B</span></span>|<span data-ttu-id="c96a4-160">**Copie du corps**: permet de transmettre des détails trop longs ou pas suffisamment importants pour être inclus dans l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="c96a4-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="c96a4-161">C</span><span class="sxs-lookup"><span data-stu-id="c96a4-161">C</span></span>|<span data-ttu-id="c96a4-162">**Actions principales**: il est recommandé d’inclure les actions principales 1-3.</span><span class="sxs-lookup"><span data-stu-id="c96a4-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="c96a4-163">Un maximum de six est autorisé.</span><span class="sxs-lookup"><span data-stu-id="c96a4-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="c96a4-164">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="c96a4-164">Best practices</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="c96a4-165">Actions principales et secondaires</span><span class="sxs-lookup"><span data-stu-id="c96a4-165">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Exemple illustrant une meilleure pratique adaptative de cartes." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="c96a4-167">Do : utiliser jusqu’à six actions principales</span><span class="sxs-lookup"><span data-stu-id="c96a4-167">Do: Use up to six primary actions</span></span>

<span data-ttu-id="c96a4-168">Bien que les cartes adaptatives puissent prendre en charge six actions principales, la plupart des cartes n’en ont pas besoin.</span><span class="sxs-lookup"><span data-stu-id="c96a4-168">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="c96a4-169">Les actions doivent être claires, concises et directes.</span><span class="sxs-lookup"><span data-stu-id="c96a4-169">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="c96a4-170">Moins est plus.</span><span class="sxs-lookup"><span data-stu-id="c96a4-170">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Exemple illustrant une meilleure pratique adaptative de cartes." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="c96a4-172">Ne pas utiliser plus de six actions principales</span><span class="sxs-lookup"><span data-stu-id="c96a4-172">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="c96a4-173">Les cartes adaptatives doivent présenter un contenu rapide et actionnable.</span><span class="sxs-lookup"><span data-stu-id="c96a4-173">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="c96a4-174">Trop d’actions peuvent inonder un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c96a4-174">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="c96a4-175">Fréquence</span><span class="sxs-lookup"><span data-stu-id="c96a4-175">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Exemple illustrant une meilleure pratique adaptative de cartes." border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="c96a4-177">Do : être concis</span><span class="sxs-lookup"><span data-stu-id="c96a4-177">Do: Be concise</span></span>

<span data-ttu-id="c96a4-178">Il est facile d’envoyer plusieurs cartes dans une conversation, mais une fois que les cartes sortent de l’affichage, elles deviennent moins utiles.</span><span class="sxs-lookup"><span data-stu-id="c96a4-178">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="c96a4-179">Essayez de vous limiter aux notions fondamentales.</span><span class="sxs-lookup"><span data-stu-id="c96a4-179">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="c96a4-180">Cela est particulièrement vrai dans un canal où les utilisateurs ont moins de tolérance pour ce qu’ils perçoivent comme « bruit ».</span><span class="sxs-lookup"><span data-stu-id="c96a4-180">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
