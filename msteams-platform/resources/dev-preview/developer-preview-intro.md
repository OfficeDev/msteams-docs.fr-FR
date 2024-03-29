---
title: Aperçu public pour les développeurs de Microsoft Teams
description: Une préversion du développeur (bêta) est un programme public qui permet d’explorer et de tester les fonctionnalités à venir en vue d’une inclusion potentielle dans votre application Microsoft Teams.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: dd0583f453e93a0127bf4cbcc29a6a56dec6655a
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100286"
---
# <a name="public-developer-preview-for-teams"></a>Aperçu public pour les développeurs de Microsoft Teams

>[!NOTE]
>Les fonctionnalités incluses dans l’aperçu peuvent ne pas être terminées et peuvent faire l’objet de modifications avant de devenir disponibles dans la version publique. Elles sont fournies uniquement à des fins de test et d’exploration. Elles ne doivent pas être utilisées dans les applications de production.

L’aperçu pour développeurs est un programme public pour les développeurs qui fournit un accès en avant-première aux fonctionnalités non publiées de Microsoft Teams. Cela vous permet d’explorer et de tester les fonctionnalités à venir pour une inclusion potentielle dans votre application Teams. Nous sommes également heureux de recevoir des [commentaires](~/feedback.md) sur toute fonctionnalité de l’aperçu pour les développeurs. L’aperçu pour les développeurs est activé pour chaque client Microsoft Teams. Vous n’avez donc pas à vous soucier d’affecter l’ensemble de votre organisation.

## <a name="developer-preview-app-manifest"></a>Manifeste de l’application de l’aperçu pour les développeurs

De nombreuses fonctionnalités activées dans l’aperçu pour les développeurs nécessiteront des modifications du fichier JSON du manifeste de votre application. Pour ce faire, vous devez utiliser le [schéma de manifeste de l’aperçu pour les développeurs.](~/resources/schema/manifest-schema-dev-preview.md) Si vous utilisez ce schéma, vous ne pourrez pas utiliser [Developer Portal pour Teams](~/concepts/build-and-test/teams-developer-portal.md) afin d’apporter ces modifications, ni l’utiliser pour charger votre application à des fins de test. Pour charger votre application, vous devez sélectionner l’icône `More apps` dans la barre de l’application, puis le `Upload a custom app link`. Avec cette méthode, vous ne pouvez télécharger qu’une version compressée du package de votre application.

Vous trouverez peut-être utile d’utiliser Developer Portal pour Teams afin de créer les parties d’aperçu non développeur de votre package d’application, puis d’exporter ce package et de modifier manuellement le fichier `manifest.json` pour ajouter les fonctionnalités d’aperçu du développeur que vous souhaitez utiliser. Une fois que vous avez ajouté des fonctionnalités d’aperçu développeur au fichier `manifest.json` , vous ne pourrez pas réimporter le package dans Developer Portal for Teams.

## <a name="enable-developer-preview"></a>Activer l’aperçu pour les développeurs

L’aperçu pour développeur est activé pour chaque client, mais l’option d’activer l’aperçu pour les développeurs est contrôlée au niveau de l’organisation. Pour activer l’option qui permet d’activer l’aperçu pour les développeurs pour une personne, vous devez vous assurer que cette dernière a la possibilité de charger des applications personnalisées. Pour plus d’informations, consultez [configuration de votre client](~/concepts/build-and-test/prepare-your-o365-tenant.md).

L’utilisation d’une application contenant des fonctionnalités d’aperçu pour les développeurs peut provoquer un comportement inattendu chez les clients qui n’ont pas activé l’aperçu pour les développeurs. Si vous ne voyez pas d’entrée relative à l’aperçu pour les développeurs, la raison la plus probable est que votre organisation n’est pas configurée pour le chargement d’applications.

### <a name="on-a-desktop-or-web-client"></a>Sur un ordinateur de bureau ou un client web

Pour activer l’aperçu public pour les développeurs sur un ordinateur de bureau ou un client web :

1. Activez le chargement d’applications personnalisées ou le chargement indépendant pour votre client développeur. Pour plus d’informations, voir [Activer les applications Teams personnalisées](../../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).
1. Sélectionnez le menu des points de suspension (...) en haut de votre profil utilisateur pour afficher le menu Teams.
1. Sélectionnez **À propos de** >  **l’aperçu pour les développeurs**.
1. Sélectionnez **Basculer vers l’aperçu pour les développeurs**.

### <a name="on-a-mobile-client"></a>Sur un client mobile

Pour activer l’aperçu public pour les développeurs sur un client mobile :

1. Activez le chargement d’application ou le chargement indépendant pour votre client développeur. Pour plus d’informations, voir [Activer les applications Teams personnalisées](../../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).
1. Ouvrez le menu hamburger en haut à gauche, puis sélectionnez **Paramètres**.
1. Sélectionnez **À propos**.
1. Activez la bascule **Aperçu pour les développeurs**.

## <a name="disable-developer-preview"></a>Désactiver l’aperçu pour les développeurs

Utilisez le même élément de menu sous À propos de → Aperçu pour les développeurs, puis cliquez dessus pour le désactiver.

## <a name="see-also"></a>Voir aussi

[Tester et déboguer votre application Microsoft Teams](~/concepts/build-and-test/debug.md)
