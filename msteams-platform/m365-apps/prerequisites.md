---
title: Configurer votre environnement dev pour l’extension Teams applications à travers Microsoft 365
description: Voici les conditions préalables à l’extension de vos applications Teams à travers Microsoft 365
ms.date: 02/11/2022
ms.openlocfilehash: eec44e149e81b420c507b0580896d2c5a4a99cc2
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355999"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Configurer votre environnement dev pour l’extension Teams applications à travers Microsoft 365

> [!NOTE]
> Étendre l’application Teams Microsoft 365 est actuellement disponible uniquement en [prévisualisation pour les développeurs publics](~/resources/dev-preview/developer-preview-intro.md).

L’environnement de développement pour l’extension Teams applications à travers Microsoft 365 est similaire à celui Microsoft Teams développement. Cet article décrit les configurations spécifiques requises pour exécuter des builds d’aperçu des applications Microsoft Teams et Microsoft Office afin de prévisualiser les applications Teams s’exécutant dans Outlook et Office.

Pour la configuration de votre environnement de développement :

> [!div class="checklist"]
> * [Obtenir Microsoft 365 développeur (bac à sable) et activer le chargement indépendant](#prepare-a-developer-tenant-for-testing)
> * [Inscrire votre client Microsoft 365 client dans *les Office 365 de publication ciblées*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Configurer votre compte pour accéder aux versions d’aperçu Outlook et Office](#install-office-apps-in-your-test-environment)
> * [Basculer vers la version d’aperçu du développeur de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Facultatif*] [Installer Teams Shared Computer Toolkit extension de Microsoft Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Préparer un client développeur pour le test

Vous avez besoin d’Microsoft 365 client bac à sable (sandbox) d’abonnement développeur pour configurer votre environnement de développement. Si vous n’en avez pas encore, créez un client [bac](/office/developer-program/microsoft-365-developer-program-get-started) à sable ou obtenez un client de test par le biais de votre organisation.

Une fois que vous avez un client, vous devez activer le chargement de version sideload pour votre client, voir [activer le chargement de version.](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading) Pour vérifier si le chargement de version de version est activé, connectez-vous à Teams, sélectionnez **Applications**, puis recherchez Télécharger **une option d’application** personnalisée.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Télécharger une option d’application personnalisée":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscrire votre client développeur pour les Office 365 de publication ciblées

> [!IMPORTANT]
> Reportez-vous aux dernières mises à jour du [blog Microsoft Teams - Microsoft 365 Developer](https://devblogs.microsoft.com/microsoft365dev/) pour vérifier si la prise en charge de Outlook.com et Office.com pour les applications Teams est disponible pour votre client test.

Pour inscrire votre client test pour les Office 365 de publication ciblées :

1. Connectez-vous [Centre d'administration Microsoft 365](https://admin.microsoft.com) avec vos informations d’identification client de test.
1. Go to **Paramètres** >  **Org Paramètres** >  **Organization profile**.
1. **Sélectionnez Préférences de publication**.
1. Sélectionnez les *préférences de publication ciblée* :
    1. **Publication cible pour tout le monde**
    1. **Publication cible pour les utilisateurs sélectionnés**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Centre d'administration Microsoft 365 menu « Préférences de publication » avec l’option de publication ciblée sélectionnée":::
    
1. Sélectionnez **Enregistrer**.

Pour plus d’informations Office 365 options de publication, voir [Configurer les options](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) de publication standard ou ciblée *dans Centre d'administration Microsoft 365'aide*.

## <a name="install-office-apps-in-your-test-environment"></a>Installer Office applications dans votre environnement de test

> [!IMPORTANT]
> Reportez-vous aux dernières mises à jour du [blog du développeur Microsoft Teams - Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/) pour vérifier si Outlook pour la prise en charge du bureau Windows pour les extensions de messagerie Teams est disponible pour votre client test.

Vous pouvez prévisualiser Teams applications s’exécutant dans Outlook sur Windows bureau à l’aide d’une *version récente du canal bêta*. Vérifiez si vous devez modifier le canal Microsoft 365 Apps [de](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) mise à jour pour votre client test afin d’installer Office 365 version bêta du canal.

Pour installer Office 365 applications de canal bêta dans votre environnement de test :

1. Connectez-vous à votre environnement de test avec vos informations d’identification client de test.
1. Téléchargez l [Office de déploiement et](https://www.microsoft.com/download/details.aspx?id=49117) extrayez-le dans un dossier local.
1. Go to the local folder and open *configuration-Office365-x86.xml* (or **x64.xml*, depending on your environment) in a text editor and update the *Channel* value to `BetaChannel`.
1. Ouvrez l’invite de commandes et accédez au chemin d’accès au dossier local.
1. Exécutez `setup.exe /configure configuration-Office365-x86.xml` (ou utilisez le *fichier *x64.xml* , en fonction de votre configuration).
1. Ouvrez Outlook (client de bureau) et définissez le compte de messagerie à l’aide de vos informations d’identification client de test.
1. **Ouvrez la** >  **Office** **AccountAbout** >  Outlook.  
   Si le numéro de build **est 14416** ou supérieur et que le canal est le canal *bêta, vous* exécutez Microsoft 365 version bêta du canal.
1. Dans le coin supérieur droit, activer le **basculement Bientôt** disponible.
    
    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Option bascule « Bientôt disponible » dans Outlook":::

> [!NOTE]
> Vous devrez peut-être fermer Outlook puis redémarrer votre ordinateur *pour que le* bouton Bientôt disponible s’affiche.

Vous pouvez vérifier la prise en charge du client test pour votre compte client :

* Pour Teams onglets personnels en cours d’exécution sur office.com, outlook.com et Outlook pour le bureau Windows, connectez-vous avec vos informations d’identification client de test et vérifiez l’option des ellipses (**...**) sur la barre latérale gauche de Office ou Outlook.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Option Ellipses ('...') sur la barre latérale gauche de Outlook":::

* Pour les extensions de messagerie dans outlook.com et Outlook pour Windows, recherchez **l’option Autres** applications en bas du volet Outlook message de composition.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Option « Autres applications » dans le volet Outlook message de composition":::

> [!NOTE]
> Si vous avez choisi d’opter pour les versions bêta du canal, mais que vous ne voyez pas ces options de sélection, il est probable que la prise en charge des fonctionnalités de prévisualisation soit en cours de déploiement sur votre client. Pour les dernières mises à jour, [voir Microsoft Teams blog du développeur](https://devblogs.microsoft.com/microsoft365dev/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Basculer vers la version d’aperçu du développeur de Teams

Veillez à basculer vers la prévisualisation pour les développeurs [publics](../resources/dev-preview/developer-preview-intro.md) à partir de votre client Microsoft Teams client.

1. Connectez-vous Teams avec vos informations d’identification de client en bac à sable.
1. Dans le menu des ellipses (**...**) en haut de votre profil utilisateur, sélectionnez **Aperçu** **AboutDeveloper** > . Une boîte de dialogue s’affiche, **sélectionnez Basculer vers l’aperçu développeur**.
1. Après le redémarrage Teams’application, sélectionnez le menu des ellipses (**...**) en regard de votre profil utilisateur  et vérifiez si l’aperçu du développeur est sélectionné.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Option de prévisualisation pour les développeurs publics dans Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Installer l Visual Studio Code et l Teams Shared Computer Toolkit de prévisualisation

Si vous le souhaitez, vous pouvez [utiliser Visual Studio Code](https://code.visualstudio.com/) pour étendre Teams applications Office et Outlook.

[L’extension Teams Shared Computer Toolkit pour Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`ou ultérieure) fournit des commandes qui peuvent vous aider à modifier votre code Teams existant pour qu’il soit compatible avec les Outlook et Office. Pour plus d’informations, [voir activer Teams onglet personnel pour Office et Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Étapes suivantes

- [Activer un onglet personnel Teams pour Office et Outlook](extend-m365-teams-personal-tab.md)
- [Activer une extension de messagerie Teams pour Outlook](extend-m365-teams-message-extension.md)
