---
title: Ajouter des fonctionnalités à vos applications Teams
author: MuyangAmigo
description: Dans ce module, découvrez comment ajouter des fonctionnalités du Kit de ressources Teams, des avantages, des limitations et des fonctionnalités
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 81cddad2297ec526f94a3ab362422028b14b4598
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2022
ms.locfileid: "66557987"
---
# <a name="add-capabilities-to-teams-apps"></a>Ajouter des fonctionnalités aux applications Teams

L’ajout d’une fonctionnalité dans le Kit de ressources Teams vous permet d’ajouter des fonctionnalités supplémentaires à votre application Teams existante. Le tableau suivant répertorie les fonctionnalités de l’application Teams :

|**Fonctionnalité**|**Description**|
|--------|-------------|
| Onglets |  Les onglets sont des balises HTML simples qui font référence aux domaines déclarés dans le manifeste de l’application. Vous pouvez ajouter des onglets dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel.|
| Bots |  Les bots permettent d’interagir avec votre service web par le biais de texte, de cartes interactives et de modules de tâches.|
| Extensions de messages | Les extensions de message permettent d’interagir avec votre service web via des boutons et des formulaires dans le client Microsoft Teams.|

## <a name="advantages"></a>Avantages

La liste suivante présente des avantages pour ajouter d’autres fonctionnalités dans TeamsFx :

* Fournit des commodités.
* Ajoute plus de fonction à votre application en ajoutant automatiquement des codes sources à l’aide du Kit de ressources Teams.

## <a name="limitations"></a>Limites

La liste suivante fournit des limitations pour ajouter d’autres fonctionnalités dans TeamsFx :

* Vous pouvez ajouter des onglets jusqu’à 16 instances.
* Vous pouvez ajouter un bot et une extension de message pour une instance chacune.

## <a name="add-capabilities"></a>Ajouter des fonctionnalités

**Vous pouvez ajouter des fonctionnalités en suivant les méthodes suivantes :**

* Pour ajouter des fonctionnalités à l’aide du Kit de ressources Teams dans Visual Studio Code.
* Pour ajouter des fonctionnalités à l’aide de la palette de commandes.

  > [!Note]
  > Vous devez provisionner pour chaque environnement, une fois que vous avez ajouté les fonctionnalités dans votre application Teams.

* **Pour ajouter des fonctionnalités à l’aide du Kit de ressources Teams dans Visual Studio Code :**

   1. Ouvrez **Visual Studio Code**.
   1. Sélectionnez **Teams Toolkit** dans le volet gauche.
   1. Sélectionnez **Ajouter des fonctionnalités** sous **DÉVELOPPEMENT**.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="mise à jour":::

* **Pour ajouter des fonctionnalités à l’aide de la palette de commandes :**

   1. Ouvrez **la palette de commandes**.
   1. Entrez **Teams :Ajouter des fonctionnalités**.
   1. Appuyez sur **Entrée**.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/Teams-add-features.png" alt-text="fonctionnalité d’équipe":::

   1. Dans la fenêtre contextuelle, sélectionnez la fonctionnalité à ajouter à votre projet.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="Notification":::

## <a name="add-capabilities-using-teamsfx-cli"></a>Ajouter des fonctionnalités à l’aide de l’interface CLI TeamsFx

* Remplacez le répertoire par votre **répertoire du projet**.
* Le tableau suivant répertorie les fonctionnalités et les commandes requises :

  |Fonctionnalité et scénario| Commande|
  |-----------------------|----------|
  |Pour ajouter un bot de notification |`teamsfx add notification`|
  |Pour ajouter un bot de commandes |`teamsfx add command-and-response`|
  |Pour ajouter l’onglet sso-enabled |`teamsfx add sso-tab`|
  |Pour ajouter un onglet |`teamsfx add tab`|
  |Pour ajouter un bot |`teamsfx add bot`|
  |Pour ajouter l’extension de message |`teamsfx add message extension`|

## <a name="available-capabilities-to-add-for-different-teams-project"></a>Fonctionnalités disponibles à ajouter pour différents projets Teams

Vous pouvez choisir d’ajouter différentes fonctionnalités en fonction du projet que vous avez créé dans l’application Teams.
Le tableau suivant répertorie les fonctionnalités disponibles à ajouter à votre projet :

|Fonctionnalités existantes|Autres fonctionnalités prises en charge|
|--------------------|--------------------|
|Onglet SPFx |Aucune|
|Onglet SSO activé |Onglet SSO, bot de notification, bot de commandes, bot, extension de message|
|Bot de notification |Onglet SSO activé, onglet|
|Bot de commandes |Onglet SSO activé, onglet|
|Tab |Onglet, bot de notification, bot de commandes, bot, extension de message|
|Bot |Extension de message, onglet SSO, onglet|
|Extension de message |Bot, onglet SSO, onglet |

## <a name="add-bot-tab-and-message-extension"></a>Ajouter le bot, l’onglet et l’extension de message

Après l’ajout d’un bot et d’une extension de message, les modifications apportées à votre projet sont les suivantes :

* Un code de modèle de bot est ajouté dans un sous-dossier avec chemin d’accès `yourProjectFolder/bot`. Cela inclut un modèle d’application de bot **Hello World** dans votre projet.
* `launch.json` et `task.json` sous `.vscode` le dossier sont mis à jour, ce qui inclut les scripts nécessaires pour Visual Studio Code, et est exécuté lorsque vous souhaitez déboguer votre application localement.
* `manifest.template.json` Le fichier sous `templates/appPackage` dossier est mis à jour, qui inclut les informations relatives au bot dans le fichier manifeste qui représente votre application dans la plateforme Teams. Les modifications sont les suivantes :
  * ID de votre bot
  * Étendues de votre bot
  * Commandes auxquelles l’application de bot Hello World peut répondre
* Les fichiers sous `templates/azure/teamsfx` sont mis à jour et `templates/azure/provision/xxx`les fichiers .bicep sont régénérés.
* Les fichiers sous `.fx/config` sont régénérés, ce qui garantit que votre projet est configuré avec les configurations appropriées pour la fonctionnalité nouvellement ajoutée.

Après l’ajout de l’onglet, les modifications apportées à votre projet sont les suivantes :

* Un code de modèle d’onglet front-end est ajouté dans un sous-dossier avec chemin d’accès `yourProjectFolder/tab`, qui inclut un modèle d’application d’onglet **Hello World** dans votre projet.
* `launch.json` et `task.json` sous `.vscode` le dossier sont mis à jour, ce qui inclut les scripts nécessaires pour Visual Studio Code, et est exécuté lorsque vous souhaitez déboguer votre application localement.
* `manifest.template.json` Le fichier sous `templates/appPackage` dossier est mis à jour, qui inclut des informations relatives aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams. Les modifications sont les suivantes :
  * Onglets configurables et statiques
  * Étendues des onglets
* Les fichiers sous `templates/azure/teamsfx` seront mis à jour et `templates/azure/provision/xxx`le fichier .bicep sera régénéré.
* Le fichier sous `.fx/config` est régénéré, ce qui garantit que votre projet est configuré avec les configurations appropriées pour la fonctionnalité nouvellement ajoutée.

## <a name="step-by-step-guide"></a>Guide pas à pas

* Suivez le guide [pas à pas](../sbs-gs-commandbot.yml) pour créer un bot de commandes dans Microsoft Teams

* Suivez le guide [pas à pas](../sbs-gs-notificationbot.yml) pour créer un bot de notification dans Microsoft Teams.

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Créer un projet Teams](create-new-project.md)
