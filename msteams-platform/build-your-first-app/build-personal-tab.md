---
title: Get started - Build a personal tab
author: girliemac
description: Créez rapidement un onglet personnel Microsoft Teams à l'aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: timura
ms.date: 03/16/2020
ms.topic: tutorial
ms.openlocfilehash: 05ef9913e338a54c7e6ebc301825b27d4bec9705
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068580"
---
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a>Créer un onglet personnel de base pour Microsoft Teams

Ce didacticiel vous apprend à créer un onglet personnel de base dans Microsoft Teams. Les onglets sont un moyen simple pour faire surface des informations dans votre application en hébergeant du contenu web dans Teams. Les onglets sont une fonctionnalité courante des applications personnelles qui fournissent un espace de travail privé pour des utilisateurs individuels. Les onglets personnels sont les plus proches d'une expérience web traditionnelle dans Teams. 

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

* Comprendre les configurations d'application et la échafaudage pertinentes pour les onglets personnels.
* Créez un contenu d'onglet avec une liste de contacts de votre organisation.
* Mettez à jour le thème de couleur d'un onglet en fonction des préférences de l'utilisateur.

## <a name="prerequisites"></a>Prerequisites

Assurez-vous que vous comprenez comment configurer et créer une application Teams simple. Pour plus d'informations, voir [créer votre première application Microsoft Teams « Hello, World!](../build-your-first-app/build-and-run.md)».

## <a name="1-understand-your-app-project-components"></a>1. Comprendre les composants de votre projet d'application

Une fois que vous avez créé un onglet personnel de base, la modèle d'application générée fournit les composants pour le rendu de votre onglet personnel dans Teams. Vous pouvez travailler avec beaucoup de choses, mais pour l'instant, laissez-nous nous concentrer sur les questions suivantes : 

* `Tab.js` dans le `src/components` répertoire de votre projet. Il s'agit du rendu de la page de contenu de votre onglet.
* Microsoft Teams JavaScript client SDK, qui est pré-chargé dans les composants frontaux de votre projet.

Comme vous pouvez le constater dans la section en haut du fichier, l'exemple de code utilise React , une bibliothèque JavaScript open source pour créer une `import` `Tabs.js` interface utilisateur. [](https://reactjs.org/) 

> [!NOTE]
> Bien que l'utilisation de React ne _soit_ pas requise pour le développement teams, ce didacticiel vous apprend à utiliser React.

## <a name="2-customize-your-tab-content-page"></a>2. Personnaliser la page de contenu de votre onglet

Vous pouvez personnaliser votre page de contenu d'onglet pour restituer une liste de contacts importants dans votre organisation. 

**Pour personnaliser la page de contenu de votre onglet**

1. Copiez et modifiez l'exemple de code suivant avec des informations pertinentes pour vous. Vous pouvez également utiliser le code tel quelle : 
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
1. Nous avons ouvert `src/components` le fichier dans le `Tab.js` répertoire. 
1. Go to `render()` and replace the template code with the modified code inside as shown in the following `return()` example:
    ```JavaScript
    render() {
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
1. Go to the `src/components` directory and modify the `App.css` file with the following code to make the email links easier to read with any theme that is used:
    ```CSS
    a {
      color: inherit;
    }
    ```
1. Enregistrez vos modifications. 

   Vous pouvez afficher le nouveau contenu dans l'onglet de votre application dans Teams.

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="Capture d'écran d'un onglet personnel avec du contenu statique.":::

## <a name="3-update-your-tab-theme"></a>3. Mettre à jour le thème de votre onglet

Il est important pour votre onglet d'avoir un thème qui semble natif de Teams. Vous devez mélanger votre onglet avec le thème Teams. Vos utilisateurs préfèrent généralement les thèmes par défaut (clair), foncé ou à contraste élevé. Comme vous l'avez peut-être remarqué dans la dernière capture d'écran, votre onglet a toujours un arrière-plan clair lorsque votre utilisateur utilise le thème foncé. Il ne s'agit pas d'une expérience utilisateur recommandée.

Le SDK client JavaScript teams peut rendre votre application sensible aux modifications de thème dans le client et y réagir. Pour cela, procédez comme suit :

1. **Obtenir le contexte sur le thème du client Teams configuré** L'appel dans votre fichier fournit un contexte sur le thème client configuré `microsoftTeams.getContext()` `Tab.js` (tel que le thème foncé). Le code suivant accède à `context` l'interface et à ses propriétés :

    ```JavaScript
    componentDidMount(){
      // Get the user context from Teams and set it in the state
      microsoftTeams.getContext((context, error) => {
        this.setState({
          context: context,
          theme: context.theme
        });
      });
    }
    ```
1. **Créer un handler de modification de thème** Avec les propriétés en main, votre application a une bonne compréhension de ce qui se passe `context` autour de elle dans Teams. Toutefois, l'application n'a toujours pas d'apparence reflétant le thème lorsqu'un utilisateur le met à jour.

   Vous avez besoin d'un handler pour mettre à jour l'état de votre application avec le thème. Pour créer un handler, insérez le handler de modification de thème suivant immédiatement après `microsoftTeams.getContext()` l'appel :

    ```JavaScript
    microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.context.theme) {
    this.setState({
      context: {
      ...this.state.context,
      theme
      }
      })   
      }
    });
      ```
1. **Correspondre aux styles de thème** Votre handler de modification de thème est en place, mais vous devez toujours répondre aux modifications et aligner les couleurs de votre onglet avec le thème actuel.

   Dans la `render()` fonction, stockez l'état fourni par le handler de modification de thème dans `isTheme` :

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > Cet exemple est simplement une façon d'appliquer des styles à votre onglet. Utilisez le code tel qu'il est, développez-le ou écrivez le vôtre.

    Après avoir stocké l'état fourni par le handler de modification de thème, fournissez la logique conditionnelle pour restituer les styles de votre onglet en fonction du thème actuel. L'exemple suivant montre une façon de faire de base :

    1. Go to `render()` and check the current theme in `isTheme` .
    1. Créez `newTheme` un objet avec des propriétés CSS pertinentes pour le thème actuel.
    1. Appliquez la CSS suivante à l'élément HTML racine de votre onglet ( `<div style={newTheme}>` :

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

       Vérifiez votre onglet dans Teams. L'apparence correspond désormais étroitement au thème foncé.

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="Capture d'écran d'un onglet personnel avec affichage de contenu statique.":::

## <a name="see-also"></a>Voir aussi

* [Kit de développement logiciel client JavaScript Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Conception de votre onglet pour le bureau et le web Microsoft Teams](../tabs/design/tabs.md) 
* [Interface de contexte](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [Conception de votre application Microsoft Teams avec des modèles d'interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) 
* [Onglets sur les appareils mobiles](../tabs/design/tabs-mobile.md)
* [Prise en charge de l' sign-on unique (SSO) pour les onglets](../tabs/how-to/authentication/auth-aad-sso.md)
* [Présentation de l’API Microsoft Teams](https://docs.microsoft.com/graph/teams-concept-overview)
* [Créer un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet de canal](../build-your-first-app/build-channel-tab.md)