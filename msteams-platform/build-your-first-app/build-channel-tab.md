---
title: Démarrer - Construire un canal et un onglet de groupe
author: girliemac
description: Créez rapidement un canal Microsoft Teams onglet groupe à l’aide de la Microsoft Teams Shared Computer Toolkit.
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
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a>Créez votre premier canal et onglet de groupe pour Microsoft Teams

Ce tutoriel vous apprend à construire un onglet de *canal de base également* connu sous le nom *d’onglet de groupe*, qui est une page plein écran pour un canal d’équipe ou de chat. Vous pouvez également configurer certains aspects de ce type d’onglet, par exemple, renommer l’onglet de sorte qu’il est significatif pour leur canal, ce que vous ne pouvez pas faire dans un onglet personnel.

## <a name="what-youll-learn"></a>Ce que vous apprendrez

* Créez un projet d’application en utilisant Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.
* Comprendre les configurations de l’application et les échafaudages pertinents pour les onglets de canal.
* Créez le contenu de l’onglet et la configuration de l’onglet.
* Créez et exécutez votre application en équipes pour les tests.

## <a name="prerequisites"></a>Configuration requise

Assurez-vous de bien comprendre comment configurer et construire une application Teams simple. Pour plus d’informations, [consultez la première Microsoft Teams application « Hello, World! »](../build-your-first-app/build-and-run.md).

## <a name="1-create-your-app-project"></a>1. Créez votre projet d’application

Le Microsoft Teams Shared Computer Toolkit vous aide à configurer votre application et à configurer l’échafaudage pertinent pour les onglets de canal et de groupe. Il contient également une page de configuration de base et une page de contenu qui affiche un « Bonjour, Monde! » Message.

**Pour créer votre projet d’application**

1. Allez à Visual Studio Code et sélectionnez **Microsoft Teams barre** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: d’activité gauche.
1. Connectez-vous à votre compte Microsoft 365 développement lorsque vous êtes invité à le faire.
1. Sur **l’écran du** projet Select, **sélectionnez JS** (JavaScript) sous **Channel et l’application de groupe**.
1. Entrez un nom pour votre application Teams’argent. 

    > [!NOTE]
    > Il s’agit du nom par défaut de votre application et aussi du nom de l’annuaire du projet d’application sur votre machine locale.

1. Sélectionnez **L’onglet Groupe Teams canal de canal**.
1. Sélectionnez **Finition** en bas de l’écran pour configurer votre projet et enregistrer votre projet sur votre machine locale.  

## <a name="2-understand-your-app-project-components"></a>2. Comprendre les composants de votre projet d’application

Une grande partie des configurations d’applications et des échafaudages sont mis en place automatiquement lorsque vous créez votre projet avec la boîte à outils. Examinons les principaux composants pour la construction d’un onglet canal.

* **Configurations d’applications**: **Ouvrez App Studio** dans la boîte à outils pour afficher et mettre à jour les configurations de votre application.
* **Échafaudage d’application**: L’échafaudage d’application fournit les composants nécessaires pour rendre votre onglet de canal Teams. Il ya beaucoup de choses que vous pouvez travailler avec, cependant, pour l’instant nous allons nous concentrer sur ce qui suit:
  * Les fichiers situés dans `src/components` l’annuaire de votre projet :
    * `Tab.js` pour rendre la page de contenu de votre onglet.
    * `TabConfig.js` pour rendre la page de configuration de votre onglet.
  * Microsoft Teams Client JavaScript SDK, qui est préchargé dans les composants front-end de votre projet.

## <a name="3-customize-your-tab-content-page"></a>3. Personnalisez votre page de contenu d’onglet

1. Copiez et modifiez l’échantillon de code suivant avec des informations pertinentes pour votre organisation. Vous pouvez également utiliser l’extrait tel qu’il est :
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
    
1. Allez à `src/components` l’annuaire et ouvrez le `Tab.js` fichier. Localisez `render()` la fonction et coller votre code à l’intérieur comme indiqué dans `return()` l’exemple suivant :
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
    
