---
title: Aperçu pour les développeurs
description: Décrit les fonctionnalités de l’aperçu public de Microsoft Teams pour les développeurs
ms.topic: conceptual
ms.localizationpriority: high
keywords: aperçu des fonctionnalités pour les développeurs de teams
ms.openlocfilehash: b953d26f517382b06d9d06d7aeac89e83137023b
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398693"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Aperçu public pour les développeurs de Microsoft Teams

>[!NOTE]
>Les fonctionnalités incluses dans l’aperçu peuvent ne pas être terminées et peuvent faire l’objet de modifications avant de devenir disponibles dans la version publique. Elles sont fournies uniquement à des fins de test et d’exploration. Elles ne doivent pas être utilisées dans les applications de production.

L’aperçu pour développeurs est un programme public pour les développeurs qui fournit un accès en avant-première aux fonctionnalités non publiées de Microsoft Teams. Cela vous permet d’explorer et de tester les fonctionnalités à venir pour une inclusion potentielle dans votre application Microsoft Teams. Nous sommes également heureux de recevoir des [commentaires](~/feedback.md) sur toute fonctionnalité de l’aperçu pour les développeurs. L’aperçu pour les développeurs est activé pour chaque client Microsoft Teams. Vous n’avez donc pas à vous soucier d’affecter l’ensemble de votre organisation.

## <a name="developer-preview-app-manifest"></a>Manifeste de l’application de l’aperçu pour les développeurs

De nombreuses fonctionnalités activées dans l’aperçu pour les développeurs nécessiteront des modifications du fichier JSON du manifeste de votre application. Pour ce faire, vous devez utiliser le [schéma de manifeste d’aperçu du développeur.](~/resources/schema/manifest-schema-dev-preview.md) Si vous utilisez ce schéma, vous ne pourrez pas utiliser [App Studio](~/concepts/build-and-test/app-studio-overview.md) pour effectuer ces modifications, ni pour télécharger votre application à des fins de test. Pour charger votre application, vous devez cliquer sur l’icône `More apps` dans la barre de l’application, puis sélectionner le `Upload a custom app link`. Avec cette méthode, vous ne pouvez télécharger qu’une version compressée du package de votre application.

Il peut être utile d’utiliser App Studio pour créer les parties du package de votre applications qui ne sont pas des aperçus pour les développeurs, puis d’exporter ce package et de modifier manuellement le fichier `manifest.json` afin d’ajouter les fonctionnalités d’aperçu pour les développeurs que vous souhaitez utiliser. Une fois que vous avez ajouté les fonctionnalités d’aperçu pour les développeurs au fichier `manifest.json`, vous ne pourrez pas réimporter le package dans App Studio.

## <a name="enable-developer-preview"></a>Activer l’aperçu pour les développeurs

L’aperçu pour développeur est activé pour chaque client, mais l’option d’activer l’aperçu pour les développeurs est contrôlée au niveau de l’organisation. Pour activer l’option qui permet d’activer l’aperçu pour les développeurs pour une personne, vous devez vous assurer que cette dernière a la possibilité de charger des applications personnalisées. Pour plus d’informations, consultez [configuration de votre client](~/concepts/build-and-test/prepare-your-o365-tenant.md).

L’utilisation d’une application contenant des fonctionnalités de l’aperçu pour les développeurs peut provoquer un comportement inattendu chez les clients qui n’ont pas activé l’aperçu pour les développeurs. Si vous ne voyez pas d’entrée pour l’aperçu pour les développeurs, la raison la plus probable est que votre organisation n’est pas configurée pour le chargement d’applications.

### <a name="on-a-desktop-or-web-client"></a>Sur un ordinateur de bureau ou un client web

Pour activer l’aperçu public pour les développeurs sur un ordinateur de bureau ou un client web, vous devez procéder comme suit :

1. Activez le chargement d’applications dans la console d’administration de votre client comme décrit [ici](~/concepts/build-and-test/prepare-your-o365-tenant.md).
1. Cliquez sur votre profil (en haut à droite ou en bas à gauche de l’interface Teams) pour afficher le menu de Teams.
1. Sélectionnez À propos → Aperçu pour les développeurs.
1. Sélectionnez **Basculer vers l’aperçu pour les développeurs**.

### <a name="on-a-mobile-client"></a>Sur un client mobile

Pour activer l’aperçu public pour les développeurs sur un client mobile, vous devez procéder comme suit :

1. Activez le chargement d’applications dans la console d’administration de votre client comme décrit [ici](~/concepts/build-and-test/prepare-your-o365-tenant.md).
1. Ouvrez le menu hamburger en haut à gauche, puis sélectionnez **Paramètres**.
1. Sélectionnez **À propos**.
1. Cliquez sur le bouton bascule d’aperçu pour les développeurs.

## <a name="disable-developer-preview"></a>Désactiver l’aperçu pour les développeurs

Utilisez le même élément de menu sous À propos → aperçu pour les développeurs, puis cliquez dessus pour le désactiver.

## <a name="see-also"></a>Voir aussi

[Tester et déboguer votre application Microsoft Teams](~/concepts/build-and-test/debug.md)
