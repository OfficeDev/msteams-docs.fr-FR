---
title: Raisons courantes de l’échec de validation d’application
description: Découvrez les raisons les plus courantes de l’échec de validation d’application, telles que les liens rompus, les erreurs inattendues, les incidents, la violation des instructions de domaine valides, les bogues fonctionnels.
ms.topic: overview
author: v-ypalikila
ms.author: v-ypalikila
ms.localizationpriority: high
ms.openlocfilehash: 65144510fcb6a63c1c5cfaed4c344185917dee9a
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560651"
---
# <a name="common-reasons-for-app-validation-failure"></a>Raisons courantes de l’échec de validation d’application

La plupart des applications ne passent pas le processus de soumission du Store en raison de problèmes pendant le développement d’applications. Les problèmes ou les raisons les plus courants sont traités dans cet article pour vous aider à mieux préparer votre application avant de [soumettre pour révision](/office/dev/store/add-in-submission-guide?toc=/microsoftteams/platform/toc.json&bc=/microsoftteams/platform/breadcrumb/toc.json). Évitez ces échecs courants et suivez les instructions de validation [Microsoft Teams Store](prepare/teams-store-validation-guidelines.md) et [stratégies de certification de la Place de marché commerciale](/legal/marketplace/certification-policies) pour augmenter la probabilité que votre application réussisse le processus de soumission au Microsoft Teams Store.

Voici les raisons les plus courantes pour lesquelles votre application est rejetée :

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/broken-links-errors-icon-1.png" link="#broken-links-functional-bugs-app-crashes-and-unexpected-errors":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/app-description-icon.png" link="#app-description":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/trademark-icon.png" link="#violation-of-microsoft-trademark-and-brand-guidelines":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/testability-icon.png" link="#testability":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/compliance-icon.png" link="#microsoft-365-app-compliance-program":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/app-guideline-icon.png" link="#violation-of-app-icon-guidelines":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/app-name-icon.png" link="#app-name":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/support-link-icon.png" link="#support-link":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/schema-icon.png" link="#manifest-schema":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/app-ui-icon.png" link="#app-ui":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/domain-icon.png" link="#valid-domains":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/localization-icon.png" link="#localization-information":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/developer-name-icon.png" link="#provider-or-developer-name-mismatch":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/privacy-policy-icon.png" link="#privacy-policy":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/terms-of-use-icon.png" link="#terms-of-use":::
   :::column-end:::
:::row-end:::

## <a name="broken-links-functional-bugs-app-crashes-and-unexpected-errors"></a>Liens rompus, bogues fonctionnels, blocages d’application et erreurs inattendues

Testez votre application pour vérifier l’exactitude, les fonctionnalités et l’utilisation de vos applications’. Veillez à tester votre application de manière approfondie, à vérifier tous les flux de travail de bout en bout pris en charge par votre application, à tester la compatibilité de l’application sur les systèmes d’exploitation et les navigateurs conformément à la [stratégie de certification de la Place de marché commerciale](/legal/marketplace/certification-policies)et à corriger tous les bogues. Vous devez éviter les erreurs suivantes dans votre application avant d’envoyer pour révision :

* Liens rompus dans une application.

* Bogues fonctionnels qui bloquent l’utilisation des applications.

* L’application se bloque.

* Chargement continu des surfaces d’application qui empêchent l’achèvement des workflows déclarés pris en charge par l’application.

* Messages d’erreur inattendus lors de l’utilisation, de la connexion et de l’expérience d’inscription de l’application, et pour les scénarios où la fonctionnalité d’application ne fonctionne pas comme prévu.

* Assurez-vous que votre application est terminée et prête à être publiée avant d’envoyer pour révision.

## <a name="app-description"></a>Description de l’application

Une description intéressante peut faire ressortir votre application dans le Microsoft Teams Store et encourager les clients à la télécharger. Vous devez éviter les erreurs suivantes dans la description de votre application :

* Les informations utiles pour les nouveaux utilisateurs, telles que les liens « S'inscrire » ou « Démarrer », ou les liens « Aide » et « Nous contacter », ne figurent pas dans le manifeste et la description complète d'AppSource.

* Le nom ou la fonctionnalité de l’application spécifique à la région n’est pas appelé dans les descriptions de manifeste et d’application Espace partenaires.

* Les limitations ou dépendances de compte sur les comptes ou services externes pour terminer l’expérience de connexion, de déconnexion et d’inscription ne sont pas appelées dans le manifeste de l’application et la description longue.

* Une description courte et complète dans le manifeste de l’application ne met pas en évidence la proposition de valeur des applications.

