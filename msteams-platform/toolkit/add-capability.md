---
title: Ajouter des fonctionnalités à vos applications Teams
author: surbhigupta
description: Dans ce module, découvrez comment ajouter des fonctionnalités du Kit de ressources Teams
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: abcda0dd19388d1cdce2f2b440ecbae833b5f9c3
ms.sourcegitcommit: 6926cf5eee55d5047c11ca13afc7f6f23e270396
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2022
ms.locfileid: "68740603"
---
# <a name="add-capabilities-to-teams-apps"></a>Ajouter des fonctionnalités aux applications Teams

L’ajout de fonctionnalités avec Teams Toolkit vous permet d’inclure des fonctionnalités supplémentaires à votre application Microsoft Teams existante. L’avantage de l’ajout de fonctionnalités supplémentaires est que vous pouvez ajouter d’autres fonctions à votre application en ajoutant automatiquement des codes sources à l’aide du Kit de ressources Teams. Vous pouvez également choisir différentes fonctionnalités en fonction du projet que vous avez créé dans votre application Teams. Le tableau suivant répertorie les fonctionnalités de l’application Teams :

|Fonctionnalité|Description|Autres fonctionnalités prises en charge|
|--------|-------------|-----------------|
|**Application Teams de base**|              |
| Tab |  Les onglets sont des balises HTML simples qui font référence à des domaines déclarés dans le manifeste de l’application. Vous pouvez ajouter des onglets dans le cadre d’un canal à l’intérieur d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel.|Onglet, bot de notification, bot de commande, bot, extension de message|
|Onglet SPFx| Les applications d’onglet SPFx sont hébergées dans Microsoft 365 et prennent en charge le développement et l’hébergement de votre solution SPFx côté client|Aucun|
|Onglet activé pour l’authentification unique|Vous pouvez créer une application d’onglet prenant en charge l’authentification unique qui autorise l’utilisateur avec la fonctionnalité d’authentification unique|Onglet prenant en charge l’authentification unique, bot de notification, bot de commande, bot, extension de message|
| Bot |  Les bots aident à interagir avec votre service web via du texte, des cartes interactives et des modules de tâches.|Extension de message, onglet activé pour l’authentification unique, onglet|
| Extension de message | Les extensions de message permettent d’interagir avec votre service web via des boutons et des formulaires dans le client Microsoft Teams.|Bot, onglet activé pour l’authentification unique, onglet|
|**Application Teams basée sur un scénario**|             |
| Bot de notification | Le bot de notification envoie de manière proactive des messages dans un canal Teams, une conversation de groupe ou une conversation personnelle. Vous pouvez déclencher le bot de notification avec une requête HTTP, telle que des cartes ou des sms. |Onglet activé pour l’authentification unique, onglet|
| Bot de commande | Le bot de commandes vous permet d’automatiser les tâches répétitives à l’aide d’un bot de commande. Il répond aux commandes simples envoyées dans les conversations avec des cartes adaptatives. |Onglet activé pour l’authentification unique, onglet|
| Bot de flux de travail| Le bot de flux de travail permet aux utilisateurs d’interagir avec une carte adaptative activée par la fonctionnalité gestionnaire d’actions de carte adaptative dans l’application bot de flux de travail.|Onglet activé pour l’authentification unique, onglet|

> [!NOTE]
> Vous pouvez ajouter des onglets jusqu’à 16 instances. En ce qui concerne votre bot et votre extension de message, vous pouvez en ajouter une pour chaque instance à la fois.

## <a name="add-capabilities"></a>Ajouter des fonctionnalités

Vous pouvez ajouter des fonctionnalités en procédant comme suit :

