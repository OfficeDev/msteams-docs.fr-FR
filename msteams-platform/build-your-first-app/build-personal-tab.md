---
title: Prise en main-créer un onglet personnel
author: heath-hamilton
description: Créez rapidement un onglet personnel Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 7c12c87fff5126662f9473ecb0c5838b61f5faf2
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452742"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="c3e9d-103">Créer un onglet personnel pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="c3e9d-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="c3e9d-104">Les onglets permettent d’exposer facilement du contenu dans votre application en incorporant essentiellement une page Web dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="c3e9d-105">Il existe deux types d’onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="c3e9d-106">Dans ce didacticiel, vous allez créer un *onglet personnel*, une page de contenu en plein écran pour les utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="c3e9d-107">(Les onglets personnels sont les plus proches de l’expérience d’un site Web classique dans Teams.)</span><span class="sxs-lookup"><span data-stu-id="c3e9d-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c3e9d-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c3e9d-108">Before you begin</span></span>

<span data-ttu-id="c3e9d-109">Vous avez besoin d’un onglet personnel de base pour commencer.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="c3e9d-110">Si vous n’en avez pas, reportez-vous à [la rubrique générer et exécuter votre première application teams](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="c3e9d-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="c3e9d-111">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="c3e9d-111">Your assignment</span></span>

<span data-ttu-id="c3e9d-112">Les personnes de votre organisation ont des difficultés à trouver des informations de contact de base pour des fonctions importantes (support technique, RH, etc.).</span><span class="sxs-lookup"><span data-stu-id="c3e9d-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="c3e9d-113">Vous êtes chargé de vous assurer qu’ils peuvent rapidement trouver ces informations à un seul endroit.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="c3e9d-114">Comment procéder ?</span><span class="sxs-lookup"><span data-stu-id="c3e9d-114">How would you do that?</span></span> <span data-ttu-id="c3e9d-115">Onglet personnel Teams, bien sûr.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c3e9d-116">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="c3e9d-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="c3e9d-117">Identifier certaines des propriétés de manifeste de l’application et la structure correspondant aux onglets personnels</span><span class="sxs-lookup"><span data-stu-id="c3e9d-117">Identify some of the app manifest properties and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="c3e9d-118">Créer un contenu de tabulation</span><span class="sxs-lookup"><span data-stu-id="c3e9d-118">Create tab content</span></span>
> * <span data-ttu-id="c3e9d-119">Mettre à jour le thème de couleurs d’un onglet en fonction de la préférence de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c3e9d-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="c3e9d-120">1. identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="c3e9d-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="c3e9d-121">La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-121">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="c3e9d-122">Examinons les principaux composants de création d’un onglet personnel.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="c3e9d-123">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="c3e9d-123">App manifest</span></span>

<span data-ttu-id="c3e9d-124">L’extrait de code suivant du manifeste de l’application (le `manifest.json` fichier dans le répertoire de votre projet `.publish` ) affiche [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , qui inclut les propriétés et les valeurs par défaut relatives aux onglets personnels.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-124">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which includes properties and default values relevant to personal tabs.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "Personal Tab",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

* <span data-ttu-id="c3e9d-125">`entityId`: Identificateur unique de la page affichée par l’onglet.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-125">`entityId`: A unique identifier for the page displayed by the tab.</span></span>
* <span data-ttu-id="c3e9d-126">`name`: Le nom complet de l’onglet (par exemple, « mes contacts »).</span><span class="sxs-lookup"><span data-stu-id="c3e9d-126">`name`: The tab's display name (for example, "My Contacts").</span></span>
* <span data-ttu-id="c3e9d-127">`contentUrl`: URL de l’hôte la page de contenu de l’onglet (doit être HTTPs).</span><span class="sxs-lookup"><span data-stu-id="c3e9d-127">`contentUrl`: The host URL the tab content page (must be HTTPS).</span></span>
* <span data-ttu-id="c3e9d-128">`scopes`: Spécifie que l’onglet est réservé à un usage personnel.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-128">`scopes`: Specifies the tab is for personal use only.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="c3e9d-129">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="c3e9d-129">App scaffolding</span></span>

<span data-ttu-id="c3e9d-130">Le échafaudage de l’application fournit les composants pour le rendu de votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-130">The app scaffolding provides the components for rendering your tab in Teams.</span></span> <span data-ttu-id="c3e9d-131">Vous pouvez utiliser un grand nombre de choses, mais pour le moment, il vous suffit de vous concentrer sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c3e9d-131">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="c3e9d-132">`Tab.js` fichier dans le `src/components` Répertoire de votre projet</span><span class="sxs-lookup"><span data-stu-id="c3e9d-132">`Tab.js` file in the `src/components` directory of your project</span></span>
* <span data-ttu-id="c3e9d-133">Kit de développement logiciel (SDK) JavaScript de Microsoft Teams, qui est préinstallé dans les composants frontaux de votre projet</span><span class="sxs-lookup"><span data-stu-id="c3e9d-133">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="c3e9d-134">2. personnaliser votre page de contenu d’onglet</span><span class="sxs-lookup"><span data-stu-id="c3e9d-134">2. Customize your tab content page</span></span>

<span data-ttu-id="c3e9d-135">Compilez une liste de contacts importants dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-135">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="c3e9d-136">Copiez et mettez à jour l’extrait de code suivant avec les informations qui vous concernent ou, pour des raisons de temps, utilisez le code tel quel.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-136">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="c3e9d-137">Accédez au `src/components` répertoire et ouvrez `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="c3e9d-137">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="c3e9d-138">Recherchez la `render()` fonction et collez votre contenu dans `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="c3e9d-138">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="c3e9d-139">Ajoutez la règle suivante pour `App.css` que les liens électroniques soient plus faciles à lire quel que soit le thème utilisé.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-139">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="c3e9d-140">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-140">Save your changes.</span></span> <span data-ttu-id="c3e9d-141">Accédez à l’onglet de votre application dans teams pour afficher le nouveau contenu.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-141">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Capture d’écran d’un onglet personnel avec du contenu statique.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="c3e9d-143">3. mettre à jour le thème de l’onglet</span><span class="sxs-lookup"><span data-stu-id="c3e9d-143">3. Update the tab theme</span></span>

<span data-ttu-id="c3e9d-144">Les applications intéressantes semblent natives pour Teams, c’est pourquoi il est important que votre onglet se mélange avec le thème des équipes que vos utilisateurs préfèrent : par défaut (clair), foncé ou contraste élevé.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-144">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="c3e9d-145">Comme vous avez pu le remarquer dans la dernière capture d’écran, votre onglet présente toujours un arrière-plan clair lorsque le client utilise le thème foncé.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-145">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="c3e9d-146">Il ne s’agit pas d’une expérience utilisateur recommandée.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-146">This is not a recommended user experience.</span></span>

<span data-ttu-id="c3e9d-147">Le [Kit de développement logiciel (SDK) du client JavaScript teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) permet à votre application de prendre en compte les modifications apportées au thème dans le client.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-147">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="c3e9d-148">Passons en revue la procédure.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-148">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="c3e9d-149">Obtenir un contexte sur le client teams</span><span class="sxs-lookup"><span data-stu-id="c3e9d-149">Get context about the Teams client</span></span>

<span data-ttu-id="c3e9d-150">Dans votre `Tab.js` fichier, il existe un `microsoftTeams.getContext()` appel qui fournit des [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) informations sur le thème client configuré, entre autres.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-150">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="c3e9d-151">Grâce à la génération de modèles automatique d’application, utilisez ce code en tant que pour accéder à l' `context` interface et à ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-151">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="c3e9d-152">Créer un gestionnaire de modification de thème</span><span class="sxs-lookup"><span data-stu-id="c3e9d-152">Create a theme change handler</span></span>

<span data-ttu-id="c3e9d-153">Avec les `context` Propriétés en main, votre application a une bonne compréhension de ce qui se passe dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-153">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="c3e9d-154">Toutefois, l’application ne connaît toujours pas son apparence doit refléter le thème choisi par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-154">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="c3e9d-155">Vous avez besoin d’un gestionnaire pour que l’état de votre application change avec le thème.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-155">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="c3e9d-156">Insérez le gestionnaire de modifications de thème suivant immédiatement après l' `microsoftTeams.getContext()` appel.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-156">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="c3e9d-157">Correspondance des styles de thème</span><span class="sxs-lookup"><span data-stu-id="c3e9d-157">Match theme styles</span></span>

<span data-ttu-id="c3e9d-158">Votre gestionnaire de modifications de thème est en place, mais vous avez besoin de code qui répond à ces modifications et aligne les couleurs de votre onglet sur le thème actuel.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-158">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="c3e9d-159">Dans l’exemple suivant, vous pouvez appliquer des styles à votre onglet. Utilisez le code tel quel, développez-le ou rédigez-le.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-159">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="c3e9d-160">Stockez l’état fourni par le gestionnaire de modifications de thème dans `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="c3e9d-160">Store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="c3e9d-161">Fournissez une logique conditionnelle pour afficher les styles de votre onglet en fonction du thème actuel.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-161">Provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="c3e9d-162">L’exemple suivant montre une méthode de base pour effectuer cette opération par 1) en vérifiant le thème actuel dans `isTheme` , 2) en créant un `newTheme` objet avec des propriétés CSS pertinentes pour le thème actuel et 3) en appliquant la feuille de style CSS à l’élément HTML racine de votre contenu d’onglet ( `<div>` ).</span><span class="sxs-lookup"><span data-stu-id="c3e9d-162">The following example shows a basic way to do this by 1) checking the current theme in `isTheme`, 2) creating a `newTheme` object with CSS properties relevant to the current theme, and 3) applying the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="c3e9d-163">Vérifiez l’onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-163">Check your tab in Teams.</span></span> <span data-ttu-id="c3e9d-164">L’apparence doit correspondre au thème foncé.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Capture d’écran d’un onglet personnel avec du contenu statique.":::

## <a name="well-done"></a><span data-ttu-id="c3e9d-166">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="c3e9d-166">Well done</span></span>

<span data-ttu-id="c3e9d-167">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="c3e9d-167">Congratulations!</span></span> <span data-ttu-id="c3e9d-168">Vous disposez d’une application teams avec un onglet personnel qui facilite la recherche de contacts importants dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="c3e9d-169">Si vous souhaitez en savoir plus</span><span class="sxs-lookup"><span data-stu-id="c3e9d-169">Learn more</span></span>

* <span data-ttu-id="c3e9d-170">[Authentifier les utilisateurs avec l’authentification](../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="c3e9d-170">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="c3e9d-171">[Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-171">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="c3e9d-172">[Créez une expérience transparente pour votre onglet](../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-172">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="c3e9d-173">[Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour les téléphones et les tablettes.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-173">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="c3e9d-174">Intégration à l’API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c3e9d-174">Integrate with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="c3e9d-175">Créer un onglet sans la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="c3e9d-175">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="c3e9d-176">Leçon suivante</span><span class="sxs-lookup"><span data-stu-id="c3e9d-176">Next lesson</span></span>

<span data-ttu-id="c3e9d-177">Vous saurez comment créer un onglet pour une utilisation personnelle.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-177">You know how to build a tab for personal use.</span></span> <span data-ttu-id="c3e9d-178">Examinons ce qu’il faut faire pour créer un onglet pour les canaux d’équipe et les conversations.</span><span class="sxs-lookup"><span data-stu-id="c3e9d-178">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3e9d-179">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="c3e9d-179">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
