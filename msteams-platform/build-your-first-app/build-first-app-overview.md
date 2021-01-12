---
title: Get started - Build your first app overview and prerequisites
author: heath-hamilton
description: Découvrez comment commencer à développer des applications Microsoft Teams et configurer votre environnement.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 06e26c57e6f6d3fd0bbeb981ef7ab46c8217bb4a
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795460"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a>Créer votre première vue d’ensemble de l’application Microsoft Teams

Dans la création **de vos premières leçons d’application,** vous créez des applications Teams de base. Chaque didacticiel vous montre comment créer une application Teams simple et réelle tout en vous présentant des outils courants, des concepts fondamentaux et des fonctionnalités plus avancées.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

Voici une idée de ce que vous allez savoir après avoir tiré les leçons.

> [!div class="checklist"]
  >
  > * Mise en route rapide avec le **Shared Computer Toolkit Teams**: le Shared Computer Toolkit Microsoft Teams pour Visual Studio Code s’occupe de la création de votre projet d’application et de la création d’une application en quelques minutes.
  > * **Configurez votre application avec App Studio :** spécifiez les fonctionnalités et les services que votre application Teams utilise.
  > * **Étendue de l’audience de votre application**: créez une application Teams pour un usage personnel, la collaboration ou les deux.
> * **Obtenez de l’expérience avec les outils et les SDK Teams**: personnalisez votre application avec l’aide du SDK client JavaScript teams. Par exemple, modifiez le jeu de couleurs de votre application pour qu’il corresponde au thème Teams. Découvrez également les outils courants pour créer et gérer des bots.
  > * **Développez votre application**: tout au long des leçons, vous trouverez des rubriques connexes qui vous intéressent probablement (telles que les instructions d’authentification et de conception).

## <a name="teams-app-fundamentals"></a>Principes de base de l’application Teams

Avant de commencer les didacticiels, vous devez connaître les informations suivantes sur la création d’applications pour Teams.

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>Les applications peuvent avoir plusieurs fonctionnalités et points d’entrée

Une application Teams est composé d’une ou de plusieurs fonctionnalités de plateforme [(comment](../concepts/capabilities-overview.md) les personnes utilisent l’application) et [de points](../concepts/extensibility-points.md) d’entrée (où les personnes découvrent l’application).

### <a name="teams-doesnt-host-your-app"></a>Teams n’héberge pas votre application

Une application Teams comprend les éléments importants suivants :

* La logique, le stockage des données et les appels d’API qui sont à l’alimentation de votre application. Ces services ne sont pas hébergés par Teams et doivent être accessibles via HTTPS.
* Client Teams (web, de bureau ou mobile) où les utilisateurs utilisent votre application.
* Votre ID d’application, qui vous permet de configurer votre application avec App Studio.

## <a name="get-prerequisites"></a>Obtenir les conditions préalables

Vérifiez que vous avez le bon compte pour créer des applications Teams et installez certains outils de développement recommandés.

### <a name="set-up-your-development-account"></a>Configurer votre compte de développement

Vous avez besoin d’un compte Teams qui autorise le chargement de version de version d’application personnalisée. (Votre compte peut déjà le fournir.)

1. Si vous avez un compte Teams, vérifiez si vous pouvez télécharger une version de version de chargement d’applications dans Teams :
    1. Dans le client Teams, sélectionnez **Applications.**
    1. Recherchez une option pour **télécharger une application personnalisée.**

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>Sélectionnez ici</b> si vous ne pouvez pas voir l’option de chargement de version de version ou si vous n’avez pas de compte Teams.</summary>

Vous pouvez obtenir un compte de test Teams gratuit qui permet le chargement de version test d’application en rejoignant le programme microsoft 365 développeur. (Le processus d’inscription prend environ deux minutes.)

1. Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).
1. Sélectionnez **Rejoindre maintenant** et suivez les instructions à l’écran.
1. Lorsque vous arrivez à l’écran d’accueil, **sélectionnez Configurer l’abonnement E5.**
1. Configurer votre compte d’administrateur. Une fois que vous avez terminé, vous devriez voir un écran comme celui-ci.
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrire au programme pour les développeurs Microsoft 365.":::
1. Connectez-vous à Teams à l’aide du compte d’administrateur que vous viennent de configurer.
1. Vérifiez si vous avez désormais l’option **Télécharger une application personnalisée.**

</details>

> [!Note]
> Si vous ne pouvez toujours pas charger une version de version de chargement d’applications, voir activer les applications Teams personnalisées et activer le chargement [d’applications personnalisées.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)

### <a name="install-your-development-tools"></a>Installer vos outils de développement

Vous pouvez créer des applications Teams avec vos outils préférés, mais ces leçons montrent comment vous pouvez commencer rapidement avec microsoft Teams Shared Computer Toolkit for Visual Studio Code.

Teams affiche le contenu de l’application uniquement par le biais de connexions HTTPS. Pour déboguer certains types d’applications localement, comme un bot, vous allez apprendre à utiliser [ngrok](../concepts/build-and-test/debug.md#locally-hosted) pour configurer un tunnel sécurisé entre Teams et votre application. (Les applications De Production Teams sont hébergées dans le cloud.)

1. Installez [Node.js](https://nodejs.org/en/).
1. Installez [ngrok](https://ngrok.com/download) si vous prévoyez de créer un bot ou une extension de messagerie.
1. Installez la dernière version de [Visual Studio Code](https://code.visualstudio.com/download). (Les versions antérieures peuvent ne pas fonctionner avec le kit de ressources.)
1. In Visual Studio Code, select **Extensions** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: on the left Activity Bar and install the Microsoft Teams **Shared Computer Toolkit**.

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Illustration montrant où, dans Visual Studio Code, vous pouvez installer l’extension Shared Computer Toolkit Microsoft Teams.":::

## <a name="about-the-tutorials"></a>À propos des didacticiels

Vous pouvez commencer avec n’importe quelle équipe qui **crée vos premières leçons** d’application. Si vous ne savez pas où aller en premier, suivez notre chemin d’accès convivial débutant et créez un « Hello, World! » application.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Arborescence de compétences montrant les parcours d’apprentissage pour les didacticiels « Créer votre première application » teams." border="false":::

## <a name="next-step"></a>Étape suivante

Une fois que vous avez installé votre compte et votre environnement, vous pouvez commencer la création.

### <a name="beginner-friendly-tutorial"></a>Didacticiel convivial pour débutant

> [!div class="nextstepaction"]
> [Créer une application « Hello, World! »](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>Autres didacticiels

> [!div class="nextstepaction"]
> [Créer un bot](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [Créer une extension de messagerie](../build-your-first-app/build-messaging-extension.md)
