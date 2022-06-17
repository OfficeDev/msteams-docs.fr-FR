---
title: Onglets sur les appareils mobiles
description: Dans ce module, découvrez comment implémenter des onglets sur Microsoft Teams mobile, leur authentification, leur connexion à faible bande passante, les tests sur les clients mobiles, la distribution, etc.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: da9757ee0153b3f2fe80e576e156f45bc90a15cd
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144264"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

Lorsque vous créez une application Microsoft Teams qui inclut un onglet, vous devez tester le fonctionnement de votre onglet sur les clients Android et iOS Microsoft Teams. Cet article décrit certains des scénarios clés que vous devez prendre en compte.

Si vous choisissez d’afficher l’onglet canal ou groupe sur Teams clients mobiles, la [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) configuration doit avoir une valeur pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, vous devez suivre les instructions relatives aux onglets sur les appareils mobiles dans cet article lors de la création de vos onglets.

Les applications [distribuées par le biais du magasin Teams](~/concepts/deploy-and-publish/appsource/publish.md) ont un processus d’approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Fonctionnalité d’application** | **Comportement si l’application est approuvée** | **Comportement si l’application n’est pas approuvée** |
| --- | --- | --- |
| **Onglets personnels** | L’application apparaît dans la barre inférieure des clients mobiles. Onglets ouverts dans le client Teams. | L’application n’apparaît pas dans la barre inférieure des clients mobiles. |
| **Onglets canal et groupe** | L’onglet s’ouvre dans le client Teams à l’aide de `contentUrl`. | L’onglet s’ouvre dans un navigateur en dehors du client Teams à l’aide `websiteUrl`de . |

> [!NOTE]
>
> * Les applications soumises à [AppSource](https://appsource.microsoft.com) pour publication sur Teams sont évaluées automatiquement pour la réactivité mobile. Pour toutes les requêtes, contactez teamsubm@microsoft.com.
> * Pour toutes les applications qui ne sont pas distribuées via AppSource, les onglets s’ouvrent dans une vue web dans l’application dans les clients Teams par défaut et aucun processus d’approbation distinct n’est requis.
> * Le comportement par défaut des applications s’applique uniquement s’il est distribué par le biais du magasin Teams. Par défaut, tous les onglets s’ouvrent dans le client Teams.
> * Pour lancer une évaluation de votre application pour la convivialité mobile, contactez teamsubm@microsoft.com avec les détails de votre application.

## <a name="authentication"></a>Authentification

Pour que l’authentification fonctionne sur des clients mobiles, vous devez vous mettre à niveau Teams SDK JavaScript vers au moins la version 1.4.1.

## <a name="low-bandwidth-and-intermittent-connections"></a>Bande passante faible et connexions intermittentes

Les clients mobiles fonctionnent avec une bande passante faible et des connexions intermittentes. Votre application doit gérer les délais d’expiration de manière appropriée en fournissant un message contextuel à l’utilisateur. Vous devez également utiliser des indicateurs de progression pour fournir des commentaires à vos utilisateurs sur les processus de longue durée.

## <a name="testing-on-mobile-clients"></a>Test sur les clients mobiles

Vous devez vérifier que votre onglet fonctionne correctement sur les appareils mobiles de différentes tailles et qualités. Pour Android appareils, vous pouvez utiliser [DevTools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant son exécution. Il est recommandé de tester sur des appareils hautes et faibles performances, y compris une tablette.

## <a name="distribution"></a>Distribution

Les applications répertoriées dans le magasin Teams doivent être approuvées pour une utilisation mobile afin de fonctionner correctement dans le client mobile Teams. La disponibilité et le comportement des onglets dépendent de l’approbation ou non de votre application.

### <a name="apps-on-teams-store-approved-for-mobile"></a>Applications sur Teams store approuvées pour les appareils mobiles

Le tableau suivant décrit la disponibilité et le comportement des onglets lorsque l’application est répertoriée dans le magasin Teams et approuvée pour une utilisation mobile :

|Fonctionnalité   |Disponibilité mobile ?   |Comportement mobile|
|----------|-----------|------------|
|Canal <br /> onglet et groupe|Oui|L’onglet s’ouvre dans le Teams client mobile à l’aide de la configuration de `contentUrl` votre application.|
|Application personnelle|Oui|Chaque onglet de l’onglet application personnelle s’ouvre dans le client mobile Teams à l’aide de sa configuration respective`contentUrl`.|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Applications sur Teams magasin non approuvées pour les appareils mobiles

Le tableau suivant décrit la disponibilité et le comportement des onglets lorsque l’application est répertoriée dans le magasin Teams, mais non approuvée pour une utilisation mobile :

| Fonctionnalité | Disponibilité mobile ? | Comportement mobile |
|----------|-----------|------------|
|Onglet Canal et groupe|Oui|L’onglet s’ouvre dans le navigateur par défaut de l’appareil au lieu du client mobile Teams à l’aide de la configuration de `websiteUrl` votre application, qui doit également être incluse dans la [fonction](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace) de `setSettings()` votre code source. Toutefois, les utilisateurs peuvent afficher l’onglet dans le client mobile Teams en sélectionnant **Plus** en regard de l’application et en choisissant **Ouvrir**, ce qui déclenche la configuration de `contentUrl` votre application.|
|Application personnelle|Non|Non applicable|

### <a name="apps-not-on-teams-store"></a>Applications qui ne sont pas sur Teams store

Si vous chargez ou publiez votre application dans le catalogue d’applications d’une organisation, le comportement de l’onglet est le même que Teams applications du Store approuvées par Microsoft pour les appareils mobiles.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Obtenir un contexte Teams pour votre onglet](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>Voir aussi

* [Instructions de conception de tabulation](~/tabs/design/tabs.md)
* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Planifier Teams mobile - Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
