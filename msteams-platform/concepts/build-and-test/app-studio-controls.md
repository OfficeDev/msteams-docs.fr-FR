---
title: Utilisation de la bibliothèque de contrôles
description: Utilisation de la bibliothèque de contrôles fournie par Microsoft teams App Studio
keywords: Bibliothèque de contrôle Team App Studio
ms.openlocfilehash: d817f55bd75216f77375b7848c5c32cbd29304c2
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673659"
---
# <a name="using-the-control-library-in-app-studio"></a><span data-ttu-id="02d25-104">Utilisation de la bibliothèque de contrôles dans App Studio</span><span class="sxs-lookup"><span data-stu-id="02d25-104">Using the control library in App Studio</span></span>

<span data-ttu-id="02d25-105">[Microsoft teams App Studio](~/get-started/get-started-app-studio.md) fournit un ensemble de contrôles que vous pouvez utiliser dans vos propres applications.</span><span class="sxs-lookup"><span data-stu-id="02d25-105">[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md) provides you with a set of controls that you can use in your own apps.</span></span> <span data-ttu-id="02d25-106">Ces contrôles sont fournis dans l’onglet *bibliothèque de contrôles* d’App Studio.</span><span class="sxs-lookup"><span data-stu-id="02d25-106">These controls are provided in the *Control Library* tab of App Studio.</span></span>

<span data-ttu-id="02d25-107">Ces contrôles ont été créés par les concepteurs Microsoft teams afin de rationaliser leurs propres flux de travail, de normaliser le comportement et les thèmes par défaut de l’équipe de support technique.</span><span class="sxs-lookup"><span data-stu-id="02d25-107">These controls were created by the Microsoft Teams designers to streamline their own workflows, standardize control behavior and support Team's default themes.</span></span> <span data-ttu-id="02d25-108">Vous pouvez utiliser cette bibliothèque dans vos propres applications pour obtenir une apparence unifiée.</span><span class="sxs-lookup"><span data-stu-id="02d25-108">You can use this library in your own apps to achieve a unified look and feel.</span></span>

<span data-ttu-id="02d25-109">Les contrôles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="02d25-109">Controls include:</span></span>

* <span data-ttu-id="02d25-110">Boutons</span><span class="sxs-lookup"><span data-stu-id="02d25-110">Buttons</span></span>
* <span data-ttu-id="02d25-111">Listes déroulantes</span><span class="sxs-lookup"><span data-stu-id="02d25-111">Dropdowns</span></span>
* <span data-ttu-id="02d25-112">Cases à cocher</span><span class="sxs-lookup"><span data-stu-id="02d25-112">Checkboxes</span></span>
* <span data-ttu-id="02d25-113">Cases d’option</span><span class="sxs-lookup"><span data-stu-id="02d25-113">Radio Buttons</span></span>
* <span data-ttu-id="02d25-114">Inverser</span><span class="sxs-lookup"><span data-stu-id="02d25-114">Toggles</span></span>
* <span data-ttu-id="02d25-115">Zones de test</span><span class="sxs-lookup"><span data-stu-id="02d25-115">Test Areas</span></span>
* <span data-ttu-id="02d25-116">Liens</span><span class="sxs-lookup"><span data-stu-id="02d25-116">Links</span></span>
* <span data-ttu-id="02d25-117">Onglets</span><span class="sxs-lookup"><span data-stu-id="02d25-117">Tabs</span></span>
* <span data-ttu-id="02d25-118">Tables</span><span class="sxs-lookup"><span data-stu-id="02d25-118">Tables</span></span>
* <span data-ttu-id="02d25-119">Icônes</span><span class="sxs-lookup"><span data-stu-id="02d25-119">Icons</span></span>

## <a name="optionally-use-react-controls"></a><span data-ttu-id="02d25-120">Utiliser éventuellement des contrôles REACT</span><span class="sxs-lookup"><span data-stu-id="02d25-120">Optionally use React controls</span></span>

<span data-ttu-id="02d25-121">La bibliothèque de contrôles complète teams utilise l' [infrastructure d’interface utilisateur JavaScript REACT](https://reactjs.org/) , mais elle est conçue de sorte qu’elle ne soit pas liée à une infrastructure d’interface utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="02d25-121">The full Teams control library uses the [React JavaScript UI framework](https://reactjs.org/) however it is built so that it is not tied to a specific UI framework.</span></span> <span data-ttu-id="02d25-122">Il existe quatre packages NPM :</span><span class="sxs-lookup"><span data-stu-id="02d25-122">There are four different npm packages:</span></span>

