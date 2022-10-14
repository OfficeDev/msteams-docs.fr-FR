---
title: Onglets sur les appareils mobiles
description: Découvrez comment l’onglet fonctionne sur les clients Microsoft Teams Android et iOS (mobile), leur authentification, leur connexion à faible bande passante, leurs tests ou leur distribution.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 0dbb74d5c2854897f82708aa83a0c49df4f28890
ms.sourcegitcommit: bd96080c78f25eb0a67ce176df5e255be348f7b1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/14/2022
ms.locfileid: "68575767"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

Lorsque vous créez une application Microsoft Teams qui inclut un onglet, vous devez tester le fonctionnement de votre onglet sur les clients Microsoft Teams Android et iOS. Cet article décrit certains des scénarios clés que vous devez prendre en compte.

Si vous choisissez d’afficher l’onglet de votre canal ou groupe sur les clients mobiles Teams, la [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) configuration doit avoir une valeur pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, vous devez suivre les instructions relatives aux onglets sur les appareils mobiles dans cet article lors de la création de vos onglets.

Les applications [distribuées via le magasin Teams](~/concepts/deploy-and-publish/appsource/publish.md) ont un processus d’approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Fonctionnalité d’application** | **Comportement si l’application est approuvée** | **Comportement si l’application n’est pas approuvée** |
| --- | --- | --- |
| **Onglets personnels** | L’application apparaît dans la barre inférieure des clients mobiles. Les onglets s’ouvrent dans le client Teams. | L’application n’apparaît pas dans la barre inférieure des clients mobiles. |
| **Onglets canal et groupe** | L’onglet s’ouvre dans le client Teams à l’aide de `contentUrl`. | L’onglet s’ouvre dans un navigateur en dehors du client Teams à l’aide `websiteUrl`de . |

> [!NOTE]
>
> * Les applications soumises à [AppSource](https://appsource.microsoft.com) pour publication sur Teams sont évaluées automatiquement pour la réactivité mobile. Pour toutes les requêtes, contactez teamsubm@microsoft.com.
> * Pour toutes les applications qui ne sont pas distribuées via AppSource, les onglets s’ouvrent dans une vue web in-app dans les clients Teams par défaut et aucun processus d’approbation distinct n’est requis.
> * Le comportement par défaut des applications s’applique uniquement s’il est distribué via le magasin Teams. Par défaut, tous les onglets s’ouvrent dans le client Teams.
> * Pour lancer une évaluation de votre application pour la convivialité mobile, contactez teamsubm@microsoft.com avec les détails de votre application.

## <a name="authentication"></a>Authentification

Pour que l’authentification fonctionne sur des clients mobiles, vous devez mettre à niveau votre Kit de développement logiciel (SDK) JavaScript Teams vers au moins la version 1.4.1.

## <a name="low-bandwidth-and-intermittent-connections"></a>Bande passante faible et connexions intermittentes

Les clients mobiles fonctionnent avec une bande passante faible et des connexions intermittentes. Votre application doit gérer les délais d’expiration de manière appropriée en fournissant un message contextuel à l’utilisateur. Vous devez également utiliser des indicateurs de progression pour fournir des commentaires à vos utilisateurs sur les processus de longue durée.

## <a name="testing-on-mobile-clients"></a>Test sur les clients mobiles

Vous devez vérifier que votre onglet fonctionne correctement sur les appareils mobiles de différentes tailles et qualités. Pour les appareils Android, vous pouvez utiliser [DevTools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant son exécution. Il est recommandé de tester sur des appareils hautes et faibles performances, y compris une tablette.

## <a name="distribution"></a>Distribution

Les applications répertoriées dans le magasin Teams doivent être approuvées pour une utilisation mobile afin de fonctionner correctement dans le client mobile Teams. La disponibilité et le comportement des onglets dépendent de l’approbation ou non de votre application.

### <a name="apps-on-teams-store-approved-for-mobile"></a>Applications sur le magasin Teams approuvées pour les appareils mobiles

Le tableau suivant décrit la disponibilité et le comportement de l’onglet lorsque l’application est répertoriée dans le magasin Teams et approuvée pour une utilisation mobile :

|Fonctionnalité   |Disponibilité mobile ?   |Comportement mobile|
|----------|-----------|------------|
|Canal <br /> onglet et groupe|Oui|L’onglet s’ouvre dans le client mobile Teams à l’aide de la configuration de `contentUrl` votre application.|
|Application personnelle|Oui|Chaque onglet de l’onglet application personnelle s’ouvre dans le client mobile Teams à l’aide de sa configuration respective `contentUrl` .|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Applications sur le magasin Teams non approuvées pour les appareils mobiles

Le tableau suivant décrit la disponibilité et le comportement de l’onglet lorsque l’application est répertoriée sur le magasin Teams, mais qu’elle n’est pas approuvée pour une utilisation mobile :

| Fonctionnalité | Disponibilité mobile ? | Comportement mobile |
|----------|-----------|------------|
|Onglet Canal et groupe|Oui|L’onglet s’ouvre dans le navigateur par défaut de l’appareil au lieu du client mobile Teams à l’aide de la configuration de `websiteUrl` votre application, qui doit également être incluse dans la [fonction](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace) de `setSettings()` votre code source. Toutefois, les utilisateurs peuvent afficher l’onglet dans le client mobile Teams en sélectionnant **Plus** en regard de l’application et en choisissant **Ouvrir**, ce qui déclenche la configuration de `contentUrl` votre application.|
|Application personnelle|Non|Non applicable|

> [!NOTE]
> Les messages du bot sont affichés dans la section de conversation si une application mobile dispose à la fois des fonctionnalités du bot et de l’onglet.
>
> Lorsque vous sélectionnez **Chat** de l’application bot et sélectionnez **Plus (...)**, vous ne pouvez pas voir la fonctionnalité d’onglet de cette application dans la liste. Toutefois, si vous sélectionnez **Plus (...)** dans le coin inférieur droit de la section **Conversation** , vous pouvez afficher l’application onglet avec un lien vers la fonctionnalité d’application bot de cette application.

### <a name="apps-not-on-teams-store"></a>Applications qui ne sont pas sur le magasin Teams

Si vous chargez ou publiez votre application dans le catalogue d’applications d’une organisation, le comportement de l’onglet est le même que celui des applications du Magasin Teams approuvées par Microsoft pour les appareils mobiles.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Obtenir un contexte Teams pour votre onglet](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>Voir aussi

* [Instructions de conception de tabulation](~/tabs/design/tabs.md)
* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Planifier Teams mobile - Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
