---
title: Prise en main-créer un onglet de canal et de groupe
author: heath-hamilton
description: Créez rapidement un onglet de chaîne et de groupe Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: f890754cdf4ca43f39c25e3ba24fcf47b08c5a9f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452854"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Créer un onglet de canal et de groupe pour Microsoft teams

Dans ce didacticiel, vous allez créer un *onglet de canal* de base (également appelé *onglet de groupe*), qui est une page plein écran pour un canal d’équipe ou une conversation. Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects de ce type d’onglet (par exemple, renommer l’onglet de sorte qu’il soit significatif pour son canal).

## <a name="your-assignment"></a>Votre affectation

Il n’y a pas longtemps, votre organisation a créé un onglet teams avec des informations sur la façon de contacter des fonctions importantes (support technique, RH, etc.). Toutefois, étant donné que l’onglet a été inclus uniquement à des fins personnelles, chaque utilisateur doit installer l’onglet pour l’afficher et l’adoption est inférieure à celle attendue. En d’autres termes, trop de travailleurs ne sachent toujours pas comment contacter le support technique.

Vous pouvez faciliter la recherche de ces informations en créant un onglet de canal, ce qui vous évite de devoir installer une application. Au lieu de cela, un utilisateur peut installer l’onglet dans un canal ou une conversation pour l’ensemble du groupe.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Créer un projet d’application à l’aide de Microsoft teams Toolkit pour Visual Studio code
> * Identifier certaines des propriétés de manifeste de l’application et la génération de modèles automatique correspondant aux onglets canal et groupe
> * Héberger une application localement
> * Créer un contenu de tabulation
> * Créer du contenu pour la page de configuration d’un onglet
> * Autoriser la configuration et l’installation d’un onglet
> * Fournir un nom d’onglet suggéré

## <a name="1-create-your-app-project"></a>1. créer votre projet d’application

La boîte à outils Microsoft teams vous permet de configurer le manifeste de l’application et les onglets de canal et de groupe, notamment une page de configuration de base et une page de contenu qui affiche un « Hello, World ! ». Message.

> [!TIP]
> Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. Entrez un nom pour votre application Teams. (Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)
1. Dans l’écran **Ajouter des fonctionnalités** , **Sélectionnez l’onglet** Groupe, puis **groupe ou Team Channel**.
1. Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.  

## <a name="2-identify-relevant-app-project-components"></a>2. identifier les composants de projet d’application pertinents

La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams. Examinons les principaux composants de création d’un onglet de canal et de groupe.

### <a name="app-manifest"></a>Manifeste de l’application

L’extrait de code suivant du manifeste de l’application indique [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) , qui inclut les propriétés et les valeurs par défaut pertinentes pour les onglets canal et groupe.

```JSON
"configurableTabs": [
    {
        "configurationUrl": "{baseUrl0}/config",
        "canUpdateConfiguration": true,
        "scopes": [
            "team",
            "groupchat"
        ]
    }
],
```

* `configurationUrl`: URL hôte de votre page de configuration d’onglet (doit être HTTPs).
* `canUpdateConfiguration`: Si ce paramètre `true` est défini sur, les utilisateurs peuvent modifier les paramètres de tabulation, renommer l’onglet ou le supprimer d’un canal ou d’une conversation.
* `scopes`: Spécifie si les utilisateurs peuvent installer l’application dans Channels ( `team` ) et les conversations ( `groupchat` ). Au moins une valeur est requise.

### <a name="app-scaffolding"></a>Génération de modèles automatique d’application

Le échafaudage de l’application fournit un `TabConfig.js` fichier, situé dans le `src/components` Répertoire de votre projet, pour afficher la page de configuration de votre onglet (en savoir plus sur cela prochainement).

## <a name="3-run-your-app"></a>3. exécuter votre application

Pour des raisons de temps, vous allez créer et exécuter votre application localement.

1. Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .
1. Exécuter `npm start` .

Une fois terminé, une **compilation est effectuée.** message dans le terminal.

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a>4. configurer un tunnel sécurisé pour votre application

À des fins de test, nous allons héberger votre onglet sur un serveur Web local (port 3000).

