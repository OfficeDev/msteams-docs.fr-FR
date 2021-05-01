---
title: Créer une page de contenu
author: laujan
description: Comment créer une page de contenu
keywords: 'onglets teams : canal de groupe configurable statique'
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8dcaf47c527ce61e080d51a322b841dd8cf61cc3
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101834"
---
# <a name="create-a-content-page-for-your-tab"></a>Créer une page de contenu pour votre onglet

Une page de contenu est une page web qui est rendue dans le client Teams client. En règle générale, ces éléments font partie des éléments ci-après :

* Onglet personnalisé d'étendue personnelle : dans ce cas, la page de contenu est la première page que l'utilisateur rencontre.
* Onglet personnalisé canal/groupe : une fois que l'utilisateur épingle et configure l'onglet dans le contexte approprié, la page de contenu s'affiche.
* Module [de tâche](~/task-modules-and-cards/what-are-task-modules.md) : vous pouvez créer une page de contenu et l'incorporer en tant que vue web à l'intérieur d'un module de tâche. La page s'restituera à l'intérieur de la fenêtre popup modale.

Cet article est spécifique à l'utilisation de pages de contenu en tant qu'onglets ; Toutefois, la majorité des conseils présentés ici s'appliquent, quelle que soit la façon dont la page de contenu est présentée à l'utilisateur final.

## <a name="tab-content-and-design-guidelines"></a>Recommandations en matière de contenu d'onglet et de conception

L'objectif global de votre onglet doit être de fournir un accès à un contenu significatif et attrayant qui a une valeur pratique et un objectif évident. Cela ne signifie pas que vous devez éviter un style agréable, mais vous devez vous concentrer sur la réduction de l'encombrement en rendant votre conception d'onglet propre, intuitive de navigation et immersif de contenu.

Pour plus d'informations, consultez les recommandations en matière de [conception](~/tabs/design/tabs.md) [d'onglets et Microsoft Teams de validation du store](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)

## <a name="integrate-your-code-with-teams"></a>Intégrer votre code avec Teams

Pour que votre page s'affiche Teams, vous devez inclure le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page. C'est ainsi que votre page et le client Teams communiquent :

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

### <a name="using-the-sdk-to-interact-with-teams"></a>Utilisation du SDK pour interagir avec les Teams

Le [Teams SDK JavaScript client](~/tabs/how-to/using-teams-client-sdk.md) fournit de nombreuses fonctions supplémentaires qui peuvent vous être utiles lors du développement de votre page de contenu.

### <a name="deep-links"></a>Liens profonds

Vous pouvez créer des liens profonds vers des entités dans Teams. En règle générale, ils sont utilisés pour créer des liens qui naviguent vers le contenu et les informations dans votre onglet. Voir [Créer des liens profonds vers du contenu et des fonctionnalités dans Microsoft Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Modules de tâche

Un module de tâche est une expérience popup modale que vous pouvez déclencher à partir de votre onglet. En règle générale, dans une page de contenu, vous ne souhaitez pas parcourir plusieurs pages pour votre utilisateur. Au lieu de cela, vous allez utiliser des modules de tâche pour présenter des formulaires pour recueillir des informations supplémentaires, afficher les détails d'un élément dans une liste ou toute autre fois que vous devez présenter à l'utilisateur des informations supplémentaires. Les modules de tâche eux-mêmes peuvent être des pages de contenu supplémentaires ou créés entièrement à l'aide de cartes adaptatives. Pour plus [d'informations, voir Utilisation des modules](~/task-modules-and-cards/task-modules/task-modules-tabs.md) de tâche dans les onglets.

### <a name="valid-domains"></a>Domaines valides

Assurez-vous que tous les domaines d'URL utilisés dans vos onglets sont inclus dans le `validDomains` tableau de votre [manifeste.](~/concepts/build-and-test/apps-package.md) Pour plus d'informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans la référence du schéma de manifeste. Toutefois, n'oubliez pas que les fonctionnalités de base de votre onglet existent au sein Teams et non en dehors de Teams.

## <a name="reorder-static-personal-tabs"></a>Réordesser les onglets personnels statiques

À partir de la version de manifeste 1.7, les développeurs peuvent réorganiser tous les onglets de leur application personnelle. En particulier, un développeur peut déplacer l'onglet de conversation du *bot,* qui est toujours en première position par défaut, n'importe où dans l'en-tête de l'onglet de l'application personnelle. Nous avons déclaré deux mots clés entityId d'onglet réservé, *conversations* et *à propos de*.

Si vous créez un bot avec une *étendue* personnelle, il s'affiche par défaut au premier onglet d'une application personnelle. Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, *conversations*. *L'onglet conversation* s'affiche sur le web ou sur le Bureau en fonction de l'endroit où vous ajoutez l'onglet *de conversation* dans le `staticTabs` tableau. 

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

À partir du schéma de manifeste [v1.7,](../../../resources/schema/manifest-schema.md)vous pouvez fournir un indicateur de chargement [natif](../../../resources/schema/manifest-schema.md#showloadingindicator) partout où votre contenu web est chargé dans Teams, par exemple, page de contenu d'onglet, [page](#integrate-your-code-with-teams) [de configuration,](configuration-page.md) [page](removal-page.md) de suppression et modules de tâche dans les [onglets.](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)

> [!NOTE]
> 1. Le comportement sur les clients mobiles n'est pas configurable via cette propriété de manifeste. Les clients mobiles montrent un indicateur de chargement natif par défaut sur les pages de contenu et les modules de tâche iframe. Cet indicateur sur mobile s'affiche lorsqu'une demande d'extraction de contenu est effectuée et est rejetée dès que la demande est terminée.
> 2. Si vous indiquez dans le manifeste de votre application, toutes les pages de configuration, de contenu et de suppression d'onglets et tous les modules de tâche iframe doivent respecter le protocole obligatoire  `"showLoadingIndicator : true`  ci-dessous :


1. Pour afficher l'indicateur de chargement, `"showLoadingIndicator": true` ajoutez-le à votre manifeste. 
2. N'oubliez pas d'appeler `microsoftTeams.initialize();` .
3. **Facultatif**. Si vous êtes prêt à imprimer à l'écran et que vous souhaitez charger différée le reste du contenu de votre application, vous pouvez masquer manuellement l'indicateur de chargement en appelant `microsoftTeams.appInitialization.notifyAppLoaded();`
4. **Obligatoire**. Enfin, appelez `microsoftTeams.appInitialization.notifySuccess()` pour informer Teams que votre application a été correctement chargée. Teams masque ensuite l'indicateur de chargement, le cas échéant. Si elle n'est pas appelée dans les 30 secondes, elle est supposée que votre application a été hors délai et qu'un écran d'erreur avec une option de nouvelle tentative  `notifySuccess`  s'affiche.
5. Si le chargement de votre application échoue, vous pouvez appeler Teams `microsoftTeams.appInitialization.notifyFailure(reason);` savoir qu'une erreur s'est produite. Un écran d'erreur s'affiche ensuite pour l'utilisateur :

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
