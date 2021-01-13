---
title: Get started - Build a personal tab
author: heath-hamilton
description: Créez rapidement un onglet personnel Microsoft Teams à l’aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 86be39503ec4e4fde5fafe63f83b3a4fb6d956bf
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797805"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="cddfe-103">Créer un onglet personnel pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cddfe-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="cddfe-104">Les onglets sont un moyen simple d’surfacer le contenu de votre application en insérant essentiellement une page web dans Teams.</span><span class="sxs-lookup"><span data-stu-id="cddfe-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="cddfe-105">Il existe deux types d’onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="cddfe-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="cddfe-106">Dans ce didacticiel, vous allez créer un onglet personnel *de* base, une page de contenu plein écran pour des utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="cddfe-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="cddfe-107">(Les onglets personnels sont les plus proches d’une expérience de site web classique dans Teams.)</span><span class="sxs-lookup"><span data-stu-id="cddfe-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cddfe-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="cddfe-108">Before you begin</span></span>

<span data-ttu-id="cddfe-109">Vous avez besoin d’un onglet personnel d’exécution de base pour commencer.</span><span class="sxs-lookup"><span data-stu-id="cddfe-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="cddfe-110">Si vous n’en avez pas, voir [créer et exécuter votre première application Teams.](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="cddfe-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="cddfe-111">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="cddfe-111">Your assignment</span></span>

<span data-ttu-id="cddfe-112">Les membres de votre organisation ont des difficultés à trouver des informations de contact de base pour des fonctions importantes (service d’aide, RESSOURCES HUMAINES, etc.).</span><span class="sxs-lookup"><span data-stu-id="cddfe-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="cddfe-113">Vous êtes chargé de vous assurer qu’ils peuvent trouver rapidement ces informations au même endroit.</span><span class="sxs-lookup"><span data-stu-id="cddfe-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="cddfe-114">Comment le feriez-vous ?</span><span class="sxs-lookup"><span data-stu-id="cddfe-114">How would you do that?</span></span> <span data-ttu-id="cddfe-115">Un onglet personnel Teams, bien entendu.</span><span class="sxs-lookup"><span data-stu-id="cddfe-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="cddfe-116">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="cddfe-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="cddfe-117">Identifier certaines configurations d’application et la échafaudage pertinentes pour les onglets personnels</span><span class="sxs-lookup"><span data-stu-id="cddfe-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="cddfe-118">Créer du contenu d’onglet</span><span class="sxs-lookup"><span data-stu-id="cddfe-118">Create tab content</span></span>
> * <span data-ttu-id="cddfe-119">Mettre à jour le thème de couleur d’un onglet en fonction des préférences de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="cddfe-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="cddfe-120">1. Identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="cddfe-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="cddfe-121">La plupart des configurations d’application et de la création de la Shared Computer Toolkit sont automatiquement définies lorsque vous créez votre projet.</span><span class="sxs-lookup"><span data-stu-id="cddfe-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="cddfe-122">Examinons les principaux composants de la création d’un onglet personnel.</span><span class="sxs-lookup"><span data-stu-id="cddfe-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="cddfe-123">Configurations d’application</span><span class="sxs-lookup"><span data-stu-id="cddfe-123">App configurations</span></span>

<span data-ttu-id="cddfe-124">Dans le kit de ressources, allez dans **App Studio** pour afficher et mettre à jour les configurations de votre application.</span><span class="sxs-lookup"><span data-stu-id="cddfe-124">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="cddfe-125">Échafaudage d’application</span><span class="sxs-lookup"><span data-stu-id="cddfe-125">App scaffolding</span></span>

<span data-ttu-id="cddfe-126">La échafaudage de l’application fournit les composants pour le rendu de votre onglet personnel dans Teams.</span><span class="sxs-lookup"><span data-stu-id="cddfe-126">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="cddfe-127">Il y a beaucoup de choses que vous pouvez utiliser, mais pour l’instant, vous ne devez vous concentrer que sur les questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="cddfe-127">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="cddfe-128">`Tab.js` dans le `src/components` répertoire de votre projet.</span><span class="sxs-lookup"><span data-stu-id="cddfe-128">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="cddfe-129">Il s’agit du rendu de la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="cddfe-129">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="cddfe-130">SDK client JavaScript Microsoft Teams, qui est pré-chargé dans les composants frontaux de votre projet.</span><span class="sxs-lookup"><span data-stu-id="cddfe-130">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="cddfe-131">2. Personnaliser la page de contenu de votre onglet</span><span class="sxs-lookup"><span data-stu-id="cddfe-131">2. Customize your tab content page</span></span>

