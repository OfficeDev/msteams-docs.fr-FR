---
title: Choix d’une configuration pour tester et déboguer votre application
description: Dans ce module, découvrez les options de test et de débogage des applications Microsoft Teams dans un environnement local et hébergé dans le cloud.
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 6b06955df7fbe236deb05fc0e057062aa5f9b180
ms.sourcegitcommit: fb0942afb8be32d92df282dec03fbb3b13f8f303
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/06/2022
ms.locfileid: "67264133"
---
# <a name="choose-a-test-setup-and-debug-your-teams-app"></a>Choisir une configuration de test et déboguer votre application Teams

Les applications Microsoft Teams contiennent une ou plusieurs fonctionnalités et les façons de les exécuter ou même de les héberger sont différentes. Pour le débogage, utilisez l’une des méthodes suivantes :

* **Purement local** : pour les bots, vous pouvez tester votre expérience dans l’émulateur de bot. Pour tout autre contenu, vous pouvez l’exécuter localement dans votre navigateur et traiter le contenu via `http://localhost`.
* **Hébergé localement dans Teams** : cela implique d’exécuter l’application localement dans le logiciel de tunneling et [création de package](~/concepts/build-and-test/apps-package.md) pour les [charger](~/concepts/deploy-and-publish/apps-upload.md) dans Teams. Cela vous permet d’exécuter et de déboguer facilement votre application dans le client Teams.
* **Hébergé dans le cloud dans Teams** : cela simule véritablement la prise en charge au niveau de la production pour une application Teams. Cela implique le chargement de votre solution sur votre serveur ou fournisseur de cloud accessible en externe de votre choix et la [création d’un package](~/concepts/build-and-test/apps-package.md) pour le [charger](~/concepts/deploy-and-publish/apps-upload.md) dans Teams.

Exécutez l’expérience à partir de votre propre ordinateur pour les tests Teams purement locaux ou locaux. En procédant ainsi, vous pouvez compiler et exécuter dans votre environnement de développement intégré et tirer pleinement parti des techniques, telles que les points d’arrêt et le débogage d’étapes.

> [!NOTE]
> Pour le débogage et le test à l’échelle de la production, nous vous recommandons de suivre les instructions de votre propre entreprise pour vous assurer que vous êtes en mesure de prendre en charge les tests, la mise en lots et le déploiement par le biais de vos propres processus.

Utilisez plusieurs manifestes et packages pour maintenir la séparation entre les services de production et de développement. Par exemple, vous pouvez choisir d’inscrire des bots de développement et de production distincts et de créer des packages appropriés pour les charger dans votre environnement de test. Nous vous recommandons également de charger et de tester votre package de production avant de soumettre votre application à des fins de publication dans notre App Store ou de distribution aux clients.

## <a name="purely-local"></a>Purement local

> [!NOTE]
> L’exécution locale du bot ne vous donne pas accès aux fonctionnalités de l’application Teams ou aux fonctions de bot spécifiques à Teams, telles que les appels de liste et d’autres fonctionnalités spécifiques au canal. En outre, certaines fonctionnalités sont autorisées par Bot Framework dans l’émulateur de bot qui peuvent ne pas fonctionner lors de l’exécution dans Teams.

Votre bot peut s’exécuter dans l’émulateur de bot. Cela vous permet de tester une partie de la logique principale du bot, d’afficher une disposition approximative des messages et d’effectuer des tests simples. Voici les étapes :

1. Exécutez le code localement.
2. Lancez l’émulateur de bot et définissez l’URL :
   * Node.js : `http://localhost:3978/api/messages`
   * .NET/C# : `http://localhost:3979/api/messages`
3. Laissez l’ID d’application Microsoft et le mot de passe de l’application Microsoft vides pour correspondre aux variables d’environnement par défaut.

## <a name="locally-hosted"></a>Hébergé localement

