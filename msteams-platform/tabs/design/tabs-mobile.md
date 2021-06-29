---
title: Onglets sur les appareils mobiles
description: Décrit les considérations pour les développeurs pour l’implémentation d’onglets sur Microsoft Teams mobile.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 5053160f2456a5d1c5f68cb74ea3ccc5c5eabca5
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179719"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

Lorsque vous construisez une application Microsoft Teams qui inclut un onglet, vous devez tester le fonctionnement de votre onglet sur les clients Microsoft Teams Android et iOS. Cet article décrit certains des scénarios clés que vous devez prendre en considération.

Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur Teams clients mobiles, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, vous devez suivre les instructions pour les onglets sur les appareils mobiles de cet article lors de la création de vos onglets.

Les [applications distribuées via Teams store ont](~/concepts/deploy-and-publish/appsource/publish.md) un processus d’approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Fonctionnalité de l’application** | **Comportement si l’application est approuvée** | **Comportement si l’application n’est pas approuvée** |
| --- | --- | --- |
| **Onglets personnels** | L’application apparaît dans la barre inférieure des clients mobiles. Les onglets s’ouvrent dans Teams client. | L’application n’apparaît pas dans la barre inférieure des clients mobiles. |
| **Onglets de canal et de groupe** | L’onglet s’ouvre dans le Teams client à l’aide `contentUrl` de . | L’onglet s’ouvre dans un navigateur en dehors du Teams client à `websiteUrl` l’aide. |

> [!NOTE]
> * Les applications soumises à [AppSource](https://appsource.microsoft.com) pour publication sur Teams sont évaluées automatiquement pour la réactivité mobile. Pour toutes les requêtes, teamsubm@microsoft.com.
> * Pour toutes les applications qui ne sont pas distribuées via AppSource, les onglets s’ouvrent dans une vue web dans l’application au sein des clients Teams par défaut et aucun processus d’approbation distinct n’est requis.
> * Le comportement par défaut des applications s’applique uniquement s’il est distribué via Teams store. Par défaut, tous les onglets s’ouvrent dans le client Teams client.
> * Pour lancer une évaluation de votre application pour la convivialité mobile, teamsubm@microsoft.com les détails de votre application.

## <a name="authentication"></a>Authentification

Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau Teams SDK JavaScript vers au moins la version 1.4.1.

## <a name="low-bandwidth-and-intermittent-connections"></a>Bande passante faible et connexions intermittentes

Les clients mobiles fonctionnent avec une bande passante faible et des connexions intermittentes. Votre application doit gérer les délai d’accès de manière appropriée en fournissant un message contextuel à l’utilisateur. Vous devez également utiliser des indicateurs de progression pour fournir des commentaires à vos utilisateurs pour tout processus de longue durée.

## <a name="testing-on-mobile-clients"></a>Test sur les clients mobiles

Vous devez vérifier que votre onglet fonctionne correctement sur des appareils mobiles de différentes tailles et qualités. Pour les appareils Android, vous pouvez utiliser [DevTools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant son exécution. Il est recommandé de tester sur les appareils hautes et faibles performances, y compris une tablette.

## <a name="distribution"></a>Distribution

Les applications répertoriées dans Teams store doivent être approuvées pour que l’utilisation mobile fonctionne correctement dans Teams client mobile. La disponibilité et le comportement des onglets dépendent de l’approbation ou non de votre application.

### <a name="apps-on-teams-store-approved-for-mobile"></a>Applications sur Teams store approuvées pour les appareils mobiles

Le tableau suivant décrit la disponibilité et le comportement des onglets lorsque l’application est répertoriée dans le Teams store et approuvée pour une utilisation mobile :

|Fonctionnalité   |Disponibilité mobile ?   |Comportement mobile|
|----------|-----------|------------|
|Canal <br /> et onglet groupe|Oui|L’onglet s’ouvre Teams client mobile à l’aide de la configuration de votre `contentUrl` application.|
|Application personnelle|Oui|Chaque onglet de l’onglet de l’application personnelle s’ouvre Teams client mobile en utilisant sa `contentUrl` configuration respective.|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Applications sur Teams store non approuvées pour appareils mobiles

Le tableau suivant décrit la disponibilité et le comportement des onglets lorsque l’application est répertoriée dans le magasin Teams mais qu’elle n’est pas approuvée pour une utilisation mobile :

| Fonctionnalité | Disponibilité mobile ? | Comportement mobile |
|----------|-----------|------------|
|Onglet Canal et groupe|Oui|L’onglet s’ouvre dans le navigateur par défaut de l’appareil au lieu du client mobile Teams à l’aide de la configuration de votre application, qui doit également être incluse dans la fonction de `websiteUrl` votre code `setSettings()` [source.](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true) Toutefois, les utilisateurs peuvent afficher l’onglet dans  le client mobile Teams en sélectionnant Plus en regard de l’application et en choisissant **Ouvrir,** ce qui déclenche la configuration de votre `contentUrl` application.|
|Application personnelle|Non|Non applicable|

### <a name="apps-not-on-teams-store"></a>Applications non stockées dans Teams store

Si vous chargez une version de votre application ou publiez-la dans le catalogue d’applications d’une organisation, le comportement des onglets est le même que celui des applications Teams store approuvées par Microsoft pour appareils mobiles.

## <a name="see-also"></a>Voir aussi

* [Recommandations en matière de conception d’onglets](~/tabs/design/tabs.md)
* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Obtenir un contexte Teams pour votre onglet](~/tabs/how-to/access-teams-context.md)