<span data-ttu-id="cddfe-132">Compilez une liste de contacts importants dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="cddfe-132">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="cddfe-133">Copiez et mettez à jour l’extrait de code suivant avec les informations qui vous sont pertinentes ou, par souci de temps, utilisez le code tel qu’il est.</span><span class="sxs-lookup"><span data-stu-id="cddfe-133">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="cddfe-134">Go to the `src/components` directory and open `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="cddfe-134">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="cddfe-135">Recherchez `render()` la fonction et collez votre contenu à l’intérieur `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="cddfe-135">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="cddfe-136">Ajoutez la règle suivante pour faciliter la lecture des liens de courrier, quel que `App.css` soit le thème utilisé.</span><span class="sxs-lookup"><span data-stu-id="cddfe-136">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="cddfe-137">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="cddfe-137">Save your changes.</span></span> <span data-ttu-id="cddfe-138">Go to your app’s tab in Teams to view the new content.</span><span class="sxs-lookup"><span data-stu-id="cddfe-138">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Capture d’écran d’un onglet personnel avec du contenu statique.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="cddfe-140">3. Mettre à jour le thème de l’onglet</span><span class="sxs-lookup"><span data-stu-id="cddfe-140">3. Update the tab theme</span></span>

<span data-ttu-id="cddfe-141">Les bonnes applications sont natives de Teams. Il est donc important que votre onglet se fonde avec le thème Teams préféré de vos utilisateurs : par défaut (clair), foncé ou à contraste élevé.</span><span class="sxs-lookup"><span data-stu-id="cddfe-141">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="cddfe-142">Comme vous l’avez peut-être remarqué dans la dernière capture d’écran, votre onglet a toujours un arrière-plan clair lorsque le client utilise le thème foncé.</span><span class="sxs-lookup"><span data-stu-id="cddfe-142">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="cddfe-143">Il ne s’agit pas d’une expérience utilisateur recommandée.</span><span class="sxs-lookup"><span data-stu-id="cddfe-143">This is not a recommended user experience.</span></span>

<span data-ttu-id="cddfe-144">Le [SDK client JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) teams peut rendre votre application sensible aux modifications de thème dans le client et y réagir.</span><span class="sxs-lookup"><span data-stu-id="cddfe-144">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="cddfe-145">Examinons comment faire.</span><span class="sxs-lookup"><span data-stu-id="cddfe-145">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="cddfe-146">Obtenir du contexte sur le client Teams</span><span class="sxs-lookup"><span data-stu-id="cddfe-146">Get context about the Teams client</span></span>

<span data-ttu-id="cddfe-147">Dans votre fichier, il existe un appel qui fournit des informations sur, entre autres, le `Tab.js` `microsoftTeams.getContext()` thème client [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) configuré.</span><span class="sxs-lookup"><span data-stu-id="cddfe-147">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="cddfe-148">Grâce à la échafaudage de l’application, utilisez ce code tel qu’il est pour accéder à `context` l’interface et à ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="cddfe-148">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="cddfe-149">Créer un handler de modification de thème</span><span class="sxs-lookup"><span data-stu-id="cddfe-149">Create a theme change handler</span></span>

<span data-ttu-id="cddfe-150">Avec les propriétés en main, votre application a une bonne compréhension de ce qui se passe `context` autour de lui dans Teams.</span><span class="sxs-lookup"><span data-stu-id="cddfe-150">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="cddfe-151">Toutefois, l’application ne sait toujours pas que son apparence doit refléter le thème choisi par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cddfe-151">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="cddfe-152">Vous avez besoin d’un handler pour que l’état de votre application change avec le thème.</span><span class="sxs-lookup"><span data-stu-id="cddfe-152">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="cddfe-153">Insérez le handler de modification de thème suivant immédiatement après `microsoftTeams.getContext()` l’appel.</span><span class="sxs-lookup"><span data-stu-id="cddfe-153">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="cddfe-154">Faire correspondre les styles de thème</span><span class="sxs-lookup"><span data-stu-id="cddfe-154">Match theme styles</span></span>