Teams est un produit entièrement basé sur le cloud. Tous les services accessibles doivent être disponibles publiquement à l’aide de points de terminaison HTTPS. Par conséquent, pour permettre à votre application de fonctionner dans Teams, vous devez publier le code dans le cloud de votre choix ou rendre notre instance en cours d’exécution locale accessible en externe. Nous pouvons effectuer cette dernière opération avec le logiciel de tunneling.

Bien que vous puissiez utiliser n’importe quel outil de votre choix, nous vous recommandons d’utiliser [ngrok](https://ngrok.com/download), qui crée une URL adressable en externe pour un port que vous ouvrez localement sur votre ordinateur.

Pour configurer ngrok en vue d’exécuter votre application Teams localement, procédez comme suit :

1. Accédez au répertoire où ngrok.exe est installé dans une application de terminal. Vous pouvez l’ajouter en tant que variable de chemin d’accès pour éviter cette étape.
2. Exécutez, par exemple, `ngrok http 3978 --host-header=localhost:3978` ou remplacez le numéro de port si nécessaire.
   Cela lance ngrok à répertorier sur le port que vous spécifiez. En retour, il vous donne une URL adressable en externe valide tant que ngrok est en cours d’exécution.

> [!NOTE]
> Si vous arrêtez et redémarrez ngrok, l’URL change.

Pour utiliser ngrok dans votre projet en fonction des fonctionnalités que vous utilisez, vous devez remplacer toutes les références d’URL dans votre code, configuration et fichier manifest.json pour utiliser ce point de terminaison d’URL.

Pour les bots inscrits dans le Microsoft Bot Framework, mettez à jour le point de terminaison de messagerie du bot pour utiliser ce nouveau point de terminaison ngrok. Par exemple : `https://2d1224fb.ngrok.io/api/messages`. Vous pouvez vérifier que ngrok fonctionne en testant la réponse du bot dans la fenêtre de conversation Test du portail Bot Framework. Là encore, comme l’émulateur, ce test ne vous permet pas d’accéder aux fonctionnalités spécifiques à Teams.

> [!NOTE]
>
> * Pour mettre à jour le point de terminaison de messagerie d’un bot, vous devez utiliser le Bot Framework. Sélectionnez votre bot dans [votre liste de bots dans Bot Framework](https://dev.botframework.com/bots). Vous n’avez pas besoin de migrer votre bot vers Microsoft Azure. Vous pouvez également mettre à jour votre point de terminaison de messagerie via [App Studio](~/concepts/build-and-test/app-studio-overview.md).

> [!WARNING]
>
> * Si vous utilisez App Studio, nous vous recommandons d’essayer le Developer Portal pour configurer, distribuer et gérer vos applications Teams. App Studio est déconseillé le 1er août 2022.

## <a name="cloud-hosted"></a>Hébergé dans le cloud

Vous pouvez utiliser n’importe quel service adressable en externe pour héberger votre code de développement et de production et leurs points de terminaison HTTPS. Il n’est pas prévu que vos fonctionnalités résident sur le même service. Nous exigeons que tous les domaines soient accessibles à partir de vos applications Teams répertoriées dans l’objet [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) dans le `manifest.json` fichier.

> [!NOTE]
> Pour garantir un environnement sécurisé, soyez explicite sur le domaine et les sous-domaines exacts que vous référencez, et ces domaines doivent être sous votre contrôle. Par exemple, `*.azurewebsites.net` n’est pas recommandé, mais `contoso.azurewebsites.net` est recommandé.

## <a name="load-and-run-your-experience"></a>Charger et exécuter votre expérience

Pour charger et exécuter votre expérience dans Teams, vous devez créer un package et le charger dans Teams. Pour plus d’informations, reportez-vous aux rubriques suivantes :

* [Créer le package pour votre application Microsoft Teams](~/concepts/build-and-test/apps-package.md).
* [Charger votre application dans Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Ajouter des données de test à votre environnement](~/concepts/build-and-test/test-data.md)

## <a name="see-also"></a>Voir aussi

[Tester et déboguer votre bot localement avec l’IDE](../../bots/how-to/debug/locally-with-an-ide.md#test-and-debug-your-bot-locally-with-ide)
