---
title: Débogage de votre application teams
description: Décrit les étapes à suivre pour exécuter et déboguer des applications Microsoft teams
keywords: teams exécuter des applications de débogage
ms.topic: conceptual
ms.openlocfilehash: 913306bd24a55797e72396a031d917ec99c43bb9
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651968"
---
# <a name="debugging-your-teams-app"></a>Débogage de votre application teams

Les applications Microsoft teams peuvent contenir une ou plusieurs fonctionnalités, et les moyens de les exécuter ou même les héberger peuvent être différents. En ce qui concerne le débogage, en général, nous avons les moyens d’exécuter votre application Microsoft teams de la manière suivante :

* **Purement local** &emsp; Pour les robots, vous pouvez tester votre expérience dans l’émulateur bot. Pour d’autres types de contenu, vous pouvez exécuter localement dans votre navigateur et adresser du contenu via `http://localhost` .
* **Hébergé localement, dans teams** &emsp; Cela implique l’exécution locale du logiciel de tunneling et [la création d’un package](~/concepts/build-and-test/apps-package.md) à [charger](~/concepts/deploy-and-publish/apps-upload.md) dans Teams. Cela vous permet d’exécuter et de déboguer facilement votre application dans le client Teams.
* **Hébergé sur le Cloud, dans teams** Cela simule réellement (ou est) une prise en charge au niveau de la production pour une application Teams. Il implique le téléchargement de votre solution sur votre serveur ou votre fournisseur de Cloud accessible en externe (nous vous recommandons Azure, bien sûr) et la [création d’un package](~/concepts/build-and-test/apps-package.md) à [charger](~/concepts/deploy-and-publish/apps-upload.md) dans Teams.

Pour le test des équipes de façon purement locale ou locale, vous exécutez l’expérience à partir de votre propre ordinateur. Cela vous permet de compiler et d’exécuter réellement dans votre IDE et de tirer pleinement parti de ces techniques comme points d’arrêt et débogage pas à pas. Pour le débogage et le test de l’envergure de production, nous vous recommandons de suivre les instructions de votre entreprise pour vous assurer de pouvoir prendre en charge les tests, la mise en œuvre et le déploiement par le biais de vos propres processus.

En général, nous vous recommandons d’utiliser plusieurs manifestes et packages pour vous permettre de maintenir la séparation entre les services de production et de développement. Par exemple, vous pouvez choisir d’enregistrer des robots de développement et de production distincts et de créer des packages appropriés pour les charger dans votre environnement de test. Nous vous recommandons également de charger et de tester votre package de production avant d’envoyer votre application pour la publication dans notre magasin d’applications ou de la distribuer à des clients.

## <a name="purely-local"></a>Purement local

> [!NOTE]
> En procédant ainsi, vous ne pouvez pas accéder à la fonctionnalité de l’application teams ou aux fonctions de bot propres à Teams, telles que les appels de liste et d’autres fonctionnalités propres au canal. De plus, certaines fonctionnalités peuvent être autorisées par l’infrastructure de robot dans l’émulateur de bot qui peut ne pas fonctionner lors de l’exécution dans Microsoft Teams.

Votre robot peut être exécuté dans l’émulateur bot. Cela vous permet de tester une partie de la logique de base du bot, de voir une disposition approximative des messages et d’effectuer des tests simples. Voici les étapes à effectuer :

* Exécuter le code localement
* Lancez l’émulateur bot et définissez l’URL :
  * Node.js :`http://localhost:3978/api/messages`
  * .NET/C# :`http://localhost:3979/api/messages`
* Ne renseignez pas le champ ID de l’application Microsoft et mot de passe Microsoft App pour qu’ils correspondent aux variables d’environnement par défaut.

## <a name="locally-hosted"></a>Hébergé localement

Étant donné que Microsoft teams est un produit entièrement basé sur le Cloud, il faut que tous les services auxquels il accède soient accessibles au public à l’aide de points de terminaison HTTPs. Par conséquent, pour permettre à votre application de fonctionner dans Teams, vous devez publier le code dans le nuage de votre choix ou rendre notre instance en cours d’exécution accessible en externe. Nous pouvons le faire avec le logiciel de tunneling.

Bien que vous puissiez utiliser n’importe quel outil de choix, nous utilisons et recommandons [ngrok](https://ngrok.com/download), qui crée une URL adressable en externe pour un port que vous ouvrez localement sur votre ordinateur. Pour configurer ngrok en vue de l’exécution locale de votre application Microsoft teams :

* Dans une application Terminal, accédez au répertoire dans lequel vous avez ngrok.exe installé. Vous pouvez l’ajouter en tant que variable PATH pour éviter cette étape.
* Exécutez, par exemple, `ngrok http 3978 --host-header=localhost:3978` ou remplacez le numéro de port selon vos besoins.

Cela lance ngrok pour écouter sur le port que vous spécifiez. En retour, elle vous fournit une URL adressable de manière externe, valide pendant le temps que ngrok est en cours d’exécution.

> [!NOTE]
> Si vous arrêtez et redémarrez ngrok, l’URL change.

Pour utiliser ngrok dans votre projet et selon les fonctionnalités que vous utilisez, vous devez remplacer toutes les références d’URL dans votre code, votre configuration et/ou manifest.jssur le fichier pour utiliser ce point de terminaison d’URL.

Par exemple, pour les robots enregistrés dans Microsoft bot Framework, mettez à jour le point de terminaison de messagerie du bot pour utiliser ce nouveau point de terminaison ngrok. Par exemple, `https://2d1224fb.ngrok.io/api/messages`. Vous pouvez vérifier que ngrok fonctionne en testant la réponse bot dans la fenêtre conversation de test du portail de l’infrastructure bot. (Encore une fois, à l’instar de l’émulateur, ce test ne vous permet pas d’accéder aux fonctionnalités spécifiques des équipes.)

> [!NOTE]
> Pour mettre à jour le point de terminaison de messagerie pour un bot, vous devez utiliser l’infrastructure bot. Cliquez sur votre robot dans [la liste des robots dans l’infrastructure de robot](https://dev.botframework.com/bots). Vous n’avez pas besoin de migrer votre bot vers Microsoft Azure. Vous pouvez également mettre à jour votre point de terminaison de messagerie via l' [application Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="cloud-hosted"></a>Hébergé dans le cloud

Vous pouvez utiliser n’importe quel service adressable en externe pour héberger votre code de développement et de production, ainsi que leurs points de terminaison HTTPs. Il n’y a aucune attente que vos fonctionnalités résident sur le même service. Nous vous recommandons de faire en sorte que tous les domaines consultés à partir de vos applications Microsoft teams soient affichés dans l' [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) objet dans le fichier manifest.js.

> [!NOTE]
> Pour garantir un environnement sécurisé, soyez explicite sur le domaine et les sous-domaines exacts que vous référencez, et ces domaines doivent être dans votre contrôle. Par exemple, `*.azurewebsites.net` n’est pas recommandé, mais le `contoso.azurewebsites.net` ferait.

## <a name="loading-and-running"></a>Chargement et exécution

En général, pour charger et exécuter votre expérience dans Microsoft Teams, vous devez créer un package et le charger dans teams à l’aide des instructions suivantes :

* [Créer le package pour votre application Microsoft teams](~/concepts/build-and-test/apps-package.md)
* [Charger votre application dans Microsoft teams](~/concepts/deploy-and-publish/apps-upload.md)
