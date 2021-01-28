---
title: Liste de vérification de soumission au Store
description: Liste de vérification à utiliser avant la publication de votre application Microsoft Teams dans AppSource
ms.topic: reference
keywords: teams publish store office publishing checklist submission Teams apps appsource validation
ms.openlocfilehash: 7cb9192c159e7d65aad188c9746de3de7947a42b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014214"
---
# <a name="prepare-for-appsource-submission"></a>Préparer la soumission d’AppSource  

Pour être répertoriée sur AppSource, votre application doit passer par un processus d’approbation. Il s’agit d’un service gratuit fourni par le groupe Microsoft Teams qui vérifie que votre application fonctionne comme décrit, contient toutes les métadonnées appropriées et fournit du contenu qui serait utile pour un utilisateur final. Pour vous aider à obtenir une approbation rapide, assurez-vous que votre application répond aux exigences et instructions suivantes :

* **Méthode de distribution :** Assurez-vous que votre application est destinée à être publiée sur une plateforme du Store. Il existe [d’autres options](../../overview.md) de distribution de votre application sans publication dans AppSource.
* **Stratégies de validation :** Votre application doit transmettre toutes les stratégies de [validation AppSource actuelles](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) avant sa soumission. 
  > [!NOTE] 
  > Les stratégies de validation Appsource sont sujettes à modification.
* **Préparation mobile :** Votre application doit être mobile réactive. Si votre application contient des onglets, ils doivent respecter les [instructions](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) de conception [pour](~/tabs/design/tabs-mobile.md) appareils mobiles et votre application ne doit respecter aucune exigence de vente à la vente sur le système d’exploitation mobile (iOS et Android).
* **Testez vous-même votre application :** Testez votre application à l’aide [de l’outil de validation de manifeste.](#teams-app-validation-tool)
* **Page de détails de l’application :** Votre application doit s’aligner sur la liste [de contrôle de la page de détails de l’application.](detail-page-checklist.md)
* **Conseils et cas d’échec fréquents :** Accordez une attention [](frequently-failed-cases.md) particulière aux conseils répertoriés et aux cas d’échec fréquents pour améliorer le temps de soumission et d’approbation de votre application.
* **Manifeste de l’application :** Vérifiez le manifeste de votre application par rapport à la liste [de contrôle du manifeste de l’application.](app-manifest-checklist.md)
* **Test et débogage :** Assurez-vous que vous avez entièrement testé et [débouggé votre application.](../../../build-and-test/debug.md)
* **Notes de test :** Inclure vos [notes de test pour la validation](#test-notes-for-validation)
* **Stratégies de confidentialité :** Assurez-vous [que votre politique de confidentialité, vos conditions d’utilisation et vos URL de support](#privacy-policy-terms-of-use-and-support-urls) respectent nos recommandations.

Une fois que vous avez rempli toutes les conditions ci-dessus, envoyez votre package à AppSource via [l’Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource).

## <a name="teams-app-validation-tool"></a>Outil de validation d’application Teams

L’outil de validation d’application se compose d’un [validateur](#teams-app-validator) d’application et d’une liste [de contrôle préliminaire.](#preliminary-checklist) L’outil réplique les mêmes cas de test utilisés par [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) pour évaluer la soumission de votre application. Par conséquent, il est essentiel de réussir tous les cas de test avant de soumettre votre solution à AppSource pour approbation. L’outil se trouve dans plusieurs zones de la plateforme Teams :

> [!div class="checklist"]
>
> * [**Page d’accueil du validateur d’application**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**Boîte à outils Visual Studio Code teams**](/toolkit/visual-studio-code-overview.md)
> * [**App Studio**](/concepts/build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>Validateur d’application Teams

La page **Valider** vous permet de vérifier votre package d’application avant de le soumettre à AppSource. Il vous suffit de charger votre package d’application et l’outil de validation vérifie votre application par rapport à tous les cas de test liés au manifeste. Pour chaque test qui a échoué, la description fournit un lien de documentation pour vous aider à corriger l’erreur.

![Outil de validation](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>Liste de contrôle préliminaire

Pour les scénarios de test qui sont difficiles à automatiser, la liste de contrôle préliminaire surfaces sept des cas de test les plus couramment échoués.

![Liste de contrôle préliminaire](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>Politique de confidentialité, conditions d’utilisation et URL de support

### <a name="privacy-policy"></a>Politique de confidentialité

Recommandations en matière de politique de confidentialité :

> [!div class="checklist"]
>
> * La politique de confidentialité peut être spécifique à votre application et/ou à une stratégie globale pour tous vos services.
> * Si vous utilisez une stratégie de confidentialité générique, elle doit faire référence aux « services », aux « applications » et aux « plateformes » pour inclure votre application Teams ainsi que votre site web.
> * Il doit inclure la façon dont vous traitez le stockage des données utilisateur, la rétention, la suppression et les contrôles de sécurité des données utilisateur.
> * Il doit inclure vos informations de contact.
> * Elle ne doit pas contenir de liens rompus, d’URL bêta ou d’URL intermédiaire.

### <a name="terms-of-use"></a>Conditions d’utilisation

Votre déclaration de conditions d’utilisation doit être spécifique et applicable à votre application et/ou votre offre de add-in.

### <a name="support-urls"></a>URL de prise en charge

Vos URL de support ne doivent pas nécessiter d’authentification ou d’informations d’identification pour vous contacter pour tout problème avec votre application.

## <a name="test-notes-for-validation"></a>Notes de test pour la validation

Incluez les informations suivantes :

* Vous devez fournir au moins deux informations d’identification de connexion, un administrateur et un non administrateur.

* À des fins de vérification, les comptes que vous fournissez doivent avoir suffisamment de données pré-remplies.

* Pour les applications d’entreprise, les applications où un abonnement est requis ou les applications où il existe une dépendance client/domaine Office 365, vous devez fournir un troisième compte dans le même domaine qui n’est pas pré-configuré pour votre application afin que nous pouvons valider l’expérience utilisateur de première utilisation.

* Si votre application dispose de fonctionnalités premium/mises à niveau, un compte avec l’accès nécessaire doit être fourni pour tester cette expérience.

* Vous pouvez choisir de télécharger vos notes de test sur SharePoint. Si c’est le cas, veuillez fournir un lien public vers le fichier.

* **Comptes de test**. Un compte de test est requis si votre application autorise uniquement les comptes sous licence ou la liste sécurisée à partir du back-end. En outre, si une étendue de conversation d’équipe/groupe est autorisée dans votre application, deux comptes de test dans le même client sont requis pour valider le scénario de collaboration d’équipe.

* **Étapes d’intégration.** Si la pré-configuration par un administrateur client est requise pour utiliser l’application, incluez les étapes et/ou fournissez des comptes d’administrateur et non administrateur configurés pour la validation. Remarque : vous pouvez vous inscrire à un abonnement au programme pour les développeurs [Office 365.](https://developer.microsoft.com/microsoft-365/dev-program) Il est *gratuit pendant* 90 jours et est continuellement renouvelé tant que vous l’utilisez pour l’activité de développement.

* **Remarques concernant les fonctionnalités de** l’application dans Teams : détaillez toutes les fonctionnalités de l’application dans Teams et les étapes de test de chaque fonctionnalité.

* **Vidéo montrant la fonctionnalité de** l’application (facultatif) : vous pouvez fournir un enregistrement vidéo du produit pour nous aider à bien comprendre les fonctionnalités de l’application.
