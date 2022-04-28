---
title: Configurez votre environnement de développement pour étendre Teams applications sur Microsoft 365
description: Voici les conditions préalables à l’extension de vos applications Teams sur Microsoft 365
ms.date: 02/11/2022
ms.openlocfilehash: 094da29fdb871ef4af091e32e123e2d644b7445f
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104069"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Configurez votre environnement de développement pour étendre Teams applications sur Microsoft 365

> [!NOTE]
> Étendre l’application Teams sur Microsoft 365 est actuellement disponible uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

L’environnement de développement pour étendre Teams applications sur Microsoft 365 est similaire au développement Microsoft Teams. Cet article décrit les configurations spécifiques requises pour exécuter des builds d’aperçu des applications Microsoft Teams et Microsoft Office afin de prévisualiser Teams applications s’exécutant dans Outlook et Office.

Pour la configuration de votre environnement de développement :

> [!div class="checklist"]
>
> * [Obtenir Microsoft 365 client développeur (bac à sable) et activer le chargement indépendant](#prepare-a-developer-tenant-for-testing)
> * [Inscrire votre locataire Microsoft 365 dans *Office 365 versions ciblées*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Configurer votre compte pour accéder aux versions préliminaires de Outlook et Office](#install-office-apps-in-your-test-environment)
> * [Basculer vers la version d’évaluation du développeur de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Facultatif*] [Installer Teams Shared Computer Toolkit extension pour Microsoft Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Préparer un locataire de développeur pour le test

Vous avez besoin d’un Microsoft 365 locataire de bac à sable (sandbox) d’abonnement développeur pour configurer votre environnement de développement. Si vous n’en avez pas encore, créez un [locataire de bac à sable](/office/developer-program/microsoft-365-developer-program-get-started) ou obtenez un locataire de test par le biais de votre organisation.

Une fois que vous avez un locataire, vous devez activer le chargement indépendant pour votre locataire. Consultez [activer le chargement indépendant](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading). Pour vérifier si le chargement indépendant est activé, connectez-vous à Teams, sélectionnez **Applications**, puis recherchez **Télécharger une option d’application personnalisée**.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Télécharger une option d’application personnalisée":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscrire votre locataire de développeur pour Office 365 versions ciblées

> [!IMPORTANT]
> Reportez-vous aux dernières mises à jour sur [Microsoft Teams - blog du développeur Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/) pour vérifier si Outlook.com et Office.com la prise en charge des applications Teams sont disponibles pour votre locataire de test.

Pour inscrire votre locataire de test pour Office 365 versions ciblées :

1. Connectez-vous à [Centre d'administration Microsoft 365](https://admin.microsoft.com) avec vos informations d’identification de locataire de test.
1. Accédez à **Paramètres** >  **Org Paramètres** >  **Organization profile**.
1. Sélectionnez **Préférences de mise en production**.
1. Sélectionnez une préférence *de publication ciblée* :
    1. **Version cible pour tout le monde**
    1. **Version cible pour certains utilisateurs**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Centre d'administration Microsoft 365 menu « Préférences de mise en production » avec l’option de mise en production ciblée sélectionnée":::

1. Sélectionnez **Enregistrer**.

Pour plus d’informations sur Office 365 options de mise en production, consultez [Configurer les options de mise en production standard ou ciblée](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) dans *Centre d'administration Microsoft 365 aide*.

## <a name="install-office-apps-in-your-test-environment"></a>Installer Office applications dans votre environnement de test

> [!IMPORTANT]
> Reportez-vous aux dernières mises à jour sur [Microsoft Teams - blog du développeur Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/) pour vérifier si Outlook pour Windows prise en charge de bureau pour Teams extensions de message est disponible pour votre locataire de test.

Vous pouvez afficher un aperçu Teams applications s’exécutant dans Outlook sur Windows bureau à l’aide d’une *build de canal bêta* récente. Vérifiez si vous devez [modifier le canal de mise à jour Microsoft 365 Apps](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) pour que votre locataire de test installe une build de canal bêta Office 365.

Pour installer Office 365 applications de canal bêta dans votre environnement de test :

1. Connectez-vous à votre environnement de test avec vos informations d’identification de locataire de test.
1. Téléchargez [l’outil de déploiement Office](https://www.microsoft.com/download/details.aspx?id=49117) et extrayez-le dans un dossier local.
1. Accédez au dossier local et ouvrez *configuration-Office365-x86.xml* (ou **x64.xml*, en fonction de votre environnement) dans un éditeur de texte et mettez à jour la valeur *du canal* sur `BetaChannel`.
1. Ouvrez l’invite de commandes et accédez au chemin du dossier local.
1. Exécutez `setup.exe /configure configuration-Office365-x86.xml` (ou utilisez le fichier **x64.xml* , en fonction de votre configuration).
1. Ouvrez Outlook (client de bureau) et configurez le compte de messagerie à l’aide de vos informations d’identification de locataire de test.
1. Ouvrez **le fichier** >  **Office accountabout** >  **Outlook**.  
   Si le numéro de build est **14416** ou supérieur et que le canal est *canal bêta*, vous exécutez Microsoft 365 build de canal bêta.
1. Dans le coin supérieur droit, activez le bouton bascule **Bientôt disponible** .

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Option bascule « Bientôt disponible » dans Outlook":::

> [!NOTE]
> Vous devrez peut-être fermer Outlook et redémarrer votre ordinateur pour que le bouton *Bientôt disponible* apparaisse.

Vous pouvez vérifier la prise en charge du locataire de test pour votre compte de locataire :

* Pour Teams onglets personnels s’exécutant sur office.com, outlook.com et Outlook pour Windows bureau, connectez-vous avec vos informations d’identification de locataire de test et recherchez l’option de points de suspension (**...**) dans la barre latérale gauche de Office ou Outlook.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Option ellipses ('...') sur la barre latérale gauche de Outlook":::

* Pour les extensions de message dans outlook.com et Outlook pour Windows, recherchez **l’option Plus d’applications** en bas du volet de composition de messages Outlook.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Option « Autres applications » dans le volet Outlook composer un message":::

> [!NOTE]
> Si vous êtes abonné aux versions du canal bêta, mais que vous ne voyez pas ces options de sélection, il est probable que la prise en charge des fonctionnalités en préversion soit en cours de déploiement sur votre locataire. Pour obtenir les dernières mises à jour, consultez [Microsoft Teams Blog du développeur](https://devblogs.microsoft.com/microsoft365dev/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Basculer vers la version d’évaluation du développeur de Teams

Veillez à basculer vers la [préversion du développeur public](../resources/dev-preview/developer-preview-intro.md) à partir de votre client Microsoft Teams.

1. Connectez-vous à Teams avec vos informations d’identification de locataire de bac à sable.
1. Dans le menu des points de suspension (**...**) en regard de votre profil utilisateur, sélectionnez La **préversion d’AboutDeveloper** > . Une boîte de dialogue s’affiche, **sélectionnez Basculer vers la préversion du développeur**.
1. Après le redémarrage de l’application Teams, accédez au menu des points de suspension (**...**) en regard de votre profil utilisateur et vérifiez si **la préversion du développeur** est sélectionnée.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Option de préversion du développeur public dans Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Installer l’extension Visual Studio Code et Teams Shared Computer Toolkit Preview

Si vous le souhaitez, vous pouvez utiliser [Visual Studio Code](https://code.visualstudio.com/) pour étendre Teams applications dans Office et Outlook.

La Teams Shared Computer Toolkit d’extension [pour Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`ou version ultérieure) fournit des commandes qui peuvent vous aider à modifier votre code Teams existant pour qu’il soit compatible avec Outlook et Office. Pour plus d’informations, consultez [activer Teams onglet personnel pour Office et Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Étapes suivantes

* [Activer un onglet personnel Teams pour Office et Outlook](extend-m365-teams-personal-tab.md)
* [Activer une extension de message Teams pour Outlook](extend-m365-teams-message-extension.md)