* <span data-ttu-id="02d25-123">**msteams-UI-styles-Core** Les principaux styles CSS des composants de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="02d25-123">**msteams-ui-styles-core** The core CSS styles of UI components.</span></span> <span data-ttu-id="02d25-124">Il est indépendant de toute infrastructure d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="02d25-124">It’s independent of any UI framework.</span></span>
* <span data-ttu-id="02d25-125">**msteams-UI-Icons-Core** Ensemble d’icônes principales de teams.</span><span class="sxs-lookup"><span data-stu-id="02d25-125">**msteams-ui-icons-core** The core set of Teams icons.</span></span>
* <span data-ttu-id="02d25-126">**msteams-UI-Components-REACT** Bibliothèque de liaison REACT.</span><span class="sxs-lookup"><span data-stu-id="02d25-126">**msteams-ui-components-react** The React binding library.</span></span> <span data-ttu-id="02d25-127">Cela dépend de msteams-UI-styles-Core.</span><span class="sxs-lookup"><span data-stu-id="02d25-127">It depends on msteams-ui-styles-core.</span></span>
* <span data-ttu-id="02d25-128">**msteams-UI-Icons-REACT** Bibliothèque de liaison REACT pour l’ensemble des icônes Teams.</span><span class="sxs-lookup"><span data-stu-id="02d25-128">**msteams-ui-icons-react** The React binding library for the set of Teams icons.</span></span> <span data-ttu-id="02d25-129">Cela dépend de msteams-UI-Icons-Core.</span><span class="sxs-lookup"><span data-stu-id="02d25-129">It depends on msteams-ui-icons-core.</span></span>

<span data-ttu-id="02d25-130">Ces bibliothèques sont toutes Open source et vous pouvez utiliser msteams-UI-styles-Core et msteams-UI-Icons sans REACT.</span><span class="sxs-lookup"><span data-stu-id="02d25-130">These libraries are all open source, and you can use msteams-ui-styles-core and msteams-ui-icons-core without React.</span></span>

## <a name="adding-the-control-library"></a><span data-ttu-id="02d25-131">Ajout de la bibliothèque de contrôles</span><span class="sxs-lookup"><span data-stu-id="02d25-131">Adding the control library</span></span>

<span data-ttu-id="02d25-132">Installez la bibliothèque de contrôles et sa dépendance `typestyle`d’homologue :</span><span class="sxs-lookup"><span data-stu-id="02d25-132">Install the control library and its peer dependency `typestyle`:</span></span>

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

<span data-ttu-id="02d25-133">*Facultatif :* Installez les icônes Teams.</span><span class="sxs-lookup"><span data-stu-id="02d25-133">*Optional:* Install the Teams icons.</span></span>

```terminal
npm install --save msteams-ui-icons-react
```

<span data-ttu-id="02d25-134">`src/App.js` Recherchez et remplacez son contenu par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="02d25-134">Find and open `src/App.js` and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, PrimaryButton } from ‘msteams-ui-components-react’

