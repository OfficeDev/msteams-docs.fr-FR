---
title: Déploiement du lien des onglets et vue des étapes
author: Rajeshwari-v
description: Découvrez comment déployer un lien, ouvrir l’affichage de la scène et épingler un onglet avec Microsoft Teams application.
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: b54eb5942d19749b39bb9bb504dd8645f5655ef3
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179943"
---
# <a name="tabs-link-unfurling-and-stage-view"></a><span data-ttu-id="ab0e6-103">Déploiement du lien des onglets et vue des étapes</span><span class="sxs-lookup"><span data-stu-id="ab0e6-103">Tabs link unfurling and Stage View</span></span>

> [!NOTE]
> <span data-ttu-id="ab0e6-104">Cette fonctionnalité est disponible uniquement en prévisualisation [pour les](../resources/dev-preview/developer-preview-intro.md) développeurs publics.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-104">This feature is available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="ab0e6-105">Stage View est un nouveau composant d’interface utilisateur qui vous permet d’afficher le contenu ouvert en plein écran en Teams et épinglé sous forme d’onglet.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-105">Stage View is a new user interface (UI) component, which allows you to render the content that is opened in full screen in Teams and pinned as a tab.</span></span>
 
> [!NOTE]
> <span data-ttu-id="ab0e6-106">Actuellement, Teams clients mobiles n’ont pas d’onglets de prise en charge du déploiement et de l’affichage de la phase.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-106">Currently, Teams mobile clients do no support tabs link unfurling and Stage View.</span></span> <span data-ttu-id="ab0e6-107">Les clients mobiles utilisent l’attribut fourni par le développeur pour ouvrir la page dans le `websiteUrl` navigateur web de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-107">Mobile clients use the `websiteUrl` attribute provided by the developer to open the page in the device's web browser.</span></span>

## <a name="stage-view"></a><span data-ttu-id="ab0e6-108">Vue d’étape</span><span class="sxs-lookup"><span data-stu-id="ab0e6-108">Stage View</span></span>

<span data-ttu-id="ab0e6-109">L’affichage d’étape est un composant d’interface utilisateur en plein écran que vous pouvez appeler pour faire surface à votre contenu web.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-109">Stage View is a full screen UI component that you can invoke to surface your web content.</span></span> <span data-ttu-id="ab0e6-110">Le service de déploiement de lien existant est mis à jour de sorte qu’il soit utilisé pour transformer les URL en onglet à l’aide d’une carte adaptative et des services de conversation.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-110">The existing link unfurling service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="ab0e6-111">Lorsqu’un utilisateur envoie une URL dans une conversation ou un canal, l’URL est déployée vers une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-111">When a user sends a URL in a chat or channel, the URL is unfurled to an Adaptive Card.</span></span> <span data-ttu-id="ab0e6-112">L’utilisateur peut sélectionner **Afficher** dans la carte et épingler le contenu sous la direction d’un onglet directement à partir de l’affichage de l’étape.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-112">The user can select **View** in the card, and pin the content as a tab directly from Stage View.</span></span>

## <a name="advantage-of-stage-view"></a><span data-ttu-id="ab0e6-113">Avantage de l’affichage de l’étape</span><span class="sxs-lookup"><span data-stu-id="ab0e6-113">Advantage of Stage View</span></span>

<span data-ttu-id="ab0e6-114">L’affichage par étapes permet d’offrir une expérience plus transparente de l’affichage du contenu Teams.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-114">Stage View helps provide a more seamless experience of viewing content in Teams.</span></span> <span data-ttu-id="ab0e6-115">Les utilisateurs peuvent ouvrir et afficher le contenu fourni par votre application sans quitter le contexte, et ils peuvent épingler le contenu à la conversation ou au canal pour un accès rapide futur.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-115">Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access.</span></span> <span data-ttu-id="ab0e6-116">Cela entraîne un plus grand engagement de l’utilisateur avec votre application.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-116">This leads to a higher user engagement with your app.</span></span>

