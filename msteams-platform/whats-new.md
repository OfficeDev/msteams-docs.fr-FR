---
title: Nouveautés
description: Décrit toutes les nouvelles fonctionnalités de développement dans Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: nouveautés des équipes
ms.openlocfilehash: b9ef7cbe1a7fa1a673a60375bab893a86c2dbf6b
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335353"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Nouveautés pour les développeurs dans Microsoft Teams

Découvrez Microsoft Teams fonctionnalités de plateforme généralement disponibles (GA) et dans la prévisualisation du développeur.

## <a name="ga-features"></a>Fonctionnalités ga

Microsoft Teams fonctionnalités de plateforme qui sont disponibles pour tous les développeurs d’applications.

<br>

<details>

<summary><b>2021</b></summary>

| **Date** | **Notes** | **Rubriques modifiées** |
| -------- | --------- | ------------------ |
|07/08/2021|L’extensibilité des applications de réunion est disponible sur les appareils mobiles. Les clients mobiles supportent les applications pendant la réunion. |[Extensibilité de l’application de réunion](apps-in-teams-meetings/meeting-app-extensibility.md)|
|06/28/2021|Intégrer la fonctionnalité s’il s’est s’il s’est s’il s'|[Intégrer Sélecteur de personnes fonctionnalité](concepts/device-capabilities/people-picker-capability.md)|  
|06/25/2021| Introduction du guide pas à pas pour envoyer des messages proactifs. | [Guide pas à pas pour envoyer des messages proactifs](sbs-send-proactive.yml) |
|06/09/2021| Vue d’étape pour les images dans les cartes adaptatives avec `allowExpand` attribut. | [Vue d’étape des images dans les cartes adaptatives](~/task-modules-and-cards/cards/cards-format.md) |
|05/31/2021| Onglets de conversation. | [Démarrer et poursuivre des conversations sur le contenu de vos onglets](~/tabs/how-to/conversational-tabs.md) |
|05/24/2021| Mise à jour Teams recommandations en matière de conception d’application avec des modèles mobiles et bien plus encore.|[Conception de votre application Teams web](~/concepts/design/design-teams-app-overview.md)
|05/13/2021| Ajout d’informations sur mConnect et Skooler.|[Système de gestion de l’apprentissage par le chat](resources/moodle-overview.md)
|05/10/2021| La version 1.10 du manifeste est publiée.|[Schéma du manifeste](resources/schema/manifest-schema.md) |
|05/10/2021| Nouvelle fonctionnalité de personnalisation d’application.| [Activer les orgs pour personnaliser votre application](concepts/design/enable-app-customization.md) |
|05/07/2021| Liens profonds pour les appels audio et vidéo dans la conversation. |[Liens profonds](concepts/build-and-test/deep-links.md#deep-linking-to-an-audio-or-audio-video-call) |
|04/30/2021|De nouveaux conseils sur la publication d’applications dans Teams store.|[Publier votre application dans le Teams, Teams](concepts/deploy-and-publish/appsource/publish.md) [de validation du Store](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) |
|04/29/2021 | Actions universelles pour les cartes adaptatives. | [Actions universelles pour les cartes adaptatives](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|04/29/2021 | Affichages spécifiques à l’utilisateur. | [Affichages spécifiques à l’utilisateur](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/User-Specific-Views.md) |
|04/29/2021 | Flux de travail séquentiels. | [Flux de travail séquentiels](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Sequential-Workflows.md) |
|04/29/2021 | Cartes à jour. | [Cartes actualisées](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Up-To-Date-Views.md) |
|04/08/2021| Fonctionnalité de personnalisation d’application.|[Présentation de l’application Design Teams,](concepts/design/enable-app-customization.md) [vue d’ensemble d’App Studio](concepts/build-and-test/app-studio-overview.md#connectors)et [schéma de manifeste](resources/schema/manifest-schema-dev-preview.md) |
|03/18/2021|Remarque : mettez à jour la version 4.10 ou supérieure du SDK Bot Framework, car nous avons commencé avec le processus de dérision pour `TeamsInfo.getMembers` et `TeamsInfo.GetMembersAsync` . | [Modifications de l’API du bot pour les membres de l’équipe/de la conversation](resources/team-chat-member-api-changes.md) |
|03/05/2021|Remarque : les onglets n’auront plus de marges autour de leur expérience. Les développeurs d’onglets doivent examiner et mettre à jour leurs applications. | [Suppression des marges de tabulation](resources/removing-tab-margins.md) |
|03/05/2021|Étendue d’installation et fonctionnalité de groupe par défaut.| [Étendue d’installation et fonctionnalité de groupe par défaut](concepts/deploy-and-publish/add-default-install-scope.md) |
|03/05/2021|Réordez les onglets des applications personnelles.|[Réordesser l’onglet de conversation dans les applications personnelles](tabs/how-to/create-personal-tab.md#reorder-static-personal-tabs)|
|03/04/2021|Masquage d’informations dans les cartes adaptatives.| [Masquage d’informations dans les cartes adaptatives](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|Ajout de fonctionnalités d’emplacement. <br/> Les informations sur les fonctionnalités d’emplacement sont ajoutées dans la vue d’ensemble des fonctionnalités de l’appareil, les autorisations natives des appareils, l’intégration des fonctionnalités multimédias et les fichiers de fonctionnalités de scanneur de QR ou de code-barres.|[Vue](concepts/device-capabilities/device-capabilities-overview.md) [d’ensemble, demander des autorisations](concepts/device-capabilities/native-device-permissions.md)d’appareil, intégrer des [fonctionnalités multimédias,](concepts/device-capabilities/mobile-camera-image-permissions.md)intégrer des fonctionnalités [de scanneur de QR](concepts/device-capabilities/qr-barcode-scanner-capability.md)ou de code-barres, intégrer [des fonctionnalités d’emplacement](concepts/device-capabilities/location-capability.md) |
|02/18/2021|Ajout de la fonctionnalité de QR ou de scanneur de code-barres. <br/> Les informations sur les fonctionnalités de QR ou de scanneur de code-barres sont ajoutées dans la vue d’ensemble des fonctionnalités de l’appareil, les autorisations natives de l’appareil et l’intégration des fichiers de fonctionnalités multimédias.|[Vue d’ensemble,](concepts/device-capabilities/device-capabilities-overview.md) [demander des autorisations d’appareil,](concepts/device-capabilities/native-device-permissions.md) [intégrer des fonctionnalités multimédias,](concepts/device-capabilities/mobile-camera-image-permissions.md)intégrer la QR ou la fonctionnalité de [scanneur de code-barres](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|Vue d’ensemble des fonctionnalités d’appareil ajoutées. <br/> Les informations sur les fonctionnalités du microphone sont ajoutées dans les autorisations d’appareil natives et intègrent les fichiers de fonctionnalités multimédias.|[Vue d’ensemble,](concepts/device-capabilities/device-capabilities-overview.md) [demander des autorisations d’appareil,](concepts/device-capabilities/native-device-permissions.md) [intégrer des fonctionnalités multimédias](concepts/device-capabilities/mobile-camera-image-permissions.md)|

<br>

</details>

<br>

<details>
  
<summary><b>2020</b></summary>

| **Date** | **Notes** | **Rubriques modifiées** |
| -------- | --------- | ------------------ |
|11/30/2020|Intégration de la plateforme d’identité Teams Shared Computer Toolkit et Visual Studio Code pour les onglets.|[Authentification unique avec authentification Teams Shared Computer Toolkit et Visual Studio Code pour les onglets](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Teams manifeste de l’application mis à jour vers la version 1.8.|[Référence : schéma de manifeste pour Microsoft Teams](resources/schema/manifest-schema.md)|
|11/10/2020|Teams recommandations en matière de conception de bot.|[Recommandations en matière de conception de bot](bots/design/bots.md)|
|09/30/2020|L’envoi et la réception de fichiers à des bots sur des appareils mobiles sont désormais pris en charge.|[Envoyer et recevoir des fichiers via votre bot](resources/bot-v3/bots-files.md)|
|09/22/2020|Nouvelles informations sur la mise en place Teams développement.|[Créer votre première vue d’Teams application](build-your-first-app/build-first-app-overview.md)|
|09/18/2020|Prise en charge des applications Teams réunion (version préliminaire).|[Créer des applications pour Teams réunions et](apps-in-teams-meetings/create-apps-for-teams-meetings.md) des applications dans Teams [réunions](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|08/19/2020|Importez Teams messages avec Microsoft Graph.|[Importer des messages de plateforme tierces pour les équipes à l’aide de Microsoft Graph](graph-api/import-messages/import-external-messages-to-teams.md)
|08/12/2020 |Prise en charge des cartes adaptatives dans le webhook entrant déplacé vers ga.|[Envoyer des cartes adaptatives à l'aide d'un webhook entrant](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|Commencer à créer Teams applications avec le Visual Studio Shared Computer Toolkit.|[Créer des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code](toolkit/visual-studio-overview.md) |
|08/06/2020|Prise en charge de l’authentification sso tabs.|[Développer un onglet DSO Microsoft Teams SSO](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Graph des bots et des messages proactifs (prévisualisation publique).|[Activer l’installation proactive du bot et la messagerie proactive dans Teams avec Microsoft Graph](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
|07/22/2020 |Mises à jour des fonctionnalités des appareils mobiles.|[Demander des autorisations d’appareil pour Microsoft Teams onglet](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|Teams Outil de validation d’application pour les soumissions AppSource.|[Teams Outil de validation d’application](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
|07/15/2020|Créez un assistant virtuel pour Teams.|[Virtual Assistant pour Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|Surfacing a native loading indicator documentation.|[Affichage d’un indicateur de chargement natif](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Commencer à créer Teams applications avec le Visual Studio Code Shared Computer Toolkit.|[Créer des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Sign-on unique for tabs GA for Teams web and desktop clients.|[Single Sign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| Schéma de manifeste mis à jour vers la version 1.7.| [Référence : schéma de manifeste pour Microsoft Teams](resources/schema/manifest-schema.md)|
|05/18/2020|Intégrez Power Virtual Agents avec Teams.|[Intégrer un chatbot Power Virtual Agents avec Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Intégrez des systèmes WFM à Shifts Connector pour Teams.|[Microsoft Teams Déplace les connecteurs WFM](samples/shifts-wfm-connectors.md)
|03/24/2020 | Prise en charge supplémentaire pour la récupération d’un seul membre d’une conversation et prise en charge supplémentaire pour la récupération des membres pagagés. | [Obtenir un contexte Teams pour votre bot](~/bots/how-to/get-teams-context.md) |

<br>

</details>

<br>

<details>
  
<summary><b>2019</b></summary>

| **Date** | **Notes** | **Rubriques modifiées** |
| -------- | --------- | ------------------ |
| 12/26/2019 | Le `replyToId` paramètre dans les charges utiles envoyées à un bot n’est plus chiffré, ce qui vous permet d’utiliser cette valeur pour créer des liens profonds vers ces messages. Les charges utiles de message incluent les valeurs chiffrées dans le paramètre `legacy.replyToId` .  |
| 11/05/2019 | Sign-on unique using the Teams JavaScript SDK. | [Authentification unique](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | Mise à jour de la documentation sur les bots de conversation et les extensions de messagerie pour refléter le SDK Bot Framework 4.6. La documentation relative au SDK v3 est disponible dans la section Ressources. | Documentation complète sur les bots et les extensions de messagerie. |
| 10/31/2019 | Nouvelle structure de la documentation et refactoriser les articles principaux. Signalez les liens morts ou les 404 en créant un GitHub. | Tous! |
| 09/13/2019 | Le bot de demande est installé à partir de l’extension de messagerie basée sur l’action. | [Lancer des actions avec des extensions de messagerie](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 08/28/2019 | Prise en charge des canaux privés dans les onglets et les connecteurs. | [Obtenir un contexte Teams pour votre onglet](tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) |
| 06/20/2019 | Partagez un site web externe, à partir d’un site web externe, dans un canal Teams externe. | [Partager avec Teams](~/share-to-teams.md) |
| 05/25/2019 | Répondez avec un message de bot à partir du module de tâche. | [Répondre avec un message bot à partir du module de tâche](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Bots dans les conversations de groupe. | [Interagir avec un bot dans une conversation de groupe ou un canal](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Localisation du manifeste de l’application. | [Localisation d’application](~/publishing/apps-localization.md) |
| 05/20/2019 | Actions de message. | [Message Actions](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Déploiement de lien (aperçus d’URL personnalisées). | [Déploiement de lien](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Programme de certification des applications du Windows Store. | [Certification des applications](~/concepts/deploy-and-publish/appsource/post-publish/overview.md#complete-microsoft-365-certification) |
| 05/06/2019 | Les modèles d’application sont désormais disponibles. | [Modèles d’application](~/samples/app-templates.md) |
| 04/23/2019 | Les extensions de messagerie basées sur l’action sont désormais disponibles. | [Extensions de message basées sur l’action](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | Création de liens profonds vers une conversation privée. | [Liaison profonde à une conversation](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | Surfacing SKU and licenceType information in the tab context. | [Contexte de l’onglet](~/concepts/tabs/tabs-context.md) |

<br>

</details>

<br>

<details>

<summary><b>2018</b></summary>

| **Date** | **Notes** | **Rubriques modifiées** |
| -------- | --------- | ------------------ |
| 11/12/2018 | Les onglets de la conversation de groupe sont désormais disponibles dans la version finale de Teams. Dans le cadre de ce travail, la section Onglets a été retravaillée pour plus de clarté.| [Onglets configurables](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | La mise en place de Node JS et de .NET/C# a été mise à jour pour utiliser App Studio dans Teams et une nouvelle section a été ajoutée sur l’hébergement d’applications Teams node dans Azure. | Commencer à travailler sur la plateforme Microsoft Teams avec [C#/.NET](~/get-started/get-started-dotnet-app-studio.md)et App Studio, commencer sur la plateforme Microsoft Teams avec [Node JS](~/get-started/get-started-nodejs-app-studio.md)et App Studio, héberger votre application [node Teams dans Azure](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | Vous pouvez désormais créer des liens profonds vers des conversations privées entre les utilisateurs. | [Liaison profonde à une conversation](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1.7 a été livré et une nouvelle fonctionnalité permet d’utiliser Microsoft Teams’onglet en tant que SharePoint Framework web. | [Onglets dans SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | La **fonctionnalité de module** de tâche a été publiée. Un module de tâche vous permet de créer des expériences popup modales dans votre application Teams, à partir de bots et d’onglets. À l’intérieur de la fenêtre popup, vous pouvez exécuter votre propre code HTML/JavaScript personnalisé, afficher un widget basé sur un widget tel qu’une vidéo YouTube ou Microsoft Stream, ou afficher une carte `<iframe>` [adaptative.](/adaptive-cards/) | [Vue d’ensemble du module de](~/concepts/task-modules/task-modules-overview.md) [tâche, module de tâche dans les onglets,](~/concepts/task-modules/task-modules-tabs.md)  [module de tâche dans les bots](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | Les informations de mise en forme des cartes ont été mises à jour et testées dans les clients de bureau, iOS et Android pour Teams. | [Cartes](~/concepts/cards/cards.md), [mise en forme de carte](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Les appels et les API de réunion en ligne pour Microsoft Graph ont été publiés en version bêta et les applications Teams peuvent désormais interagir avec les utilisateurs de manière enrichie à l’aide de la voix et de la vidéo. | [Appels et bots](~/concepts/calls-and-meetings/registering-calling-bot.md)de réunions en ligne, [concepts](~/concepts/calls-and-meetings/real-time-media-concepts.md)multimédias en temps réel, inscription d’un [bot](~/concepts/calls-and-meetings/registering-calling-bot.md)d’appel, débogage et test [local,](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)support hébergé par [l’application](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md), gestion des notifications d’appels [entrants](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Les pages de configuration d’onglets sont désormais beaucoup plus grandes. | [Création d’onglets](tabs/design/tabs.md) |
| 08/15/2018 | Les cartes adaptatives sont désormais Teams.|[Actions de carte adaptative dans Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | Prise en charge du client pour DevTools.| [DevTools pour le client Microsoft Teams bureau](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Les extensions de messagerie prend désormais en charge plusieurs commandes. | [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | La configuration en ligne est désormais prise en charge dans les connecteurs. La documentation des connecteurs a également été révisée et étendue pour des raisons de clarté.| [Connecteurs](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Votre bot peut désormais envoyer et recevoir des fichiers.| [Envoyer et recevoir des fichiers via votre bot](~/bots/how-to/bots-filesv4.md)|
| 07/23/2018 | Des informations sur la nouvelle certification des applications ont été ajoutées à la section Publication. |[Autorisations de manifeste](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | Davantage d’espace a été alloué à la page de configuration de l’onglet. | [La page de configuration de l’onglet est beaucoup plus grande](tabs/design/tabs.md)|
| 07/12/2018 | Informations sur l’accès invité. | [Accès invité dans Microsoft Teams](/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Des informations sur Microsoft Teams catalogue d’applications client ont été ajoutées. | [Publier votre application Microsoft Teams web](~/publishing/apps-publish.md)|
| 05/29/2018 | Les cartes adaptatives sont pris en charge Teams. | [Actions de carte adaptative dans Teams](task-modules-and-cards/cards/cards-reference.md) |
| 04/17/2018 | ReplyToID a été ajouté à la charge utile pour les `Invoke` actions de carte et les actions de `MessageBack` carte. Ceci est particulièrement utile si vous devez mettre à jour le message dont l’action de carte est d’provenance. | [Actions de carte](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Ajout de cette rubrique pour suivre les modifications apportées à l’interface Teams programmation et à cet ensemble de documentation. | [Nouveautés](~/whats-new.md)|
| 04/10/2018 | URL d’authentification modifiées pour utiliser de manière cohérente l’ID de client dans le chemin d’accès. | [Flux d’authentification pour les onglets,](~/concepts/authentication/auth-flow-tab.md) [authentification par onglets AAD](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | Ajout d’instructions de conception pour l’utilisation de la zone de commande. |[Zone de commande](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Utilisation de bots pour envoyer des notifications pour votre application. |[Bots avec notification seulement](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Documentation étendue pour la messagerie proactive. |[Démarrer une conversation](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Documentation refactorisante pour les cartes. |[Cartes,](~/concepts/cards/cards.md) [actions de carte,](~/concepts/cards/cards-actions.md) [mise en forme de carte,](~/concepts/cards/cards-format.md) [référence de carte](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Ajout de la documentation Teams App Studio. |[Développer rapidement des applications avec Teams App Studio](~/get-started/get-started-app-studio.md), à l’aide de la bibliothèque de [contrôles dans App Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Ajout d’un exemple de code pour démontrer la méthode AsTeamsChannelAccounts(). |[Obtenir un contexte pour votre bot](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Ajout de rubriques pour commencer à utiliser C#. |[Prise en main de la plateforme Microsoft Teams avec C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

<br>

</details>

## <a name="developer-preview"></a>Aperçu pour les développeurs

La prévisualisation pour développeurs est un programme public qui fournit un accès en avant-première aux fonctionnalités Teams plateforme.  

| **Date** | **Notes** | **Rubriques modifiées** |
| -------- | --------- | ------------------ |
|06/23/2021| API Détails de la réunion et événements de Teams en temps réel. | [Créer des applications pour les réunions Teams](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-details-api) |
|06/21/2021|Comportement de désinstallation pour une application personnelle avec un bot | [Désinstaller les mises à jour de comportement dans les applications personnelles avec des bots](bots/how-to/conversations/subscribe-to-conversation-events.md#uninstall-behavior-for-personal-app-with-bot)|
|06/16/2021| Consentement spécifique aux ressources pour les conversations. |[Consentement spécifique à la](graph-api/rsc/resource-specific-consent.md)ressource , [Tester les autorisations](graph-api/rsc/test-resource-specific-consent.md) de consentement spécifiques à la ressource dans Teams|  
|05/26/2021|Créer des onglets avec les Cartes adaptatives|[Créer des onglets](tabs/how-to/build-adaptive-card-tabs.md)|
|05/25/2021| Mise à jour Teams Shared Computer Toolkit pour [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) et [Visual Studio](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit&ssr=false#overview). | [Prendre en Teams développement d’applications](~/get-started/prerequisites.md) |
|05/25/2021| Nouveau portail pour les développeurs Teams pour la gestion de vos applications Teams de développement. | [Documentation pour les développeurs](concepts/build-and-test/teams-developer-portal.md) |
|05/25/2021| La fonctionnalité de scènes en mode ensemble personnalisé combine les participants dans une scène virtuelle unique et place leurs flux vidéo dans des sièges pré-déterminés. | [Scènes personnalisées en mode ensemble](~/apps-in-teams-meetings/teams-together-mode.md) |
|05/24/2021|Les bots peuvent être activés pour recevoir tous les messages de canal à l’aide du consentement spécifique aux ressources (RSC).|[Recevoir tous les messages avec RSC,](~/bots/how-to/conversations/channel-messages-with-rsc.md)vue d’ensemble [de la conversation de bot,](~/bots/how-to/conversations/conversation-basics.md) [conversations](~/bots/how-to/conversations/channel-and-group-conversations.md)de canal et de groupe et schéma de manifeste d’aperçu [développeur](~/resources/schema/manifest-schema-dev-preview.md) |
|05/21/2021|Déploiement de liens d’onglets et vue d’étape|[Déploiement de liens d’onglets et vue d’étape](tabs/tabs-link-unfurling.md) |
|03/05/2021| Les onglets n’auront plus de marges autour de leur expérience. Les développeurs d’onglets doivent examiner et mettre à jour leurs applications. | [Suppression des marges de tabulation](resources/removing-tab-margins.md) |

Pour plus d’informations, voir [la prévisualisation pour](~/resources/dev-preview/developer-preview-intro.md)les développeurs publics Teams .

## <a name="teams-app-template-catalog"></a>Teams catalogue de modèles d’application

En plus de nouvelles fonctionnalités, nous fournissons également des [modèles](samples/app-templates.md) d’application Teams prêt pour la production que vous pouvez déployer immédiatement ou modifier selon vos besoins. Les modèles nouvellement ajoutés sont indiqués par une étoile ..

## <a name="submit-your-feedback"></a>Envoyer vos commentaires

Nous encourageons Teams développeurs à poser des questions, à déposer des bogues, à soumettre des demandes de fonctionnalités et à apporter des contributions. Vous pouvez envoyer des commentaires via l’un des [canaux disponibles.](feedback.md)
