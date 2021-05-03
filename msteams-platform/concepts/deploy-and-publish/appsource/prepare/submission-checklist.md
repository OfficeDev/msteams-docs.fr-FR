---
title: Préparer l'envoi de votre magasin
description: Décrit les dernières étapes avant d'envoyer votre Microsoft Teams pour qu'elle soit répertoriée dans le Store.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: d46d21c3d984b5688c00857e485210b0f0fcf2c7
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101680"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>Préparer votre soumission Microsoft Teams au Store

Vous avez conçu, créé et testé votre application Microsoft Teams web. Vous êtes maintenant prêt à la réen lister pour que les personnes peuvent découvrir et commencer à utiliser votre application.

Avant de soumettre votre application à [l'Partner Center,](/office/dev/store/use-partner-center-to-submit-to-appsource)assurez-vous que vous avez effectué les choses suivantes.

## <a name="validate-your-app-package"></a>Valider votre package d'application

Bien que votre application fonctionne peut-être dans un environnement de test, vous devez vérifier votre package d'application pour éviter les problèmes pendant le processus de soumission.

L Microsoft Teams de validation d'application vous permet d'identifier et de résoudre les problèmes avant de les soumettre à l'Partner Center. L'outil vérifie automatiquement les configurations de votre application par rapport aux mêmes cas de test utilisés lors de la validation du Store.

1. Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html). (Remarque : l'outil est également disponible [dans App Studio.)](../../../build-and-test/app-studio-overview.md)
1. Télécharger votre package d'application pour exécuter les tests automatisés.
1. Go to the **Preliminary checklist** and review the test cases that are difficult to automate.
1. [Corrigez les problèmes de configuration ou](~/resources/schema/manifest-schema.md) d'application en général si les tests automatisés vous donnent des erreurs ou si vous n'avez pas satisfait à tous les critères de la liste de contrôle.

## <a name="compile-testing-instructions"></a>Compiler les instructions de test

Fournissez des instructions et des ressources pour aider les réviseurs à tester votre application, y compris les comptes de test, les informations d'identification et les clés de licence. Vous pouvez ajouter des instructions dans l'Partner Center ou les télécharger dans un emplacement disponible publiquement sur SharePoint.

### <a name="feature-list"></a>Liste des fonctionnalités

Fournissez des détails sur les fonctionnalités de votre application dans Teams et les étapes de test de chacune d'elles.

### <a name="accounts"></a>Comptes

Vous devez fournir des comptes de test si votre application nécessite une licence ou une liste sécurisée back-end. Tous les comptes que vous fournissez doivent inclure des données pré-remplies pour faciliter le test.

En fonction des fonctionnalités de votre application, vous devrez peut-être fournir les éléments suivants :

* Compte d'administrateur (obligatoire)
* Compte non administrateur (obligatoire)
* Un compte qui n'est pas pré-configuré pour tester correctement l'expérience de première utilisation de la signature (obligatoire)
* Un compte ayant accès aux fonctionnalités premium ou mises à niveau (le cas échéant)
* Deux comptes dans le même client pour tester l'expérience de collaboration pour les applications qui fonctionnent dans des contextes partagés (le cas échéant)

### <a name="tenant-configurations"></a>Configurations de client

Si vous devez configurer un client Teams pour utiliser votre application, incluez ces instructions et les comptes administrateur et non administrateur pour la validation.

### <a name="video-optional"></a>Vidéo (facultatif)

Fournissez un enregistrement de votre application afin que Microsoft puisse bien comprendre ses fonctionnalités.

## <a name="create-your-store-listing-details"></a>Créer les détails de la description dans le Store

Les informations que [](https://partner.microsoft.com) vous soumettez à l'&#8212;, notamment votre nom, descriptions, icônes et images&#8212;, deviennent le Teams Store et la description Microsoft AppSource de votre application.

Une liste dans le Store peut être la première impression de votre application. Augmentez les installations avec une liste qui transmet efficacement les avantages, les fonctionnalités et la marque de votre application.

### <a name="specify-a-short-name"></a>Spécifier un nom court

Le nom de votre application (en particulier, son nom [*court)*](~/resources/schema/manifest-schema.md#name)joue un rôle crucial dans la façon dont les utilisateurs la découvrent dans le Store.

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Exemple de capture d'écran sur laquelle le nom court d'une application s'affiche dans une liste du Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre nom court respecte les instructions [de validation du Store.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)

### <a name="write-descriptions"></a>Écrire des descriptions

Vous devez avoir une description courte et longue de votre application.

#### <a name="short-description"></a>Description brève

Résumé concis de votre application qui doit être original, attrayant et adressé à votre public cible. Conservez la description courte jusqu'à une phrase.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Exemple de capture d'écran sur laquelle la description courte d'une application s'affiche dans une description dans le Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre brève description respecte les instructions [de validation du Store.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)

#### <a name="long-description"></a>Description longue

La description longue peut fournir un narratif qui met en évidence les principales fonctionnalités de votre application, les problèmes qu'elle résout et son public cible. Bien que cette description puisse prendre jusqu'à 4 000 caractères, la plupart des utilisateurs ne lisent qu'entre 300 et 500 mots.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Exemple de capture d'écran sur laquelle la description longue d'une application s'affiche dans une description dans le Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre description longue respecte les instructions [de validation du Store.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)

### <a name="adhere-to-icon-design-guidelines"></a>Respecter les instructions de conception des icônes

Les icônes sont l'un des principaux éléments que les utilisateurs voient lors de la navigation dans le Store. Vos icônes doivent communiquer la marque et l'objectif de votre application tout en respectant les Teams requises.

Pour plus d'informations, voir [les conseils sur la création Teams icônes d'application.](~/concepts/build-and-test/apps-package.md#app-icons)

### <a name="capture-screenshots"></a>Capture d'écran

Les captures d'écran fournissent un aperçu visuel de votre application pour compléter le nom, l'icône et les descriptions de votre application.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Exemple de capture d'écran sur laquelle les captures d'écran d'application s'affichent dans une liste du Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Souvenez-vous des captures d'écran suivantes :

* Vous pouvez avoir jusqu'à cinq captures d'écran par liste.
* Les types de fichiers pris en charge sont PNG, JPEG et GIF.
* Les dimensions doivent être de 1 366 x 768 pixels.
* Taille maximale de 1 024 Ko.

Pour obtenir les meilleures pratiques, consultez les ressources suivantes :

* [Teams de validation du magasin d'informations](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [Création d'images efficaces pour les magasins d'applications Microsoft](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>Créer une vidéo

Une vidéo dans votre liste peut être le moyen le plus efficace de communiquer pourquoi les personnes doivent utiliser votre application. Vous devez répondre aux questions suivantes dans une vidéo :

* Qui votre application est-elle pour ?
* Quels problèmes votre application peut-elle résoudre ?
* Comment fonctionne votre application ?
* Quels autres avantages bénéficiez-vous de l'utilisation de votre application ?

#### <a name="best-practices-for-videos"></a>Meilleures pratiques pour les vidéos

* Conservez votre vidéo entre 30 et 90 secondes.
* Visez la qualité. Dans une liste, les utilisateurs voient votre vidéo avant les captures d'écran.

### <a name="select-a-category-for-your-app"></a>Sélectionner une catégorie pour votre application

Lors de la soumission, vous êtes invité à catégoriser votre application. Le tableau suivant ma Teams catégories de magasin aux catégories répertoriées dans [l'Partner Center](https://aka.ms/PartnerCenterHomePage).

| Teams catégories       | Catégories de l'Centre partenaires  |
|:---------------------|:---------------|
| Analyse et bi | Analyse, visualisation des données et bi |
| Développeur et informatique | Outils de développement, administrateur informatique |
| Éducation | Éducation |
| Ressources humaines | Ressources humaines et recrutement |
| Productivité | Gestion de contenu, fichiers et documents, productivité, formation et didacticiels, et utilitaires |
| Gestion de projet | Communication, gestion Project, flux de travail et gestion de l'entreprise |
| Ventes et support | Gestion des clients et des contacts, support client, gestion financière, ventes et marketing |
| Social et fun | Galeries d'images et de vidéos, style de vie, actualités et météo, réseau social, voyage et navigation |

### <a name="localize-your-store-listing"></a>Localisez votre liste dans le Store

L'Partner Center prend [en charge les listes de magasins localisées.](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions) Pour plus d'informations, voir comment localiser votre [liste Teams'application.](../../../../concepts/build-and-test/apps-localization.md)

## <a name="complete-publisher-verification"></a>Vérification Publisher complète

[Publisher vérification est](/azure/active-directory/develop/publisher-verification-overview) requise pour Teams applications répertoriées dans le Windows Store. Pour plus d'informations, voir [les questions fréquemment posées,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)comment marquer votre application comme éditeur vérifié et résoudre les problèmes de vérification de [l'éditeur](/azure/active-directory/develop/troubleshoot-publisher-verification). [](/azure/active-directory/develop/mark-app-as-publisher-verified)

## <a name="complete-publisher-attestation"></a>Attestation d'Publisher complète

[Publisher attestation est](/microsoft-365-app-certification/docs/attestation) également requise pour Teams applications répertoriées dans le Windows Store. Le processus inclut la réalisation d'une auto-évaluation de la sécurité, de la gestion des données et des pratiques de conformité de votre application qui peuvent aider les clients potentiels à prendre des décisions éclairées sur l'utilisation de votre application.

> [!NOTE]
> Si vous soumettez une nouvelle application, vous ne pouvez pas terminer officiellement l'attestation d'Publisher tant que votre application n'est pas répertoriée dans le Teams store. Si vous êtes en train de mettre à jour une application répertoriée, Publisher attestation avant de soumettre la dernière version de l'application pour validation.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Envoyer votre application](https://docs.microsoft.com/office/dev/store/add-in-submission-guide)
