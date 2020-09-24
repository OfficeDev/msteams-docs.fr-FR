---
title: Créer un onglet personnel teams
author: heath-hamilton
description: Découvrez comment créer un onglet personnel pour votre première application Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: a86c9e1e46b97c6b265bfa9ad2f618655c524ee4
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237803"
---
# <a name="build-a-teams-personal-tab"></a>Créer un onglet personnel teams

Les onglets permettent d’exposer facilement du contenu dans votre application en incorporant essentiellement une page Web dans Teams.

Il existe deux types d’onglets dans Teams. Dans ce didacticiel, vous allez créer un *onglet personnel*, une page de contenu en plein écran pour les utilisateurs individuels. (Les onglets personnels sont les plus proches de l’expérience d’un site Web classique dans Teams.)

## <a name="before-you-begin"></a>Avant de commencer

Vous avez besoin d’un onglet personnel de base pour commencer. Si vous n’en avez pas, reportez-vous à [la rubrique générer et exécuter votre première application teams](../build-your-first-app/build-and-run.md).

## <a name="your-assignment"></a>Votre affectation

Les personnes de votre organisation ont des difficultés à trouver des informations de contact de base pour des fonctions importantes (support technique, RH, etc.). Vous êtes chargé de vous assurer qu’ils peuvent rapidement trouver ces informations à un seul endroit. Comment procéder ? Onglet personnel Teams, bien sûr.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Identifier certaines des propriétés de manifeste de l’application et la structure correspondant aux onglets personnels
> * Créer un contenu de tabulation
> * Mettre à jour le thème de couleurs d’un onglet en fonction de la préférence de l’utilisateur

## <a name="1-identify-relevant-app-project-components"></a>1. identifier les composants de projet d’application pertinents

La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams. Examinons les principaux composants de création d’un onglet personnel.

### <a name="app-manifest"></a>Manifeste de l’application

L’extrait de code suivant du manifeste de l’application (le `manifest.json` fichier dans le répertoire de votre projet `.publish` ) affiche [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , qui inclut les propriétés et les valeurs par défaut relatives aux onglets personnels.

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

* `entityId`: Identificateur unique de la page affichée par l’onglet.
* `name`: Le nom complet de l’onglet (par exemple, « mes contacts »).
* `contentUrl`: URL de l’hôte la page de contenu de l’onglet (doit être HTTPs).
* `scopes`: Spécifie que l’onglet est réservé à un usage personnel.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

Le échafaudage de l’application fournit les composants pour le rendu de votre onglet dans Teams. Vous pouvez utiliser un grand nombre de choses, mais pour le moment, il vous suffit de vous concentrer sur les éléments suivants :

* `Tab.js` fichier dans le `src/components` Répertoire de votre projet
* Kit de développement logiciel (SDK) JavaScript de Microsoft Teams, qui est préinstallé dans les composants frontaux de votre projet

## <a name="2-customize-your-tab-content-page"></a>2. personnaliser votre page de contenu d’onglet

Compilez une liste de contacts importants dans votre organisation. Copiez et mettez à jour l’extrait de code suivant avec les informations qui vous concernent ou, pour des raisons de temps, utilisez le code tel quel.

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

Accédez au `src/components` répertoire et ouvrez `Tab.js` . Recherchez la `render()` fonction et collez votre contenu dans `return()` (comme illustré).

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

Ajoutez la règle suivante pour `App.css` que les liens électroniques soient plus faciles à lire quel que soit le thème utilisé.

```CSS
a {
  color: inherit;
}
```

Enregistrez vos modifications. Accédez à l’onglet de votre application dans teams pour afficher le nouveau contenu.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Capture d’écran d’un onglet personnel avec du contenu statique.":::

## <a name="3-update-the-tab-theme"></a>3. mettre à jour le thème de l’onglet

Les applications intéressantes semblent natives pour Teams, c’est pourquoi il est important que votre onglet se mélange avec le thème des équipes que vos utilisateurs préfèrent : par défaut (clair), foncé ou contraste élevé. Comme vous avez pu le remarquer dans la dernière capture d’écran, votre onglet présente toujours un arrière-plan clair lorsque le client utilise le thème foncé. Il ne s’agit pas d’une expérience utilisateur recommandée.

Le [Kit de développement logiciel (SDK) du client JavaScript teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) permet à votre application de prendre en compte les modifications apportées au thème dans le client. Passons en revue la procédure.

### <a name="get-context-about-the-teams-client"></a>Obtenir un contexte sur le client teams

Dans votre `Tab.js` fichier, il existe un `microsoftTeams.getContext()` appel qui fournit des [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) informations sur le thème client configuré, entre autres. Grâce à la génération de modèles automatique d’application, utilisez ce code en tant que pour accéder à l' `context` interface et à ses propriétés.

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

### <a name="create-a-theme-change-handler"></a>Créer un gestionnaire de modification de thème

Avec les `context` Propriétés en main, votre application a une bonne compréhension de ce qui se passe dans Teams. Toutefois, l’application ne connaît toujours pas son apparence doit refléter le thème choisi par l’utilisateur.

Vous avez besoin d’un gestionnaire pour que l’état de votre application change avec le thème. Insérez le gestionnaire de modifications de thème suivant immédiatement après l' `microsoftTeams.getContext()` appel.

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>Correspondance des styles de thème

Votre gestionnaire de modifications de thème est en place, mais vous avez besoin de code qui répond à ces modifications et aligne les couleurs de votre onglet sur le thème actuel.

> [!NOTE]
> Dans l’exemple suivant, vous pouvez appliquer des styles à votre onglet. Utilisez le code tel quel, développez-le ou rédigez-le.

Stockez l’état fourni par le gestionnaire de modifications de thème dans `isTheme` .

```JavaScript
  const isTheme = this.state.theme
```

Fournissez une logique conditionnelle pour afficher les styles de votre onglet en fonction du thème actuel. L’exemple suivant montre une méthode de base pour effectuer cette opération par 1) en vérifiant le thème actuel dans `isTheme` , 2) en créant un `newTheme` objet avec des propriétés CSS pertinentes pour le thème actuel et 3) en appliquant la feuille de style CSS à l’élément HTML racine de votre contenu d’onglet ( `<div>` ).

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

Vérifiez l’onglet dans Teams. L’apparence doit correspondre au thème foncé.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Capture d’écran d’un onglet personnel avec affichage de contenu statique.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’une application teams avec un onglet personnel qui facilite la recherche de contacts importants dans votre organisation.

## <a name="learn-more"></a>En savoir plus

* [Authentifier les utilisateurs avec l’authentification](../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).
* [Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.
* [Créez une expérience transparente pour votre onglet](../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.
* [Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour les téléphones et les tablettes.
* [Intégration à l’API Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)
* [Créer un onglet sans la boîte à outils](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>Leçon suivante

Vous saurez comment créer un onglet pour une utilisation personnelle. Examinons ce qu’il faut faire pour créer un onglet pour les canaux d’équipe et les conversations.

> [!div class="nextstepaction"]
> [Créer un onglet de canal](../build-your-first-app/build-channel-tab.md)
