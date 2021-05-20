---
title: Authentification unique avec Teams Shared Computer Toolkit et Visual Studio Code pour onglets
description: Créez un onglet qui prend en charge les appels à guichet unique et Microsoft Graph directement dans Visual Studio Code avec le Microsoft Teams Shared Computer Toolkit
keywords: équipes visual studio code toolkit onglets sso graph authentification Azure plate-forme d’identité
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 11e642ce335dae4344f1c730b73763e9172fd76c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566830"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Authentification unique avec Teams Shared Computer Toolkit et Visual Studio Code pour onglets

Le Microsoft Teams Shared Computer Toolkit vous permet de créer une authentification unique de connect-on (SSO) pour les applications d’onglets directement dans Visual Studio Code. La boîte à outils vous guide tout au long du processus et fournit tout ce dont vous avez besoin, y compris la fourniture Plateforme d’identités Microsoft’inscription sur le portail Azure.

## <a name="get-started--create-a-project"></a>Démarrer — créer un projet

1. Créez un nouveau projet dans la boîte à outils.
1. Sélectionnez l’onglet comme type d’extension que vous souhaitez créer.
1. Sélectionnez l’option pour prendre en charge SSO.

> [!TIP]
> Après l’installation, vous devriez voir les Teams Shared Computer Toolkit la barre d Visual Studio Code’activité. Si ce n’est pas le cas, cliquez à droite dans la barre **d’activité et sélectionnez Microsoft Teams** épingler la boîte à outils pour un accès facile.

## <a name="configure-your-project"></a>Configurez votre projet

1. Pour activer SSO dans Teams, votre application doit avoir une ressource d’enregistrement d’application Azure. Le Teams Shared Computer Toolkit l’inscription de l’application en votre nom.
1. Entrez l’URL où votre application sera hébergée et sélectionnez **ensuite**. L’enregistrement de votre application sera configuré à l’aide de l’URL fournie.
1. Les détails de configuration de l’enregistrement de l’application seront `.env` stockés dans les fichiers dans le code source de votre projet.

Si vous souhaitez en savoir plus sur la façon dont l’enregistrement de votre application Azure sera provisionné, veuillez _consulter_ notre [support de connect-on unique (SSO) pour la documentation des onglets.](../tabs/how-to/authentication/auth-aad-sso.md)

> [!TIP]
> Vous devrez vous rendre aux **enregistrements d’applications Azure et** mettre à jour *votre API URI et* *rediriger les URL chaque fois* que vous modifiez cette URL.

## <a name="run-your-project"></a>Exécutez votre projet

1. Sélectionnez **npm installer** à partir du `api-server` dossier. Puis **npm commencer**.
1. Sélectionnez **npm installer** à partir du `.src` dossier. Puis **npm commencer**.
1. Si vous utilisez un service de tunnelage comme [ngrok, exécutez-le](https://ngrok.com/)et assurez-vous que l’URL correspond à ce que vous avez entré dans l’assistant de création de projet. Si ce n’est pas le cas, vous devrez mettre à jour _votre API URI et_ _rediriger l’URL_ dans l’enregistrement de l’application créée dans Azure.
1. Accédez à la barre d’activité sur le côté gauche de la Visual Studio Code fenêtre.
1. Sélectionnez **l’icône** Exécuter pour afficher **la vue Exécuter et Debug.**
1. Vous pouvez également utiliser le raccourci clavier **Ctrl+Shift+D**.

> [!TIP]
> Il se peut que vous ne voyiez pas l’application installer le dialogue dans le navigateur si les fenêtres contextées sont désactivées pour votre navigateur. Si cela se produit, activez les fenêtres contexturées et actualisez la page.

## <a name="see-also"></a>Voir aussi

- [Créez des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code](visual-studio-code-overview.md)
