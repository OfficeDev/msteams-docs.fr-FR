---
title: Prise en main-créer un onglet de canal et de groupe
author: heath-hamilton
description: Créez rapidement un onglet de chaîne et de groupe Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: bb87d34974469057287cf63725e7722125c57c34
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605244"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Créer un onglet de canal et de groupe pour Microsoft teams

Dans ce didacticiel, vous allez créer un *onglet de canal* de base (également appelé *onglet de groupe*), qui est une page plein écran pour un canal d’équipe ou une conversation. Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects de ce type d’onglet (par exemple, renommer l’onglet de sorte qu’il soit significatif pour son canal).

## <a name="your-assignment"></a>Votre affectation

Il n’y a pas longtemps, votre organisation a créé une application teams qui utilise un onglet pour afficher les informations de contact importantes (support technique, RH, etc.). Toutefois, étant donné qu’il s’agit d’un onglet personnel, chaque utilisateur doit installer l’onglet pour l’afficher et l’adoption est plus faible que prévu. En d’autres termes, trop de travailleurs ne sachent toujours pas comment contacter le support technique.

Vous pouvez faciliter la recherche de ces informations en créant un onglet de canal, ce qui vous évite de devoir installer une application. Au lieu de cela, un utilisateur peut ajouter l’onglet dans un canal ou une conversation pour l’ensemble du groupe.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application à l’aide de Microsoft teams Toolkit pour Visual Studio code
> * Identifier certaines configurations d’application et la génération de modèles automatique concernant les onglets canal et groupe
> * Créer un contenu de tabulation
> * Créer du contenu pour la page de configuration d’un onglet
> * Fournir un nom d’onglet suggéré
> * Créer et exécuter votre application localement
> * Chargement de votre application dans teams à des fins de test

## <a name="before-you-begin"></a>Avant de commencer

Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).

## <a name="1-create-your-app-project"></a>1. créer votre projet d’application

Le kit de développement Microsoft teams vous aide à configurer votre application et à configurer la génération de modèles automatique correspondant aux onglets canal et groupe, notamment une page de configuration de base et une page de contenu qui affiche un « Hello, World ! ». Message.

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.
1. Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Cochez les options de l’onglet **personnel** , des **onglets de groupe ou de canal teams** . (Vous saurez bientôt pourquoi vous avez besoin des deux types d’onglets.)
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.  

## <a name="2-identify-relevant-app-project-components"></a>2. identifier les composants de projet d’application pertinents

La plupart des configurations et des modèles d’application sont configurés automatiquement lorsque vous créez votre projet à l’aide de Team Toolkit. Examinons les principaux composants de création d’un onglet de canal et de groupe.

### <a name="app-configurations"></a>Configurations d’application

Vous pouvez afficher et mettre à jour les configurations de vos applications à l’aide d’App Studio, qui est inclus dans la boîte à outils.

Lors de l’installation, le kit de fonctions a initialement configuré deux composants essentiels des onglets canal et groupe :

* **Page de configuration**: modal pour l’ajout d’un onglet à un canal ou une conversation. (Dans App Studio, vous pouvez trouver cette page en accédant à onglets **> onglet équipe**.)
* **Page de contenu**: où vous affichez votre contenu principal. (Dans App Studio, vous pouvez trouver cette page en accédant aux **onglets > ajouter un onglet personnel**.)

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

Le échafaudage de l’application fournit les composants pour le rendu de votre onglet personnel dans Teams. Vous pouvez utiliser un grand nombre de choses, mais pour le moment, il vous suffit de vous concentrer sur les éléments suivants :

* Deux fichiers situés dans le `src/components` Répertoire de votre projet :
  * `Tab.js` pour afficher la page de contenu de votre onglet.
  * `TabConfig.js` pour afficher la page de configuration de votre onglet.
* Le kit de développement logiciel (SDK) JavaScript de Microsoft Teams, qui est préchargé dans les composants frontaux de votre projet.

## <a name="3-customize-your-tab-content-page"></a>3. personnaliser votre page de contenu d’onglet