1. Rendez-vous à `src/components` l’annuaire et mettez à jour le fichier avec le code suivant pour faciliter la lecture `App.css` des liens e-mail dans n’importe quel thème utilisé :
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a>4. Personnalisez votre page de configuration d’onglet

Chaque onglet d’un canal ou d’un chat a une page de configuration, un modal avec au moins une option de configuration qui s’affiche lorsque les utilisateurs ajoutent votre application. La page de configuration par défaut demande aux utilisateurs s’ils veulent aviser le canal ou le chat lorsque l’onglet est installé. Vous pouvez personnaliser la page de configuration en ajoutant du contenu personnalisé.

Pour ajouter du contenu personnalisé, ouvrez le `TabConfig.js` fichier à partir de `src/components` l’annuaire et mettez à jour le contenu du espace réservé à `return()` l’intérieur comme indiqué dans l’exemple suivant :

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
> Donnez une brève information sur votre application sur cette page puisque ce serait la première fois que les utilisateurs lisent à ce sujet. Vous pouvez également inclure des options de configuration personnalisées ou un [workflow d’authentification,](../tabs/how-to/authentication/auth-aad-sso.md)ce qui est courant sur les pages de configuration d’onglets.

## <a name="5-customize-your-tab-name"></a>5. Personnalisez le nom de votre onglet

Lorsque vous ajoutez un onglet canal, le nom de l’application s’affiche par défaut, par exemple, **la première application**. Vous pouvez également fournir un nom plus logique dans le cadre de la collaboration de groupe, par exemple, Contacts **d’équipe**:

1. Allez à `src/components` l’annuaire et ouvrez le `TabConfig.js` fichier.
1. Ajoutez la `suggestedDisplayName` propriété avec le nom d’onglet que vous souhaitez afficher par défaut sous `microsoftTeams.settings.setSettings` l’exemple suivant :

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a>6. Créez et exécutez votre application

Ce tutoriel vous apprend à créer et exécuter votre application localement. 

1. Allez à l’annuaire racine de votre projet d’application dans Terminal.
1. Exécutez `npm install`.
1. Exécutez `npm start`.

Ces informations sont également présentes dans la `README` section de la boîte à outils.
Votre application est en cours `https://localhost:3000` d’exécution après le compilé avec **succès!** message apparaît dans le terminal. 

## <a name="7-sideload-your-app-in-teams"></a>7. Chargez votre application de côté dans Teams

Votre application est prête à être testé en Teams. Pour ce faire, vous devez avoir un compte qui permet le chargement latéral de l’application. 

1. Ouvrez un Teams client Web en Visual Studio Code avec la **clé F5.**
1. Ajoutez `localhost` () comme digne de confiance en suivant ces étapes pour permettre à votre contenu d’application de s’afficher Teams :

   1. Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouverte avec **la touche F5.**
   1. Ouvrez `https://localhost:3000/tab` et passez à la page.

1. Sélectionnez **Ajouter à une équipe** ou Ajouter à un chat **et** localiser un canal ou un chat que vous pouvez utiliser pour tester à partir du modal dans Teams.
1. Sélectionnez **Configurer un onglet**. La page de configuration s’affiche dans un modal.

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran d’une page de configuration d’onglet de canal.":::

1. Sélectionnez **Enregistrer** pour configurer l’onglet. La page de contenu suivante s’affiche :

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran d’un onglet canal avec vue de contenu statique.":::

## <a name="see-also"></a>Voir aussi

* [Créez et exécutez votre première application Microsoft Teams](../build-your-first-app/build-and-run.md) 
* [Kit de développement logiciel client JavaScript Teams](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Conception de votre onglet pour Microsoft Teams bureau et web](../tabs/design/tabs.md) 
* [Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) 
* [Onglets sur les appareils mobiles](../tabs/design/tabs-mobile.md)
* [Prise en charge unique de la signalisation (SSO) pour les onglets](../tabs/how-to/authentication/auth-aad-sso.md)
* [Présentation de l’API Microsoft Teams](/graph/teams-concept-overview)
* [Créez un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [Créer une extension de messagerie](../build-your-first-app/build-messaging-extension.md)