* Les fonctionnalités d’application prises en charge ne sont pas mises à jour.

* Comparaison d’applications avec une autre application.

* Références aux intégrations, qui ne font pas partie des fonctionnalités de l’application.

* Erreurs grammaticales.

* Les descriptions courtes et complètes de l’application sont identiques.

## <a name="violation-of-microsoft-trademark-and-brand-guidelines"></a>Violation des directives de marque et de marque Microsoft

Les ressources de la marque Microsoft, notamment les logos, les icônes, les conceptions, les vêtements commerciaux, les polices, les noms de produits, les services, les sons, les emojis et tous les autres éléments et fonctionnalités de la marque, qu’ils soient inscrits ou non inscrits sont des actifs propriétaires appartenant à Microsoft et à son groupe d’entreprises.

Lorsque vous faites référence à des marques commerciales, des noms de produits et des services Microsoft, vous devez suivre les[directives de marque et de marque Microsoft](https://www.microsoft.com/legal/intellectualproperty/trademarks). Vous devez éviter les violations courantes suivantes qui entraînent le rejet de l’application :

* Abréviation de Microsoft en tant que MS ou MSFT dans la liste des offres, faisant référence à la première instance de Microsoft Teams dans la description de l’offre en tant que **Teams** au lieu de **Microsoft Teams**.

* Utilisation des ressources de marque Microsoft dans le contenu de l’offre sans licence rapide de Microsoft.

* Création d’une description d’offre (y compris la description de l’offre, le titre, l’icône, les captures d’écran et les vidéos) qui emprunte l’identité ou donne l’impression qu’il s’agit d’une application Microsoft officielle pour le Microsoft Teams Store.

## <a name="testability"></a>Testabilité  

 [Instructions de test détaillées](prepare/teams-store-validation-guidelines.md#app-package-and-store-listing) et les informations d’identification vous aident à examiner correctement votre application.

Veillez à fournir tous les détails nécessaires pour passer en revue votre application dans la section Notes pour les informations de certification de Espace partenaires, des informations d’identification de démonstration valides pour les fonctionnalités qui nécessitent une connexion et des instructions pour définir une configuration spéciale, une vidéo de démonstration ou du matériel pour les fonctionnalités nécessitant un environnement difficile à répliquer et à terminer. Veillez également à fournir les informations de contact les plus récentes.

Vous devez éviter les problèmes suivants qui se produisent dans 20 % des applications rejetées lors de l’examen de l’application :

* Aucune instruction de test ni aucune information d’identification pour tester l’application.

* Un seul compte de test est fourni lorsqu’il existe une dépendance avec deux comptes de test pour tester des scénarios de collaboration.

* Les instructions de test et les informations d’identification fournies ne sont pas suffisantes pour effectuer les tests fonctionnels de l’application.

## <a name="microsoft-365-app-compliance-program"></a>Programme de conformité d’Application Microsoft 365  

Le programme de conformité des applications Microsoft 365 aide les organisations à évaluer et à gérer les risques en évaluant les informations de sécurité et de conformité relatives à une application. Vous **devez effectuer** une [vérification de l’éditeur](/azure/active-directory/develop/mark-app-as-publisher-verified) avant de soumettre votre application pour révision afin qu’elle soit publiée sur le Microsoft Teams Store.

## <a name="violation-of-app-icon-guidelines"></a>Violation des instructions relatives aux icônes d’application

Les icônes sont l’un des principaux éléments que les utilisateurs voient lors de la navigation dans le Microsoft Teams Store. Vos icônes doivent communiquer la marque et l’objectif de votre application tout en respectant les instructions de l’[Icône d’application](../../build-and-test/apps-package.md#app-icons). Vous devez éviter les violations suivantes qui entraînent le rejet de l’application :

* Soumissions d’applications qui contiennent des packages d’application avec des icônes de couleur et de contour différentes ou des icônes de contour non blanches et non transparentes.

* Soumissions d’applications avec différents logos dans Espace partenaires et le package d’application soumis pour révision.

## <a name="app-name"></a>Nom de l'application

Le nom de votre application joue un rôle essentiel pour que les utilisateurs découvrent votre application sur le Microsoft Teams Store. Assurez-vous que le nom de votre application respecte [directives de nom d’application](prepare/teams-store-validation-guidelines.md#app-name) et qu’il n’enfreint pas les[marques commerciales et de marque Microsoft](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks). Vous devez éviter les violations suivantes qui entraînent le rejet de l’application :

* Utilisation incohérente du nom de l’application dans toutes les fonctionnalités des applications.
* Incompatibilité entre le nom de l’application mentionné dans le manifeste d’application envoyé dans le cadre du package d’application et l’Espace partenaires.
* Les noms d’application ajoutés à *Beta*, *Dev* et *Prod* indiquent que l’application n’est pas prête pour la production.
* Soumissions d’applications où le développeur a modifié le nom de l’application, mais où l’ancien nom d’application est utilisé dans l’application.

## <a name="support-link"></a>Lien vers le support technique

 Les liens de support ne doivent pas demander l’authentification aux utilisateurs et doivent diriger directement vers les informations de support appropriées. Vous devez vous assurer que votre application inclut un lien de support valide pour les utilisateurs à contacter.

## <a name="manifest-schema"></a>Schéma du manifeste

Le manifeste de l’application Teams décrit comment l’application s’intègre au produit Microsoft Teams. Votre manifeste d’application doit être conforme à un [schéma de manifeste](../../../resources/schema/manifest-schema.md) publié publiquement. Si votre application prend en charge la localisation, veillez à utiliser un schéma de manifeste de localisation version 1.5 ou ultérieure. Les packages d’application qui contiennent des schémas d’aperçu (non publiés publiquement) échouent à la révision de l’application.

Vous devez mettre à jour la version de l’application déclarée dans le manifeste si vous soumettez une mise à jour d’application. Nous vous recommandons de toujours utiliser le dernier schéma de manifeste publié publiquement lors de l’envoi d’une nouvelle application ou d’une mise à jour d’application, et de vous assurer que la version du schéma de manifeste dans Microsoft Teams Store et Microsoft AppSource est la même.

Votre package d’application doit contenir uniquement le manifeste, l’icône de couleur et l’icône de contour de vos applications. Les packages d’application qui contiennent d’autres fichiers ou dossiers échouent à la révision de l’application.

## <a name="app-ui"></a>Interface utilisateur de l’application

L’interface utilisateur de vos applications ne doit pas sembler incomplète et doit être intuitive. Assurez-vous que les utilisateurs ne disposent pas d’un écran vide lors de l’exécution d’une action sur l’interface utilisateur des applications. Les applications qui ont du contenu tronqué ou qui se chevauche et les applications qui affichent des images rompues échouent à la révision de l’application.

## <a name="valid-domains"></a>Domaines valides

Votre soumission d’application doit respecter les instructions relatives aux [domaines externes](/legal/marketplace/certification-policies) sous la stratégie de certification de la Place de marché commerciale de Microsoft. Pour que votre application puisse passer en revue, assurez-vous que les domaines valides répertoriés dans le manifeste de l’application sont sous le contrôle direct de votre organisation.

## <a name="localization-information"></a>Informations de localisation

Vous devez inclure les fichiers de langue localisés dans votre package d’application si votre application prend en charge la localisation. Les fichiers de localisation doivent être conformes au [schéma de localisation Teams](../../build-and-test/apps-localization.md). Les applications qui prennent en charge la localisation mais qui ne disposent pas d’informations de localisation dans le manifeste de l’application échouent à la révision de l’application.

## <a name="provider-or-developer-name-mismatch"></a>Incompatibilité de nom de fournisseur ou de développeur

Vous devez vous assurer de fournir le même nom de développeur dans votre liste d’offres dans les deux vitrines afin d’éviter toute confusion de l’utilisateur final lors de l’acquisition des applications’ à partir du Microsoft Teams Store ou Microsoft AppSource. Les offres avec incompatibilité dans le nom du développeur échouent fréquemment à la révision de l’application.

## <a name="privacy-policy"></a>Déclaration de confidentialité

Votre description d’offre doit inclure un lien de stratégie de confidentialité valide. Les offres avec des liens de stratégie de confidentialité non valides, non sécurisés et rompus échouent à la révision de l’application. Votre politique de confidentialité doit respecter les [lignes directrices de la politique de confidentialité](prepare/teams-store-validation-guidelines.md#privacy-policy).

## <a name="terms-of-use"></a>Conditions d’utilisation

Votre description d’offre doit inclure un lien Conditions d’utilisation valide. Les offres avec des liens de Conditions d’utilisation non valides, non sécurisés et rompus échouent à la révision de l’application. Vous devez suivre les [instructions relatives aux conditions d’utilisation](prepare/teams-store-validation-guidelines.md#terms-of-use).

## <a name="see-also"></a>Voir aussi

* [Instructions de validation du magasin Microsoft Teams](prepare/teams-store-validation-guidelines.md)
* [Stratégies de certification de la Place de marché commerciale](/legal/marketplace/certification-policies)
* [Recommandations en matière de marque et de marque Microsoft](https://www.microsoft.com/legal/intellectualproperty/trademarks)
