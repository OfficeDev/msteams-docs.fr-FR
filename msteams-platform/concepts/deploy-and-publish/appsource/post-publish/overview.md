---
title: Maintenir et prendre en charge votre application publiée
description: Ce à quoi il faut penser une fois que votre magasin est répertorié dans Teams store et AppSource.
ms.topic: conceptual
ms.localizationpriority: medium
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 5c85d30e595d30a236318d13535584d949b1075a
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212411"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>Maintenir votre application Microsoft Teams publiée

Une fois votre application répertoriée dans le Microsoft Teams, commencez à réfléchir à la façon dont vous allez gérer l’application à l’avenir et augmenter les téléchargements et l’utilisation.

## <a name="publish-updates-to-your-app"></a>Publier des mises à jour sur votre application

> [!NOTE]
> Teams magasin a évolué :
> 
> Auparavant, les liens étaient copiés en sélectionnant des ellipses sur la vignette de l’application. Une fois l’expérience Teams mise à jour mise à jour, vous accéderez à la même expérience à partir de l’onglet Détails des applications. Cette mise à jour sera généralement disponible d’ici le 01 mars 2022.

Vous pouvez soumettre des modifications à votre application (par exemple, de nouvelles fonctionnalités ou même des métadonnées) dans l’Partner Center. Ces modifications nécessitent un nouveau processus de révision.

Veillez à ce qui suit lors de la publication des mises à jour :

* Ne modifiez pas votre ID d’application.
* Incrémentez le numéro de version de votre application.
* Dans l’Partner Center, ne sélectionnez **pas Ajouter une nouvelle application** pour la mise à jour. À la place, allez sur la page de votre application.

### <a name="app-updates-requiring-user-consent"></a>Mises à jour d’application nécessitant le consentement de l’utilisateur

Lorsqu’un utilisateur installe votre application, il doit lui accorder l’autorisation d’accéder aux services et aux informations dont l’application a besoin pour fonctionner. Dans la plupart des cas, les utilisateurs doivent le faire une seule fois et les nouvelles versions de votre application s’installent automatiquement.
Toutefois, si vous a apporté l’une des modifications suivantes à votre application, vos utilisateurs existants doivent accepter une autre demande d’autorisation pour installer la mise à jour :

* Ajoutez ou supprimez un bot.
* Modifiez l’ID du bot.
* Modifier la configuration de notification à sens seul d’un bot.
* Modifier la prise en charge d’un bot pour le chargement et le téléchargement de fichiers.
* Ajouter ou supprimer une extension de messagerie.
* Ajoutez un onglet personnel.
* Ajoutez un canal et un onglet de groupe.
* Ajoutez un connecteur.
* Modifiez les configurations liées à l’inscription Azure Active Directory votre application. Pour plus dʼinformations, reportez-vous à [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="fix-issues-with-your-published-app"></a>Résoudre les problèmes avec votre application publiée

Microsoft exécute des tests d’automatisation quotidiens sur les applications répertoriées dans Teams store. Si des problèmes avec votre application sont identifiés, nous vous contactons avec un rapport détaillé sur la façon de reproduire les problèmes et les recommandations pour les résoudre. Si vous ne pouvez pas résoudre les problèmes dans une chronologie, la liste de votre application peut être supprimée du Store.

## <a name="promote-your-app-on-another-site"></a>Promouvoir votre application sur un autre site

Lorsque votre application est répertoriée dans le magasin Teams, vous pouvez créer un lien qui lance Teams et affiche une boîte de dialogue pour installer votre application. Vous pouvez inclure ce lien, par exemple, avec un bouton de téléchargement sur la page marketing de votre produit.

Créez le lien à l’aide de l’URL suivante, à l’aide de l’ID de votre application `https://teams.microsoft.com/l/app/<your-app-id>` :

## <a name="complete-microsoft-365-certification"></a>Certification Microsoft 365 complète

[Microsoft 365 certification](/microsoft-365-app-certification/docs/certification) garantit que les données et la confidentialité sont correctement sécurisées et protégées lorsqu’un application Office ou un add-in tiers est installé dans votre écosystème Microsoft 365. La certification confirme que votre application est compatible avec les technologies Microsoft, conforme aux meilleures pratiques de sécurité des applications cloud et prise en charge par Microsoft.

## <a name="see-also"></a>Voir aussi

[Monétisez votre application via Microsoft Commercial Marketplace](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
