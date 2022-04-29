---
title: Planifier teams mobiles
author: surbhigupta
description: Guide de planification de la création d’une application sur teams mobile
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-abirade
ms.openlocfilehash: 16eada349d2a6adc5b45e89f075107838594eeeb
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111723"
---
# <a name="plan-responsive-tabs-for-teams-mobile"></a>Planifier des onglets réactifs pour Teams mobile

 La plateforme Teams offre la possibilité de créer des applications sur les appareils mobiles et de bureau. Les utilisateurs de votre application peuvent préférer le bureau ou mobile, ou les deux. Les utilisateurs peuvent préparer des données sur le bureau, mais consommer et partager davantage de données à l’aide de la fonctionnalité mobile. La clé pour créer n’importe quelle application consiste à comprendre et à répondre aux besoins des utilisateurs. Il existe des fonctionnalités telles que les bots, les extensions de message et les connecteurs qui fonctionnent en toute transparence sur les ordinateurs de bureau et les appareils mobiles. Toutefois, la création d’onglets et de modules de tâches nécessite la planification de l’hébergement de votre expérience web sur teams mobile. Cet article vous guide pour planifier vos pages web réactives sur Teams Mobile.

## <a name="identify-apps-scope"></a>Identifier l’étendue des applications

La liste suivante fournit les informations clés pour planifier la création d’applications pour teams mobiles :

* Envisagez les fonctionnalités inter-appareils de l’application Teams. Par exemple, si vous disposez d’une application performante sur le bureau, vous pouvez explorer pour créer une application similaire sur mobile. Au départ, il peut être difficile de déplacer l’ensemble de l’expérience de bureau sur les appareils mobiles. Vous pouvez commencer par des scénarios de base mais courants. Ajoutez des fonctionnalités et des fonctionnalités après avoir collecté plus d’informations et de commentaires des utilisateurs.

* Veillez à cibler le personnage utilisateur approprié sur un appareil mobile. Par exemple, si vous créez une application qui fournit un service aux utilisateurs finaux et fournit également un accès aux données aux développeurs et aux responsables supérieurs, les utilisateurs finaux peuvent utiliser davantage l’application pendant que vous commencez à créer une application sur teams mobile. Vous pouvez répondre à tous les personnages que vous avez sur votre application de bureau. Toutefois, il est recommandé de commencer par un personnage avec une base plus grande et des utilisateurs précoces possibles pour une expérience d’écran plus petite. Conformément à l’exemple, les utilisateurs finaux sont les personnages utilisateur appropriés. Vous pouvez ajouter progressivement des fonctionnalités pour prendre en charge d’autres personnages utilisateur sur votre appareil mobile Teams.

## <a name="understand-different-stages-to-build-apps"></a>Comprendre les différentes étapes de création d’applications

Une fois que vous avez identifié l’étendue de l’application, il est temps de comprendre les trois étapes suivantes pour planifier n’importe quelle application sur Teams mobile et améliorer l’expérience utilisateur :

1. **Consommation**

   Affichez les applications sur les appareils mobiles. Pour créer une application sur mobile, vous pouvez commencer par l’expérience de consommation. Dans la mesure où le monde mobile a fait du défilement du contenu une pratique courante, vous pouvez afficher des informations pertinentes. Utilisez des mécanismes d’engagement, tels que des notifications, pour informer les mises à jour.

2. **Actions rapides**

   Utilisez l’application sur mobile. Une fois que vos utilisateurs ont commencé à consommer le contenu sur mobile, vous pouvez mettre à l’échelle votre application au niveau suivant en migrant certaines actions à partir de l’application de bureau. Vous pouvez optimiser et créer de nouvelles actions pour les appareils mobiles.

3. **Activation**

   Fournissez des expériences d’application complètes pour vous impliquer sur les appareils mobiles. Au fur et à mesure que vos utilisateurs s’engagent dans votre application, offrez une expérience immersive complète sur les appareils mobiles, soit à parité, soit mieux que l’expérience de bureau. Pour offrir une bonne expérience à vos utilisateurs, rendez tous les cas d’usage réactifs sur les appareils mobiles.

> [!TIP]
> Pour obtenir des informations sur les instructions de conception, consultez [processus de conception pour les applications Teams](design-teams-app-process.md).

## <a name="use-cases"></a>Cas d’utilisation

Passons en revue les cas d’usage suivants pour comprendre comment planifier différents types d’applications pour teams mobiles :

<br>

<details>

<summary><b>Tableaux de bord et applications de visualisation des données</b></summary>

Vous pouvez comprendre comment planifier des onglets réactifs pour les applications de tableau de bord et de visualisation des données sur la plateforme mobile Teams.

Consommation:

Dans la première étape, vous pouvez implémenter l’expérience de consommation la plus basique pour afficher les données. L’objectif de n’importe quelle application du domaine est d’afficher des données sous la forme de visualisations. Dans votre application, vous pouvez afficher les visualisations récemment affichées sur le Bureau ou la liste de tous les graphiques autorisés pour les utilisateurs. Après avoir créé des tableaux de bord sur le bureau, les utilisateurs peuvent accéder aux informations à l’aide de l’appareil mobile. Vous pouvez afficher une vue détaillée de n’importe quel graphique sélectionné par l’utilisateur en tant que vue développée dans vos onglets ou à l’aide de modules de tâches.

