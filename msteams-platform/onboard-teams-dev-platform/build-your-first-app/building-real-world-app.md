---
title: Prise en main de la création de votre première application teams
author: heath-hamilton
ms.author: lajanuar
description: Vue d’ensemble et conditions préalables pour la création de votre première application Microsoft teams
ms.openlocfilehash: 9392096a285a43d3a1f8bed5020e3464da0f7f18
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964664"
---
# <a name="get-started-building-your-first-teams-app"></a>Prise en main de la création de votre première application teams

Dans les leçons créer **votre première application** , vous créez des applications teams de base. Chaque Didacticiel explique comment créer une application de teams simple et réelle de teams tout en vous présentant des outils courants, des concepts fondamentaux et des fonctionnalités plus avancées.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

Voici une idée de ce que vous saurez après les leçons.

> [!div class="checklist"]
  >
  > * **Soyez rapidement opérationnel avec Team Toolkit**: Microsoft teams Toolkit for Visual Studio code s’occupe de la création de votre projet d’application et de votre génération de modèles automatique afin que vous puissiez utiliser une application en cours d’exécution en quelques minutes.
  > * **Définissez votre application avec le manifeste**: le manifeste de l’application est l’endroit où vous spécifiez les capacités et les services utilisés par votre application Teams.
  > * **Portée de l’audience de votre application**: créez une application de teams pour l’utilisation personnelle, la collaboration ou les deux.
  > * **Obtenez de l’expérience avec les infrastructures**: Personnalisez votre application (par exemple, modifiez son jeu de couleurs pour qu’elle corresponde au thème Teams) avec l’aide du kit de développement logiciel JavaScript de teams. En savoir plus sur les outils courants de création et de gestion des robots.
  > * **Développez votre application**: tout au long des leçons, vous trouverez des rubriques connexes qui vous intéresseront probablement (telles que les instructions de conception et d’authentification).

## <a name="teams-app-fundamentals"></a>Principes fondamentaux des applications teams

Avant de commencer les didacticiels, vous devez connaître les points suivants relatifs à la création d’applications pour Teams.

### <a name="apps-can-have-multiple-capabilities"></a>Les applications peuvent avoir plusieurs fonctionnalités

Les applications teams se composent d’une ou de plusieurs [fonctionnalités de plateforme](../capabilities-overview.md). Vous pouvez afficher ces fonctionnalités à l’aide d’un certain nombre de [composants et de conventions de l’interface utilisateur](../doc-links/teams-ui-conventions.md)propres à Teams, tels que des cartes et des modules de tâches.

### <a name="teams-doesnt-host-your-app"></a>Teams n’héberge pas votre application

Une application teams comprend trois parties importantes :

* La logique, le stockage de données et les appels d’API qui alimentent votre application. Ces services ne sont pas hébergés par teams et doivent être accessibles via HTTPs.
* Le client Teams (Web, de bureau ou mobile) où les utilisateurs utilisent votre application.
* Votre package d’application, que vous utilisez pour installer l’application dans Teams. Il contient des métadonnées d’application et des pointeurs vers vos services hébergés.

## <a name="get-prerequisites"></a>Obtenir les conditions préalables

Vérifiez que vous disposez du compte approprié pour créer des applications teams et installer des outils de développement recommandés.

### <a name="set-up-your-development-account"></a>Configurer votre compte de développement

Vous avez besoin d’un compte teams qui autorise les chargement d’applications personnalisées. (Il est possible que votre compte vous fournisse déjà.)

1. Si vous disposez d’un compte Teams, vérifiez si vous pouvez chargement des applications dans teams :
    1. Dans le client Teams, sélectionnez **applications**.
    1. Recherchez une option permettant de **Télécharger une application personnalisée**.

    :::image type="content" source="../doc-links/images/upload-custom-app-closeup.png" alt-text="chargement, option":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>Sélectionnez ici</b> si vous ne voyez pas l’option chargement ou si vous ne disposez pas d’un compte Teams.</summary>

Vous pouvez obtenir un compte de test gratuit teams qui autorise l’application chargement en rejoignant le programme de développement Microsoft 365. (Le processus d’inscription prend environ deux minutes.)

1. Accédez au [programme de développement Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Sélectionnez **rejoindre** et suivez les instructions à l’écran.
1. Lorsque vous accédez à l’écran d’accueil, sélectionnez **configurer l’abonnement E5**.
1. Configurez votre compte d’administrateur. Une fois que vous avez terminé, un écran semblable à celui-ci s’affiche.
:::image type="content" source="../doc-links/images/dev-program-subscription.png" alt-text="affichage de l’abonnement au programme de développement":::
1. Connectez-vous à teams à l’aide du compte d’administrateur que vous venez de configurer.
1. Vérifiez si vous disposez maintenant de l’option **Télécharger une application personnalisée** .

</details>

### <a name="install-your-development-tools"></a>Installer vos outils de développement

Vous pouvez créer des applications teams avec vos outils préférés, mais ces leçons montrent comment vous pouvez commencer rapidement avec Microsoft teams Toolkit pour Visual Studio code.

Teams affiche le contenu de l’application uniquement via les connexions HTTPs. Étant donné que vous hébergerez votre première application localement, vous apprendrez à utiliser [ngrok pour configurer un tunnel sécurisé](../doc-links/debug.md#locally-hosted) entre teams et votre application.

1. Installez [Node.js](https://nodejs.org/en/).
1. Installez la dernière version de [Visual Studio code](https://code.visualstudio.com/download). (Les versions antérieures peuvent ne pas fonctionner avec la boîte à outils.)
1. Dans Visual Studio code, sélectionnez **Extensions** :::image type="icon" source="../doc-links/images/vs-code-extensions.png"::: sur la barre d’activité de gauche et installez le kit de développement **Microsoft teams**.
    :::image type="content" source="../doc-links/images/vsc-install-toolkit.png" alt-text="installer le mode Toolkit":::
1. Installez [ngrok](https://ngrok.com/download).

## <a name="next-step"></a>Étape suivante

Une fois que vous avez configuré votre compte et votre environnement, vous pouvez commencer à créer.

> [!div class="nextstepaction"]
> [Créer et exécuter votre première application](../build-your-first-app/build-and-run.md)
