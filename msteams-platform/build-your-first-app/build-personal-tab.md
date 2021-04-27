---
title: Get started - Build a personal tab
author: heath-hamilton
description: Créez rapidement un onglet personnel Microsoft Teams à l'aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: dabe427142dd3e6a1d2f01f83601cbffd4a20dbd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019978"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="78d6d-103">Créer un onglet personnel pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="78d6d-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="78d6d-104">Les onglets sont un moyen simple d'surfacer le contenu de votre application en insérant essentiellement une page web dans Teams.</span><span class="sxs-lookup"><span data-stu-id="78d6d-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="78d6d-105">Il existe deux types d'onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="78d6d-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="78d6d-106">Dans ce didacticiel, vous allez créer un onglet personnel *de* base, une page de contenu plein écran pour des utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="78d6d-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="78d6d-107">(Les onglets personnels sont les plus proches d'une expérience de site web classique dans Teams.)</span><span class="sxs-lookup"><span data-stu-id="78d6d-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="78d6d-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="78d6d-108">Before you begin</span></span>

<span data-ttu-id="78d6d-109">Vous avez besoin d'un onglet personnel d'exécution de base pour commencer.</span><span class="sxs-lookup"><span data-stu-id="78d6d-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="78d6d-110">Si vous n'en avez pas, voir [créer et exécuter votre première application Teams.](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="78d6d-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="78d6d-111">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="78d6d-111">Your assignment</span></span>

