---
title: Configurer votre environnement dev pour l’extension Teams applications à travers Microsoft 365
description: Voici les conditions préalables à l’extension de vos applications Teams à travers Microsoft 365
ms.date: 11/15/2021
ms.topic: how-to
ms.custom: m365apps
ms.openlocfilehash: 967e45bb59c431476ead902e1413ab743c566779
ms.sourcegitcommit: 239807b74aa222452559509d49c4f2808cd9c9ca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2021
ms.locfileid: "61391345"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-m365-preview"></a>Configurer votre environnement dev pour l’extension Teams applications sur M365 (prévisualisation)

L’environnement de développement pour l’extension Teams applications à travers Microsoft 365 est similaire à ce que vous utilisez pour Microsoft Teams développement. Cet article décrit les configurations spécifiques requises pour exécuter des builds d’aperçu des applications Microsoft Teams et Microsoft Office afin de prévisualiser les applications Teams s’exécutant dans Outlook et Office. Pour configurer votre environnement de développement, vous devez :

> [!div class="checklist"]
> * [Obtenir un client développeur M365 (bac à sable) et activer le chargement indépendant](#prepare-a-developer-tenant-for-testing)
> * [Inscrire votre client M365 dans *des Office 365 ciblées*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Configurer votre compte pour accéder aux versions d’aperçu Outlook et Office](#install-office-apps-in-your-test-environment)
> * [Basculer vers la version d’aperçu du développeur de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Facultatif*] [Installer Teams Shared Computer Toolkit extension de Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Préparer un client développeur pour le test

Si vous n’en avez pas encore, créez un client bac à sable [Microsoft 365](/office/developer-program/microsoft-365-developer-program-get-started) développeur ou obtenez un client test par le biais de votre organisation.

Une fois que vous avez un [](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading) client, vous devez activer le chargement de version d’installation pour votre client en vous signant à [Centre d'administration Microsoft 365](https://admin.microsoft.com) et en naviguant vers Afficher toutes les applications > Teams > Teams > les stratégies d’installation > **globale**.  Basculez sur Télécharger **applications personnalisées et** **enregistrez.**

Si vous avez un client existant, vérifiez que le chargement de version latéral est activé en vous Teams et en sélectionnant **Applications.** Vous verrez **l’Télécharger une** option d’application personnalisée si le chargement de version de version est activé pour votre client.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Le chargement indépendant est activé pour votre client si vous voyez l’option « Télécharger une application personnalisée » à partir du Teams « Applications »":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscrire votre client développeur pour les Office 365 de publication ciblées

> [!IMPORTANT]
> Reportez-vous au dernier blog [du développeur Microsoft Teams - Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/category/teams/) pour vérifier si la prise en charge outlook.com et office.com des applications Teams est disponible pour votre client test.

Pour afficher un aperçu Teams applications en cours d’exécution outlook.com ou office.com, choisissez votre client test pour Office 365 [de publication ciblées.](/microsoft-365/admin/manage/release-options-in-office-365#targeted-release)

1. Connectez-vous Centre d'administration Microsoft 365 à l’aide des informations d’identification de votre client test et accédez à l’onglet Profil d’organisation (*Paramètres* Profil d’organisation des [](https://admin.microsoft.com/AdminPortal/Home?#/Settings/OrganizationProfile)  >  *paramètres* de  >>  l’organisation).) Sélectionnez **les préférences de publication** et l’une des préférences de *publication* ciblée :

  :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Centre d'administration Microsoft 365 menu « Préférences de publication » avec l’option de publication ciblée sélectionnée":::

  Pour plus d’informations sur Office 365 options de publication, voir Configurer les options de publication [standard](/microsoft-365/admin/manage/release-options-in-office-365) ou ciblée dans *Centre d'administration Microsoft 365'aide.*

1. Vérifiez que votre client dispose de la prise en charge Teams onglets personnels en cours d’exécution sur office.com et outlook.com en vous signant avec vos informations d’identification client de test. Si vous voyez une option d’ellipses (**...**) sur la barre latérale (point d’entrée pour les onglets personnels chargés de Teams), votre client est pris en charge.

  :::image type="content" source="images/outlook-web-ellipses.png" alt-text="Ellipses '...' point d’entrée vers les applications Teams d’onglets chargés de outlook.com":::

1. Vérifiez la prise en charge du client test pour  les extensions de messagerie dans outlook.com en vérifiant l’option Plus d’applications dans Outlook zone de message de composition.

> [!NOTE]
> Si vous avez choisi d’opter pour les publication ciblées, mais que ces options ne s’offrent pas à vous, il est probable que la prise en charge des fonctionnalités de prévisualisation soit encore en cours de déploiement sur votre client. Pour les dernières mises à jour, [voir Microsoft Teams blog du développeur.](https://devblogs.microsoft.com/microsoft365dev/category/teams/)

## <a name="install-office-apps-in-your-test-environment"></a>Installer Office applications de test dans votre environnement de test

> [!IMPORTANT]
> Reportez-vous au blog du développeur [Microsoft Teams - Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/category/teams/) pour vérifier si Outlook pour la prise en charge du bureau Windows pour les extensions de message Teams est disponible pour votre client test.

Vous pouvez prévisualiser Teams applications s’exécutant dans Outlook sur Windows bureau à l’aide d’une version *récente du canal* bêta. Pour installer une Outlook de canal bêta dans votre environnement de [](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) test, vous devrez probablement modifier le canal Microsoft 365 Apps de mise à jour pour votre client test.

Voici les étapes à suivre pour installer Office 365 applications de canal *bêta* dans votre environnement de test :

1. Connectez-vous à votre environnement de test à l’aide de votre compte client test.
1. Téléchargez [l Office de déploiement et](https://www.microsoft.com/download/details.aspx?id=49117) extrayez-le dans un dossier local.
1. Ouvrez *configuration-Office365-x86.xml* (ou le **x64.xml*, en fonction de votre environnement) dans un éditeur de texte et mettez à jour la valeur *du* canal sur `BetaChannel` .
1. À partir d’une invite de commandes avec élévation dex64.xml, exécutez (ou utilisez le fichier `setup.exe /configure configuration-Office365-x86.xml` **x64.xml,* en fonction de votre configuration).
1. Ouvrez Outlook (client de bureau) et configurer le compte de messagerie à l’aide de vos informations d’identification client de test.
1. In Outlook, open **File**  >  **Office Account** About  >  **Outlook**, and confirm that you are now on the *Beta Channel* and that your build number is **14416** or higher.
1. Basculez sur le **bouton Bientôt** disponible dans le coin de votre fenêtre Outlook client :

   :::image type="content" source="images/outlook-coming-soon.png" alt-text="Bouton « Bientôt disponible » Outlook bureau bascule sur « On » }":::

  > [!NOTE]
  > Vous devrez peut-être fermer Outlook puis redémarrer votre ordinateur pour *que* le bouton Bientôt disponible s’affiche.

Vous pouvez vérifier que votre client prend en charge les onglets personnels Teams en cours d’exécution sur Outlook pour le bureau Windows en vous signant avec vos informations d’identification de client test et en cherchant une option d’ellipses (**...**) sur la barre latérale (point d’entrée pour les onglets personnels Teams chargés de nouveau).

:::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Ellipses '...' point d’entrée vers les applications Teams onglets chargés de Outlook bureau":::

De même, vous pouvez vérifier la prise en charge du client de test pour  les extensions de messagerie dans Outlook pour le bureau Windows en vérifiant l’option Plus d’applications dans le ruban Outlook composer un message.

> [!NOTE]
> Si vous avez choisi d’opter pour les versions bêta du canal, mais que vous ne voyez pas ces options de sélection, il est probable que la prise en charge des fonctionnalités de prévisualisation soit encore en cours de déploiement sur votre client. Pour les dernières mises à jour, [voir Microsoft Teams blog du développeur.](https://devblogs.microsoft.com/microsoft365dev/category/teams/)

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Basculer vers la version d’aperçu du développeur de Teams

Assurez-vous d’opter pour la prévisualisation pour les développeurs [*publics*](../resources/dev-preview/developer-preview-intro.md) à partir de Microsoft Teams client.

1. Connectez-vous Teams avec votre compte client en bac à sable.
1. Dans le menu des ellipses (**...**) en de côté de votre profil utilisateur, sélectionnez À **propos** de et sélectionnez l’option **d’aperçu développeur.**
1. Une fois que  la boîte de dialogue s’affiche, sélectionnez Basculer vers l’aperçu développeur pour redémarrer Teams et vérifiez que la prévisualisation du développeur est désormais activée.

:::image type="content" source="images/teams-dev-preview.png" alt-text="À Teams menu des ellipses, ouvrez « À propos de » et vérifiez que l’option « Aperçu développeur » est cochée":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Installer l Visual Studio Code et l Teams Shared Computer Toolkit de prévisualisation

Si vous le souhaitez, vous pouvez tirer parti [Visual Studio Code](https://code.visualstudio.com/) pour étendre Teams applications Office et Outlook.

Le Teams Shared Computer Toolkit d’extension pour [Visual Studio Code](https://aka.ms/teams-toolkit) (ou une Teams) fournit des commandes qui peuvent vous aider à modifier votre code Teams existant pour qu’il soit compatible avec les Outlook `v2.10.0` et Office. Continuez [à activer Teams onglet personnel](extend-m365-teams-personal-tab.md) pour Office et Outlook pour en savoir plus.

## <a name="next-steps"></a>Prochaines étapes

- [Activer un onglet personnel Teams pour Office et Outlook](extend-m365-teams-personal-tab.md)
- [Activer une extension de messagerie Teams pour Outlook](extend-m365-teams-message-extension.md)