<span data-ttu-id="cddfe-155">Votre responsable des modifications de thème est en place, mais vous avez besoin d’un code qui répond à ces modifications et aligne les couleurs de votre onglet sur le thème actuel.</span><span class="sxs-lookup"><span data-stu-id="cddfe-155">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="cddfe-156">L’exemple suivant est simplement une façon d’appliquer des styles à votre onglet. Utilisez le code tel qu’il est, développez-le ou écrivez le vôtre.</span><span class="sxs-lookup"><span data-stu-id="cddfe-156">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="cddfe-157">Dans la `render()` fonction, stockez l’état fourni par le handler de modification de thème dans `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="cddfe-157">In the `render()` function, store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="cddfe-158">Après avoir stocké l’état fourni par le handler de modification de thème, fournissez une logique conditionnelle pour restituer les styles de votre onglet en fonction du thème actuel.</span><span class="sxs-lookup"><span data-stu-id="cddfe-158">After storing the state provided by the theme change handler, provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="cddfe-159">L’exemple suivant montre une façon de faire de base :</span><span class="sxs-lookup"><span data-stu-id="cddfe-159">The following example shows a basic way to do this:</span></span>
1. <span data-ttu-id="cddfe-160">Vérifiez le thème actuel dans `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="cddfe-160">Check the current theme in `isTheme`.</span></span>
2. <span data-ttu-id="cddfe-161">Créez `newTheme` un objet avec des propriétés CSS pertinentes pour le thème actuel.</span><span class="sxs-lookup"><span data-stu-id="cddfe-161">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
3. <span data-ttu-id="cddfe-162">Appliquez la CSS à l’élément HTML racine de votre onglet ( `<div>` ).</span><span class="sxs-lookup"><span data-stu-id="cddfe-162">Apply the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="cddfe-163">Vérifiez votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="cddfe-163">Check your tab in Teams.</span></span> <span data-ttu-id="cddfe-164">L’apparence doit correspondre étroitement au thème foncé.</span><span class="sxs-lookup"><span data-stu-id="cddfe-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Capture d’écran d’un onglet personnel avec affichage de contenu statique.":::

## <a name="well-done"></a><span data-ttu-id="cddfe-166">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="cddfe-166">Well done</span></span>

<span data-ttu-id="cddfe-167">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="cddfe-167">Congratulations!</span></span> <span data-ttu-id="cddfe-168">Vous avez une application Teams avec un onglet personnel qui facilite la recherche de contacts importants dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="cddfe-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="cddfe-169">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="cddfe-169">Learn more</span></span>

* <span data-ttu-id="cddfe-170">[](../tabs/how-to/authentication/auth-aad-sso.md)Authentifier les utilisateurs d’onglets avec l’authentification unique : si vous souhaitez uniquement que les utilisateurs autorisés l’affichent, configurer l’authentification unique (SSO) via Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="cddfe-170">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="cddfe-171">[Incorporer du contenu](../tabs/how-to/tab-requirements.md)à partir d’une application web ou d’une page web existante : nous vous avons montré comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="cddfe-171">[Embed content from an existing web app or webpage](../tabs/how-to/tab-requirements.md): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="cddfe-172">[Créez une expérience transparente pour votre onglet](../tabs/design/tabs.md): consultez les recommandations pour concevoir des onglets Teams.</span><span class="sxs-lookup"><span data-stu-id="cddfe-172">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="cddfe-173">[Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): comprendre comment développer des onglets pour téléphones et tablettes.</span><span class="sxs-lookup"><span data-stu-id="cddfe-173">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="cddfe-174">Utiliser les données Teams avec Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="cddfe-174">Utilize Teams data with Microsoft Graph</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="cddfe-175">Créer un onglet sans le kit de ressources</span><span class="sxs-lookup"><span data-stu-id="cddfe-175">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a><span data-ttu-id="cddfe-176">Leçon suivante</span><span class="sxs-lookup"><span data-stu-id="cddfe-176">Next lesson</span></span>

<span data-ttu-id="cddfe-177">Vous savez comment créer un onglet pour une utilisation personnelle.</span><span class="sxs-lookup"><span data-stu-id="cddfe-177">You know how to build a tab for personal use.</span></span> <span data-ttu-id="cddfe-178">Examinons ce qu’il faut pour créer un onglet pour les canaux d’équipe et les conversations.</span><span class="sxs-lookup"><span data-stu-id="cddfe-178">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cddfe-179">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="cddfe-179">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
