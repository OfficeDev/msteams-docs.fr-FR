---
title: Installation de l’intégration de Moodle avec Microsoft teams
description: Procédure d’installation et de configuration de l’application d’intégration Moodle pour Microsoft teams
keywords: Plug-in teams Moodle d’intégration des applications
ms.date: 01/31/2019
ms.openlocfilehash: 012d6e9c979386e892b5a47b7655208eca95e11a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673509"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a>Installation de l’intégration de Moodle avec Microsoft teams

> [!VIDEO https://www.youtube.com/embed/OHlPt22nKoE]

[Moodle](https://moodle.org/), le système de gestion des formations Open source le plus populaire et ouvert dans le monde entier, est désormais intégré à Microsoft teams ! Cette intégration permet aux enseignants et aux enseignants de collaborer sur des cours Moodle, de poser des questions sur leurs notes et leurs devoirs et de rester informés des notifications--directement dans Teams.

Pour aider les administrateurs informatiques à configurer facilement cette intégration, nous avons mis à jour notre plug-in Moodle Open source Office 365 avec les fonctionnalités suivantes :

* Enregistrement automatique de votre serveur Moodle avec Azure AD.
* Déploiement en un clic de votre bot Assistant Moodle vers Azure.
* Mise en service automatique de teams et synchronisation automatique des inscriptions d’équipe pour tous les cours Moodle ou Select.
* Installation automatique de l’onglet Moodle et du bot Assistant Moodle dans chaque équipe synchronisée. (Bientôt disponible)
* Publication en un clic de l’application Moodle dans le magasin d’applications de teams privées. (Bientôt disponible)

Pour en savoir plus sur les fonctionnalités de cette intégration, cliquez [ici](https://education.microsoft.com/courses-and-resources/resources/microsoft-teams-moodle).

## <a name="prerequisites"></a>Conditions préalables

Pour installer et configurer cette application, vous avez besoin des éléments suivants :

1. Informations d’identification d’administrateur moodle
2. Informations d’identification de l’administrateur Azure AD
3. Un abonnement Azure auquel vous pouvez créer des ressources

## <a name="step-1-install-the-office-365-moodle-plugin"></a>Étape 1 : installer le plug-in Office 365 moodle

> [!VIDEO https://www.youtube.com/embed/SETEC5nzMgk]

L’intégration de Moodle dans Microsoft teams est gérée par l' [ensemble de plug-ins Moodle Office 365](https://github.com/Microsoft/o365-moodle)Open source. Pour installer le plug-in dans votre serveur Moodle :

1. Tout d’abord, téléchargez le [jeu de plug-ins Office 365](https://moodle.org/plugins/pluginversions.php?plugin=local_o365) et enregistrez-le sur votre ordinateur local. Vous devez utiliser la version 3,5 ou une version ultérieure.
    * L’installation du plug-in local_o365 installera également les plug-ins [auth_oidc](https://moodle.org/plugins/auth_oidc) et [boost_o365Teams](https://moodle.org/plugins/pluginversions.php?plugin=theme_boost_o365teams) .
1. Connectez-vous à votre serveur Moodle en tant qu’administrateur, puis sélectionnez **administration du site** dans le volet de navigation gauche.
1. Sélectionnez l’onglet **plugins** , puis cliquez sur **installer les plugins**.
1. Sous la section **installer le plug-in à partir du fichier zip** , cliquez sur le bouton **choisir un fichier** .
1. Sélectionnez les options **charger un fichier** dans le volet de navigation de gauche, recherchez le fichier que vous avez téléchargé ci-dessus, puis cliquez sur **Télécharger ce fichier**.
1. Sélectionnez l’option **administration de site** dans le volet de navigation gauche pour revenir à votre tableau de bord d’administration. Faites défiler vers le bas jusqu’aux **plugins locaux** et cliquez sur le lien **intégration de Microsoft Office 365** . Conservez cette page de configuration ouverte dans un onglet de navigateur distinct, car vous l’utiliserez dans le reste de ce processus.

Vous trouverez plus d’informations sur l’installation des plug-ins Moodle dans la [documentation Moodle](https://docs.moodle.org/34/en/Installing_plugins).

**Remarque importante :** Conservez votre page de configuration du plug-in Office 365 Moodle ouverte dans un onglet de navigateur distinct, car vous revenez à cet ensemble de pages tout au long de ce processus.

*Vous n’avez pas encore de site Moodle ?* Vous pouvez consulter notre Moodle sur Azure [référentiel](https://github.com/azure/moodle) où vous pouvez rapidement déployer une instance Moodle sur Azure et la personnaliser en fonction de vos besoins.

## <a name="step-2-configure-the-connection-between-the-office-365-plugin-and-azure-active-directory"></a>Étape 2 : configuration de la connexion entre le plug-in Office 365 et Azure Active Directory

> [!VIDEO https://www.youtube.com/embed/FpGEezaJ3SA]

Ensuite, vous devez enregistrer Moodle en tant qu’application dans votre Azure Active Directory. Nous avons fourni un script PowerShell pour vous aider à effectuer ce processus. Le script PowerShell met en place une nouvelle application Azure AD pour votre client Office 365, qui sera utilisé par le plug-in Office 365 moodle. Le script mettra en service l’application pour votre client O365, configurez toutes les URL de réponse et les autorisations requises pour l’application approvisionnée et renvoyez l’AppID et la clé. Vous pouvez utiliser l’AppID et la clé générés dans votre page d’installation du plug-in Moodle O365 pour configurer votre serveur Moodle avec Azure AD. Si vous souhaitez voir les étapes manuelles détaillées que le script PowerShell automatise, vous pouvez les trouver dans la [documentation complète du plug-in](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).

### <a name="moodle-tab-for-microsoft-teams-information-flow"></a>Onglet Moodle pour le flux d’informations Microsoft teams

<img width="530px" src="~/assets/images/MoodleTabInformationFlow.png" title="Onglet Moodle pour le flux d’informations Microsoft teams" />

1. Dans la page plug-in d’intégration Microsoft Office 365, sélectionnez l’onglet **configuration** .
1. Cliquez sur le bouton **Télécharger le script PowerShell** et enregistrez-le sur votre ordinateur local.
1. Vous devez préparer le script PowerShell à partir du fichier ZIP. Pour ce faire, procédez comme suit :
    * Téléchargez et extrayez le `Moodle-AzureAD-Powershell.zip` fichier.
    * Ouvrez le dossier extrait.
    * Cliquez avec le bouton droit `Moodle-AzureAD-Script.ps1` sur le fichier et sélectionnez **Propriétés**.
    * Sous l’onglet **général** de la fenêtre Propriétés, activez la `Unblock` case à cocher en regard de l’attribut **sécurité** en bas.
    * Cliquez sur **OK**.
    * Copiez le chemin d’accès au répertoire du dossier extrait.
1. Ensuite, vous allez exécuter PowerShell en tant qu’administrateur :
    * Cliquez sur Démarrer.
    * Tapez PowerShell.
    * Cliquez avec le bouton droit sur Windows PowerShell.
    * Cliquez sur « Exécuter en tant qu’administrateur ».
1. Accédez au répertoire dézippé en tapant `cd ...\...\Moodle-AzureAD-Powershell` où `...\...` est le chemin d’accès au répertoire.
1. Exécutez le script PowerShell en procédant comme suit :
    * Entrée `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.
    * Entrée `.\Moodle-AzureAD-Script.ps1`.
    * Connectez-vous à votre compte d’administrateur Office 365 dans la fenêtre contextuelle.
    * Entrez le nom de l’application Azure AD (par exemple, Plug-in Moodle/Moodle).
    * Entrez l’URL de votre serveur moodle.
    * Copiez l' **ID d’application** et la clé d' **application** générés par le script et enregistrez-les.
1. Ensuite, vous devez ajouter l’ID et la clé au plug-in Office 365 moodle. Revenez à la page d’administration des plug-ins (administration du site > plugins > l’intégration de Microsoft Office 365).
1. Dans l’onglet **installation** , ajoutez l' **ID** de l’application et la clé de l' **application** que vous avez copiés précédemment, puis cliquez sur **enregistrer les modifications**.
1. Une fois la page actualisée, vous devriez voir une nouvelle section **Choose Connection Method**. Cliquez sur la case à cocher intitulée **par défaut** , puis cliquez à nouveau sur **enregistrer les modifications** .
1. Une fois que la page est actualisée, vous voyez s’afficher un autre accord d’administrateur pour la nouvelle section **& des informations supplémentaires**.
    * Cliquez sur le lien **fournir le consentement** de l’administrateur, entrez vos informations d’identification d’administrateur général office3 365, puis **acceptez** d’accorder les autorisations.
    * En regard du champ **client Azure ad** , cliquez sur le bouton **détecter** .
    * En regard de l' **URL de OneDrive entreprise** , cliquez sur le bouton **détecter** .
    * Une fois que les champs sont renseignés, cliquez à nouveau sur le bouton **enregistrer les modifications** .
1. Cliquez sur le bouton **mettre à jour** pour vérifier l’installation, puis **Enregistrez les modifications**.
1. Ensuite, vous devez synchroniser les utilisateurs entre votre serveur Moodle et Azure Active Directory. En fonction de votre environnement, vous pouvez sélectionner différentes options pendant cette étape. Notez que la configuration que vous définissez ici s’exécute avec chaque Moodle cron exécuté (généralement une fois par jour) pour maintenir tout le temps de synchronisation. Pour commencer, procédez comme suit :
    * Basculer vers l' **onglet Paramètres de synchronisation**
    * Dans la section **synchroniser les utilisateurs avec Azure ad** , sélectionnez les cases à cocher qui s’appliquent à votre environnement. En règle générale, vous devez sélectionner au moins :
        * Créer des comptes dans Moodle pour les utilisateurs dans Azure AD
        * Mettre à jour tous les comptes dans Moodle pour les utilisateurs d’Azure AD
    * Dans la section **restriction de création** de l’utilisateur, vous pouvez configurer un filtre pour limiter les utilisateurs Azure ad qui seront synchronisés avec moodle.
    * La section **mappage des champs utilisateur** vous permet de personnaliser le mappage de champs de profil utilisateur Azure ad vers moodle.
    * Dans la section **Sync teams** , vous pouvez choisir de créer automatiquement des groupes (Teams) pour certains ou tous les cours Moodle existants.
1. Pour valider les travaux cron (et les exécuter manuellement si vous le souhaitez pour la première exécution), cliquez sur le lien **page de gestion des tâches planifiées** dans la section **synchroniser les utilisateurs avec Azure ad** . Cette opération vous permet d’accéder à la page **tâches planifiées** .
    * Faites défiler la liste vers le bas et recherchez le travail **synchroniser les utilisateurs avec Azure ad** , puis cliquez sur **Exécuter maintenant**.
    * Si vous choisissez de créer des groupes basés sur des cours existants, vous pouvez également exécuter le travail **créer des groupes d’utilisateurs dans Office 365** .
1. Revenez à la page d’administration des plug-ins (administration du site > plugins > l’intégration de Microsoft Office 365) et sélectionnez la page **paramètres teams** . Vous devrez configurer certains paramètres de sécurité pour activer l’intégration des applications Teams.
    * Pour activer OpenID Connect, cliquez sur le lien **gérer l’authentification** , puis cliquez sur l’icône représentant un oeil sur la ligne de **connexion OpenID** si elle est grisée.
    * Ensuite, vous devez activer l’incorporation de cadres. Cliquez sur le lien de **sécurité http** , puis sur la case à cocher en regard de **autoriser l’incorporation de cadre**.
    * L’étape suivante consiste à activer les services Web qui activent les fonctionnalités de l’API moodle. Cliquez sur le lien **fonctionnalités avancées** , puis assurez-vous que la case à cocher en regard de **activer les services Web** est activée.
    * Enfin, vous devez activer les services externes pour Office 365. Cliquez sur le lien **services externes** , puis :
        * Cliquez sur **modifier** sur la ligne **Moodle Office 365 WebServices** .
        * Activez la case à cocher en regard de **activé**, puis cliquez sur **enregistrer les modifications** .
    * Ensuite, vous devez modifier vos autorisations d’utilisateur authentifié afin de les autoriser à créer des jetons de service Web. Cliquez sur le lien **« utilisateur authentifié » du rôle d’édition** . Faites défiler la liste vers le bas et recherchez la fonctionnalité **créer un jeton de service Web** et activez la case à cocher **autoriser** .

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a>Étape 3 : déployer le robot Assistant Moodle vers Azure

> [!VIDEO https://www.youtube.com/embed/gbkJxf8FlfY]

Le robot gratuit Moodle Assistant pour Microsoft teams aide les enseignants et les étudiants à répondre aux questions sur leurs cours, devoirs, notes et autres informations dans Moodle. Le bot envoie également des notifications Moodle aux étudiants et aux enseignants directement dans Teams. Ce robot est un projet open source géré par Microsoft et est [disponible sur GitHub](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
> Dans cette section, vous allez déployer des ressources dans votre abonnement Azure, et toutes les ressources seront configurées à l’aide de la couche **libre** . En fonction de l’utilisation de votre bot, il se peut que vous deviez mettre à l’ampleur ces ressources.
> Si vous souhaitez simplement utiliser l’onglet Moodle sans le bot, passez à l' [étape 4](#step-4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flux d’informations du robot moodle

<img width="530px" src="~/assets/images/MoodleBotInformationFlow.png" title="Moodle bot pour le flux d’informations Microsoft teams" />

Pour installer le robot, vous devez d’abord l’enregistrer sur la [plateforme d’identité Microsoft](https://identity.microsoft.com/Landing). Cela permet à votre bot de s’authentifier auprès de vos points de terminaison Microsoft. Pour enregistrer votre robot :

1. Revenez à la page d’administration des plug-ins (administration du site > plugins > l’intégration de Microsoft Office 365) et sélectionnez l’onglet **paramètres teams** .
1. Cliquez sur le lien **portail d’inscription de l’application Microsoft** et connectez-vous avec votre identifiant Microsoft.
1. Entrez un nom pour votre application (par exemple, MoodleBot), puis cliquez sur le bouton **créer** .
1. Copiez l' **ID d’application** et collez-le dans le champ ID de l' **application bot** de la page **paramètres d’équipe** .
1. Cliquez sur le bouton **générer un nouveau mot de passe** . Copiez le mot de passe généré et collez-le dans le champ **mot de passe de l’application bot** de la page **paramètres d’équipe** .
1. Faites défiler vers le bas du formulaire, puis cliquez sur **enregistrer les modifications**.

À présent que vous avez généré l’ID et le mot de passe de votre application, il est temps de déployer votre bot vers Azure. Cliquez sur le bouton **déployer sur Azure** et remplissez le formulaire avec les informations nécessaires (l’ID de l’application bot, le mot de passe de l’application bot et la clé secrète Moodle figurent sur la page des **paramètres d’équipe** , et les informations Azure se trouvent sur la page **d’installation** ). Une fois que le formulaire est rempli, cliquez sur la case à cocher pour accepter les termes et conditions, puis cliquez sur le bouton **acheter** (toutes les ressources Azure sont déployées vers la couche libre).

Une fois que les ressources ont terminé le déploiement vers Azure, vous devez configurer le plug-in Office 365 Moodle avec son point de terminaison de messagerie. Tout d’abord, vous devez obtenir le point de terminaison à partir de votre robot dans Azure. Pour cela :

1. Si ce n’est pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com).
2. Dans le volet gauche, sélectionnez **groupes de ressources**.
3. Dans la liste, sélectionnez le groupe de ressources que vous venez d’utiliser (ou créé) lors du déploiement de votre robot.
4. Sélectionnez la ressource **webapp bot** dans la liste des ressources du groupe.
5. Copiez le **point de terminaison de messagerie** à partir de la section **vue d’ensemble** .
6. Dans Moodle, ouvrez la page **paramètres d’équipe** de votre plug-in Office 365 moodle.
7. Dans le champ **point de terminaison de bot** , collez l’URL que vous venez de copier et modifiez les *messages* Word en *webhook*. L’URL doit maintenant ressembler à`https://botname.azurewebsites.net/api/webhook`
8. Cliquez sur **enregistrer les modifications** .
9. Une fois que vos modifications ont été enregistrées, revenez à l’onglet **paramètres d’équipe** , cliquez sur le bouton **Télécharger le fichier manifeste** et enregistrez le package de manifeste sur votre ordinateur (vous l’utiliserez dans la section suivante).

## <a name="step-4-deploy-your-microsoft-teams-app"></a>Étape 4 : déploiement de votre application Microsoft teams

> [!VIDEO https://www.youtube.com/embed/2rMb7gtM_ZM]

Maintenant que votre bot est déployé sur Azure et configuré pour communiquer avec votre serveur Moodle, il est temps de déployer votre application Microsoft Teams. Pour ce faire, chargez le fichier manifeste que vous avez téléchargé à partir de la page Paramètres d’équipe du plug-in Office 365 Moodle à l’étape précédente.

Avant de pouvoir installer l’application, vous devez vous assurer que les applications externes et le téléchargement d’applications sont activés. Pour ce faire, procédez comme [suit](https://docs.microsoft.com/microsoftteams/platform/get-started/get-started-tenant). Une fois que vous avez vérifié que les applications externes sont activées, vous pouvez suivre les étapes ci-dessous pour déployer votre application.

1. Ouvrez Microsoft Teams.
2. Cliquez sur l’icône de la **Boutique** située en bas à gauche de la barre de navigation.
3. Cliquez sur le lien **Télécharger une application personnalisée** dans la liste d’options. *Remarque :* Si vous êtes connecté en tant qu’administrateur global, vous aurez la possibilité de télécharger l’application dans le magasin d’applications de votre organisation, sinon vous pourrez uniquement charger l’application pour une équipe dont vous êtes membre.
4. Sélectionnez le `manifest.zip` package que vous avez téléchargé précédemment, puis cliquez sur **Enregistrer**. Si vous n’avez pas encore téléchargé le package de manifeste, vous pouvez le faire à partir de l’onglet **paramètres d’équipe** de la page Configuration du plug-in dans Moodle.

Maintenant que l’application est installée, vous pouvez ajouter l’onglet à n’importe quel canal auquel vous avez accès. Pour ce faire, accédez au canal, cliquez sur **+** le symbole et sélectionnez votre application dans la liste. Suivez les invites pour terminer l’ajout de votre onglet de cours Moodle à un canal.

Voilà ! Vous et votre équipe pouvez désormais commencer à travailler avec vos cours Moodle directement à partir de Microsoft Teams.

Pour partager des demandes de fonctionnalités ou des commentaires avec nous, consultez notre [page voix utilisateur](https://microsoftteams.uservoice.com/forums/916759-moodle).
