---
title: Installer Moodle LMS
description: Dans cet article, vous allez découvrir comment installer et configurer l’application d’intégration Moodle pour Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 0c19d8bc4e3919fe49f6594c8ec738bafc1c76d3
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189634"
---
# <a name="install-moodle-lms"></a>Installer Moodle LMS

Dans cet article, vous allez apprendre à installer moodle LMS.

> [!NOTE]
> Pour aider les administrateurs informatiques à configurer facilement l’intégration Moodle et Teams, les plug-ins moodle Microsoft 365 open source sont mis à jour pour les éléments suivants :
>
> * Inscription automatique de votre serveur Moodle avec [Microsoft Azure Active Directory (Azure AD).](https://azure.microsoft.com/services/active-directory/)
>
> * Déploiement en un clic de votre bot Moodle Assistant sur Azure.
>
> * Provisionnement automatique des équipes et synchronisation automatique des inscriptions d’équipe pour tous ou sélection des cours Moodle.
>
> * Installation automatique de l’onglet Moodle et du bot Assistant Moodle dans chaque équipe synchronisée.
>
> Pour en savoir plus sur les fonctionnalités fournies par cette intégration, consultez [Microsoft Teams et Moodle](https://education.microsoft.com/resource/3dffb3a8).

## <a name="prerequisites"></a>Configuration requise

Voici les conditions préalables à l’installation de Moodle :

* Informations d’identification de l’administrateur Moodle.

* Informations d’identification de l’administrateur Azure AD.

* Un abonnement Azure dans lequel vous pouvez créer des ressources.

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Installer les plug-ins moodle Microsoft 365

L’intégration moodle dans Microsoft Teams est optimisée par le jeu de [plug-ins moodle Microsoft 365 open source](https://github.com/Microsoft/o365-moodle).

### <a name="requisite-applications-and-plugins"></a>Applications et plug-ins requis

Veillez à installer et télécharger les éléments suivants avant de poursuivre l’installation des plug-ins Microsoft 365 Moodle :

1. Veillez à installer une [version stable actuelle de Moodle](https://download.moodle.org/releases/latest/).

1. Téléchargez et enregistrez le [Connecter Moodle OpenID](https://moodle.org/plugins/auth_oidc) et les [plug-ins d’intégration Microsoft 365](https://moodle.org/plugins/local_o365) sur votre ordinateur local.

    > [!NOTE]
    > L’installation des plug-ins OpenID Connecter et Microsoft 365 Integration est requise pour l’intégration Teams.
    >
    > En outre, les [plug-ins thème Microsoft 365 Teams](https://moodle.org/plugins/theme_boost_o365teams) sont fortement recommandés.

### <a name="microsoft-365-moodle-plugins"></a>plug-ins Microsoft 365 Moodle

1. Connectez-vous à votre serveur Moodle en tant qu’administrateur et sélectionnez **Administration du site** dans le [bloc Paramètres](https://docs.moodle.org/22/en/Settings_block) situé dans le panneau de navigation gauche.

1. Sélectionnez l’onglet **Plug-ins** , puis **installez les plug-ins**.

1. Dans la section **Installer les plug-ins de la section Fichier ZIP** , **sélectionnez Choisir un fichier**.

1. Sélectionnez **Télécharger une** option de fichier dans le volet de navigation gauche, recherchez le fichier que vous avez téléchargé, puis sélectionnez **Télécharger ce fichier**.

1. Sélectionnez **Administration du site** dans le volet de navigation gauche pour revenir à votre tableau de bord d’administration. Faites défiler jusqu’aux **plug-ins locaux** et sélectionnez le lien **d’intégration Microsoft 365**.

    > [!IMPORTANT]
    >
    > * Laissez votre Microsoft 365 page de configuration des plug-ins Moodle ouverte dans un onglet de navigateur distinct, car vous devez revenir à cet ensemble de pages tout au long du processus.  
    >
    > * Si vous n’avez pas de site Moodle existant, accédez au référentiel [Moodle sur Azure](https://github.com/azure/moodle) , déployez rapidement une instance Moodle et personnalisez-la en fonction de vos besoins.

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-ad"></a>2. Configurer la connexion entre les plug-ins Microsoft 365 et Azure AD

Vous devez configurer la connexion entre les plug-ins Microsoft 365 et Azure AD.

### <a name="requisites"></a>Accessoires

Inscrivez Moodle en tant qu’application dans Azure AD à l’aide du script PowerShell. Le script provisionne les éléments suivants :

* Nouvelle application Azure AD pour votre locataire Microsoft 365, qui est utilisée par les plug-ins moodle Microsoft 365.
* L’application de votre locataire Microsoft 365, configurez les URL de réponse et les autorisations requises pour l’application approvisionnée, puis retourne le `AppID` et `Key`.

Utilisez la page de configuration des plug-ins Moodle générée `AppID` et `Key` dans votre Microsoft 365 pour configurer votre site serveur Moodle avec Azure AD.

> [!IMPORTANT]
>
> * Le script PowerShell n’est pas mis à jour avec les derniers éléments de configuration. Par conséquent, vous devez effectuer la configuration manuellement en suivant les étapes décrites dans les pages de publication Moodle [3.8.0.4 et 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) et [3.8.0.5 et 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) .
>
> * Pour plus d’informations sur l’inscription manuelle de votre instance Moodle, consultez [Inscrire votre instance Moodle en tant qu’application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Onglet Moodle pour Microsoft Teams flux d’informations

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. Dans la page des plug-ins d’intégration Microsoft 365, sélectionnez l’onglet **Configuration**.

1. Sélectionnez le bouton **Télécharger le script PowerShell** et enregistrez-le sous forme de dossier ZIP sur votre ordinateur local.

1. Préparez le script PowerShell à partir du fichier ZIP comme suit :

    1. Téléchargez et extrayez le `Moodle-AzureAD-Powershell.zip` fichier.
    1. Ouvrez le dossier extrait.
    1. Cliquez avec le bouton droit sur le `Moodle-AzureAD-Script.ps1` fichier et sélectionnez **Propriétés**.
    1. Sous l’onglet **Général** de l’Fenêtre Propriétés, cochez la `Unblock` case en regard de l’attribut **Sécurité** situé en bas de la fenêtre.
    1. Sélectionnez **OK**.
    1. Copiez le chemin d’accès au répertoire dans le dossier extrait.

1. Exécutez PowerShell en tant qu’administrateur :

    1. Sélectionnez Démarrer.
    1. Tapez PowerShell.
    1. Cliquez avec le bouton droit sur **Windows PowerShell**.
    1. Sélectionnez **Exécuter en tant qu’administrateur**.

1. Accédez au répertoire décompressé en tapant `cd .../.../Moodle-AzureAD-Powershell` où `.../...` se trouve le chemin d’accès au répertoire.

1. Exécutez le script PowerShell :

    1. Entrez `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.
    1. Entrez `./Moodle-AzureAD-Script.ps1`.
    1. Connectez-vous à votre compte d’administrateur Microsoft 365 dans la fenêtre contextuelle.
    1. Entrez le nom de l’application Azure AD, par exemple, les plug-ins Moodle ou Moodle.
    1. Entrez l’URL de votre serveur Moodle.
    1. Copiez **l’ID d’application (`AppID`)** et la **clé d’application(`Key`)** générés par le script et enregistrez-les.

1. Ensuite, vous devez ajouter les `AppID` plug-ins `Key` Moodle Microsoft 365. Revenez à la page d’administration des plug-ins, Administration du site > Plug-ins > Microsoft 365 Intégration.

1. Sous l’onglet **Installation** , ajoutez les `AppID` éléments que `Key` vous avez copiés précédemment, puis **sélectionnez Enregistrer les modifications**. Une fois la page actualisée, vous pouvez voir une nouvelle section **Choisir la méthode de connexion**.

1. Dans la **méthode Choisir la connexion**, cochez la case intitulée **Par défaut**, puis réélectionnez **Enregistrer les modifications** .

1. Une fois la page actualisée, vous pouvez voir une autre nouvelle section **Administration consentement & des informations supplémentaires**.
    1. Sélectionnez **Fournir Administration lien De consentement**, entrez vos informations d’identification d’administrateur général Microsoft 365, puis **Acceptez** d’accorder les autorisations.
    1. En regard du champ **Locataire Azure AD** , sélectionnez le bouton **Détecter** .
    1. En regard de **l’URL OneDrive Entreprise**, sélectionnez le bouton **Détecter**.
    1. Une fois les champs renseignés, sélectionnez à nouveau le bouton **Enregistrer les modifications** .

1. Sélectionnez le bouton **Mettre à jour** pour vérifier l’installation, puis **sélectionnez Enregistrer les modifications**.

1. Synchronisez les utilisateurs entre votre serveur Moodle et Azure AD. Pour commencer :

    > [!NOTE]
    > En fonction de votre environnement, vous pouvez sélectionner différentes options au cours de cette étape.

1. Synchronisez les utilisateurs entre votre serveur Moodle et Azure AD. En fonction de votre environnement, vous pouvez sélectionner différentes options au cours de cette étape. Pour commencer :
    1. Basculez vers **l’onglet Synchroniser Paramètres**.

    1. Dans la section **Synchroniser les utilisateurs avec Azure AD** , cochez les cases qui s’appliquent à votre environnement. Vous devez sélectionner les éléments suivants :  

        ✔ Créez des comptes dans Moodle pour les utilisateurs dans Azure AD.

        ✔ Mettez à jour tous les comptes dans Moodle pour les utilisateurs dans Azure AD.

    1. Dans la section **Restriction de création d’utilisateurs** , vous pouvez configurer un filtre pour limiter les utilisateurs Azure AD synchronisés avec Moodle.
    1. La section **Mappage des champs** utilisateur vous permet de personnaliser le mappage des champs Profil utilisateur Azure AD vers Moodle.
    1. Dans la section **Teams Synchronisation**, vous pouvez choisir de créer automatiquement des groupes, tels que des équipes pour une partie ou la totalité de vos cours Moodle existants.

13. Pour valider les travaux [cron](https://docs.moodle.org/310/en/Cron) et les exécuter manuellement pour la première exécution, sélectionnez le lien de **la page de gestion des tâches planifiées** dans la section **Synchroniser les utilisateurs avec Azure AD** . Vous accédez alors à la page **Tâches planifiées** .

    1. Faites défiler vers le bas et recherchez **les utilisateurs de synchronisation avec la tâche Azure AD** , puis sélectionnez **Exécuter maintenant**.
    1. Si vous choisissez de créer des groupes en fonction des cours existants, vous pouvez également exécuter les **groupes d’utilisateurs dans Microsoft 365** travail.

    > [!NOTE]
    >
    > Moodle [Cron](https://docs.moodle.org/310/en/Cron) s’exécute selon la planification des tâches. La planification par défaut est une fois par jour. Toutefois, le cron doit s’exécuter plus fréquemment pour que tout reste synchronisé.

1. Revenez à la page d’administration des plug-ins, **à l’administration du site > aux plug-ins > Microsoft 365 à l’intégration**, puis sélectionnez la page **Teams Paramètres**.

1. Dans la page **Teams Paramètres**, configurez les paramètres requis pour activer l’intégration de l’application Teams.

    1. Pour activer **OpenID Connecter**, sélectionnez le lien **Gérer l’authentification**, puis sélectionnez l’icône d’œil sur la ligne **Connecter OpenId** si elle n’est pas disponible.
    1. Pour activer l’incorporation d’images, sélectionnez le lien **Sécurité HTTP**, puis cochez la case en regard d’Autoriser l’incorporation d’images.
    1. Pour activer les services web, qui activent les fonctionnalités de l’API Moodle, sélectionnez le lien **Fonctionnalités avancées** , puis vérifiez que la case à cocher en regard **d’Activer les services web** est sélectionnée.
    1. Pour activer les services externes pour Microsoft 365, sélectionnez le lien **Services externes**, puis :  

        ✔ Sélectionnez **Modifier** sur la ligne **Moodle Microsoft 365 Webservices**.

        ✔ Cochez la case en regard de **Activé**, puis **sélectionnez Enregistrer les modifications**

    1. Modifiez vos autorisations utilisateur authentifiées pour leur permettre de créer des jetons de service web.

        ✔ Sélectionnez le **lien Utilisateur authentifié du rôle d’édition** .

        ✔ Faites défiler vers le bas et **recherchez la fonctionnalité Créer un jeton de service web** , puis cochez la case **Autoriser** .

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Déployer le bot Assistant Moodle sur Azure

Le bot d’assistant Moodle gratuit pour Microsoft Teams aide les enseignants et les étudiants à répondre à des questions sur leurs cours, devoirs, notes et autres informations dans Moodle. Le bot envoie également des notifications Moodle aux étudiants et aux enseignants dans Teams. Le bot est un projet open source géré par Microsoft et disponible sur [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
>
> * Déployez des ressources sur votre abonnement Azure. Toutes les ressources ont été configurées à l’aide du niveau **gratuit** . Selon l’utilisation de votre bot, vous devrez peut-être mettre à l’échelle ces ressources.
>
> * Pour utiliser l’onglet Moodle sans le bot, passez à [4](#4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flux d’informations sur le bot Moodle

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Pour installer le bot, vous devez l’inscrire sur la [plateforme d’identités Microsoft](https://identity.microsoft.com/Landing). Cela permet à votre bot de s’authentifier auprès de vos points de terminaison Microsoft.

Pour inscrire votre bot :

1. Accédez à la page d’administration des plug-ins, puis sélectionnez **Plug-ins**. Sous **Microsoft 365 Intégration**, sélectionnez l’onglet **Teams Paramètres**.

1. Sélectionnez le lien **Portail d’inscription d’applications Microsoft** et connectez-vous avec votre ID Microsoft.

1. Entrez un nom pour votre application, par exemple MoodleBot, puis sélectionnez le bouton **Créer** .

1. Copiez **l’ID d’application** et collez-le dans le champ **Bot Application ID** de la page **Team Paramètres**.

1. Sélectionnez le bouton **Générer un nouveau mot de passe** . Copiez le mot de passe généré et collez-le dans le champ **Mot de passe de l’application** bot sur la page **Team Paramètres**.

1. Faites défiler jusqu’au bas du formulaire et **sélectionnez Enregistrer les modifications**.

Après avoir généré votre ID d’application et votre mot de passe, déployez votre bot sur Azure :

> [!div class="checklist"]
>
> * Sélectionnez **Déployer sur Azure** et remplissez le formulaire avec les informations nécessaires, telles que l’ID d’application bot, le mot de passe de l’application bot et le secret Moodle sur la page **Teams Paramètres**. Les informations Azure se trouve dans la page **d’installation** .
> * Une fois le formulaire rempli, cochez la case pour accepter les conditions générales.
> * Sélectionnez **Acheter**. Toutes les ressources Azure sont déployées sur le niveau gratuit.

Une fois le déploiement des ressources terminé sur Azure, vous devez configurer les plug-ins moodle Microsoft 365 avec un point de terminaison de messagerie. Vous devez obtenir le point de terminaison à partir de votre bot dans Azure :

1. Connectez-vous au [portail Microsoft Azure](https://portal.azure.com).

1. Dans le volet gauche, sélectionnez **Groupes de ressources** , puis sélectionnez le groupe de ressources que vous avez utilisé ou créé, lors du déploiement de votre bot.

1. Sélectionnez la ressource **WebApp Bot** dans la liste des ressources du groupe.

1. Copiez le point **de terminaison de messagerie** à partir de la section **Vue d’ensemble** .

1. Dans Moodle, ouvrez la page **Team Paramètres** de vos plug-ins Moodle Microsoft 365.

1. Dans le champ **Bot Endpoint** , collez l’URL que vous avez copiée et remplacez les *messages* word par *webhook*. L’URL doit apparaître comme suit : `https://botname.azurewebsites.net/api/webhook`

1. Sélectionnez **Enregistrer les modifications**.

1. Après avoir enregistré les modifications, revenez à l’onglet **Équipe Paramètres**, **sélectionnez le bouton Télécharger le fichier manifeste** et enregistrez le package de manifeste d’application sur votre ordinateur pour une utilisation ultérieure.

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Déployer votre application Microsoft Teams

Une fois votre bot déployé sur Azure et configuré pour communiquer avec votre serveur Moodle, vous devez déployer votre application Microsoft Teams. Pour ce faire, vous devez charger le fichier manifeste de l’application que vous avez téléchargé à partir de la page Paramètres Microsoft 365 Moodle Plugins Team à l’étape précédente.

Avant d’installer l’application, vous devez vous assurer d’activer les applications externes et le chargement des applications. Pour plus d’informations, consultez [Préparer votre locataire Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md).

Pour déployer votre application :

1. Ouvrez **Microsoft Teams**.

1. Sélectionnez **l’icône Application** dans la zone inférieure gauche de la barre de navigation.

1. Sélectionnez le **Télécharger un lien d’application personnalisée** dans la liste des options.

   > [!NOTE]
   > Si vous êtes connecté en tant qu’administrateur général, vous devez avoir la possibilité de charger l’application dans le catalogue d’applications de votre organisation. Sinon, vous ne pouvez charger l’application que pour une équipe dans laquelle vous êtes membre.

4. Sélectionnez le `manifest.zip` package que vous avez téléchargé précédemment, puis **sélectionnez Enregistrer**. Si vous n’avez pas téléchargé le package de manifeste d’application, vous pouvez télécharger à partir de l’onglet **Team Paramètres** de la page de configuration des plug-ins dans Moodle.

Maintenant que vous avez installé l’application, vous pouvez ajouter l’onglet à n’importe quel canal auquel vous avez accès. Pour ce faire, accédez au canal, sélectionnez le symbole **plus** (➕) et sélectionnez votre application dans la liste. Suivez les invites pour terminer l’ajout de votre onglet de cours Moodle à un canal.

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Autoriser la création automatique d’onglets Moodle dans Microsoft Teams

Bien que les onglets Moodle soient créés manuellement dans Microsoft Teams, vous pouvez décider de les créer automatiquement lorsque des équipes sont créées à partir de la synchronisation de cours. Pour ce faire, vous devez configurer l’ID de l’application Microsoft Teams chargée dans Moodle.

Pour autoriser la création automatique d’onglets Moodle :

1. Ouvrir Microsoft Teams.

1. Sélectionnez l’icône Applications dans le volet inférieur gauche.

1. Recherchez **l’application Moodle** chargée > sélectionnez l’icône **d’options** > sélectionner **le lien copier**.

1. Dans un éditeur de texte, collez le contenu copié. Il doit contenir une URL telle que `https://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff`. Copiez la dernière partie de l’URL, par `00112233-4455-6677-8899-aabbccddeeff`exemple, qui est l’ID de l’application Microsoft Teams.

1. Dans Moodle, ouvrez l’onglet **Teams’application Moodle** à partir de votre page de configuration Microsoft 365 plug-ins Moodle.

1. Collez l’ID de l’application Microsoft Teams dans le champ ID de l’application Moodle, puis enregistrez les modifications.

Lorsqu’un cours Moodle est synchronisé, Teams installe automatiquement l’application Moodle dans l’équipe, crée un onglet Moodle dans le canal Général de Teams et la configure pour contenir la page de cours du cours Moodle à partir duquel il est synchronisé. Vous pouvez maintenant commencer à utiliser vos cours Moodle directement à partir de Teams.

> [!NOTE]
> Pour partager des demandes de fonctionnalités ou des commentaires avec nous, visitez notre [page User Voice](https://support.microsoft.com/en-us/office/uservoice-pages-430e1a78-e016-472a-a10f-dc2a3df3450a).

## <a name="see-also"></a>Voir aussi

* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
* [Moodle](https://moodle.org/)
* [Documentation Moodle](https://docs.moodle.org/34/en/Installing_plugins).
