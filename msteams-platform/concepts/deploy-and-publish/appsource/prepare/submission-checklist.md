---
title: Préparer l'envoi de votre magasin
description: Décrit les étapes finales avant de soumettre votre application Microsoft Teams à répertorier sur le Store. Découvrez comment valider votre package d’application, compiler des instructions de test et créer les détails de votre description dans le Store.
ms.topic: how-to
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
keywords: les instructions de validation de package d’application de la banque de soumissions sont localisées
ms.openlocfilehash: e1c2f94eb0bb3989ea461b10543fcea3051ef52a
ms.sourcegitcommit: 591bab4c7e01ac9099b9a540f149b64e6e31e6e8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2022
ms.locfileid: "65135751"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>Préparer votre soumission au Microsoft Teams store

Vous avez conçu, créé et testé votre application Microsoft Teams. Vous êtes maintenant prêt à la répertorier afin que les utilisateurs puissent découvrir et commencer à utiliser votre application.

Avant de soumettre votre application à [Espace partenaires](/office/dev/store/use-partner-center-to-submit-to-appsource), vérifiez que vous avez effectué les opérations suivantes.

## <a name="validate-your-app-package"></a>Valider votre package d’applications

Bien que votre application fonctionne dans un environnement de test, vous devez vérifier votre package d’application pour éviter de rencontrer des problèmes pendant le processus de soumission.