<span data-ttu-id="78d6d-112">Les membres de votre organisation ont des difficultés à trouver des informations de contact de base pour des fonctions importantes (service d'aide, RESSOURCES HUMAINES, etc.).</span><span class="sxs-lookup"><span data-stu-id="78d6d-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="78d6d-113">Vous êtes chargé de vous assurer qu'ils peuvent trouver rapidement ces informations au même endroit.</span><span class="sxs-lookup"><span data-stu-id="78d6d-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="78d6d-114">Comment le feriez-vous ?</span><span class="sxs-lookup"><span data-stu-id="78d6d-114">How would you do that?</span></span> <span data-ttu-id="78d6d-115">Un onglet personnel Teams, bien entendu.</span><span class="sxs-lookup"><span data-stu-id="78d6d-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="78d6d-116">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="78d6d-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="78d6d-117">Identifier certaines configurations d'application et la échafaudage pertinentes pour les onglets personnels</span><span class="sxs-lookup"><span data-stu-id="78d6d-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="78d6d-118">Créer du contenu d'onglet</span><span class="sxs-lookup"><span data-stu-id="78d6d-118">Create tab content</span></span>
> * <span data-ttu-id="78d6d-119">Mettre à jour le thème de couleur d'un onglet en fonction des préférences de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="78d6d-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="78d6d-120">1. Identifier les composants de projet d'application pertinents</span><span class="sxs-lookup"><span data-stu-id="78d6d-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="78d6d-121">La plupart des configurations d'application et de la création de la Shared Computer Toolkit sont automatiquement définies lorsque vous créez votre projet.</span><span class="sxs-lookup"><span data-stu-id="78d6d-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="78d6d-122">Examinons les principaux composants de la création d'un onglet personnel.</span><span class="sxs-lookup"><span data-stu-id="78d6d-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="78d6d-123">Configurations d'application</span><span class="sxs-lookup"><span data-stu-id="78d6d-123">App configurations</span></span>

<span data-ttu-id="78d6d-124">Dans le kit de ressources, allez dans **App Studio** pour afficher et mettre à jour les configurations de votre application.</span><span class="sxs-lookup"><span data-stu-id="78d6d-124">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="78d6d-125">Échafaudage d'application</span><span class="sxs-lookup"><span data-stu-id="78d6d-125">App scaffolding</span></span>

<span data-ttu-id="78d6d-126">La échafaudage de l'application fournit les composants pour le rendu de votre onglet personnel dans Teams.</span><span class="sxs-lookup"><span data-stu-id="78d6d-126">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="78d6d-127">Il y a beaucoup de choses que vous pouvez utiliser, mais pour l'instant, vous ne devez vous concentrer que sur les questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="78d6d-127">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="78d6d-128">`Tab.js` dans le `src/components` répertoire de votre projet.</span><span class="sxs-lookup"><span data-stu-id="78d6d-128">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="78d6d-129">Il s'agit du rendu de la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="78d6d-129">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="78d6d-130">SDK client JavaScript Microsoft Teams, qui est pré-chargé dans les composants frontaux de votre projet.</span><span class="sxs-lookup"><span data-stu-id="78d6d-130">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="78d6d-131">2. Personnaliser la page de contenu de votre onglet</span><span class="sxs-lookup"><span data-stu-id="78d6d-131">2. Customize your tab content page</span></span>

<span data-ttu-id="78d6d-132">Compilez une liste de contacts importants dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="78d6d-132">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="78d6d-133">Copiez et mettez à jour l'extrait de code suivant avec les informations qui vous sont pertinentes ou, dans un souci de temps, utilisez le code tel qu'il est.</span><span class="sxs-lookup"><span data-stu-id="78d6d-133">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="78d6d-134">Go to the `src/components` directory and open `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="78d6d-134">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="78d6d-135">Recherchez `render()` la fonction et collez votre contenu à l'intérieur `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="78d6d-135">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="78d6d-136">Ajoutez la règle suivante pour que les liens de messagerie soient plus faciles à `App.css` lire, quel que soit le thème utilisé.</span><span class="sxs-lookup"><span data-stu-id="78d6d-136">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="78d6d-137">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="78d6d-137">Save your changes.</span></span> <span data-ttu-id="78d6d-138">Go to your app's tab in Teams to view the new content.</span><span class="sxs-lookup"><span data-stu-id="78d6d-138">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Capture d'écran d'un onglet personnel avec du contenu statique.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="78d6d-140">3. Mettre à jour le thème de l'onglet</span><span class="sxs-lookup"><span data-stu-id="78d6d-140">3. Update the tab theme</span></span>

<span data-ttu-id="78d6d-141">Les bonnes applications sont natives de Teams. Il est donc important que votre onglet se fonde avec le thème Teams préféré de vos utilisateurs : par défaut (clair), foncé ou contraste élevé.</span><span class="sxs-lookup"><span data-stu-id="78d6d-141">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="78d6d-142">Comme vous l'avez peut-être remarqué dans la dernière capture d'écran, votre onglet a toujours un arrière-plan clair lorsque le client utilise le thème foncé.</span><span class="sxs-lookup"><span data-stu-id="78d6d-142">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="78d6d-143">Il ne s'agit pas d'une expérience utilisateur recommandée.</span><span class="sxs-lookup"><span data-stu-id="78d6d-143">This is not a recommended user experience.</span></span>

<span data-ttu-id="78d6d-144">Le [SDK client JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) teams peut rendre votre application sensible aux modifications de thème dans le client et y réagir.</span><span class="sxs-lookup"><span data-stu-id="78d6d-144">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="78d6d-145">Examinons comment faire.</span><span class="sxs-lookup"><span data-stu-id="78d6d-145">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="78d6d-146">Obtenir du contexte sur le client Teams</span><span class="sxs-lookup"><span data-stu-id="78d6d-146">Get context about the Teams client</span></span>

<span data-ttu-id="78d6d-147">Dans votre fichier, il existe un appel qui fournit des informations sur, entre autres, le `Tab.js` `microsoftTeams.getContext()` thème client [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) configuré.</span><span class="sxs-lookup"><span data-stu-id="78d6d-147">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="78d6d-148">Grâce à la échafaudage de l'application, utilisez ce code tel qu'il est pour accéder à `context` l'interface et à ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="78d6d-148">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

```JavaScript
componentDidMount(){
  // Get the user context from Teams and set it in the state
  microsoftTeams.getContext((context, error) => {
    this.setState({
      context: context
    });
  });
  // Next steps: Error handling using the error object
}
```

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="78d6d-149">Créer un handler de modification de thème</span><span class="sxs-lookup"><span data-stu-id="78d6d-149">Create a theme change handler</span></span>

<span data-ttu-id="78d6d-150">Avec les propriétés en main, votre application a une bonne compréhension de ce qui se passe `context` autour de elle dans Teams.</span><span class="sxs-lookup"><span data-stu-id="78d6d-150">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="78d6d-151">Toutefois, l'application ne sait toujours pas que son apparence doit refléter le thème choisi par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="78d6d-151">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="78d6d-152">Vous avez besoin d'un handler pour que l'état de votre application change avec le thème.</span><span class="sxs-lookup"><span data-stu-id="78d6d-152">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="78d6d-153">Insérez le handler de modification de thème suivant immédiatement après `microsoftTeams.getContext()` l'appel.</span><span class="sxs-lookup"><span data-stu-id="78d6d-153">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="78d6d-154">Faire correspondre les styles de thème</span><span class="sxs-lookup"><span data-stu-id="78d6d-154">Match theme styles</span></span>

<span data-ttu-id="78d6d-155">Votre handler de modification de thème est en place, mais vous avez besoin d'un code qui répond à ces modifications et aligne les couleurs de votre onglet sur le thème actuel.</span><span class="sxs-lookup"><span data-stu-id="78d6d-155">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="78d6d-156">L'exemple suivant n'est qu'une façon d'appliquer des styles à votre onglet. Utilisez le code tel qu'il est, développez-le ou écrivez le vôtre.</span><span class="sxs-lookup"><span data-stu-id="78d6d-156">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="78d6d-157">Dans la `render()` fonction, stockez l'état fourni par le handler de modification de thème dans `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="78d6d-157">In the `render()` function, store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="78d6d-158">Après avoir stocké l'état fourni par le handler de modification de thème, fournissez une logique conditionnelle pour restituer les styles de votre onglet en fonction du thème actuel.</span><span class="sxs-lookup"><span data-stu-id="78d6d-158">After storing the state provided by the theme change handler, provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="78d6d-159">L'exemple suivant montre une façon de faire de base :</span><span class="sxs-lookup"><span data-stu-id="78d6d-159">The following example shows a basic way to do this:</span></span>
1. <span data-ttu-id="78d6d-160">Vérifiez le thème actuel dans `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="78d6d-160">Check the current theme in `isTheme`.</span></span>
2. <span data-ttu-id="78d6d-161">Créez `newTheme` un objet avec des propriétés CSS pertinentes pour le thème actuel.</span><span class="sxs-lookup"><span data-stu-id="78d6d-161">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
3. <span data-ttu-id="78d6d-162">Appliquez la CSS à l'élément HTML racine de votre onglet ( `<div style={newTheme}>` ).</span><span class="sxs-lookup"><span data-stu-id="78d6d-162">Apply the CSS to your tab content's root HTML element (`<div style={newTheme}>`).</span></span>

```JavaScript
let newTheme

if (isTheme === "default") {
  newTheme = {
    backgroundColor: "#EEF1F5",
    color: "#16233A"
  };
} else {
  newTheme = {
    backgroundColor: "#2B2B30",
    color: "#FFFFFF"
  };
}
```

<span data-ttu-id="78d6d-163">Vérifiez votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="78d6d-163">Check your tab in Teams.</span></span> <span data-ttu-id="78d6d-164">L'apparence doit correspondre étroitement au thème foncé.</span><span class="sxs-lookup"><span data-stu-id="78d6d-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Capture d'écran d'un onglet personnel avec affichage de contenu statique.":::

## <a name="well-done"></a><span data-ttu-id="78d6d-166">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="78d6d-166">Well done</span></span>

<span data-ttu-id="78d6d-167">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="78d6d-167">Congratulations!</span></span> <span data-ttu-id="78d6d-168">Vous avez une application Teams avec un onglet personnel qui facilite la recherche de contacts importants dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="78d6d-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="78d6d-169">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="78d6d-169">Learn more</span></span>

* <span data-ttu-id="78d6d-170">Suivez nos [instructions de conception](../tabs/design/tabs.md) et créez avec des [modèles d'interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) prêts pour la production pour créer une expérience transparente.</span><span class="sxs-lookup"><span data-stu-id="78d6d-170">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="78d6d-171">Comprendre [les considérations mobiles pour](../tabs/design/tabs-mobile.md) les onglets.</span><span class="sxs-lookup"><span data-stu-id="78d6d-171">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="78d6d-172">[Ajoutez l'authentification sso à votre onglet.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="78d6d-172">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="78d6d-173">Utiliser les données Teams avec [Microsoft Graph.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="78d6d-173">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* <span data-ttu-id="78d6d-174">[Créez un onglet sans le kit de ressources.](../tabs/quickstarts/create-personal-tab-node-yeoman.md)</span><span class="sxs-lookup"><span data-stu-id="78d6d-174">[Create a tab without the toolkit](../tabs/quickstarts/create-personal-tab-node-yeoman.md).</span></span>

## <a name="next-lesson"></a><span data-ttu-id="78d6d-175">Leçon suivante</span><span class="sxs-lookup"><span data-stu-id="78d6d-175">Next lesson</span></span>

<span data-ttu-id="78d6d-176">Vous savez comment créer un onglet pour une utilisation personnelle.</span><span class="sxs-lookup"><span data-stu-id="78d6d-176">You know how to build a tab for personal use.</span></span> <span data-ttu-id="78d6d-177">Examinons ce qu'il faut pour créer un onglet pour les canaux d'équipe et les conversations.</span><span class="sxs-lookup"><span data-stu-id="78d6d-177">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="78d6d-178">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="78d6d-178">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
