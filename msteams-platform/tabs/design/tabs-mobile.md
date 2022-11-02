---
title: Onglets sur les appareils mobiles
description: Découvrez comment l’onglet fonctionne sur les clients Android et iOS Microsoft Teams (mobile), leur authentification, leur connexion à faible bande passante, les tests ou la distribution.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 8dac56cd609466c116f39baf5dc9d9a7970645ec
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820079"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

Lorsque vous créez une application Microsoft Teams qui inclut un onglet, vous devez tester le fonctionnement de votre onglet sur les clients Microsoft Teams Android et iOS. Cet article décrit certains des scénarios clés que vous devez prendre en compte.

Si vous choisissez d’afficher l’onglet de votre canal ou groupe sur les clients mobiles Teams, la [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) configuration doit avoir une valeur pour la `websiteUrl` propriété . Pour garantir une expérience utilisateur optimale, vous devez suivre les instructions relatives aux onglets sur mobile dans cet article lors de la création de vos onglets.

Les applications [distribuées via le magasin Teams](~/concepts/deploy-and-publish/appsource/publish.md) ont un processus d’approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Fonctionnalité de l’application** | **Comportement si l’application est approuvée** | **Comportement si l’application n’est pas approuvée** |
| --- | --- | --- |
| **Onglets personnels** | L’application apparaît dans la barre inférieure des clients mobiles. Les onglets s’ouvrent dans le client Teams. | L’application n’apparaît pas dans la barre inférieure des clients mobiles. |
| **Onglets de canal et de groupe** | L’onglet s’ouvre dans le client Teams à l’aide de `contentUrl`. | L’onglet s’ouvre dans un navigateur en dehors du client Teams à l’aide de `websiteUrl`. |

> [!NOTE]
>
> * Les applications soumises à [AppSource](https://appsource.microsoft.com) pour publication sur Teams sont évaluées automatiquement en fonction de la réactivité mobile. Pour toutes les requêtes, contactez teamsubm@microsoft.com.
> * Pour toutes les applications qui ne sont pas distribuées via AppSource, les onglets s’ouvrent dans une vue web in-app au sein des clients Teams par défaut et aucun processus d’approbation distinct n’est requis.
> * Le comportement par défaut des applications s’applique uniquement si elles sont distribuées via le magasin Teams. Par défaut, tous les onglets s’ouvrent dans le client Teams.
> * Pour lancer une évaluation de la convivialité de votre application pour les appareils mobiles, contactez teamsubm@microsoft.com avec les détails de votre application.

## <a name="authentication"></a>Authentification

Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau votre Kit de développement logiciel (SDK) JavaScript Teams vers au moins la version 1.4.1.

## <a name="low-bandwidth-and-intermittent-connections"></a>Faible bande passante et connexions intermittentes

Les clients mobiles fonctionnent avec une faible bande passante et des connexions intermittentes. Votre application doit gérer les délais d’expiration de manière appropriée en fournissant un message contextuel à l’utilisateur. Vous devez également utiliser des indicateurs de progression pour fournir des commentaires à vos utilisateurs pour tout processus de longue durée.

## <a name="testing-on-mobile-clients"></a>Test sur les clients mobiles

Vous devez vérifier que votre onglet fonctionne correctement sur des appareils mobiles de différentes tailles et qualités. Pour les appareils Android, vous pouvez utiliser [DevTools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant son exécution. Il est recommandé de procéder à des tests sur des appareils hautes et faibles performances, y compris sur une tablette.

## <a name="distribution"></a>Distribution

Les applications répertoriées dans le magasin Teams doivent être approuvées pour une utilisation mobile afin de fonctionner correctement dans le client mobile Teams. La disponibilité et le comportement des onglets varient selon que votre application est approuvée ou non.

### <a name="apps-on-teams-store-approved-for-mobile"></a>Applications sur le Store Teams approuvées pour les appareils mobiles

Le tableau suivant décrit la disponibilité et le comportement des onglets lorsque l’application est répertoriée dans le magasin Teams et approuvée pour une utilisation mobile :

|Fonctionnalité   |Disponibilité des appareils mobiles ?   |Comportement mobile|
|----------|-----------|------------|
|Canal <br /> onglet et groupe|Oui|L’onglet s’ouvre dans le client mobile Teams à l’aide de la configuration de `contentUrl` votre application.|
|Application personnelle|Oui|Chaque onglet de l’onglet de l’application personnelle s’ouvre dans le client mobile Teams à l’aide de sa configuration respective `contentUrl` .|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Applications sur le magasin Teams non approuvées pour les appareils mobiles

Le tableau suivant décrit la disponibilité et le comportement des onglets lorsque l’application est répertoriée dans le magasin Teams mais n’est pas approuvée pour une utilisation mobile :

| Fonctionnalité | Disponibilité des appareils mobiles ? | Comportement mobile |
|----------|-----------|------------|
|Onglet Canal et groupe|Oui|Tab s’ouvre dans le navigateur par défaut de l’appareil au lieu du client mobile Teams à l’aide de la configuration de `websiteUrl` votre application, qui doit également être incluse dans la [fonction](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace) de `setSettings()` votre code source. Toutefois, les utilisateurs peuvent afficher l’onglet dans le client mobile Teams en sélectionnant **Plus** en regard de l’application et en choisissant **Ouvrir**, ce qui déclenche la configuration de `contentUrl` votre application.|
|Application personnelle|Non|Non applicable|

> [!NOTE]
> Les messages du bot sont affichés dans la section de conversation si une application mobile dispose à la fois des fonctionnalités bot et onglet.
>
> Lorsque vous sélectionnez **Conversation** de l’application bot et que vous sélectionnez **Plus (...)**, vous ne pouvez pas voir la fonctionnalité d’onglet de cette application dans la liste. Toutefois, si vous sélectionnez **Plus (...)** en bas à droite de la section **Conversation** , vous pouvez afficher l’application d’onglet avec un lien vers la fonctionnalité d’application bot de cette application.

### <a name="apps-not-on-teams-store"></a>Applications ne figurant pas dans le magasin Teams

Si vous chargez une version test de votre application ou que vous la publiez dans le catalogue d’applications d’une organisation, le comportement des onglets est identique à celui des applications du Magasin Teams approuvées par Microsoft pour les appareils mobiles.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Obtenir un contexte Teams pour votre onglet](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>Voir aussi

* [Créer des onglets pour Teams](../what-are-tabs.md)
* [Créer des onglets avec les Cartes adaptatives](../how-to/build-adaptive-card-tabs.md)
* [Créer un onglet personnel](../how-to/create-personal-tab.md)
* [Planifier des onglets réactifs pour Teams mobile](../../concepts/design/plan-responsive-tabs-for-teams-mobile.md)
* [Concevoir votre onglet pour Microsoft Teams](tabs.md)
* [DevTools pour les onglets Microsoft Teams](../how-to/developer-tools.md)
* [Tester votre application](../../concepts/build-and-test/test-app-overview.md)
* [Distribuer votre application Microsoft Teams](../../concepts/deploy-and-publish/apps-publish-overview.md)
* [Créer un package d’application Teams](../../concepts/build-and-test/apps-package.md)