> [!NOTE]
 > Si vous utilisez App Studio, nous vous recommandons d’essayer le [Portail des développeurs](https://dev.teams.microsoft.com/) pour configurer, distribuer et gérer vos applications Teams. App Studio sera déconseillé d’ici le 30 juin 2022.

L’outil de validation d’application Microsoft Teams vous permet d’identifier et de résoudre les problèmes avant de les soumettre à Espace partenaires. L’outil vérifie automatiquement les configurations de votre application par rapport aux cas de test utilisés lors de la validation du Store.

1. Accédez à l’[outil de validation d’application Microsoft Teams](https://dev.teams.microsoft.com/appvalidation.html). (Remarque : l’outil est également disponible dans [App Studio](../../../build-and-test/app-studio-overview.md).)
1. Chargez votre package d’application pour exécuter les tests automatisés.
1. Accédez à la **liste de contrôle préliminaire** et passez en revue les cas de test difficiles à automatiser.
1. [Résoudre les problèmes liés à vos configurations](~/resources/schema/manifest-schema.md) ou application en général. Ces problèmes se produisent si les tests automatisés vous donnent des erreurs ou si vous ne répondez pas à tous les critères de la liste de vérification.

## <a name="compile-testing-instructions"></a>Compiler les instructions de test

Fournissez des instructions et des ressources pour aider les réviseurs à tester votre application, notamment :

* Tester les comptes
* Identifiants
* Clés de licence

Vous pouvez ajouter des instructions dans Espace partenaires ou les charger dans un emplacement disponible publiquement sur SharePoint.

### <a name="feature-list"></a>Liste des fonctionnalités

Fournissez des détails sur les fonctionnalités de votre application dans Teams et les étapes de test de chacune d’elles.

### <a name="accounts"></a>Comptes

Fournissez des comptes de test si votre application nécessite une licence ou une liste fiable de back-end. Tous les comptes que vous fournissez doivent inclure des données préremplies pour faciliter les tests.

Selon les fonctionnalités de votre application, vous devrez peut-être fournir tous les comptes suivants :

* Compte d’administrateur (obligatoire)
* Compte non administrateur (obligatoire)
* Un compte qui n’est pas préconfiguré pour tester correctement l’expérience de connexion de première exécution (obligatoire)
* Un compte ayant accès aux fonctionnalités Premium ou mises à niveau (le cas échéant)
* Deux comptes dans le même locataire pour tester l’expérience de collaboration pour les applications qui fonctionnent dans des contextes partagés (le cas échéant)

### <a name="tenant-configurations"></a>Configurations de locataire

Si vous devez configurer un locataire Teams pour utiliser votre application, incluez ces instructions et les comptes administrateur et non-administrateur à des fins de validation.

### <a name="video-optional"></a>Vidéo (facultatif)

Fournissez un enregistrement de votre application afin que Microsoft puisse comprendre pleinement ses fonctionnalités.

## <a name="create-your-store-listing-details"></a>Créer les détails de votre description dans le Store

Les informations que vous envoyez à [Espace partenaires](https://partner.microsoft.com)&#8212;y compris votre nom, descriptions, icônes et images&#8212;deviennent la description de votre application dans le magasin Teams et Microsoft AppSource.

Une description dans le Store peut être la première impression d’une personne sur votre application. Augmentez les installations avec une liste qui transmet efficacement les avantages, les fonctionnalités et la marque de votre application.

### <a name="specify-a-short-name"></a>Spécifier un nom court

Le nom de votre application (plus précisément, son [*nom court*](~/resources/schema/manifest-schema.md#name)) joue un rôle essentiel dans la façon dont les utilisateurs le découvrent dans le Store.

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Exemple de capture d’écran met en évidence l’affichage du nom court d’une application dans une description dans le Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre nom court respecte les [instructions de validation du magasin](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name).

### <a name="write-descriptions"></a>Écrire des descriptions

Vous devez avoir une description courte et longue de votre application.

#### <a name="short-description"></a>Description courte

Résumé concis de votre application qui doit être original, attrayant et destiné à votre public cible. Conservez la brève description d’une phrase.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Exemple de capture d’écran met en évidence l’affichage de la brève description d’une application dans une description du Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre brève description respecte les [instructions de validation du magasin](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description).

#### <a name="long-description"></a>Description longue

La description longue peut fournir une narration qui met en évidence vos applications :

* Principales fonctionnalités
* Les problèmes qu’il résout
* Public cible

Bien que cette description puisse contenir jusqu’à 4 000 caractères, la plupart des utilisateurs ne lisent qu’entre 300 et 500 mots.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Exemple de capture d’écran met en évidence l’affichage de la description longue d’une application dans une description du Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre description longue respecte les [instructions de validation du magasin](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description).

### <a name="adhere-to-icon-design-guidelines"></a>Respecter les instructions de conception d’icône

Les icônes sont l’un des principaux éléments que les utilisateurs voient lors de la navigation dans le Store. Vos icônes doivent communiquer la marque et l’objectif de votre application tout en respectant les exigences de Teams.

Pour plus d’informations, consultez les[conseils sur la création d’icônes d’application Teams](~/concepts/build-and-test/apps-package.md#app-icons).

### <a name="capture-screenshots"></a>Captures d’écran

Les captures d’écran fournissent un aperçu visuel évident de votre application pour compléter le nom, l’icône et les descriptions de votre application.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Exemple de capture d’écran met en évidence l’affichage des captures d’écran d’application dans une description dans le Store.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

N’oubliez pas les meilleures pratiques suivantes concernant les captures d’écran :

* Vous pouvez avoir jusqu’à cinq captures d’écran par référencement.
* Les types de fichiers pris en charge incluent les formats d’image .png, .jpeg et gif.
* Les dimensions doivent être de 1366 x 768 pixels.
* Taille maximale de 1 024 Ko.

Pour connaître les meilleures pratiques, consultez les ressources suivantes :

* [Instructions de validation du Magasin Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [Créer des images efficaces pour les magasins d’applications Microsoft](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>Créer une vidéo

Une vidéo dans votre description peut être le moyen le plus efficace de communiquer pourquoi les utilisateurs doivent utiliser votre application. Répondez aux questions suivantes dans une vidéo :

* À qui est destinée votre application ?
* Quels problèmes votre application peut-elle résoudre ?
* Comment fonctionne votre application ?
* Quels autres avantages tirez-vous de l’utilisation de votre application ?

Vous pouvez ajouter une URL pour votre vidéo YouTube ou Vimeo.

#### <a name="best-practices-for-videos"></a>Meilleures pratiques pour les vidéos

* Conservez votre vidéo entre 60 et 90 secondes.
* Visez la qualité. Dans une liste, les utilisateurs verront votre vidéo avant les captures d’écran.
* Communiquez la valeur du produit sous forme de narration.
* Montrez le fonctionnement du produit.

### <a name="select-a-category-for-your-app"></a>Sélectionner une catégorie pour votre application

Lors de l’envoi, vous êtes invité à classer votre application. Le tableau suivant mappe les catégories du Magasin Teams aux catégories répertoriées dans [Espace partenaires](https://aka.ms/PartnerCenterHomePage).

| Catégories Teams       | Espace partenaires catégories  |
|:---------------------|:---------------|
| Analyse et BI | Analytique, visualisation des données et décisionnel |
| Développeur et informatique | Outils de développement, administrateur informatique |
| Formation | Formation |
| Ressources humaines | Ressources humaines et recrutement |
| Productivité | Gestion de contenu, fichiers et documents, productivité, formation et didacticiels, et utilitaires |
| Gestion de projet | Communication, gestion de projet, flux de travail et gestion d’entreprise |
| Ventes et support | Gestion des clients et des contacts, support client, gestion financière et ventes et marketing |
| Social et divertissement | Galeries d’images et de vidéos, Style de vie, Actualités et météo, Réseaux sociaux, Voyage et Navigation |

### <a name="localize-your-store-listing"></a>Localiser votre description dans le Store

Espace partenaires prend en charge les[listes de magasins localisées](/office/dev/store/prepare-localized-solutions). Pour plus d’informations, consultez [comment localiser votre liste d’applications Teams](../../../../concepts/build-and-test/apps-localization.md).

## <a name="complete-publisher-verification"></a>Terminer la vérification de l’éditeur

[Vérification de l’éditeur](/azure/active-directory/develop/publisher-verification-overview) est nécessaire pour les applications Teams répertoriées dans le Store. Pour plus d’informations, voir [forum aux questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [comment marquer votre application comme éditeur vérifié](/azure/active-directory/develop/mark-app-as-publisher-verified) et [résoudre les problèmes de vérification de l’éditeur](/azure/active-directory/develop/troubleshoot-publisher-verification).

## <a name="complete-publisher-attestation"></a>Terminer l’attestation du serveur de publication

[Attestation d’éditeur](/microsoft-365-app-certification/docs/attestation) est également requise pour les applications Teams répertoriées dans le Store. Le processus inclut l’exécution d’une auto-évaluation des pratiques de sécurité, de gestion des données et de conformité de votre application. Le processus peut aider les clients potentiels à prendre des décisions éclairées sur l’utilisation de votre application.

> [!NOTE]
> Si vous soumettez une nouvelle application, vous ne pouvez pas terminer officiellement l’attestation du serveur de publication tant que votre application n’est pas répertoriée dans le Magasin Teams. Si vous mettez à jour une application répertoriée, effectuez l’attestation de l’éditeur avant de soumettre la dernière version de l’application pour validation.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Envoyer votre application](/office/dev/store/add-in-submission-guide)

## <a name="see-also"></a>Voir aussi

[Résoudre les problèmes en cas d’échec de l’envoi de votre magasin Microsoft Teams](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)