## <a name="stage-view-vs-task-module"></a><span data-ttu-id="ab0e6-117">Affichage de l’étape et module de tâche</span><span class="sxs-lookup"><span data-stu-id="ab0e6-117">Stage View vs. Task module</span></span>

|<span data-ttu-id="ab0e6-118">Vue d’étape</span><span class="sxs-lookup"><span data-stu-id="ab0e6-118">Stage View</span></span>|<span data-ttu-id="ab0e6-119">Module de tâche</span><span class="sxs-lookup"><span data-stu-id="ab0e6-119">Task module</span></span>|
|:-----------|:-----------|
|<span data-ttu-id="ab0e6-120">L’affichage d’étape est utile lorsque vous avez du contenu enrichi à afficher aux utilisateurs, comme une page, un tableau de bord, un fichier, etc.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-120">Stage View is useful when you have rich content to display to the users, such as a page, a dashboard, a file, and so on.</span></span> <span data-ttu-id="ab0e6-121">Il fournit des fonctionnalités enrichies qui permettent d’restituer votre contenu dans le canevas plein écran.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-121">It provides  rich features that helps to render your content in the full-screen canvas.</span></span>|<span data-ttu-id="ab0e6-122">[Le module de](../task-modules-and-cards/task-modules/task-modules-tabs.md) tâche est particulièrement utile pour afficher les messages qui nécessitent l’attention de l’utilisateur ou collecter les informations requises pour passer à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-122">[Task module](../task-modules-and-cards/task-modules/task-modules-tabs.md) is especially useful to display messages that require user attention, or collect information required to move to the next step.</span></span>|
  
## <a name="invoke-stage-view"></a><span data-ttu-id="ab0e6-123">Appeler l’affichage de l’étape</span><span class="sxs-lookup"><span data-stu-id="ab0e6-123">Invoke Stage View</span></span>

<span data-ttu-id="ab0e6-124">Vous pouvez appeler l’affichage de l’étape des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="ab0e6-124">You can invoke Stage View in the following  ways:</span></span>

