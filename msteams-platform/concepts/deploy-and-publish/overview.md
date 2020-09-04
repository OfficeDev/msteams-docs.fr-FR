---
title: Distribuer votre application.
description: Décrit les trois options de distribution de votre application'
keywords: Team Publish Store Office distribue AppSource chargement upload App
ms.openlocfilehash: d3fd81e69f74b6332d9033412a7b6688239cd801
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340957"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribuer votre application Microsoft teams

Une fois que vous avez créé votre application, vous disposez de trois options pour la distribuer :

1. [Téléchargez votre application directement](#upload-your-app-directly).
2. [Publiez votre application dans le catalogue d’applications de votre organisation](#publish-to-your-organizations-app-catalog).
3. [Publiez votre application via AppSource](#publish-to-appsource).

## <a name="enterprise-organizations"></a>Organisations d’entreprise

### <a name="upload-your-app-directly"></a>Télécharger directement votre application

Il s’agit de la méthode la plus simple pour tester et utiliser votre application. Si vous êtes le propriétaire de l’équipe et/ou que le téléchargement d' [applications personnalisées est activé](/microsoftteams/admin-settings), vous pouvez [directement télécharger (ou chargement)](./apps-upload.md) l’application et commencer à l’utiliser immédiatement. Toutefois, si vous souhaitez partager l’application avec d’autres utilisateurs, vous devrez leur envoyer votre package d’application et leur demander de le charger indépendamment.

Si vous souhaitez distribuer votre application plus largement, teams fournit une galerie d’applications pour les utilisateurs qui souhaitent trouver ou découvrir des applications de teams de grande qualité. Pour que votre solution soit disponible dans la Galerie, vous devez la [publier dans le catalogue d’applications de votre organisation](#publish-to-your-organizations-app-catalog) ou la [publier sur AppSource](./appsource/publish.md).

### <a name="publish-to-your-organizations-app-catalog"></a>Publier dans le catalogue d’applications de votre organisation

Le catalogue d’applications de votre organisation contient des applications propres à votre organisation et se trouve entièrement sous le contrôle de votre organisation. Vous trouverez plus d’informations dans l’article [*publier des applications dans le catalogue d’applications de votre organisation*](/microsoftteams/tenant-apps-catalog-teams). Cette fonctionnalité ne peut être gérée que par des utilisateurs de teams disposant de privilèges d’administrateur client Microsoft Office 365.

### <a name="publish-to-appsource"></a>Publier sur AppSource

AppSource (anciennement appelé Office Store) fournit un emplacement pratique pour la distribution de votre application Microsoft Teams, ainsi que d’autres types d’extensibilité Office 365, tels que les compléments Office et les compléments SharePoint. Suivez nos instructions pour [soumettre votre application à AppSource](./appsource/publish.md).

## <a name="government-community-cloud-gcc-organizations"></a>Organisations de cloud public (GCC)

### <a name="upload-your-custom-app-directly-to-teams"></a>Charger votre application personnalisée directement dans teams

 En tant qu’administrateur client GCC, vous allez décider s’il faut télécharger une application personnalisée dans votre environnement client et si vous souhaitez la publier dans votre catalogue d’applications client. Microsoft ne peut pas détenir ou contrôler vos applications personnalisées, par conséquent, vous devez vous assurer que tous les points de terminaison sont conformes aux exigences de votre organisation. En outre, si la solution d’application inclut un bot ou une extension de message, vous devez effectuer l’inscription de l' [infrastructure de robot](https://dev.botframework.com/) comme suit :

1. Sur la page **se connecter aux canaux** , sous **Ajouter un canal proposé**, sélectionnez **teams**.
1. Accédez à la page **configurer MSTeams** (*voir* ci-dessous).
1. Sous **messagerie** , sélectionnez la case **d’option Microsoft teams pour les clients gouvernementaux** .
1. Dans le coin inférieur gauche de la page, sélectionnez **Enregistrer**.  

>[!IMPORTANT]
> Vous ne pouvez pas utiliser la configuration commerciale de teams pour télécharger/chargement votre application personnalisée dans un environnement GCC, vous devez sélectionner la case d’option **Microsoft teams pour les clients gouvernementaux** pour une configuration compatible GCC.

![Page Configuration de la messagerie teams](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * Les instructions de téléchargement pour les environnements GCC, présentés ci-dessus, s’appliquent aux applications personnalisées Teams. </br>
> * Les applications Microsoft conformes sont activées dans l’environnement GCC, par défaut, dans Teams.
> * Les applications tierces sont désactivées au niveau du client et doivent être gérées via les [stratégies d’autorisation](/microsoftteams/teams-app-permission-policies)de l’application de votre organisation. Assurez-vous que vous examinez toutes les applications tierces pour vous assurer qu’elles s’alignent avec les stratégies et procédures de votre organisation.

> [!TIP]
>
> Les partenaires de développeurs Microsoft 365 fournissent des informations sur la sécurité, la gestion des données et la conformité pour leurs applications de teams tierces via le programme de certification de l' [application Microsoft 365](/microsoft-365-app-certification/overview). *Voir aussi* [certification des applications Microsoft teams](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification).
</br></br>
