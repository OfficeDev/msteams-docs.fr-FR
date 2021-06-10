---
title: Onglets sur les appareils mobiles
description: Décrit les considérations pour les développeurs pour l’implémentation d’onglets sur Microsoft Teams mobile.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 41ba96b64bd31f3b226aeba72969bc44c1ae8955
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630655"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

Lorsque vous construisez une application Microsoft Teams qui inclut un onglet, vous devez prendre en compte (et tester) le fonctionnement de votre onglet sur les clients Microsoft Teams Android et iOS. Les sections ci-dessous décrivent certains des scénarios clés que vous devez prendre en considération.

## <a name="authentication"></a>Authentification

Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau Teams SDK JavaScript vers au moins la version 1.4.1.

## <a name="low-bandwidth-and-intermittent-connections"></a>Bande passante faible et connexions intermittentes

Les clients mobiles doivent régulièrement fonctionner avec une bande passante faible et des connexions intermittentes. Votre application doit gérer les délai d’accès de manière appropriée en fournissant un message contextuel à l’utilisateur. Vous devez également fournir des indicateurs de progression des utilisateurs pour fournir des commentaires à vos utilisateurs pour tout processus de longue durée.

## <a name="testing-on-mobile-clients"></a>Test sur les clients mobiles

Vous devez vérifier que votre onglet fonctionne correctement sur des appareils mobiles de différentes tailles et qualités. Pour les appareils Android, vous pouvez utiliser [DevTools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant son exécution. Nous vous recommandons de tester sur les appareils hautes et faibles performances, y compris une tablette.

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
|Onglet Canal et groupe|Oui|L’onglet s’ouvre dans le navigateur par défaut de l’appareil au lieu du client mobile Teams à l’aide de la configuration de votre application, qui doit également être incluse dans la fonction de `websiteUrl` votre code `setSettings()` [source.](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true) Toutefois, les utilisateurs peuvent toujours afficher l’onglet  dans le client mobile Teams en sélectionnant Plus en regard de l’application et en choisissant **Ouvrir,** ce qui déclenche la configuration de votre `contentUrl` application.|
|Application personnelle|Non|Non applicable|

### <a name="apps-not-on-teams-store"></a>Applications non stockées dans Teams store

Si vous chargez une version de votre application ou que vous publiez sur le catalogue d’applications d’une organisation, le comportement de l’onglet sera le même que celui des applications Teams Store approuvées par Microsoft pour appareils mobiles.

## <a name="see-also"></a>Voir aussi

* [Recommandations en matière de conception d’onglets](~/tabs/design/tabs.md)
