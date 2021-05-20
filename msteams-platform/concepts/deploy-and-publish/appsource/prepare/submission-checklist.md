---
title: Préparer l'envoi de votre magasin
description: Décrit les dernières étapes avant de soumettre votre Microsoft Teams’application à coté sur le magasin.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 975d3ef8fc8bdc8d6d7c336cf3a61a3a42ef5315
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566032"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>Préparez votre soumission Microsoft Teams magasin

Vous avez conçu, construit et testé votre application Microsoft Teams. Maintenant, vous êtes prêt à l’énumérer afin que les gens puissent découvrir et commencer à utiliser votre application.

Avant de soumettre votre application à [Partner Center,](/office/dev/store/use-partner-center-to-submit-to-appsource)assurez-vous d’avoir fait ce qui suit.

## <a name="validate-your-app-package"></a>Valider votre package d’application

Bien que votre application fonctionne peut-être dans un environnement de test, vous devez vérifier votre paquet d’applications pour éviter de tomber sur des problèmes pendant le processus de soumission.

L’Microsoft Teams validation d’application vous aide à identifier et à résoudre les problèmes avant de vous soumettre au Partner Center. L’outil vérifie automatiquement les configurations de votre application par rapport aux mêmes cas de test utilisés lors de la validation en magasin.

