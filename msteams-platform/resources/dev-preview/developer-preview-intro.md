---
title: Aperçu pour les développeurs
description: Décrit les fonctionnalités de la version d’évaluation pour développeurs publics de Microsoft teams
keywords: fonctionnalités de développeur d’aperçu teams
ms.openlocfilehash: a09e715e4e2d4aba72726cc96c4d248c550a3ab1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673831"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Aperçu public pour les développeurs pour Microsoft teams

>[!NOTE]
>Les fonctionnalités incluses dans l’aperçu ne sont peut-être pas complètes et peuvent être modifiées avant de devenir disponibles dans la version publique. Elles sont fournies à des fins de test et d’exploration uniquement. Elles ne doivent pas être utilisées dans les applications de production.

Developer Preview est un programme public pour les développeurs qui fournit un accès anticipé aux fonctionnalités non commercialisées dans Microsoft Teams. Cela vous permet d’explorer et de tester les fonctionnalités à venir afin de les inclure dans votre application Microsoft Teams. Nous souhaitons également nous faire [part de vos commentaires](~/feedback.md) sur n’importe quelle fonctionnalité de developer preview. L’aperçu des développeurs est activé par client Microsoft Teams, vous n’avez donc pas à vous soucier de l’impact de l’ensemble de votre organisation.

## <a name="developer-preview-app-manifest"></a>Manifeste d’application d’aperçu développeur

De nombreuses fonctionnalités activées dans l’Aperçu pour les développeurs nécessitent des modifications de votre fichier JSON de manifeste d’application. Pour ce faire, vous devez utiliser le [schéma de manifeste d’aperçu développeur](~/resources/schema/manifest-schema-dev-preview.md) si vous utilisez ce schéma, vous ne pourrez pas utiliser [app Studio](~/concepts/build-and-test/app-studio-overview.md) pour effectuer ces modifications et vous ne pourrez pas l’utiliser pour télécharger votre application à des fins de test. Pour télécharger votre application, vous devez cliquer sur l' `More apps` icône dans la barre de l’application, puis `Upload a custom app link`sélectionnez le. À l’aide de cette méthode, vous pouvez uniquement télécharger une version zippée de votre package d’application.

Il peut s’avérer utile d’utiliser app Studio pour créer des parties d’aperçu non développeur de votre package d’application, puis exporter ce package et modifier manuellement `manifest.json` le fichier pour ajouter les fonctionnalités d’aperçu développeur que vous souhaitez utiliser. Une fois que vous avez ajouté les `manifest.json` fonctionnalités d’aperçu développeur au fichier, vous ne serez pas en mesure de réimporter le package dans l’application Studio.

## <a name="enable-developer-preview"></a>Activer l’Aperçu pour les développeurs

L’aperçu des développeurs est activé pour chaque client, mais l’option d’activation de l’Aperçu pour les développeurs est contrôlée au niveau de l’organisation. Pour permettre à l’utilisateur d’activer l’Aperçu pour un individu, vous devez vous assurer qu’il est en mesure de télécharger des applications personnalisées. Pour plus d’informations, consultez [la rubrique Configuration de votre client](~/concepts/build-and-test/prepare-your-o365-tenant.md) .

L’utilisation d’une application qui contient des fonctionnalités d’aperçu pour les développeurs peut entraîner un comportement inattendu des clients qui n’ont pas activé l’aperçu des développeurs. Si vous ne voyez pas d’entrée pour l’aperçu du développeur, la raison la plus probable est que votre organisation n’est pas configurée pour le téléchargement de l’application.

### <a name="on-a-desktop-or-web-client"></a>Sur un client de bureau ou Web

Pour activer la préversion publique pour les développeurs sur un ordinateur de bureau ou un client Web, procédez comme suit :

1. Activation du téléchargement d’applications dans la console d’administration de votre client, comme décrit [ici](~/concepts/build-and-test/prepare-your-o365-tenant.md).
1. Cliquez sur votre profil (en haut à droite ou en bas à gauche de l’interface Teams) pour afficher le menu Teams.
1. Sélectionnez à propos de → aperçu développeur.
1. Sélectionnez **basculer vers l’aperçu du développeur**.

### <a name="on-a-mobile-client"></a>Sur un client mobile

Pour activer la préversion publique pour les développeurs sur un client mobile, procédez comme suit :

1. Activation du téléchargement d’applications dans la console d’administration de votre client, comme décrit [ici](~/concepts/build-and-test/prepare-your-o365-tenant.md).
1. Ouvrez le menu hamburger dans la partie supérieure gauche, puis sélectionnez **paramètres**.
1. Sélectionnez **à propos de**.
1. Cliquez sur le bouton Aperçu du développeur.

## <a name="disable-developer-preview"></a>Désactiver l’Aperçu pour les développeurs

Utilisez le même élément de menu sous à propos de → aperçu développeur, puis cliquez dessus pour le désactiver.

## <a name="features-available-in-developer-preview"></a>Fonctionnalités disponibles dans l’Aperçu pour les développeurs

Pour obtenir la liste complète des fonctionnalités actuellement activées dans l’Aperçu pour les développeurs, voir : [Features in public developer preview](../../resources/dev-preview/developer-preview-features.md).
