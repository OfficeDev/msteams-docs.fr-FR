---
title: Authentification par authentification unique avec Teams Toolkit et Visual Studio Code pour les onglets
description: Créez un onglet qui prend en charge l’authentification unique et les appels Microsoft Graph directement dans Visual Studio Code avec le kit de ressources Microsoft Teams.
keywords: teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 7cca78c2ca3669d647dd76dd71e0a2b999b09dd1
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123870"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Authentification par authentification unique avec Teams Toolkit et Visual Studio Code pour les onglets

> [!IMPORTANT]
> **Ce document fait référence à une ancienne version de Teams Toolkit**
>
> Pour plus d’informations, lisez les [prérequis](../get-started/prerequisites.md) et suivez l’un des didacticiels les plus nouveaux.

Le kit de ressources Microsoft Teams vous permet de créer une authentification unique (SSO) pour les applications onglet directement dans Visual Studio Code. Le kit de ressources vous guide tout au long du processus et fournit tout ce dont vous avez besoin, y compris l’approvisionnement de votre inscription Plateforme d'identités Microsoft dans le portail Microsoft Azure.

## <a name="get-started--create-a-project"></a>Démarrage : créer un projet

1. Créez un projet dans le kit de ressources.
1. Sélectionnez tab comme type d’extension que vous souhaitez créer.
1. Sélectionnez l’option pour prendre en charge l’authentification unique.

> [!TIP]
> Après l’installation, vous devez voir le kit de ressources Teams dans la barre d’activité Visual Studio Code. Si ce n’est pas le cas, cliquez avec le bouton droit dans la barre d’activité et sélectionnez **Microsoft Teams** pour épingler le kit de ressources pour faciliter l’accès.

## <a name="configure-your-project"></a>Configurer votre projet

1. Pour activer l’authentification unique dans Teams, votre application doit disposer d’une ressource d’inscription d’application Azure. Le kit de ressources Teams provisionne l’inscription de l’application en votre nom.
1. Entrez l’URL dans laquelle votre application sera hébergée, puis sélectionnez **la suivante**. L’inscription de votre application sera configurée à l’aide de l’URL fournie.
1. Les détails de configuration de l’inscription de l’application sont stockés dans les `.env` fichiers du code source de votre projet.

Si vous souhaitez en savoir plus sur le provisionnement de votre inscription d’application Azure, *consultez*  notre documentation sur la prise en charge de l’authentification [unique (SSO) pour les onglets](../tabs/how-to/authentication/tab-sso-overview.md) .

> [!TIP]
> Vous devez accéder à **Azure App Inscriptions** et mettre à jour votre *URI d’API* et *rediriger les URL* chaque fois que vous modifiez cette URL.

## <a name="run-your-project"></a>Exécuter votre projet

1. Sélectionnez **npm installer** à partir du `api-server` dossier. Puis **npm démarrer**.
1. Sélectionnez **npm installer** à partir du `.src` dossier. Puis **npm démarrer**.
1. Si vous utilisez un service de tunneling comme [ngrok](https://ngrok.com/), exécutez-le et vérifiez que l’URL correspond à ce que vous avez entré dans l’Assistant création de projet. Si ce n’est pas le cas, vous devez mettre à jour votre *URI d’API* et *l’URL de redirection* dans l’inscription d’application qui a été créée dans Azure.
1. Accédez à la barre d’activité sur le côté gauche de la fenêtre code Visual Studio.
1. Sélectionnez l’icône **Exécuter** pour afficher la vue **Exécuter et déboguer** .
1. Vous pouvez également utiliser le raccourci clavier **Ctrl+Maj+D**.

> [!TIP]
> La boîte de dialogue d’installation de l’application peut ne pas s’afficher dans le navigateur si les fenêtres contextuelles sont désactivées pour votre navigateur. Si cela se produit, activez les fenêtres contextuelles et actualisez la page.

## <a name="see-also"></a>Voir aussi

[Créez des applications avec la boîte à outils Microsoft Teams et Visual Studio Code](visual-studio-code-overview.md)
