---
title: Installer Moodle LMS
description: Comment installer et configurer l’application d’intégration Moodle pour Microsoft Teams
keywords: Teams Plugins d’intégration d’applications Moodle
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: d7fddad80ca08fd4ca8dee352cdcbc46e8e97dcd
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566718"
---
# <a name="install-moodle-lms"></a>Installer Moodle LMS

Dans cet article, vous apprendrez à installer le Moodle LMS.

> [!NOTE]
> Pour aider les administrateurs informatique à configurer facilement Moodle et l’intégration Teams, les Microsoft 365 Moodle Plugins open source sont mis à jour pour les éléments suivants :
>
> * Enregistrement automatique de votre serveur Moodle avec [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).
>
> * Déploiement en un clic de votre bot Moodle Assistant sur Azure.
>
> * Auto-provision des équipes et autosynchronisation des inscriptions d’équipe pour tous ou sélectionner les cours Moodle.
>
> * Auto-installation de l’onglet Moodle et du bot assistant Moodle dans chaque équipe synchronisée.
>
> Pour en savoir plus sur les fonctionnalités de cette intégration, [consultez Microsoft Teams et Moodle](https://education.microsoft.com/resource/3dffb3a8).

## <a name="prerequisites"></a>Configuration requise

Voici les conditions préalables à l’installation de Moodle :

* Informations d’identification de l’administrateur Moodle.

* Informations d’identification de l’administrateur AD Azure.

* Un abonnement Azure où vous pouvez créer de nouvelles ressources.

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Installez les plugins Microsoft 365 Moodle

L’intégration moodle Microsoft Teams est alimentée par l’open source [Microsoft 365 ensemble de plugins Moodle.](https://github.com/Microsoft/o365-moodle)

### <a name="requisite-applications-and-plugins"></a>Applications et plugins requis

Assurez-vous d’installer et de télécharger ce qui suit avant de procéder à l Microsoft 365 installer des plugins Moodle :

1. Assurez-vous [d’installer une version stable actuelle de Moodle](https://download.moodle.org/releases/latest/).

1. Téléchargez et enregistrez les plugins Moodle [OpenID Connecter](https://moodle.org/plugins/auth_oidc) et [Microsoft 365'intégration](https://moodle.org/plugins/local_o365) de votre ordinateur local.

    > [!NOTE]
    > L’installation des plugins openid Connecter et Microsoft 365'intégration sont nécessaires pour l’intégration Teams’intégration.
    >
    > En outre, les [plugins Microsoft 365 Teams thème](https://moodle.org/plugins/theme_boost_o365teams) sont fortement recommandés.

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365 Plugins Moodle

1. Connectez-vous à votre serveur Moodle en tant qu’administrateur et **sélectionnez l’administration** du site [à partir du bloc Paramètres situé](https://docs.moodle.org/22/en/Settings_block) dans le panneau de navigation gauche.

1. Sélectionnez **l’onglet Plugins,** puis sélectionnez **Installer des plugins.**

1. À partir **des plugins Installer de la** section fichier ZIP, **sélectionnez Choisir un fichier**.

1. Sélectionnez **Télécharger une** option de fichier à partir du panneau de navigation gauche, recherchez le fichier que vous avez téléchargé et **sélectionnez Télécharger ce fichier**.

1. Sélectionnez **l’administration** du site à partir du panneau de navigation gauche pour revenir à votre tableau de bord admin. Faites défiler vers le **bas pour les plugins** locaux et sélectionnez **le lien Microsoft 365'intégration.**

    > [!IMPORTANT]
    >
    > * Gardez votre page Microsoft 365 configuration Moodle Plugins ouverte dans un onglet de navigateur distinct, car vous devez revenir à cet ensemble de pages tout au long du processus.  
    >
    > * Si vous n’avez pas de site Moodle existant, rendez-vous sur le repo [Moodle on Azure,](https://github.com/azure/moodle) et déployez rapidement une instance Moodle et personnalisez-la à vos besoins.

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a>2. Configurer la connexion entre les plugins Microsoft 365 et Azure Active Directory (Azure AD)

Vous devez configurer la connexion entre les plugins Microsoft 365 et Azure AD.

### <a name="requisites"></a>Accessoires

Inscrivez Moodle comme application dans votre annonce Azure, en utilisant le script PowerShell. Le script Powershell dispositions suivantes:

* Une nouvelle application Azure AD pour votre Microsoft 365, qui est utilisée par les Microsoft 365 Moodle Plugins.
* L’application pour votre Microsoft 365, configurer les URL de réponse requises et les autorisations pour l’application provisionnée, et retourne le `AppID` et `Key` .

Utilisez la `AppID` `Key` page d’installation Microsoft 365 Moodle Plugins pour configurer votre site serveur Moodle avec Azure AD.

> [!IMPORTANT]
>
> * Le script PowerShell n’est pas mis à jour avec les derniers éléments de configuration, par conséquent, vous devez compléter la configuration manuellement en suivant les étapes décrites dans les pages de sortie Moodle [3.8.0.4 et 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) [et 3.8.0.5 et 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)
>
> * Pour plus d’informations sur l’enregistrement manuel de votre instance Moodle, [consultez l’enregistrement de votre instance Moodle en tant qu’application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>L’onglet Moodle pour le flux Microsoft Teams’information

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. À partir de la page Microsoft 365'intégration, sélectionnez **l’onglet Configuration.**

1. Sélectionnez **le bouton Télécharger powershell** script et enregistrez-le comme un dossier ZIP sur votre ordinateur local.

1. Préparez le script PowerShell à partir du fichier ZIP comme suit : 

    1. Téléchargez et extrayz `Moodle-AzureAD-Powershell.zip` le fichier.
    1. Ouvrez le dossier extrait.
    1. Cliquez à droite sur le `Moodle-AzureAD-Script.ps1` fichier et sélectionnez **Propriétés**.
    1. Sous **l’onglet** Général de la fenêtre Propriétés, sélectionnez la `Unblock` case à cocher à côté de **l’attribut** Sécurité situé au bas de la fenêtre.
    1. Sélectionnez **OK**.
    1. Copiez le chemin d’annuaire vers le dossier extrait.

1. Exécutez PowerShell en tant qu’administrateur :

    1. Sélectionnez Démarrer.
    1. Type PowerShell.
    1. Clic droit sur **Windows PowerShell**.
    1. Sélectionnez **Exécuter en tant qu’administrateur**.

1. Naviguez vers le répertoire décompressé en tapant `cd .../.../Moodle-AzureAD-Powershell` `.../...` où est le chemin vers le répertoire.

1. Exécutez le script PowerShell :

    1. Entrez `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .
    1. Entrez `./Moodle-AzureAD-Script.ps1` .
    1. Connectez-vous à votre Microsoft 365'administrateur de votre ordinateur dans la fenêtre contextée.
    1. Entrez le nom de l’application AD Azure, par exemple, les plugins Moodle ou Moodle.
    1. Entrez l’URL de votre serveur Moodle.
    1. Copiez **l’ID `AppID` d’application ( )** et la clé **`Key` d’application ( )** généré par le script et enregistrez-les.

1. Ensuite, vous devez ajouter `AppID` le et à la Microsoft 365 `Key` Moodle Plugins. Retour à la page d’administration des plugins, administration du site > plugins > Microsoft 365 intégration.

1. Sur **l’onglet** Configuration ajouter `AppID` le et vous copié `Key` précédemment, puis sélectionnez **Enregistrer les modifications**. Après la mise à jour de la page, vous pouvez voir une nouvelle section **Choisir la méthode de connexion**.

1. Dans la **méthode de connexion Choisir,** sélectionnez la case à cocher **étiquetée Par défaut,** puis sélectionnez **Enregistrer les modifications à** nouveau.

1. Après la page se rafraîchit, vous pouvez voir une autre nouvelle section **Consentement admin & informations supplémentaires**.
    1. Sélectionnez **Fournir le lien consentement** administrateur, entrez vos Microsoft 365 informations d’identification de l’administrateur global, puis **acceptez** d’accorder les autorisations.
    1. À côté du **champ Locataire AD Azure,** sélectionnez le **bouton Détecter.**
    1. À côté de **l OneDrive Entreprise URL,** sélectionnez **le bouton** Détecter.
    1. Une fois que les champs se peuplent, sélectionnez **à nouveau le** bouton Enregistrer les modifications.

1. Sélectionnez le **bouton Mise** à jour pour vérifier l’installation, puis sélectionnez Enregistrer **les modifications**.

1. Synchronisez les utilisateurs entre votre serveur Moodle et Azure AD. Pour commencer :

    > [!NOTE]
    > Selon votre environnement, vous pouvez sélectionner différentes options au cours de cette étape.

1. Synchronisez les utilisateurs entre votre serveur Moodle et Azure AD. Selon votre environnement, vous pouvez sélectionner différentes options au cours de cette étape. Pour commencer :
    1. Passez à **l’onglet Paramètres Sync**.

    1. Dans la section **Synchron utilisateurs avec Azure AD,** sélectionnez les casettes qui s’appliquent à votre environnement. Vous devez sélectionner les éléments suivants :  

        ✔ créer des comptes dans Moodle pour les utilisateurs d’Azure AD.

        ✔ mettre à jour tous les comptes de Moodle pour les utilisateurs d’Azure AD.

    1. Dans la section **Restriction de création** utilisateur, vous pouvez configurer un filtre pour limiter les utilisateurs azure ad synchronisés avec Moodle.
    1. La section **De mappage de** champ utilisateur vous permet de personnaliser l’annonce Azure à la cartographie de champ de profil utilisateur Moodle.
    1. Dans la **section Teams Sync,** vous pouvez sélectionner pour créer automatiquement des groupes, tels que des équipes pour certains ou pour tous vos cours Moodle existants.

13. Pour valider [les travaux cron](https://docs.moodle.org/310/en/Cron) et les exécuter manuellement pour la première série, sélectionnez le lien **de page de gestion des tâches** planifiées dans la section Sync utilisateurs avec **Azure AD.** Cela vous emmène à la page **Tâches planifiées.**

    1. Faites défiler vers le bas et **trouvez les utilisateurs Sync avec azure AD** travail et **sélectionnez Exécuter maintenant**.
    1. Si vous sélectionnez pour créer des groupes en fonction des cours existants, vous pouvez également exécuter **les groupes d’utilisateurs Create Microsoft 365** travail.

    > [!NOTE]
    >
    > Le Moodle [Cron fonctionne](https://docs.moodle.org/310/en/Cron) selon le calendrier des tâches. L’horaire par défaut est une fois par jour. Toutefois, le cron doit fonctionner plus fréquemment pour garder tout synchronisé.

1. Revenez à la page d’administration des plugins, **à l’administration du site > à l’intégration > Microsoft 365 et** sélectionnez la page **Teams Paramètres** site.

1. Sur la page **Teams Paramètres,** configurez les paramètres requis pour activer l’intégration Teams’application.

    1. Pour activer **OpenID Connecter**, sélectionnez le lien **d’authentification Manage** et sélectionnez l’icône **œil sur la ligne openid Connecter** si elle est grisonnée.
    1. Pour activer l’intégration du cadre, sélectionnez le **lien HTTP Security,** puis sélectionnez la case à cocher à côté pour **autoriser l’intégration du cadre.**
    1. Pour activer les services Web, qui permettent les fonctionnalités de l’API Moodle, sélectionnez **le lien Fonctionnalités** avancées, puis assurez-vous que la case à cocher **à côté des services Web Enable** est sélectionnée.
    1. Pour activer les services externes pour Microsoft 365, sélectionnez le **lien services** externes, puis :  

        ✔ **Sélectionnez Modifier** sur **la ligne Moodle Microsoft 365 Webservices.**

        ✔ sélectionnez la case à cocher à côté **de Activé,** puis sélectionnez **Enregistrer les modifications**

    1. Modifiez vos autorisations utilisateur authentifiées pour leur permettre de créer des jetons de service Web.

        ✔ le rôle **d’édition Lien utilisateur authentifié.**

        ✔ faites défiler vers le bas et **trouvez la fonctionnalité de jetons de service Web** Create a et sélectionnez la case à cocher **Autoriser.**

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Déployer le Moodle Assistant Bot sur Azure

Le bot gratuit assistant Moodle pour les Microsoft Teams les enseignants et les étudiants à répondre aux questions sur leurs cours, devoirs, notes, et d’autres informations dans Moodle. Le bot envoie également des notifications Moodle aux élèves et aux enseignants dans Teams. Le bot est un projet open-source maintenu par Microsoft, et est disponible sur [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
>
> * Déployez des ressources sur votre abonnement Azure. Toutes les ressources ont été configurées à l’aide **du** niveau gratuit. Selon l’utilisation de votre bot, vous devrez peut-être mettre à l’échelle ces ressources.
>
> * Pour utiliser l’onglet Moodle sans le bot, passer à [4](#4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flux d’information de bot moodle

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Pour installer le bot, vous devez l’enregistrer sur la [plate-forme d’identité Microsoft](https://identity.microsoft.com/Landing). Cela permet à votre bot de s’authentifier par rapport à vos paramètres Microsoft. 

**Pour enregistrer votre bot**

1. Allez à la page d’administration plugins, puis sélectionnez **Plugins**. Sous **Microsoft 365'intégration,** sélectionnez **l’onglet** Teams Paramètres’eau.

1. Sélectionnez le **lien Portail d’enregistrement d’applications Microsoft** et connectez-vous avec votre identifiant Microsoft.

1. Entrez un nom pour votre application, tel que MoodleBot et sélectionnez le **bouton Créer.**

1. Copiez **l’ID d’application** et passez-le dans **le champ d’identification de** l’application Bot sur la page **Paramètres’équipe.**

1. Sélectionnez le **bouton Générer un nouveau mot** de passe. Copiez le mot de passe généré et coller dans le champ **Mot de passe d’application Bot** sur la page **Paramètres’équipe.**

1. Faites défiler vers le bas du formulaire et sélectionnez **Enregistrer les modifications**.

Après avoir généré votre identifiant d’application et votre mot de passe, déployez votre bot sur Azure :

> [!div class="checklist"]
> * Sélectionnez **Déployer sur Azure** et remplissez le formulaire avec les informations nécessaires, telles que l’ID d’application Bot, le mot de passe d’application Bot et le Secret Moodle sur la page **Teams Paramètres'** utilisateur. Les informations Azure sont sur la page **Configuration.** 
> * Après avoir rempli le formulaire, sélectionnez la case à cocher pour accepter les modalités.
> * Sélectionnez **Achat**. Toutes les ressources Azure sont déployées au niveau libre.

Une fois les ressources déployées sur Azure, vous devez configurer les plugins Moodle Microsoft 365 avec un point de terminaison de messagerie. Vous devez obtenir le point de terminaison de votre bot dans Azure :

1. Connectez-vous au [portail Azure](https://portal.azure.com).

1. Dans le volet gauche, sélectionnez groupes de **ressources et** sélectionnez le groupe de ressources que vous avez utilisé ou créé, tout en déployant votre bot.

1. Sélectionnez **la ressource WebApp Bot** à partir de la liste des ressources du groupe.

1. Copiez le **point de terminaison de** messagerie de la section Vue **d’ensemble.**

1. Dans Moodle, ouvrez la **page Paramètres’équipe** de votre Microsoft 365 Moodle Plugins.

1. Dans le **champ Bot Endpoint,** coller l’URL que vous venez de copier et modifier les *messages de mot* en *webhook*. L’URL doit apparaître comme suit : `https://botname.azurewebsites.net/api/webhook`

1. Sélectionnez **Enregistrer les modifications**.

1. Après avoir sélectionné les modifications, retournez à **l’onglet Team Paramètres,** sélectionnez **le bouton Télécharger le fichier manifeste** et enregistrez le paquet manifeste de l’application sur votre ordinateur pour une utilisation supplémentaire.

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Déployez votre application Microsoft Teams’argent

Après le déploiement de votre bot sur Azure et configuré pour parler à votre serveur Moodle, vous devez déployer votre Microsoft Teams application. Pour ce faire, vous devez charger le fichier manifeste de l’application que vous avez téléchargé à partir de la page Microsoft 365 Moodle Plugins Team Paramètres dans l’étape précédente.

Avant d’installer l’application, vous devez vous assurer d’activer les applications externes et le téléchargement d’applications. Pour plus d’informations, [consultez Préparer votre Microsoft 365 locataire.](../concepts/build-and-test/prepare-your-o365-tenant.md) 

**Pour déployer votre application** 

1. Ouvrez **Microsoft Teams**. 

1. Sélectionnez **l’icône** App sur la zone inférieure gauche de la barre de navigation.

1. Sélectionnez le **Télécharger un lien d’application** personnalisé à partir de la liste des options.

   > [!NOTE]
   > Si vous êtes connecté en tant qu’administrateur global, vous devez avoir la possibilité de télécharger l’application sur le catalogue d’applications de votre organisation, sinon vous ne pouvez charger l’application que pour une équipe dont vous êtes membre.

4. Sélectionnez le `manifest.zip` package que vous avez téléchargé précédemment et sélectionnez **Enregistrer**. Si vous n’avez pas téléchargé le paquet manifeste de l’application, vous pouvez télécharger **à partir de l’onglet Team Paramètres** de la page de configuration des plugins dans Moodle.

Maintenant que vous avez installé l’application, vous pouvez ajouter l’onglet à n’importe quel canal à qui vous avez accès. Pour ce faire, accédez au canal, **sélectionnez le symbole plus** (➕) et sélectionnez votre application dans la liste. Suivez les invites pour terminer l’ajout de votre onglet de cours Moodle à un canal.

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Autoriser la création automatique d’onglets Moodle dans Microsoft Teams

Bien que les onglets Moodle soient créés manuellement dans Microsoft Teams, vous pouvez décider de les créer automatiquement lorsque des équipes sont créées à partir de la synchronisation des cours. Pour ce faire, vous devez configurer l’iD de l’application Microsoft Teams téléchargée dans Moodle.

**Pour permettre la création automatique d’onglets Moodle**

1. Ouvrir Microsoft Teams.

1. Sélectionnez l’icône Apps dans la zone inférieure gauche de la barre de navigation.

1. Localisez **l’application Moodle téléchargée** > l’icône **options** > sélectionner le **lien de copie**.

1. Dans un éditeur de texte, coller le contenu copié. Il doit contenir une URL telle que ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff. Copiez la dernière partie de l’URL, par exemple `00112233-4455-6677-8899-aabbccddeeff` , qui est l’ID de l’application Microsoft Teams’utilisateur.

1. Dans Moodle, ouvrez **l’onglet Teams’application Moodle** de votre page de configuration Microsoft 365 Moodle Plugins.

1. Coller l’iD de l’application Microsoft Teams dans le champ d’identification de l’application Moodle, et enregistrer les modifications.

Lorsqu’un cours Moodle est synchronisé, Microsoft Teams installe automatiquement l’application Moodle dans l’équipe, crée un onglet Moodle dans le canal général de Teams et la configure pour contenir la page de cours du cours Moodle à partir duquel elle est synchronisée. Vous pouvez maintenant commencer à travailler avec vos cours Moodle directement à partir de Microsoft Teams.

> [!NOTE]
> Pour partager toutes les demandes de fonctionnalités ou commentaires avec nous, visitez notre [page Voix utilisateur](https://microsoftteams.uservoice.com/forums/916759-moodle).

## <a name="see-also"></a>Voir aussi

- [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
- [Moodle](https://moodle.org/)
- [Documentation Moodle](https://docs.moodle.org/34/en/Installing_plugins).

