---
title: Choix d’une configuration pour tester et déboguer votre application
description: Décrit les options de test et de débogage des applications Microsoft Teams
keywords: les équipes exécutent des applications de débogage
ms.topic: conceptual
ms.openlocfilehash: ea851a0d3ecf3ec87093bcc095050190a282c25e
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797798"
---
# <a name="choosing-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Choix d’une configuration pour tester et déboguer votre application Microsoft Teams

Les applications Microsoft Teams peuvent contenir une ou plusieurs fonctionnalités, et les méthodes d’exécuter ou même d’héberger ces fonctionnalités peuvent être différentes. En ce qui concerne le débogage, en général, nous avons les méthodes suivantes pour exécuter votre application Microsoft Teams :

* **Purement local** &emsp; Pour les bots, vous pouvez tester votre expérience dans l’émulateur de bot. Pour d’autres contenus, vous pouvez exécuter localement dans votre navigateur et traiter le contenu via `http://localhost` .
* **Hébergé localement, dans Teams** &emsp; Cela implique l’exécution locale avec un logiciel de tunneling et la [création d’un package](~/concepts/build-and-test/apps-package.md) à [télécharger](~/concepts/deploy-and-publish/apps-upload.md) dans Teams. Cela vous permet d’exécuter et de déboguer facilement votre application dans le client Teams.
* **Hébergé dans le cloud, dans Teams** Cela simule véritablement (ou est) la prise en charge au niveau de la production pour une application Teams. Cela implique le téléchargement de votre solution vers votre serveur accessible en externe ou le fournisseur cloud de votre choix (nous vous recommandons Azure, bien entendu) et la création d’un [package](~/concepts/build-and-test/apps-package.md) à télécharger [dans](~/concepts/deploy-and-publish/apps-upload.md) Teams.

Pour les tests Teams purement locaux ou locaux, vous exécutez l’expérience à partir de votre propre ordinateur. Cela vous permet de compiler et d’exécuter au sein de votre IDE, et de tirer pleinement parti de techniques telles que les points d’arrêt et le débogage d’étape. Pour le débogage et les tests à l’échelle de la production, nous vous recommandons de suivre les instructions de votre entreprise pour vous assurer que vous êtes en mesure de prendre en charge les tests, les étapes et le déploiement par le biais de vos propres processus.

En général, nous vous recommandons d’utiliser plusieurs manifestes et packages pour vous permettre de conserver la séparation entre les services de production et de développement. Par exemple, vous pouvez choisir d’inscrire des robots de développement et de production distincts et de créer des packages appropriés pour les télécharger dans votre environnement de test. Nous vous recommandons également de charger et de tester votre package de production avant de soumettre votre application pour publication dans notre App Store ou de la distribuer aux clients.

## <a name="purely-local"></a>Purement local

> [!NOTE]
> L’exécution de cette façon ne vous permet pas d’accéder aux fonctionnalités de l’application Teams ou aux fonctions de bot propres à Teams, telles que les appels de liste de membres et d’autres fonctionnalités propres au canal. En outre, certaines fonctionnalités peuvent être autorisées par Bot Framework dans l’émulateur de bot qui peuvent ne pas fonctionner lors de l’exécution dans Microsoft Teams.

Votre bot peut être exécuté dans l’émulateur de bot. Cela vous permet de tester une partie de la logique principale du bot, de voir une disposition approximative des messages et d’effectuer des tests simples. Voici les étapes à effectuer :

* Exécuter le code localement
* Lancez l’émulateur de bot et définissez l’URL :
  * Node.js : `http://localhost:3978/api/messages`
  * .NET/C# : `http://localhost:3979/api/messages`
* Laissez l’ID de l’application Microsoft et le mot de passe de l’application Microsoft vides, pour qu’ils correspondent aux variables d’environnement par défaut.

## <a name="locally-hosted"></a>Hébergé localement

Étant donné que Microsoft Teams est un produit entièrement basé sur le cloud, tous les services accessibles doivent être disponibles publiquement à l’aide des points de terminaison HTTPS. Par conséquent, pour permettre à votre application de fonctionner dans Teams, vous devez publier le code dans le cloud de votre choix ou rendre notre instance locale en cours d’exécution accessible en externe. Nous pouvons le faire avec un logiciel de tunneling.

Bien que vous pouvez utiliser n’importe quel outil de votre choix, nous utilisons et recommandons [ngrok,](https://ngrok.com/download)qui crée une URL adressan externe pour un port que vous ouvrez localement sur votre ordinateur. Pour configurer ngrok en vue de l’exécution locale de votre application Microsoft Teams :

* Dans une application terminal, go the directory where you have ngrok.exe installed. Vous pouvez l’ajouter en tant que variable de chemin d’accès pour éviter cette étape.
* Exécutez, par exemple, `ngrok http 3978 --host-header=localhost:3978` ou remplacez le numéro de port selon vos besoins.

Cela lance ngrok pour écouter sur le port que vous spécifiez. En retour, il vous donne une URL adressan externe, valide tant que ngrok est en cours d’exécution.

> [!NOTE]
> Si vous arrêtez et redémarrez ngrok, l’URL change.

Pour utiliser ngrok dans votre projet et en fonction des fonctionnalités que vous utilisez, vous devez remplacer toutes les références d’URL dans votre fichier code, configuration et/ou manifest.jspour utiliser ce point de terminaison d’URL.

Par exemple, pour les bots inscrits dans Microsoft Bot Framework, mettez à jour le point de terminaison de messagerie du bot pour utiliser ce nouveau point de terminaison ngrok. Par exemple, `https://2d1224fb.ngrok.io/api/messages`. Vous pouvez vérifier que ngrok fonctionne en testant la réponse du bot dans la fenêtre de conversation test du portail Bot Framework. (Là encore, comme l’émulateur, ce test ne vous permet pas d’accéder aux fonctionnalités propres à Teams.)

> [!NOTE]
> Pour mettre à jour le point de terminaison de messagerie d’un bot, vous devez utiliser Bot Framework. Cliquez sur votre bot dans [votre liste de bots dans Bot Framework.](https://dev.botframework.com/bots) Vous n’avez pas besoin de migrer votre bot vers Microsoft Azure. Vous pouvez également mettre à jour votre point de terminaison de messagerie via [App Studio.](~/concepts/build-and-test/app-studio-overview.md)

## <a name="cloud-hosted"></a>Hébergé dans le cloud

Vous pouvez utiliser n’importe quel service adressaisable en externe pour héberger votre code de développement et de production et leurs points de terminaison HTTPS. Il n’est pas attendu que vos fonctionnalités résident sur le même service. Nous exigeons que tous les domaines accessibles à partir de vos applications Microsoft Teams soient répertoriés dans l’objet [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) du fichier manifest.jssur.

> [!NOTE]
> Pour garantir un environnement sécurisé, soyez explicite sur le domaine et les sous-domaines exacts que vous référencez, et ces domaines doivent être dans votre contrôle. Par exemple, `*.azurewebsites.net` ce n’est pas recommandé, mais `contoso.azurewebsites.net` c’est le cas.

## <a name="loading-and-running"></a>Chargement et exécution

En règle générale, pour charger et exécuter votre expérience dans Microsoft Teams, vous devez créer un package et le télécharger dans Teams, en suivant les instructions suivantes :

* [Créer le package pour votre application Microsoft Teams](~/concepts/build-and-test/apps-package.md)
* [Télécharger votre application dans Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md)
