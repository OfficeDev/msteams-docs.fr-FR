---
title: Configurez votre environnement de développement pour étendre les applications Teams sur Microsoft 365
description: Conditions requises pour configurer votre environnement de développement pour étendre les applications Teams dans Microsoft 365. Connaître les configurations requises pour exécuter les builds des applications Microsoft Teams et Microsoft Office.
ms.date: 05/24/2022
ms.custom: m365apps
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 99050d8b8db4fac38e9d36c42a6c3efe7f1bf28d
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789911"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Configurez votre environnement de développement pour étendre les applications Teams sur Microsoft 365

L’environnement de développement pour étendre des applications Teams sur Microsoft 365 est similaire au développement Microsoft Teams. Cet article décrit les configurations spécifiques requises pour exécuter des versions d’évaluation de Microsoft Teams et des applications Microsoft Office afin d’afficher un aperçu des applications Teams s’exécutant dans Outlook et Office.

Pour la configuration de votre environnement de développement :

> [!div class="checklist"]
>
> * [Obtenir Microsoft 365 Développeur (Sandbox) et activer le chargement indépendant](#prepare-a-developer-tenant-for-testing)
> * [inscrire votre client Microsoft 365 dans *des versions ciblées d’Office 365*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Installer Canal bêta builds d’applications Microsoft 365 dans votre environnement de test](#install-office-apps-in-your-test-environment)
> * [basculer vers la préversion développeur de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*facultatif*] [installer l’extension Teams Toolkit pour Microsoft Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Préparer un locataire de développeur pour le test

Vous avez besoin d’un locataire de bac à sable Microsoft 365 abonnement développeur pour configurer votre environnement de développement. Si vous n’en avez pas encore, créez [un locataire de bac à sable](/office/developer-program/microsoft-365-developer-program-get-started) ou obtenez un locataire de test au sein de votre organisation.

Vous devez également activer le chargement indépendant pour votre locataire :

 1. Connectez-vous au [Centre d’administration Teams](https://admin.teams.microsoft.com/dashboard) avec vos informations d’identification de locataire de test.

 1. Accédez à **Applications Teams** > **Gérer les applications**.

 1. En haut à droite, sélectionnez **Paramètres de l’application à l’échelle de l’organisation**.

 1. Sous Applications personnalisées, activez le bouton bascule **Interaction avec l’application personnalisée** et **Enregistrer**.

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="La capture d’écran est un exemple qui active le chargement indépendant pour les applications personnalisées à partir du Centre Administration Teams":::

 1. Outre les paramètres d’application à l’échelle de l’organisation, les paramètres de stratégie d’application personnalisée permettent également aux utilisateurs de charger des applications personnalisées dans Teams. Pour plus d’informations, consultez [Gérer les stratégies et les paramètres d’application personnalisés](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).

 1. Dans le Centre d’administration Teams, accédez à Stratégies **d’installation des** **applications** >  Teams, puis sélectionnez **Stratégie globale (par défaut à l’échelle de l’organisation).**

 1. Activez **Charger des applications personnalisées**, puis sélectionnez **Enregistrer**.

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscrire votre locataire de développeur pour les versions ciblées d’Office 365

> [!IMPORTANT]
> Il peut s'écouler jusqu'à cinq jours après la création d'un client [Microsoft 365 developer sandbox](/office/developer-program/microsoft-365-developer-program-get-started) et l'inscription aux [versions ciblées d'Office 365](#enroll-your-developer-tenant-for-office-365-targeted-releases) pour que les applications Teams chargées en version test apparaissent dans Outlook et Office.

Pour inscrire votre locataire de test aux versions ciblées d’Office 365 :

1. Connectez-vous à [Centre d’administration Microsoft 365](https://admin.microsoft.com) avec vos informations d’identification de locataire de test.
1. Accédez à **Paramètres** > **Paramètres de l’organisation** > **profil d’organisation**.
1. Sélectionnez **préférences de publication**.
1. Sélectionnez une préférence de *diffusion ciblée* :
    1. **version cible pour tout le monde**
    1. **version cible pour certains utilisateurs**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="La capture d’écran est un exemple montrant l’Centre d'administration Microsoft 365 menu « Préférences de mise en production » avec l’option Publication ciblée sélectionnée.":::

1. Sélectionnez **Enregistrer**.

Pour plus d’informations sur Office 365 options de publication, consultez [Configurer les options de publication standard ou ciblée](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) dans *Centre d'administration Microsoft 365 aide*.

## <a name="install-office-apps-in-your-test-environment"></a>Installer des applications Office dans votre environnement de test

### <a name="desktop"></a>Ordinateur de bureau

Vous pouvez afficher un aperçu des applications Teams s’exécutant dans Outlook sur le bureau Windows à l’aide d’une build *Canal bêta récente*. Vérifiez si vous devez [modifier le canal de mise à jour Microsoft 365 Apps](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) pour votre locataire de test afin d’installer une build de canal bêta Office 365.

Pour installer des applications Office 365 Canal bêta dans votre environnement de test :

1. Connectez-vous à votre environnement de test avec vos informations d’identification de locataire de test.
1. Téléchargez [l’outil déploiement d’Office](https://www.microsoft.com/download/details.aspx?id=49117) et extrayez-le dans un dossier local.
1. Accédez au dossier local et ouvrez *configuration-Office365-x86.xml* (ou **x64.xml*, en fonction de votre environnement) dans un éditeur de texte et mettez à jour la valeur *canal* sur `BetaChannel`.
1. Ouvrez l’invite de commandes et accédez au chemin du dossier local.
1. Exécutez `setup.exe /configure configuration-Office365-x86.xml` (ou utilisez le fichier *de x64.xml **, selon votre configuration).
1. Ouvrez Outlook (client de bureau) et configurez le compte de messagerie à l’aide de vos informations d’identification de locataire de test.
1. Ouvrez **Fichier** > **Compte Office** > **À propos d’Outlook** pour confirmer que vous exécutez un build de *canal bêta* Microsoft 365 de Outlook.

    :::image type="content" source="images/outlook-about-beta-channel.png" alt-text="La capture d’écran est un exemple qui montre à propos d’Outlook pour vérifier que vous exécutez une build de canal bêta.":::

1. Vérifiez que *Microsoft Edge WebView2 Runtime* est installé. Ouvrez Windows **Démarrage** > **Applications et fonctionnalités**, puis recherchez **webview** :

    :::image type="content" source="images/windows-addremove-webview2.png" alt-text="La capture d’écran est un exemple qui montre le champ de recherche dans vos paramètres Windows.":::

    S’il n’est pas répertorié, installez [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) dans votre environnement de test.

### <a name="mobile"></a>Mobile

Vous pouvez afficher un aperçu des onglets personnels Teams en cours d’exécution dans l’application Office pour Android en rejoignant le programme bêta.

Pour installer la dernière version bêta de l’application Office, générez sur votre appareil Android physique ou votre émulateur Android :

1. Veillez à utiliser un [appareil Android pris en charge par](https://support.google.com/googleplay/answer/1727131) Google Play.
1. Lancez le **Play Store** sur votre appareil Android.
1. Recherchez office et sélectionnez **Microsoft Office : Modifier & Partager**.
1. Sélectionnez le bouton **Installer** .

    :::image type="content" source="images/office-android-install.png" alt-text="La capture d’écran est un exemple montrant le bouton d’installation de Microsoft Office : Modifier &'application Partager dans Google Play Store.":::

1. Sélectionnez **Rejoindre** sous **Rejoindre la section bêta** une fois l’installation terminée.

    :::image type="content" source="images/office-android-join-beta.png" alt-text="La capture d’écran est un exemple montrant l’écran Rejoindre la version bêta.":::

1. Lancez l’application Office et connectez-vous avec vos informations d’identification de locataire de test.
1. Ouvrez votre profil **(Moi) > Paramètres** et faites défiler jusqu’au bas du menu.
2. Veillez à utiliser l’application Office version 16.0.15726.20000 ou ultérieure pour Android.

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Basculer vers la préversion développeur de Teams

Veillez à passer à la [Public Developer Preview](../resources/dev-preview/developer-preview-intro.md) à partir de votre client Microsoft Teams.

1. Connectez-vous à Teams avec vos informations d’identification de locataire de bac à sable.
1. Dans le menu des points de suspension (**...**) en regard de votre profil utilisateur, sélectionnez **À propos de** > **d’aperçu développeur**. Une boîte de dialogue s’affiche, sélectionnez **Basculer vers la préversion du développeur**.
1. Après le redémarrage de l’application Teams, accédez au menu points de suspension (**...**) en regard de votre profil utilisateur et vérifiez si **Developer Preview** est sélectionné.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="La capture d’écran est un exemple montrant l’option de préversion publique pour les développeurs dans Teams.":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>Installer Visual Studio Code et l’extension Teams Toolkit

Si vous le souhaitez, vous pouvez utiliser [Visual Studio Code](https://code.visualstudio.com/) pour étendre les applications Teams à Office et Outlook.

The extension [Teams Toolkit for Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0` or later) provides commands that can help modify your existing Teams code to be compatible with Outlook and Office. For more information, see [enable Teams personal tab for Office and Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-step"></a>Étape suivante

Créez ou mettez à jour une application Teams pour qu’elle s’exécute sur Microsoft 365 :

> [!div class="nextstepaction"]
> [Activer un onglet personnel Teams pour Office et Outlook](extend-m365-teams-personal-tab.md)
> [!div class="nextstepaction"]
> [activer une extension de message Teams pour Outlook](extend-m365-teams-message-extension.md)
