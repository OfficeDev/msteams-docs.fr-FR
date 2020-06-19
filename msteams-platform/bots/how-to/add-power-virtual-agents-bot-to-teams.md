---
title: Ajouter des agents virtuels chatbot à teams
author: laujan
description: intégration d’agents virtuels chatbot dans la plateforme teams
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 4f32a3c13d9288c3e733e92369645bcf9e32d586
ms.sourcegitcommit: 28af65730884b788ff77a4ec4032219380df8b70
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2020
ms.locfileid: "44801142"
---
# <a name="integrate-your-power-virtual-agents-chatbot-with-microsoft-teams"></a>Intégration de vos agents Virtual chatbot avec Microsoft teams

[Power Virtual agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) est une solution d’interface graphique guidée sans code qui permet à chaque membre de votre équipe de créer des chatbotss riches et conversation qui s’intègrent facilement à la plateforme Teams. Tout le contenu créé dans les agents de la fonctionnalité de gestion de l’alimentation est rendu naturellement dans teams et les robots des agents virtual agent sont associés aux utilisateurs de la zone de conversation native de teams. Vos administrateurs informatiques, analystes d’entreprise, spécialistes des domaines et développeurs d’applications compétents peuvent concevoir, développer et publier des agents virtuels intelligents pour teams sans avoir à configurer un environnement de développement, créer un service Web ou s’enregistrer directement auprès de l’infrastructure de robot.  *Voir* [Create a chatbot for teams with Microsoft Power Virtual agents](../what-are-bots.md#create-a-chatbot-for-teams-with-microsoft-power-virtual-agents).

> [!NOTE]
> En ajoutant votre chatbot à Microsoft Teams, certaines données, telles que le contenu des robots et le contenu de la conversation utilisateur final, seront partagées avec Microsoft Teams (ce qui signifie que vos données transitent en dehors de la [conformité et des frontières géographiques ou régionales](/power-virtual-agents/data-location)de votre organisation). <br/>
> Pour plus d’informations, consultez la rubrique [sécurité et conformité dans Microsoft teams](/MicrosoftTeams/security-compliance-overview).

## <a name="make-your-chatbot-reachable-in-teams-in-the-power-virtual-agents-portal"></a>Rendez vos chatbot accessibles dans teams dans le portail des agents Virtual Power

1. **Publiez le contenu de robot le plus récent**.  Une fois que vous avez créé un chatbot dans le [portail Power Virtual agents](https://powervirtualagents.microsoft.com), vous devez publier votre robot au moins une fois avant que les utilisateurs de teams puissent interagir avec lui. Voir [publier le contenu de robot le plus récent](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).

![publier dans le portail des agents Virtual Power](../../assets/images/pva-publish.png)

2. **Configurez le canal teams**. Après avoir publié votre robot, vous pouvez ajouter le canal teams pour permettre aux utilisateurs de teams d’accéder au bot.

![canaux dans le portail des agents Virtual Power](../../assets/images/pva-channels.png)

3. **Générer un ID d’application pour votre chatbot**  Une fois que le canal teams a été ajouté à votre chatbot, un **ID d’application** est généré dans la boîte de dialogue. L’ID de l’application est un identificateur Microsoft généré unique pour votre bot.  Copiez et enregistrez l’ID de l’application : vous en aurez besoin plus tard pour créer un package d’application pour Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Ajouter votre robot à teams à l’aide d’App Studio

Si le téléchargement d' [applications personnalisées est activé](/microsoftteams/admin-settings) dans votre instance de teams, vous pouvez utiliser teams App Studio pour télécharger directement votre chatbot et commencer à l’utiliser immédiatement. Si vous souhaitez partager votre chatbot, vous pouvez demander à votre administrateur de rendre votre robot disponible dans le catalogue d’applications client ou d’envoyer à d’autres personnes votre package d’application et de lui demander de le charger indépendamment.

1. **Installez App Studio dans teams**. App Studio est une application de teams que vous pouvez installer à partir du Store teams qui simplifie la création et l’enregistrement de votre robot dans teams : 

  * Sélectionnez l’icône App Store située en bas de la barre de navigation gauche dans votre instance de teams, puis recherchez **app Studio**.
>
&emsp;&emsp; <img  width="450px" title="Recherche d’App Studio dans le Store" src="../../assets/images/get-started/app-studio-store.png"/>    

  * Sélectionnez la vignette **app Studio** et choisissez **installer** dans la boîte de dialogue contextuelle.
>
&emsp;&emsp; <img  width="450px" title="Installation d’App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. **Créez le manifeste d’application teams dans App Studio**.  Les robots dans teams sont définis par un fichier de manifeste d’application (JSON) qui fournit des informations de base sur votre robot et ses fonctionnalités. Dans **app Studio** , sélectionnez **éditeur de manifeste**   =>  **créer une application**.
3. **Ajoutez les détails de votre robot**. Pour obtenir une description complète de chaque champ, voir [manifeste Schema Definition](../../resources/schema/manifest-schema.md). Veillez à renseigner tous les champs obligatoires.
4. **Configurez votre robot**. Accédez à l’onglet **robots** , sélectionnez le bouton **configuration** , choisissez **bot existant**, puis entrez votre nom de robot.
5. **Ajoutez votre ID d’application**. Naviguez jusqu’à **un ID de bot différent** et collez-le dans l' **ID d’application** que vous avez copié précédemment. Sous étendue, sélectionnez **personnel** , puis **Enregistrer**.
6. **Ajoutez des domaines valides pour votre robot**.  Cette étape est obligatoire uniquement si votre bot requiert que l’utilisateur se connecte. Accédez à **domaines et autorisations** et, dans le champ **domaines valides** , entrez les éléments suivants :

```bash
token.botframework.com
```

7.  **Testez et distribuez votre bot**. Choisissez l’onglet **test et distribution** , puis choisissez **installer** pour ajouter votre bot directement à votre instance d’équipe. Si vous le souhaitez, vous pouvez télécharger votre package d’application terminé afin de le partager avec des utilisateurs de teams ou de le fournir à votre administrateur pour qu’il rende votre bot disponible dans le catalogue d’applications client.
8. **Démarrez une conversation**. Le processus de configuration pour l’ajout de votre robot de conversation Power Virtual agents à teams est terminé. Vous pouvez maintenant démarrer une conversation avec votre robot dans une conversation personnelle.

> [!div class="nextstepaction"]
> [En savoir plus sur la publication de votre robot d’agents Virtual Power](/power-virtual-agents/publication-fundamentals-publish-channels)