---
title: Installer Moodle LMS
description: Comment installer et configurer l’application d’intégration Dentele pour Microsoft Teams
keywords: Teams plug-ins d’intégration de l’application Enfichable
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 7460a4f6e1a15df30ebc9b1c50f43b561908c7d4
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212383"
---
# <a name="install-moodle-lms"></a>Installer Moodle LMS

Dans cet article, vous allez découvrir comment installer le LMS Dentelet.

> [!NOTE]
> Pour aider les administrateurs informatiques à configurer facilement l’intégration de Teams et De Latuale, open source Microsoft 365 Plug-ins De l’espace de jeu Est mis à jour pour les raisons suivantes :
>
> * Inscription automatique de votre serveur Dente avec [Azure Active Directory](https://azure.microsoft.com/services/active-directory/).
>
> * Déploiement en un seul clic de votre bot Assistant d’accès à Azure.
>
> * Mise en service automatique des équipes et synchronisation automatique des inscriptions d’équipes pour toutes les équipes ou sélectionnez Des cours De commercialisation.
>
> * Installation automatique de l’onglet Dente et du bot assistant Dentier dans chaque équipe synchronisée.
>
> Pour en savoir plus sur les fonctionnalités que fournit cette intégration, [voir Microsoft Teams et Lassy.](https://education.microsoft.com/resource/3dffb3a8)

## <a name="prerequisites"></a>Configuration requise

Voici les conditions préalables à l’installation de Sondèle :

* Informations d’identification de l’administrateur en cas de mauvaises choses.

* Azure AD’informations d’identification de l’administrateur.

* Un abonnement Azure dans lequel vous pouvez créer de nouvelles ressources.

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Installer les plug-ins Microsoft 365 Insoeff.

L’intégration de La Microsoft Teams est optimisée par le plug-in open source [Microsoft 365 Plug-ins Le jeu de plug-ins Dente.](https://github.com/Microsoft/o365-moodle)

### <a name="requisite-applications-and-plugins"></a>Applications et plug-ins requis

Assurez-vous d’installer et de télécharger les données suivantes avant de poursuivre l’installation Microsoft 365 plug-ins Enfichables Enfichables :

1. Assurez-vous d’installer [une version stable actuelle de Lasa.](https://download.moodle.org/releases/latest/)

1. Téléchargez et enregistrez les [plug-ins](https://moodle.org/plugins/auth_oidc) d’Connecter Et d’intégration [Microsoft 365](https://moodle.org/plugins/local_o365) à votre ordinateur local.

    > [!NOTE]
    > L’installation des plug-ins OpenID Connecter et Microsoft 365'intégration est requise pour l’intégration Teams’installation.
    >
    > En outre, les [plug-ins Microsoft 365 Teams Thème](https://moodle.org/plugins/theme_boost_o365teams) sont vivement recommandés.

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365 plug-ins Le chatin

1. Connectez-vous à votre serveur En tant qu’administrateur, puis sélectionnez Administration du **site** dans le bloc [Paramètres](https://docs.moodle.org/22/en/Settings_block) situé dans le panneau de navigation de gauche.

1. Sélectionnez **l’onglet Plug-ins,** puis installez **les plug-ins.**

1. Dans la section **Installer les plug-ins à** partir du fichier ZIP, **sélectionnez Choisir un fichier.**

1. Sélectionnez **Télécharger une** option de fichier dans le panneau de navigation de gauche, recherchez le fichier que vous avez téléchargé, puis sélectionnez Télécharger **ce fichier.**

1. Sélectionnez **Administration du site** dans le panneau de navigation de gauche pour revenir à votre tableau de bord d’administration. Faites défiler vers le bas **jusqu’aux plug-ins locaux** et sélectionnez **le lien Microsoft 365'intégration** locale.

    > [!IMPORTANT]
    >
    > * Gardez votre page Microsoft 365 configuration des plug-ins Enfichables à l’ouverture dans un onglet de navigateur distinct, car vous devez revenir à cet ensemble de pages tout au long du processus.  
    >
    > * Si vous n’avez pas de site Vous pouvez le faire, rendez-vous dans le repo [D’Azure,](https://github.com/azure/moodle) puis déployez rapidement une instance De Sondessage et personnalisez-la en fonction de vos besoins.

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory"></a>2. Configurez la connexion entre les plug-ins Microsoft 365 et les Azure Active Directory

Vous devez configurer la connexion entre les plug-ins Microsoft 365 et les Azure AD.

### <a name="requisites"></a>Conditions requises

Inscrivez Votre application En tant qu’application dans votre Azure AD, à l’aide du script PowerShell. Le script Powershell a les dispositions suivantes :

* Une nouvelle application Azure AD pour votre client Microsoft 365 client, qui est utilisée par les plug-ins Microsoft 365 Lev.
* L’application pour votre client Microsoft 365, configurer les URL de réponse requises et les autorisations pour l’application mise en service, et renvoie le `AppID` et `Key` .

Utilisez la page d’installation générée et dans votre `AppID` `Key` Microsoft 365 Plug-ins Enfichables Pour configurer votre site serveur Dentele avec Azure AD.

> [!IMPORTANT]
>
> * Le script PowerShell n’est pas mis à jour avec les éléments de configuration les plus récents. Par conséquent, vous devez effectuer la configuration manuellement en suivant les étapes décrites dans les pages de publication Der [3.8.0.4 et 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) et [3.8.0.5 et 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)
>
> * Pour plus d’informations sur l’inscription manuelle de votre instance Dente, voir Enregistrer votre [instance Dente en tant qu’application.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Onglet Dentelé pour le flux Microsoft Teams’informations

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. Dans la page Microsoft 365 plug-ins Intégration, sélectionnez **l’onglet** Installation.

1. Sélectionnez **le bouton Télécharger le script PowerShell** et enregistrez-le en tant que dossier ZIP sur votre ordinateur local.

1. Préparez le script PowerShell à partir du fichier ZIP comme suit : 

    1. Téléchargez et extrayz le `Moodle-AzureAD-Powershell.zip` fichier.
    1. Ouvrez le dossier extrait.
    1. Cliquez avec le bouton droit sur `Moodle-AzureAD-Script.ps1` le fichier et sélectionnez **Propriétés.**
    1. Sous **l’onglet Général** de la fenêtre Propriétés, cochez la case en regard de l’attribut Security situé en `Unblock` bas de la fenêtre. 
    1. Sélectionnez **OK**.
    1. Copiez le chemin d’accès au répertoire dans le dossier extrait.

1. Exécutez PowerShell en tant qu’administrateur :

    1. Sélectionnez Démarrer.
    1. Tapez PowerShell.
    1. Cliquez avec le bouton **droit sur Windows PowerShell**.
    1. Sélectionnez **Exécuter en tant qu’administrateur.**

1. Accédez au répertoire décompressé en tapant où se trouve `cd .../.../Moodle-AzureAD-Powershell` `.../...` le chemin d’accès au répertoire.

1. Exécutez le script PowerShell :

    1. Entrez `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .
    1. Entrez `./Moodle-AzureAD-Script.ps1` .
    1. Connectez-vous à Microsoft 365 compte d’administrateur dans la fenêtre pop-up.
    1. Entrez le nom de l’application Azure AD, par exemple, Les plug-ins Il est vrai ou Non.
    1. Entrez l’URL de votre serveur Dentelé.
    1. Copiez **l’ID d’application ( `AppID` ) et** la clé **d’application ( `Key` )** générés par le script et enregistrez-les.

1. Ensuite, vous devez ajouter les `AppID` `Key` plug-ins Microsoft 365 Et à l’autre. Revenir à la page d’administration des plug-ins, Administration du site > plug-ins > Microsoft 365'intégration.

1. Sous **l’onglet Installation,** ajoutez et `AppID` `Key` copiez-le précédemment, puis sélectionnez **Enregistrer les modifications.** Une fois la page actualisée, vous pouvez voir une nouvelle section **Choisir la méthode de connexion.**

1. Dans la **méthode Choisir la connexion,** cochez la case par **défaut,** puis sélectionnez **Enregistrer les modifications** à nouveau.

1. Une fois la page actualisée, vous pouvez voir une autre nouvelle section consentement de **l’administrateur & informations supplémentaires.**
    1. Sélectionnez **Fournir le lien Consentement de** l’administrateur, entrez Microsoft 365 informations d’identification de l’administrateur général, puis acceptez d’accorder les autorisations. 
    1. En de côté du **Azure AD client,** sélectionnez **le bouton** Détecter.
    1. En plus de **l OneDrive Entreprise URL,** sélectionnez **le bouton** Détecter.
    1. Une fois les champs remplis, sélectionnez de nouveau le bouton Enregistrer **les modifications.**

1. Sélectionnez le **bouton** Mettre à jour pour vérifier l’installation, puis **sélectionnez Enregistrer les modifications.**

1. Synchronisez les utilisateurs entre votre serveur Et votre Azure AD. Pour commencer :

    > [!NOTE]
    > En fonction de votre environnement, vous pouvez sélectionner différentes options au cours de cette étape.

1. Synchronisez les utilisateurs entre votre serveur Et votre Azure AD. En fonction de votre environnement, vous pouvez sélectionner différentes options au cours de cette étape. Pour commencer :
    1. Basculez vers **l’onglet Paramètres synchronisation.**

    1. Dans la section **Synchroniser les utilisateurs Azure AD,** cochez les case qui s’appliquent à votre environnement. Vous devez sélectionner ce qui suit :  

        ✔ créer des comptes dans Le Chatin pour les utilisateurs Azure AD.

        ✔ mettre à jour tous les comptes dans Le Chatin pour les utilisateurs Azure AD.

    1. Dans la section **Restriction de création** d’utilisateur, vous pouvez configurer un filtre pour limiter le nombre Azure AD utilisateurs synchronisés avec Lele.
    1. La section **Mappage des** champs utilisateur vous permet de personnaliser l’Azure AD mappage de champ Profil utilisateur De façon à ce qu’il soit plus simple de le faire.
    1. Dans la section **Teams** sync, vous pouvez choisir de créer automatiquement des groupes, tels que des équipes pour une partie ou l’ensemble, de vos cours Ententaux existants.

13. Pour valider [les travaux cron](https://docs.moodle.org/310/en/Cron) et les exécuter manuellement pour la première utilisation, sélectionnez le lien de **la page** Gestion des tâches programmées dans la section Synchroniser les utilisateurs **avec Azure AD.** Vous êtes alors sur la page **Tâches programmées.**

    1. Faites défiler vers le bas et recherchez les **utilisateurs** de synchronisation Azure AD travail et sélectionnez **Exécuter maintenant.**
    1. Si vous choisissez de créer des groupes en fonction des cours existants, vous pouvez également exécuter le travail Créer des groupes d’utilisateurs **Microsoft 365** travail.

    > [!NOTE]
    >
    > Le [Cron](https://docs.moodle.org/310/en/Cron) DeNte s’exécute en fonction de la planification des tâches. La planification par défaut est une fois par jour. Toutefois, le cron doit s’exécuter plus fréquemment pour que tout reste synchronisé.

1. Revenir à la page d’administration des plug-ins, administration > **sites > Microsoft 365'intégration,** puis sélectionnez la page **Teams Paramètres** page.

1. Dans la page **Teams Paramètres,** configurez les paramètres requis pour activer l’intégration Teams’application.

    1. Pour activer **OpenID Connecter,** sélectionnez le lien Gérer l’authentification, puis sélectionnez l’icône d’œil sur la ligne  **OpenId Connecter** si elle est grisée.
    1. Pour activer l’incorporation d’images, sélectionnez le lien **sécurité HTTP,** puis cochez la case en regard de l’incorporation **d’une image .**
    1. Pour activer les services web, qui activent  les fonctionnalités de l’API Contrôle d’accès, sélectionnez le lien Fonctionnalités avancées, puis assurez-vous que la case à cocher en regard de Activer les **services web** est activée.
    1. Pour activer les services externes pour Microsoft 365, sélectionnez le lien **Services** externes, puis :  

        ✔ **sélectionnez Modifier** sur la **ligne Microsoft 365 WebServices.**

        ✔ cochez la case en regard de **Activé,** puis sélectionnez **Enregistrer les modifications**

    1. Modifiez vos autorisations utilisateur authentifiées pour leur permettre de créer des jetons de service web.

        ✔ sélectionnez le lien utilisateur authentifié du rôle **d’édition.**

        ✔ faites défiler vers le bas et recherchez la fonctionnalité Créer un jeton **de service web** et cochez la **case** Autoriser.

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Déployer le bot Assistant Dentelé sur Azure

Le bot de l’Assistant Dente pour Microsoft Teams aide les enseignants et les étudiants à répondre à des questions sur leurs cours, devoirs, notes et autres informations dans Le jeu. Le bot envoie également des notifications à l’adresse d’étudiants et d’enseignants Teams. Le bot est un projet open source tenu à jour par Microsoft et est disponible [sur GitHub](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
>
> * Déployez des ressources dans votre abonnement Azure. Toutes les ressources ont été configurées à l’aide **du niveau** libre. Selon l’utilisation de votre bot, vous de devez peut-être mettre à l’échelle ces ressources.
>
> * Pour utiliser l’ongletUlation sans le bot, passez à [4](#4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flux d’informations sur le bot de chatouillement

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Pour installer le bot, vous devez l’inscrire sur la [plateforme d’identités Microsoft.](https://identity.microsoft.com/Landing) Cela permet à votre bot de s’authentifier sur vos points de terminaison Microsoft. 

**Pour inscrire votre bot**

1. Go to the plugins administration page, and then select **Plugins**. Sous **Microsoft 365'intégration,** sélectionnez **Teams Paramètres’onglet.**

1. Sélectionnez le **lien Portail d’inscription des** applications Microsoft et connectez-vous avec votre ID Microsoft.

1. Entrez un nom pour votre application, tel que SondèleBot, puis sélectionnez **le bouton** Créer.

1. Copiez **l’ID d’application** et collez-le dans le champ **ID de l’application** bot sur la page **Paramètres** équipe.

1. Sélectionnez le **bouton Générer un nouveau mot de** passe. Copiez le mot de passe généré et collez-le dans le champ Mot de passe de **l’application** bot sur la page **Paramètres** équipe.

1. Faites défiler jusqu’au bas du formulaire et sélectionnez **Enregistrer les modifications.**

Après avoir généré votre ID d’application et votre mot de passe, déployez votre bot sur Azure :

> [!div class="checklist"]
> * Sélectionnez Déployer sur **Azure** et complétez le formulaire avec les informations nécessaires, telles que l’ID de l’application bot, le mot de passe de l’application bot et le secret de la Teams Paramètres **page.** Les informations Azure se trouve sur la page **d’installation.** 
> * Une fois le formulaire terminé, cochez la case pour accepter les conditions générales.
> * Sélectionnez **Acheter.** Toutes les ressources Azure sont déployées sur le niveau gratuit.

Une fois le déploiement des ressources terminé sur Azure, vous devez configurer les plug-ins Microsoft 365 Leindent avec un point de terminaison de messagerie. Vous devez obtenir le point de terminaison à partir de votre bot dans Azure :

1. Connectez-vous au [portail Azure](https://portal.azure.com).

1. Dans le volet gauche, sélectionnez les groupes de ressources et sélectionnez le groupe de ressources que vous avez utilisé ou créé lors du déploiement de votre bot. 

1. Sélectionnez **la ressource Bot WebApp** dans la liste des ressources du groupe.

1. Copiez **le point de terminaison de messagerie à** partir de la section Vue **d’ensemble.**

1. Dans Le chat, ouvrez la page **d Paramètres** d’équipe de Microsoft 365 plug-ins Enfichables Enfichables.

1. Dans le **champ Point de terminaison du bot,** collez l’URL que vous avez copiée et modifiez le *mot messages* en *webhook.* L’URL doit apparaître comme suit : `https://botname.azurewebsites.net/api/webhook`

1. Sélectionnez **Enregistrer les modifications**.

1. Après avoir enregistrer les modifications, revenir à l’onglet **Paramètres** d’équipe, sélectionnez le bouton Télécharger le fichier manifeste, puis enregistrez le package de manifeste de l’application sur votre ordinateur pour une utilisation supplémentaire. 

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Déployer votre application Microsoft Teams de messagerie

Une fois que votre bot a été déployé sur Azure et configuré pour parler à votre serveur Dente, vous devez déployer votre application Microsoft Teams web. Pour ce faire, vous devez charger le fichier manifeste de l’application que vous avez téléchargé à partir de la page Microsoft 365 La page d’équipe Plug-ins Enfichables Enfichables Paramètres l’étape précédente.

Avant d’installer l’application, vous devez veiller à activer les applications externes et à télécharger des applications. Pour plus d’informations, [voir Préparer Microsoft 365 client.](../concepts/build-and-test/prepare-your-o365-tenant.md) 

**Pour déployer votre application** 

1. Ouvrez **Microsoft Teams**. 

1. Sélectionnez **l’icône** Application dans la zone inférieure gauche de la barre de navigation.

1. Sélectionnez le **Télécharger un lien d’application** personnalisé dans la liste des options.

   > [!NOTE]
   > Si vous êtes connecté en tant qu’administrateur général, vous devez avoir la possibilité de télécharger l’application dans le catalogue d’applications de votre organisation, sinon vous ne pouvez charger l’application que pour une équipe dont vous êtes membre.

4. Sélectionnez `manifest.zip` le package que vous avez téléchargé précédemment et sélectionnez **Enregistrer.** Si vous n’avez pas téléchargé le package de manifeste de l’application, vous pouvez le télécharger à partir de l’onglet **Paramètres** d’équipe de la page de configuration des plug-ins dans Lele.

Maintenant que l’application est installée, vous pouvez ajouter l’onglet à n’importe quel canal à qui vous avez accès. Pour ce faire, accédez au canal, sélectionnez le **symbole plus** (➕) et sélectionnez votre application dans la liste. Suivez les invites pour terminer l’ajout de l’onglet de cours DeNte à un canal.

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Autoriser la création automatique d’onglets Dentelé dans Microsoft Teams

Bien que les onglets Dentelé soient créés manuellement dans Microsoft Teams, vous pouvez décider de les créer automatiquement lorsque des équipes sont créées à partir de la synchronisation de cours. Pour ce faire, vous devez configurer l’ID de l’application Microsoft Teams téléchargée dans Le chat.

**Pour autoriser la création automatique d’onglets Dentelé**

1. Ouvrir Microsoft Teams.

1. Sélectionnez l’icône Applications dans la zone inférieure gauche de la barre de navigation.

1. Recherchez l’application **Dentier** téléchargée > sélectionnez **l’icône d’options** > sélectionner le lien **copier.**

1. Dans un éditeur de texte, collez le contenu copié. Il doit contenir une URL telle que ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff. Copiez la dernière partie de l’URL, par exemple, qui est l’ID de `00112233-4455-6677-8899-aabbccddeeff` l’Microsoft Teams’application.

1. Dans L’espace de commentaires, ouvrez **l Teams a tabulation de l’application Enfichables à** partir de Microsoft 365 page de configuration des plug-ins Enfichables Enfichables.

1. Collez l’ID de l’Microsoft Teams dans le champ D’ID de l’application Dente, puis enregistrez les modifications.

Lors de la synchronisation d’un cours DNS, Microsoft Teams installe automatiquement l’application Dente dans l’équipe, crée un onglet Dentelé dans le canal Général de Teams et le configure pour qu’il contienne la page de cours pour le cours À partir duquel il est synchronisé. Vous pouvez maintenant commencer à utiliser vos cours De la part de Microsoft Teams.

> [!NOTE]
> Pour partager des demandes de fonctionnalités ou des commentaires avec nous, visitez notre [page User Voice.](https://microsoftteams.uservoice.com/forums/916759-moodle)

## <a name="see-also"></a>Voir aussi

- [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
- [Moodle](https://moodle.org/)
- [Documentation en toute fin](https://docs.moodle.org/34/en/Installing_plugins)de vie.
