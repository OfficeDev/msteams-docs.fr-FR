---
title: Installation de l’intégration DeNte avec Microsoft Teams
description: Comment installer et configurer l’application d’intégration Dentele pour Microsoft Teams
keywords: Plug-in d’intégration d’application Teams
ms.topic: how-to
ms.author: lajanuar
author: laujan
ms.openlocfilehash: bb3de6b3897105ff3564ecd332cba28a0db85b0f
ms.sourcegitcommit: a16590b2ccc46e1b6d17cbb367762a3c16ff779c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/05/2021
ms.locfileid: "50115740"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a>Installation de l’intégration d’Ile-de-la-Chateille à Microsoft Teams

[Le système](https://moodle.org/)LMS (Learning Management System) open source populaire est désormais intégré à Microsoft Teams. Cette intégration permet aux enseignants et aux enseignants de collaborer autour des cours De l’esprit, de poser des questions sur les notes et les devoirs, et de rester à jour avec des notifications directement dans Teams.

Pour aider les administrateurs informatiques à configurer facilement cette intégration, nous avons mis à jour notre plug-in Open Source Microsoft 365 Etendu avec les fonctionnalités suivantes :

* Inscription automatique de votre serveur DeNte avec [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).
* Déploiement en un seul clic de votre bot Assistant d’accès à Azure.
* Mise en service automatique des équipes et synchronisation automatique des inscriptions d’équipes pour toutes les équipes ou sélectionnez Des cours De commercialisation.
* Installation automatique de l’onglet Dente et du bot assistant Dentier dans chaque équipe synchronisée.

Pour en savoir plus sur les  fonctionnalités que cette intégration fournit, consultez [Microsoft Teams et Lele.](https://education.microsoft.com/resource/3dffb3a8)

## <a name="prerequisites"></a>Configuration requise

Pour installer et configurer cette application, vous devez :

1. Informations d’identification de l’administrateur en cas de mauvaises choses.

1. Informations d’identification de l’administrateur Azure AD.

1. Un abonnement Azure dans lequel vous pouvez créer de nouvelles ressources.

## <a name="step-1-install-the-microsoft-365-moodle-plugins"></a>Étape 1 : Installer les plug-ins Microsoft 365

L’intégration de L’espace Dentrechable dans Microsoft Teams est optimisée par le plug-in Open source [Microsoft 365.](https://github.com/Microsoft/o365-moodle) Pour installer le plug-in dans votre serveur Dente, vous devez avoir installé les logiciels suivants :

1. Une [version stable actuelle de Sondèle](https://download.moodle.org/releases/latest/).

1. Les plug-ins [DN OpenID Connect](https://moodle.org/plugins/auth_oidc) et [Intégration Microsoft 365](https://moodle.org/plugins/local_o365) ont été téléchargés et enregistrés sur votre ordinateur local.

> [!NOTE]
> L’installation des plug-ins OpenID Connect et Intégration De Microsoft 365 est requise pour l’intégration de Teams. En outre, le [plug-in de thème Microsoft 365 Teams](https://moodle.org/plugins/theme_boost_o365teams) est vivement recommandé.

3. Connectez-vous à votre serveur En tant qu’administrateur et sélectionnez Administration du **site** dans le bloc [Paramètres](https://docs.moodle.org/22/en/Settings_block) situé dans le panneau de navigation de gauche.

1. Sélectionnez **l’onglet Plug-ins,** puis **sélectionnez Installer les plug-ins.**

1. Sous le **plug-in Installer à partir de la** section Fichier ZIP, sélectionnez le bouton Choisir **un** fichier.

1. Sélectionnez les options **Télécharger un fichier** à partir du navigation de gauche, recherchez le fichier que vous avez téléchargé ci-dessus, puis choisissez Télécharger ce **fichier.**

1. Sélectionnez **l’option d’administration du** site dans le panneau de navigation de gauche pour revenir à votre tableau de bord d’administration. Faites défiler vers le bas **jusqu’aux plug-ins locaux** et sélectionnez le lien Intégration **Microsoft 365.** **Gardez cette page de configuration ouverte dans un onglet de navigateur distinct tout au long du processus d’installation.**

Vous trouverez plus d’informations sur la façon d’installer des plug-ins De l’api Dente dans la [documentation de LaSerrante.](https://docs.moodle.org/34/en/Installing_plugins)

> [!IMPORTANT]
>
> * Conservez votre page de configuration du plug-in Dente Enfichable Microsoft 365 ouverte dans un onglet de navigateur distinct . Vous revenirez à cet ensemble de pages tout au long du processus.  <br/><br/>
>* Si vous n’avez pas de site Vous pouvez consulter LeInsécante sur le [repo](https://github.com/azure/moodle) Azure dans lequel vous pouvez déployer rapidement une instance De son côté et la personnaliser en fonction de vos besoins.

## <a name="step-2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a>Étape 2 : Configurer la connexion entre le plug-in Microsoft 365 et Azure Active Directory (Azure AD)

Ensuite, vous devrez inscrire Le chat en tant qu’application dans votre Azure AD. Nous avons fourni un script PowerShell pour vous aider à effectuer ce processus. Le script PowerShell propose une nouvelle application Azure AD pour votre client Microsoft 365, qui sera utilisée par le plug-in Microsoft 365 Moodle. Le script configurera l’application pour votre client Microsoft 365, configurera les URL et autorisations de réponse requises pour l’application mise en service, et retournera `AppID` et `Key` . Vous pouvez utiliser le plug-in généré et dans votre page d’installation du plug-in Microsoft 365 Il vous permet de configurer votre site serveur `AppID` `Key` Dente avec Azure AD.

>[!IMPORTANT]
> Le script PowerShell n’est pas mis à jour avec les éléments de configuration les plus récents. Vous devez donc effectuer la configuration manuellement en suivant les étapes décrites dans les pages de publication De l’édition [3.8.0.4 et 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) et [3.8.0.5 et 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) </br></br>
> Pour afficher en détail les étapes manuelles  que le script PowerShell automatise, voir Enregistrer votre [instance Dente en tant qu’application.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Onglet Dentelé pour le flux d’informations Microsoft Teams

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. Dans la page plug-in Intégration de Microsoft 365, sélectionnez **l’onglet** Installation.

1. Sélectionnez **le bouton Télécharger le script PowerShell** et enregistrez-le sur votre ordinateur local.

1. Vous devez préparer le script PowerShell à partir du fichier ZIP. Pour ce faire, procédez comme suit :

    * Téléchargez et extrayz le `Moodle-AzureAD-Powershell.zip` fichier.
    * Ouvrez le dossier extrait.
    * Cliquez avec le bouton droit sur `Moodle-AzureAD-Script.ps1` le fichier et sélectionnez **Propriétés.**
    * Sous **l’onglet Général** de la fenêtre Propriétés, cochez la case en regard de l’attribut Security situé `Unblock` en bas de la fenêtre. 
    * Sélectionnez **OK**.
    * Copiez le chemin d’accès au répertoire dans le dossier extrait.

1. Vous allez ensuite exécuter PowerShell en tant qu’administrateur :

    * Sélectionnez Démarrer.
    * Tapez PowerShell.
    * Cliquez avec le bouton droit Windows PowerShell.
    * Sélectionnez « Exécuter en tant qu’administrateur ».

1. Accédez au répertoire décompressé en tapant où se trouve `cd .../.../Moodle-AzureAD-Powershell` `.../...` le chemin d’accès au répertoire.

1. Exécutez le script PowerShell :

    * Entrez `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .
    * Entrez `./Moodle-AzureAD-Script.ps1` .
    * Connectez-vous à votre compte d’administrateur Microsoft 365 dans la fenêtre pop-up.
    * Entrez le nom de l’application Azure AD (par exemple, plug-in Boniment/Songle).
    * Entrez l’URL de votre serveur Dentelé.
    * Copiez **l’ID d’application** et la **clé d’application** générés par le script et enregistrez-les.

1. Ensuite, vous devez ajouter le ` AppID` plug-in `Key` Microsoft 365 Et au plug-in De l’autre côté. Revenir à la page d’administration du plug-in (Site administration ➡ Plugins ➡ Microsoft 365 Integration).

1. Sous **l’onglet Installation,** ajoutez **l’ID d’application** et la clé **d’application** que vous avez copiés précédemment, puis **sélectionnez Enregistrer les modifications.**

1. Une fois la page actualisée, vous devez voir une nouvelle section **Choisir la méthode de connexion.** Cochez la case par **défaut,** puis sélectionnez **Enregistrer les modifications** à nouveau.

1. Une fois la page actualisée, vous verrez une autre nouvelle section consentement de **l’administrateur & informations supplémentaires.**
    * Sélectionnez **le lien Fournir le consentement de** l’administrateur, entrez vos informations d’identification d’administrateur général Microsoft 365, puis acceptez d’accorder les autorisations. 
    * En regard du **champ Client Azure AD,** sélectionnez **le bouton** Détecter.
    * En de côté de **l’URL OneDrive Entreprise,** sélectionnez **le bouton** Détecter.
    * Une fois les champs remplis, sélectionnez de nouveau le bouton Enregistrer **les modifications.**

1. Sélectionnez le **bouton** Mettre à jour pour vérifier l’installation, puis **enregistrez les modifications.**

1. Ensuite, vous devez synchroniser les utilisateurs entre votre serveur Et Azure AD. En fonction de votre environnement, vous pouvez sélectionner différentes options au cours de cette étape. Pour commencer :
    * Basculer vers **l’onglet Paramètres de synchronisation**
    * Dans la section **Synchroniser les utilisateurs avec Azure AD,** cochez les case qui s’appliquent à votre environnement. En règle générale, vous devez, au minimum, sélectionner ce qui suit :  

        ✔ créer des comptes dans Le Chatin pour les utilisateurs dans Azure AD . 
        ✔ tous les comptes dans Le Chatin pour les utilisateurs dans Azure AD.  

    * Dans la section **Restriction de création d’utilisateur,** vous pouvez configurer un filtre pour limiter les utilisateurs d’Azure AD qui seront synchronisés avec Lele.
    * La section **Mappage des champs utilisateur** vous permet de personnaliser Azure AD en mappage de champ Profil utilisateur en toute convivialisation.
    * Dans la section **Synchronisation de Teams,** vous pouvez choisir de créer automatiquement des groupes (c’est-à-dire, des équipes) pour une partie ou l’ensemble de vos cours Existants.

> [!NOTE]
> Le [cron](https://docs.moodle.org/310/en/Cron) Dente s’exécutera en fonction de la planification des tâches (une fois par jour par défaut). Toutefois, le cron doit s’exécuter plus fréquemment pour que tout reste synchronisé.

13. Pour valider [les travaux cron](https://docs.moodle.org/310/en/Cron) (et/ou les exécuter manuellement pour la première utilisation), sélectionnez le lien de **la page** Gestion des tâches programmées dans la section Synchroniser les utilisateurs avec **Azure AD.** Vous serez alors sur la page **Tâches programmées.**

    * Faites défiler vers le bas et recherchez les utilisateurs de synchronisation avec le travail **Azure AD,** puis **sélectionnez Exécuter maintenant.**
    * Si vous avez choisi de créer des groupes en fonction des cours existants, vous pouvez également exécuter le travail Créer des groupes d’utilisateurs **dans Microsoft 365.**

1. Revenir à la page d’administration du plug-in (Administration du site ➡ plug-ins ➡'intégration Microsoft 365) et sélectionnez la page **Paramètres teams.** Vous devez configurer certains paramètres pour activer l’intégration de l’application Teams.

    * Pour activer **OpenID Connect,** sélectionnez le lien Gérer l’authentification, puis sélectionnez l’icône d’œil sur la ligne  **OpenId Connect** si elle est grisée.
    * Ensuite, vous devez activer l’incorporation d’images. Sélectionnez **le lien sécurité HTTP,** puis cochez la case en regard de l’incorporation d’une image **d’autorisation.**
    * L’étape suivante consiste à activer les services web qui activeront les fonctionnalités de l’API Dente. Sélectionnez **le lien Fonctionnalités** avancées, puis assurez-vous que la case à cocher en regard de Activer les **services web** est cochée.
    * Enfin, vous devez activer les services externes pour Microsoft 365. Sélectionnez **ensuite le lien Services** externes :  

        ✔ **sélectionnez Modifier** sur la ligne **Deservices WebServices Microsoft 365.**  
        ✔ la case à cocher en regard de **Activé,** puis sélectionnez **Enregistrer les modifications**

    * Ensuite, vous devez modifier vos autorisations utilisateur authentifiées pour leur permettre de créer des jetons de service web. Sélectionnez **le lien Modifier le rôle « Utilisateur authentifié** ». Faites défiler vers le bas et recherchez la fonctionnalité Créer **un jeton de service web** et marquez la case **à** cocher Autoriser.

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a>Étape 3 : Déployer le bot assistant de contrôle d’accès à Azure

Le bot d’assistant Free Moodle pour Microsoft Teams aide les enseignants et les étudiants à répondre à des questions sur leurs cours, devoirs, notes et autres informations dans Le jeu. Le bot envoie également des notifications À l’esprit aux étudiants et aux enseignants au sein de Teams. Le bot est un projet open source tenu à jour par Microsoft et est disponible sur [GitHub.](https://github.com/microsoft/Moodle-Teams-Bot)

> [!NOTE]
> Dans cette section, vous allez déployer des ressources dans votre abonnement Azure. Toutes les ressources sont configurées à l’aide du **niveau** libre. Selon l’utilisation de votre bot, vous devrez peut-être mettre à l’échelle ces ressources.
> Si vous souhaitez utiliser l’onglet Dentelé sans le bot, passez à [l’étape 4](#step-4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flux d’informations sur le bot de chatouillement

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Pour installer le bot, vous devez d’abord l’inscrire sur la [plateforme d’identités Microsoft.](https://identity.microsoft.com/Landing) Cela permet à votre bot de s’authentifier sur vos points de terminaison Microsoft. Pour inscrire votre bot :

1. Revenir à la page d’administration du plug-in (Administration du site ➡ plug-ins ➡'intégration Microsoft 365) et sélectionnez l’onglet **Paramètres teams.**

1. Sélectionnez le **lien Portail d’inscription des** applications Microsoft et connectez-vous avec votre ID Microsoft.

1. Entrez un nom pour votre application (par exemple, SoftleBot) et sélectionnez le **bouton** Créer.

1. Copiez **l’ID d’application** et collez-le dans le champ **ID de l’application bot** dans la page **Paramètres de l’équipe.**

1. Sélectionnez le **bouton Générer un nouveau mot de** passe. Copiez le mot de passe généré et collez-le dans le champ Mot de passe de **l’application bot** dans la page **Paramètres de l’équipe.**

1. Faites défiler jusqu’au bas du formulaire et sélectionnez **Enregistrer les modifications.**

Maintenant que vous avez généré votre ID d’application et votre mot de passe, il est temps de déployer votre bot sur Azure :

> [!div class="checklist"]
> * Sélectionnez le bouton Déployer sur **Azure** et complétez le formulaire avec les informations nécessaires (l’ID de l’application bot, le mot de passe de l’application bot et le secret de la souris se trouver dans la page Paramètres de **l’équipe.** Les informations Azure se trouve sur la page **d’installation).** 
> * Une fois le formulaire rempli, cochez la case pour accepter les conditions générales.
> * Sélectionnez **le bouton** Acheter (toutes les ressources Azure sont déployées sur le niveau gratuit).

Une fois le déploiement des ressources terminé sur Azure, vous devez configurer le plug-in Microsoft 365 Moodle avec un point de terminaison de messagerie. Vous devez obtenir le point de terminaison à partir de votre bot dans Azure :

1. Connectez-vous au [portail Azure.](https://portal.azure.com)

1. Dans le volet gauche, sélectionnez **Groupes** de ressources et choisissez le groupe de ressources que vous avez utilisé (ou créé) lors du déploiement de votre bot.

1. Sélectionnez **la ressource Bot WebApp** dans la liste des ressources du groupe.

1. Copiez **le point de terminaison de messagerie à** partir de la section Vue **d’ensemble.**

1. Dans Le chat, ouvrez la page **Paramètres** de l’équipe de votre plug-in Microsoft 365.

1. Dans le **champ Point de terminaison du bot,** collez l’URL que vous avez copiée et modifiez le *mot messages* en *webhook.* L’URL doit maintenant apparaître comme suit :  `https://botname.azurewebsites.net/api/webhook`

1. Sélectionnez **Enregistrer les modifications.**

1. Une fois vos modifications **enregistrées,** revenir à l’onglet Paramètres de l’équipe, sélectionnez le bouton Télécharger le fichier manifeste, puis enregistrez le package de manifeste de l’application sur votre ordinateur (vous l’utiliserez dans la section suivante). 

## <a name="step-4-deploy-your-microsoft-teams-app"></a>Étape 4 : Déployer votre application Microsoft Teams

Maintenant que votre bot est déployé sur Azure et configuré pour parler à votre serveur Dente, il est temps de déployer votre application Microsoft Teams. Pour ce faire, vous allez charger le fichier manifeste de l’application que vous avez téléchargé à partir de la page Paramètres de l’équipe du plug-in Microsoft 365 À l’étape précédente.

Avant de pouvoir installer l’application, vous devez vous assurer que les applications externes et le téléchargement des applications sont activés. Pour ce faire, vous pouvez suivre les étapes de la documentation sur la préparation de votre client [Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) dans Teams. Une fois que vous avez garanti que les applications externes sont activées, vous pouvez suivre les étapes ci-dessous pour déployer votre application :

1. Ouvrez **Microsoft Teams.** 

1. Sélectionnez **l’icône** Application dans la zone inférieure gauche de la barre de navigation.

1. Sélectionnez **le lien Télécharger une application personnalisée** dans la liste des options.

> [!Note]
> Si vous êtes connecté en tant qu’administrateur général, vous avez la possibilité de télécharger l’application dans le catalogue d’applications de votre organisation, sinon vous ne pourrez charger l’application que pour une équipe dont vous êtes membre.

4. Sélectionnez `manifest.zip` le package que vous avez téléchargé précédemment et sélectionnez **Enregistrer.** Si vous n’avez pas téléchargé le package de manifeste de l’application, vous pouvez le faire à partir de l’onglet **Paramètres** de l’équipe de la page de configuration du plug-in dans Lele.

Maintenant que l’application est installée, vous pouvez ajouter l’onglet à n’importe quel canal à qui vous avez accès. Pour ce faire, accédez au canal, sélectionnez le **symbole plus** (➕) et sélectionnez votre application dans la liste. Suivez les invites pour terminer l’ajout de l’onglet de cours De l’enfant à un canal.

## <a name="step-5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>Étape 5 : Autoriser la création automatique d’onglets Dentelé dans Microsoft Teams

Bien qu’il soit possible de créer manuellement les onglets Il est possible de les créer manuellement dans Microsoft Teams, mais vous pouvez décider de les créer automatiquement lorsque des équipes sont créées à partir de la synchronisation de cours. Pour ce faire, vous allez configurer l’ID de l’application Microsoft Teams téléchargée dans Le chat :

1. Ouvrir Microsoft Teams.

1. Sélectionnez l’icône Applications dans la zone inférieure gauche de la barre de navigation.

1. Recherchez l’application **Dentele** téléchargée ➡ **l’icône d’options** ➡ sélectionner le lien **copier**.

1. Dans un éditeur de texte, collez le contenu copié. Il doit contenir une URL telle que ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff. Copiez la dernière partie de l’URL, par exemple, qui est l’ID de `00112233-4455-6677-8899-aabbccddeeff` l’application Microsoft Teams.

1. Dans La page de configuration du plug-in Dente, ouvrez l’onglet de l’application **Teams.**

1. Collez l’ID de l’application Microsoft Teams dans le champ D’ID de l’application Softle, puis enregistrez les modifications.

Désormais, lors de la synchronisation d’un cours Dentele, Microsoft Teams installe automatiquement l’application Dente dans l’équipe, crée un onglet Dente dans le canal Général de Teams et le configure pour qu’il contienne la page de cours pour le cours Dentele à partir duquel il est synchronisé.

### <a name="thats-it-you-and-your-team-can-now-start-working-with-your-moodle-courses-directly-from-microsoft-teams"></a>Voilà ! Vous et votre équipe pouvez désormais commencer à utiliser vos cours d’équipe à partir de Microsoft Teams.

Pour partager des demandes de fonctionnalités ou des commentaires avec nous, visitez notre [page User Voice.](https://microsoftteams.uservoice.com/forums/916759-moodle)
