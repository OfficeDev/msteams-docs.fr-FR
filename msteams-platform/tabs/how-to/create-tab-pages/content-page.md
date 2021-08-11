---
title: Créer une page de contenu
author: surbhigupta
description: Comment créer une page de contenu
keywords: 'onglets teams : canal de groupe configurable statique'
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f6f673420de73d786ddee95b4da7870750f3e6851a80f6ad71b1e606d650ba60
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708307"
---
# <a name="create-a-content-page-for-your-tab"></a>Créer une page de contenu pour votre onglet

Une page de contenu est une page web qui est rendue dans le client Teams client. Ces éléments font partie des éléments ci-après :

* Onglet personnalisé d’étendue personnelle : dans ce cas, la page de contenu est la première page que l’utilisateur rencontre.
* Onglet personnalisé de canal ou de groupe : la page de contenu s’affiche après que l’utilisateur épingle et configure l’onglet dans le contexte approprié.
* Module [de tâche](~/task-modules-and-cards/what-are-task-modules.md): vous pouvez créer une page de contenu et l’incorporer en tant que vue web à l’intérieur d’un module de tâche. La page est restituer à l’intérieur de la fenêtre pop-up modale.

Cet article est spécifique à l’utilisation de pages de contenu en tant qu’onglets ; Toutefois, la majorité des conseils présentés ici s’appliquent, quelle que soit la présentation de la page de contenu à l’utilisateur.

## <a name="tab-content-and-design-guidelines"></a>Recommandations en matière de contenu d’onglet et de conception

L’objectif global de votre onglet est de fournir un accès à un contenu significatif et attrayant qui a une valeur pratique et un objectif évident. Vous devez vous concentrer sur le nettoyage, l’intuitive et l’immersif du contenu de votre conception d’onglet.

Pour plus d’informations, voir [recommandations en matière](~/tabs/design/tabs.md) de conception d’onglets [et Microsoft Teams de validation du store.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)

## <a name="integrate-your-code-with-teams"></a>Intégrer votre code avec Teams

Pour que votre page s’affiche Teams, vous devez inclure le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et inclure un appel après le chargement `microsoftTeams.initialize()` de votre page. 

Le code suivant fournit un exemple de la façon dont votre page et le client Teams communiquent :

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.10.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="access-additional-content"></a>Accéder à du contenu supplémentaire

Vous pouvez accéder à du contenu supplémentaire à l’aide du SDK pour interagir avec Teams, créer des liens profonds, utiliser des modules de tâche et vérifier si les domaines d’URL sont inclus dans le `validDomains` tableau.

### <a name="use-the-sdk-to-interact-with-teams"></a>Utiliser le SDK pour interagir avec les Teams

Le [Teams SDK JavaScript client](~/tabs/how-to/using-teams-client-sdk.md) fournit de nombreuses fonctions supplémentaires que vous pouvez trouver utiles lors du développement de votre page de contenu.

### <a name="deep-links"></a>Liens profonds

Vous pouvez créer des liens profonds vers des entités dans Teams. Ceux-ci sont utilisés pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Pour plus d’informations, voir [créer des liens profonds vers du contenu et](~/concepts/build-and-test/deep-links.md)des fonctionnalités dans Teams .

### <a name="task-modules"></a>Modules de tâche

Un module de tâche est une expérience de fenêtre pop-up modale que vous pouvez déclencher à partir de votre onglet. Dans une page de contenu, vous pouvez utiliser des modules de tâche pour présenter des formulaires pour recueillir des informations supplémentaires, afficher les détails d’un élément dans une liste ou présenter à l’utilisateur des informations supplémentaires. Les modules de tâche eux-mêmes peuvent être des pages de contenu supplémentaires ou créés entièrement à l’aide de cartes adaptatives. Pour plus d’informations, voir [l’utilisation de modules de tâche dans les onglets.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

### <a name="valid-domains"></a>Domaines valides

Assurez-vous que tous les domaines d’URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau dans votre [manifeste.](~/concepts/build-and-test/apps-package.md) Pour plus d’informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence du schéma de manifeste.

> [!NOTE]
> La fonctionnalité de base de votre onglet existe au sein Teams et non en dehors de Teams.

## <a name="show-a-native-loading-indicator"></a>Afficher un indicateur de chargement natif

À partir [du schéma de manifeste v1.7,](../../../resources/schema/manifest-schema.md)vous pouvez fournir un indicateur de chargement [natif.](../../../resources/schema/manifest-schema.md#showloadingindicator) Par exemple, page [de contenu d’onglet,](#integrate-your-code-with-teams) [page de configuration,](configuration-page.md) [page de suppression](removal-page.md)et [modules de tâche dans les onglets](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
> * Le comportement sur les clients mobiles n’est pas configurable via la propriété de l’indicateur de chargement natif. Les clients mobiles affichent cet indicateur par défaut sur les pages de contenu et les modules de tâche iframe. Cet indicateur sur mobile s’affiche lorsqu’une demande d’extraction de contenu est effectuée et est rejetée dès que la demande est terminée.

Si vous indiquez dans le manifeste de votre application, toutes les pages de configuration, de contenu et de suppression d’onglets et tous les modules de tâche iframe doivent suivre `showLoadingIndicator : true`  les étapes suivantes :

**Pour afficher l’indicateur de chargement**

1. `"showLoadingIndicator": true`Ajoutez-le à votre manifeste.
1. Appel `microsoftTeams.initialize();`.
1. Dans le **cas d’une** étape obligatoire, appelez Teams `microsoftTeams.appInitialization.notifySuccess()` que votre application a été correctement chargée. Teams masque ensuite l’indicateur de chargement, le cas échéant. Si elle n’est pas appelée dans les 30 secondes, elle est supposée que votre application a été hors délai et qu’un écran d’erreur avec une option de nouvelle `notifySuccess`  tentative s’affiche.
1. **Si vous le** souhaitez, si vous êtes prêt à imprimer à l’écran et que vous souhaitez charger différément le reste du contenu de votre application, vous pouvez masquer manuellement l’indicateur de chargement en `microsoftTeams.appInitialization.notifyAppLoaded();` appelant.
1. Si le chargement de votre application échoue, vous pouvez appeler Teams `microsoftTeams.appInitialization.notifyFailure(reason);` savoir qu’une erreur s’est produite. Un écran d’erreur s’affiche pour l’utilisateur. Le code suivant fournit un exemple de raisons d’échec d’application :

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Créer une page de contenu](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md)