Vous pouvez afficher les informations suivantes :

* Tableaux de bord et résumés
* Visuels de données, cartes et infographies
* Graphiques, graphiques et tableaux

![Consommation des applications de tableau de bord et de visualisation des données](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-consumption.png)

Actions rapides :

Dans la deuxième étape, les utilisateurs peuvent travailler sur les graphiques et visuels existants à partir de l’expérience de bureau. Vous pouvez présenter les actions suivantes :

* Contenu de la recherche
* Filtrer les données
* Créer des signets

![Actions rapides des applications de tableau de bord et de visualisation des données](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-quick-actions.png)

Activation : 

Dans la troisième étape, permettre aux utilisateurs de créer du contenu tel que des graphiques et des graphiques à partir de zéro. Veillez à introduire toutes les fonctionnalités de votre application pour les appareils mobiles. Par exemple, vous pouvez utiliser des modules de tâche pour accéder à des éléments de données spécifiques avec une vue détaillée.

Vous pouvez fournir l’accès suivant aux utilisateurs :

* Modifier le titre et la description
* Insérer des éléments de données pour créer des visualisations
* Partager des visualisations dans un canal ou une conversation de groupe

![Activation des applications de tableau de bord et de visualisation des données](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-enablement.png)

<br>

</details>

<br>

<details>

<summary><b>tâche d’intégration d’applications</b></summary>

Vous pouvez comprendre comment planifier des onglets réactifs pour l’intégration des tâches d’applications sur la plateforme mobile Teams.

Consommation:

Dans la première étape, votre application peut afficher la liste des tâches à l’utilisateur dans une pile verticale. S’il existe plusieurs catégories de tâches, telles que **Proposée** , **Active** et **Bouclée**, fournissez des filtres pour afficher les tâches groupées ou en tant qu’en-têtes pour afficher les tâches groupées.

![Consommation des applications d’intégration de tâches](../../assets/images/app-fundamentals/taskboarding-apps-consumption.png)

Actions rapides :

Dans la deuxième étape, vous pouvez fournir l’accès à l’application suivant aux utilisateurs :

* Créer des tâches ou des éléments avec les champs obligatoires pour réduire la charge cognitive des utilisateurs
* Modifier le type ou la vue du tableau
* Passer en revue les tâches en développant la vue
* Utiliser des modules de tâche pour afficher une vue détaillée
* Déplacer les tâches dans différentes catégories
* Partager des tâches pertinentes dans des conversations et des canaux via des e-mails et un flux d’activité

![Actions rapides d’intégration de tâches d’applications](../../assets/images/app-fundamentals/taskboarding-apps-quick-actions.png)

Activation : 

Dans la troisième étape, vous pouvez activer l’expérience des utilisateurs avec les activités suivantes :

* Ajouter de nouveaux projets et tableaux
* Ajoutez et modifiez différentes catégories, telles que **Proposée**, **Active** et **Bouclée**
* Configurer les tâches pour les commentaires, les pièces jointes et d’autres fonctionnalités complexes

![Activation des applications d’intégration de tâche](../../assets/images/app-fundamentals/taskboarding-apps-enablement.png)
<br>

</details>

<br>

<details>

<summary><b>Applications de co-écriture et création de tableau blanc</b></summary>

Vous pouvez comprendre comment planifier des onglets réactifs pour la co-création et le tableau blanc des applications sur la plateforme mobile Teams.

Consommation:

Dans la première étape, vous pouvez envisager l’expérience de bureau pour afficher le contenu et les ressources dans votre application.  Vous pouvez afficher les fonctions suivantes :

* Commentaires ou commentaires
* Effectuer un zoom avant ou arrière
* Étape actuelle ou progression d’un document en attente

![Utilisation des applications de co-écriture et création de tableau blanc](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-consumption.png)

Actions rapides :

Dans la deuxième étape, vous pouvez introduire les actions suivantes :

* Créer un tableau pour la collaboration ou de nouveaux documents pour la signature
* Partager des tableaux en interne et avec des invités
* Configurer les autorisations d’administrateur

> [!TIP]
> Vous exposez des actions qui peuvent être affichées facilement sur les petits écrans.

![Actions rapides des applications de co-écriture et création de tableau blanc](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-quick-actions.png)

Activation : 

Dans la troisième étape, fournissez une expérience complète à vos utilisateurs. Vous pouvez activer l’expérience des utilisateurs avec les activités suivantes :

* Ajout de texte, de formes et de notes rapides
* Naviguer dans le contenu
* Ajouter des couches et des filtres
* Opérations de suppression, d’annulation et de rétablissement
* Accédez à la caméra et au microphone à l’aide des API du Kit de développement logiciel (SDK) JS. Pour plus d’informations sur les fonctionnalités des appareils, consultez [vue d’ensemble des fonctionnalités des appareils](../device-capabilities/device-capabilities-overview.md).

![Activation des applications de co-création et de tableau blanc](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-enablement.png)

<br>

</details>

## <a name="see-also"></a>Voir aussi

Les instructions de conception et de validation suivantes vous aident en fonction de l’étendue de votre application :

* [Conception de votre onglet](../../tabs/design/tabs.md)
* [Conception de votre bot](../../bots/design/bots.md)
* [Conception de modules de tâches](../..//task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [Recommandations en matière de validation du Store](../deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)
