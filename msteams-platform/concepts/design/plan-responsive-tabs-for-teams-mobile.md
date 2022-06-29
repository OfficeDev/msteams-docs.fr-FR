---
title: Planifier teams mobiles
author: surbhigupta
description: Avec ce module d’apprentissage, vous allez apprendre à planifier la création d’une application sur Teams mobile et à comprendre différentes étapes pour créer une application.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: v-abirade
ms.openlocfilehash: 23f42e07f8c7b44cbcda35b5ed5f8fe17a320271
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66483999"
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

* Tableaux de bord et résumés.
* Visuels de données, cartes et infographies.
* Graphiques, graphiques et tableaux.

:::image type="content" source="../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-consumption.png" alt-text="Afficher les données sous la forme d’une visualisation.":::

Actions rapides :

Dans la deuxième étape, les utilisateurs peuvent travailler sur les graphiques et visuels existants à partir de l’expérience de bureau. Vous pouvez présenter les actions suivantes :

* Rechercher du contenu.
* Filtrer les données.
* Créez des signets.

:::image type="content" source="../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-quick-actions.png" alt-text="Actions rapides sur le graphique et les visuels existants.":::

Activation : 

Dans la troisième étape, permettre aux utilisateurs de créer du contenu tel que des graphiques et des graphiques à partir de zéro. Veillez à introduire toutes les fonctionnalités de votre application pour les appareils mobiles. Par exemple, vous pouvez utiliser des modules de tâche pour accéder à des éléments de données spécifiques avec une vue détaillée.

Vous pouvez fournir l’accès suivant aux utilisateurs :

* Modifiez le titre et la description.
* Insérez des éléments de données pour créer des visualisations.
* Partagez des visualisations dans un canal ou une conversation de groupe.

:::image type="content" source="../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-enablement.png" alt-text="Permettre aux utilisateurs de créer du contenu tel que des graphiques graphiques.":::

<br>

</details>

<br>

<details>

<summary><b>tâche d’intégration d’applications</b></summary>

Vous pouvez comprendre comment planifier des onglets réactifs pour l’intégration des tâches d’applications sur la plateforme mobile Teams.

Consommation:

Dans la première étape, votre application peut afficher la liste des tâches à l’utilisateur dans une pile verticale. S’il existe plusieurs catégories de tâches, telles que **Proposée** , **Active** et **Bouclée**, fournissez des filtres pour afficher les tâches groupées ou en tant qu’en-têtes pour afficher les tâches groupées.

:::image type="content" source="../../assets/images/app-fundamentals/taskboarding-apps-consumption.png" alt-text="Affiche la liste des tâches dans une pile verticale.":::

Actions rapides :

Dans la deuxième étape, vous pouvez fournir l’accès à l’application suivant aux utilisateurs :

* Créez des tâches ou des éléments avec les champs obligatoires pour réduire la charge cognitive des utilisateurs.
* Modifiez le type ou la vue du tableau.
* Passez en revue les tâches en développant la vue.
* Utilisez les modules de tâches pour afficher une vue détaillée.
* Déplacez les tâches dans différentes catégories.
* Partagez les tâches pertinentes dans les conversations et les canaux par le biais d’e-mails et de flux d’activité.

:::image type="content" source="../../assets/images/app-fundamentals/taskboarding-apps-quick-actions.png" alt-text="Créez des tâches pour réduire la charge cognitive des utilisateurs.":::

Activation : 

Dans la troisième étape, vous pouvez activer l’expérience des utilisateurs avec les activités suivantes :

* Ajoutez de nouveaux projets et tableaux.
* Ajoutez et modifiez différentes catégories, telles que **Proposé**, **Actif** et **Fermé**.
* Configurez les tâches pour les commentaires, les pièces jointes et d’autres fonctionnalités complexes.

:::image type="content" source="../../assets/images/app-fundamentals/taskboarding-apps-enablement.png" alt-text="Activez l’expérience utilisateur en ajoutant des projets et des tableaux.":::

<br>

</details>

<br>

<details>

<summary><b>Applications de co-écriture et création de tableau blanc</b></summary>

Vous pouvez comprendre comment planifier des onglets réactifs pour la co-création et le tableau blanc des applications sur la plateforme mobile Teams.

Consommation:

Dans la première étape, vous pouvez envisager l’expérience de bureau pour afficher le contenu et les ressources dans votre application.  Vous pouvez afficher les fonctions suivantes :

* Commentaires ou commentaires.
* Zoom avant ou arrière.
* Étape ou progression actuelle d’un document en attente.

:::image type="content" source="../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-consumption.png" alt-text="Affiche le contenu et les ressources dans l’expérience de bureau.":::

Actions rapides :

Dans la deuxième étape, vous pouvez introduire les actions suivantes :

* Créez un tableau pour la collaboration ou de nouveaux documents pour la signature.
* Partagez des tableaux en interne et également avec des invités.
* Configurez les autorisations d’administrateur.

> [!TIP]
> Vous exposez des actions qui peuvent être affichées facilement sur les petits écrans.

:::image type="content" source="../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-quick-actions.png" alt-text="Présente la création d’un tableau pour la collaboration.":::

Activation : 

Dans la troisième étape, fournissez une expérience complète à vos utilisateurs. Vous pouvez activer l’expérience des utilisateurs avec les activités suivantes :

* Ajout de texte, de formes et de notes rapides.
* Parcourez le contenu.
* Ajoutez des couches et des filtres.
* Opérations de suppression, d’annulation et de restauration.
* Accédez à la caméra et au microphone à l’aide des API du Kit de développement logiciel (SDK) JS. Pour plus d’informations sur les fonctionnalités des appareils, consultez [vue d’ensemble des fonctionnalités des appareils](../device-capabilities/device-capabilities-overview.md).

:::image type="content" source="../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-enablement.png" alt-text="Activez l’expérience utilisateur en ajoutant des formes de texte, des notes rapides et d’autres fonctionnalités.":::

<br>

</details>

## <a name="see-also"></a>Voir aussi

Les instructions de conception et de validation suivantes vous aident en fonction de l’étendue de votre application :

* [Conception de votre onglet](../../tabs/design/tabs.md)
* [Conception de votre bot](../../bots/design/bots.md)
* [Conception de modules de tâches](../..//task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [Recommandations en matière de validation du Store](../deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)
