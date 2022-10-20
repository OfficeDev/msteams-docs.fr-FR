---
title: Maintenir et prendre en charge votre application publiée
description: Gérez votre application Microsoft Teams publiée. Analyser l’utilisation des applications, publier des mises à jour, promouvoir votre application, terminer la certification Microsoft 365.
ms.topic: conceptual
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: cbb97bd1fcd3422af968e7928436f4da1ae4038d
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615288"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>Maintenir votre application Microsoft Teams publiée

Une fois votre application répertoriée dans le store Microsoft Teams, commencez à réfléchir à la façon dont vous allez gérer l’application à l’avenir et augmenter les téléchargements et l’utilisation.

## <a name="analyze-app-usage"></a>Analyser l’utilisation des applications

Vous pouvez suivre l’utilisation de votre application dans le [rapport d’utilisation des applications Teams](/office/dev/store/teams-apps-usage) dans Espace partenaires. Les mesures incluent les utilisateurs actifs mensuels, quotidiens et hebdomadaires, ainsi que les graphiques de rétention et d’intensité qui vous permettent de suivre l’évolution et la fréquence de l’utilisation.

L’affichage des données concernant les applications récemment publiées prend environ une semaine dans le rapport.

## <a name="publish-updates-to-your-app"></a>Publier des mises à jour sur votre application

Vous pouvez envoyer des modifications à votre application (telles que de nouvelles fonctionnalités ou même des métadonnées) dans Espace partenaires. Ces modifications nécessitent un nouveau processus d’évaluation.

Vérifiez les éléments suivants lors de la publication des mises à jour :

* Ne modifiez pas votre ID d’application.
* Incrémentez le numéro de version de votre application.
* In Partner Center, don't select **Add a new app** to do the update. Go to your app's page instead.

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
* Modify configurations related to your Microsoft Azure Active Directory (Azure AD) app registration. For more information, see [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).

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
