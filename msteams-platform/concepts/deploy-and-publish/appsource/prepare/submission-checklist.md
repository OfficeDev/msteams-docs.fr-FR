---
title: Liste de vérification pour l’envoi
description: Liste de vérification à utiliser avant la publication de votre application Microsoft teams vers AppSource
keywords: teams publier le magasin de la liste de vérification de publication Office Publishing prepare
ms.openlocfilehash: 3379fe670c9835c1f2223067592d9574fff83a69
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801110"
---
# <a name="prepare-for-appsource-submission"></a>Préparer l’envoi de AppSource  

Pour figurer sur AppSource, votre application doit passer par un processus d’approbation. Il s’agit d’un service gratuit fourni par le groupe Microsoft teams qui vérifie que votre application fonctionne comme décrit, contient toutes les métadonnées appropriées et fournit un contenu qui pourrait être utile à un utilisateur final. Pour vous aider à obtenir une approbation rapide, vérifiez que votre application remplit les conditions et exigences suivantes :

* **Méthode de distribution :** Assurez-vous que votre application est destinée à un magasin. Il existe d' [autres options](../../overview.md) permettant de distribuer votre application sans la publier sur AppSource.
* **Page de détails de l’application :** Votre application est conforme à la [liste de contrôle des détails](detail-page-checklist.md) de l’application
* **Conseils et cas d’échec fréquents :** Prêtez une attention particulière à ces [conseils et aux cas souvent ayant échoué](frequently-failed-cases.md) pour améliorer la soumission de votre application au temps d’approbation.
* **Manifeste de l’application :** Vérifier le manifeste de votre application par rapport à la [liste de vérification du manifeste](app-manifest-checklist.md) de l’application et au vérificateur de manifeste dans App Studio
* **Test et débogage :** Vous avez entièrement [testé et débogué votre application](../../../build-and-test/debug.md).
* **Stratégies de validation :** Elle doit transmettre toutes les [stratégies de validation AppSource](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) actuelles pour les onglets et les robots Teams. Veuillez noter que ces stratégies peuvent faire l’objet de modifications.
* **Test des notes :** Inclure [des notes de test pour la validation](#test-notes-for-validation)
* **Stratégies de confidentialité :** Assurez-vous que votre [politique de confidentialité, les conditions d’utilisation et les URL de support](#privacy-policy-terms-of-use-and-support-urls) suivent nos instructions.

Une fois que vous avez effectué toutes les exigences ci-dessus, vous pouvez soumettre votre package à la source de l’application via le [Centre de partenaires](/office/dev/store/use-partner-center-to-submit-to-appsource).

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>Stratégie de confidentialité, conditions d’utilisation et URL de support

### <a name="privacy-policy"></a>Politique de confidentialité

Recommandations en matière de politique de confidentialité :
* La politique de confidentialité peut être spécifique à votre application et/ou complément ou à une stratégie globale pour tous vos services. 
* Si vous utilisez une stratégie de confidentialité générique, elle doit référencer « services/applications/plateformes » pour traiter votre application teams ainsi que votre site Web. 
* Elle doit inclure le mode de gestion des informations relatives au stockage des données utilisateur, à la rétention des données utilisateur, à la suppression et aux contrôles de sécurité.
* Il doit inclure vos coordonnées.
* Il ne doit pas contenir de liens rompus, d’URL bêta ou d’URL de transit. 

### <a name="terms-of-use"></a>Conditions d’utilisation

Votre déclaration de conditions d’utilisation doit être spécifique et applicable à votre application et/ou à votre offre de complément.

### <a name="support-urls"></a>URL de prise en charge

Vos URL de prise en charge ne doivent pas obligatoirement nécessiter une authentification ou des informations d’identification pour vous contacter pour les problèmes liés à votre application.

## <a name="test-notes-for-validation"></a>Notes de test pour la validation

Veuillez inclure les éléments suivants :

* Vous devez fournir au moins deux informations d’identification d’ouverture de session, un administrateur et un autre non-administrateur.

* À des fins de vérification, les comptes que vous fournissez doivent disposer de données pré-renseignées suffisantes.

* Pour les applications d’entreprise, les applications où un abonnement est requis, ou les applications où une dépendance client/domaine Office 365 est requise, vous devez fournir un troisième compte dans le même domaine qui n’est pas préconfiguré pour votre application afin de valider l’expérience utilisateur de première exécution.

* Si votre application dispose de fonctionnalités Premium/mises à niveau, un compte disposant de l’accès nécessaire doit être fourni pour tester cette expérience.

* Vous pouvez choisir de télécharger vos notes de test sur SharePoint. Si c’est le cas, indiquez un lien public vers le fichier.

* **Comptes de test**. Un compte de test est requis si votre application autorise uniquement les comptes sous licence ou la liste d’autorisation à partir du serveur principal. En outre, si une étendue de conversation d’équipe/de groupe est autorisée dans votre application, deux comptes de test dans le même client sont requis pour valider le scénario de collaboration d’équipe.

* **Étapes d’intégration**. Si une préconfiguration par un administrateur client est requise pour utiliser l’application, incluez les étapes et/ou fournissez les comptes administrateur et non administrateur configurés pour la validation. Remarque : vous pouvez vous inscrire pour obtenir un abonnement [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) . Elle est *gratuite* pendant 90 jours et se renouvelle en permanence tant que vous l’utiliserez pour l’activité de développement.

* **Remarques concernant les fonctionnalités de l’application dans teams**: détaillez toutes les fonctionnalités proposées par l’application dans teams et les étapes de test de chaque fonctionnalité.

* **Vidéo illustrant la fonctionnalité de l’application (facultatif)**: vous pouvez fournir un enregistrement vidéo du produit pour que nous comprenions entièrement les fonctionnalités de l’application.


