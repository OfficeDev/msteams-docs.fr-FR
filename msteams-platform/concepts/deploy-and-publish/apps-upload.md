---
title: Téléchargez votre application personnalisée
description: Découvrez comment charger votre application dans Microsoft Teams. Le chargement latéral est courant lors du test et du débogage d'une application pendant le développement.
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: ffa7cdb0fabf07254c90590fe94fe2347c35658c
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044678"
---
# <a name="upload-your-app-in-teams"></a>Charger votre application dans Teams

Vous pouvez télécharger les applications Microsoft Teams sans avoir à les publier dans votre organisation ou dans le magasin Teams dans les situations suivantes :

* Vous souhaitez tester et déboguer une application localement vous-même ou avec d'autres développeurs.
* Vous avez créé une application pour vous-même afin d’automatiser un flux de travail.
* Vous avez créé une application pour un petit groupe d'utilisateurs, tel que votre groupe de travail.

> [!NOTE]
> Le chargement indépendant de votre application d’extension de messagerie plusieurs fois affiche plusieurs instances pour les extensions de messagerie.

> [!IMPORTANT]
>
> * Actuellement, le chargement indépendant des applications n’est possible que dans le cloud de la communauté du secteur public (GCC) et n’est pas possible dans GCC-High et le ministère de la Défense (DOD).
> * L’installation de l’application est prise en charge uniquement sur l’application de bureau Teams.

## <a name="prerequisites"></a>Configuration requise

* Veillez à créer votre [package d'application](~/concepts/build-and-test/apps-package.md) et [à le valider](https://dev.teams.microsoft.com/appvalidation.html) pour les erreurs.
* [Activez le téléchargement d'applications personnalisées](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) dans Teams.
* Assurez-vous que votre application est en cours d'exécution et accessible via HTTPS.

## <a name="upload-your-app"></a>Télécharger votre application

Vous pouvez télécharger votre application dans une équipe, un chat, une réunion ou pour un usage personnel selon la façon dont vous avez configuré la portée de votre application.

1. Connectez-vous au client Teams avec votre [compte de développement Microsoft 365](https://developer.microsoft.com/en-us/microsoft-365/dev-program).
1. Sélectionnez **Apps** > **Gérer vos applications** et **Publier une application**.

    :::image type="content" source="~/assets/images/publish-app/manage-apps.png" alt-text="Publier une application":::

1. Sélectionnez **Charger une application personnalisée**.

   :::image type="content" source="~/assets/images/publish-app/publish-app.png" alt-text="Charger une application personnalisée":::

1. Sélectionnez le fichier .zip de votre package d'application.
1. Ajoutez votre application à Teams en fonction de vos besoins :</br>

   a. Select **Add** to add your personal app.</br>
   b. Use the dropdown menu to add your app to a Team or chat.

    :::image type="content" source="~/assets/images/publish-app/teams-app-detail.png" alt-text="Description de l’application":::

## <a name="troubleshoot"></a>Résoudre des problèmes

Si votre application ne parvient pas à charger une version test ou rencontre des problèmes de chargement, consultez les options suivantes :

1. Vérifiez que vous avez suivi toutes les instructions pour la [création de votre package d’application](../../concepts/build-and-test/apps-package.md).
1. [Validez votre package d'application](https://dev.teams.microsoft.com/appvalidation.html).
1. Vérifiez que le manifeste de votre application correspond au [schéma](../../resources/schema/manifest-schema.md) le plus récent.

## <a name="manage-your-apps"></a>Gérer vos applications

Manage your apps allows users to have a dedicated place to manage, update and remove their apps, permissions, and subscriptions on the Teams client. The users can install the apps from **Manage your apps**.

### <a name="access-your-app"></a>Accéder à votre application

Pour accéder aux applications via **Gérer vos applications**, procédez comme suit :

1. Accédez à **Applications** et sélectionnez **Gérer vos applications** dans Teams pour afficher les applications installées sur tous vos canaux ou pour un usage personnel dans un format de liste.

    :::image type="content" source="~/assets/images/publish-app/manage-apps-list.png" alt-text="Accéder à la liste des applications Teams":::

1. Sélectionnez le menu déroulant de l’application pour afficher toutes les étendues où l’application est installée.

    :::image type="content" source="~/assets/images/publish-app/app-scopes.png" alt-text="Accéder à la portée de l’application Teams":::

1. Sélectionnez la portée de l’application pour accéder à l’application dans le canal ou la vue personnelle. La liste des étendues comprend uniquement l’étendue personnelle et l’étendue Teams. Les applications installées dans l’étendue de la conversation de groupe ne sont pas affichées dans cette vue pour le moment.

Teams propose plusieurs façons d'ouvrir des applications. Pour plus d'informations, voir [accéder à vos applications dans Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

### <a name="update-your-app"></a>Mettre à jour votre application

Vous n'avez pas besoin de charger à nouveau votre application si vous apportez des modifications au code (celles-ci sont reflétées dans Teams en temps réel). Cependant, vous devez réinstaller si vous modifiez des configurations d'application.

Si une mise à jour est disponible pour votre application, l’option **Mise à jour disponible** est activée. Pour mettre à jour, suivez les étapes :

1. Sélectionnez **Mettre à jour disponible** pour afficher la mise à jour.

     :::image type="content" source="~/assets/images/publish-app/update-available.png" alt-text="Mettez à jour l’application Teams.":::

1. Sélectionnez **Afficher la mise à jour**. Une fenêtre avec l’option de mise à jour s’affiche.
1. Sélectionnez le bouton **Mettre à jour** pour mettre à jour votre application.

     :::image type="content" source="~/assets/images/publish-app/update-window.png" alt-text="Mettez à jour l’application Teams dans gérer les applications.":::

     :::image type="content" source="~/assets/images/publish-app/updated-app.png" alt-text="Application mise à jour.":::

### <a name="remove-your-app"></a>Supprimer votre application

Pour supprimer l’application dans Teams, suivez les étapes :

1. Recherchez l’application dans **Gérer votre application**.

1. Sélectionnez &nbsp;:::image type="content" source="~/assets/images/publish-app/bin-icon.png" alt-text="Supprimer l’application dans Teams.":::&nbsp; à l’étendue de l’application installée.

    :::image type="content" source="~/assets/images/publish-app/uninstall-from-channel.png" alt-text="Supprimez l’application dans un canal.":::

1. Sélectionnez **Supprimer** pour supprimer votre application.

    :::image type="content" source="~/assets/images/publish-app/remove-app-teams.png" alt-text="Supprimez une application de Teams.":::

> [!NOTE]
>
> * You can't remove personal bot activity entirely. If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.
> * Actuellement, vous ne pouvez pas migrer votre application personnalisée vers le Magasin Teams. Si vous souhaitez répertorier votre application dans le Magasin Teams, consultez [Publier votre application dans le Microsoft Teams Store](appsource/publish.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
>[Créer des applications pour les réunions Teams](../../apps-in-teams-meetings/teams-apps-in-meetings.md)

## <a name="see-also"></a>Voir aussi

* [Configurer les options d’installation par défaut](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Maintenir votre application Microsoft Teams publiée](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
* [Ajouter une application à la conversation](/graph/api/chat-post-installedapps)