class App extends Component {
   render() {
      // Sets up the top-level context for the library. It accepts global
      // configurations such as font size and theme. fontSize is your page’s
      // default font size. We made it a parameter so that you could use this
      // library with CSS frameworks such as Bootstrap. Some CSS frameworks
      // set the default font size for the page; retrieve it and use it
      // instead of {16} in the block.
      // This library uses the power of CSS to do most of the work for you.
      // Instead of passing themes as a parameter to every UI component,
      // we set it on a parent HTML element. All HTML elements nested within
      // that parent will inherit these properties.

      return (
        <TeamsComponentContext
            fontSize={16}
            theme={ThemeStyle.Light}
        />
      );
   }
}
export default App;
```

<span data-ttu-id="02d25-135">Exécution de l’application</span><span class="sxs-lookup"><span data-stu-id="02d25-135">Run the app</span></span>

```terminal
npm run start
```

<span data-ttu-id="02d25-136">Lorsque vous accédez à http://localhost:3000, l’écran suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="02d25-136">When you navigate to http://localhost:3000, you should see the following screen:</span></span>

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="Bouton bibliothèque de contrôles"/>

## <a name="dynamically-handling-theme-changes"></a><span data-ttu-id="02d25-138">Gestion dynamique des modifications de thème</span><span class="sxs-lookup"><span data-stu-id="02d25-138">Dynamically handling theme changes</span></span>

<span data-ttu-id="02d25-139">Votre application doit gérer les thèmes lorsque :</span><span class="sxs-lookup"><span data-stu-id="02d25-139">Your app needs to handle themes when:</span></span>

* <span data-ttu-id="02d25-140">L’onglet est initialement chargé</span><span class="sxs-lookup"><span data-stu-id="02d25-140">The tab is initially loaded</span></span>
* <span data-ttu-id="02d25-141">Un utilisateur modifie le thème une fois que l’onglet est déjà chargé</span><span class="sxs-lookup"><span data-stu-id="02d25-141">A user changes the theme after the tab is already loaded</span></span>

<span data-ttu-id="02d25-142">Le thème est inclus dans le [contexte](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)d’un onglet, qui peut être récupéré avant le chargement de l’onglet via les valeurs d’espace réservé d’URL, ou à tout moment à l’aide du [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/%40microsoft/teams-js/context).</span><span class="sxs-lookup"><span data-stu-id="02d25-142">The theme is included in a tab’s [Context](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest), which can be retrieved before the tab is loaded via URL placeholder values, or at any time by using the [Microsoft Teams JavaScript client SDK](/javascript/api/%40microsoft/teams-js/context).</span></span>

<span data-ttu-id="02d25-143">La manière dont le thème actuel est récupéré et comment répondre aux modifications de thème est abordée ici : [obtenir le contexte de votre onglet Microsoft teams](~/concepts/tabs/tabs-context.md).</span><span class="sxs-lookup"><span data-stu-id="02d25-143">How the current theme is retrieved and how to respond to theme changes is discussed here: [Get context for your Microsoft Teams tab](~/concepts/tabs/tabs-context.md).</span></span>

<span data-ttu-id="02d25-144">Cet exemple de code montre comment procéder.</span><span class="sxs-lookup"><span data-stu-id="02d25-144">This sample code shows how this is done.</span></span>

```js
componentWillMount() {
    // If you are deploying your site as a MS Teams static or configurable tab,
    // you should add “?theme={theme}” to your tabs URL in the manifest.
    // That way you will get the current theme before it’s loaded; getContext()
    // is called only after the tab is loaded, which will cause the tab to flash
    // if the current theme is different than the default.
    this.updateTheme(this.getQueryVariable('theme'));
    this.setState({
        fontSize: this.pageFontSize(),
    });

    // If you are not using the MS Teams Javascript SDK, you can remove this entire
    // if block, but if you want theme changes in the MS Teams client to propagate
    // to the tab, leave it here.
    microsoftTeams.initialize();
    microsoftTeams.registerOnThemeChangeHandler(this.updateTheme);
}
```

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a><span data-ttu-id="02d25-145">Connecter votre propre composant au TeamsComponentContext</span><span class="sxs-lookup"><span data-stu-id="02d25-145">Connect your own component to the TeamsComponentContext</span></span>

<span data-ttu-id="02d25-146">Si vous souhaitez utiliser votre propre code CSS, vous pouvez toujours répondre aux modifications de thème et utiliser les couleurs définies par Teams.</span><span class="sxs-lookup"><span data-stu-id="02d25-146">If you want to use your own CSS code you can still respond to theme changes and use colors defined by teams.</span></span> <span data-ttu-id="02d25-147">TeamsComponentContext vous permet de le faire.</span><span class="sxs-lookup"><span data-stu-id="02d25-147">TeamsComponentContext allows you to do this.</span></span>

<span data-ttu-id="02d25-148">Une fois encore, modifiez `src/App.js` votre fichier et remplacez son contenu par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="02d25-148">Once again, edit your `src/App.js` file and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, ConnectedComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponent extends Component {
    render() {
        return (
            <ConnectedComponent render={(props) => {
                const context = props.context;

                switch (context.style) {
                case ThemeStyle.Dark:
                    return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
                case ThemeStyle.HighContrast:
                    return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
                case ThemeStyle.Light:
                    return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
                }
            }} />
        );
    }
}

export default App;
```

