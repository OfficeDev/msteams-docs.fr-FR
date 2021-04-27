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
# <a name="build-a-personal-tab-for-microsoft-teams"></a>Créer un onglet personnel pour Microsoft Teams

Les onglets sont un moyen simple d'surfacer le contenu de votre application en insérant essentiellement une page web dans Teams.

Il existe deux types d'onglets dans Teams. Dans ce didacticiel, vous allez créer un onglet personnel *de* base, une page de contenu plein écran pour des utilisateurs individuels. (Les onglets personnels sont les plus proches d'une expérience de site web classique dans Teams.)

## <a name="before-you-begin"></a>Avant de commencer

Vous avez besoin d'un onglet personnel d'exécution de base pour commencer. Si vous n'en avez pas, voir [créer et exécuter votre première application Teams.](../build-your-first-app/build-and-run.md)

## <a name="your-assignment"></a>Votre affectation

Les membres de votre organisation ont des difficultés à trouver des informations de contact de base pour des fonctions importantes (service d'aide, RESSOURCES HUMAINES, etc.). Vous êtes chargé de vous assurer qu'ils peuvent trouver rapidement ces informations au même endroit. Comment le feriez-vous ? Un onglet personnel Teams, bien entendu.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Identifier certaines configurations d'application et la échafaudage pertinentes pour les onglets personnels
> * Créer du contenu d'onglet
> * Mettre à jour le thème de couleur d'un onglet en fonction des préférences de l'utilisateur

## <a name="1-identify-relevant-app-project-components"></a>1. Identifier les composants de projet d'application pertinents

La plupart des configurations d'application et de la création de la Shared Computer Toolkit sont automatiquement définies lorsque vous créez votre projet. Examinons les principaux composants de la création d'un onglet personnel.

### <a name="app-configurations"></a>Configurations d'application

Dans le kit de ressources, allez dans **App Studio** pour afficher et mettre à jour les configurations de votre application.

### <a name="app-scaffolding"></a>Échafaudage d'application

La échafaudage de l'application fournit les composants pour le rendu de votre onglet personnel dans Teams. Il y a beaucoup de choses que vous pouvez utiliser, mais pour l'instant, vous ne devez vous concentrer que sur les questions suivantes :

* `Tab.js` dans le `src/components` répertoire de votre projet. Il s'agit du rendu de la page de contenu de votre onglet.
* SDK client JavaScript Microsoft Teams, qui est pré-chargé dans les composants frontaux de votre projet.

## <a name="2-customize-your-tab-content-page"></a>2. Personnaliser la page de contenu de votre onglet

Compilez une liste de contacts importants dans votre organisation. Copiez et mettez à jour l'extrait de code suivant avec les informations qui vous sont pertinentes ou, dans un souci de temps, utilisez le code tel qu'il est.

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

Go to the `src/components` directory and open `Tab.js` . Recherchez `render()` la fonction et collez votre contenu à l'intérieur `return()` (comme illustré).

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

Ajoutez la règle suivante pour que les liens de messagerie soient plus faciles à `App.css` lire, quel que soit le thème utilisé.

```CSS
a {
  color: inherit;
}
```

Enregistrez vos modifications. Go to your app's tab in Teams to view the new content.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Capture d'écran d'un onglet personnel avec du contenu statique.":::

## <a name="3-update-the-tab-theme"></a>3. Mettre à jour le thème de l'onglet

Les bonnes applications sont natives de Teams. Il est donc important que votre onglet se fonde avec le thème Teams préféré de vos utilisateurs : par défaut (clair), foncé ou contraste élevé. Comme vous l'avez peut-être remarqué dans la dernière capture d'écran, votre onglet a toujours un arrière-plan clair lorsque le client utilise le thème foncé. Il ne s'agit pas d'une expérience utilisateur recommandée.

Le [SDK client JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) teams peut rendre votre application sensible aux modifications de thème dans le client et y réagir. Examinons comment faire.

### <a name="get-context-about-the-teams-client"></a>Obtenir du contexte sur le client Teams

Dans votre fichier, il existe un appel qui fournit des informations sur, entre autres, le `Tab.js` `microsoftTeams.getContext()` thème client [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) configuré. Grâce à la échafaudage de l'application, utilisez ce code tel qu'il est pour accéder à `context` l'interface et à ses propriétés.

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

### <a name="create-a-theme-change-handler"></a>Créer un handler de modification de thème

Avec les propriétés en main, votre application a une bonne compréhension de ce qui se passe `context` autour de elle dans Teams. Toutefois, l'application ne sait toujours pas que son apparence doit refléter le thème choisi par l'utilisateur.

Vous avez besoin d'un handler pour que l'état de votre application change avec le thème. Insérez le handler de modification de thème suivant immédiatement après `microsoftTeams.getContext()` l'appel.

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>Faire correspondre les styles de thème

Votre handler de modification de thème est en place, mais vous avez besoin d'un code qui répond à ces modifications et aligne les couleurs de votre onglet sur le thème actuel.

> [!NOTE]
> L'exemple suivant n'est qu'une façon d'appliquer des styles à votre onglet. Utilisez le code tel qu'il est, développez-le ou écrivez le vôtre.

Dans la `render()` fonction, stockez l'état fourni par le handler de modification de thème dans `isTheme` .

```JavaScript
  const isTheme = this.state.theme
```

Après avoir stocké l'état fourni par le handler de modification de thème, fournissez une logique conditionnelle pour restituer les styles de votre onglet en fonction du thème actuel. L'exemple suivant montre une façon de faire de base :
1. Vérifiez le thème actuel dans `isTheme` .
2. Créez `newTheme` un objet avec des propriétés CSS pertinentes pour le thème actuel.
3. Appliquez la CSS à l'élément HTML racine de votre onglet ( `<div style={newTheme}>` ).

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

Vérifiez votre onglet dans Teams. L'apparence doit correspondre étroitement au thème foncé.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Capture d'écran d'un onglet personnel avec affichage de contenu statique.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous avez une application Teams avec un onglet personnel qui facilite la recherche de contacts importants dans votre organisation.

## <a name="learn-more"></a>En savoir plus

* Suivez nos [instructions de conception](../tabs/design/tabs.md) et créez avec des [modèles d'interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) prêts pour la production pour créer une expérience transparente.
* Comprendre [les considérations mobiles pour](../tabs/design/tabs-mobile.md) les onglets.
* [Ajoutez l'authentification sso à votre onglet.](../tabs/how-to/authentication/auth-aad-sso.md)
* Utiliser les données Teams avec [Microsoft Graph.](https://docs.microsoft.com/graph/teams-concept-overview)
* [Créez un onglet sans le kit de ressources.](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-lesson"></a>Leçon suivante

Vous savez comment créer un onglet pour une utilisation personnelle. Examinons ce qu'il faut pour créer un onglet pour les canaux d'équipe et les conversations.

> [!div class="nextstepaction"]
> [Créer un onglet de canal](../build-your-first-app/build-channel-tab.md)