* [<span data-ttu-id="ab0e6-125">Appeler la vue d’étape à partir d’une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="ab0e6-125">Invoke Stage View from Adaptive Card</span></span>](#invoke-stage-view-from-adaptive-card)
* [<span data-ttu-id="ab0e6-126">Appeler l’affichage de l’étape par le biais d’un lien profond</span><span class="sxs-lookup"><span data-stu-id="ab0e6-126">Invoke Stage View through deep link</span></span>](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a><span data-ttu-id="ab0e6-127">Appeler la vue d’étape à partir d’une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="ab0e6-127">Invoke Stage View from Adaptive Card</span></span>

<span data-ttu-id="ab0e6-128">Lorsque l’utilisateur entre une URL sur le client de bureau Teams, [](../task-modules-and-cards/cards/cards-actions.md) le bot est appelé et renvoie une carte adaptative avec la possibilité d’ouvrir l’URL dans une étape.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-128">When the user enters a URL on the Teams desktop client, the bot is invoked and returns an [Adaptive Card](../task-modules-and-cards/cards/cards-actions.md) with the option to open the URL in a stage.</span></span> <span data-ttu-id="ab0e6-129">Une fois qu’une étape est lancée et que l’étape est fournie, vous pouvez ajouter la possibilité d’épingler l’étape `tabInfo` sous la mesure d’un onglet.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-129">After a stage is launched and the `tabInfo` is provided, you can add the ability to pin the stage as a tab.</span></span>  

<span data-ttu-id="ab0e6-130">Les images suivantes affichent une étape ouverte à partir d’une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="ab0e6-130">The following images display a stage opened from an Adaptive Card:</span></span>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

### <a name="example"></a><span data-ttu-id="ab0e6-131">Exemple</span><span class="sxs-lookup"><span data-stu-id="ab0e6-131">Example</span></span>

<span data-ttu-id="ab0e6-132">Voici le code pour ouvrir une étape à partir d’une carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="ab0e6-132">Following is the code to open a stage from an Adaptive Card:</span></span>

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

<span data-ttu-id="ab0e6-133">Le `invoke` type de requête doit être `composeExtension/queryLink` .</span><span class="sxs-lookup"><span data-stu-id="ab0e6-133">The `invoke` request type must be `composeExtension/queryLink`.</span></span>

> [!NOTE]
> * <span data-ttu-id="ab0e6-134">`invoke` est similaire au flux de travail `appLinking` actuel.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-134">`invoke` workflow is similar to the current `appLinking` workflow.</span></span> 
> * <span data-ttu-id="ab0e6-135">Pour conserver la cohérence, il est recommandé de nommer `Action.Submit` comme `View` .</span><span class="sxs-lookup"><span data-stu-id="ab0e6-135">To maintain consistency, it is recommended to name `Action.Submit` as `View`.</span></span>
> * <span data-ttu-id="ab0e6-136">`websiteUrl` est une propriété obligatoire à passer dans `TabInfo` l’objet.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-136">`websiteUrl` is a required property to be passed in the `TabInfo` object.</span></span>

<span data-ttu-id="ab0e6-137">Voici le processus d’appel de l’affichage de l’étape :</span><span class="sxs-lookup"><span data-stu-id="ab0e6-137">Following is the process to invoke Stage View:</span></span>

* <span data-ttu-id="ab0e6-138">Lorsque l’utilisateur sélectionne **Affichage,** le bot reçoit une `invoke` demande.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-138">When the user selects **View**, the bot receives an `invoke` request.</span></span> <span data-ttu-id="ab0e6-139">Le type de requête `composeExtension/queryLink` est .</span><span class="sxs-lookup"><span data-stu-id="ab0e6-139">The request type is `composeExtension/queryLink`.</span></span>
* <span data-ttu-id="ab0e6-140">`invoke` La réponse du bot contient une carte adaptative avec son `tab/tabInfoAction` type.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-140">`invoke` response from bot contains an Adaptive Card with type `tab/tabInfoAction` in it.</span></span>
* <span data-ttu-id="ab0e6-141">Le bot répond par un `200` code.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-141">The bot responds with a `200` code.</span></span>

> [!NOTE]
> <span data-ttu-id="ab0e6-142">Actuellement, Teams clients mobiles ne la prise en charge de la fonctionnalité d’affichage de la scène.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-142">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="ab0e6-143">Lorsqu’un utilisateur sélectionne **Afficher** sur un client mobile, l’utilisateur est conduit au navigateur de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-143">When a user selects **View** on a mobile client, the user is taken to the device's browser.</span></span> <span data-ttu-id="ab0e6-144">Le navigateur ouvre l’URL spécifiée dans le `websiteUrl` paramètre de `TabInfo` l’objet.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-144">The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.</span></span>

## <a name="invoke-stage-view-through-deep-link"></a><span data-ttu-id="ab0e6-145">Appeler l’affichage de l’étape par le biais d’un lien profond</span><span class="sxs-lookup"><span data-stu-id="ab0e6-145">Invoke Stage View through deep link</span></span>

<span data-ttu-id="ab0e6-146">Pour appeler l’affichage de l’étape via un lien profond à partir de votre onglet, vous devez encapsuler l’URL du lien profond dans `microsoftTeams.executeDeeplink(url)` l’API.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-146">To invoke the Stage View through deep link from your tab, you must wrap the deep link URL in the `microsoftTeams.executeDeeplink(url)` API.</span></span> <span data-ttu-id="ab0e6-147">Le lien profond peut également être transmis via une `OpenURL` action dans la carte.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-147">The deep link can also be passed through an `OpenURL` action in the card.</span></span>

<span data-ttu-id="ab0e6-148">L’image suivante affiche une vue d’étape invoquée via un lien profond :</span><span class="sxs-lookup"><span data-stu-id="ab0e6-148">The following image displays a Stage View invoked through a deep link:</span></span>

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a><span data-ttu-id="ab0e6-149">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ab0e6-149">Syntax</span></span>

<span data-ttu-id="ab0e6-150">Voici la syntaxe du lien profond :</span><span class="sxs-lookup"><span data-stu-id="ab0e6-150">Following is the deeplink syntax:</span></span>  
 
<span data-ttu-id="ab0e6-151"> https://teams.microsoft.com/l/stage/{appId}/0?context={« contentUrl »:"[contentUrl] »,"websiteUrl »:"[websiteUrl] »,"name »:"[name]"}</span><span class="sxs-lookup"><span data-stu-id="ab0e6-151">https://teams.microsoft.com/l/stage/{appId}/0?context={“contentUrl”:”[contentUrl]”,“websiteUrl”:”[websiteUrl]”,“name”:”[name]”}</span></span>

### <a name="examples"></a><span data-ttu-id="ab0e6-152">Exemples</span><span class="sxs-lookup"><span data-stu-id="ab0e6-152">Examples</span></span>

<span data-ttu-id="ab0e6-153">Lorsqu’un utilisateur entre une URL, elle est déployée dans une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-153">When a user enters a URL, it is unfurled into an Adaptive card.</span></span>

<span data-ttu-id="ab0e6-154">Voici les exemples de liens profonds pour appeler l’affichage de l’étape :</span><span class="sxs-lookup"><span data-stu-id="ab0e6-154">Following are the deep link examples to invoke Stage View:</span></span>

<span data-ttu-id="ab0e6-155">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="ab0e6-155">**Example 1**</span></span>

<span data-ttu-id="ab0e6-156"> https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={« contentUrl »:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx »,"websiteUrl »:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx »,"name »:"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="ab0e6-156">https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

<span data-ttu-id="ab0e6-157">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="ab0e6-157">**Example 2**</span></span>

<span data-ttu-id="ab0e6-158"> https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={« contentUrl »:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx »,"websiteUrl »:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx »,"name »:"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="ab0e6-158">https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

> [!NOTE]
> * <span data-ttu-id="ab0e6-159">Le `name` lien profond est facultatif.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-159">The `name` is optional in deep link.</span></span> <span data-ttu-id="ab0e6-160">S’il n’est pas inclus, le nom de l’application le remplace.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-160">If not included, the app name replaces it.</span></span>
> * <span data-ttu-id="ab0e6-161">Le lien profond peut également être transmis via une `OpenURL` action.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-161">The deep link can also be passed through an `OpenURL` action.</span></span>
> * <span data-ttu-id="ab0e6-162">Actuellement, Teams clients mobiles ne la prise en charge de la fonctionnalité d’affichage de la scène.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-162">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="ab0e6-163">Lorsque les utilisateurs sélectionnent un lien profond vers une vue d’étape, ils sont conduits au navigateur web de leur appareil.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-163">When users select a deep link to a Stage View, they are taken to their device's web browser.</span></span> <span data-ttu-id="ab0e6-164">Le navigateur web ouvre l’URL spécifiée dans le `websiteUrl` paramètre du lien profond.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-164">The web browser opens the URL specified in the `websiteUrl` parameter of the deep link.</span></span>
> * <span data-ttu-id="ab0e6-165">Lorsque vous lancez une étape à partir d’un certain contexte, assurez-vous que votre application fonctionne dans ce contexte.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-165">When you launch a Stage from a certain context, ensure that your app works in that context.</span></span> <span data-ttu-id="ab0e6-166">Par exemple, si votre vue d’étape est lancée à partir d’une application personnelle, vous devez vous assurer que votre application a une étendue personnelle.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-166">For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.</span></span>

## <a name="tab-information-property"></a><span data-ttu-id="ab0e6-167">Propriété d’informations sur l’onglet</span><span class="sxs-lookup"><span data-stu-id="ab0e6-167">Tab information property</span></span>

| <span data-ttu-id="ab0e6-168">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="ab0e6-168">Property name</span></span> | <span data-ttu-id="ab0e6-169">Type</span><span class="sxs-lookup"><span data-stu-id="ab0e6-169">Type</span></span> | <span data-ttu-id="ab0e6-170">Nombre de caractères</span><span class="sxs-lookup"><span data-stu-id="ab0e6-170">Number of characters</span></span> | <span data-ttu-id="ab0e6-171">Description</span><span class="sxs-lookup"><span data-stu-id="ab0e6-171">Description</span></span> |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | <span data-ttu-id="ab0e6-172">String</span><span class="sxs-lookup"><span data-stu-id="ab0e6-172">String</span></span> | <span data-ttu-id="ab0e6-173">64</span><span class="sxs-lookup"><span data-stu-id="ab0e6-173">64</span></span> | <span data-ttu-id="ab0e6-174">Cette propriété est un identificateur unique de l’entité affichée par l’onglet.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-174">This property is a  unique identifier for the entity that the tab displays.</span></span> <span data-ttu-id="ab0e6-175">Ce champ est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-175">This is a required field.</span></span>|
| `name` | <span data-ttu-id="ab0e6-176">String</span><span class="sxs-lookup"><span data-stu-id="ab0e6-176">String</span></span> | <span data-ttu-id="ab0e6-177">128</span><span class="sxs-lookup"><span data-stu-id="ab0e6-177">128</span></span> | <span data-ttu-id="ab0e6-178">Cette propriété est le nom complet de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-178">This property is the display name of the tab in the channel interface.</span></span> <span data-ttu-id="ab0e6-179">Ce champ est facultatif.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-179">This is an optional field.</span></span>|
| `contentUrl` | <span data-ttu-id="ab0e6-180">String</span><span class="sxs-lookup"><span data-stu-id="ab0e6-180">String</span></span> | <span data-ttu-id="ab0e6-181">2048</span><span class="sxs-lookup"><span data-stu-id="ab0e6-181">2048</span></span> | <span data-ttu-id="ab0e6-182">Cette propriété est l’URL https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans Teams dessin.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-182">This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span> <span data-ttu-id="ab0e6-183">Ce champ est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-183">This is a required field.</span></span>|
| `websiteUrl?` | <span data-ttu-id="ab0e6-184">String</span><span class="sxs-lookup"><span data-stu-id="ab0e6-184">String</span></span> | <span data-ttu-id="ab0e6-185">2048</span><span class="sxs-lookup"><span data-stu-id="ab0e6-185">2048</span></span> | <span data-ttu-id="ab0e6-186">Cette propriété est l’URL https:// pointer vers, si un utilisateur choisit d’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-186">This property is the https:// URL to point at, if a user selects to view in a browser.</span></span> <span data-ttu-id="ab0e6-187">Ce champ est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-187">This is a required field.</span></span>|
| `removeUrl?` | <span data-ttu-id="ab0e6-188">String</span><span class="sxs-lookup"><span data-stu-id="ab0e6-188">String</span></span> | <span data-ttu-id="ab0e6-189">2048</span><span class="sxs-lookup"><span data-stu-id="ab0e6-189">2048</span></span> | <span data-ttu-id="ab0e6-190">Cette propriété est l’URL https:// qui pointe vers l’interface utilisateur à afficher lorsque l’utilisateur supprime l’onglet. Il s’agit d’un champ facultatif.</span><span class="sxs-lookup"><span data-stu-id="ab0e6-190">This property is the https:// URL that points to the UI to be displayed when the user deletes the tab. This is an optional field.</span></span>|

## <a name="see-also"></a><span data-ttu-id="ab0e6-191">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ab0e6-191">See also</span></span>

* [<span data-ttu-id="ab0e6-192">Déploiement des liens des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="ab0e6-192">Messaging extensions link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="ab0e6-193">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="ab0e6-193">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="ab0e6-194">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="ab0e6-194">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="ab0e6-195">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="ab0e6-195">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a><span data-ttu-id="ab0e6-196">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="ab0e6-196">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab0e6-197">Créer des onglets de conversation</span><span class="sxs-lookup"><span data-stu-id="ab0e6-197">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)