<span data-ttu-id="02d25-149">Dans ce code, un nouveau composant est défini appelé MyComponent.</span><span class="sxs-lookup"><span data-stu-id="02d25-149">In this code, a new component is defined called MyComponent.</span></span> <span data-ttu-id="02d25-150">Un composant spécial de la bibliothèque de contrôles appelé ConnectedComponent est ensuite ajouté.</span><span class="sxs-lookup"><span data-stu-id="02d25-150">Then a special component from the control library called ConnectedComponent is added.</span></span> <span data-ttu-id="02d25-151">ConnectedComponent possède une propriété appelée `render` qui prend une fonction en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="02d25-151">ConnectedComponent has a property called `render` which takes a function as a parameter.</span></span> <span data-ttu-id="02d25-152">Au moment du rendu, cette fonction est appelée avec le contexte approprié pour votre onglet. Le contexte inclut le thème dans lequel la page est affichée, ainsi que l’objet de couleur globale que vous pouvez utiliser pour appliquer les couleurs de teams à votre onglet. Comme vous pouvez le voir dans `switch` l’instruction, l' `<div>` élément approprié est choisi en fonction du thème.</span><span class="sxs-lookup"><span data-stu-id="02d25-152">At render time this function will be called with the appropriate context for your tab. The context includes the theme that the page is being rendered in as well as the global color object that you can use to apply Teams colors to your tab. As you can see in the `switch` statement, the appropriate `<div>` is chosen based on the theme.</span></span>

<span data-ttu-id="02d25-153">Pour modifier les thèmes, nous devons transmettre au niveau racine TeamsComponentContext un autre thème.</span><span class="sxs-lookup"><span data-stu-id="02d25-153">To change themes, we need to pass the root-level TeamsComponentContext a different theme.</span></span> <span data-ttu-id="02d25-154">Lorsqu’un thème change, tous les éléments enfants encapsulés dans ConnectedComponent seront ré-rendus.</span><span class="sxs-lookup"><span data-stu-id="02d25-154">When a theme changes, all the child elements wrapped in ConnectedComponent will be re-rendered.</span></span> <span data-ttu-id="02d25-155">Voir la section précédente « gérer dynamiquement les modifications de thème ».</span><span class="sxs-lookup"><span data-stu-id="02d25-155">See previous section “Dynamically Handle Theme Changes.”</span></span>

<span data-ttu-id="02d25-156">Il existe d’autres façons de connecter votre composant à TeamsComponentContext.</span><span class="sxs-lookup"><span data-stu-id="02d25-156">There are other ways to connect your component to TeamsComponentContext.</span></span> <span data-ttu-id="02d25-157">Si vous êtes familiarisé avec [Redux](https://redux.js.org/basics/usage-with-react), vous pouvez préférer le modèle suivant :</span><span class="sxs-lookup"><span data-stu-id="02d25-157">If you’re familiar with [Redux](https://redux.js.org/basics/usage-with-react), you may prefer the following pattern:</span></span>

```js
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, connectTeamsComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponentInner extends Component {
    render() {
        const context = this.props.context;
        switch (context.style) {
            case ThemeStyle.Dark:
                return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
            case ThemeStyle.HighContrast:
                return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
            case ThemeStyle.Light:
                return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
        }
    }
}

const MyComponent = connectTeamsComponent(MyComponentInner);

export default App;
```

<span data-ttu-id="02d25-158">Dans cette méthode, au lieu d’utiliser ConnectedComponent, vous utilisez la fonction connectTeamsComponent.</span><span class="sxs-lookup"><span data-stu-id="02d25-158">In this method, instead of using ConnectedComponent, you use the connectTeamsComponent function.</span></span> <span data-ttu-id="02d25-159">La fonction connectTeamsComponent prend votre composant actuel et renvoie un nouveau composant avec l’objet Context injecté.</span><span class="sxs-lookup"><span data-stu-id="02d25-159">The connectTeamsComponent function takes your current component and returns a new component with the context object injected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02d25-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02d25-160">Next steps</span></span>

<span data-ttu-id="02d25-161">Dirigez Team App Studio et découvrez tous les contrôles que nous proposons et un exemple de code expliquant comment les utiliser.</span><span class="sxs-lookup"><span data-stu-id="02d25-161">Head to Teams App Studio and check out all the controls we offer and sample code of how to use them.</span></span> <span data-ttu-id="02d25-162">N’oubliez pas de les explorer dans différents thèmes.</span><span class="sxs-lookup"><span data-stu-id="02d25-162">Don’t forget to explore them in different themes.</span></span>