Copiez et mettez à jour l’extrait de code suivant avec des informations pertinentes pour votre organisation ou, pour des raisons de temps, utilisez le code tel quel.

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

Ajoutez la règle suivante à `App.css` (également dans `src/components` ) de sorte que les liens électroniques soient plus faciles à lire, quel que soit le thème utilisé.

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. personnaliser votre page de configuration d’onglet

Chaque onglet d’un canal ou d’une conversation comporte une page de configuration, modale avec au moins une option d’installation qui s’affiche lorsque les utilisateurs ajoutent votre application. La page Configuration par défaut demande à l’utilisateur s’il souhaite avertir le canal ou la conversation lorsque l’onglet est installé.

Ajoutez du contenu personnalisé à votre page de configuration. Accédez au répertoire de votre projet `src/components` , ouvrez `TabConfig.js` et mettez à jour le contenu de l’espace réservé dans `return()` (comme illustré dans l’exemple suivant).

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
> Au minimum, fournissez des informations succinctes sur votre application sur cette page, car il peut s’agir de la première fois que les utilisateurs en apprennent à le faire. Vous pouvez également inclure des options de configuration personnalisées ou un [flux de travail d’authentification](../tabs/how-to/authentication/auth-aad-sso.md), qui est courant sur les pages de configuration d’onglet.

## <a name="5-provide-a-suggested-tab-name"></a>5. fournir un nom d’onglet suggéré

Lorsque vous ajoutez un onglet de canal ou de groupe, le nom de l’application s’affiche par défaut (par exemple, **First-App**).

Cela peut être approprié en fonction de ce que vous appelez votre application, mais vous souhaiterez peut-être attribuer un nom plus évocateur dans le contexte de la collaboration de groupe (par exemple, **contacts d’équipe**).

Dans `TabConfig.js` , accédez à `microsoftTeams.settings.setSettings` . Ajoutez la `suggestedDisplayName` propriété avec le nom de l’onglet que vous souhaitez afficher par défaut (comme illustré). Utilisez le nom fourni ou créez-en un. (Par défaut, les utilisateurs peuvent modifier le nom si ils le souhaitent.)

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. générez et exécutez votre application

Pour des raisons de temps, vous allez créer et exécuter votre application localement.

(Ces informations sont également disponibles dans la boîte à outils `README` .)

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` .

Une fois terminé, une **compilation est effectuée.** message dans le terminal. Votre application est en cours d’exécution sur `https://localhost:3000` .

## <a name="7-sideload-your-app-in-teams"></a>7. chargement de votre application dans teams

Votre application est prête à être testée dans Teams. Pour ce faire, vous devez disposer d’un compte qui autorise l’application chargement. (Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)

1. Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.
1. Pour afficher le contenu de votre application dans Teams, spécifiez le lieu de fiabilité de votre application ( `localhost` ).
   1. Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyé sur **F5**.
   1. Accédez à `https://localhost:3000/tab` la page et passez à la page.
1. Revenir à Teams. Dans le modal, sélectionnez **Ajouter à une équipe** ou **Ajouter à une conversation** et recherchez un canal ou une conversation que vous pouvez utiliser à des fins de test.
1. Sélectionnez **configurer un onglet**. La page de configuration s’affiche dans un modal.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran de la page de configuration de l’onglet canal.":::
1. Sélectionnez **Enregistrer** pour configurer l’onglet. La page de contenu s’affiche.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran d’un onglet de canal avec affichage de contenu statique.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’une application teams avec un onglet qui permet d’afficher du contenu utile dans les canaux et les conversations.

## <a name="learn-more"></a>En savoir plus

* [Authentifier les utilisateurs avec l’authentification](../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).
* [Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.
* [Créez une expérience transparente pour votre onglet](../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.
* [Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour les téléphones et les tablettes.
* [Utiliser des données de teams avec l’API Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)
* [Créer un onglet sans la boîte à outils](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>Leçon suivante

Vous saurez comment créer un onglet pour la collaboration. Vous souhaitez essayer de créer un autre type d’application teams ?

> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)
