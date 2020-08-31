---
title: Nouveautés
description: Décrit toutes les nouvelles fonctionnalités de développement de Microsoft teams
keywords: Nouveautés de teams
ms.openlocfilehash: 46e18dbe385680fea38c98f4396047a8d10a2b9c
ms.sourcegitcommit: b3962a7b36f260aef1af9124d14d71ae08b01ac4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2020
ms.locfileid: "47303716"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Nouveautés pour les développeurs dans Microsoft teams

>[!TIP]
> Consultez nos modèles prêts pour la production dans le   [**catalogue des modèles d’applications teams**](samples/app-templates.md). Le catalogue est classé par ordre alphabétique et les compléments les plus récents sont balisés avec une étoile **&#9734;**.

## <a name="change-log"></a>Journal des modifications

Le journal des modifications répertorie les modifications apportées à la plateforme Microsoft teams et à cet ensemble de documents. Les entrées peuvent être utilisées pour attirer l’attention sur une nouvelle fonctionnalité qui est simplement intéressante pour les développeurs de teams.

| **Date** | **Notes** | **Rubriques modifiées** |
| -------- | --------- | ------------------ |
| 08/12/2020 |Prise en charge des cartes adaptatives dans le webhook entrant déplacée vers GA.|[Envoyer des cartes adaptatives à l'aide d'un webhook entrant](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
| 07/22/2020 |Mises à jour des capacités des appareils mobiles.|[Demander des autorisations de périphérique pour votre onglet Microsoft teams](~/tabs/how-to/native-device-permissions.md) |
|07/20/2020|Outil de validation des applications teams pour les envois AppSource.|[Outil de validation des applications teams](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)
|07/15/2020|Créer un assistant virtuel pour teams|[Assistant virtuel pour Microsoft teams](samples/virtual-assistant.md)|
|07/14/2020|Revêtement d’une documentation d’indicateur de chargement natif|[Affichage d’un indicateur de chargement natif](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Commencer à créer des applications teams à l’aide de Visual Studio code Toolkit.|[Créer des applications avec Microsoft teams Toolkit et Visual Studio code](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Authentification unique pour les onglets GA pour les clients Web et de bureau teams|[Authentification unique (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| Schéma de manifeste mis à jour vers la version 1,7| [Référence : schéma de manifeste pour Microsoft teams](resources/schema/manifest-schema.md)|
| 05/20/2020 | Les autorisations de consentement propres aux ressources à l’aide des API Microsoft Graph sont dans la version préliminaire pour les développeurs. |[Consentement propre à la ressource (RSC) — Aperçu pour les développeurs](graph-api/rsc/resource-specific-consent.md) |
|5/18/2020|Intégrer des agents virtuels de puissance à teams|[Intégration d’un système d’agents virtuels chatbot à Microsoft teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Intégration de systèmes WFM avec le connecteur de mutations pour teams|[Microsoft teams décale les connecteurs WFM](samples/shifts-wfm-connectors.md)
| 03/24/2020 | Ajout de la prise en charge de la récupération d’un membre d’une conversation et de la prise en charge supplémentaire pour la récupération des membres de la page. | [Obtenir un contexte Teams pour votre bot](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | Le `replyToId` paramètre dans les charges utiles envoyées à un bot n’est plus chiffré, ce qui vous permet d’utiliser cette valeur pour construire deeplinks à ces messages. Les charges utiles de message incluent les valeurs chiffrées dans le paramètre. `legacy.replyToId`.  |
| 11/5/2019 | L’authentification unique à l’aide du kit de développement logiciel (SDK) Team JavaScript dans une page de contenu Web est dans l’aperçu développeur. | [Authentification unique](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | La documentation sur les robots de conversation et les extensions de messagerie mise à jour pour refléter le kit de développement logiciel (SDK) de robot 4,6. La documentation du kit de développement logiciel (SDK) v3 est disponible dans la section ressources. | Tout le robot et la documentation d’extension de messagerie. |
| 10/31/2019 | Nouvelle structure de la documentation et refactorisation d’article principal. Veuillez signaler les liens morts ou les 404s en créant un problème GitHub. | Tous! |
| 9/13/2019 | Le moteur de demande est installé à partir de l’extension de messagerie basée sur une action. | [Initier des actions à l’aide des extensions de messagerie](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | Prise en charge des canaux privés dans les onglets et les connecteurs. | [Obtenir le contexte de votre onglet](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | Partager un site Web externe, depuis un site Web externe, vers un canal Teams. | [Partager avec teams](~/share-to-teams.md) |
| 05/25/2019 | Répondre avec un message bot à partir du module de tâche. | [Répondre avec un message de robot à partir du module de tâche](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Robots dans les conversations de groupe. | [Interagir avec un bot dans une conversation ou un canal de groupe](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Localisation de manifeste d’application. | [Localisation de l’application](~/publishing/apps-localization.md) |
| 05/20/2019 | Actions de message. | [Actions de message](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Link unfurling (aperçus d’URL personnalisées). | [Déploiement de lien](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Programme de certification d’application pour les applications du Store. | [Certification d’application](~/publishing/application-certification.md) |
| 05/06/2019 | Les modèles d’application sont maintenant disponibles. | [Modèles d’application](~/samples/app-templates.md) |
| 04/23/2019 | Les extensions de messagerie basées sur les actions sont désormais disponibles. | [Extensions de message basées sur des actions](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | Il n’est pas possible de créer des liens approfondis vers la conversation privée pour les développeurs. | [Liaison profonde à une conversation](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | LicenceType les informations SKU et les informations de référence dans le contexte d’onglet. | [Contexte d’onglet](~/concepts/tabs/tabs-context.md) |
| 11/12/2018 | Les onglets de la conversation de groupe sont désormais disponibles dans la version finale de teams et ont été déplacés de l’aperçu développeur. Dans le cadre de cette tâche, la section onglets a été retravaillée pour plus de clarté.| [Onglets configurables](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | La mise en route du nœud JS et de .NET/C# a été mise à jour pour utiliser app Studio dans Teams, et une nouvelle section a été ajoutée sur les applications teams basées sur des nœuds d’hébergement dans Azure. | [Prise en main de la plateforme Microsoft teams avec C#/.net et App Studio](~/get-started/get-started-dotnet-app-studio.md),  [prise en main de la plateforme Microsoft teams avec node JS and App Studio](~/get-started/get-started-nodejs-app-studio.md), [héberger votre application de nœud teams dans Azure](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | Vous pouvez désormais créer des liens détaillés vers des conversations privées entre les utilisateurs. | [Liaison profonde à une conversation](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1,7 a été livré avec une nouvelle fonctionnalité d’utilisation de l’onglet Microsoft teams en tant que composant WebPart SharePoint Framework. | [Onglets dans SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | La fonctionnalité « module de tâche » a été publiée. Un module de tâches vous permet de créer des expériences de menu contextuel modal dans votre application Teams, à partir des robots et des onglets. À l’intérieur de la fenêtre contextuelle, vous pouvez exécuter votre propre code HTML/JavaScript personnalisé, afficher un `<iframe>` widget basé sur une vidéo YouTube ou une vidéo Microsoft Stream, ou afficher une [carte adaptative](https://docs.microsoft.com/adaptive-cards/). | [Vue d’ensemble du module de tâche](~/concepts/task-modules/task-modules-overview.md), [module tâches dans les onglets](~/concepts/task-modules/task-modules-tabs.md),  [module de tâches dans les robots](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | Les informations de mise en forme pour les cartes ont été mises à jour et testées sur les clients de bureau, iOS et Android pour Teams. | [Cartes](~/concepts/cards/cards.md), [mise en forme de carte](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Les appels et les API de réunion en ligne pour Microsoft Graph ont été publiés dans la version bêta, et les applications teams peuvent désormais interagir avec les utilisateurs de manière enrichie à l’aide de la voix et de la vidéo. | [Appels et robots de réunions en ligne](~/concepts/calls-and-meetings/registering-calling-bot.md), [concepts de média en temps réel](~/concepts/calls-and-meetings/real-time-media-concepts.md), [enregistrement d’un bot appelant](~/concepts/calls-and-meetings/registering-calling-bot.md), [débogage et test local](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md), [multimédia hébergé par l’application](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md), [gestion des notifications d’appels entrants](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Les pages de configuration d’onglet sont maintenant sensiblement plus haut. | [Création d’onglets](tabs/design/tabs.md) |
| 08/15/2018 | Les cartes adaptatives sont désormais prises en charge dans Teams.|[Actions de carte adaptative dans teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | La prise en charge des clients pour DevTools a été documentée pour les développeurs.| [DevTools pour le client de bureau Microsoft teams](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Les extensions de messagerie prennent désormais en charge plusieurs commandes. Cette fonctionnalité a été en version préliminaire pour les développeurs et est désormais publiée sur tous les utilisateurs.| [composeExtensions. Commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | La configuration incorporée est désormais prise en charge dans les connecteurs. La documentation sur les connecteurs a également été révisée et étendue pour plus de clarté.| [Connecteurs](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Votre robot peut désormais envoyer et recevoir des fichiers.| [Envoyer et recevoir des fichiers via votre robot](~/concepts/bots/bots-files.md)|
| 07/27/2018 | L’Aperçu pour les développeurs prend désormais en charge plusieurs commandes dans les extensions de messagerie. | [Extensions de messagerie étendues](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | Des informations sur la nouvelle certification d’application ont été ajoutées à la section publication. |[Autorisations de manifeste](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | En mode Aperçu pour les développeurs, davantage d’espace a été alloué à la page de configuration de l’onglet. | [La page Configuration de l’onglet est beaucoup plus haute](tabs/design/tabs.md#configuration-page-height)|
| 07/12/2018 | Informations sur l’accès invité. | [Accès invité dans Microsoft Teams](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Les informations de version préliminaire du catalogue d’applications client Microsoft teams ont été ajoutées. | [Publier votre application Microsoft teams](~/publishing/apps-publish.md)|
| 05/31/2018 | Team Developer Preview (Ring 3,6) a été mis à jour pour inclure la possibilité d’ajouter des robots et des onglets à Group chat. | [Fonctionnalités dans l’aperçu du développeur, le schéma d'](~/resources/dev-preview/developer-preview-features.md) [Aperçu développeur](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | Les cartes adaptatives sont désormais prises en charge dans teams dans les [actions de carte adaptative dans teams](task-modules-and-cards/cards/cards-reference.md). |
| 05/29/2018 | Si vous utilisez la version [préliminaire pour développeurs](~/resources/dev-preview/developer-preview-intro.md), votre robot peut désormais envoyer et recevoir des fichiers.| [Envoyer et recevoir des fichiers via votre robot](~/concepts/bots/bots-files.md), [fonctionnalités de la version préliminaire pour développeurs de Microsoft teams](~/resources/dev-preview/developer-preview-features.md)|
| 04/17/2018 | replyToID a été ajouté à la charge utile pour `Invoke` les `MessageBack` actions de carte et. Ceci est particulièrement utile si vous devez mettre à jour le message depuis lequel l’action de la carte provient. | [Actions de carte](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Ajout de cette rubrique pour suivre les modifications apportées à l’interface de programmation de teams et à cette documentation. | [Nouveautés](~/whats-new.md)|
| 04/10/2018 | Modification des URL d’authentification de manière à ce qu’elles utilisent l’ID de client dans le chemin d’accès. | [Flux d’authentification pour les onglets](~/concepts/authentication/auth-flow-tab.md), [authentification AAD de l’onglet](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | Ajout d’instructions de conception pour l’utilisation de la zone de commande. |[Zone de commande](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Utilisation de robots pour envoyer des notifications pour votre application. |[Bots avec notification seulement](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Documentation étendue pour la messagerie proactive. |[Démarrer une conversation](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Refactorisation de la documentation pour les cartes. |[Cartes](~/concepts/cards/cards.md), [actions de carte](~/concepts/cards/cards-actions.md), [format](~/concepts/cards/cards-format.md)de carte, [référence de carte](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Ajout de la documentation de teams App Studio. |[Développer rapidement des applications avec teams App Studio](~/get-started/get-started-app-studio.md), [à l’aide de la bibliothèque de contrôles dans App Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Ajout d’un exemple de code pour illustrer la méthode AsTeamsChannelAccounts (). |[Obtenir le contexte de votre robot](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Ajout de rubriques pour commencer à utiliser C#. |[Prise en main de la plateforme Microsoft Teams avec C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>Envoyer vos questions, bogues, demandes de fonctionnalité et contributions

Nous écoutons la communauté des développeurs sur [plusieurs canaux](feedback.md).
