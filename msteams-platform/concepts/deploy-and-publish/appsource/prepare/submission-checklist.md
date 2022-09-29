---
title: Préparer l'envoi de votre magasin
description: Découvrez les étapes finales avant de soumettre votre application Microsoft Teams à répertorier dans le Store. Apprenez à valider votre package d’application. Découvrez comment mettre à jour l’ID d’équipe Apple App Store Connect sur l’Espace partenaires.
ms.topic: how-to
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 9d850b76bddf288e766bdcc039711ef1d3059df8
ms.sourcegitcommit: c74e1e12175969c75e112a580949f96d2610c24e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2022
ms.locfileid: "68160712"
---
# <a name="prepare-your-teams-store-submission"></a>Préparer l'envoi de votre Magasin Teams

Vous avez conçu, créé et testé votre application Microsoft Teams. Vous êtes maintenant prêt à la répertorier afin que les utilisateurs puissent découvrir et commencer à utiliser votre application.

Regardez la vidéo suivante pour en savoir plus sur la publication de votre application dans l’App Store Microsoft Teams :
<br>

> [!VIDEO <https://www.microsoft.com/videoplayer/embed/RE4WG3l>]
<br>

Avant de soumettre votre application à [Espace partenaires](/office/dev/store/use-partner-center-to-submit-to-appsource), vérifiez que vous avez effectué les opérations suivantes.

## <a name="validate-your-app-package"></a>Valider votre package d’applications

Bien que votre application fonctionne dans un environnement de test, vous devez vérifier votre package d’application pour éviter de rencontrer des problèmes pendant le processus de soumission.

L’outil de validation d’application Microsoft Teams vous permet d’identifier et de résoudre les problèmes avant de les soumettre à Espace partenaires. L’outil vérifie automatiquement les configurations de votre application par rapport aux cas de test utilisés lors de la validation du Store.

1. Accédez à l’[outil de validation d’application Microsoft Teams](https://dev.teams.microsoft.com/appvalidation.html).

   Vous pouvez également valider votre application à l’aide [du portail des développeurs pour Teams.](~/concepts/build-and-test/teams-developer-portal.md)

1. Chargez votre package d’application pour exécuter les tests automatisés.
1. Accédez à la **liste de contrôle préliminaire** et passez en revue les cas de test difficiles à automatiser.
1. [Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general. These issues occur if the automated tests give you errors or you haven't met all the criteria in the checklist.

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

Le nom de votre application (plus précisément, son *[nom court](~/resources/schema/manifest-schema.md#name)*) joue un rôle essentiel dans la façon dont les utilisateurs le découvrent dans le Store.

:::row:::

:::column span="3":::
:::image type="content" source="../../../../assets/images/store-detail-page/specifying-short-name-under-submission.png" alt-text="Exemple de capture d’écran met en évidence l’affichage du nom court d’une application dans une description dans le Store.":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

Assurez-vous que votre nom court respecte les [instructions de validation du magasin](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name).

### <a name="write-descriptions"></a>Écrire des descriptions

Vous devez avoir une description courte et longue de votre application.

#### <a name="short-description"></a>Description courte

A concise summary of your app that should be original, engaging, and directed at your target audience. Keep the short description to one sentence.

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/specifying-short-description-under-submission.png" alt-text="Exemple de capture d’écran met en évidence l’affichage de la brève description d’une application dans une description du Store.":::
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
:::image type="content" source="~/assets/images/store-detail-page/specifying-long-description-under-submission.png" alt-text="Exemple de capture d’écran met en évidence l’affichage de la description longue d’une application dans une description du Store.":::
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
:::image type="content" source="~/assets/images/store-detail-page/specifying-of-capturing-screenshots-submission.png" alt-text="Exemple de capture d’écran met en évidence l’affichage des captures d’écran d’application dans une description dans le Store.":::
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

A video in your listing can be the most effective way to communicate why people should use your app. Address the following questions in a video:

* À qui est destinée votre application ?
* Quels problèmes votre application peut-elle résoudre ?
* Comment fonctionne votre application ?
* Quels autres avantages tirez-vous de l’utilisation de votre application ?

Vous pouvez ajouter une URL pour votre vidéo YouTube ou Vimeo.

#### <a name="best-practices-for-videos"></a>Meilleures pratiques pour les vidéos

* Conservez votre vidéo entre 60 et 90 secondes.
* Aim for quality. In a listing, users will see your video before screenshots.
* Communiquez la valeur du produit sous forme de narration.
* Montrez le fonctionnement du produit.

### <a name="select-a-category-for-your-app"></a>Sélectionner une catégorie pour votre application

Lors de l’envoi, vous êtes invité à classer votre application. Vous pouvez catégoriser votre application en fonction des catégories suivantes :

|Categories  |
|--------------|
| Microsoft |
| Éducation |
| Productivité |
| Images & galeries vidéo |
| Gestion de projet |
| Utilitaires |
| Social |
| Communication |
| Gestion de contenu |
| Fichiers & documents |
| Gestion des flux de travail & l’entreprise |
| Informatique/Administration |
| Ressources humaines & recrutement|
| Outils de développement |
| Réunions & planification |
| Visualisation des données & BI |
| Didacticiel & de formation |
| Actualités & météo |
| Service client |
| Référence |
| Marketing & des ventes |
| Regarder & sentir |
| Gestion des contacts client & (CRM) |
| Gestion financière |
| Mappe les flux & |
| Autre |

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
