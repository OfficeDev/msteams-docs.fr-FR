---
title: Get started - Build a channel and group tab
author: heath-hamilton
description: Créez rapidement un onglet de groupe et de canal Microsoft Teams à l’aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 2ad0474859118f302a39e823f7669dc54061d525
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795453"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Créer un onglet de canal et de groupe pour Microsoft Teams

Dans ce didacticiel, vous allez créer un onglet de canal de base *(également* appelé onglet *groupe),* qui est une page en plein écran pour un canal d’équipe ou une conversation. Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects de ce type d’onglet (par exemple, renommer l’onglet afin qu’il soit significatif pour leur canal).

## <a name="your-assignment"></a>Votre affectation

Il n’y a pas longtemps, votre organisation a créé une application Teams qui utilise un onglet pour afficher des informations de contact importantes (service d’aide, RESSOURCES HUMAINES, etc.). Toutefois, étant donné qu’il s’agit d’un onglet personnel, chaque utilisateur doit installer l’onglet pour le voir et son adoption est inférieure aux attentes. En d’autres termes, trop d’employés ne savent toujours pas comment joindre le service d’aide.

Vous pouvez faciliter la recherche de ces informations en construisant un onglet de canal, ce qui permet de supprimer la charge de l’installation d’une application par tout le monde. Au lieu de cela, un utilisateur peut ajouter l’onglet dans un canal ou une conversation au profit d’un groupe entier.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application à l’aide du Shared Computer Toolkit Microsoft Teams pour Visual Studio Code
> * Identifier certaines configurations d’application et la échafaudage pertinentes pour les onglets de canal
> * Créer du contenu d’onglet
> * Créer du contenu pour la page de configuration d’un onglet
> * Fournir un nom d’onglet suggéré
> * Créer et exécuter votre application localement
> * Chargement de version test de votre application dans Teams

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l’avez pas encore fait, assurez-vous que vous comprenez et installez les [conditions préalables de développement teams.](build-first-app-overview.md#get-prerequisites)

## <a name="1-create-your-app-project"></a>1. Créer votre projet d’application

Le Shared Computer Toolkit Microsoft Teams vous aide à configurer votre application et à configurer la modèle pour les onglets de canal et de groupe, y compris une page de configuration de base et une page de contenu qui affiche « Hello, World! ». Message.

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut vous être utile de suivre ces [instructions](../build-your-first-app/build-and-run.md) qui expliquent les projets plus en détail.

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.
1. Dans **l’écran Ajouter des fonctionnalités,** sélectionnez **Onglet,** puis **Suivant**.
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.) Sélectionnez **l’onglet de canal Groupe ou Teams.**
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.  

## <a name="2-identify-relevant-app-project-components"></a>2. Identifier les composants de projet d’application pertinents

La plupart des configurations d’application et de la création de la échafaudage sont automatiquement définies lorsque vous créez votre projet avec le kit de ressources. Examinons les principaux composants de la création d’un onglet de canal.

### <a name="app-configurations"></a>Configurations d’application

Dans le kit de ressources, allez dans **App Studio** pour afficher et mettre à jour les configurations de votre application.

### <a name="app-scaffolding"></a>Échafaudage d’application

La échafaudage de l’application fournit les composants pour le rendu de l’onglet de votre canal dans Teams. Il y a beaucoup de choses que vous pouvez utiliser, mais pour l’instant, vous ne devez vous concentrer que sur les questions suivantes :

* Deux fichiers se trouvent dans `src/components` le répertoire de votre projet :
  * `Tab.js` pour le rendu de la page de contenu de votre onglet.
  * `TabConfig.js` pour le rendu de la page de configuration de votre onglet.
* SDK client JavaScript Microsoft Teams, qui est pré-chargé dans les composants frontaux de votre projet.

## <a name="3-customize-your-tab-content-page"></a>3. Personnaliser la page de contenu de votre onglet

Copiez et mettez à jour l’extrait de code suivant avec des informations pertinentes pour votre organisation ou, par souci de temps, utilisez le code tel qu’il est.

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

Go to the `src/components` directory and open `Tab.js` . Recherchez `render()` la fonction et collez votre contenu à l’intérieur `return()` (comme illustré).

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

Ajoutez la règle suivante à (également située dans ) afin que les liens de messagerie soient plus faciles à lire, quel que `App.css` soit le thème `src/components` utilisé.

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. Personnaliser la page de configuration de votre onglet

