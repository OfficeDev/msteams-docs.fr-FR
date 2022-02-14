---
title: Conditions requises et considérations pour les robots multimédias hébergés par l’application
description: Comprendre les exigences et considérations importantes, ainsi que les considérations relatives à l’évolutivité et aux performances liées à la création de bots multimédias hébergés par l’application pour Microsoft Teams à l’aide d’exemples et d’exemples de code.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: serveur multimédia hébergé par Windows’application Azure VM
ms.date: 11/16/2018
ms.openlocfilehash: 1e9fa106376a3068039dd74c8e0b4f2b8c8802d6
ms.sourcegitcommit: bfa9d24f736fb8915a9e3ef09c47dbe29a950cb5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2022
ms.locfileid: "62801368"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>Conditions requises et considérations pour les robots multimédias hébergés par l’application

Un bot multimédia hébergé par l’application nécessite que [`Microsoft.Graph.Communications.Calls.Media` la bibliothèque .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) accède aux flux multimédias audio et vidéo. Le bot doit être déployé sur un ordinateur local Windows Server ou un système d’exploitation invité Windows Server dans Azure.

> [!NOTE]
> * Les instructions pour le développement de bots de messagerie et de réponse vocale interactive (IVR) ne s’appliquent pas complètement à la création de bots multimédias hébergés par l’application.
> * Comme la plateforme Microsoft Real-time Media pour les bots est en version préliminaire pour les développeurs, les instructions de ce document peuvent faire l’objet de changements.

## <a name="c-or-net-and-windows-server-for-development"></a>C# ou .NET et Windows Server pour le développement

Un bot multimédia hébergé par l’application requiert les procédures suivantes :

- Le bot doit être développé dans C# et la .NET Framework standard et déployé dans Microsoft Azure. Vous ne pouvez pas utiliser les API C++ ou Node.js pour accéder aux médias en temps réel et .NET Core n’est pas pris en charge pour un bot multimédia hébergé par l’application.

- Le bot peut être hébergé dans l’un des environnements de service Azure suivants :
    - Service cloud.
    - Service Fabric avec des jeux d’échelle de machine virtuelle (VMSS).
    - Ordinateur virtuel IaaS (Infrastructure as a Service).  
  
- Le bot ne peut pas être déployé en tant qu’application web Azure.

- Le bot doit être en cours d’exécution sur une version récente de la bibliothèque `Microsoft.Graph.Communications.Calls.Media` .NET. Le bot doit utiliser soit la dernière version disponible du [package NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/), soit une version qui n’a pas plus de trois mois. Les versions antérieures de la bibliothèque sont dépréciées et ne fonctionnent pas après quelques mois. La mise `Microsoft.Graph.Communications.Calls.Media` à jour de la bibliothèque garantit la meilleure interopérabilité entre le bot et Microsoft Teams.

La section suivante fournit des détails sur l’emplacement des appels multimédias en temps réel.

## <a name="real-time-media-calls-stay-where-they-are-created"></a>Les appels multimédias en temps réel restent là où ils sont créés

Les appels multimédias en temps réel restent sur l’ordinateur où ils ont été créés. Un appel multimédia en temps réel est épinglé à l’instance de machine virtuelle (VM) qui a accepté ou démarré l’appel. Le média d’un Microsoft Teams ou d’une réunion est envoyé vers cette instance de la VM, et le support que le bot renvoie à Microsoft Teams doit également provenir de cette VM. Si des appels multimédias en temps réel sont en cours lorsque la VM est arrêtée, ces appels sont brusquement arrêtés. Si le bot a déjà connaissance de l’arrêt de la VM en attente, il peut mettre fin aux appels.

La section suivante fournit des détails sur l’accessibilité des robots multimédias hébergés par l’application.

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>Bots multimédias hébergés par l’application accessibles sur Internet

Les robots multimédias hébergés par l’application doivent être directement accessibles sur Internet. Ces bots doivent inclure les fonctionnalités suivantes :

- Chaque instance d’unem vm hébergeant un bot multimédia hébergé par l’application dans Azure doit être directement accessible à partir d’Internet à l’aide d’une adresse IP publique (ILPIP) au niveau de l’instance.
    - Pour obtenir et configurer un ILPIP pour un service cloud Azure, consultez la vue d’ensemble de [l’adresse IP publique classique au niveau de l’instance](/azure/virtual-network/virtual-networks-instance-level-public-ip).
    - Pour configurer un ILPIP pour un jeu d’échelles de machines virtuelles, voir [public IPv4 par ordinateur virtuel](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine).
