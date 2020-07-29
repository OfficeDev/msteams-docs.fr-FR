---
title: Créer une page de contenu
author: laujan
description: ''
keywords: onglets teams groupe de canaux configurable statique
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: 49cd771c45bc3c4f91a7ab5f38beaf01da712544
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434488"
---
# <a name="create-a-content-page-for-your-tab"></a>Créer une page de contenu pour votre onglet

Une page de contenu est une page Web qui s’affiche dans le client Teams. En règle générale, il s’agit des éléments suivants :

* Onglet personnalisé d’étendue personnelle : cette instance de contenu est la première page rencontrée par l’utilisateur.
* Un onglet personnalisé canal/groupe-une fois que l’utilisateur épingle et configure l’onglet dans le contexte approprié, la page de contenu s’affiche.
* Un [module de tâches](~/task-modules-and-cards/what-are-task-modules.md) : vous pouvez créer une page de contenu et l’incorporer en tant que WebView à l’intérieur d’un module de tâches. La page s’affiche dans le menu contextuel modal.

Cet article est spécifique à l’utilisation des pages de contenu en tant qu’onglets ; Toutefois, la majorité des conseils s’appliquent indépendamment de la présentation de la page de contenu à l’utilisateur final.

## <a name="tab-content-and-style-guidelines"></a>Contenu des onglets et règles de style

L’objectif général de votre onglet doit être de fournir un accès à du contenu pertinent et attrayant qui a une valeur pratique et un objectif évident. Cela ne signifie pas que vous devez vous conformer à un style agréable, mais vous devez vous concentrer sur la réduction du courrier non trié en rendant le design de votre onglet propre, intuitif et le contenu immersif. Voir le [contenu et les conversations, en même temps à l’aide des onglets et de l’aide sur](~/tabs/design/tabs.md) le [processus d’approbation des applications Microsoft teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)

## <a name="integrate-your-code-with-teams"></a>Intégration de votre code à teams

Pour que votre page s’affiche dans Teams, vous devez inclure le [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) et inclure un appel à `microsoftTeams.initialize()` après le chargement de votre page. Voici comment votre page et le client teams communiquent :

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
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

## <a name="accessing-additional-content"></a>Accès à du contenu supplémentaire

### <a name="using-the-sdk-to-interact-with-teams"></a>Utilisation du kit de développement logiciel (SDK) pour interagir avec teams

Le [Kit de développement logiciel (SDK) du client teams](~/tabs/how-to/using-teams-client-sdk.md) fournit de nombreuses fonctions supplémentaires que vous pouvez trouver utiles lorsque vous développez votre page de contenu.

### <a name="deep-links"></a>Liens profonds

Vous pouvez créer des liens approfondis vers des entités dans Teams. En règle générale, ces éléments sont utilisés pour créer des liens qui naviguent vers le contenu et les informations au sein de votre onglet. Voir [créer des liens détaillés vers du contenu et des fonctionnalités dans Microsoft teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Modules de tâches

Un module de tâches est une expérience de type popup modale que vous pouvez déclencher à partir de votre onglet. généralement dans une page de contenu, vous ne souhaitez pas parcourir votre utilisateur sur plusieurs pages. Au lieu de cela, vous utiliserez des modules de tâches pour présenter des formulaires permettant de collecter des informations supplémentaires, en affichant les détails d’un élément dans une liste ou à tout autre moment pour présenter à l’utilisateur des informations supplémentaires. Les modules de tâches eux-mêmes peuvent être des pages de contenu supplémentaires ou être entièrement créés à l’aide de cartes adaptatives. Pour obtenir des informations complètes, voir [utilisation des modules de tâches dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md) .

### <a name="valid-domains"></a>Domaines valides

Assurez-vous que tous les domaines d’URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau dans votre [manifeste](~/concepts/build-and-test/apps-package.md). Pour plus d’informations, consultez la rubrique [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence de schéma de manifeste. Toutefois, gardez à l’esprit que la fonctionnalité principale de votre onglet existe dans teams et non en dehors de teams.

## <a name="show-a-native-loading-indicator"></a>Afficher un indicateur de chargement natif

À partir [du schéma de manifeste version 1.7](../../../resources/schema/manifest-schema.md), vous pouvez fournir un indicateur de [chargement natif](../../../resources/schema/manifest-schema.md#showloadingindicator) où le contenu de votre site Web est chargé dans Teams, par exemple, page de contenu de l' [onglet](#integrate-your-code-with-teams), page de [configuration](configuration-page.md), [page de suppression](removal-page.md) et [modules de tâches dans les onglets](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
> Si vous indiquez `"showLoadingIndicator : true` dans votre manifeste d’application, toutes les pages de configuration d’onglet, de contenu et de suppression, ainsi que tous les modules de tâches basés sur iframe doivent suivre le protocole obligatoire, ci-dessous :

1. Pour afficher l’indicateur de chargement, ajoutez `"showLoadingIndicator": true` à votre manifeste. 
2. N’oubliez pas d’appeler `microsoftTeams.initialize();` .
3. **Facultatif**. Si vous êtes prêt à imprimer à l’écran et si vous souhaitez charger en différé le reste du contenu de votre application, vous pouvez masquer manuellement l’indicateur de chargement en appelant`microsoftTeams.appInitialization.notifyAppLoaded();`
4. **Obligatoire**. Enfin, appelez `microsoftTeams.appInitialization.notifySuccess()` pour avertir les équipes que votre application a été chargée avec succès. Le cas échéant, teams masque l’indicateur de chargement. Si `notifySuccess` n’est pas appelé dans les 30 secondes, il est supposé que votre application a expiré et un écran d’erreur contenant une option Retry apparaît.
5. Si votre application ne se charge pas, vous pouvez appeler `microsoftTeams.appInitialization.notifyFailure(reason);` pour informer les équipes qu’une erreur s’est produite. Un écran d’erreur s’affiche ensuite à l’utilisateur :

```typescript
``
/* List of failure reasons */
export const enum FailedReason {
    AuthFailed = "AuthFailed",
    Timeout = "Timeout",
    Other = "Other"
}
```
>
