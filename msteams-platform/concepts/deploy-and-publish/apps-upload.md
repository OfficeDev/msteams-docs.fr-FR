---
title: Téléchargez votre application personnalisée
description: Découvrez comment charger votre application dans Microsoft Teams. Le chargement latéral est courant lors du test et du débogage d'une application pendant le développement.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.localizationpriority: high
---

# <a name="upload-your-app-in-microsoft-teams"></a>Téléchargez votre application dans Microsoft Teams

Vous pouvez télécharger les applications Microsoft Teams sans avoir à les publier dans votre organisation ou dans le magasin Teams. Cela a du sens dans les scénarios suivants :

* Vous souhaitez tester et déboguer une application localement vous-même ou avec d'autres développeurs.
* Vous avez créé une application rien que pour vous. Par exemple, pour automatiser un workflow.
* Vous avez créé une application pour un petit groupe d'utilisateurs, tel que votre groupe de travail.

> [!IMPORTANT]
> Actuellement, les applications de chargement latéral sont disponibles dans Government Community Cloud (GCC), mais ne sont pas disponibles pour GCC-High et Department of Defence (DOD).

## <a name="prerequisites"></a>Configuration requise

* Créez votre [package d'application](~/concepts/build-and-test/apps-package.md) et [validez-le](https://dev.teams.microsoft.com/appvalidation.html) pour les erreurs.
* [Activez le téléchargement d'applications personnalisées](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) dans Teams.
* Assurez-vous que votre application est en cours d'exécution et accessible via HTTPs.

## <a name="upload-your-app"></a>Télécharger votre application

Vous pouvez télécharger votre application dans une équipe, un chat, une réunion ou pour un usage personnel selon la façon dont vous avez configuré la portée de votre application.

1. Connectez-vous au client Teams avec votre [compte de développement Microsoft 365](~/build-your-first-app/build-and-run.md#prerequisites).
1. Sélectionnez **Applications** et choisissez **Charger une application personnalisée**.
1. Sélectionnez le fichier .zip de votre package d'application. Une boîte de dialogue d'installation s'affiche.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Capture d'écran montrant un exemple de boîte de dialogue d'installation de l'application Teams.":::
1. Ajoutez votre application à Teams.

> [!NOTE]
> La méthode `onInstallationUpdateActivityAsync()` est utilisée pour obtenir les paramètres régionaux de Microsoft Teams lors de l’ajout du bot à Microsoft Teams.

## <a name="troubleshoot-upload-issues"></a>Résoudre les problèmes de téléchargement

Si votre application ne parvient pas à se charger, procédez comme suit jusqu'à ce que le problème soit résolu :

1. Reprendre les instructions de [création de votre package d'application](../../concepts/build-and-test/apps-package.md).
1. [Valider à nouveau votre package d'application.](https://dev.teams.microsoft.com/appvalidation.html)
1. Assurez-vous que le manifeste de votre application correspond au dernier [schéma](../../resources/schema/manifest-schema.md).

## <a name="access-your-app"></a>Accéder à votre application

Teams propose plusieurs façons d'ouvrir des applications. Pour plus d'informations, voir [accéder à vos applications dans Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## <a name="update-your-app"></a>Mettre à jour votre application

Vous n'avez pas besoin de charger à nouveau votre application si vous apportez des modifications au code (celles-ci sont reflétées dans Teams en temps réel). Cependant, vous devez réinstaller si vous modifiez des configurations d'application.

## <a name="remove-your-app"></a>Supprimer votre application

Pour supprimer votre application, cliquez avec le bouton droit sur l'icône de l'application dans Teams et sélectionnez **Désinstaller**.

> [!NOTE]
> Vous ne pouvez pas supprimer entièrement l'activité personnelle du bot. Si vous supprimez l'application et l'ajoutez à nouveau, la nouvelle communication avec le bot s'ajoute à la conversation précédente avec lui.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Utiliser votre application Teams](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)

## <a name="see-also"></a>Voir aussi

* [Configurer les options d’installation par défaut](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Maintenir votre application Microsoft Teams publiée](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
