---
title: Authentification unique avec authentification Teams Shared Computer Toolkit et Visual Studio Code pour les onglets
description: Créez un onglet qui prend en charge l' sign-on unique et les appels Microsoft Graph directement dans Visual Studio Code avec le Microsoft Teams Shared Computer Toolkit
keywords: teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 2ef409a45b92240cced09d2d77793af33945589e
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721814"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Authentification unique avec authentification Teams Shared Computer Toolkit et Visual Studio Code pour les onglets

> [!IMPORTANT]
> **Ce document fait référence à une ancienne version de Teams Shared Computer Toolkit**
>
> Pour plus d’informations, lisez [les conditions préalables](../get-started/prerequisites.md) et suivez l’un des didacticiels les plus nouveaux.

Le Microsoft Teams Shared Computer Toolkit vous permet de créer l’authentification unique (SSO) pour les applications onglet directement dans Visual Studio Code. Le kit de ressources vous guide tout au long du processus et fournit tout ce dont vous avez besoin, y compris la mise en service de votre Plateforme d’identités Microsoft inscription dans le portail Azure.

## <a name="get-started--create-a-project"></a>Commencer : créer un projet

1. Créez un projet dans le kit de ressources.
1. Sélectionnez l’onglet comme type d’extension que vous souhaitez créer.
1. Sélectionnez l’option de prise en charge de l' sso.

> [!TIP]
> Après l’installation, vous devez voir le Teams Shared Computer Toolkit dans la barre d Visual Studio Code’activité. Si ce n’est pas le cas, cliquez avec le bouton droit dans la barre **d’activité** et sélectionnez Microsoft Teams pour épingler le kit de ressources pour un accès facile.

## <a name="configure-your-project"></a>Configurer votre projet

1. Pour activer l' utilisateur Teams, votre application doit avoir une ressource d’inscription d’application Azure. L Teams Shared Computer Toolkit approvisionnement de l’inscription de l’application en votre nom.
1. Entrez l’URL où votre application sera hébergée et sélectionnez **ensuite.** L’inscription de votre application sera configurée à l’aide de l’URL fournie.
1. Les détails de configuration de l’inscription de l’application sont stockés dans les fichiers du `.env` code source de votre projet.

Si vous souhaitez en savoir plus sur la façon  dont l’inscription de votre application Azure sera mise en service, consultez notre prise en charge de l' [sign-on unique (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) pour la documentation sur les onglets.

> [!TIP]
> Vous devrez accéder à **Azure App Registrations** et  mettre à jour votre *URI d’API* et rediriger les URL chaque fois que vous modifiez cette URL.

## <a name="run-your-project"></a>Exécuter votre projet

1. Sélectionnez **l’installation npm** dans le `api-server` dossier. Puis **npm start**.
1. Sélectionnez **l’installation npm** dans le `.src` dossier. Puis **npm start**.
1. Si vous utilisez un service de tunneling comme [ngrok,](https://ngrok.com/)exécutez-le et assurez-vous que l’URL correspond à ce que vous avez entré dans l’Assistant de création de projet. Si ce n’est pas le cas, vous devrez mettre à jour votre _URI d’API_ et _rediriger l’URL_ dans l’inscription de l’application qui a été créée dans Azure.
1. Accédez à la barre d’activité sur le côté gauche de Visual Studio Code fenêtre.
1. Sélectionnez **l’icône** Exécuter pour afficher **l’affichage Exécuter et déboguer.**
1. Vous pouvez également utiliser le raccourci clavier **Ctrl+Shift+D**.

> [!TIP]
> Vous ne verrez peut-être pas le dialogue d’installation de l’application dans le navigateur si les fenêtres pop-up sont désactivées pour votre navigateur. Si cela se produit, activez les fenêtres pop-up et actualisez la page.

## <a name="see-also"></a>Voir aussi

[Créer des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code](visual-studio-code-overview.md)
