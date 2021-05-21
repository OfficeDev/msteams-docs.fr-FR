---
title: Get started - Build a channel and group tab
author: girliemac
description: Créez rapidement un onglet Microsoft Teams canal et de groupe à l’aide du Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: ff9cfbfb7d099db52966f119add4ce8729929aa1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566067"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a>Créez votre premier onglet de canal et de groupe pour Microsoft Teams

Ce didacticiel vous  apprend à créer un onglet de canal de base également appelé onglet de *groupe,* qui est une page en plein écran pour un canal d’équipe ou une conversation. Vous pouvez également configurer certains aspects de ce type d’onglet, par exemple renommer l’onglet afin qu’il soit significatif pour son canal, ce que vous ne pouvez pas faire dans un onglet personnel.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

* Créez un projet d’application à l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.
* Comprendre les configurations d’application et la échafaudage pertinentes pour les onglets de canal.
* Créez le contenu de l’onglet et la configuration de l’onglet.
* Créez et exécutez votre application dans teams pour les tests.

## <a name="prerequisites"></a>Conditions préalables

Assurez-vous que vous comprenez comment configurer et créer une application Teams simple. Pour plus d’informations, [voir créer votre première Microsoft Teams application « Hello World!](../build-your-first-app/build-and-run.md)».

## <a name="1-create-your-app-project"></a>1. Créer votre projet d’application

Le Microsoft Teams Shared Computer Toolkit vous permet de configurer votre application et la configuration de la échafaudage pertinente pour les onglets de canal et de groupe. Il contient également une page de configuration de base et une page de contenu qui affiche un « Hello, World! » Message.

**Pour créer votre projet d’application**

1. Go to Visual Studio Code and select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar.
1. Connectez-vous avec votre Microsoft 365 de développement lorsque vous y être invité.
1. Dans **l’écran Sélectionner un** projet, **sélectionnez JS** (JavaScript) sous **Canal et application de groupe.**
1. Entrez un nom pour votre application Teams de messagerie. 

    > [!NOTE]
    > Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.

1. Sélectionnez **l’onglet Teams canal.**
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet et enregistrez-le sur votre ordinateur local.  

## <a name="2-understand-your-app-project-components"></a>2. Comprendre les composants de votre projet d’application

La plupart des configurations d’application et de la création de la échafaudage sont automatiquement définies lorsque vous créez votre projet avec le kit de ressources. Examinons les principaux composants de la création d’un onglet de canal.

* **Configurations d’application**: **ouvrez App Studio** dans le kit de ressources pour afficher et mettre à jour les configurations de votre application.
* **Échafaudage d’application**: la échafaudage de l’application fournit les composants nécessaires au rendu de l’onglet de votre canal Teams. Toutefois, pour l’instant, nous allons nous concentrer sur les questions suivantes :
  * Fichiers situés dans le `src/components` répertoire de votre projet :
    * `Tab.js` pour le rendu de la page de contenu de votre onglet.
    * `TabConfig.js` pour le rendu de la page de configuration de votre onglet.
  * Microsoft Teams SDK client JavaScript, qui est pré-chargé dans les composants frontaux de votre projet.

## <a name="3-customize-your-tab-content-page"></a>3. Personnaliser la page de contenu de votre onglet

1. Copiez et modifiez l’exemple de code suivant avec des informations pertinentes pour votre organisation. Vous pouvez également utiliser l’extrait de code tel qu’il est :
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
    
1. Go to the `src/components` directory and open the `Tab.js` file. Recherchez `render()` la fonction et collez votre code à l’intérieur, comme illustré dans `return()` l’exemple suivant :
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
    
1. Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a>4. Personnaliser la page de configuration de votre onglet

Chaque onglet d’un canal ou d’une conversation possède une page de configuration, une page modale avec au moins une option de configuration qui s’affiche lorsque les utilisateurs ajoutent votre application. La page de configuration demande par défaut aux utilisateurs s’ils souhaitent avertir le canal ou la conversation lors de l’installation de l’onglet. Vous pouvez personnaliser la page de configuration en ajoutant du contenu personnalisé.

Pour ajouter du contenu personnalisé, ouvrez le fichier à partir du répertoire et mettez à jour le contenu de l’espace réservé à l’intérieur, comme `TabConfig.js` `src/components` illustré dans `return()` l’exemple suivant :

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
> Donnez de brèves informations sur votre application sur cette page, car c’est la première fois que les utilisateurs lisent des informations à ce sujet. Vous pouvez également inclure des options de configuration personnalisées ou [un](../tabs/how-to/authentication/auth-aad-sso.md)flux de travail d’authentification, ce qui est courant dans les pages de configuration d’onglets.

## <a name="5-customize-your-tab-name"></a>5. Personnaliser le nom de votre onglet

Lorsque vous ajoutez un onglet de canal, le nom de l’application s’affiche par défaut, par exemple, **première application.** Vous pouvez également fournir un nom plus logique dans le contexte de la collaboration de groupe, par exemple, **Contacts d’équipe**:

1. Go to the `src/components` directory and open the `TabConfig.js` file.
1. Ajoutez la propriété avec le nom d’onglet que vous souhaitez afficher par défaut, comme `suggestedDisplayName` `microsoftTeams.settings.setSettings` illustré dans l’exemple suivant :

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a>6. Créer et exécuter votre application

Ce didacticiel vous apprend à créer et exécuter votre application localement. 

1. Go to the root directory of your app project in Terminal.
1. Exécutez `npm install`.
1. Exécutez `npm start`.

Ces informations sont également présentes dans la `README` section du kit de ressources.
Votre application est en cours `https://localhost:3000` d’exécution après la compilation **!** s’affiche dans le terminal. 

## <a name="7-sideload-your-app-in-teams"></a>7. Chargement d’une version de version Teams

Votre application est prête à être testée dans Teams. Pour ce faire, vous devez avoir un compte qui autorise le chargement de version d’application. 

1. Ouvrez un client web Teams dans Visual Studio Code avec la **touche F5.**
1. Ajoutez ( ) comme digne de confiance en suivant les étapes suivantes pour permettre l’affichage du contenu de `localhost` votre application dans Teams :

   1. Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouverte avec la **touche F5.**
   1. Ouvrez `https://localhost:3000/tab` et continuez jusqu’à la page.

1. Sélectionnez **Ajouter à une équipe ou** Ajouter à une **conversation** et recherchez un canal ou une conversation que vous pouvez utiliser pour le test à partir de la modale dans Teams.
1. Sélectionnez **Configurer un onglet.** La page de configuration s’affiche dans une forme modale.

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran d’une page de configuration d’onglet de canal.":::

1. Sélectionnez **Enregistrer** pour configurer l’onglet. La page de contenu suivante s’affiche :

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran d’un onglet de canal avec affichage de contenu statique.":::

## <a name="see-also"></a>Voir aussi

* [Créer et exécuter votre première application Microsoft Teams application](../build-your-first-app/build-and-run.md) 
* [Kit de développement logiciel client JavaScript Teams](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Conception de votre onglet pour Microsoft Teams bureau et web](../tabs/design/tabs.md) 
* [Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) 
* [Onglets sur les appareils mobiles](../tabs/design/tabs-mobile.md)
* [Prise en charge de l' sign-on unique (SSO) pour les onglets](../tabs/how-to/authentication/auth-aad-sso.md)
* [Présentation de l’API Microsoft Teams](/graph/teams-concept-overview)
* [Créez un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [Créer une extension de messagerie](../build-your-first-app/build-messaging-extension.md)
