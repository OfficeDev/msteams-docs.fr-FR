---
title: Configuration requise et considérations relatives aux robots multimédia hébergés par l’application
description: Découvrez les conditions requises et les considérations importantes liées à la création de robots multimédia hébergés par l’application pour Microsoft Teams.
keywords: ordinateur virtuel Windows Server Azure hébergé par une application
ms.date: 11/16/2018
ms.openlocfilehash: f5b721edacb11e867d05c8213b74036cb51f419c
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801070"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>Configuration requise et considérations relatives aux robots multimédia hébergés par l’application

Toutes les instructions pour le développement de la messagerie et des robots de réponse vocale interactive (IVR) s’appliquent également à la création de robots multimédia hébergés par l’application. Cet article décrit certaines des exigences et considérations importantes pour le développement et l’exécution d’un robot multimédia hébergé par l’application.

> [!NOTE]
> Étant donné que la plateforme multimédia Microsoft Real-Time pour les bots est en version préliminaire pour les développeurs, les conseils de cet article sont susceptibles d’être modifiés.

## <a name="application-hosted-media-bot-development-requires-cnet-and-windows-server"></a>Le développement de Media bot hébergé par l’application requiert C#/.NET et Windows Server

- Un robot multimédia hébergé par une application requiert la `Microsoft.Graph.Communications.Calls.Media` bibliothèque .net ([disponible ici](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) pour accéder aux flux multimédia audio et vidéo, et le bot doit être déployé sur un ordinateur Windows Server (ou système d’exploitation Windows Server invité dans Azure). Par conséquent, le bot doit être développé en C# et dans .NET Framework standard et déployé dans Microsoft Azure. Vous ne pouvez pas utiliser des API C++ ou Node.js pour accéder à des médias en temps réel et .NET Core n’est pas pris en charge pour un robot multimédia hébergé par une application.

- Un robot multimédia hébergé par une application peut être hébergé dans l’un des environnements de service Azure suivants :
  - Service Cloud.
  - Service Fabric avec des ensembles d’adaptations de machines virtuelles (VMSS).
  - Machine virtuelle IaaS (infrastructure as a service).  
  
- Un bot multimédia hébergé par l’application ne peut pas être déployé en tant qu’application Web Azure.

- Un robot multimédia hébergé par une application doit s’exécuter sur une version récente de la `Microsoft.Graph.Communications.Calls.Media` bibliothèque .net. Le bot doit utiliser la version disponible la plus récente du [package NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)ou une version qui n’est pas postérieure à trois mois. Les versions antérieures de la bibliothèque seront déconseillées et risquent de ne pas fonctionner après quelques mois. La mise à jour de la `Microsoft.Graph.Communications.Calls.Media` bibliothèque garantit une meilleure interopérabilité entre le bot et Microsoft Teams.

## <a name="real-time-media-calls-stay-on-the-machine-where-they-were-created"></a>Les appels multimédia en temps réel restent sur l’ordinateur où ils ont été créés.

- Un appel multimédia en temps réel est épinglé à l’instance de machine virtuelle (VM) qui a accepté ou démarré l’appel. Les médias d’un appel ou d’une réunion Microsoft teams iront vers cette instance VM et les médias renvoyés par le robot à Microsoft teams doivent également provenir de cette machine virtuelle.
- Si des appels multimédia en temps réel sont en cours lors de l’arrêt de l’ordinateur virtuel, ces appels seront brusquement arrêtés. Si le bot a une connaissance préalable de l’arrêt de l’ordinateur virtuel en attente, il peut essayer de terminer les appels de manière « appropriée ».

## <a name="application-hosted-media-bots-must-be-directly-accessible-on-the-internet"></a>Les robots multimédia hébergés par l’application doivent être directement accessibles sur Internet.

- Chaque instance VM hébergeant un robot multimédia hébergé sur une application dans Azure doit être directement accessible à partir d’Internet à l’aide d’une adresse IP publique au niveau de l’instance (ILPIP).
  - Pour obtenir et configurer un ILPIP pour un service Cloud Azure, voir [instance Level public IP (Classic) Overview](/azure/virtual-network/virtual-networks-instance-level-public-ip).
  - Pour configurer un ILPIP pour un ensemble d’mises à l’ampleur d’une machine virtuelle, consultez [la rubrique public IPv4 per Virtual Machine](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine).
- Le service hébergeant un robot multimédia hébergé par une application doit également configurer chaque instance VM avec un port accessible au public qui mappe à l’instance spécifique.
  - Pour un service Cloud Azure, cela nécessite un point de terminaison d’entrée d’instance ; consultez la rubrique [activer la communication pour les instances de rôle dans Azure](/azure/cloud-services/cloud-services-enable-communication-role-instances).
  - Pour un ensemble d’ordinateurs VM, une règle NAT sur l’équilibreur de charge doit être configurée ; consultez [la rubrique réseaux virtuels et machines virtuelles dans Azure](/azure/virtual-machines/windows/network-overview).
- Les robots multimédias hébergés par l’application ne sont pas pris en charge par l’émulateur de l’infrastructure bot.

## <a name="scalability-and-performance-considerations"></a>Considérations relatives à l’évolutivité et aux performances

- Les robots multimédias hébergés par l’application nécessitent davantage de capacité de calcul et de réseau (bande passante) que les robots de messagerie et peuvent entraîner des coûts d’exploitation sensiblement plus élevés. Un développeur de robots multimédia en temps réel doit mesurer soigneusement l’évolutivité du robot et s’assurer que le bot n’accepte pas plus d’appels simultanés qu’il ne peut en gérer. Un bot vidéo peut ne prendre en charge qu’une ou deux sessions multimédia simultanées par processeur (en cas d’utilisation des formats vidéo RGB24 ou NV12).
- La plateforme multimédia en temps réel ne bénéficie actuellement d’aucune unité de traitement graphique (GPU) disponible sur l’ordinateur virtuel pour décharger le codage/décodage vidéo H. 264 H. 264. Au lieu de cela, le codage et le décodage vidéo sont effectués dans le logiciel du processeur. Si une unité GPU est disponible, le bot peut en tirer parti pour son propre rendu graphique (par exemple, si le bot utilise un moteur graphique 3D).
- L’instance VM hébergeant le robot multimédia en temps réel doit avoir au moins 2 cœurs d’UC. Pour Azure, il est recommandé d’avoir un ordinateur virtuel dv2 Series. Pour les autres types de machines virtuelles Azure, un système doté de 4 processeurs virtuels (CPU) est la taille minimale requise. Des informations détaillées sur les types de machines virtuelles Azure sont disponibles dans la [documentation Azure](/azure/virtual-machines/windows/sizes-general).

## <a name="samples-and-additional-resources"></a>Exemples et ressources supplémentaires

- [Exemples d’applications](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Documentation du kit de développement logiciel appelant Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
