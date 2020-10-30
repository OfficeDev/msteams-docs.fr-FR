---
title: Liste de vérification pour l’envoi
description: Liste de vérification à utiliser avant la publication de votre application Microsoft teams vers AppSource
keywords: teams publier le magasin Office Publishing liste de vérification de la soumission applications teams AppSource validation
ms.openlocfilehash: 1b25a449901c303269334e5cea6de46fa3b6f6e5
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796301"
---
# <a name="prepare-for-appsource-submission"></a>Préparer l’envoi de AppSource  

Pour figurer sur AppSource, votre application doit passer par un processus d’approbation. Il s’agit d’un service gratuit fourni par le groupe Microsoft teams qui vérifie que votre application fonctionne comme décrit, contient toutes les métadonnées appropriées et fournit un contenu qui pourrait être utile à un utilisateur final. Pour vous aider à obtenir une approbation rapide, vérifiez que votre application remplit les conditions et exigences suivantes :

* **Méthode de distribution :** Assurez-vous que votre application est destinée à être compubliée sur une plateforme de magasin. Il existe d' [autres options](../../overview.md) permettant de distribuer votre application sans la publier sur AppSource.
* **Stratégies de validation :** Votre application doit transmettre toutes les [stratégies de validation AppSource](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) actuelles avant l’envoi. Veuillez noter que ces stratégies peuvent faire l’objet de modifications. 
* * * Testez votre application avec l' [outil de validation de manifeste](#teams-app-validation-tool) .
* **Page de détails de l’application :** Votre application doit s’aligner sur la liste de vérification de la  [page détaillée](detail-page-checklist.md)de l’application.
* **Conseils et cas d’échec fréquents :** Prêtez une attention particulière aux [conseils cités et aux cas souvent infructueuses](frequently-failed-cases.md)  pour améliorer le temps d’envoi et d’approbation de votre application.
* **Manifeste de l’application :** Vérifiez le manifeste de votre application par rapport à la [liste de vérification du manifeste](app-manifest-checklist.md)de l’application.
* **Test et débogage :** Assurez-vous que vous avez entièrement [testé et débogué votre application](../../../build-and-test/debug.md).
* **Test des notes :** Inclure vos [notes de test pour validation](#test-notes-for-validation)
* **Stratégies de confidentialité :** Assurez-vous que votre [politique de confidentialité, les conditions d’utilisation et les URL de support](#privacy-policy-terms-of-use-and-support-urls) suivent nos instructions.

Une fois que vous avez effectué toutes les exigences ci-dessus, envoyez votre package à AppSource via le [Centre de partenaires](/office/dev/store/use-partner-center-to-submit-to-appsource).

## <a name="teams-app-validation-tool"></a>Outil de validation des applications teams

L’outil de validation d’application se compose d’un [validateur d’application](#teams-app-validator) et d’une [liste de vérification préliminaire](#preliminary-checklist). L’outil réplique les mêmes cas de test utilisés par [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) pour évaluer la soumission de votre application. Par conséquent, il est essentiel de transmettre tous les cas de test avant de soumettre votre solution à AppSource pour approbation. L’outil peut être trouvé dans plusieurs zones de la plateforme teams :

> [!div class="checklist"]
>
> * [**Page d’accueil du validateur d’application**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**Kit de développement Visual Studio Visual Studio teams**](/toolkit/visual-studio-code-overview.md)
> * [**App Studio**](/concepts/build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>Validateur d’application teams

La page **valider** vous permet de vérifier votre package d’application avant de l’envoyer à AppSource. Il suffit de charger votre package d’application et l’outil de validation vérifie votre application par rapport à tous les cas de test liés au manifeste. Pour chaque test ayant échoué, la description fournit un lien vers la documentation pour vous aider à résoudre l’erreur.

![Outil de validation](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>Liste de vérification préliminaire

Pour les scénarios de test difficiles à automatiser, la liste de vérification préliminaire couvre sept des cas de test les plus fréquents.

![Liste de vérification préliminaire](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>Stratégie de confidentialité, conditions d’utilisation et URL de support

### <a name="privacy-policy"></a>Politique de confidentialité

Recommandations en matière de politique de confidentialité :

> [!div class="checklist"]
>
> * La stratégie de confidentialité peut être spécifique à votre application et/ou une stratégie globale pour tous vos services.
> * Si vous utilisez une stratégie de confidentialité générique, il doit faire référence aux « services », « applications » et « plateformes » pour inclure votre application teams ainsi que votre site Web.
> * Elle doit inclure le mode de gestion du stockage des données utilisateur, de la rétention, de la suppression et des contrôles de sécurité des utilisateurs.
> * Il doit inclure vos coordonnées.
> * Il ne doit pas contenir de liens rompus, d’URL bêta ou d’URL de transit.

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

* **Comptes de test** . Un compte de test est requis si votre application autorise uniquement les comptes sous licence ou safelisting à partir du serveur principal. En outre, si une étendue de conversation d’équipe/de groupe est autorisée dans votre application, deux comptes de test dans le même client sont requis pour valider le scénario de collaboration d’équipe.

* **Étapes d’intégration** . Si une préconfiguration par un administrateur client est requise pour utiliser l’application, incluez les étapes et/ou fournissez les comptes administrateur et non administrateur configurés pour la validation. Remarque : vous pouvez vous inscrire pour obtenir un abonnement [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) . Elle est *gratuite* pendant 90 jours et se renouvelle en permanence tant que vous l’utiliserez pour l’activité de développement.

* **Remarques concernant les fonctionnalités de l’application dans teams** : détaillez toutes les fonctionnalités proposées par l’application dans teams et les étapes de test de chaque fonctionnalité.

* **Vidéo illustrant la fonctionnalité de l’application (facultatif)** : vous pouvez fournir un enregistrement vidéo du produit pour que nous comprenions entièrement les fonctionnalités de l’application.