Chaque onglet d’un canal ou d’une conversation possède une page de configuration, une page modale avec au moins une option de configuration qui s’affiche lorsque les utilisateurs ajoutent votre application. La page de configuration demande par défaut aux utilisateurs s’ils souhaitent avertir le canal ou la conversation lors de l’installation de l’onglet.

Ajoutez du contenu personnalisé à votre page de configuration. Go to your project’s `src/components` directory, open `TabConfig.js` , and update the placeholder content inside `return()` (as shown in the following example).

```JavaScript
return (
    <div>
      <h1>Add My Contoso Contacts</h1>
      <div>
        Select <b>Save</b> to add our organization's important contacts to this workspace.
      </div>
    </div>
);
```
 
> [!TIP]
> Fournissez au moins quelques informations brèves sur votre application sur cette page, car il peut s’agit de la première fois que les utilisateurs en font l’apprentissage. Vous pouvez également inclure des options de configuration personnalisées ou [un](../tabs/how-to/authentication/auth-aad-sso.md)flux de travail d’authentification, ce qui est courant dans les pages de configuration d’onglets.

## <a name="5-provide-a-suggested-tab-name"></a>5. Fournir un nom d’onglet suggéré

Lorsque vous ajoutez un onglet de canal, le nom de l’application s’affiche par défaut (par exemple, **première application).**

Cela peut être correct en fonction de ce que vous appelez votre application, mais vous souhaitez peut-être fournir un nom plus logique dans le contexte de la collaboration de groupe (par exemple, Contacts **d’équipe).**

1. Dans `TabConfig.js` , allez à `microsoftTeams.settings.setSettings` .
2. Ajoutez `suggestedDisplayName` la propriété avec le nom d’onglet que vous souhaitez afficher par défaut. 
3. Utilisez le nom fourni dans l’exemple suivant ou tapez votre nom. (Par défaut, les utilisateurs peuvent modifier le nom.)

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. Créer et exécuter votre application

Dans l’intérêt du temps, vous allez créer et exécuter votre application localement.

(Ces informations sont également disponibles dans le kit de `README` ressources.)

1. Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécutez `npm start` .

Une fois terminé, une compilation a **réussi !** dans le terminal. Votre application est en cours d’exécution sur `https://localhost:3000` .

## <a name="7-sideload-your-app-in-teams"></a>7. Chargement de version secondaire de votre application dans Teams

Votre application est prête à être testée dans Teams. Pour ce faire, vous devez avoir un compte qui autorise le chargement de version de version d’application. (Si vous n’êtes pas sûr de l’avoir, découvrez comment obtenir un compte [de développement Teams.)](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)

1. Dans Visual Studio Code, appuyez sur la **touche F5** pour lancer un client web Teams.
1. Pour afficher le contenu de votre application dans Teams, spécifiez que l’endroit où votre application est en cours d’exécution ( `localhost` ) est digne de confiance :
   1. Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyez sur **F5**.
   1. Go to `https://localhost:3000/tab` and proceed to the page.
1. Revenir à Teams. Dans la modale, sélectionnez Ajouter à une équipe ou Ajouter à une **conversation** et recherchez un canal ou une conversation que vous pouvez utiliser pour le test. 
1. Sélectionnez **Configurer un onglet.** La page de configuration s’affiche dans une forme modale.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran d’une page de configuration d’onglet de canal.":::
1. Sélectionnez **Enregistrer** pour configurer l’onglet. La page de contenu s’affiche.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran d’un onglet de canal avec affichage de contenu statique.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous avez une application Teams avec un onglet pour afficher du contenu utile dans les canaux et les conversations.

## <a name="learn-more"></a>En savoir plus

* [](../tabs/how-to/authentication/auth-aad-sso.md)Authentifier les utilisateurs d’onglets avec l’authentification unique : si vous souhaitez uniquement que les utilisateurs autorisés l’affichent, configurer l’authentification unique (SSO) via Azure Active Directory (AD).
* [Incorporer du contenu](../tabs/how-to/add-tab.md#tab-requirements)à partir d’une application web ou d’une page web existante : nous vous avons montré comment créer du contenu pour un onglet, mais vous pouvez également charger du contenu à partir d’une URL externe.
* [Créez une expérience d’onglet](../tabs/design/tabs.md)transparente : consultez les recommandations pour la conception des onglets Teams.
* [Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): comprendre comment développer des onglets pour téléphones et tablettes.
* [Utiliser les données Teams avec l’API Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)
* [Créer un onglet sans le kit de ressources](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>Leçon suivante

Vous savez comment créer un onglet pour la collaboration. Vous souhaitez essayer de créer un autre type d’application Teams ?

> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)
