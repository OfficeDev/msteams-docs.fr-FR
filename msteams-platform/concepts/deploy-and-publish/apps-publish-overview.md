---
title: 'Vue d’ensemble : distribuer votre application'
description: Décrit les options de publication de votre application Microsoft Teams, de téléchargement de votre application et de Cloud de la communauté du secteur public.
ms.topic: conceptual
author: v-rpatkur
ms.author: surbhigupta
ms.localizationpriority: none
keywords: déployer le chargement de l’application de publication gcc
ms.openlocfilehash: 567abdb058f3618236840c993a0ab1a4d638c016
ms.sourcegitcommit: 660273bc6833ab84ba7550e6b374ea6e3780459d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2021
ms.locfileid: "61233497"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribuer votre application Microsoft Teams de messagerie

Vous pouvez fournir votre application Microsoft Teams à une personne, une équipe, une organisation ou toute autre personne qui souhaite l’utiliser. La distribution dépend de plusieurs facteurs, notamment les besoins des utilisateurs, les besoins professionnels, les exigences techniques et vos objectifs pour l’application.

## <a name="configure-default-install-options"></a>Configurer les options d’installation par défaut

Vous configurez les options d’installation par défaut. Par exemple, si la fonctionnalité principale de votre application est un bot, vous pouvez également faire du bot la fonctionnalité par défaut lorsqu’un utilisateur installe votre application dans une équipe.

## <a name="create-your-app-package"></a>Créer votre package d’application

Pour distribuer votre application Microsoft Teams, vous devez avoir un package d’application valide.  Un package d’application est un fichier zip qui contient un manifeste **d’application et** des **icônes d’application.**

## <a name="upload-your-app-in-teams"></a>Télécharger votre application dans Teams

Chargez une application pour une utilisation personnelle, collaborez avec votre équipe ou testez et déboguer. Ce type de distribution ne nécessite pas de processus de révision formel.

> [!IMPORTANT]
> Pour l’instant, les applications de chargement de version Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), mais ne sont pas disponibles pour GCC-High et le Département de la Défense (DOD).

Pour plus d’informations, [voir charger votre application dans Teams](apps-upload.md).

## <a name="publish-your-app-to-your-org"></a>Publier votre application dans votre organisation

Rendez votre application disponible pour les personnes de votre organisation. Ce type de distribution nécessite l’Teams’administrateur.

Pour plus d’informations, [voir gérer vos applications dans le centre Teams’administration.](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json)

### <a name="government-community-cloud-gcc-organizations"></a>Cloud de la communauté du secteur public organisations (Cloud de la communauté du secteur public)

Dans Cloud de la communauté du secteur public Teams environnements, les applications Microsoft compatibles sont activées par défaut. Toutefois, avant de publier une application, assurez-vous que tous les points de terminaison de l’application sont conformes aux Cloud de la communauté du secteur public de votre organisation.

> [!IMPORTANT]
>Si votre application comprend un bot ou une extension de messagerie, vous devez sélectionner l’option **Microsoft Teams** pour le gouvernement lors de la configuration d’un canal entre votre bot et Teams dans Azure. Pour plus d’informations, voir [connecter un bot à des canaux.](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true)

## <a name="publish-your-app-to-the-teams-store"></a>Publier votre application dans le Teams store

Rendez votre application accessible à tous. Ce type de distribution nécessite l’approbation de Microsoft.

Pour plus d’informations, [voir publier sur le Teams store.](~/concepts/deploy-and-publish/appsource/publish.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Configurer les options d’installation par défaut de l’application](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>Voir aussi

[Programme de conformité d’Application Microsoft 365](/microsoft-365-app-certification/overview)
