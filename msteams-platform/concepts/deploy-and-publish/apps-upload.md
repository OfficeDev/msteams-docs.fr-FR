---
title: Télécharger votre application personnalisée
description: Découvrez comment recharger une version de version de votre application dans Microsoft Teams. Le chargement de version test est courant lors du test et du débogage d’une application pendant le développement.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 93df0d92ce6912888dd1932be3295ca92fa5a967
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345261"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Télécharger votre application dans Microsoft Teams

Vous pouvez télécharger une version Microsoft Teams applications sans avoir à publier dans votre organisation ou le Teams store. Cela est logique dans les scénarios suivants :

* Vous souhaitez tester et déboguer une application localement vous-même ou avec d’autres développeurs.
* Vous avez créé une application uniquement pour vous-même. Par exemple, pour automatiser un flux de travail.
* Vous avez créé une application pour un petit groupe d’utilisateurs, par exemple, votre groupe de travail.

> [!IMPORTANT]
> Pour l’instant, les applications de chargement de version Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), mais ne sont pas disponibles pour GCC-High et le Département de la Défense (DOD).

## <a name="prerequisites"></a>Conditions préalables

* Créez votre [package d’application](~/concepts/build-and-test/apps-package.md) [et validez-le pour les](https://dev.teams.microsoft.com/appvalidation.html) erreurs.
* [Activez le chargement d’applications personnalisées](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) dans Teams.
* Assurez-vous que votre application est en cours d’exécution et accessible via HTTPs.

## <a name="upload-your-app"></a>Télécharger votre application

Vous pouvez charger une version de votre application vers une équipe, une conversation, une réunion ou pour une utilisation personnelle en fonction de la façon dont vous avez configuré l’étendue de votre application.

1. Connectez-vous au client Teams avec [votre compte Microsoft 365 développement.](~/build-your-first-app/build-and-run.md#prerequisites)
1. Sélectionnez **applications** et choisissez **Télécharger une application personnalisée.**
1. Sélectionnez votre package d'.zip fichier. Une boîte de dialogue d’installation s’affiche.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Screenshot showing an example of a Teams app install dialog.":::
1. Ajoutez votre application à Teams.

## <a name="troubleshoot-upload-issues"></a>Résoudre les problèmes de téléchargement

Si le chargement de version de votre application échoue, faites les choses suivantes jusqu’à ce que le problème soit résolu :

1. Revenir en arrière dans les instructions de [création de votre package d’application.](../../concepts/build-and-test/apps-package.md)
1. [Validez à nouveau votre package d’application.](https://dev.teams.microsoft.com/appvalidation.html)
1. Assurez-vous que le manifeste de votre application correspond au [schéma le plus récent.](../../resources/schema/manifest-schema.md)

## <a name="access-your-app"></a>Accéder à votre application

Teams propose plusieurs façons d’ouvrir des applications. Pour plus d’informations, [voir accéder à vos applications dans Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## <a name="update-your-app"></a>Mettre à jour votre application

Vous n’avez pas à recharger votre application de nouveau si vous a apporté des modifications de code (celles-ci sont reflétées dans Teams en temps réel). Toutefois, vous devez réinstaller si vous modifiez des configurations d’application.

## <a name="remove-your-app"></a>Supprimer votre application

Pour supprimer votre application, cliquez avec le bouton droit sur l’icône de l’Teams puis **sélectionnez Désinstaller.**

> [!NOTE]
> Vous ne pouvez pas supprimer entièrement l’activité du bot personnel. Si vous supprimez l’application et l’ajoutez à nouveau, une nouvelle communication avec le bot s’ajoute à la conversation précédente avec elle.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Utiliser votre application Teams de messagerie](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
