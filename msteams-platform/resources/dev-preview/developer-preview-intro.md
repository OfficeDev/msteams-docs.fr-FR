---
title: Aperçu du développeur
description: Décrit les fonctionnalités de la prévisualisation pour les développeurs publics de Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: Teams prévisualiser les fonctionnalités de développement
ms.openlocfilehash: ddf935279d5298caa032df7f109369bdc4b798ef51206f5cc688846061fd6720
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57703960"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Prévisualisation pour les développeurs publics Microsoft Teams

>[!NOTE]
>Les fonctionnalités incluses dans la prévisualisation peuvent ne pas être terminées et peuvent faire l’objet de modifications avant de devenir disponibles dans la version publique. Elles sont fournies uniquement à des fins de test et d’exploration. Elles ne doivent pas être utilisées dans les applications de production.

La prévisualisation pour développeurs est un programme public pour les développeurs qui fournit un accès en avant-première aux fonctionnalités non Microsoft Teams. Cela vous permet d’explorer et de tester les fonctionnalités à venir pour une inclusion potentielle dans votre Microsoft Teams application. Nous vous souhaitons également la [bienvenue sur](~/feedback.md) toutes les fonctionnalités de la prévisualisation pour les développeurs. La prévisualisation développeur est activée par client Microsoft Teams, vous n’avez donc pas à vous soucier d’affecter l’ensemble de votre organisation.

## <a name="developer-preview-app-manifest"></a>Manifeste de l’application d’aperçu développeur

De nombreuses fonctionnalités activées dans la prévisualisation du développeur nécessitent des modifications de votre fichier JSON de manifeste d’application. Pour ce faire, vous devrez utiliser le schéma de manifeste d’aperçu développeur Si vous utilisez ce schéma, vous ne serez pas en mesure d’utiliser [App Studio](~/concepts/build-and-test/app-studio-overview.md) pour apporter ces modifications, ni de l’utiliser pour télécharger votre application à des moments de test. [](~/resources/schema/manifest-schema-dev-preview.md) Pour télécharger votre application, vous devez cliquer sur l’icône dans la barre de l’application, `More apps` puis sélectionner le `Upload a custom app link` . À l’aide de cette méthode, vous pouvez uniquement charger une version compressée de votre package d’application.

Il peut s’avérer utile d’utiliser App Studio pour créer les parties d’aperçu non développeur de votre package d’application, puis exporter ce package et modifier manuellement le fichier pour ajouter les fonctionnalités d’aperçu de développeur que vous souhaitez `manifest.json` utiliser. Une fois que vous avez ajouté les fonctionnalités d’aperçu développeur au fichier, vous ne pourrez pas `manifest.json` ré-importer le package dans App Studio.

## <a name="enable-developer-preview"></a>Activer la prévisualisation pour les développeurs

La prévisualisation du développeur est activée par client, mais l’option d’activer la prévisualisation du développeur est contrôlée au niveau de l’organisation. Pour activer l’option d’activer la prévisualisation du développeur pour une personne, vous devez vous assurer qu’elle a la possibilité de télécharger des applications personnalisées. Pour plus [d’informations, voir](~/concepts/build-and-test/prepare-your-o365-tenant.md) configuration de votre client.

L’utilisation d’une application qui contient des fonctionnalités de prévisualisation pour les développeurs peut entraîner un comportement inattendu des clients qui n’ont pas activé la prévisualisation pour les développeurs. Si vous ne voyez pas d’entrée pour la prévisualisation pour les développeurs, la raison la plus probable est que votre organisation n’est pas configurée pour le téléchargement d’applications.

### <a name="on-a-desktop-or-web-client"></a>Sur un client de bureau ou web

Pour activer la prévisualisation pour les développeurs publics sur un client de bureau ou web, vous devez :

1. Activation du téléchargement d’applications dans la console d’administration de votre client, comme décrit [ici.](~/concepts/build-and-test/prepare-your-o365-tenant.md)
1. Cliquez sur votre profil (en haut à droite ou en bas à gauche de l’interface Teams)) pour afficher le menu Teams menu.
1. Select About → Developer preview.
1. Sélectionnez **Basculer vers l’aperçu développeur.**

### <a name="on-a-mobile-client"></a>Sur un client mobile

Pour activer la prévisualisation pour les développeurs publics sur un client mobile, vous devez :

1. Activation du téléchargement d’applications dans la console d’administration de votre client, comme décrit [ici.](~/concepts/build-and-test/prepare-your-o365-tenant.md)
1. Ouvrez le menu hamburger en haut à gauche, puis **sélectionnez Paramètres**.
1. Sélectionnez **À propos de**.
1. Cliquez sur le bouton bascule d’aperçu développeur.

## <a name="disable-developer-preview"></a>Désactiver la prévisualisation pour les développeurs

Utilisez le même élément de menu sous À propos → aperçu développeur, puis cliquez dessus pour le désactiver.

## <a name="features-available-in-developer-preview"></a>Fonctionnalités disponibles dans la prévisualisation du développeur

Pour obtenir la liste complète des fonctionnalités actuellement activées dans la prévisualisation pour les développeurs, voir : Fonctionnalités de la prévisualisation [publique pour les développeurs.](../../resources/dev-preview/developer-preview-features.md)
