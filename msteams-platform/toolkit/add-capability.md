---
title: Ajouter des fonctionnalités à vos applications Teams
author: surbhigupta
description: Dans ce module, découvrez comment ajouter des fonctionnalités de Teams Toolkit
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: fe78407c0a269d26a63e23efe5a04a1cd0d83e4b
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616962"
---
# <a name="add-capabilities-to-microsoft-teams-apps"></a>Ajouter des fonctionnalités aux applications Microsoft Teams

L’ajout de fonctionnalités avec le Kit de ressources Teams vous permet d’inclure des fonctionnalités supplémentaires à votre application Teams existante. L’avantage d’ajouter d’autres fonctionnalités est que vous pouvez ajouter d’autres fonctions à votre application en ajoutant automatiquement des codes sources à l’aide du Kit de ressources Teams. Vous pouvez également choisir différentes fonctionnalités en fonction du projet que vous avez créé dans votre application Teams. Le tableau suivant répertorie les fonctionnalités de l’application Teams :

|Fonctionnalité|Description|Autres fonctionnalités prises en charge|
|--------|-------------|-----------------|
|**Application Teams de base**|              |
| Tab |  Les onglets sont des balises HTML simples qui font référence aux domaines déclarés dans le manifeste de l’application. Vous pouvez ajouter des onglets dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel.|Onglet, bot de notification, bot de commandes, bot, extension de message|
|Onglet SPFx| Les applications de l’onglet SPFx sont hébergées dans Microsoft 365 et prennent en charge le développement et l’hébergement de votre solution SPFx côté client|Aucun|
|Onglet SSO activé|Vous pouvez créer une application d’onglet prenant en charge l’authentification unique qui permet à l’utilisateur avec la fonctionnalité d’authentification unique|Onglet SSO, bot de notification, bot de commandes, bot, extension de message|
| Bot |  Les bots permettent d’interagir avec votre service web par le biais de texte, de cartes interactives et de modules de tâches.|Extension de message, onglet SSO, onglet|
| Extension de message | Les extensions de message permettent d’interagir avec votre service web via des boutons et des formulaires dans le client Microsoft Teams.|Bot, onglet SSO, onglet|
|**Application Teams basée sur un scénario**|             |
| Bot de notification | Le bot de notification envoie de manière proactive des messages dans un canal Teams, une conversation de groupe ou une conversation personnelle. Vous pouvez déclencher le bot de notification avec une requête HTTP, telle que des cartes ou des textes. |Onglet SSO activé, onglet|
| Bot de commandes | Le bot de commandes vous permet d’automatiser les tâches répétitives à l’aide d’un bot de commandes. Il répond aux commandes simples envoyées dans les conversations avec des cartes adaptatives. |Onglet SSO activé, onglet|

> [!NOTE]
> Vous pouvez ajouter des onglets jusqu’à 16 instances. En ce qui concerne votre bot et l’extension de message, vous pouvez en ajouter un pour chaque instance à la fois.

## <a name="add-capabilities"></a>Ajouter des fonctionnalités

Vous pouvez ajouter des fonctionnalités en suivant les méthodes suivantes :

* [Utilisation de Teams Toolkit dans Microsoft Visual Studio Code](#using-teams-toolkit-in-microsoft-visual-studio-code)
* [Utilisation de la palette de commandes](#using-the-command-palette)
* [Utilisation de l’interface CLI TeamsFx](#using-teamsfx-cli)

### <a name="using-teams-toolkit-in-microsoft-visual-studio-code"></a>Utilisation de Teams Toolkit dans Microsoft Visual Studio Code

   1. Ouvrez **Visual Studio Code**.
   1. Sélectionnez **Teams Toolkit** dans la barre d’activité.
   1. Sélectionnez **Ajouter des fonctionnalités** sous **DÉVELOPPEMENT**.

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="Ajouter des fonctionnalités à partir du Kit de ressources Teams":::

      > [!NOTE]
      > Une fois que vous avez ajouté les fonctionnalités dans votre application Teams, vous devez provisionner pour chaque environnement.

### <a name="using-the-command-palette"></a>Utilisation de la palette de commandes

   1. Sélectionnez **Afficher** >  la **palette de commandes...** ou **Ctrl+Maj+P**.

      :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add-capabilities-command-palette.png" alt-text="Ajouter des fonctionnalités à partir de la commande palatte":::

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
  |Pour ajouter un bot de commandes |`teamsfx add command-and-response`|
  |Pour ajouter l’onglet sso-enabled |`teamsfx add sso-tab`|
  |Pour ajouter un onglet |`teamsfx add tab`|
  |Pour ajouter un bot |`teamsfx add bot`|
  |Pour ajouter l’extension de message |`teamsfx add message extension`|

## <a name="changes-after-adding-capabilities"></a>Modifications après l’ajout de fonctionnalités

Le tableau suivant présente les modifications qui peuvent être vues dans les fichiers de votre application lors de l’ajout des fonctionnalités :

|Ajouter une fonctionnalité|Description| Modifications|
|------------|------------------------|---------|
|Bot, extension de message et onglet|Inclut un bot **Hello World**&nbsp;ou un modèle d’application d’onglet dans votre projet.|Un bot frontal ou un code de modèle d’onglet est ajouté dans un sous-dossier avec le chemin d’accès `yourProjectFolder/bot` ou `yourProjectFolder/tab` respectivement.|
| Bot, extension de message et onglet |Inclut les scripts nécessaires pour Visual Studio Code et est exécuté lorsque vous souhaitez déboguer votre application localement. |Les fichiers `launch.json` et `task.json` sous `.vscode` le dossier sont mis à jour.|
| Bot et extension de message|Inclut des informations relatives au bot ou aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams.|Le fichier`manifest.template.json` sous `templates/appPackage` le dossier est mis à jour, ce qui inclut les informations relatives aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams. Les modifications sont visibles dans l’ID de votre bot, les étendues de votre bot et les commandes auxquelles hello world bot ou tab application peut répondre.|
|Tab|Inclut des informations relatives au bot ou aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams.|Le fichier`manifest.template.json` sous `templates/appPackage` le dossier est mis à jour, ce qui inclut les informations relatives aux onglets dans le fichier manifeste qui représente votre application dans la plateforme Teams. Les modifications sont visibles dans les onglets configurables et statiques, ainsi que dans les étendues des onglets.|
|Bot, extension de message et onglet|Inclut des informations relatives aux bots ou aux&nbsp;onglets dans teamsfx et fournit des fichiers destinés à l’intégration de fonctions Azure.|Les fichiers sous `templates/azure/teamsfx` sont mis à jour et `templates/azure/provision/xxx`les fichiers .bicep sont régénérés.|
|Bot, extension de message et onglet|Garantit que votre projet est configuré avec les configurations appropriées pour la fonctionnalité nouvellement ajoutée.|Les fichiers sous `.fx/config` sont régénérés|

## <a name="step-by-step-guide"></a>Guide pas à pas

* Suivez le guide [pas à pas](../sbs-gs-commandbot.yml) pour créer un bot de commandes dans Microsoft Teams

* Suivez le guide [pas à pas](../sbs-gs-notificationbot.yml) pour créer un bot de notification dans Microsoft Teams.

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Créer un projet Teams](create-new-project.md)
