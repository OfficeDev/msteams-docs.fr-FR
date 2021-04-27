---
title: Installer Moodle LMS
description: Comment installer et configurer l'application d'intégration Dentele pour Microsoft Teams
keywords: Plug-in d'intégration d'application Teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 091192054c5add7cfbdc1e7baabc86e34cef7631
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020591"
---
# <a name="install-moodle-lms"></a>Installer Moodle LMS

Il s'agit d'un système LMS (Learning Management System) open source populaire. Il est désormais intégré à Microsoft Teams. Cette intégration permet aux enseignants et aux enseignants de collaborer autour des cours De céseurs, de poser des questions sur les notes et les devoirs, et de rester à jour avec des notifications directement dans Teams.

Pour aider les administrateurs informatiques à configurer facilement cette intégration, le plug-in Microsoft 365 En open source Est mis à jour avec les fonctionnalités suivantes :

* Inscription automatique de votre serveur Dente avec [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).
* Déploiement en un seul clic de votre bot Assistant d'accès à Azure.
* Mise en service automatique des équipes et synchronisation automatique des inscriptions d'équipes pour toutes les équipes ou sélectionnez Des cours De commercialisation.
* Installation automatique de l'onglet Dente et du bot assistant Dentier dans chaque équipe synchronisée.

Pour en savoir plus sur les fonctionnalités de cette intégration, consultez [Microsoft Teams et Le tout.](https://education.microsoft.com/resource/3dffb3a8)

## <a name="prerequisites"></a>Prerequisites

Voici les conditions préalables à l'installation et à la configuration de l'application Moodle : 

1. Informations d'identification de l'administrateur en cas de mauvaises choses.

1. Informations d'identification de l'administrateur Azure AD.

1. Un abonnement Azure dans lequel vous pouvez créer de nouvelles ressources.

**Pour installer et configurer l'application** 

Pour installer et configurer l'application, effectuez les étapes suivantes : 

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Installer les plug-ins Microsoft 365

L'intégration de L'espace Dentrechable dans Microsoft Teams est optimisée par le plug-in Open source [Microsoft 365.](https://github.com/Microsoft/o365-moodle) Pour installer le plug-in dans votre serveur Dente, vous devez avoir installé les applications suivantes :

1. Une [version stable actuelle de Sondèle](https://download.moodle.org/releases/latest/).

1. Les plug-ins [DN OpenID Connect](https://moodle.org/plugins/auth_oidc) et [Intégration Microsoft 365](https://moodle.org/plugins/local_o365) ont été téléchargés et enregistrés sur votre ordinateur local.

   > [!NOTE]
   > L'installation des plug-ins OpenID Connect et Intégration Microsoft 365 est requise pour l'intégration de Teams. En outre, le [plug-in thème Microsoft 365 Teams](https://moodle.org/plugins/theme_boost_o365teams) est vivement recommandé.

1. Connectez-vous à votre serveur En tant qu'administrateur et sélectionnez Administration du **site** dans le bloc [Paramètres](https://docs.moodle.org/22/en/Settings_block) situé dans le panneau de navigation de gauche.

1. Sélectionnez **l'onglet Plug-ins,** puis installez **les plug-ins.**

1. Dans la section **Installer le plug-in à** partir du fichier ZIP, **sélectionnez Choisir un bouton de** fichier.

1. Sélectionnez **Télécharger une** option de fichier à partir du navigation de gauche, recherchez le fichier que vous avez téléchargé, puis **sélectionnez Télécharger ce fichier.**

1. Sélectionnez **l'administration du site** dans le panneau de navigation de gauche pour revenir à votre tableau de bord d'administration. Faites défiler vers le bas **jusqu'aux plug-ins locaux** et sélectionnez le lien Intégration **Microsoft 365.** 

> [!IMPORTANT]
>
> * Conservez votre page de configuration du plug-in Dente Enfichable Microsoft 365 ouverte dans un onglet de navigateur distinct, car vous devez revenir à cet ensemble de pages tout au long du processus.  <br/><br/>
> * Si vous n'avez pas de site Vous pouvez consulter LeInsécante sur le [repo](https://github.com/azure/moodle) Azure dans lequel vous pouvez déployer rapidement une instance De son côté et la personnaliser en fonction de vos besoins.

## <a name="2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a>2. Configurer la connexion entre le plug-in Microsoft 365 et Azure Active Directory (Azure AD)

Vous devez inscrire Sondèle en tant qu'application dans votre Azure AD. Utilisez le script PowerShell pour effectuer ce processus. Le script PowerShell propose une nouvelle application Azure AD pour votre client Microsoft 365, qui est utilisée par le plug-in Microsoft 365. Le script provisione l'application pour votre client Microsoft 365, configurer les URL et autorisations de réponse requises pour l'application mise en service, puis renvoyer le `AppID` et `Key` . Vous pouvez utiliser le plug-in généré et dans votre page d'installation du plug-in Microsoft 365 Il vous permet de configurer votre site serveur `AppID` `Key` Dente avec Azure AD.

> [!IMPORTANT]
> * Le script PowerShell n'est pas mis à jour avec les éléments de configuration les plus récents. Vous devez donc effectuer la configuration manuellement en suivant les étapes décrites dans les pages de publication De l'édition [3.8.0.4 et 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) et [3.8.0.5 et 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) </br></br>
> * Pour afficher en détail les étapes manuelles que le script PowerShell automatise, voir Enregistrer votre [instance Dente en tant qu'application.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Onglet Dentelé pour le flux d'informations Microsoft Teams

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. Dans la page du plug-in Intégration de Microsoft 365, sélectionnez **l'onglet** Installation.

1. Sélectionnez **le bouton Télécharger le script PowerShell** et enregistrez-le sur votre ordinateur local.

1. Vous devez préparer le script PowerShell à partir du fichier ZIP. Effectuez les étapes suivantes pour préparer le script PowerShell à partir du fichier ZIP :

    1. Téléchargez et extrayz le `Moodle-AzureAD-Powershell.zip` fichier.
    1. Ouvrez le dossier extrait.
    1. Cliquez avec le bouton droit sur `Moodle-AzureAD-Script.ps1` le fichier et sélectionnez **Propriétés.**
    1. Sous **l'onglet Général** de la fenêtre Propriétés, cochez la case en regard de l'attribut Security situé `Unblock` en bas de la fenêtre. 
    1. Sélectionnez **OK**.
    1. Copiez le chemin d'accès au répertoire dans le dossier extrait.

1. Exécutez PowerShell en tant qu'administrateur :

    1. Sélectionnez Démarrer.
    1. Tapez PowerShell.
    1. Cliquez avec le bouton droit Windows PowerShell.
    1. Sélectionnez **Exécuter en tant qu'administrateur.**

1. Accédez au répertoire décompressé en tapant où se trouve `cd .../.../Moodle-AzureAD-Powershell` `.../...` le chemin d'accès au répertoire.

1. Exécutez le script PowerShell :

    1. Entrez `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .
    1. Entrez `./Moodle-AzureAD-Script.ps1` .
    1. Connectez-vous à votre compte d'administrateur Microsoft 365 dans la fenêtre pop-up.
    1. Entrez le nom de l'application Azure AD (par exemple, plug-in Il s'agit d'un plug-in Degle/CsDL).
    1. Entrez l'URL de votre serveur Dentelé.
    1. Copiez **l'ID d'application** et la **clé d'application** générés par le script et enregistrez-les.

1. Ensuite, vous devez ajouter le `AppID` `Key` plug-in Et au plug-in Microsoft 365 Moodle. Revenir à la page d'administration du plug-in. Le flux est le ➡ d'administration ➡'intégration Microsoft 365.

1. Sous **l'onglet Installation,** ajoutez **l'ID d'application** et la clé **d'application** que vous avez copiés précédemment, puis **sélectionnez Enregistrer les modifications.**

1. Une fois la page actualisée, vous pouvez voir une nouvelle section **Choisir la méthode de connexion.** Cochez la case par **défaut,** puis sélectionnez **Enregistrer les modifications** à nouveau.

1. Une fois la page actualisée, vous pouvez voir une autre nouvelle section consentement de **l'administrateur & informations supplémentaires.**
    1. Sélectionnez **Fournir le lien Consentement** de l'administrateur, entrez vos informations d'identification d'administrateur général Microsoft 365, puis **acceptez** d'accorder les autorisations.
    1. En regard du **champ Client Azure AD,** sélectionnez **le bouton** Détecter.
    1. En plus de **l'URL OneDrive Entreprise,** sélectionnez **le bouton** Détecter.
    1. Une fois les champs remplis, sélectionnez de nouveau le bouton Enregistrer **les modifications.**

1. Sélectionnez le **bouton** Mettre à jour pour vérifier l'installation, puis **enregistrez les modifications.**

1. Synchronisez les utilisateurs entre votre serveur Et Azure AD. En fonction de votre environnement, vous pouvez sélectionner différentes options au cours de cette étape. Pour commencer :
    1. Basculer vers **l'onglet Paramètres de synchronisation**
    1. Dans la section **Synchroniser les utilisateurs avec Azure AD,** cochez les case qui s'appliquent à votre environnement. Vous devez sélectionner ce qui suit :  

        ✔ créer des comptes dans Le Chatin pour les utilisateurs dans Azure AD . 
        ✔ tous les comptes dans Le Chatin pour les utilisateurs dans Azure AD.  

    1. Dans la section **Restriction de création d'utilisateur,** vous pouvez configurer un filtre pour limiter les utilisateurs d'Azure AD synchronisés avec Lele.
    1. La section **Mappage des champs** utilisateur vous permet de personnaliser Azure AD en mappage de champ De profil utilisateur en toute convivialisation.
    1. Dans la section **Synchronisation teams,** vous pouvez choisir de créer automatiquement des groupes, tels que des équipes pour une partie ou l'ensemble, de vos cours Vous pouvez créer des groupes.

> [!NOTE]
> Le [Cron](https://docs.moodle.org/310/en/Cron) DeNte s'exécute en fonction de la planification des tâches. La planification par défaut est une fois par jour. Toutefois, le cron doit s'exécuter plus fréquemment pour que tout reste synchronisé.

13. Pour valider [les travaux cron](https://docs.moodle.org/310/en/Cron) et les exécuter manuellement pour la première utilisation, sélectionnez le lien de **la page** Gestion des tâches programmées dans la section Synchroniser les utilisateurs avec **Azure AD.** Vous êtes alors sur la page **Tâches programmées.**

    1. Faites défiler vers le bas et recherchez les utilisateurs de synchronisation avec le travail **Azure AD,** puis **sélectionnez Exécuter maintenant.**
    1. Si vous choisissez de créer des groupes en fonction des cours existants, vous pouvez également exécuter le travail Créer des groupes d'utilisateurs **dans Microsoft 365.**

1. Revenir à la page d'administration du plug-in. Le flux de navigation est le ➡ des plug-ins ➡ Microsoft 365 Integratio. Ensuite, sélectionnez la page **Paramètres teams.** Vous devez configurer certains paramètres pour activer l'intégration de l'application Teams.

    1. Pour activer **OpenID Connect,** sélectionnez le lien Gérer l'authentification, puis sélectionnez l'icône d'œil sur la ligne  **OpenId Connect** si elle est grisée.
    1. Activez l'incorporation de cadre. Sélectionnez le **lien sécurité HTTP,** puis cochez la case en regard de l'incorporation **d'une image d'autorisation.**
    1. Activez les services web qui activent les fonctionnalités de l'API Dente. Sélectionnez **le lien Fonctionnalités** avancées, puis assurez-vous que la case à cocher en regard de Activer les **services web** est cochée.
    1. Activez les services externes pour Microsoft 365. Sélectionnez **ensuite le lien Services** externes :  

        ✔ **sélectionnez Modifier** sur la ligne **Deservices WebServices Microsoft 365.**  
        ✔ la case à cocher en regard de **Activé,** puis sélectionnez **Enregistrer les modifications**

    1. Modifiez vos autorisations utilisateur authentifiées pour leur permettre de créer des jetons de service web. Sélectionnez **le lien Modifier le rôle « Utilisateur authentifié** ». Faites défiler vers le bas et recherchez la fonctionnalité **Créer un jeton de service web** et marquez la case **à** cocher Autoriser.

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Déployer le bot assistant de l'assistant de pare-vie sur Azure

Le bot d'assistant Free Moodle pour Microsoft Teams aide les enseignants et les étudiants à répondre à des questions sur leurs cours, devoirs, notes et autres informations dans Le jeu. Le bot envoie également des notifications À l'esprit aux étudiants et aux enseignants au sein de Teams. Le bot est un projet open source tenu à jour par Microsoft et est disponible sur [GitHub.](https://github.com/microsoft/Moodle-Teams-Bot)

> [!NOTE]
> * Dans cette section, vous devez déployer des ressources dans votre abonnement Azure. Toutes les ressources sont configurées à l'aide du **niveau** libre. Selon l'utilisation de votre bot, vous devez mettre à l'échelle ces ressources.
> * Pour utiliser l'ongletUlation sans le bot, passez à [4](#4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flux d'informations sur le bot de chatouillement

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Pour installer le bot, vous devez l'inscrire sur la [plateforme d'identités Microsoft.](https://identity.microsoft.com/Landing) Cela permet à votre bot de s'authentifier sur vos points de terminaison Microsoft. 

**Pour inscrire votre bot**:

1. Go to the plugin administration page. Go to **Plugins**. Sous **Intégration Microsoft 365,** sélectionnez l'onglet **Paramètres teams.**

1. Sélectionnez le **lien Portail d'inscription des** applications Microsoft et connectez-vous avec votre ID Microsoft.

1. Entrez un nom pour votre application, tel que SondentleBot, puis sélectionnez **le bouton** Créer.

1. Copiez **l'ID d'application** et collez-le dans le champ **ID de l'application bot** dans la page **Paramètres de l'équipe.**

1. Sélectionnez le **bouton Générer un nouveau mot de** passe. Copiez le mot de passe généré et collez-le dans le champ Mot de passe de **l'application bot** dans la page **Paramètres de l'équipe.**

1. Faites défiler jusqu'au bas du formulaire et sélectionnez **Enregistrer les modifications.**

Lorsque vous avez généré votre ID d'application et votre mot de passe, l'étape suivante consiste à déployer votre bot sur Azure :

> [!div class="checklist"]
> * Sélectionnez le bouton Déployer sur **Azure** et complétez le formulaire avec les informations nécessaires, telles que l'ID de l'application bot, le mot de passe de l'application bot et le secret de l'utilisateur, sur la page **Paramètres** de l'équipe. Les informations Azure se trouve sur la page **d'installation).** 
> * Une fois le formulaire terminé, cochez la case pour accepter les conditions générales.
> * Sélectionnez le **bouton** Acheter. Toutes les ressources Azure sont déployées sur le niveau gratuit.

Une fois le déploiement des ressources terminé sur Azure, vous devez configurer le plug-in Microsoft 365 Moodle avec un point de terminaison de messagerie. Vous devez obtenir le point de terminaison à partir de votre bot dans Azure :

**Configurer le plug-in Microsoft 365 Moodle avec un point de terminaison de messagerie**  
1. Connectez-vous au [portail Azure](https://portal.azure.com).

1. Dans le volet gauche, sélectionnez les groupes de ressources et sélectionnez le groupe de ressources que vous avez utilisé ou créé lors du déploiement de votre bot. 

1. Sélectionnez **la ressource Bot WebApp** dans la liste des ressources du groupe.

1. Copiez **le point de terminaison de messagerie à** partir de la section Vue **d'ensemble.**

1. Dans Le chat, ouvrez la page **Paramètres** de l'équipe de votre plug-in Microsoft 365.

1. Dans le **champ Point de terminaison du bot,** collez l'URL que vous avez copiée et modifiez le *mot messages* en *webhook.* L'URL doit maintenant apparaître comme suit : `https://botname.azurewebsites.net/api/webhook`

1. Sélectionnez **Enregistrer les modifications.**

1. Après avoir enregistrer les modifications, revenir à  l'onglet **Paramètres** de l'équipe, sélectionnez le bouton Télécharger le fichier manifeste et enregistrez le package de manifeste de l'application sur votre ordinateur pour une utilisation supplémentaire.

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Déployer votre application Microsoft Teams

Une fois que votre bot a été déployé sur Azure et configuré pour parler à votre serveur Dente, vous devez déployer votre application Microsoft Teams. Pour ce faire, vous devez charger le fichier manifeste de l'application que vous avez téléchargé à partir de la page Paramètres de l'équipe du plug-in Microsoft 365 À l'étape précédente.

Avant d'installer l'application, vous devez veiller à activer les applications externes et à télécharger des applications. Pour ce faire, vous pouvez suivre les étapes de la documentation sur la préparation de votre client [Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) dans Teams. Vous pouvez effectuer les étapes suivantes pour déployer votre application : 

**Pour déployer votre application**

1. Ouvrez **Microsoft Teams.** 

1. Sélectionnez **l'icône** Application dans la zone inférieure gauche de la barre de navigation.

1. Sélectionnez **le lien Télécharger une application personnalisée** dans la liste des options.

   > [!NOTE]
   > Si vous êtes connecté en tant qu'administrateur général, vous devez avoir la possibilité de télécharger l'application dans le catalogue d'applications de votre organisation, sinon vous ne pouvez charger l'application que pour une équipe dont vous êtes membre.

4. Sélectionnez `manifest.zip` le package que vous avez téléchargé précédemment et sélectionnez **Enregistrer.** Si vous n'avez pas téléchargé le package de manifeste de l'application, vous pouvez le télécharger à partir de l'onglet **Paramètres** de l'équipe de la page de configuration du plug-in dans Lele.

Maintenant que l'application est installée, vous pouvez ajouter l'onglet à n'importe quel canal à qui vous avez accès. Pour ce faire, accédez au canal, sélectionnez le **symbole plus** (➕) et sélectionnez votre application dans la liste. Suivez les invites pour terminer l'ajout de l'onglet de cours De l'enfant à un canal.

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Autoriser la création automatique d'onglets Dentelé dans Microsoft Teams

Bien que les onglets Dentelé soient créés manuellement dans Microsoft Teams, vous pouvez décider de les créer automatiquement lorsque des équipes sont créées à partir de la synchronisation de cours. Pour ce faire, vous devez configurer l'ID de l'application Microsoft Teams téléchargée dans Le chat :

1. Ouvrir Microsoft Teams.

1. Sélectionnez l'icône Applications dans la zone inférieure gauche de la barre de navigation.

1. Recherchez l'application **Dentele** téléchargée ➡ sélectionnez **l'icône d'options** ➡ sélectionner le lien **de copie.**

1. Dans un éditeur de texte, collez le contenu copié. Elle doit contenir une URL telle que ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff. Copiez la dernière partie de l'URL, par exemple, qui est  `00112233-4455-6677-8899-aabbccddeeff` l'ID de l'application Microsoft Teams.

1. Dans La page de configuration du plug-in Dente, ouvrez l'onglet de l'application **Teams.**

1. Collez l'ID de l'application Microsoft Teams dans le champ D'ID de l'application Softle, puis enregistrez les modifications.

Lors de la synchronisation d'un cours d'équipe, Microsoft Teams installe automatiquement l'application Dente dans l'équipe, crée un onglet Dente dans le canal Général de Teams et la configure pour qu'elle contienne la page de cours pour le cours Dentele à partir duquel elle est synchronisée. Vous pouvez maintenant commencer à utiliser vos cours De la part de Vous pouvez commencer à utiliser vos cours d'équipe directement à partir de Microsoft Teams.

Pour partager des demandes de fonctionnalités ou des commentaires avec nous, visitez notre [page User Voice.](https://microsoftteams.uservoice.com/forums/916759-moodle)

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)

> [!div class="nextstepaction"]
> [Moodle](https://moodle.org/)

> [!div class="nextstepaction"]
> [Documentation en toute fin](https://docs.moodle.org/34/en/Installing_plugins)de vie.
