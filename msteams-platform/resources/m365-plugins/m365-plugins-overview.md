---
title: Plug-ins Microsoft 365
description: Dans cet article, vous aurez des plug-ins Microsoft 365, une liste de plug-ins et des étiquettes, Microsoft 365 et une interaction OneNote, etc.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: 56ba41598fb7d9e75aff92f240f7a3132988c1ec
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499306"
---
# <a name="microsoft-365-plugins"></a>Plug-ins Microsoft 365

Les plug-ins Microsoft 365 permettent une intégration entre le site web Moodle et Teams. Ces plug-ins simplifient la planification, la remise et la collaboration sur un contenu du cours par les utilisateurs. Les plug-ins peuvent être utilisés individuellement ou ensemble selon les besoins.

## <a name="plugin-list-and-labels"></a>Liste et étiquettes des plug-ins

Le tableau suivant répertorie les plug-ins et étiquettes GitHub à utiliser en fonction des besoins.

<!--Old content of the table updated and revamped |Plugins to install |Description |GitHub label(s)|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|Enable SSO for users who work using both Moodle and Microsoft Teams|auth_oidc|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) |Create Teams instances for each course in Moodle, and sync faculty as owners, and students as team members|• auth_oidc </br> • local_o365|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Teams Theme**](#microsoft-365-teams-theme)| Remove Moodle blocks and extra chrome within the Moodle iframes for Teams, which applies while mapping courses to Teams instances | • auth_oidc </br> • local_o365 </br> • themeboost_o365teams |
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Microsoft 365 Repository**](#microsoft-365-repository) |Leverage Microsoft 365 OneDrive content for file repositories to reduce storage needs in Moodle | • auth_oidc </br> * local_o365 </br> • repository_office 365|
|• [**OpenID Connect**](#openid-connect) </br> • [**OneNote**](#onenote-integration) </br> • [**OneNote Submissions**](#onenote-integration) </br> • [**OneNote Feedback**](#onenote-integration) | Enable OneNote to be used for assignment, submission and feedback |• auth_oidc </br> • local_onenote </br> • assignsubmission_onenote </br> • assignfeedback_onenote |  
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) • [**Microsoft 365 Repository**](#microsoft-365-repository) </br> • [**Microsoft Block**](#microsoft-365-repository) | Enable 365 quick access blocks within Moodle with links to Microsoft 365 collaboration services and install links for Microsoft Office | • auth_oidc </br> • local_o365 </br> • repository_office365 </br> • block_microsoft |
|[**Teams Meeting**](#teams-meetings) | Enable Atto editor in Moodle to create Teams meeting links |atto_teamsmeeting |
|[**oEmbed Filter**](#oembed-filter) | Enable video links in Moodle | Filter_oembed| -->

|Plug-ins à installer |Description |Étiquette(s) GitHub|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|Active l’authentification unique des utilisateurs qui travaillent en utilisant Moodle et Teams.|auth_oidc|
|[**Intégration de Microsoft 365**](#microsoft-365-integration)|Créez des instances Teams pour chaque cours dans Moddle et synchronisez les enseignants en tant que propriétaires et les étudiants en tant que membres de l’équipe.|local_o365|
|[**Référentiel Microsoft 365**](#microsoft-365-repository) |Prend en charge le contenu OneDrive Microsoft 365 pour les référentiels de fichiers afin de réduire les besoins en stockage dans Moodle.| repository_office 365|
|[**Réunions Teams**](#teams-meetings) |Autorise l’éditeur Atto dans Moodle pour créer des liens de réunion Teams.|atto_teamsmeeting |
|[**Thème Teams**](#microsoft-365-teams-theme)| Supprimez les blocs Moodle et le chrome supplémentaire dans les iFrames Moodle pour Teams, qui s’applique lors du mappage des cours aux instances Teams.| themeboost_o365teams |
|[**OneNote**](#onenote-integration)| Permettez l’utilisation de OneNote pour les devoirs, les soumissions et les commentaires.|local_onenote, assignsubmission_onenote et assignfeedback_onenote </br>|  
|[**Bloc Microsoft**](#microsoft-block) | Permet les blocs d’accès rapide Microsoft 365 au sein de Moodle avec des liens vers les services de collaboration Microsoft 365 et l’installation des liens pour Microsoft Office.|block_microsoft |
|[**Filtre oEmbed**](#oembed-filter) | Activez des liens vidéo dans Moodle.|Filter_oembed|

Le système de gestion des formations Moodle prend en charge les plug-ins suivants :

## <a name="openid-connect"></a>OpenID Connect

Le plug-in Connexion OpenID permet aux utilisateurs d’authentifier les sites web ou outils prenant en charge les spécifications nécessaires et fournit une prise en charge de l’authentification unique (SSO) avec Microsoft Office 365. Le plug-in Connexion OpenID fournit aux établissements les options de connexion suivantes pour répondre à leurs besoins spécifiques :

* Les utilisateurs peuvent entrer leurs informations d’identification Office 365, telles que l’adresse e-mail et le mot de passe, pour se connecter directement ou se connecter à l’aide des champs nom d’utilisateur et mot de passe de Moodle, sans connexion à Office 365.
* Les utilisateurs peuvent sélectionner le lien pour se connecter via Office 365 ou le fournisseur Connexion OpenID sur la page Moodle.

L’image suivante affiche la page de connexion Connexion OpenID :

:::image type="content" source="../../assets/images/MoodleInstructions/openid-connect.png" alt-text="Se connecter à Connexion OpenID":::

## <a name="microsoft-365-integration"></a>Intégration de Microsoft 365

L’intégration Microsoft 365 se compose de plusieurs applications avec de nombreuses fonctionnalités qui permettent aux utilisateurs de rester connectés et d’effectuer différentes actions selon les besoins. Le plug-in permet aux administrateurs de vérifier les éléments suivants :

* Consulter les fonctions d’intégration appropriées.
* Synchroniser les utilisateurs entre Office 365 et Moodle.
* Configurer les autorisations nécessaires pour les utilisateurs.
* Configurer un site web SharePoint pour les fichiers de cours.

L’image suivante affiche la page de configuration de l’intégration Microsoft 365 :

:::image type="content" source="../../assets/images/MoodleInstructions/365-integration.png" alt-text="Intégration de Microsoft 365":::

### <a name="user-functions"></a>Fonctions utilisateur

Les utilisateurs peuvent effectuer les actions suivantes avec l’intégration Microsoft 365 :

* Vérifier le fonctionnement global de toutes les intégrations du plug-in Microsoft 365.
* Télécharger un fichier CSV qui compare Moodle aux utilisateurs d’Office 365.
* Vérifier les configurations pour les autorisations Azure AD.

## <a name="microsoft-365-repository"></a>Référentiel Microsoft 365

Le plug-in du référentiel Microsoft 365 permet aux utilisateurs de stocker des fichiers de cours dans OneDrive. Les enseignants peuvent ajouter dans le référentiel des fichiers à partir de la section de fichier de cours de OneDrive ou de leur propre espace personnel.

Le référentiel Microsoft 365 permet à l’utilisateur de l’utiliser en tant que référentiel de fichier pour une institution tout en conservant la structure simple des données Moodle. Le plug-in du référentiel Microsoft 365 fournit les services suivants :

* Les enseignants peuvent stocker les fichiers de cours dans OneDrive. Chaque cours dispose de son propre dossier créé dans OneDrive, ce qui permet aux enseignants d’ajouter des fichiers à partir de la zone de fichiers du cours de OneDrive ou à partir de leur propre espace personnel.  
* Pour ajouter des fichiers dans Moodle en tant que copie ou créer un lien vers le fichier. Le fichier lié s’affiche dans une nouvelle fenêtre de l’application ou est incorporé dans la page web.
* Pour télécharger des fichiers vers OneDrive ou SharePoint à l’aide du sélecteur de fichier Moodle.

L’image suivante affiche le référentiel de fichiers Microsoft 365 :

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-365- repository.png" alt-text="Référentiel M365" :::

## <a name="teams-meetings"></a>Réunions Teams

Le plug-in de réunions Teams permet à l’utilisateur de créer des demandes de réunion dans le calendrier, des devoirs, des billets de forum, ainsi que dans l’éditeur Atto selon la disponibilité.

Une fois le plug-in installé, les enseignants et les étudiants peuvent créer une réunion audio ou vidéo à l’aide de Moodle, ce qui nécessite un compte Microsoft 365 et des autorisations Moodle.

>[!NOTE]
>Les réunions Teams n’apparaissent pas dans le calendrier Outlook ou Teams. Toutefois, des noms individuels d’étudiants peuvent être ajoutés à l’invitation pour la même raison.

L’image suivante affiche la page de connexion à une réunion Teams :

:::image type="content" source="../../assets/images/MoodleInstructions/teams-meeting.png" alt-text="Se connecter à une réunion Teams":::

## <a name="microsoft-365-teams-theme"></a>Thème Teams Microsoft 365

Le plug-in de thème Teams Microsoft 365 fournit aux utilisateurs un affichage personnalisé de la page d’accueil du cours Moodle et il est disponible pour l’affichage lorsque l’utilisateur accède à ses cours Moodle au sein de Teams.

Le plug-in de thème offre aux utilisateurs une expérience améliorée unifiée avec les fonctionnalités suivantes :

* S’adapte aux modifications apportées au Thème Microsoft Teams, tel que par défaut, mode sombre et contraste élevé.
* Met l’accent sur les activités du cours.
* Supprime les blocs, la navigation, l’en-tête et le pied de page Moodle.
* Fournit des éléments de l’interface utilisateur (IU) Microsoft Teams.

L’image suivante affiche le thème Teams configuré par l’utilisateur :

:::image type="content" source="../../assets/images/MoodleInstructions/teams-theme.png" alt-text="Thème Microsoft Teams":::

## <a name="onenote-integration"></a>Intégration OneNote

Le plug-in d’intégration OneNote fournit aux utilisateurs des options pour parcourir des blocs-notes, des sections et des pages; l’emplacement où les devoirs sont soumis et où les enseignants fournissent les commentaires nécessaires sur les devoirs correspondants dans OneNote. OneNote améliore également l’expérience utilisateur en ajoutant des fonctionnalités au-delà des tests et des liens, tout en tendant les fonctionnalités aux appareils mobiles à l’aide de stylets numériques, de supports photo ou vidéo et de la co-création avec des groupes.

L’intégration OneNote facilite l’accès aux textes, aux graphiques et aux référentiels audio. Le plug-in offre les avantages suivants :

* Inclure des blocs-notes de navigation, des sections et des pages dans lesquels les étudiants travaillent sur des devoirs et fournissent des commentaires sur ceux-ci dans OneNote.
* Combiner un classeur numérique pour les notes, les devoirs et les commentaires pour référence et évaluation.
* Développer des capacités de rédaction au-delà du texte et des liens, et étendre l’utilisation mobile à l’aide de stylets numériques, de supports photo ou vidéo et de la co-création avec des groupes.
* Inclure la page de soumission et de commentaires pour chaque devoir sous le compte des enseignants. Lorsqu’un tel fichier est enregistré dans Moodle, une copie du code HTML et des images associées sont placées dans le package d’un fichier zip.

> [!NOTE]
> Les événements de soumission ou de commentaires déclenchent une création OneNote avec une section pour chaque cours dans lequel l’étudiant s’est inscrit.

## <a name="microsoft-block"></a>Bloc Microsoft

Le plug-in bloc Microsoft permet à l’utilisateur d’accéder à l’emplacement du fichier SharePoint du cours et d’afficher le cours dans un bloc-notes OneNote pour les soumissions, ainsi que la possibilité de modifier les préférences d’intégration Office 365. Les administrateurs peuvent configurer le bloc pour qu’il s’affiche sur toutes les pages du cours.

Le bloc Microsoft améliore l’expérience utilisateur en fournissant une interface utilisateur pour modifier les fonctionnalités d’intégration et d’accès Microsoft 365 à ses nombreuses ressources. Les administrateurs peuvent configurer le bloc pour voir les modifications apportées à afficher sur chaque page du cours. Le bloc permet à l’utilisateur d’effectuer les activités suivantes :

* Accéder à l’emplacement du fichier SharePoint et au bloc-notes OneNote du cours.
* Afficher le cours dans un bloc-notes OneNote pour les soumissions.
* Configurer la synchronisation du calendrier Outlook.
* Gère la connexion à Office 365.
* Personnaliser les préférences d’intégration Office 365.

L’image suivante illustre l’interface utilisateur du bloc Microsoft :

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-block-1.png" alt-text="bloc microsoft":::

## <a name="oembed-filter"></a>Filtre oEmbed

Le plug-in de filtre oEmbed simplifie et améliore l’expérience utilisateur en facilitant l’inclusion de contenu HTML externe dans Moodle. Voici les avantages du filtre oEmbed.

* Réduit le temps d’incorporation de vidéos dans une page HTML.
* Permet l’incorporation de plusieurs fournisseurs de contenu vidéo.
* Garantit un moyen plus rapide pour copier et incorporer du code à partir de l’un des services pris en charge.
* Permet l’incorporation de vidéos sans clé d’API.

L’image suivante illustre l’inclusion de contenu HTML externe dans Moodle :

:::image type="content" source="../../assets/images/MoodleInstructions/oEmbed-filter.png" alt-text="Page de filtre oEmbed":::

## <a name="see-also"></a>Voir aussi

* [Applications partenaires pour Moodle](../partner-apps-for-moodle.md)
* [FAQ Moodle](../faqs.md)
