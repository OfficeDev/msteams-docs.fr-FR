---
title: Créer une page de contenu
author: laujan
description: comment créer une page de contenu
keywords: équipes onglets canal de groupe configurable statique
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 136160cb9154d62be40d8e29075ac1fc86135a6b
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566676"
---
# <a name="create-a-content-page-for-your-tab"></a>Créez une page de contenu pour votre onglet

Une page de contenu est une page Web qui est rendue dans le Teams client. En règle générale, ceux-ci font partie de:

* Onglet personnalisé à portée personnelle : dans ce cas, la page de contenu est la première page que l’utilisateur rencontre.
* Onglet personnalisé canal/groupe : après que l’utilisateur épingle et configure l’onglet dans le contexte approprié, la page de contenu s’affiche.
* Un [module de tâches :](~/task-modules-and-cards/what-are-task-modules.md)Vous pouvez créer une page de contenu et l’intégrer comme une webview à l’intérieur d’un module de tâches. La page sera rendue à l’intérieur du popup modal.

Cet article est spécifique à l’utilisation de pages de contenu comme onglets; toutefois, la majorité des directives ici s’appliqueraient indépendamment de la façon dont la page de contenu est présentée à l’utilisateur final.

## <a name="tab-content-and-design-guidelines"></a>Lignes directrices sur le contenu et la conception des onglets

L’objectif global de votre onglet devrait être de fournir l’accès à un contenu significatif et engageant qui a une valeur pratique et un but évident. Cela ne signifie pas que vous devriez renoncer à un style agréable, mais vous devez vous concentrer sur la minimisation de l’encombrement en rendant votre conception d’onglet propre, navigation intuitive, et le contenu immersif.

Pour plus d’informations, consultez les lignes [directrices de conception des onglets](~/tabs/design/tabs.md) [et les Microsoft Teams de validation des magasins](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)

## <a name="integrate-your-code-with-teams"></a>Intégrez votre code à Teams

Pour que votre page s’affiche en Teams, vous devez [inclure le client JavaScript Microsoft Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et inclure un appel `microsoftTeams.initialize()` après que votre page se charge. C’est ainsi que votre page et Teams client communiquent :

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

### <a name="using-the-sdk-to-interact-with-teams"></a>Utiliser le SDK pour interagir avec Teams

Le [Teams client JavaScript SDK fournit de nombreuses](~/tabs/how-to/using-teams-client-sdk.md) fonctions supplémentaires que vous pouvez trouver utiles lors du développement de votre page de contenu.

### <a name="deep-links"></a>Liens profonds

Vous pouvez créer des liens profonds avec des entités en Teams. En règle générale, ceux-ci sont utilisés pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Pour plus d’informations, [voir Créer des liens profonds vers le contenu et les fonctionnalités dans Microsoft Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Modules de tâches

Un module de tâche est une expérience modale popup-like que vous pouvez déclencher à partir de votre onglet. En règle générale, dans une page de contenu, vous ne souhaitez pas naviguer sur votre utilisateur à travers plusieurs pages. Au lieu de cela, vous utiliserez des modules de tâches pour présenter des formulaires pour recueillir des informations supplémentaires, afficher les détails d’un élément dans une liste, ou tout autre moment où vous devez présenter à l’utilisateur des informations supplémentaires. Les modules de tâches eux-mêmes peuvent être des pages de contenu supplémentaires, ou créés complètement à l’aide de cartes adaptatives. Voir Utilisation [de modules de tâches dans les onglets pour](~/task-modules-and-cards/task-modules/task-modules-tabs.md) des informations complètes.

### <a name="valid-domains"></a>Domaines valides

Assurez-vous que tous les domaines URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau dans votre [manifeste](~/concepts/build-and-test/apps-package.md). Pour plus d’informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence manifeste du schéma. Cependant, n’oubliez pas que la fonctionnalité de base de votre onglet existe dans Teams et non en dehors de Teams.

## <a name="reorder-static-personal-tabs"></a>Réorganiser les onglets personnels statiques

À partir de la version manifeste 1.7, les développeurs peuvent réorganiser tous les onglets de leur application personnelle. En particulier, un développeur peut déplacer l’onglet *de chat bot,* qui est toujours par défaut à la première position, n’importe où dans l’en-tête de l’onglet application personnelle. Nous avons déclaré deux mots clés, conversations et *environ* *.*

Si vous créez un bot avec une *portée* personnelle, il s’affichera dans la première position de l’onglet dans une application personnelle par défaut. Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, *conversations*. *L’onglet conversation* s’affiche sur le Web ou le bureau en fonction de l’endroit où vous ajoutez *l’onglet conversation* dans le `staticTabs` tableau. 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a>Afficher un indicateur de chargement natif

En commençant [par le schéma manifeste v1.7](../../../resources/schema/manifest-schema.md), vous pouvez fournir un indicateur de chargement natif [partout](../../../resources/schema/manifest-schema.md#showloadingindicator) où votre contenu Web est chargé dans Teams. Par exemple, page [de contenu d’onglet,](#integrate-your-code-with-teams) [page de configuration,](configuration-page.md) [page de suppression,](removal-page.md) [et modules de tâche dans les onglets.](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)

> [!NOTE]
> * Le comportement sur les clients mobiles n’est pas configurable grâce à cette propriété manifeste. Les clients mobiles affichent un indicateur de chargement natif par défaut sur toutes les pages de contenu et les modules de tâches basés sur iframe. Cet indicateur sur mobile s’affiche lorsqu’une demande est faite pour récupérer du contenu et est rejeté dès que la demande est terminée.
> * Si vous indiquez  `"showLoadingIndicator : true`  dans votre manifeste d’application, alors toutes les pages de configuration, de contenu et de suppression d’onglets et tous les modules de tâches basés sur iframe doivent suivre le protocole obligatoire, ci-dessous :

**Pour afficher l’indicateur de chargement**

* Ajoutez `"showLoadingIndicator": true` à votre manifeste. 
* N’oubliez pas d’appeler `microsoftTeams.initialize();` .
* **Facultatif**: Si vous êtes prêt à imprimer à l’écran et souhaitez charger paresseux le reste du contenu de votre application, vous pouvez masquer manuellement l’indicateur de chargement en appelant `microsoftTeams.appInitialization.notifyAppLoaded();`
* **Obligatoire**: Enfin, appelez `microsoftTeams.appInitialization.notifySuccess()` pour informer Teams que votre application a chargé avec succès. Teams cachera alors l’indicateur de chargement le cas échéant. Si  `notifySuccess`  elle n’est pas appelée dans les 30 secondes, on suppose que votre application est expirée et qu’un écran d’erreur avec une option de nouvelle tentative s’affiche.
* Si votre application ne se charge pas, vous pouvez appeler pour `microsoftTeams.appInitialization.notifyFailure(reason);` vous faire savoir Teams’il y a eu une erreur. Un écran d’erreur sera alors affiché à l’utilisateur :

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
