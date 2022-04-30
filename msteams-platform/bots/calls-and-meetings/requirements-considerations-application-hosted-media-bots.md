---
title: Exigences et considérations relatives aux bots multimédias hébergés par des applications
description: Comprendre les exigences et considérations importantes, ainsi que les considérations relatives à l’extensibilité et aux performances liées à la création de bots multimédias hébergés par des applications pour Microsoft Teams à l’aide d’exemples de code et d’exemples.
ms.topic: conceptual
ms.localizationpriority: high
keywords: machine virtuelle Windows Server Azure multimédia hébergée par une application
ms.date: 11/16/2018
ms.openlocfilehash: 35ad133d898b53538f51c2ae4c699cd19368f9af
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111982"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>Exigences et considérations relatives aux bots multimédias hébergés par des applications

Un bot multimédia hébergé par une application requiert la [`Microsoft.Graph.Communications.Calls.Media` bibliothèque .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) pour accéder aux flux multimédias audio et vidéo. Le bot doit être déployé sur une machine locale Windows Server ou un système d’exploitation invité Windows Server dans Azure.

> [!NOTE]
>
> * Les conseils pour le développement de bots de messagerie et de réponse vocale interactive (IVR) ne s’appliquent pas complètement à la création de bots multimédias hébergés par des applications.
> * Étant donné que Microsoft Real-time Media Platform for bots est en préversion pour les développeurs, les instructions de ce document sont susceptibles d’être modifiées.

## <a name="c-or-net-and-windows-server-for-development"></a>C# ou .NET et Windows Server pour le développement

Un bot multimédia hébergé par une application requiert les éléments suivants :

* Le bot doit être développé en C# et le .NET Framework standard et déployé dans Microsoft Azure. Vous ne pouvez pas utiliser les API C++ ou Node.js pour accéder aux médias en temps réel et .NET Core n’est pas pris en charge pour un bot multimédia hébergé par une application.

* Le bot peut être hébergé dans l’un des environnements de service Azure suivants :
  * Service cloud.
  * Service Fabric avec Virtual Machine Scale Sets (VMSS).
  * Machine virtuelle IaaS (Infrastructure as a Service).  
  
* Le bot ne peut pas être déployé en tant qu’application web Azure.

* Le bot doit s’exécuter sur une version récente de la bibliothèque .NET `Microsoft.Graph.Communications.Calls.Media`. Le bot doit utiliser la dernière version disponible du [package NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/), ou une version qui n’a pas plus de trois mois. Les versions antérieures de la bibliothèque sont déconseillées et ne fonctionnent pas après quelques mois. La mise à jour de la bibliothèque `Microsoft.Graph.Communications.Calls.Media` garantit la meilleure interopérabilité entre le bot et Microsoft Teams.

La section suivante fournit des détails sur l’emplacement des appels multimédias en temps réel.

## <a name="real-time-media-calls-stay-where-they-are-created"></a>Les appels multimédias en temps réel restent là où ils sont créés

Les appels multimédias en temps réel restent sur l’ordinateur sur lequel ils ont été créés. Un appel multimédia en temps réel est épinglé à l’instance de machine virtuelle qui a accepté ou démarré l’appel. Les médias d’un appel ou d’une réunion Microsoft Teams circulent vers cette instance de machine virtuelle, et les médias que le bot renvoie à Microsoft Teams doivent également provenir de cette machine virtuelle. S’il existe des appels multimédias en temps réel en cours lorsque la machine virtuelle est arrêtée, ces appels sont soudainement arrêtés. Si le bot a connaissance préalablement de l’arrêt de la machine virtuelle en attente, il peut mettre fin aux appels.

La section suivante fournit des détails sur l’accessibilité des bots multimédias hébergés par l’application.

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>Bots multimédias hébergés par des applications accessibles sur Internet

Les bots multimédias hébergés par l’application doivent être directement accessibles sur Internet. Ces bots doivent inclure les fonctionnalités suivantes :

* Chaque instance de machine virtuelle hébergeant un bot multimédia hébergé par une application dans Azure doit être directement accessible à partir d’Internet à l’aide d’une adresse IP publique au niveau de l’instance (ILPIP).
  * Pour obtenir et configurer un ILPIP pour un service cloud Azure, consultez [vue d’ensemble de l’adresse IP publique classique au niveau de l’instance](/azure/virtual-network/virtual-networks-instance-level-public-ip).
  * Pour configurer un ILPIP pour un groupe de machines virtuelles identiques, consultez [IPv4 public par machine virtuelle](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine).