* [Utilisation de Teams Toolkit dans Microsoft Visual Studio Code](#using-teams-toolkit-in-microsoft-visual-studio-code)
* [Utilisation de la palette de commandes](#using-the-command-palette)
* [Utilisation de l’interface CLI TeamsFx](#using-teamsfx-cli)

### <a name="using-teams-toolkit-in-microsoft-visual-studio-code"></a>Utilisation de Teams Toolkit dans Microsoft Visual Studio Code

   1. Ouvrez **Visual Studio Code**.
   1. Sélectionnez **Teams Toolkit dans** la barre d’activité.
   1. Sélectionnez **Ajouter des fonctionnalités** sous **DÉVELOPPEMENT**.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="Ajouter des fonctionnalités à partir du Kit de ressources Teams":::

      > [!NOTE]
      > Après avoir ajouté les fonctionnalités dans votre application Teams, vous devez provisionner pour chaque environnement.

### <a name="using-the-command-palette"></a>Utilisation de la palette de commandes

   1. Sélectionnez **Afficher** > **la palette de commandes...** ou **Ctrl+Maj+P**.

      :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add-capabilities-command-palette.png" alt-text="Ajouter des fonctionnalités à partir de la palatte de commande":::

   1. Entrez **Teams : Ajouter des fonctionnalités**.
   1. Appuyez sur Entrée.

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/teams-add-features.png" alt-text="Pour ajouter des fonctionnalités à l’aide de la palette de commandes.":::

   1. Dans la fenêtre contextuelle, sélectionnez la fonctionnalité que vous devez ajouter à votre projet.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="Notification":::

### <a name="using-teamsfx-cli"></a>Utilisation de l’interface CLI TeamsFx

* Remplacez le répertoire par votre **répertoire du projet**.
* Le tableau suivant répertorie les fonctionnalités et les commandes requises :

  |Fonctionnalité et scénario| Commande|
  |-----------------------|----------|
  |Pour ajouter un bot de notification |`teamsfx add notification`|
  |Pour ajouter un bot de commande |`teamsfx add command-and-response`|
  |Pour ajouter l’onglet activé pour l’authentification unique |`teamsfx add sso-tab`|
  |Pour ajouter l’onglet |`teamsfx add tab`|
  |Pour ajouter un bot |`teamsfx add bot`|
  |Pour ajouter une extension de message |`teamsfx add message extension`|

## <a name="changes-after-adding-capabilities"></a>Modifications après l’ajout de fonctionnalités

Le tableau suivant présente les modifications qui peuvent être visibles dans les fichiers de votre application lors de l’ajout des fonctionnalités :

|Ajouter une fonctionnalité|Description| Modifications|
|------------|------------------------|---------|
|Bot, extension de message et onglet|Inclut un modèle **d’application** de bot ou d’onglet Hello World &nbsp;dans votre projet.|Un code de modèle de bot frontal ou d’onglet est ajouté à un sous-dossier avec le chemin d’accès `yourProjectFolder/bot` ou `yourProjectFolder/tab` respectivement.|
| Bot, extension de message et onglet |Inclut les scripts nécessaires pour Visual Studio Code et est exécuté lorsque vous souhaitez déboguer votre application localement. |Les fichiers `launch.json` et `task.json` sous `.vscode` le dossier sont mis à jour.|
| Bot et extension de message|Inclut des informations relatives au bot ou aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams.|Le fichier`manifest.template.json` sous `templates/appPackage` le dossier est mis à jour, qui inclut des informations relatives aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams. Les modifications sont visibles dans l’ID de votre bot, les étendues de votre bot et les commandes auxquelles le bot hello world ou l’application d’onglet peut répondre.|
|Tab|Inclut des informations relatives au bot ou aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams.|Le fichier `manifest.template.json` sous `templates/appPackage` le dossier est mis à jour, qui inclut des informations relatives aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams. Les modifications sont visibles dans les onglets configurables et statiques, ainsi que dans les étendues des onglets.|
|Bot, extension de message et onglet|Inclut des informations relatives aux bots ou aux&nbsp;onglets dans les fichiers teamsfx et de provisionnement destinés à l’intégration des fonctions Azure.|Les fichiers sous `templates/azure/teamsfx` sont mis à jour et `templates/azure/provision/xxx`les fichiers .bicep sont régénérés.|
|Bot, extension de message et onglet|Garantit que votre projet est défini avec les configurations appropriées pour les fonctionnalités nouvellement ajoutées.|Les fichiers sous `.fx/config` sont régénérés|

## <a name="step-by-step-guide"></a>Guide pas à pas

* Suivez le guide [pas à pas](../sbs-gs-commandbot.yml) pour créer un bot de commande dans Microsoft Teams.

* Suivez le guide [pas à pas](../sbs-gs-notificationbot.yml) pour créer un bot de notification dans Microsoft Teams.

* Suivez le guide [pas à pas](../sbs-gs-workflow-bot.yml) pour créer un bot de flux de travail dans Microsoft Teams.

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Créer un projet Teams](create-new-project.md)
