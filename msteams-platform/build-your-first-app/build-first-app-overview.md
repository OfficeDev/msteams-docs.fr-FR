---
title: Commencer à créer une application de première équipe
author: heath-hamilton
description: Vue d’ensemble et conditions préalables à la création d’une application Microsoft teams
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: bcfbcaa9de85f4b7135483aed3d1d11bf8bffad6
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210108"
---
# <a name="building-your-first-teams-app-overview"></a>Présentation de la création de votre première application teams

Dans les leçons créer **votre première application** , vous créez des applications teams de base. Chaque Didacticiel explique comment créer une application de teams simple et réelle de teams tout en vous présentant des outils courants, des concepts fondamentaux et des fonctionnalités plus avancées.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

Voici une idée de ce que vous saurez après les leçons.

> [!div class="checklist"]
  >
  > * **Soyez rapidement opérationnel avec Team Toolkit**: Microsoft teams Toolkit for Visual Studio code s’occupe de la création de votre projet d’application et de votre génération de modèles automatique afin que vous puissiez utiliser une application en cours d’exécution en quelques minutes.
  > * **Définissez votre application avec le manifeste**: le manifeste de l’application est l’endroit où vous spécifiez les capacités et les services utilisés par votre application Teams.
  > * **Portée de l’audience de votre application**: créez une application de teams pour l’utilisation personnelle, la collaboration ou les deux.
  > * **Obtenez de l’expérience avec Team frameworks**: Personnalisez votre application (par exemple, modifiez son jeu de couleurs pour qu’elle corresponde au thème Teams) avec l’aide du kit de développement logiciel JavaScript de teams. En savoir plus sur les outils courants de création et de gestion des robots.
  > * **Développez votre application**: tout au long des leçons, vous trouverez des rubriques connexes qui vous intéresseront probablement (telles que les instructions de conception et d’authentification).

## <a name="teams-app-fundamentals"></a>Principes fondamentaux des applications teams

Avant de commencer les didacticiels, vous devez connaître les points suivants relatifs à la création d’applications pour Teams.

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>Les applications peuvent avoir plusieurs fonctionnalités et points d’entrée

Les applications teams se composent d’une ou de plusieurs [fonctionnalités de plateforme](../concepts/capabilities-overview.md) et de [points d’entrée](../concepts/extensibility-points.md). Vous pouvez présenter votre application à l’aide d’un certain nombre de [composants et de conventions d’interface utilisateur](../concepts/extensibility-points.md#ui-components)propres à Teams, tels que des cartes et des modules de tâches.

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

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où, dans Teams, vous pouvez télécharger une application personnalisée.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>Sélectionnez ici</b> si vous ne voyez pas l’option chargement ou si vous ne disposez pas d’un compte Teams.</summary>

Vous pouvez obtenir un compte de test gratuit teams qui autorise l’application chargement en rejoignant le programme de développement Microsoft 365. (Le processus d’inscription prend environ deux minutes.)

1. Accédez au [programme de développement Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Sélectionnez **rejoindre** et suivez les instructions à l’écran.
1. Lorsque vous accédez à l’écran d’accueil, sélectionnez **configurer l’abonnement E5**.
1. Configurez votre compte d’administrateur. Une fois que vous avez terminé, un écran semblable à celui-ci s’affiche.
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrit au programme pour les développeurs Microsoft 365.":::
1. Connectez-vous à teams à l’aide du compte d’administrateur que vous venez de configurer.
1. Vérifiez si vous disposez maintenant de l’option **Télécharger une application personnalisée** .

</details>

### <a name="install-your-development-tools"></a>Installer vos outils de développement

Vous pouvez créer des applications teams avec vos outils préférés, mais ces leçons montrent comment vous pouvez commencer rapidement avec Microsoft teams Toolkit pour Visual Studio code.

Teams affiche le contenu de l’application uniquement via les connexions HTTPs. Étant donné que vous hébergerez votre première application localement pour gagner du temps, vous apprendrez à utiliser [ngrok pour configurer un tunnel sécurisé](../concepts/build-and-test/debug.md#locally-hosted) entre teams et votre application. (Les applications teams de niveau production sont hébergées dans le Cloud.)

1. Installez [Node.js](https://nodejs.org/en/).
1. Installez [ngrok](https://ngrok.com/download).
1. Installez la dernière version de [Visual Studio code](https://code.visualstudio.com/download). (Les versions antérieures peuvent ne pas fonctionner avec la boîte à outils.)
1. Dans Visual Studio code, sélectionnez **Extensions** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: sur la barre d’activité de gauche et installez le kit de développement **Microsoft teams**.
    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Illustration montrant où dans Visual Studio code vous pouvez installer l’extension Microsoft teams Toolkit.":::

## <a name="about-the-tutorials"></a>À propos des didacticiels

Vous pouvez commencer avec n’importe quelle équipe de **création de votre première** expérience d’application. Si vous ne savez pas où commencer, suivez notre chemin convivial et créez un « Hello, World ! ». Phone.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Arborescence des compétences montrant des cursus pour les didacticiels « créer vos premières applications » Teams." border="false":::

## <a name="next-step"></a>Étape suivante

Une fois que vous avez configuré votre compte et votre environnement, vous pouvez commencer à créer.

### <a name="beginner-friendly-tutorial"></a>Didacticiel convivial

> [!div class="nextstepaction"]
> [Créer une application « Hello, World ! »](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>Autres didacticiels

> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [Créer une extension de messagerie](../build-your-first-app/build-messaging-extension.md)