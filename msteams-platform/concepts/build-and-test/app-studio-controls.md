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
# <a name="using-the-control-library-in-app-studio"></a>Utilisation de la bibliothèque de contrôles dans App Studio

[Microsoft teams App Studio](~/get-started/get-started-app-studio.md) fournit un ensemble de contrôles que vous pouvez utiliser dans vos propres applications. Ces contrôles sont fournis dans l’onglet *bibliothèque de contrôles* d’App Studio.

Ces contrôles ont été créés par les concepteurs Microsoft teams afin de rationaliser leurs propres flux de travail, de normaliser le comportement et les thèmes par défaut de l’équipe de support technique. Vous pouvez utiliser cette bibliothèque dans vos propres applications pour obtenir une apparence unifiée.

Les contrôles sont les suivants :

* Boutons
* Listes déroulantes
* Cases à cocher
* Cases d’option
* Inverser
* Zones de test
* Liens
* Onglets
* Tables
* Icônes

## <a name="optionally-use-react-controls"></a>Utiliser éventuellement des contrôles REACT

La bibliothèque de contrôles complète teams utilise l' [infrastructure d’interface utilisateur JavaScript REACT](https://reactjs.org/) , mais elle est conçue de sorte qu’elle ne soit pas liée à une infrastructure d’interface utilisateur spécifique. Il existe quatre packages NPM :

* **msteams-UI-styles-Core** Les principaux styles CSS des composants de l’interface utilisateur. Il est indépendant de toute infrastructure d’interface utilisateur.
* **msteams-UI-Icons-Core** Ensemble d’icônes principales de teams.
* **msteams-UI-Components-REACT** Bibliothèque de liaison REACT. Cela dépend de msteams-UI-styles-Core.
* **msteams-UI-Icons-REACT** Bibliothèque de liaison REACT pour l’ensemble des icônes Teams. Cela dépend de msteams-UI-Icons-Core.

Ces bibliothèques sont toutes Open source et vous pouvez utiliser msteams-UI-styles-Core et msteams-UI-Icons sans REACT.

## <a name="adding-the-control-library"></a>Ajout de la bibliothèque de contrôles

Installez la bibliothèque de contrôles et sa dépendance `typestyle`d’homologue :

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

*Facultatif :* Installez les icônes Teams.

```terminal
npm install --save msteams-ui-icons-react
```

`src/App.js` Recherchez et remplacez son contenu par le code suivant :

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

Exécution de l’application

```terminal
npm run start
```

Lorsque vous accédez à http://localhost:3000, l’écran suivant s’affiche :

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="Bouton bibliothèque de contrôles"/>

## <a name="dynamically-handling-theme-changes"></a>Gestion dynamique des modifications de thème

Votre application doit gérer les thèmes lorsque :

* L’onglet est initialement chargé
* Un utilisateur modifie le thème une fois que l’onglet est déjà chargé

Le thème est inclus dans le [contexte](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)d’un onglet, qui peut être récupéré avant le chargement de l’onglet via les valeurs d’espace réservé d’URL, ou à tout moment à l’aide du [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/%40microsoft/teams-js/context).

La manière dont le thème actuel est récupéré et comment répondre aux modifications de thème est abordée ici : [obtenir le contexte de votre onglet Microsoft teams](~/concepts/tabs/tabs-context.md).

Cet exemple de code montre comment procéder.

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

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a>Connecter votre propre composant au TeamsComponentContext

Si vous souhaitez utiliser votre propre code CSS, vous pouvez toujours répondre aux modifications de thème et utiliser les couleurs définies par Teams. TeamsComponentContext vous permet de le faire.

Une fois encore, modifiez `src/App.js` votre fichier et remplacez son contenu par le code suivant :

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

Dans ce code, un nouveau composant est défini appelé MyComponent. Un composant spécial de la bibliothèque de contrôles appelé ConnectedComponent est ensuite ajouté. ConnectedComponent possède une propriété appelée `render` qui prend une fonction en tant que paramètre. Au moment du rendu, cette fonction est appelée avec le contexte approprié pour votre onglet. Le contexte inclut le thème dans lequel la page est affichée, ainsi que l’objet de couleur globale que vous pouvez utiliser pour appliquer les couleurs de teams à votre onglet. Comme vous pouvez le voir dans `switch` l’instruction, l' `<div>` élément approprié est choisi en fonction du thème.

Pour modifier les thèmes, nous devons transmettre au niveau racine TeamsComponentContext un autre thème. Lorsqu’un thème change, tous les éléments enfants encapsulés dans ConnectedComponent seront ré-rendus. Voir la section précédente « gérer dynamiquement les modifications de thème ».

Il existe d’autres façons de connecter votre composant à TeamsComponentContext. Si vous êtes familiarisé avec [Redux](https://redux.js.org/basics/usage-with-react), vous pouvez préférer le modèle suivant :

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

Dans cette méthode, au lieu d’utiliser ConnectedComponent, vous utilisez la fonction connectTeamsComponent. La fonction connectTeamsComponent prend votre composant actuel et renvoie un nouveau composant avec l’objet Context injecté.

## <a name="next-steps"></a>Étapes suivantes

Dirigez Team App Studio et découvrez tous les contrôles que nous proposons et un exemple de code expliquant comment les utiliser. N’oubliez pas de les explorer dans différents thèmes.