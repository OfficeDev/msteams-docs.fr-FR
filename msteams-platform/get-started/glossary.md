---
title: Documentation pour développeurs Microsoft Teams – Glossaire
description: En savoir plus sur les termes utilisés dans Microsoft Teams documentation du développeur
ms.localizationpriority: high
ms.topic: reference
ms.openlocfilehash: 742c2c940c5b3c39037b28eaf6ecc14fac3b0874
ms.sourcegitcommit: 68bf3adb8aaae07caf684f7d9efb5cb7c84598b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2022
ms.locfileid: "67382943"
---
# <a name="glossary"></a>Glossaire

Termes et définitions courants utilisés dans la documentation pour développeurs Teams.

## <a name="a"></a>A

| Terme | Définition |
| --- | --- |
| [Commande d’action](../messaging-extensions/how-to/action-commands/define-action-command.md) | Type d’application d’extension de message qui utilise une fenêtre contextuelle pour collecter ou afficher des informations. <br>**Voir aussi** : [Extension de messagerie](#m) ; [Commandes de recherche](#s) |
| [Cartes adaptatives](../task-modules-and-cards/what-are-cards.md) | Extrait de contenu actionnable ajouté à une conversation par un bot ou une extension de message. Utilisez du texte, des graphiques et des boutons avec ces cartes pour une communication enrichie. |
| [Utilisateur anonyme](../apps-in-teams-meetings/meeting-app-extensibility.md#user-types-in-a-meeting) | Un type de participant à une réunion Teams qui n'a pas d'identité Azure AD et n'est pas fédéré avec un locataire. Ils sont comme des utilisateurs externes dans une réunion. <br>**Voir aussi** : [Utilisateur fédéré](#f) |
| [Catalogue d’applications](../toolkit/publish.md) | Site qui stocke les applications SharePoint et Office pour l’utilisation interne d’une organisation. <br>**Voir aussi** : [SPFx](#s) |
| [Manifeste d'application](../resources/schema/manifest-schema.md) | Le manifeste de l’application Teams décrit comment l’application s’intègre au produit Microsoft Teams. Votre manifeste doit être conforme au [schéma du manifeste](https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json). |
| [Package de l’application](../concepts/build-and-test/apps-package.md) | Un package d’application Teams est un fichier zip qui contient le fichier manifeste de l’application, l’icône de couleur et l’icône de contour. |
| [Autorisation de l’application](../concepts/device-capabilities/browser-device-permissions.md#enable-apps-device-permissions) | Une option dans une application Teams pour activer les autorisations d’appareil. Il est disponible uniquement lorsque le fichier manifeste de l’application déclare que l’application a besoin d’autorisations d’appareil. <br> **Voir aussi** : [Autorisations de l’appareil](#d) |
| [Étendue de l’application](../concepts/design/app-structure.md) | Zone dans Teams où les utilisateurs peuvent utiliser votre application. Les applications peuvent avoir une ou plusieurs étendues, notamment personnelles, canaux, conversations et réunions. Une application Teams peut exister entre les étendues. |
| Bac d’application | Un bac d’application situé dans la barre inférieure d’une application mobile Teams. Il collecte toutes les applications qui sont ouvertes mais qui ne sont pas actuellement utilisées ou actives. <br>**Voir aussi** : [Teams Mobile](#t) |
| [Ressource Azure](../toolkit/provision.md) | Un service disponible via Azure que votre application Teams peut utiliser pour le déploiement Azure. Il peut s’agir de comptes de stockage, d’applications web, de bases de données, etc. |
| [Azure Active Directory](../tabs/how-to/authentication/auth-tab-aad.md) | Service de gestion des identités et des accès basé sur le cloud de Microsoft. Il permet aux utilisateurs authentifiés d’accéder aux ressources internes et externes. |
| [Authentification](../concepts/authentication/authentication.md) | Processus de validation de l’identité d’un utilisateur pour accéder à votre application. <br> **Voir aussi :** [Fournisseurs d’identité](#i) ; [SSO](#s) |
| [Flux d’authentification](../concepts/authentication/authentication.md) | La façon dont un utilisateur s’authentifie auprès de votre application. Pour les applications Teams, nous vous recommandons d’utiliser l’authentification unique (SSO) à l’aide d’Azure Active Directory (AAD), mais une alternative consiste à utiliser un fournisseur OAuth tiers.|

## <a name="b"></a>B

| Terme | Définition |
| --- | --- |
| [Blazor](../get-started/get-started-overview.md) | Un framework web gratuit et open-source qui permet aux développeurs de créer des applications web en utilisant C# et HTML. Il est développé par Microsoft. |
| [Bicep](../toolkit/provision.md) | Langage déclaratif, ce qui signifie que les éléments peuvent apparaître dans n’importe quel ordre. Contrairement aux langages impératifs, l’ordre des éléments n’affecte pas le traitement du déploiement. |
| [Bot](../bots/what-are-bots.md) | Un bot est une application qui exécute des tâches répétitives programmées. <br> **Voir aussi** : [Bot conversationnel](#c) ; [Bot de conversation](#c) |
| [Bot Emulator](../bots/how-to/debug/locally-with-an-ide.md#use-the-bot-emulator) | Application de bureau qui vous permet de tester et déboguer des bots, localement ou à distance. |
| [Bot Framework](../bots/bot-features.md) | Un kit de développement logiciel (SDK) riche utilisé pour créer des bots à l’aide de C#, Java, Python et JavaScript. Si vous avez un bot basé sur le Bot Framework, vous pouvez le modifier pour qu’il fonctionne dans Teams. |

## <a name="c"></a>C

| Terme | Définition |
| --- | --- |
| [Bot d’appel](../bots/calls-and-meetings/calls-meetings-bots-overview.md) | Bot qui participe à des appels audio ou vidéo et à des réunions en ligne. <br> **Voir aussi :** [Bot de conversation](#c) ; [Bot de réunion](#m) |
| [Fonctionnalité](../toolkit/add-capability.md) | Une fonctionnalité Teams que vous pouvez intégrer à votre application pour interagir avec les utilisateurs de l’application. Une fonctionnalité d’application est utilisée pour étendre Teams en fonction des besoins de votre application. Une application peut avoir une ou plusieurs fonctionnalités principales, telles que l’onglet, le bot et l’extension de message. <br>**Voir aussi :** [Fonctionnalité de l’appareil](#d) ; [Fonctionnalité multimédia](#m) |
| [Bot de conversation](../bots/how-to/conversations/conversation-basics.md) | Un bot est également appelé chatbot ou bot de conversation. Il s’agit d’une application qui exécute des tâches simples et répétitives pour les utilisateurs tels que le service clientèle ou le personnel du support technique. <br> **Voir aussi** : [Bot conversationnel](#c) |
| Canal | Un emplacement unique où une équipe peut partager des messages, des outils et des fichiers. Vous pouvez utiliser un canal pour le travail d’équipe et la communication. <br>**Voir aussi** : [Conversation](#c) |
| [Clé secrète client](../bots/how-to/authentication/add-authentication.md) | Chaîne secrète que l’application utilise pour prouver son identité lors de la demande d’un jeton. En outre, il peut être appelé mot de passe d’application.|
| [Ressources cloud](../toolkit/add-resource.md) | Service disponible sur le cloud via Internet que votre application Teams peut utiliser. Il peut s’agir de comptes de stockage, d’applications web, de bases de données, etc. |
| [Application de collaboration](../concepts/extensibility-points.md) | Application avec des fonctionnalités qui permet à un utilisateur de travailler dans un espace de travail collaboratif avec d’autres utilisateurs. <br> **Voir aussi** : [Application autonome](#s) |
| [Composer l’extension](../resources/schema/manifest-schema.md#composeextensions) | Propriété dans le manifeste d’application (`composeExtensions`) qui fait référence à la fonctionnalité d’extension de message. Il est utilisé lorsque votre extension doit s’authentifier ou se configurer pour continuer. <br>**Voir aussi :** [Manifeste de l’application](#a) ; [Extension de messagerie](#m) |
| [Zone de commande](../resources/schema/manifest-schema.md) | Type de contexte dans le manifeste d’application (`commandBox`) que vous pouvez configurer pour appeler une extension de message à partir de la zone de commande Teams. |
| [Connector](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) | Il permet aux utilisateurs de s’abonner pour recevoir des notifications et des messages des services web. Les connecteurs exposent le point de terminaison HTTPS pour que le service publie des messages sur les canaux Teams, généralement sous la forme de cartes. <br> **Voir aussi** : [Webhook](#w) |
| Conversation | Une série de messages envoyés entre votre application Microsoft Teams (onglet ou bot) et un ou plusieurs utilisateurs. Une conversation peut avoir trois étendues : canal, personnel et conversation de groupe. <br>**Voir aussi** : [Conversation un-à-un](#o) ; [Conversation de groupe](#g) ; [Canal](#c) |
| [Bot conversationnel](../bots/how-to/conversations/conversation-messages.md) |  Il permet à un utilisateur d’interagir avec votre service web à l’aide de texte, de cartes interactives et de modules de tâche. <br>**Voir aussi** [Bot de conversation](#c) |

## <a name="d"></a>D

| Terme | Définition |
| --- | --- |
| [Liaisons profondes](../concepts/build-and-test/deep-links.md) | Dans une application Teams, vous pouvez créer des liens profonds vers des informations et des fonctionnalités dans Teams ou pour aider l’utilisateur à accéder au contenu de votre application. |
|[Département de la Défense (DoD)](../concepts/app-fundamentals-overview.md#government-community-cloud)| Les environnements DoD sont conformes aux recommandations du département de la Défense sur les exigences de sécurité, au Supplément aux règlements fédéraux d’acquisition de la défense (DFARS) et au International Traffic in Arms Regulations (ITAR).|
| [Documentation pour les développeurs](../concepts/build-and-test/teams-developer-portal.md) | L’outil principal pour configurer, distribuer et gérer vos applications Microsoft Teams. Avec le Portail du développeur, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’exécution, et bien plus encore. |
| [Aperçu pour les développeurs](../resources/dev-preview/developer-preview-intro.md) | Programme public pour les développeurs qui fournit un accès anticipé aux fonctionnalités non disponibles dans Microsoft Teams. Il vous permet d’explorer et de tester les fonctionnalités à venir pour une inclusion potentielle dans votre application Microsoft Teams. |
| Déployer | Processus de chargement du code principal et frontal pour l’application. Lors du déploiement, le code de votre application est copié dans les ressources que vous avez créées lors de l’approvisionnement. <br>**Voir aussi :** [Provision](#p) |
| [Fonctionnalités de l’appareil](../concepts/device-capabilities/device-capabilities-overview.md) | Les appareils intégrés, tels que l’appareil photo, le microphone, le scanneur de codes-barres, la galerie de photos, dans un appareil mobile ou de bureau. Vous pouvez accéder aux fonctionnalités d’appareil suivantes sur les appareils mobiles ou de bureau via des API dédiées disponibles dans le Kit de développement logiciel (SDK) client JavaScript de Microsoft Teams. <br>**Voir aussi** : [Fonctionnalité](#c) ; [Fonctionnalité multimédia](#m) ; [Fonctionnalité d’emplacement](#l) |
| [Autorisation de l’appareil](../concepts/device-capabilities/browser-device-permissions.md) | Un paramètre d’application Teams que vous pouvez configurer dans votre application. Vous l’utilisez pour demander l’autorisation à votre application d’accéder à une fonctionnalité d’appareil native et d’utiliser celle-ci. Vous pouvez gérer les autorisations d’appareil dans les paramètres Teams. <br>**Voir aussi** : [Autorisations d’application](#a) |
| [Environnement de développement](../toolkit/teamsfx-multi-env.md#create-a-new-environment) | Type d’environnement de développement créé par le Kit de ressources Teams par défaut. Il représente les configurations d’environnements distants ou cloud. Un projet peut avoir plusieurs environnements distants. Vous pouvez ajouter d’autres environnements de développement à votre projet à l’aide du Kit de ressources Teams. <br>**Voir aussi** [Environnement](#e) ; [Environnement local](#l) |
| [DevTools](../tabs/how-to/developer-tools.md) | Les DevTools du navigateur permettent d’afficher les journaux de la console, d’afficher ou de modifier les demandes réseau runtime, d’ajouter des points d’arrêt au code (JavaScript) et d’effectuer un débogage interactif pour une application Teams. La fonctionnalité est disponible uniquement pour les clients de bureau et Android après l’activation de la préversion du développeur. |
| [Recherche dynamique](../task-modules-and-cards/cards/dynamic-search.md#dynamic-typeahead-search) | Une fonctionnalité de recherche pour Cartes adaptatives qui est utile pour rechercher et sélectionner des données dans des jeux de données volumineux. Elle permet de filtrer les choix lorsque l’utilisateur entre dans la chaîne de recherche. <br>**Voir aussi** : [Recherche statique](#s) |

## <a name="e"></a>E

| Terme | Définition |
| --- | --- |
| [Compte de développeur E5](../toolkit/accounts.md) | Abonnement pour développeurs E5 pour la création d’applications pour étendre Microsoft 365. Il inclut 25 licences utilisateur, y compris l’administrateur, à des fins de développement uniquement.  <br>**Voir aussi** : [Compte Microsoft 365](#m) |
| [Point d’entrée](../concepts/app-fundamentals-overview.md) | Un point d’accès, tel que l’équipe, le canal et la conversation, pour une application Teams où les utilisateurs peuvent utiliser votre application. |
| [Environnement](../toolkit/teamsfx-multi-env.md) | Une fonctionnalité du Kit de ressources Teams qui vous permet de créer et d’utiliser plusieurs environnements de développement pour votre projet d’application. Le Kit de ressources Teams crée deux environnements de développement par défaut : environnement local et environnement de développement. <br>**Voir aussi** : [Environnement local](#l) ; [Environnement de développement](#d) |

## <a name="f"></a>F

| Terme | Définition |
| --- | --- |
| [Utilisateur fédéré](../apps-in-teams-meetings/meeting-app-extensibility.md#user-types-in-a-meeting) | Type d’utilisateur dans une réunion d’application Teams qui est externe et est invité à la réunion. Cet utilisateur dispose d’informations d’identification valides fédérées par des partenaires Teams autorisés. Ils sont également appelés utilisateurs externes. <br>**Voir aussi** : [Utilisateur anonyme](#a) |
| [Expérience de première exécution](../concepts/design/design-teams-app-ui-templates.md)|Une expérience de première exécution (FRE) est l’introduction d’un utilisateur à votre produit. Le FRE aide les utilisateurs à prendre en main les fonctions, les fonctionnalités et les avantages du produit, et influence les utilisateurs à revenir et à continuer à utiliser votre produit.|

## <a name="g"></a>G

| Terme | Définition |
| --- | --- |
|[Cloud de la communauté gouvernementale (GCC)](../concepts/app-fundamentals-overview.md#government-community-cloud)| L’environnement gcc fournit la conformité avec les exigences fédérales pour les services cloud, y compris FedRAMP High, Defense Federal Acquisition Regulations Supplement (DFARS) et les exigences relatives à la justice pénale et aux systèmes d’information fiscale fédéraux (types de données CJI et FTI).|
|[Cloud de la communauté gouvernementale (GCC) High](../concepts/app-fundamentals-overview.md#government-community-cloud)|Les environnements de haute qualité du GCC sont conformes aux directives sur les exigences de sécurité du ministère de la Défense (DoD), au Supplément aux règlements fédéraux sur les acquisitions de défense (DFARS) et au International Traffic in Arms Regulations (ITAR).<br>**Voir aussi** : [Department of Defense (DoD)](#d)|
| [API Graph](../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) | Microsoft Graph est une API web RESTful qui vous permet d’accéder aux ressources de service Cloud Microsoft. <br>**Voir aussi** : [L’afficheur Microsoft Graph](#m) |
| [Conversation de groupe.](../resources/bot-v3/bot-conversations/bots-conversations.md) | Fonctionnalité de conversation dans laquelle un utilisateur peut discuter avec un bot dans un paramètre de groupe à l’aide de @mention pour appeler le bot. <br>**Voir aussi** : [Conversation un-à-un](#o) ; [Bot de conversation](#c) |

## <a name="i"></a>I

| Terme | Définition |
| --- | --- |
| [Fournisseur d'identité](../concepts/authentication/configure-identity-provider.md) | Entité qui stocke et fournit des informations d’identification à l’utilisateur. Les utilisateurs peuvent également s’inscrire auprès d’un fournisseur d’identité.  <br>**Voir aussi :** [Authentification](#a) |
| [Webhook entrant](../webhooks-and-connectors/how-to/add-incoming-webhook.md) | Permet à une application externe de partager du contenu dans les canaux Teams. Ces webhooks sont utilisés comme outils de suivi et de notification. <br>**Voir aussi** : [Webhook](#w) ; [Webhook sortant](#o) |
| [Expérience d'application en réunion](../apps-in-teams-meetings/meeting-app-extensibility.md#in-meeting-app-experience) | Une étape du cycle de vie d'une réunion Teams. Avec l'expérience des apps de réunion, vous pouvez impliquer les participants pendant la réunion en utilisant des apps et la boîte de dialogue de réunion. <br>**Voir aussi :** [Cycle de vie des réunions](#m) |

## <a name="l"></a>L

| Terme | Définition |
| --- | --- |
| [Déploiement de lien](../messaging-extensions/how-to/link-unfurling.md) | Fonctionnalité utilisée avec l’extension de message et la réunion pour déplier les liens collés dans une zone de composition de message. Les liens s’étendent pour afficher des informations supplémentaires sur le lien dans Cartes adaptatives ou dans l’affichage de la phase de réunion. |
| [Environnement local](../toolkit/teamsfx-multi-env.md#create-a-new-environment) | Environnement de développement par défaut créé par le Kit de ressources Teams.  <br>**Voir aussi** : [Environnement](#e) ; [Environnement de développement](#d) |
| [Workbench local](../sbs-gs-spfx.yml) | Option par défaut permettant d’exécuter et de déboguer une application Teams dans Visual Studio Code créée à l’aide de SPFx. <br>**Voir aussi** : [Workbench](#w) ; [Teams workbench](#t) |
| [Fonctionnalité d’emplacement](../concepts/device-capabilities/location-capability.md) | Une fonctionnalité de dispositif que vous pouvez intégrer à votre application pour connaître l'emplacement géographique de l'utilisateur de l'application afin d'améliorer l'expérience de collaboration. Cette fonctionnalité est actuellement disponible uniquement pour les clients mobiles Teams. <br>**Voir aussi** : [Fonctionnalité](#c) ; [Fonctionnalité multimédia](#m) ; [Fonctionnalité de l’appareil](#d) ; [Teams Mobile](#t) |
| [Applications à faible code](../samples/teams-low-code-solutions.md) | Une application Teams personnalisée conçue à partir de zéro à l’aide de Microsoft Power Platform qui nécessite peu ou pas de codage, et qui peut être développée et déployée rapidement. |

## <a name="m"></a>M

| Terme | Définition |
| --- | --- |
| [Fonctionnalité multimédia](../concepts/device-capabilities/media-capabilities.md) | Fonctionnalités natives de l’appareil, telles que la caméra et le microphone, que vous pouvez intégrer à votre application Teams. <br>**Voir aussi** : [Fonctionnalité](#c) ; [Fonctionnalité de l’appareil](#d) |
| [Bot de réunion](../bots/calls-and-meetings/calls-meetings-bots-overview.md) | Bots qui interagissent avec les appels et réunions Teams à l’aide de la voix, de la vidéo et du partage d’écran en temps réel. <br>**Voir aussi :** [Bot d’appel](#c) ; [Bot de conversation](#c) |
| [Cycle de vie des réunions](../apps-in-teams-meetings/meeting-app-extensibility.md#meeting-lifecycle) | Il s’étend de l’expérience d’application de pré-réunion, en réunion et à la post-réunion. Vous pouvez intégrer des onglets, des bots et des extensions de message à chaque étape du cycle de vie de la réunion. <br>**Voir aussi** : [Expérience en réunion](#i) |
| [Étape de la réunion](../sbs-meetings-stage-view.yml) | Fonctionnalité de l’application d’extension de réunion. Il s’agit d’un espace partagé accessible à tous les participants pendant la réunion. Il permet aux participants d’interagir et de collaborer avec le contenu de l’application en temps réel. <br>**Voir aussi :** [Vue des l’étapes](#s) |
| [Extension de message](../messaging-extensions/what-are-messaging-extensions.md) | Les extensions de message sont des raccourcis permettant d’insérer du contenu d’application ou d’agir sur un message. Vous pouvez utiliser une extension de message sans quitter la conversation. <br>**Voir aussi** : [Commandes de recherche](#s) ; [Commandes d’action](#a) |
| [Extension de réunion](../apps-in-teams-meetings/design/designing-apps-in-meetings.md) | Application conçue pour être utilisée pendant le cycle de vie des réunions pour la rendre plus productive, comme le tableau blanc, le tableau de bord, etc. |
| [Compte Microsoft 365](../toolkit/accounts.md#microsoft-365-developer-account-types) | Le compte Microsoft 365 inclut 25 licences utilisateur, y compris l’administrateur, à des fins de développement uniquement. |
| [Programme de développement Microsoft 365](../toolkit/accounts.md)| Le programme de développement Microsoft 365 vous aide à créer des applications qui étendent Microsoft 365. |
| [Afficheur Microsoft Graph](../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) | La passerelle vers les données et l'intelligence dans Microsoft 365. Elle fournit un modèle de programmabilité unifié que vous pouvez utiliser pour accéder aux données dans Microsoft 365, Windows 10 et Enterprise Mobility + Security. |
| [Microsoft Teams](../overview.md) | Microsoft Teams est un logiciel de collaboration de groupe qui peut être utilisé pour aider les équipes à collaborer à distance. |
| [Plateforme Microsoft Teams](../concepts/app-fundamentals-overview.md) | La plateforme de développement Microsoft Teams permet aux développeurs d’intégrer facilement leurs propres applications et services à Teams. |
| [Bibliothèque d’interface utilisateur Microsoft Teams](../concepts/design/design-teams-app-ui-templates.md#microsoft-teams-ui-library) | La bibliothèque d’interface utilisateur Microsoft Teams vous permet d’afficher et de tester des modèles d’interface utilisateur Teams individuels et des composants associés dans votre navigateur. |
| [Kit de ressources d’interface utilisateur Microsoft Teams](../concepts/design/design-teams-app-ui-templates.md#microsoft-teams-ui-library) | Le Kit d’interface utilisateur Microsoft Teams inclut des composants et des modèles conçus spécifiquement pour la création d’applications Teams. |

## <a name="o"></a>O

| Terme | Définition |
| --- | --- |
| [Connecteur Office 365](../webhooks-and-connectors/how-to/connectors-creating.md) | Il vous permet de créer une page de configuration personnalisée pour votre webhook entrant et de les empaqueter dans le cadre d’une application Teams. Vous pouvez envoyer des messages principalement à l’aide de cartes de connecteur Office 365 et vous avez la possibilité de leur ajouter un ensemble limité d’actions de carte. |
| [Webhook sortant](../webhooks-and-connectors/how-to/add-outgoing-webhook.md) | Il agit comme un bot et recherche des messages dans les canaux à l’aide de @mention. Il envoie des notifications aux services web externes et répond avec des messages enrichis, qui incluent des cartes et des images. <br>**Voir aussi** : [Webhook](#w) ; [Webhook entrant](#i) |
| [Canal Outlook](../m365-apps/extend-m365-teams-message-extension.md#add-an-outlook-channel-for-your-bot) | Fonctionnalité de l’application d’extension de message Teams qui permet aux utilisateurs d’interagir avec elle à partir de Microsoft Outlook. |
| [Conversation un-à-un](../resources/bot-v3/bot-conversations/bots-conv-personal.md) | Type de conversation entre une application de bot personnel Teams et un seul utilisateur. <br>**Voir aussi :** [Conversation de groupe](#g) ; [Bot de conversation](#c) |

## <a name="p"></a>P

| Terme | Définition |
| --- | --- |
| [Sélecteur de personnes](../task-modules-and-cards/cards/people-picker.md) | Contrôle natif dans la plateforme Teams permettant de rechercher et de sélectionner des personnes, qui peuvent être intégrées dans les applications web, les cartes adaptatives, etc. |
| [Application personnelle](../concepts/design/personal-apps.md) | Une application personnelle est une application Teams avec une étendue personnelle. Il se concentre sur les interactions avec un seul utilisateur. Il peut s’agir d’un bot conversationnel pour participer à des conversations un-à-un avec un utilisateur ou un onglet personnel fournissant une expérience web incorporée, ou les deux. <br>**Voir aussi** : [Application partagée](#s) |
| [Power Virtual Agents](../bots/how-to/add-power-virtual-agents-bot-to-teams.md) | Solution d’interface graphique guidée sans code qui permet à chaque membre de votre équipe de créer des bots conversationnels riches qui s’intègrent facilement à la plateforme Teams. |
| [Messages proactifs](../bots/how-to/conversations/send-proactive-messages.md) | Message envoyé par un bot qui n’est pas une réponse à une demande d’un utilisateur, comme les messages d’accueil, les notifications, les messages planifiés. |
| [Approvisionnement](../toolkit/provision.md) | Un processus qui crée des ressources dans Azure et Microsoft 365 pour votre application, mais aucun code (HTML, CSS, JavaScript, etc.) n'est copié dans les ressources. Il s'agit d'une condition préalable au déploiement. <br>**Voir aussi** : [Déployer](#d) |

## <a name="r"></a>R

| Terme | Définition |
| --- | --- |
| [Limitation des débits](../bots/how-to/rate-limit.md) | Méthode permettant de limiter les messages à une certaine fréquence maximale pour s’assurer que le nombre de messages est suffisant et qu’ils n’apparaissent pas comme du courrier indésirable. |
| [Affichages basés sur des rôles](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md) | Fonctionnalité des onglets où l’expérience de tabulation peut être différente pour les utilisateurs en fonction de leur niveau d’autorisation. |
| [Autorisation RSC](../graph-api/rsc/resource-specific-consent.md) | La fonctionnalité d’autorisation RSC (Resource-Specific Consent) est nécessaire aux propriétaires d’équipe pour permettre à une application bot de recevoir des messages sur les canaux d’une équipe sans être @mentioned. |

## <a name="s"></a>S

| Terme | Définition |
| --- | --- |
| [Commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) | Type d’application d’extension de message qui permet aux utilisateurs de rechercher des systèmes externes et d’inclure le résultat de la recherche dans un message à l’aide d’une carte. <br>**Voir aussi** : [Extensions de messagerie](#m); [Commandes d’action](#a) |
| [Flux de travail séquentiel](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md) | Flux de travail qui permet à un bot d’effectuer une conversation avec un utilisateur en fonction de la réponse de l’utilisateur. |
| [Application partagée](../concepts/extensibility-points.md#shared-app-experiences) | Application qui existe dans une équipe, un canal ou une conversation dans laquelle les utilisateurs peuvent collaborer et interagir. <br>**Voir aussi :** Application personnelle |
| [Collection de sites SharePoint](../sbs-gs-spfx.yml) | Un site de collecte pour les applications SharePoint. Vous devez disposer d'un compte administrateur pour ce site avant de pouvoir déployer votre application SPFx sur le site SharePoint. <br>**Voir aussi** : SPFx |
| [Chargement de version test](../toolkit/publish.md#publish-to-individual-scope-or-sideload-permission) | Processus dans lequel une application Teams est chargée sur le client Teams pour la tester dans l’environnement Teams avant de la distribuer. |
| [SidePanel](../sbs-meetings-sidepanel.yml) | Fonctionnalité de l’application de réunion Teams qui vous permet de personnaliser les expériences d’une réunion qui permettent aux organisateurs et aux présentateurs d’avoir différents ensembles de vues et d’actions. |
| [SPFx](../sbs-gs-spfx.yml) | SharePoint Framework (SPFx) est un modèle de développement permettant de créer des solutions côté client pour Microsoft Teams et SharePoint. |
| Authentification unique | Acronyme de l’authentification unique, méthode d’authentification dans laquelle un utilisateur doit se connecter à un service indépendant d’une plateforme logicielle (par exemple, Microsoft 365) une seule fois. L’utilisateur est alors en mesure d’accéder à tous les services sans avoir à passer à nouveau par l’authentification. <br>**Voir aussi :** [Authentification](#a) |
| [vue des étapes](../sbs-meetings-stage-view.yml) | Un composant d'interface utilisateur qui vous permet de rendre le contenu qui est ouvert en plein écran dans Teams et épinglé comme un onglet. Il est invoqué pour faire apparaître le contenu Web dans Teams. Notez que ce *n'est pas* la même chose que la scène de réunion. <br>**Voir aussi :** [Étape de la réunion](#m) |
| [Application autonome](../samples/integrating-web-apps.md) | Une application à page unique ou volumineuse et complexe. L’utilisateur peut utiliser certains aspects de celui-ci dans Teams. <br>**Voir aussi** : [Collaboration aap](#c) |
| [Recherche statique](../task-modules-and-cards/cards/dynamic-search.md) | Méthode de recherche typeahead qui permet aux utilisateurs de rechercher à partir de valeurs prédéfinies dans la charge utile les cartes adaptatives. <br>**Voir aussi** : [Recherche dynamique](#d) |
| [Recommandations en matière de validation du Store](../concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) | Un ensemble de recommandations Teams spécifiques à la validation d’une application avant qu’elle ne puisse être soumise à Teams store. <br>**Voir aussi** : [Teams store](#t) |

## <a name="t"></a>T

| Terme | Définition |
| --- | --- |
| [Tab](../tabs/what-are-tabs.md) | Les onglets sont des pages web prenant en charge Teams incorporées dans Microsoft Teams qui pointent vers des domaines déclarés dans le manifeste. Vous pouvez l’ajouter à l’intérieur d’une équipe, d’une conversation de groupe ou d’une application personnelle. |
| [Conversation par onglets](../tabs/how-to/conversational-tabs.md) | Type d’onglet qui permet à un utilisateur d’avoir une expérience de conversation axée sur les onglets dynamiques. |
| [Modules de tâche](../task-modules-and-cards/what-are-task-modules.md) | Fonctionnalité de l’application Teams permettant de créer une fenêtre contextuelle modale pour effectuer des tâches, afficher des vidéos ou un tableau de bord. |
| [Conversation de thread](../tabs/design/tabs.md#thread-discussion) | Conversation publiée sur un canal ou une conversation entre les utilisateurs. <br>**Voir aussi** [Conversation](#c) ; [Canal](#c) |
| [Teams](../overview.md) | Microsoft Teams est l’application de message la plus adaptée à votre organisation. Il s’agit d’un espace de travail pour la collaboration et la communication en temps réel, les réunions, le partage de fichiers et d’applications. |
| [Toolkit Teams](../toolkit/teams-toolkit-fundamentals.md) | Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement deVisual Studio Code.  |
| [TeamsFx](../toolkit/teamsfx-cli.md) | TeamsFx est une interface de ligne de commande en mode texte qui accélère le développement des applications Teams. Elle est également appelée TeamsFx CLI.|
| [Kit de développement logiciel (SDK) TeamsFx](../toolkit/teamsfx-sdk.md) | Le Kit de développement logiciel (SDK) TeamsFx est préconfiguré dans un projet généré automatiquement à l’aide du Kit de ressources TeamsFx ou de l’interface CLI. |
| [TeamsJS SDK](../tabs/how-to/using-teams-client-sdk.md) | Le SDK TeamsJS vous permet de créer des expériences hébergées dans Teams. À partir de TeamsJS v.2.0.0, vous pouvez étendre les applications Teams pour qu'elles fonctionnent dans Outlook et Office. |
| [Teams Mobile](../concepts/design/plan-responsive-tabs-for-teams-mobile.md) | Microsoft Teams disponible en tant qu’application mobile. |
| [Teams store](../concepts/deploy-and-publish/appsource/publish.md) | Page d’accueil de Store qui permet aux utilisateurs d’accéder aux applications dans un emplacement unique. Les applications sont classées par utilisation, secteur d’activité, etc. Une application doit suivre les instructions de validation de Windows Store et obtenir une approbation avant qu’elle ne soit disponible pour les utilisateurs via le Magasin Teams.  <br>**Voir aussi :** [Instructions de validation de Store](#s) |
| [Teams workbench](../sbs-gs-spfx.yml) | Workbench dans Visual Studio Code utilisé lors de la génération pour les applications Teams créées à l’aide de SPFx et de Teams Toolkit. <br>**Voir aussi** : [Workbench](#w) ; [Workbench local](#l) |

## <a name="u"></a>U

| Terme | Définition |
| --- | --- |
| [Composants interface utilisateur](../concepts/design/design-teams-app-basic-ui-components.md) | Pour le développement d’applications Teams, vous pouvez utiliser des composants d’interface utilisateur Fluent pour créer votre application à partir de zéro. |
| [Modèles d’interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) | Pour le développement d’applications Teams, vous pouvez utiliser des modèles d’interface utilisateur Teams pour concevoir rapidement vos applications. |
| [Actions universelles pour les cartes adaptatives](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) | Un moyen d’implémenter des cartes adaptatives sur plusieurs plateformes et applications. Il utilise un bot comme back-end commun pour gérer les actions. |

## <a name="v"></a>V

| Terme | Définition |
| --- | --- |
| [Virtual Assistant](../samples/virtual-assistant.md) | Modèle open source Microsoft qui vous permet de créer une solution conversationnelle robuste. |

## <a name="w"></a>W

| Terme | Définition |
| --- | --- |
| [URL du site web](../tabs/design/tabs-mobile.md) | Une propriété du fichier manifeste de l'application (`websiteUrl`) qui relie l'application au site Web de l'organisation ou à la page de renvoi du produit concerné. Il s'agit d'une configuration obligatoire pour le client mobile Teams. <br>**Voir aussi :** [Manifeste de l’application](#a) ; [Teams Mobile](#t) |
| [Application web](../samples/integrate-web-apps-overview.md) | Application qui s’exécute sur un serveur web. Il peut être intégré à la plateforme Microsoft Teams. |
| [Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) | Il s’agit d’une fonctionnalité d’une application Teams utilisée pour l’intégrer à des applications externes. <br>**Voir aussi** : webhook entrant ; webhook sortant |
| [Composant WebPart](../sbs-gs-spfx.yml) | Composant d’interface utilisateur utilisé pour créer une page ou un site dans une application Teams créée à l’aide de Visual Studio Code et SharePoint Framework. <br>**Voir aussi** : [SPFx](#s) |
| [Workbench](../sbs-gs-spfx.yml) | Visual Studio Code d’interface utilisateur globale qui englobe les composants de l’interface utilisateur, tels que la barre de titre, le panneau, etc. <br>**Voir aussi** : [Workbench local](#l) ; [Teams workbench](#t) |

## <a name="y"></a>v

| Terme | Définition |
| --- | --- |
| [YoTeams](../get-started/get-started-overview.md) | Kit de ressources de développement pour la création d’applications Microsoft Teams basées sur TypeScript et node.js. |
