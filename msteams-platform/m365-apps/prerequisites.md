---
title: Configurez votre environnement de développement pour étendre les applications Teams sur Microsoft 365
description: Voici les conditions préalables à l’extension de vos applications Teams dans Microsoft 365
ms.date: 05/24/2022
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 6e4376d01a398400a7aaefbe1fee14f5547ff372
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2022
ms.locfileid: "65654733"
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

Vous devez également activer le chargement indépendant pour votre client :

1. Connectez-vous à Centre d’administration Microsoft 365 (https://admin.microsoft.com) avec vos informations d’identification client de test et sélectionnez **Teams** dans le volet latéral pour ouvrir le *Centre d’administration Microsoft Teams*
1. Sélectionnez : Applications Teams > Gérer les applications > **paramètres d’application à l’échelle de l’organisation**
1. Sous **Applications personnalisées**, activez l’option *Interaction avec les applications personnalisées*

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="Activer le chargement indépendant pour les applications personnalisées à partir du Centre d’administration Teams":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscrire votre locataire de développeur pour les versions ciblées d’Office 365

> [!Important]
> Il peut s'écouler jusqu'à cinq jours après la création d'un client [Microsoft 365 developer sandbox](/office/developer-program/microsoft-365-developer-program-get-started) et l'inscription aux [versions ciblées d'Office 365](#enroll-your-developer-tenant-for-office-365-targeted-releases) pour que les applications Teams chargées en version test apparaissent dans Outlook et Office.

Pour inscrire votre locataire de test aux versions ciblées d’Office 365 :

1. Connectez-vous à [Centre d’administration Microsoft 365](https://admin.microsoft.com) avec vos informations d’identification de locataire de test.
1. Accédez à **Paramètres** > **Paramètres de l’organisation** > **profil d’organisation**.
1. Sélectionnez **préférences de publication**.
1. Sélectionnez une préférence de *diffusion ciblée* :
    1. **version cible pour tout le monde**
    1. **version cible pour certains utilisateurs**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Centre d’administration Microsoft 365 menu « Préférences de mise en production » avec l’option de mise en production ciblée sélectionnée":::

1. Sélectionnez **Enregistrer**.

Pour plus d’informations sur les options de publication d’Office 365, consultez [Configurer les options de publication standard ou ciblée](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) dans *Centre d’administration Microsoft 365 aide*.

## <a name="install-office-apps-in-your-test-environment"></a>Installer des applications Office dans votre environnement de test

Vous pouvez afficher un aperçu des applications Teams s’exécutant dans Outlook sur le bureau Windows à l’aide d’une build *Canal bêta récente*. Vérifiez si vous devez [modifier le canal de mise à jour Microsoft 365 Apps](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) pour que votre client de test installe une build Office 365 Canal bêta.

Pour installer des applications Office 365 Canal bêta dans votre environnement de test :

1. Connectez-vous à votre environnement de test avec vos informations d’identification de locataire de test.
1. Téléchargez [l’outil déploiement d’Office](https://www.microsoft.com/download/details.aspx?id=49117) et extrayez-le dans un dossier local.
1. Accédez au dossier local et ouvrez *configuration-Office365-x86.xml* (ou **x64.xml*, en fonction de votre environnement) dans un éditeur de texte et mettez à jour la valeur *canal* sur `BetaChannel`.
1. Ouvrez l’invite de commandes et accédez au chemin d’accès au dossier local.
1. Exécutez `setup.exe /configure configuration-Office365-x86.xml` (ou utilisez le fichier *de x64.xml **, selon votre configuration).
1. Ouvrez Outlook (client de bureau) et configurez le compte de messagerie à l’aide de vos informations d’identification de locataire de test.
1. Ouvrez **Fichier** > **Compte Office** > **À propos d’Outlook** pour confirmer que vous exécutez un build de *canal bêta* Microsoft 365 de Outlook.

    :::image type="content" source="images/outlook-about-beta-channel.png" alt-text="Accédez à « À propos d’Outlook » à partir de votre compte Office pour vérifier que vous exécutez une build Canal bêta.":::

1. Vérifiez que *Microsoft Edge WebView2 Runtime* est installé. Ouvrez Windows **Démarrer** > **Applications et fonctionnalités** et recherchez « webview » :

    :::image type="content" source="images/windows-addremove-webview2.png" alt-text="Recherchez « webview » sous « Applications et fonctionnalités » dans vos paramètres Windows":::

    S’il n’est pas répertorié, installez [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) dans votre environnement de test.

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Basculer vers la préversion développeur de Teams

Veillez à passer à la [Public Developer Preview](../resources/dev-preview/developer-preview-intro.md) à partir de votre client Microsoft Teams.

1. Connectez-vous à Teams avec vos informations d’identification de locataire de bac à sable.
1. Dans le menu des points de suspension (**...**) en regard de votre profil utilisateur, sélectionnez **À propos de** > **d’aperçu développeur**. Une boîte de dialogue s’affiche, sélectionnez **Basculer vers la préversion du développeur**.
1. Après le redémarrage de l’application Teams, accédez au menu points de suspension (**...**) en regard de votre profil utilisateur et vérifiez si **Developer Preview** est sélectionné.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Option de préversion publique pour les développeurs dans Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>Installer Visual Studio Code et l’extension Teams Toolkit

Si vous le souhaitez, vous pouvez utiliser [Visual Studio Code](https://code.visualstudio.com/) pour étendre les applications Teams à Office et Outlook.

L'extension [Teams Toolkit for Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`ou ultérieure) fournit des commandes qui peuvent aider à modifier votre code Teams existant pour qu'il soit compatible avec Outlook et Office. Pour plus d'informations, voir [activer l'onglet personnel Teams pour Office et Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Étapes suivantes

Créez ou mettez à jour une application Teams pour qu’elle s’exécute sur Microsoft 365 :

* [Activer un onglet personnel Teams pour Office et Outlook](extend-m365-teams-personal-tab.md)
* [activer une extension de message Teams pour Outlook](extend-m365-teams-message-extension.md)
