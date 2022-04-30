---
title: Ajouter Power Virtual Agents chatbot à Teams
author: surbhigupta
description: Apprenez à intégrer un chatbot Power Virtual Agents dans la plateforme Teams pour créer des bots conversationnels et l’intégrer à Teams
ms.topic: how-to
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: 53a938ca4a195ba6f477de130a8290242709cb19
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111772"
---
# <a name="add-power-virtual-agents-chatbot"></a>Ajouter le chatbot Power Virtual Agents

Power Virtual Agents est une solution d’interface graphique guidée sans code qui permet à chaque membre de votre équipe de créer des chatbots conversationnels riches qui s’intègrent facilement à la plateforme Teams. Tout le contenu créé dans Power Virtual Agents s’affiche naturellement dans Teams. Power Virtual Agents bots communiquent avec les utilisateurs dans le canevas de conversation natif Teams. Les administrateurs informatiques, les analystes d’entreprise, les spécialistes du domaine et les développeurs d’applications qualifiés peuvent concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement. Ils peuvent créer un service web ou s’inscrire directement auprès du Bot Framework.

Ce document vous guide sur la façon de rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents et d’ajouter votre bot à Teams à l’aide d’App Studio.

Power Virtual Agents vous permet de créer des bots conversationnels puissants qui peuvent répondre aux questions posées par vos clients, d’autres employés ou les visiteurs de votre site web ou service.

Ces bots peuvent être créés facilement sans avoir besoin de scientifiques des données ou de développeurs.

> [!NOTE]
> * En ajoutant votre chatbot à Microsoft Teams, certaines données, telles que le contenu du bot et le contenu de conversation utilisateur, sont partagées avec Microsoft Teams. Cela signifie que vos données circulent en dehors de la [conformité de vos organisations et des limites géographiques ou régionales](/power-virtual-agents/data-location). <br/>
> * Vous ne devez pas utiliser Microsoft Power Platform pour créer des applications destinées à être publiées dans la boutique d'applications Teams. Les applications Microsoft Power Platform peuvent être publiées dans l’App Store d’une organisation uniquement.

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>Rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents

Pour rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents, vous devez effectuer les étapes de processus suivantes :

Pour rendre le chatbot disponible dans Teams :

1. **publier le dernier contenu du bot**  
Après avoir créé un chatbot dans le portail Power Virtual Agents, vous devez publier votre bot avant que les utilisateurs Teams puissent interagir avec lui. Pour plus d’informations, consultez [Publier le contenu du bot le plus récent](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).

   ![publier dans le portail Power Virtual Agents](../../assets/images/pva-publish.png)

1. **configurer le canal Teams**  
Après avoir publié votre bot, ajoutez le canal Teams pour le mettre à la disposition des utilisateurs de Teams.

   ![canaux dans le portail power virtual agents](../../assets/images/pva-channels.png)

1. **générer un ID d’application pour votre chatbot**  
Après avoir ajouté le canal Teams à votre chatbot, un **App ID** est généré dans la boîte de dialogue. L’ID d’application est un identificateur unique généré par Microsoft pour votre bot. Enregistrez l’ID d’application pour créer un package d’application pour Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Ajouter votre bot à Teams à l’aide d’App Studio

Si [chargement d’applications personnalisées est activé](/microsoftteams/admin-settings) dans votre instance Teams, vous pouvez utiliser Teams App Studio pour charger directement votre chatbot et commencer à l’utiliser immédiatement. Pour partager votre chatbot, vous pouvez demander à votre administrateur de rendre votre bot disponible dans le catalogue d’applications client ou vous pouvez envoyer votre package d’application à d’autres personnes et leur demander de le charger indépendamment.

1. **Installer App Studio dans Teams**  
App Studio est une application Teams. Installez App Studio à partir du magasin Teams qui simplifie le processus de création et d’inscription de bot dans Teams :

   1. Sélectionnez l’icône de l’App Store dans l’instance Teams, puis recherchez **App Studio**.

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>

   1. Sélectionnez la vignette **App Studio** et sélectionnez **Installer** dans la boîte de dialogue contextuelle.

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **Créer le manifeste d’application Teams dans App Studio**  
Les bots dans Teams sont définis par un fichier JSON de manifeste d’application qui fournit les informations de base sur votre bot et ses fonctionnalités. Dans **App Studio**, sélectionnez **l’éditeur de manifeste**, puis sélectionnez **Créer une application**.

    ![créer une application](../../assets/images/get-started/create-new-app.png)

1. **Ajouter les détails de votre bot**  
Complétez tous les champs obligatoires. Pour obtenir une description complète de chaque champ, consultez [définition de schéma de manifeste](../../resources/schema/manifest-schema.md).

    ![ajouter les détails de l’application](../../assets/images/get-started/add-app-details.png)

1. **configurer votre bot** Pour configurer le bot, procédez comme suit :
     1. Ouvrez l’onglet **bots**.
     1. Sélectionnez **configuration** > **de bot existant** et entrez le nom de votre bot.

   ![Configuration du bot](../../assets/images/get-started/bot-set-up.png)

   L’image suivante montre comment configurer un bot existant :

   ![configuration de bot existante](../../assets/images/get-started/existing-bot-set-up.png)

1. **ajouter votre ID d’application**  
Pour ajouter votre ID d’application, procédez comme suit :  
    1. Sélectionnez **Connectez-vous à un autre** ID de bot et collez **l’ID d’application** que vous avez copié précédemment.
    1. Sélectionnez **Étendue** > **personnel** > **Enregistrer**.

    ![Ajouter un ID d’application](../../assets/images/get-started/add-app-id.png)

1. **Ajouter des domaines valides pour votre bot**  
Cette étape n’est requise que si votre bot exige que l’utilisateur se connecte. Sélectionnez **domaines et autorisations** et, dans le champ **Domaines valides** , fournissez l’entrée suivante :

    ```bash
       token.botframework.com
    ```

1. **tester et distribuer votre bot**  
Ouvrez **Test et distribuez** onglet, puis sélectionnez **Installer** pour ajouter votre bot directement à votre instance Teams. Vous pouvez également télécharger le package d’application terminé à partager avec les utilisateurs Teams ou le fournir à votre administrateur pour rendre votre bot disponible dans le catalogue d’applications client.

1. **démarrer une conversation** Le processus de configuration de l’ajout de votre bot de conversation Power Virtual Agents à Teams est terminé. Vous pouvez maintenant démarrer une conversation avec votre bot dans une conversation personnelle.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un assistant virtuel](~/samples/virtual-assistant.md)

## <a name="see-also"></a>Voir aussi

* [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* [créer un chatbot pour Teams avec Microsoft Power Virtual Agents](../bot-features.md#bots-with-power-virtual-agents)
* [Portail Power Virtual Agents](https://powervirtualagents.microsoft.com)
* [publier votre de bot Power Virtual Agents](/power-virtual-agents/publication-fundamentals-publish-channels)
* [Sécurité et de la conformité dans Microsoft Teams](/MicrosoftTeams/security-compliance-overview)
