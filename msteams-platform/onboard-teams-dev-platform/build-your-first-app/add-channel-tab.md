---
author: heath-hamilton
description: Découvrez comment créer un onglet de canal dans votre première application Microsoft Teams.
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
title: Créer un onglet de canal pour teams
ms.openlocfilehash: 2346c67d10ea857bdafbfac6d29a07cb58f5c644
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964612"
---
# <a name="create-a-channel-tab-for-teams"></a>Créer un onglet de canal pour teams

Dans ce didacticiel, vous allez créer un *onglet de canal*de base, une page de contenu plein écran pour un canal d’équipe ou une conversation. Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects d’un onglet de canal (par exemple, renommer l’onglet de sorte qu’il soit significatif pour le canal).

## <a name="before-you-begin"></a>Avant de commencer

Vous avez besoin d’une application de base en cours d’exécution pour commencer. Si vous n’en avez pas, suivez les [instructions créer et exécuter les premières applications de teams](../build-your-first-app/build-and-run.md). Lorsque vous créez votre projet d’application, choisissez uniquement l’option de l' **onglet canal groupe ou teams** .

## <a name="your-assignment"></a>Votre affectation

Il n’y a pas longtemps, votre organisation a créé un onglet teams avec des informations sur la façon de contacter des fonctions importantes (support technique, RH, etc.). Toutefois, étant donné que l’onglet a été inclus uniquement à des fins personnelles, chaque utilisateur doit installer l’onglet pour l’afficher et l’adoption est inférieure à celle attendue. En d’autres termes, trop de travailleurs ne sachent toujours pas comment contacter le support technique.

Vous pouvez faciliter la recherche de ces informations en créant un onglet de canal, ce qui vous évite de devoir installer une application. Au lieu de cela, un utilisateur peut installer l’onglet dans un canal ou une conversation pour l’ensemble du groupe.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
>
> * Identifier les propriétés de manifeste de l’application et la structure des onglets de canal
> * Créer un contenu de tabulation
> * Créer du contenu pour la page de configuration d’un onglet
> * Autoriser la configuration et l’installation d’un onglet
> * Fournir un nom d’onglet suggéré

## <a name="identify-relevant-app-project-components"></a>Identifier les composants de projet d’application pertinents

La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams. Examinons les principaux composants de la création d’un onglet de canal.

### <a name="app-manifest"></a>Manifeste de l’application

L’extrait de code suivant du manifeste de l’application indique [`configurableTabs`](../../resources/schema/manifest-schema.md#configurabletabs) , qui inclut les propriétés et les valeurs par défaut pertinentes pour les onglets de canal.

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

## <a name="create-your-tab-content"></a>Créer le contenu de votre onglet

Ouvrez le manifeste de votre application ( `manifest.json` ) et définissez les propriétés suivantes dans [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs) , qui définit la page de contenu de votre onglet.

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

## <a name="create-your-tab-configuration-page"></a>Créer votre page de configuration d’onglet

Chaque onglet de canal comporte une page de configuration, modale avec au moins une option d’installation qui s’affiche lors de l’installation de l’application. La page Configuration par défaut demande à l’utilisateur s’il souhaite avertir le canal ou la conversation lorsque l’onglet est installé.

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
> Au minimum, fournissez des informations succinctes sur votre application sur cette page, car il peut s’agir de la première fois que les utilisateurs en apprennent à le faire. Vous pouvez également inclure des options de configuration personnalisées ou un [flux de travail d’authentification](../../tabs/how-to/authentication/auth-aad-sso.md), qui est courant sur les pages de configuration d’onglet.

## <a name="allow-the-tab-to-be-configured-and-installed"></a>Autoriser la configuration et l’installation de l’onglet

Pour que les utilisateurs puissent configurer et installer correctement l’onglet canal, vous devez ajouter l’URL d’hôte que vous avez configurée lors de la [création et de l’exécution de votre première application](../build-your-first-app/build-and-run.md) sur le composant de page de configuration.

Accédez à `TabConfig.js` et recherchez `microsoftTeams.settings.setSettings` . Pour `"contentUrl"` , remplacez la `localhost:3000` partie de l’URL par le domaine dans lequel vous hébergez le contenu de l’onglet (comme illustré ci-dessous).

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
    });
```

Assurez-vous également que `microsoftTeams.settings.setValidityState(true);` . C’est par défaut, mais si ce paramètre est défini sur `false` , le bouton **Enregistrer** est désactivé sur la page de configuration.

## <a name="provide-a-suggested-tab-name"></a>Fournir un nom d’onglet suggéré

Lorsque vous installez un onglet pour une utilisation personnelle, le nom d’affichage est la `name` propriété dans la `staticTabs` partie du manifeste de l’application (par exemple, **mes contacts**). Lorsque vous installez un onglet canal, le nom de l’application s’affiche par défaut (par exemple, **First-App**).

Cela peut être approprié en fonction de ce que vous appelez votre application, mais vous souhaiterez peut-être attribuer un nom plus évocateur dans le contexte de la collaboration de groupe (par exemple, **contacts d’équipe**).

Dans `TabConfig.js` , revenez à `microsoftTeams.settings.setSettings` . Ajoutez la `suggestedDisplayName` propriété avec le nom de l’onglet que vous souhaitez afficher par défaut (comme illustré). Utilisez le nom fourni ou créez-en un. N’oubliez pas que dans le manifeste, vous autorisez les utilisateurs à modifier le nom s’ils le souhaitent.

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
      "suggestedDisplayName": "Team Contacts"
    });
```

## <a name="view-the-channel-tab"></a>Affichage de l’onglet canal

Pour afficher les pages de configuration et de contenu de l’onglet canal, vous devez l’installer dans un canal ou une conversation.

1. Dans le client Teams, sélectionnez **applications**.
1. Sélectionnez **Télécharger une application personnalisée** et choisissez l’application `Development.zip` .
1. Sélectionnez **Ajouter à une équipe** ou **Ajouter à une conversation** , puis recherchez un canal ou une conversation que vous pouvez utiliser à des fins de test.
1. Sélectionnez **configurer un onglet**. La page Configuration s’affiche.

:::image type="content" source="../doc-links/images/channel-tab-tutorial-content.png" alt-text="Exemple de capture d’écran d’un onglet de canal avec contenu statique.":::

Une fois que vous sélectionnez **Enregistrer** pour configurer l’onglet, le contenu s’affiche.

:::image type="content" source="../doc-links/images/channel-tab-tutorial-content-installed.png" alt-text="Exemple de capture d’écran de l’onglet canal avec contenu statique.":::

## <a name="well-done"></a>Bien jouer

Félicitations ! Vous disposez d’une application teams avec un onglet Channel pour afficher du contenu utile dans des canaux et des conversations.

## <a name="learn-more"></a>Si vous souhaitez en savoir plus

* [Authentifier les utilisateurs avec l’authentification](../../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).
* [Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.
* [Créez une expérience transparente pour votre onglet](../../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.
* [Créer des onglets pour les appareils mobiles](../../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour les téléphones et les tablettes.

## <a name="next-lesson"></a>Leçon suivante

Vous saurez comment créer un onglet pour la collaboration. Vous souhaitez essayer de créer un autre type d’application teams ?

> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/add-bot.md)