- Le service hébergeant un bot multimédia hébergé par l’application doit également configurer chaque instance d’une vm avec un port public qui est mapmé sur l’instance spécifique.
    - Pour un service Cloud Azure, cela nécessite un point de terminaison d’entrée d’instance. Pour plus d’informations, voir [activer la communication pour les instances de rôle dans Azure](/azure/cloud-services/cloud-services-enable-communication-role-instances).
    - Pour un jeu d’échelles de vm, une règle NAT sur l’équilibrage de charge doit être configurée. Pour plus d’informations, [voir les réseaux virtuels et les machines virtuelles dans Azure](/azure/virtual-machines/windows/network-overview).
- Les robots multimédias hébergés par l’application ne sont pas pris en charge par le Bot Framework Emulator.

La section suivante fournit des détails sur les considérations d’évolutivité et de performances des robots multimédias hébergés par l’application.

## <a name="scalability-and-performance-considerations"></a>Considérations relatives à l’évolutivité et aux performances

Les bots multimédias hébergés par l’application nécessitent les considérations suivantes en ce qui a lieu en ce qui a été question de l’évolutivité et des performances :
- Les bots multimédias hébergés par l’application nécessitent plus de capacité de calcul et de réseau (bande passante) que les bots de messagerie et peuvent subir des coûts d’exploitation beaucoup plus élevés. Un développeur de bot multimédia en temps réel doit mesurer avec soin l’évolutivité du bot et s’assurer qu’il n’accepte pas plus d’appels simultanés qu’il ne peut gérer. Un bot vidéo peut être en mesure de supporter une ou deux sessions multimédias simultanées par cœur d’UC (si vous utilisez les formats vidéo RGB24 ou NV12 « bruts »).
- La plateforme Real-time Media ne tire actuellement parti d’aucune unité de traitement graphique (GPU) disponible sur la VM pour décharger le codage/décodage vidéo H.264. Au lieu de cela, le code vidéo et le décodage sont effectués dans le logiciel sur l’UC. Si un processeur graphique est disponible, le bot peut en tirer parti pour son propre rendu graphique, par exemple, si le bot utilise un moteur graphique 3D.
- L’instance de la VM hébergeant le bot multimédia en temps réel doit avoir au moins 2 cœurs d’UC. Pour Azure, une machine virtuelle de la série Dv2 est recommandée. Pour les autres types d’ordinateur virtuel Azure, un système avec quatre processeurs virtuels (vCPU) est la taille minimale requise. Des informations détaillées sur les types de vm Azure sont disponibles dans [la documentation Azure](/azure/virtual-machines/windows/sizes-general). 

## <a name="code-sample"></a>Exemple de code

Les exemples de bots multimédias hébergés par l’application sont les suivants :

| **Exemple de nom** | **Description** | **Graph** |
|------------|-------------|-----------|
| Exemple de média local | Exemples illustrant différents scénarios de médias locaux. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| Exemple de média distant | Exemples illustrant différents scénarios de médias distants. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Formats multimédias pris en charge](~/resources/media-formats.md)

## <a name="see-also"></a>Voir aussi

- [Graph documentation du SDK Calling](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
- Les bots nécessitent plus de capacité de calcul et de bande passante réseau que les bots de messagerie et encourent des coûts d’exploitation beaucoup plus élevés. Un développeur de bot multimédia en temps réel doit mesurer avec soin l’évolutivité du bot et s’assurer qu’il n’accepte pas plus d’appels simultanés qu’il ne peut gérer. Un bot vidéo ne peut supporter qu’une ou deux sessions multimédias simultanées par cœur d’UC si vous utilisez les formats vidéo RGB24 ou NV12 bruts.
- La plateforme Real-time Media ne tire actuellement parti d’aucune unité de traitement graphique (GPU) disponible sur la VM pour décharger le codage ou le décodage vidéo H.264. Au lieu de cela, le code vidéo et le décodage sont effectués dans le logiciel sur l’UC. Si un processeur graphique est disponible, le bot en tire parti pour son propre rendu graphique, par exemple, si le bot utilise un moteur graphique 3D.
- L’instance de la VM hébergeant le bot multimédia en temps réel doit avoir au moins 2 cœurs d’UC. Pour Azure, une machine virtuelle de la série Dv2 est recommandée. Pour les autres types d’ordinateur virtuel Azure, un système avec 4 processeurs virtuels (vCPU) est la taille minimale requise. Pour plus d’informations sur les types de vm Azure, voir [la documentation Azure](/azure/virtual-machines/windows/sizes-general).

La section suivante fournit des exemples qui illustrent différents scénarios de médias locaux.

## <a name="samples-and-additional-resources"></a>Exemples et ressources supplémentaires

- [Exemples d’applications](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Graph documentation du SDK appelant](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)