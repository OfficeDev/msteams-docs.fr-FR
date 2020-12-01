---
title: Authentification unique avec Team Toolkit et Visual Studio code pour les onglets
description: Créer un onglet qui prend en charge les appels d’authentification unique et Microsoft Graph directement dans Visual Studio code avec Microsoft teams Toolkit
keywords: Visual Studio code Toolkit (onglets de la boîte à outils d’authentification par graphique SSO)
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477733"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Authentification unique avec Team Toolkit et Visual Studio code pour les onglets

Le kit de développement Microsoft teams vous permet de créer une authentification unique (SSO) pour les applications d’onglet directement dans Visual Studio code. Le kit de connaissances vous guide tout au long du processus et vous fournit tout ce dont vous avez besoin, notamment la mise en service de votre enregistrement de plateforme d’identité Microsoft dans le portail Azure.

## <a name="get-started--create-a-project"></a>Prise en main : créer un projet

1. Créez un projet dans la boîte à outils.
1. Sélectionnez l’onglet comme type d’extension que vous souhaitez créer.
1. Sélectionnez l’option permettant de prendre en charge l’authentification unique.

> [!TIP]
> Après l’installation, vous devriez voir la boîte à outils teams dans la barre d’activité code Visual Studio. Si ce n’est pas le cas, cliquez avec le bouton droit de la barre d’activité et sélectionnez **Microsoft teams** pour épingler la boîte à outils pour un accès facile.

## <a name="configure-your-project"></a>Configurer votre projet

1. Pour activer l’authentification unique (SSO) dans Teams, votre application doit disposer d’une ressource d’inscription Azure App. La boîte à outils teams configurera l’inscription de l’application en votre nom.
1. Entrez l’URL où votre application sera hébergée et cliquez sur **suivant**. L’inscription de votre application sera configurée à l’aide de l’URL fournie.
1. Les détails de configuration de l’enregistrement de l’application seront stockés dans les `.env` fichiers dans le code source de votre projet.

Si vous souhaitez en savoir plus sur le mode d’inscription de votre application Azure, _reportez-vous_  à notre [prise en charge de l’authentification unique (SSO) pour les onglets](../tabs/how-to/authentication/auth-aad-sso.md) documentation.

> [!TIP]
> Vous devrez accéder aux **inscriptions d’applications Azure** et mettre à jour votre *URI d’API* et *Rediriger les URL* chaque fois que vous modifiez cette URL.

## <a name="run-your-project"></a>Exécuter votre projet

1. Sélectionnez **NPM installer** dans le `api-server` dossier. Ensuite **NPM Start**.
1. Sélectionnez **NPM installer** dans le `.src` dossier. Ensuite **NPM Start**.
1. Si vous utilisez un service de tunneling comme [ngrok](https://ngrok.com/), exécutez-le et assurez-vous que l’URL correspond à ce que vous avez entré dans l’Assistant Création de projet. Si ce n’est pas le cas, vous devez mettre à jour l’URI de votre _API_ et l' _URL de redirection_ dans l’inscription de l’application qui a été créée dans Azure.
1. Accédez à la barre d’activité sur le côté gauche de la fenêtre de code Visual Studio.
1. Sélectionnez l’icône **exécuter** pour afficher l’affichage **exécuter et déboguer** .
1. Vous pouvez également utiliser le raccourci clavier **Ctrl + Maj + D**.

> [!TIP]
> Il se peut que la boîte de dialogue d’installation de l’application ne s’affiche pas dans le navigateur si les fenêtres contextuelles sont désactivées pour votre navigateur. Dans ce cas, activez les fenêtres contextuelles et actualisez la page.

> [!div class="nextstepaction"]
> [En savoir plus : créer des applications avec Microsoft teams Toolkit et Visual Studio code](visual-studio-code-overview.md)
