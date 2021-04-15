---
title: Ajouter un chatbot d'agents virtuels Power à Teams
author: laujan
description: intégration d'un chatbot d'agents virtuels Power dans la plateforme Teams
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 6103e3b58d7283eab6e9a9932f6dc7778d6fc697
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697094"
---
# <a name="integrate-a-power-virtual-agents-chatbot-with-microsoft-teams"></a>Intégrer un chatbot d'agents virtuels Power à Microsoft Teams

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) est une solution d'interface graphique guidée sans code qui permet à chaque membre de votre équipe de créer des chatbots riches et conversationnels qui s'intègrent facilement à la plateforme Teams. Tout le contenu rédigé dans Les agents power virtual s'restituera naturellement dans les bots Teams et Les agents virtuels Power impliquent des utilisateurs dans le canevas de conversation native Teams. Vos administrateurs informatiques, analystes d'entreprise, spécialistes de domaines et développeurs d'applications compétents peuvent concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement, à créer un service web ou à s'inscrire directement auprès de Bot Framework.  *Voir* [Créer un chatbot pour Teams avec les agents virtuels Microsoft Power.](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)

> [!NOTE]
> En ajoutant votre chatbot à Microsoft Teams, certaines données, telles que le contenu du bot et le contenu de conversation de [l'utilisateur](/power-virtual-agents/data-location)final, seront partagées avec Microsoft Teams (ce qui signifie que vos données seront partagées en dehors des limites géographiques et régionales et de conformité de votre organisation). <br/>
> Pour plus d'informations, voir [la sécurité et la conformité dans Microsoft Teams.](/MicrosoftTeams/security-compliance-overview)

## <a name="make-your-chatbot-available-in-teams-via-the-power-virtual-agents-portal"></a>Rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents

1. **Publiez le contenu du bot le plus récent.**  Une fois que vous avez créé un chatbot dans le portail [Power Virtual Agents,](https://powervirtualagents.microsoft.com)vous devez publier votre bot au moins une fois pour que les utilisateurs de Teams peuvent interagir avec celui-ci. Voir [Publier le contenu du bot le plus récent.](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)

![publier dans le portail des agents virtuels d'alimentation](../../assets/images/pva-publish.png)

2. **Configurez le canal Teams.** Après avoir publié votre bot, vous pouvez ajouter le canal Teams pour le rendre accessible aux utilisateurs de Teams.

![canaux dans le portail des agents virtuels d'alimentation](../../assets/images/pva-channels.png)

3. **Générez un ID d'application pour votre chatbot.**  Une fois que le canal Teams a été ajouté à votre chatbot, un **ID** d'application est généré dans la boîte de dialogue. L'ID d'application est un identificateur Microsoft unique généré pour votre bot.  Copiez et enregistrez l'ID de l'application. Vous en aurez besoin ultérieurement pour créer un package d'application pour Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Ajouter votre bot à Teams à l'aide d'App Studio

Si [le téléchargement d'applications](/microsoftteams/admin-settings) personnalisées est activé dans votre instance Teams, vous pouvez utiliser Teams App Studio pour télécharger directement votre chatbot et commencer à l'utiliser immédiatement. Si vous souhaitez partager votre chatbot, vous pouvez demander à votre administrateur de rendre votre bot disponible dans le catalogue d'applications client ou vous pouvez envoyer votre package d'application à d'autres personnes et leur demander de le télécharger indépendamment.

1. **Installez App Studio dans Teams.** App Studio est une application Teams que vous pouvez installer à partir du magasin Teams qui simplifie la création et l'inscription de votre bot dans Teams : 

  * Sélectionnez l'icône du Magasin d'applications en bas de la barre de navigation de gauche dans votre instance Teams, puis recherchez **App Studio.**
>

&emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="/msteams-docs/msteams-platform/assets/images/get-started/app-studio-store.png"/>   

  * Sélectionnez **la vignette App Studio,** puis **sélectionnez Installer** dans la boîte de dialogue de fenêtre pop-up.
>
&emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. **Créez le manifeste de l'application Teams dans App Studio.**  Les bots dans Teams sont définis par un fichier de manifeste d'application (JSON) qui fournit des informations de base sur votre bot et ses fonctionnalités. Dans **App Studio, sélectionnez** **Éditeur de manifeste** Créer une   =>  **application.**
3. **Ajoutez les détails de votre bot.** Pour obtenir une description complète de chaque champ, voir [la définition du schéma de manifeste.](../../resources/schema/manifest-schema.md) Assurez-vous d'effectuer tous les champs requis.
4. **Configurer votre bot**. Accédez à **l'onglet Bots,** sélectionnez le bouton **Installation,** choisissez **Bot** existant, puis entrez votre nom de bot.
5. **Ajoutez votre ID d'application.** Accédez **à Se connecter à un autre ID de bot** et collez-le dans l'ID **d'application** que vous avez copié précédemment. Sous l'étendue, **sélectionnez Personnel,** puis **Enregistrer.**
6. **Ajoutez des domaines valides pour votre bot.**  Cette étape est requise uniquement si votre bot nécessite que l'utilisateur se connecte. Accédez **à Domaines et autorisations,** puis dans le champ Domaines **valides,** accédez aux informations suivantes :

```bash
token.botframework.com
```

7.  **Testez et distribuez votre bot.** Sélectionnez **l'onglet Tester et distribuer** et choisissez **Installer** pour ajouter votre bot directement à votre instance Teams. Si vous le souhaitez, vous pouvez télécharger votre package d'application terminé pour le partager avec les utilisateurs de Teams ou le fournir à votre administrateur pour que votre bot soit disponible dans le catalogue d'applications client.
8. **Démarrer une conversation.** Le processus de configuration pour l'ajout de votre bot de conversation Power Virtual Agents à Teams est terminé. Vous pouvez maintenant démarrer une conversation avec votre bot dans une conversation personnelle.

> [!div class="nextstepaction"]
> [En savoir plus : Publier votre bot d'agents power virtual](/power-virtual-agents/publication-fundamentals-publish-channels)