* Le service hébergeant un bot multimédia hébergé par une application doit également configurer chaque instance de machine virtuelle avec un port public qui correspond à l’instance spécifique.
  * Pour un service cloud Azure, cela nécessite un point de terminaison d’entrée d’instance. Pour plus d’informations, consultez [activer la communication pour les instances de rôle dans Azure](/azure/cloud-services/cloud-services-enable-communication-role-instances).
  * Pour un groupe de machines virtuelles identiques, une règle NAT sur l’équilibreur de charge doit être configurée. Pour plus d’informations, consultez [réseaux virtuels et machines virtuelles dans Azure](/azure/virtual-machines/windows/network-overview).

* Les bots multimédias hébergés par l’application ne sont pas pris en charge par le Bot Framework Emulator.

La section suivante fournit des détails sur les considérations relatives à l’extensibilité et aux performances des bots multimédias hébergés par l’application.

## <a name="scalability-and-performance-considerations"></a>Considérations relatives à l’évolutivité et aux performances

Les bots multimédias hébergés par l’application nécessitent les considérations suivantes en matière d’extensibilité et de performances :

* Les bots multimédias hébergés par des applications nécessitent une capacité de calcul et de réseau (bande passante) supérieure à celle des bots de messagerie et peuvent entraîner des coûts opérationnels beaucoup plus élevés. Un développeur de bot multimédia en temps réel doit mesurer avec soin l’extensibilité du bot et s’assurer qu’il n’accepte pas plus d’appels simultanés qu’il ne peut le gérer. Un bot vidéo peut être en mesure de ne gérer qu’une ou deux sessions multimédias simultanées par cœur d’UC (si vous utilisez le « raw » Formats vidéo RVB24 ou NV12).
* La plateforme multimédia en temps réel ne tire actuellement parti d’aucune unité de traitement graphique (GPU) disponible sur la machine virtuelle pour décharger l’encodage/décodage vidéo H.264. Au lieu de cela, l’encodage et le décodage vidéo sont effectués dans les logiciels sur l’UC. Si un GPU est disponible, le bot peut en tirer parti pour son propre rendu graphique, par exemple, si le bot utilise un moteur graphique 3D.
* L’instance de machine virtuelle hébergeant le bot multimédia en temps réel doit avoir au moins 2 cœurs d’UC. Pour Azure, une machine virtuelle de la série Dv2 est recommandée. Pour les autres types de machines virtuelles Azure, un système avec quatre processeurs virtuels est la taille minimale requise. Des informations détaillées sur les types de machines virtuelles Azure sont disponibles dans la [documentation Azure](/azure/virtual-machines/windows/sizes-general).

## <a name="code-sample"></a>Exemple de code

Les exemples de bots multimédias hébergés par l’application sont les suivants :

| **Exemple de nom** | **Description** | **Graph** |
|------------|-------------|-----------|
| Exemple de média local | Exemples illustrant différents scénarios multimédias locaux. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| Exemple de média distant | Exemples qui illustrent différents scénarios multimédias distants. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Formats multimédias pris en charge](~/resources/media-formats.md)

## <a name="see-also"></a>Voir aussi

* Documentation du Kit de développement logiciel (SDK) [Graph Calling](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
* Les bots nécessitent plus de capacité de calcul et de bande passante réseau que les bots de messagerie et entraînent des coûts opérationnels nettement plus élevés. Un développeur de bot multimédia en temps réel doit mesurer avec soin l’extensibilité du bot et s’assurer qu’il n’accepte pas plus d’appels simultanés qu’il ne peut le gérer. Un bot vidéo ne peut supporter qu’une ou deux sessions multimédias simultanées par cœur de processeur si vous utilisez les formats vidéo RVB24 ou NV12 bruts.
* La plateforme multimédia en temps réel ne tire actuellement parti d’aucune unité de traitement graphique (GPU) disponible sur la machine virtuelle pour décharger l’encodage vidéo H.264 ou le décodage. Au lieu de cela, l’encodage et le décodage vidéo sont effectués dans les logiciels sur l’UC. Si un GPU est disponible, le bot en tire parti pour son propre rendu graphique, par exemple, si le bot utilise un moteur graphique 3D.
* L’instance de machine virtuelle hébergeant le bot multimédia en temps réel doit avoir au moins 2 cœurs d’UC. Pour Azure, une machine virtuelle de la série Dv2 est recommandée. Pour les autres types de machines virtuelles Azure, un système avec 4 processeurs virtuels est la taille minimale requise. Pour plus d’informations sur les types de machines virtuelles Azure, consultez [documentation Azure](/azure/virtual-machines/windows/sizes-general).

La section suivante fournit des exemples qui illustrent différents scénarios de médias locaux.

## <a name="samples-and-additional-resources"></a>Exemples et ressources supplémentaires

* [exemples d’applications](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
* [documentation du Kit de développement logiciel (SDK) d’appel Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
