---
title: Ajouter Power Virtual Agents chatbot à Teams
author: laujan
description: l’intégration d Power Virtual Agents chatbot dans la plate-forme Teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 2a8f9c23eaa1acf2555b91cc4caf8d0f3298c114
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566116"
---
# <a name="add-power-virtual-agents-chatbot"></a>Ajouter le chatbot Power Virtual Agents 

Power Virtual Agents est une solution d’interface graphique guidée sans code qui permet à chaque membre de votre équipe de créer des chatbots riches et conversationnels qui s’intègrent facilement à la plate-forme Teams technologie. Tout le contenu écrit dans Power Virtual Agents rend naturellement dans Teams. Power Virtual Agents bots s’engagent avec les utilisateurs dans Teams toile de chat natif. Les administrateurs informatiques, les analystes d’entreprise, les spécialistes du domaine et les développeurs d’applications qualifiés peuvent concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement. Ils peuvent créer un service Web ou s’inscrire directement au Cadre Bot. 

Ce document vous guide sur la façon de rendre votre chatbot disponible en Teams via le portail Power Virtual Agents, et d’ajouter votre bot à Teams en utilisant App Studio. 

Power Virtual Agents vous permet de créer de puissants chatbots qui peuvent répondre aux questions posées par vos clients, d’autres employés ou les visiteurs de votre site Web ou service.

Ces bots peuvent être créés facilement sans avoir besoin de scientifiques ou de développeurs de données.

> [!NOTE]
> En ajoutant votre chatbot à Microsoft Teams, certaines données, telles que le contenu bot et le contenu du chat utilisateur, sont partagées avec Microsoft Teams. Cela signifie que vos données circulent en dehors de la conformité [de votre organisation et des frontières géographiques ou régionales.](/power-virtual-agents/data-location) <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>Rendez votre chatbot disponible en Teams le portail Power Virtual Agents vidéo

Pour rendre votre chatbot disponible en Teams par le portail Power Virtual Agents, vous devez effectuer les étapes de processus suivantes :

**Pour rendre le chatbot disponible en Teams**

1. **Publier le dernier contenu bot**  
Après avoir créé un chatbot dans le Power Virtual Agents, vous devez publier votre bot avant que Teams utilisateurs puissent interagir avec lui. Pour plus d’informations, [voir Publier le dernier contenu bot](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).

   ![publier dans le portail des agents virtuels de puissance](../../assets/images/pva-publish.png)

1. **Configurer le canal Teams’œil**  
Après avoir publié votre bot, ajoutez le canal Teams pour mettre le bot à la disposition des Teams utilisateurs.

   ![canaux dans le portail des agents virtuels de puissance](../../assets/images/pva-channels.png)

1. **Générer un ID app pour votre chatbot**  
Après avoir ajouté le Teams à votre chatbot, un identifiant **d’application est** généré dans la boîte de dialogue. L’ID app est un identifiant microsoft unique généré pour votre bot. Enregistrez l’ID de l’application pour créer un package d’application pour Teams.

## <a name="add-your-bot-to-teams-using-app-studio"></a>Ajoutez votre bot à votre Teams’utilisation d’App Studio

Si [le téléchargement d’applications personnalisées est](/microsoftteams/admin-settings) activé dans votre instance Teams, vous pouvez utiliser Teams App Studio pour télécharger directement votre chatbot et commencer à l’utiliser immédiatement. Pour partager votre chatbot, vous pouvez demander à votre administrateur de rendre votre bot disponible dans le catalogue d’applications locataires ou vous pouvez envoyer votre paquet d’applications à d’autres et leur demander de le télécharger indépendamment.

1. **Installer App Studio dans Teams**  
App Studio est une application Teams gratuite. Installez App Studio depuis le Teams qui simplifie le processus de création et d’enregistrement de bots en Teams : 

   1. Sélectionnez l’icône de l’App Store Teams’instance et recherchez **App Studio**.

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. Sélectionnez **la vignette App Studio** et sélectionnez **Installer** dans la boîte de dialogue pop-up.

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **Créez le manifeste Teams’application dans App Studio**  
Les bots en Teams sont définis par un fichier JSON manifeste d’application qui fournit les informations de base sur votre bot et ses capacités. Dans **App Studio**, sélectionnez Manifest **editor**, et **sélectionnez Créer une nouvelle application**.

    ![créer une nouvelle application](../../assets/images/get-started/create-new-app.png)

1. **Ajoutez les détails de votre bot**  
Complétez tous les champs requis. Pour une description complète de chaque champ voir la [définition manifeste schéma](../../resources/schema/manifest-schema.md).

    ![ajouter les détails de l’application](../../assets/images/get-started/add-app-details.png)

1. **Configurer votre bot** Pour configurer le bot, effectuez les étapes suivantes : 
     1. Ouvrez **l’onglet Bots.** 
     1. Sélectionnez **Setup**  >  **Bot existant** et entrez le nom de votre bot.

   ![Mise en place de bots](../../assets/images/get-started/bot-set-up.png) 

   L’image suivante montre comment configurer un bot existant :      

   ![mise en place de bots existants](../../assets/images/get-started/existing-bot-set-up.png)
       
1. **Ajouter votre identifiant d’application**  
Pour ajouter votre identifiant d’application, effectuez les étapes suivantes :  
    1. Sélectionnez **Connecter un id bot différent et coller l’id** app que **vous** avez copié plus tôt. 
    1. Sélectionnez **Scope**  >  **Personal**  >  **Save**.

    ![ajouter l’id de l’application](../../assets/images/get-started/add-app-id.png)

1. **Ajouter des domaines valides pour votre bot**  
Cette étape n’est requise que si votre bot exige que l’utilisateur se connecte. Sélectionnez **domaines et autorisations** et dans le **domaine des domaines valides,** fournissez l’entrée suivante :

    ```bash
       token.botframework.com
    ```

1. **Testez et distribuez votre bot**  
Ouvrez **test et distribuez** l’onglet **et** sélectionnez Installer pour ajouter votre bot directement à votre Teams instance. Alternativement, vous pouvez télécharger le package d’application complété à partager avec les utilisateurs de Teams ou le fournir à votre administrateur pour rendre votre bot disponible dans le catalogue d’applications locataires.

1. **Démarrer un chat**   
Le processus de mise en place pour l’ajout de votre Power Virtual Agents bot de chat à Teams est complet. Vous pouvez maintenant commencer une conversation avec votre bot dans un chat personnel.

## <a name="see-also"></a>Voir aussi

- [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- [Créez un chatbot pour Teams avec Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).  

- [portail Power Virtual Agents’information](https://powervirtualagents.microsoft.com)

- [Publiez votre bot Power Virtual Agents](/power-virtual-agents/publication-fundamentals-publish-channels)

- [Sécurité et conformité dans Microsoft Teams](/MicrosoftTeams/security-compliance-overview).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un assistant virtuel](~/samples/virtual-assistant.md)

