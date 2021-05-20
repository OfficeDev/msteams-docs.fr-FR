---
title: Télécharger votre application personnalisée
description: Découvrez comment sideload votre application dans Microsoft Teams. Le chargement latéral est courant lors du test et du débogage d’une application pendant le développement.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565192"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Télécharger votre application dans Microsoft Teams

Vous pouvez sideload Microsoft Teams applications sans avoir à publier à votre organisation ou le magasin Teams magasin. Cela est logique dans les scénarios suivants :

* Vous souhaitez tester et déboger une application localement vous-même ou avec d’autres développeurs.
* Vous avez créé une application juste pour vous-même. Par exemple, automatiser un flux de travail.
* Vous avez créé une application pour un petit ensemble d’utilisateurs, tels que votre groupe de travail.

## <a name="prerequisites"></a>Configuration requise

* Créez votre paquet [d’applications](~/concepts/build-and-test/apps-package.md) et [validez-le pour](https://dev.teams.microsoft.com/appvalidation.html) les erreurs.
* [Activez le téléchargement d’applications](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) personnalisées dans Teams.
* Assurez-vous que votre application est en cours d’exécution et accessible via https.

## <a name="upload-your-app"></a>Télécharger votre application

Vous pouvez mettre votre application sur le côté d’une équipe, d’un chat, d’une réunion ou d’un usage personnel en fonction de la façon dont vous avez configuré la portée de votre application.

1. Connectez-vous au client Teams avec votre [compte Microsoft 365 développement de vos clients.](~/build-your-first-app/build-and-run.md#prerequisites)
1. Sélectionnez **apps** et **choisissez Télécharger une application personnalisée**.
1. Sélectionnez votre paquet d’application .zip fichier. Un dialogue d’installation affiche.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Capture d’écran montrant un exemple d’Teams appos de messagerie installer le dialogue.":::
1. Ajoutez votre application à Teams.

## <a name="troubleshoot-upload-issues"></a>Résoudre les problèmes de téléchargement

Si votre application ne se charge pas latéralement, faites ce qui suit jusqu’à ce que le problème se résout :

1. Revenez en arrière par les instructions pour [créer votre paquet d’application.](../../concepts/build-and-test/apps-package.md)
1. [Validez à nouveau votre package](https://dev.teams.microsoft.com/appvalidation.html) d’application.
1. Assurez-vous que votre manifeste d’application correspond au [dernier schéma](../../resources/schema/manifest-schema.md).

## <a name="access-your-app"></a>Accédez à votre application

Teams fournit plusieurs façons d’ouvrir des applications. Pour plus d’informations, [consultez l’accès à vos applications dans Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## <a name="update-your-app"></a>Mettre à jour votre application

Vous n’avez pas à recharger votre application à nouveau si vous modifiez le code (celles-ci sont reflétées dans Teams en temps réel). Toutefois, vous devez réinstaller si vous modifiez les configurations d’application.

## <a name="remove-your-app"></a>Supprimez votre application

Pour supprimer votre application, cliquez à droite sur l’icône de l’application Teams et **sélectionnez Désinstaller**.

> [!NOTE]
> Vous ne pouvez pas supprimer complètement l’activité personnelle du bot. Si vous supprimez l’application et l’ajoutez à nouveau, une nouvelle communication avec le bot s’ajoute à la conversation précédente avec elle.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Utilisez votre application Teams](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
