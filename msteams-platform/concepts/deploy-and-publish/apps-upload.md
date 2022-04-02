---
title: Téléchargez votre application personnalisée
description: Découvrez comment charger votre application dans Microsoft Teams. Le chargement latéral est courant lors du test et du débogage d'une application pendant le développement.
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: a9ac73d3c3e41c5c57892273e788855a16642457
ms.sourcegitcommit: 3dc9b539c6f7fbfb844c47a78e3b4d2200dabdad
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2022
ms.locfileid: "64571105"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Téléchargez votre application dans Microsoft Teams

Vous pouvez télécharger les applications Microsoft Teams sans avoir à les publier dans votre organisation ou dans le magasin Teams dans les situations suivantes :

* Vous souhaitez tester et déboguer une application localement vous-même ou avec d'autres développeurs.
* Vous avez créé une application pour vous-même afin d’automatiser un flux de travail.
* Vous avez créé une application pour un petit groupe d'utilisateurs, tel que votre groupe de travail.

> [!IMPORTANT]
> Actuellement, les applications de chargement latéral sont disponibles dans Government Community Cloud (GCC), mais ne sont pas disponibles pour GCC-High et Department of Defence (DOD).

## <a name="prerequisites"></a>Configuration requise

* Veillez à créer votre [package d'application](~/concepts/build-and-test/apps-package.md) et [à le valider](https://dev.teams.microsoft.com/appvalidation.html) pour les erreurs.
* [Activez le téléchargement d'applications personnalisées](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) dans Teams.
* Assurez-vous que votre application est en cours d'exécution et accessible via HTTPS.

## <a name="upload-your-app"></a>Télécharger votre application

Vous pouvez télécharger votre application dans une équipe, un chat, une réunion ou pour un usage personnel selon la façon dont vous avez configuré la portée de votre application.

1. Connectez-vous au client Teams avec votre [compte de développement Microsoft 365](https://developer.microsoft.com/en-us/microsoft-365/dev-program).
1. Sélectionnez **Applications**, puis **Gérer vos applications**.
1. Sélectionnez **Charger une application personnalisée**.
1. Sélectionnez le fichier .zip de votre package d'application.
2. Ajoutez votre application à Teams en fonction de vos besoins :</br>

   Sélectionnez **Ajouter** pour ajouter votre application personnelle.</br>
   b. Utilisez le menu déroulant pour ajouter votre application à une équipe ou à une conversation.

![Créer une application Teams](~/assets/videos/app-teams.gif)

## <a name="troubleshooting"></a>Résolution des problèmes

Si votre application ne parvient pas à charger une version test ou si vous rencontrez des problèmes de chargement, vérifiez les options suivantes :

1. Assurez-vous que vous avez suivi toutes les instructions pour la [création de votre package d’application](../../concepts/build-and-test/apps-package.md).
1. [Validez votre package d'application](https://dev.teams.microsoft.com/appvalidation.html).
1. Assurez-vous que le manifeste de votre application correspond au dernier [schéma](../../resources/schema/manifest-schema.md).

## <a name="access-your-app"></a>Accéder à votre application

Teams propose plusieurs façons d'ouvrir des applications. Pour plus d'informations, voir [accéder à vos applications dans Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## <a name="update-your-app"></a>Mettre à jour votre application

Vous n'avez pas besoin de charger à nouveau votre application si vous apportez des modifications au code (celles-ci sont reflétées dans Teams en temps réel). Cependant, vous devez réinstaller si vous modifiez des configurations d'application.

## <a name="remove-your-app"></a>Supprimer votre application

Pour supprimer votre application, cliquez avec le bouton droit sur l'icône de l'application dans Teams et sélectionnez **Désinstaller**.

> [!NOTE]
>
> * Vous ne pouvez pas supprimer entièrement l’activité personnelle du bot. Si vous supprimez l’application et l’ajoutez à nouveau, la nouvelle communication avec le bot s’ajoute à la conversation précédente avec lui.
> * Actuellement, vous ne pouvez pas migrer votre application personnalisée vers le Magasin Teams. Si vous souhaitez répertorier votre application dans le Magasin Teams, consultez [Publier votre application dans le Microsoft Teams Store](appsource/publish.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Utiliser votre application Teams](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b)

## <a name="see-also"></a>Voir aussi

* [Configurer les options d’installation par défaut](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Maintenir votre application Microsoft Teams publiée](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
