---
title: Choix d’une configuration pour tester et déboguer votre application
description: Décrit les options de test et de débogage Microsoft Teams applications dans un environnement local et hébergé dans le cloud.
keywords: les équipes exécutent des applications de débogage hébergées localement sur le cloud
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: eddcd41a7bebae183df079bc5dfe67deed65056e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355705"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Choisir une configuration pour tester et déboguer votre Microsoft Teams application

Microsoft Teams applications contiennent une ou plusieurs fonctionnalités et les façons de les exécuter ou même de les héberger sont différentes. Pour le débogage, utilisez l’une des méthodes suivantes :

* **Purement local** : pour les bots, vous pouvez tester votre expérience dans bot Emulator. Pour d’autres contenus, vous pouvez exécuter localement dans votre navigateur et traiter le contenu via `http://localhost`.
* **Hébergé localement dans Teams** : cela implique l’exécution de l’application localement dans un logiciel de tunneling et la création [](~/concepts/deploy-and-publish/apps-upload.md) d’un [package](~/concepts/build-and-test/apps-package.md) à charger dans Teams. Cela vous permet d’exécuter et de déboguer facilement votre application dans le client Teams client.
* **Hébergé dans le cloud dans Teams** : cela simule véritablement la prise en charge du niveau de production pour une Teams application. Cela implique le téléchargement de votre solution vers votre serveur ou fournisseur cloud accessible en externe de votre choix et la création d’un [package](~/concepts/build-and-test/apps-package.md) à télécharger dans Teams.[](~/concepts/deploy-and-publish/apps-upload.md)

Exécutez l’expérience à partir de votre propre ordinateur pour des tests de Teams local ou purement local. En faisant cela, vous pouvez compiler et exécuter dans votre environnement de développement intégré et tirer pleinement parti des techniques, telles que les points d’arrêt et le débogage d’étape.

> [!NOTE]
> Pour le débogage et les tests à l’échelle de la production, nous vous recommandons de suivre les instructions de votre entreprise pour vous assurer que vous êtes en mesure de prendre en charge les tests, les étapes et le déploiement par le biais de vos propres processus.

Utilisez plusieurs manifestes et packages pour conserver la séparation entre les services de production et de développement. Par exemple, vous pouvez choisir d’inscrire des bots de développement et de production distincts et de créer des packages appropriés pour les télécharger dans votre environnement de test. Nous vous recommandons également de charger et de tester votre package de production avant de soumettre votre application pour publication dans notre App Store ou la distribution aux clients.

## <a name="purely-local"></a>Purement local

> [!NOTE]
> L’exécution locale du bot ne vous permet pas d’accéder aux fonctionnalités de l’application Teams ni aux fonctions de bot spécifiques à Teams telles que les appels de liste de membres et d’autres fonctionnalités propres au canal. En outre, certaines fonctionnalités sont autorisées par Bot Framework dans bot Emulator qui peuvent ne pas fonctionner lors de l’exécution en Microsoft Teams.

Votre bot peut s’exécuter dans le bot Emulator. Cela vous permet de tester une partie de la logique principale du bot, de voir une disposition approximative des messages et d’effectuer des tests simples. Voici les étapes à suivre :

1. Exécutez le code localement.
2. Lancez le bot Emulator et définissez l’URL :
   * Node.js : `http://localhost:3978/api/messages`
   * .NET/C# : `http://localhost:3979/api/messages`
3. Laissez l’ID de l’application Microsoft et le mot de passe de l’application Microsoft vides pour qu’ils correspondent aux variables d’environnement par défaut.

## <a name="locally-hosted"></a>Hébergé localement

Microsoft Teams est un produit entièrement basé sur le cloud, tous les services accessibles doivent être disponibles publiquement à l’aide des points de terminaison HTTPS. Par conséquent, pour permettre à votre application de fonctionner dans Teams, vous devez publier le code dans le cloud de votre choix ou rendre notre instance locale en cours d’exécution accessible en externe. Nous pouvons le faire avec un logiciel de tunneling.

Bien que vous pouvez utiliser n’importe quel outil de votre choix, nous utilisons et recommandons [ngrok](https://ngrok.com/download), qui crée une URL adressan externe pour un port que vous ouvrez localement sur votre ordinateur.

Pour configurer ngrok en vue de l’exécution Microsoft Teams votre application localement, suivez les étapes suivantes :

1. Go to the directory where you have ngrok.exe installed in a terminal application. Vous pouvez l’ajouter en tant que variable de chemin d’accès pour éviter cette étape.
2. Exécutez, par exemple, `ngrok http 3978 --host-header=localhost:3978`ou remplacez le numéro de port selon vos besoins.
   Cela lance ngrok pour la liste sur le port que vous spécifiez. En retour, il vous donne une URL adressan externe valide tant que ngrok est en cours d’exécution.

> [!NOTE]
> Si vous arrêtez et redémarrez ngrok, l’URL change.

Pour utiliser ngrok dans votre projet en fonction des fonctionnalités que vous utilisez, vous devez remplacer toutes les références d’URL dans votre code, configuration et fichier manifest.json pour utiliser ce point de terminaison d’URL.

Pour les bots inscrits dans le Microsoft Bot Framework, mettez à jour le point de terminaison de messagerie du bot pour utiliser ce nouveau point de terminaison ngrok. Par exemple : `https://2d1224fb.ngrok.io/api/messages`. Vous pouvez vérifier que ngrok fonctionne en testant la réponse du bot dans la fenêtre de conversation test du portail Bot Framework. Là encore, comme l’émulateur, ce test ne vous permet pas d’accéder Teams fonctionnalités spécifiques.

> [!NOTE]
> Pour mettre à jour le point de terminaison de messagerie d’un bot, vous devez utiliser Bot Framework. Sélectionnez votre bot [dans votre liste de bots dans Bot Framework](https://dev.botframework.com/bots). Vous n’avez pas besoin de migrer votre bot vers Microsoft Azure. Vous pouvez également mettre à jour votre point de terminaison de messagerie via [App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="cloud-hosted"></a>Hébergé dans le cloud

Vous pouvez utiliser n’importe quel service adressan externe pour héberger votre code de développement et de production et leurs points de terminaison HTTPS. Il n’est pas attendu que vos fonctionnalités résident sur le même service. Nous exigeons que tous les domaines soient accessibles à partir Microsoft Teams applications répertoriées dans [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) l’objet dans le `manifest.json` fichier.

> [!NOTE]
> Pour garantir un environnement sécurisé, soyez explicite sur le domaine et les sous-domaines exacts que vous référencez et ces domaines doivent être dans votre contrôle. Par exemple, `*.azurewebsites.net` n’est pas recommandé, mais `contoso.azurewebsites.net` il est recommandé.

## <a name="load-and-run-your-experience"></a>Charger et exécuter votre expérience

Pour charger et exécuter votre expérience dans Microsoft Teams, vous devez créer un package et le télécharger dans Teams. Pour plus d’informations, voir :

* [Créez le package pour votre Microsoft Teams application.](~/concepts/build-and-test/apps-package.md)
* [Télécharger votre application dans Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Ajouter des données de test à votre environnement](~/concepts/build-and-test/test-data.md)

## <a name="see-also"></a>Voir aussi

[Tester et déboguer votre bot localement](../../bots/how-to/debug/locally-with-an-ide.md#test-and-debug-your-bot-locally)