1. Allez à [l’outil Microsoft Teams validation de l’application](https://dev.teams.microsoft.com/appvalidation.html). (Note: L’outil est également disponible dans [App Studio](../../../build-and-test/app-studio-overview.md).)
1. Télécharger paquet d’applications pour exécuter les tests automatisés.
1. Consultez la liste **de vérification préliminaire et** examinez les cas de test difficiles à automatiser.
1. [Résoudre les problèmes avec vos configurations ou](~/resources/schema/manifest-schema.md) application en général si les tests automatisés vous donnent des erreurs ou si vous n’avez pas satisfait à tous les critères de la liste de contrôle.

## <a name="compile-testing-instructions"></a>Compiler les instructions de test

Fournissez des instructions et des ressources pour aider les examinateurs à tester votre application, y compris les comptes de test, les informations d’identification et les clés de licence. Vous pouvez ajouter des instructions dans Partner Center ou les télécharger sur un emplacement accessible au public sur SharePoint.

### <a name="feature-list"></a>Liste des fonctionnalités

Fournissez des détails sur les capacités de votre application dans Teams et les étapes pour tester chacune d’entre vous.

### <a name="accounts"></a>Comptes

Vous devez fournir des comptes de test si votre application nécessite une licence ou une liste de sécurité backend. Tous les comptes que vous fournissez doivent inclure des données pré-remplies pour faciliter les tests.

Selon les fonctionnalités de votre application, vous devrez peut-être fournir tous les éléments suivants :

* Compte admin (requis)
* Compte non admin (requis)
* Un compte qui n’est pas préconfiguré afin de tester correctement l’expérience de connecte de première série (requise)
* Un compte ayant accès à des fonctionnalités premium ou améliorées (le cas échéant)
* Deux comptes dans le même locataire pour tester l’expérience de collaboration pour les applications qui fonctionnent dans des contextes partagés (le cas échéant)

### <a name="tenant-configurations"></a>Configurations des locataires

Si vous devez configurer un Teams pour utiliser votre application, incluez ces instructions et les comptes d’administration et non admin pour validation.

### <a name="video-optional"></a>Vidéo (facultatif)

Fournissez un enregistrement de votre application afin que Microsoft puisse bien comprendre ses fonctionnalités.

## <a name="create-your-store-listing-details"></a>Créez les détails de votre annonce de magasin

Les informations que vous soumettez [à Partner Center](https://partner.microsoft.com)&#8212;y compris votre nom, descriptions, icônes et images&#8212;devient le magasin Teams et microsoft AppSource liste pour votre application.

Une annonce de magasin peut être la première impression de quelqu’un de votre application. Augmentez les installations avec une liste qui transmet efficacement les avantages, les fonctionnalités et la marque de votre application.

### <a name="specify-a-short-name"></a>Spécifier un nom court

Le nom de votre application (en particulier, son nom [*court) joue*](~/resources/schema/manifest-schema.md#name)un rôle crucial dans la façon dont les utilisateurs la découvrent dans le magasin.

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Exemple de capture d’écran met en évidence où le nom court d’une application s’affiche dans une annonce de magasin.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre nom court respecte les lignes directrices [de validation du magasin.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)

### <a name="write-descriptions"></a>Rédiger des descriptions

Vous devez avoir une description courte et longue de votre application.

#### <a name="short-description"></a>Description brève

Un résumé concis de votre application qui doit être original, engageant et dirigé vers votre public cible. Gardez la courte description à une phrase.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Exemple de capture d’écran met en évidence où la courte description d’une application s’affiche dans une annonce de magasin.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre courte description respecte les lignes directrices [de validation du magasin.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)

#### <a name="long-description"></a>Description longue

La longue description peut fournir un récit qui met en évidence les principales fonctionnalités de votre application, les problèmes qu’elle résout, et son public cible. Bien que cette description puisse aller jusqu’à 4 000 caractères, la plupart des utilisateurs ne liront qu’entre 300 et 500 mots.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="Exemple de capture d’écran met en évidence où la longue description d’une application s’affiche dans une liste de magasins.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Assurez-vous que votre longue description respecte les lignes directrices [de validation du magasin.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)

### <a name="adhere-to-icon-design-guidelines"></a>Respecter les lignes directrices sur la conception d’icônes

Les icônes sont l’un des principaux éléments que les utilisateurs voient lors de la navigation dans le magasin. Vos icônes doivent communiquer la marque et le but de votre application tout en respectant les Teams exigences.

Pour plus d’informations, consultez [les conseils sur la création Teams icônes d’applications](~/concepts/build-and-test/apps-package.md#app-icons).

### <a name="capture-screenshots"></a>Capturez des captures d’écran

Les captures d’écran fournissent un aperçu visuel important de votre application pour compléter le nom, l’icône et les descriptions de votre application.

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="Exemple de capture d’écran met en évidence où les captures d’écran d’application s’affichent dans une liste de magasins.":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

Rappelez-vous ce qui suit sur les captures d’écran:

* Vous pouvez avoir jusqu’à cinq captures d’écran par annonce.
* Les types de fichiers pris en charge incluent PNG, JPEG et GIF.
* Les dimensions doivent être de 1366x768 pixels.
* Taille maximale de 1 024 KB.

Pour les meilleures pratiques, consultez les ressources suivantes :

* [Teams de validation des magasins](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [Créez des images efficaces pour les magasins d’applications Microsoft](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>Créer une vidéo

Une vidéo dans votre annonce peut être le moyen le plus efficace de communiquer pourquoi les gens devraient utiliser votre application. Vous devez répondre aux questions suivantes dans une vidéo :

* Qui est votre application pour?
* Quels problèmes votre application peut-elle résoudre ?
* Comment fonctionne votre application ?
* Quels autres avantages bénéficiez-vous de l’utilisation de votre application ?

#### <a name="best-practices-for-videos"></a>Meilleures pratiques pour les vidéos

* Gardez votre vidéo entre 30-90 secondes.
* Visez la qualité. Dans une annonce, les utilisateurs verront votre vidéo avant les captures d’écran.

### <a name="select-a-category-for-your-app"></a>Sélectionnez une catégorie pour votre application

Lors de la soumission, il vous est demandé de classer votre application. Les cartes de tableau suivantes Teams les catégories de magasins aux catégories énumérées dans [Partner Center](https://aka.ms/PartnerCenterHomePage).

| Teams catégories       | Catégories de centres partenaires  |
|:---------------------|:---------------|
| Analyse et BI | Analyse, visualisation de données et BI |
| Développeur et informatique | Outils de développeur, administrateur informatique |
| Éducation | Éducation |
| Ressources humaines | Ressources humaines et recrutement |
| Productivité | Gestion de contenu, fichiers et documents, productivité, formation et didacticiels et services publics |
| Gestion de projet | Communication, Project, Workflow et Gestion d’entreprise |
| Ventes et support | Gestion de la clientèle et des contacts, soutien à la clientèle, gestion financière, ventes et marketing |
| Social et amusant | Galeries d’images et de vidéos, mode de vie, nouvelles et météo, social, voyage et navigation |

### <a name="localize-your-store-listing"></a>Localisez votre annonce de magasin

Partner Center prend en [charge les annonces localisées des magasins](/office/dev/store/prepare-localized-solutions). Pour plus d’informations, [découvrez comment localiser votre liste d Teams apprisation .](../../../../concepts/build-and-test/apps-localization.md)

## <a name="complete-publisher-verification"></a>Vérification complète Publisher’œil

[Publisher vérification est](/azure/active-directory/develop/publisher-verification-overview) nécessaire pour les Teams les applications répertoriées dans le magasin. Pour plus d’informations, [consultez les questions fréquemment posées,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)comment marquer votre application comme éditeur [vérifié, et](/azure/active-directory/develop/mark-app-as-publisher-verified)la vérification de [l’éditeur de dépannage](/azure/active-directory/develop/troubleshoot-publisher-verification).

## <a name="complete-publisher-attestation"></a>Attestation Publisher complète

[Publisher attestation est](/microsoft-365-app-certification/docs/attestation) également nécessaire pour les Teams les applications répertoriées dans le magasin. Le processus comprend l’auto-évaluation des pratiques de sécurité, de traitement des données et de conformité de votre application qui peuvent aider les clients potentiels à prendre des décisions éclairées concernant l’utilisation de votre application.

> [!NOTE]
> Si vous soumettez une nouvelle application, vous ne pouvez pas remplir officiellement l’attestation Publisher tant que votre application n’est pas répertoriée sur le Teams store. Si vous mettez à jour une application répertoriée, remplissez Publisher attestation avant de soumettre la dernière version de l’application pour validation.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Envoyer votre application](/office/dev/store/add-in-submission-guide)
