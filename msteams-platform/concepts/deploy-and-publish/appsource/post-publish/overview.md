---
title: Maintenir et prendre en charge votre application publiée
description: Découvrez comment gérer votre application Microsoft Teams publiée et ce à quoi vous devez penser une fois que votre magasin est répertorié sur le Magasin Teams et AppSource.
ms.topic: conceptual
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 3e73725bcfd1f51cc2f1ab82ba7437b205028c09
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66484844"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>Maintenir votre application Microsoft Teams publiée

Une fois votre application répertoriée dans le store Microsoft Teams, commencez à réfléchir à la façon dont vous allez gérer l’application à l’avenir et augmenter les téléchargements et l’utilisation.

## <a name="analyze-app-usage"></a>Analyser l’utilisation des applications

Vous pouvez suivre l’utilisation de votre application dans le [rapport d’utilisation des applications Teams](/office/dev/store/teams-apps-usage) dans Espace partenaires. Les mesures incluent les utilisateurs actifs mensuels, quotidiens et hebdomadaires, ainsi que les graphiques de rétention et d’intensité qui vous permettent de suivre l’évolution et la fréquence de l’utilisation.

L’affichage des données concernant les applications récemment publiées prend environ une semaine dans le rapport.

## <a name="publish-updates-to-your-app"></a>Publier des mises à jour sur votre application

> [!NOTE]
> Le magasin Teams a évolué :
>
> Auparavant, les liens étaient copiés en sélectionnant des points de suspension sur la vignette de l’application. Avec l’expérience mise à jour du magasin Teams, vous accédez de la même manière à partir de l’onglet Détails des applications. Cette mise à jour sera mise à la disposition générale d’ici le 1er mars 2022.

Vous pouvez envoyer des modifications à votre application (telles que de nouvelles fonctionnalités ou même des métadonnées) dans Espace partenaires. Ces modifications nécessitent un nouveau processus d’évaluation.

Vérifiez les éléments suivants lors de la publication des mises à jour :

* Ne modifiez pas votre ID d’application.
* Incrémentez le numéro de version de votre application.
* Dans Espace partenaires, ne sélectionnez pas **Ajouter une nouvelle application** pour effectuer la mise à jour. Accédez plutôt à la page de votre application.

### <a name="app-updates-requiring-user-consent"></a>Mises à jour d’application nécessitant le consentement de l’utilisateur

Lorsqu’un utilisateur installe votre application, il doit lui accorder l’autorisation d’accéder aux services et aux informations dont l’application a besoin pour fonctionner. Dans la plupart des cas, cette action ne doit être effectuée qu’une seule fois et la nouvelle version de votre application s'installe automatiquement.
Toutefois, si vous apportez l’une des modifications suivantes à votre application, vos utilisateurs existants doivent accepter une autre demande d’autorisation pour installer la mise à jour :

* Ajout ou suppression d’un bot.
* Modification de l’ID du bot.
* Modification de la configuration de notification unidirectionnelle d’un bot.
* Modification de la prise en charge d’un bot pour le chargement et le téléchargement de fichiers.
* Ajoutez ou supprimez une extension de message.
* Ajout d’un onglet personnel.
* Création d’un onglet de canal et de groupe.
* Ajout d’un connecteur.
* Modifiez les configurations liées à l’inscription de votre application Microsoft Azure Active Directory (Azure AD). Pour plus d’informations, consultez [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="fix-issues-with-your-published-app"></a>Résoudre les problèmes liés à votre application publiée

Microsoft exécute des tests d’automatisation quotidiens sur les applications répertoriées dans le magasin Teams. Si des problèmes liés à votre application sont identifiés, nous vous contactons avec un rapport détaillé sur la façon de reproduire les problèmes et les recommandations pour les résoudre. Si vous ne pouvez pas résoudre les problèmes dans une chronologie, la liste de votre application peut être supprimée du Store.

## <a name="promote-your-app-on-another-site"></a>Promouvoir votre application sur un autre site

Lorsque votre application est répertoriée dans le Magasin Teams, vous pouvez créer un lien qui lance Teams et affiche une boîte de dialogue pour installer votre application. Vous pouvez inclure ce lien, par exemple, avec un bouton de téléchargement sur la page marketing de votre produit.

Créez le lien à l’aide de l’URL suivante ajoutée à votre ID d’application : `https://teams.microsoft.com/l/app/<your-app-id>`.

## <a name="complete-microsoft-365-certification"></a>Terminer la certification Microsoft 365

[Microsoft 365 Certification](/microsoft-365-app-certification/docs/certification) garantit que les données et la confidentialité sont correctement sécurisées et protégées lorsqu’une application Office tierce ou un complément est installé dans votre écosystème Microsoft 365. La certification confirme que votre application est compatible avec les technologies Microsoft, qu’elle est conforme aux meilleures pratiques de sécurité des applications cloud et qu’elle est prise en charge par Microsoft.

## <a name="stop-app-distribution"></a>Arrêter la distribution des applications

Vous pouvez supprimer une application de la [Place de marché commerciale Microsoft](/azure/marketplace/overview) pour empêcher sa découverte et son utilisation.

Pour arrêter la distribution d’une application une fois que vous l’avez publié, procédez comme suit :

1. Dans la page **Vue d’ensemble du produit**, **sélectionnez Arrêter la vente**. Elle supprime l’application de Microsoft AppSource.
1. Pour lancer la suppression de la liste de l’application, dans **Espace partenaires**, sélectionnez la page **Vue d’ensemble**, puis **Arrêtez la vente**.

Après avoir arrêté la distribution d’une application, vous pouvez toujours la voir dans Espace partenaires avec un état **Non disponible** . Si vous décidez de répertorier à nouveau l’application, suivez les instructions pour [publier votre application dans le Microsoft Teams Store](../publish.md).

## <a name="see-also"></a>Voir aussi

[Monétisez votre application via Microsoft Commercial Marketplace](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
