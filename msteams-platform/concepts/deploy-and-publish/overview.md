---
title: Distribuer votre application.
description: Décrit les trois options de distribution de votre application .
ms.topic: conceptual
localization_priority: Normal
keywords: teams publish store office distribute AppSource sideload upload app
ms.openlocfilehash: a033b90be436fbf20ef11fe95059d04388cefdf8
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020778"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribuer votre application Microsoft Teams

Une fois que vous avez créé votre application, trois options s'offrent à vous pour la distribuer :

1. [Chargez votre application directement.](#upload-your-app-directly)
2. [Publiez votre application dans le catalogue d'applications de votre organisation.](#publish-to-your-organizations-app-catalog)
3. [Publiez votre application via AppSource.](#publish-to-appsource)

## <a name="enterprise-organizations"></a>Organisations d'entreprise

### <a name="upload-your-app-directly"></a>Charger votre application directement

Il s'agit du moyen le plus simple de tester et d'utiliser votre application. Si vous êtes le propriétaire de l'équipe et/ou si le téléchargement d'applications personnalisées est [activé,](/microsoftteams/admin-settings)vous pouvez directement charger (ou charger une version de [chargement)](./apps-upload.md) de l'application et commencer à l'utiliser immédiatement. Toutefois, si vous souhaitez partager l'application avec d'autres personnes, vous devez leur envoyer votre package d'application et leur demander de la télécharger indépendamment.

Si vous souhaitez distribuer votre application plus largement, Teams fournit une galerie dans l'application pour que les utilisateurs trouvent ou découvrent des applications Teams de haute qualité. Pour que votre solution soit disponible dans la galerie, vous devez soit publier dans le catalogue [d'applications](#publish-to-your-organizations-app-catalog) de votre organisation, soit [publier sur AppSource.](./appsource/publish.md)

### <a name="publish-to-your-organizations-app-catalog"></a>Publier dans le catalogue d'applications de votre organisation

Le catalogue d'applications de votre organisation contient des applications propres à votre organisation et est entièrement sous le contrôle de votre organisation. Vous trouverez plus d'informations dans l'article Publier des applications dans [*le catalogue d'applications de votre organisation.*](/microsoftteams/tenant-apps-catalog-teams) Cette fonctionnalité peut uniquement être gérée par les utilisateurs de Teams Microsoft Office 365 privilèges d'administrateur client.

### <a name="publish-to-appsource"></a>Publier sur AppSource

AppSource (anciennement Appelé Office Store) vous permet de distribuer facilement votre application Microsoft Teams, ainsi que d'autres types d'extensibilité Office 365 tels que les applications Office et SharePoint. Suivez nos instructions pour [soumettre votre application à AppSource.](./appsource/publish.md)

## <a name="government-community-cloud-gcc-organizations"></a>Organisations gcc (Government Community Cloud)

### <a name="upload-your-custom-app-directly-to-teams"></a>Télécharger votre application personnalisée directement dans Teams

 En tant qu'administrateur client GCC, vous devez décider s'il faut télécharger une application personnalisée dans votre environnement client et la publier dans votre catalogue d'applications client. Microsoft ne possède pas ou ne contrôle pas vos applications personnalisées, par conséquent, vous devez vous assurer que tous les points de terminaison sont conformes aux exigences de votre organisation. En outre, si la solution d'application inclut une extension de bot ou de message, vous devez terminer l'inscription [bot Framework](https://dev.botframework.com/) comme suit :

1. Dans la page **Se connecter aux canaux,** sous **Ajouter un canal sélectionné,** sélectionnez **Teams.**
1. Accédez à la page **Configurer MSTeams** *(voir ci-dessous).*
1. Sous **Messagerie, sélectionnez** la **radio Microsoft Teams pour les clients du** gouvernement.
1. Dans le coin inférieur gauche de la page, sélectionnez **Enregistrer.**  

>[!IMPORTANT]
> Vous ne pouvez pas utiliser la configuration commerciale teams pour charger/charger une version de votre application personnalisée dans un environnement GCC. Vous devez sélectionner la radio **Microsoft Teams pour** les clients du secteur secteur pour une configuration CONFORME GCC.

![Page de configuration de la messagerie Teams](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * Les instructions de téléchargement pour les environnements GCC, présentées ci-dessus, s'appliquent aux applications personnalisées Teams. </br>
> * Les applications Microsoft conformes sont activées dans l'environnement GCC, par défaut, dans Teams.
> * Les applications tierces sont désactivées au niveau du client et doivent être gérées via les stratégies d'autorisation [d'application de votre organisation.](/microsoftteams/teams-app-permission-policies) Veillez à passer en revue toutes les applications tierces pour vous assurer qu'elles s'alignent sur les stratégies et procédures de votre organisation.

> [!TIP]
>
> Les partenaires de développement Microsoft 365 fournissent des détails sur la sécurité, la gestion des données et la conformité pour leurs applications Teams tierces via le programme de certification des applications [Microsoft 365.](/microsoft-365-app-certification/overview) *Voir aussi Certification* [des applications Microsoft Teams.](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification)
</br></br>
