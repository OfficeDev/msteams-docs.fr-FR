---
title: Vue d’ensemble - Distribuer votre application
description: Décrit les options de publication de votre application Microsoft Teams, de chargement de votre application et de Cloud de la communauté du secteur public.
ms.topic: conceptual
author: v-rpatkur
ms.author: surbhigupta
ms.localizationpriority: none
keywords: déployer publier le gcc de chargement d’application
ms.openlocfilehash: 5db182f9276865fc98d277f642f7e58fd4a52df5
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104433"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribuer votre application Microsoft Teams

Vous pouvez fournir votre application Microsoft Teams à une personne, une équipe, une organisation ou toute personne qui souhaite l’utiliser. La façon dont vous distribuez dépend de plusieurs facteurs, notamment les besoins des utilisateurs, l’entreprise, les exigences techniques et vos objectifs pour l’application.

## <a name="configure-default-install-options"></a>Configurer les options d’installation par défaut

Vous configurez les options d’installation par défaut. Par exemple, si la fonctionnalité principale de votre application est un bot, vous pouvez également faire du bot la fonctionnalité par défaut lorsqu’un utilisateur installe votre application dans une équipe.

## <a name="create-your-app-package"></a>Créer votre package d’application

Pour distribuer votre application Microsoft Teams, vous devez disposer d’un package d’application valide.  Un package d’application est un fichier zip qui contient un **manifeste d’application** et **des icônes d’application**.

## <a name="upload-your-app-in-teams"></a>Télécharger votre application dans Teams

Chargez une application à des fins personnelles, collaborez avec votre équipe ou testez et déboguez. Ce type de distribution ne nécessite pas de processus d’examen formel.

> [!IMPORTANT]
> Actuellement, les applications de chargement latéral sont disponibles dans Government Community Cloud (GCC), mais ne sont pas disponibles pour GCC-High et Department of Defence (DOD).

Pour plus d’informations, consultez [charger votre application dans Teams](apps-upload.md).

## <a name="publish-your-app-to-your-org"></a>Publier votre application dans votre organisation

Mettez votre application à la disposition des personnes de votre organisation. Ce type de distribution nécessite l’approbation de votre administrateur Teams.

Pour plus d’informations, consultez [gérer vos applications dans le centre d’administration Teams](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json).

### <a name="government-community-cloud-gcc-organizations"></a>organisations Cloud de la communauté du secteur public (Cloud de la communauté du secteur public)

Dans Cloud de la communauté du secteur public Teams environnements, les applications Microsoft conformes sont activées par défaut. Toutefois, avant de publier une application, assurez-vous que tous les points de terminaison de l’application sont conformes aux exigences de votre organisation Cloud de la communauté du secteur public. Pour plus d’informations, consultez [Cloud de la communauté du secteur public](../app-fundamentals-overview.md#government-community-cloud).

> [!IMPORTANT]
>Si votre application inclut un bot ou une extension de message, vous devez sélectionner l’option **Microsoft Teams for Government** lors de la configuration d’un canal entre votre bot et Teams dans Azure. Pour plus d’informations, consultez [Connecter un bot aux canaux](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true).

## <a name="publish-your-app-to-the-teams-store"></a>Publier votre application dans le Teams Store

Mettez votre application à la disposition de tous. Ce type de distribution nécessite l’approbation de Microsoft.

Pour plus d’informations, consultez [publier dans le magasin Teams](~/concepts/deploy-and-publish/appsource/publish.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Configurer les options d’installation par défaut de l’application](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>Voir aussi

[Programme de conformité d’Application Microsoft 365](/microsoft-365-app-certification/overview)