1. Dans un terminal, exécutez `ngrok http 3000` .
1. Copiez l’URL HTTPs que vous avez fournie.
1. Dans votre `.publish` répertoire, ouvrez `Development.env` .
1. Remplacez la `baseUrl0` valeur par l’URL copiée. (Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ca5.ngrok.io` .)

Le manifeste de votre application pointe vers l’emplacement où vous hébergez l’onglet.

## <a name="5-customize-your-tab-content-page"></a>5. personnaliser votre page de contenu d’onglet

Ouvrez le manifeste de l’application ( `manifest.json` ) dans le `.publish` répertoire et définissez les propriétés suivantes dans [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , qui définit la page de contenu de votre onglet.

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "My Contacts",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

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

Ajoutez la règle suivante pour `App.css` que les liens électroniques soient plus faciles à lire quel que soit le thème utilisé.

```CSS
a {
  color: inherit;
}
```

## <a name="6-create-your-tab-configuration-page"></a>6. créer votre page de configuration d’onglet

Chaque onglet d’un canal ou d’une conversation comporte une page de configuration, modale avec au moins une option d’installation qui s’affiche lorsque les utilisateurs installent votre application. La page Configuration par défaut demande à l’utilisateur s’il souhaite avertir le canal ou la conversation lorsque l’onglet est installé.

Ajoutez du contenu à votre page de configuration. Accédez au répertoire de votre projet `src/components` , ouvrez-le `TabConfig.js` et insérez du contenu dans `return()` (comme illustré).

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

## <a name="7-allow-the-tab-to-be-configured-and-installed"></a>7. autoriser la configuration et l’installation de l’onglet

Pour que les utilisateurs puissent configurer et installer correctement l’onglet, vous devez ajouter l' [URL d’hôte sécurisé que vous avez définie](#4-set-up-a-secure-tunnel-to-your-app) au composant de page de configuration.

Accédez à `TabConfig.js` et recherchez `microsoftTeams.settings.setSettings` . Pour `"contentUrl"` , remplacez la `localhost:3000` partie de l’URL par le domaine dans lequel vous hébergez le contenu de l’onglet (comme illustré ci-dessous).

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

Assurez-vous également que `microsoftTeams.settings.setValidityState(true);` . C’est par défaut, mais si ce paramètre est défini sur `false` , le bouton **Enregistrer** est désactivé sur la page de configuration.

## <a name="8-provide-a-suggested-tab-name"></a>8. fournir un nom d’onglet suggéré

Lorsque vous installez un onglet pour une utilisation personnelle, le nom complet est la `name` propriété dans la `staticTabs` partie du manifeste de l’application (par exemple, **mes contacts**). Lorsque vous installez un onglet canal, le nom de l’application s’affiche par défaut (par exemple, **First-App**).

Cela peut être approprié en fonction de ce que vous appelez votre application, mais vous souhaiterez peut-être attribuer un nom plus évocateur dans le contexte de la collaboration de groupe (par exemple, **contacts d’équipe**).

Dans `TabConfig.js` , revenez à `microsoftTeams.settings.setSettings` . Ajoutez la `suggestedDisplayName` propriété avec le nom de l’onglet que vous souhaitez afficher par défaut (comme illustré). Utilisez le nom fourni ou créez-en un. N’oubliez pas que dans le manifeste, vous autorisez les utilisateurs à modifier le nom s’ils le souhaitent.

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="9-view-the-tab"></a>9. afficher l’onglet

Pour afficher les pages de configuration et de contenu de votre onglet, vous devez l’installer dans un canal ou une conversation.

1. Dans le client Teams, sélectionnez **applications**.
1. Sélectionnez **Télécharger une application personnalisée** et choisissez l’application `Development.zip` .
1. Sélectionnez **Ajouter à une équipe** ou **Ajouter à une conversation** , puis recherchez un canal ou une conversation que vous pouvez utiliser à des fins de test.
1. Sélectionnez **configurer un onglet**. La page Configuration s’affiche.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran de la page de configuration de l’onglet canal.":::
1. Sélectionnez **Enregistrer** pour configurer l’onglet. Le contenu s’affiche.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran de la page de configuration de l’onglet canal.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’une application teams avec un onglet qui permet d’afficher du contenu utile dans les canaux et les conversations.

## <a name="learn-more"></a>Si vous souhaitez en savoir plus

* [Authentifier les utilisateurs avec l’authentification](../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).
* [Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.
* [Créez une expérience transparente pour votre onglet](../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.
* [Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour les téléphones et les tablettes.
* [Créer un onglet sans la boîte à outils](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>Leçon suivante

Vous saurez comment créer un onglet pour la collaboration. Vous souhaitez essayer de créer un autre type d’application teams ?

> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)
