---
title: Créer une page de contenu
author: surbhigupta
description: comment créer une page de contenu
keywords: onglets teams , canal de groupe configurable statique
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 68ce03e9b1ef303bd66043baed39baf954fb1d0f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111429"
---
# <a name="create-a-content-page-for-your-tab"></a>Créer une page de contenu pour votre onglet

Une page de contenu est une page web qui est affichée dans le client Teams. Ces éléments font partie des éléments suivants :

* Onglet personnalisé à portée personnelle : dans ce cas, la page de contenu est la première page rencontrée par l’utilisateur.
* Onglet personnalisé de canal ou de groupe : la page de contenu s’affiche après que l’utilisateur a épinglé et configuré l’onglet dans le contexte approprié.
* [Module de tâche](~/task-modules-and-cards/what-are-task-modules.md): vous pouvez créer une page de contenu et l’incorporer en tant que vue web à l’intérieur d’un module de tâche. La page est rendue dans la fenêtre contextuelle modale.

Cet article est spécifique à l’utilisation de pages de contenu sous forme d’onglets ; toutefois, la majorité des instructions s’appliquent ici, quelle que soit la façon dont la page de contenu est présentée à l’utilisateur.

## <a name="tab-content-and-design-guidelines"></a>Instructions de conception et de contenu de tabulation

L’objectif global de votre onglet est de fournir l’accès à du contenu significatif et attrayant qui a une valeur pratique et un objectif évident. Vous devez vous concentrer sur le nettoyage, la navigation et l’immersif de votre conception d’onglets.

Pour plus d’informations, consultez [instructions de conception de l’onglet](~/tabs/design/tabs.md) et [instructions de validation du Magasin Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).

## <a name="integrate-your-code-with-teams"></a>Intégrer votre code à Teams

Pour que votre page s’affiche dans Teams, vous devez inclure le [kit de développement logiciel (SDK) client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et inclure un appel à `microsoftTeams.initialize()` après le chargement de votre page.

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

Vous pouvez accéder à du contenu supplémentaire à l’aide du Kit de développement logiciel (SDK) pour interagir avec Teams, créer des liens profonds, utiliser des modules de tâche et vérifier si les domaines d’URL sont inclus dans le tableau `validDomains` .

### <a name="use-the-sdk-to-interact-with-teams"></a>Utiliser le Kit de développement logiciel (SDK) pour interagir avec Teams

Le kit de développement logiciel (SDK) [JavaScript du client Teams](~/tabs/how-to/using-teams-client-sdk.md) fournit de nombreuses fonctions supplémentaires que vous pouvez trouver utiles lors du développement de votre page de contenu.

### <a name="deep-links"></a>Liens profonds

Vous pouvez créer des liens profonds vers des entités dans Teams. Ceux-ci sont utilisés pour créer des liens qui accèdent au contenu et aux informations dans votre onglet. Pour plus d’informations, consultez [créer des liens profonds vers du contenu et des fonctionnalités dans Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Modules de tâche

Un module de tâche est une expérience contextuelle modale que vous pouvez déclencher à partir de votre onglet. Dans une page de contenu, vous pouvez utiliser des modules de tâche pour présenter des formulaires permettant de collecter des informations supplémentaires, d’afficher les détails d’un élément dans une liste ou de présenter des informations supplémentaires à l’utilisateur. Les modules de tâches eux-mêmes peuvent être des pages de contenu supplémentaires ou entièrement créés à l’aide de Cartes adaptatives. Pour plus d’informations, consultez [à l’aide de modules de tâche dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md).

### <a name="valid-domains"></a>Domaines valides

Assurez-vous que tous les domaines URL utilisés dans vos onglets sont inclus dans le tableau `validDomains` de votre [manifeste](~/concepts/build-and-test/apps-package.md). Pour plus d’informations, consultez [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence du schéma du manifeste.

> [!NOTE]
> La fonctionnalité principale de votre onglet existe dans Teams et non en dehors de Teams.

## <a name="show-a-native-loading-indicator"></a>Affichage d'un indicateur de chargement natif

À partir du [schéma de manifeste v1.7](../../../resources/schema/manifest-schema.md), vous pouvez fournir [un indicateur de chargement natif](../../../resources/schema/manifest-schema.md#showloadingindicator). Par exemple, [page de contenu de l’onglet](#integrate-your-code-with-teams), [page de configuration](configuration-page.md), [page de suppression](removal-page.md)et [modules de tâches dans les onglets](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
>
> * Le comportement sur les clients mobiles n’est pas configurable via la propriété d’indicateur de chargement natif. Les clients mobiles affichent cet indicateur par défaut dans les pages de contenu et les modules de tâche basés sur iframe. Cet indicateur sur mobile s’affiche lorsqu’une demande est effectuée pour extraire du contenu et est ignorée dès que la demande est terminée.

Si vous indiquez `showLoadingIndicator : true`  dans le manifeste de votre application, la configuration de l’onglet, le contenu, les pages de suppression et tous les modules de tâche basés sur iframe doivent suivre ces étapes :

Pour afficher l’indicateur de chargement :

1. Ajoutez `"showLoadingIndicator": true` à votre manifeste.
1. Appel `microsoftTeams.initialize();`.
1. Comme étape **obligatoire**, appelez `microsoftTeams.appInitialization.notifySuccess()` pour notifier aux équipes que votre application a été chargée avec succès. Teams masque ensuite l’indicateur de chargement, le cas échéant. Si `notifySuccess` n’est pas appelé dans les 30 secondes, il est supposé que votre application a expiré et qu’un écran d’erreur avec une option de nouvelle tentative s’affiche.
1. **éventuellement**, si vous êtes prêt à imprimer à l’écran et que vous souhaitez charger tardivement le reste du contenu de votre application, vous pouvez masquer manuellement l’indicateur de chargement en appelant `microsoftTeams.appInitialization.notifyAppLoaded();`.
1. Si le chargement de votre application échoue, vous pouvez appeler `microsoftTeams.appInitialization.notifyFailure(reason);` pour informer Teams qu’une erreur s’est produite. Un écran d’erreur s’affiche pour l’utilisateur. Le code suivant fournit un exemple de raisons d’échec d’application :

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md)

## <a name="see-also"></a>Voir aussi

* [onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Déploiement du lien des onglets et vue de scène](~/tabs/tabs-link-unfurling.md)
* [Créer une page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [DevTools pour les onglets Microsoft Teams](~/tabs/how-to/developer-tools.md)
