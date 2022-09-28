---
title: Gérer vos applications avec le Developer Portal
description: Dans cet article, découvrez comment configurer, distribuer et gérer vos applications à l’aide du portail des développeurs pour Microsoft Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 02b9272c2c0d325501c28d150ac728230ac65255
ms.sourcegitcommit: 9ebb516ac448627e1deb42e18703791fc2ad583d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68098917"
---
# <a name="manage-your-apps-in-developer-portal"></a>Gérez vos applications dans le portail des développeurs

Après avoir créé ou chargé votre application, vous pouvez gérer vos applications dans le portail des développeurs avec les éléments suivants :

* [Vue d’ensemble](#overview)
* [Configurer](#configure)
* [Avancé](#advanced)
* [Publier](#publish)

## <a name="overview"></a>Vue d’ensemble

Dans la section **Vue d’ensemble** , vous pouvez voir les composants suivants pour gérer votre application :

* Tableau de bord

  * Dans la section **Tableau de bord** sous **Vue d’ensemble** , vous pouvez voir les composants suivants pour votre application :
    * **Validation du Magasin Teams** : l’outil de validation d’application vérifie votre package d’application par rapport aux cas de test utilisés par Microsoft lors de l’examen de votre application.
    * **Annonce** : Dernières mises à jour de vos applications sur le portail des développeurs pour Teams
    * **Utilisateurs actifs (préversion)** : affiche le nombre d’utilisateurs actifs
    * **Informations de base** : affiche l’ID d’application, la version, la version du manifeste, et ainsi de suite.

    :::image type="content" source="../../assets/images/tdp/dashboard-page.png" alt-text="La capture d’écran est un exemple montrant la page Vue d’ensemble de l’application que vous avez créée dans le portail des développeurs pour Teams.":::

* Analyse

    Dans la page **Analyse** de la section **Vue d’ensemble** , vous pouvez voir le nombre total d’utilisateurs actifs pour votre application. Pour plus [d’informations, consultez Analyser l’utilisation de votre application](analyze-your-apps-usage-in-developer-portal.md).

## <a name="configure"></a>Configurer

Pour installer et afficher votre application dans Teams, vous devez inclure un ensemble de configurations que Teams reconnaît. Pour charger vos applications dans Teams, vous devez disposer du manifeste de l’application, qui contient tous les détails de l’application pour afficher votre application dans Teams. Vous pouvez y parvenir à l’aide de composants et d’outils disponibles dans le portail des développeurs.

Dans la section **Configurer** , vous pouvez voir les composants suivants pour gérer et accéder à votre application :

* **Informations de base** : cette section affiche et vous permet de modifier le nom de l’application, l’ID d’application, les descriptions, la version, les informations de développeur, les URL d’application, l’ID d’application (client) et l’ID microsoft partner network.
* **Personnalisation** : cette page affiche les détails de l’icône de l’application.
* **Fonctionnalités de l’application** : vous pouvez ajouter les fonctionnalités suivantes à votre application :
  * Application personnelle
  * Bot
  * Connector
  * Scène
  * Application de groupe et de canal
  * Extension de la messagerie
  * Extension de réunion
  * Notification de flux d’activité
* **Autorisations** : cette section vous permet d’accorder des autorisations d’appareil, des autorisations d’équipe, des autorisations de conversation ou de réunion et des autorisations utilisateur pour votre application.
* **Authentification unique** : le bot inscrit sur Azure AD prend en charge l’authentification unique Sign-On (SSO). Si un bot est inscrit sur le portail Bot Framework (ou dans le portail des développeurs sous Bot Management), ces bots ne prennent pas en charge l’authentification unique et vous devez inscrire votre bot sur Azure AD pour prendre en charge l’authentification unique. Pour un bot inscrit sur Azure AD, ajoutez **l’URI d’ID d’application**. Pour obtenir l’URI d’ID d’application à partir d’Azure AD, consultez [Utiliser l’authentification unique pour les bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).
* **Langues** : vous pouvez configurer ou modifier la langue de votre application.
* **Domaine** : vous pouvez ajouter les domaines pour charger vos applications dans le client Teams (par exemple : *.example.com).

:::image type="content" source="../../assets/images/tdp/configure.png" alt-text="La capture d’écran est un exemple qui montre comment configurer des fonctionnalités pour gérer et accéder à votre application dans le portail des développeurs.":::

## <a name="advanced"></a>Avancé

Dans la section **Avancé** , vous pouvez voir les composants suivants pour gérer votre application dans le portail des développeurs :

* **Propriétaires**

    Chaque application inclut une page **Propriétaires** , dans laquelle vous pouvez partager votre inscription d’application avec d’autres personnes de votre organisation. Vous pouvez ajouter **un rôle Administrateur** et **Opérationnel** pour gérer qui peut modifier les paramètres de votre application. Le rôle **Opérateur** dispose des mêmes autorisations que le rôle **Administrateur** , à l’exception de la suppression d’une application.

    Pour ajouter un propriétaire :

    1. Dans la section **Avancé** , sélectionnez **Propriétaires**.
    1. Sélectionnez **Ajouter un propriétaire**.
    1. Entrez un nom et sélectionnez un ID d’utilisateur dans la liste déroulante.
    1. Sous **Rôle**, sélectionnez **Opérateur** ou **Administrateur**.
    1. Sélectionnez **Ajouter**.

* **Contenu de l’application** : vous pouvez configurer votre application avec les fonctionnalités supplémentaires suivantes :
  
  * Indicateur de chargement : affiche un indicateur pour informer les utilisateurs du contenu de votre application hébergée (par exemple, les onglets et les modules De tâches) est en train de charger.
  * Mode plein écran : affiche une application personnelle sans en-tête d’application. Il est uniquement pris en charge pour les applications publiées sur votre organisation.

* **Environnements**

    Vous pouvez configurer des environnements et des variables globales pour faciliter la transition de votre application de votre runtime local vers la production. Les variables globales sont utilisées dans tous les environnements.

    Pour configurer un environnement :

    1. Dans le portail des développeurs, sélectionnez les **applications** que vous travaillez.
    1. Accédez à **Environnements** sous la section **Avancé** , puis sélectionnez **+ Ajouter un environnement**.
    1. Sélectionnez **Ajouter**.

  * **Variables globales**

      1. Sélectionnez **Ajouter une variable globale** pour créer des variables de configuration pour votre environnement.

      Pour utiliser des variables globales :

      Utilisez les noms de variables au lieu de valeurs codées en dur pour définir les configurations de votre application.

      1. Entrez `{{` dans n’importe quel champ du Developer Portal. Une liste déroulante contenant toutes les variables que vous avez créées pour l’environnement choisi ainsi que les variables globales s’affiche.  
      1. Avant de télécharger votre package d’application (par exemple, lors de la préparation de la publication dans le Magasin Teams), sélectionnez l’environnement que vous souhaitez utiliser. Les configurations de votre application sont mises à jour automatiquement en fonction de l’environnement.

* **Plan et tarification** : vous pouvez lier une offre SaaS que vous avez créée dans l’Espace partenaires pour votre application.
* **paramètres de Administration** :
  * Personnalisation de l’application : vous pouvez personnaliser votre application
  * Bloquer l’application par défaut : vous pouvez bloquer votre application par défaut pour les utilisateurs jusqu’à ce qu’un administrateur client choisisse de l’activer.

## <a name="publish"></a>Publier

Vous pouvez publier votre application sur votre organisation ou dans le Magasin Teams.

* **Publiez votre application sur l’organisation** :

   1. Dans la page **Vue d’ensemble** de l’application, sous **Publier**, sélectionnez **Publier sur l’organisation**.
   1. Sélectionnez **Publier votre application**.

* **Publiez votre application pour stocker** :

   1. Dans la page **Vue d’ensemble** de l’application, sous **Publier**, sélectionnez **Publier dans le Store**.
   1. Sélectionnez **Publier**.

   > [!NOTE]
   > L’outil de validation d’application vérifie votre package d’application par rapport aux cas de test utilisés par Microsoft pour examiner votre application. Résolvez les erreurs ou les avertissements et lisez la **liste de vérification de soumission** de l’application avant de soumettre votre application.

   Vous pouvez télécharger le package d’application en sélectionnant le bouton **Télécharger le package d’application** dans la page Publier dans le store.

* **Package d’application** : le package d’application décrit comment votre application est configurée, qui inclut les fonctionnalités de l’application, les ressources requises et d’autres attributs importants dans le manifeste. L’onglet Icône affiche l’icône utilisée pour votre application.

## <a name="test-your-app-directly-in-teams"></a>Tester votre application directement dans Teams

Le Developer Portal fournit des options pour tester et déboguer votre application :

* Dans la page **Vue d’ensemble** , vous pouvez voir un instantané si votre application est configurée et validée par rapport aux cas de test du Magasin Teams.
* Le bouton **Aperçu dans Teams** lance rapidement votre application dans le client Teams pour le débogage.

## <a name="use-tools-to-create-app-features"></a>Utiliser des outils pour créer des fonctionnalités d’application

Le portail des développeurs inclut également des outils pour vous aider à créer des fonctionnalités clés des applications Teams. Voici les outils suivants :

* **Scene Studio**: concevez [des scènes en mode Ensemble personnalisées](~/apps-in-teams-meetings/teams-together-mode.md) pour les réunions Teams.
* **Cartes adaptatives** de l’éditeur : créez et affichez un aperçu Cartes adaptatives à inclure avec vos applications.
* **Gestion de la plateforme d'identité Microsoft** : Enregistrez vos apps auprès d'Azure Active Directory pour aider les utilisateurs à se connecter et leur donner accès aux API.
* **Validation de l’application du Magasin Teams** : vérifiez votre package d’application par rapport aux cas de test utilisés par Microsoft pour passer en revue votre application.
* **Gestion des** bots : ajoutez des bots conversationnels à votre application qui communiquent avec les utilisateurs, répondent à leurs questions et les informent de manière proactive des modifications et d’autres événements.

Pour ajouter un bot :

1. Dans le portail des développeurs, sélectionnez **Outils** dans le volet gauche.
1. Sélectionnez la **gestion du bot**.
1. Dans la page de gestion du bot, sélectionnez **Nouveau bot**.
1. Entrez le nom et **sélectionnez Ajouter**.

   :::image type="content" source="../../assets/images/tdp/tools-in-dev-portal.png" alt-text="La capture d’écran est un exemple montrant les outils du portail des développeurs, qui vous aide à créer des fonctionnalités clés.":::

À partir du portail des développeurs, vous pouvez accéder au portail Bot Framework et configurer votre bot pour mettre à jour l’icône et d’autres propriétés.

## <a name="see-also"></a>Voir aussi

[Inclure une offre SaaS avec votre application Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
