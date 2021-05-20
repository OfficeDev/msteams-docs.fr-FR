---
title: Choisir une configuration pour tester et débobug votre application
description: Décrit les options de test et de débogage Microsoft Teams applications
keywords: les équipes exécutent des applications de débogage
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 1f11834ad83e8bea7e4114d25d022df2f62c1700
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565157"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Choisissez une configuration pour tester et débobug votre application Microsoft Teams

Microsoft Teams applications contiennent une ou plusieurs fonctionnalités et les moyens de les exécuter ou même de les héberger sont différents. Pour le débogage, utilisez l’une des façons suivantes :

* **Purement local :** Pour les bots, vous pouvez tester votre expérience dans l’Émulateur Bot. Pour d’autres contenus, vous pouvez exécuter localement dans votre navigateur et adresser le contenu à travers `http://localhost` .
* **Hébergé localement dans Teams**: Il s’agit d’exécuter l’application localement dans un logiciel de tunneling [et de créer un package](~/concepts/build-and-test/apps-package.md) [à](~/concepts/deploy-and-publish/apps-upload.md) télécharger dans Teams. Cela vous permet d’exécuter et de débobug facilement votre application au sein Teams client.
* **Hébergée dans le cloud Teams**: Cela simule vraiment la prise en charge au niveau de production d’une Teams’application. Il s’agit de télécharger votre solution sur votre serveur ou fournisseur de cloud accessible à l’extérieur de votre choix et [de créer](~/concepts/build-and-test/apps-package.md) [un package à](~/concepts/deploy-and-publish/apps-upload.md) télécharger dans Teams.

Exécutez l’expérience à partir de votre propre ordinateur pour des tests de Teams locaux ou locaux. Ce faisant, vous pouvez compiler et exécuter dans votre environnement de développement intégré et tirer pleinement parti des techniques, telles que les points d’arrêt et le débogage d’étapes. 

> [!NOTE]
> Pour le débogage et les tests à l’échelle de la production, nous vous recommandons de suivre les directives de votre propre entreprise pour vous assurer que vous êtes en mesure de prendre en charge les tests, la mise en scène et le déploiement à travers vos propres processus.

Utilisez plusieurs manifestes et paquets pour maintenir la séparation entre les services de production et de développement. Par exemple, vous pouvez choisir d’enregistrer des robots de développement et de production distincts et de créer des paquets appropriés pour les télécharger dans votre environnement de test. Nous vous recommandons également de télécharger et de tester votre package de production avant de soumettre votre application pour publication dans notre App Store ou distribution aux clients.

## <a name="purely-local"></a>Purement local

> [!NOTE]
> L’exécution du bot localement ne vous donne pas accès à la fonctionnalité de l’application Teams ou aux fonctions de bot spécifiques à Teams comme les appels de liste et d’autres fonctionnalités spécifiques au canal. En outre, certaines fonctionnalités sont autorisées par le cadre bot dans l’émulateur bot qui pourrait ne pas fonctionner lors de l’exécution Microsoft Teams.

Votre bot peut fonctionner dans l’émulateur Bot. Cela vous permet de tester une partie de la logique de base du bot, voir une mise en page approximative des messages, et effectuer des tests simples. Voici les étapes suivantes :

1. Exécutez le code localement.
2. Lancez l’émulateur Bot et définissez l’URL :
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#: `http://localhost:3979/api/messages`
3. Laissez l’ID de l’application Microsoft et le mot de passe de l’application Microsoft vierges, pour correspondre aux variables d’environnement par défaut.

## <a name="locally-hosted"></a>Hébergé localement

Microsoft Teams est un produit entièrement basé sur le cloud, il nécessite que tous les services qu’il accède soient disponibles publiquement en utilisant les points de terminaison HTTPS. Par conséquent, pour permettre à votre application de fonctionner dans les Teams, vous devez soit publier le code sur le nuage de votre choix, soit rendre notre instance de fonctionnement locale accessible à l’extérieur. Nous pouvons faire ce dernier avec un logiciel de tunneling.

Bien que vous puissiez utiliser n’importe quel outil de votre choix, nous utilisons [et recommandons ngrok](https://ngrok.com/download), qui crée une URL adressable extérieurement pour un port que vous ouvrez localement sur votre machine. 

**Pour configurer ngrok en vue de l’exécution de votre application Microsoft Teams localement**

1. Rendez-vous à l’annuaire où vous ngrok.exe installé dans une application terminale. Vous pouvez l’ajouter comme variable de chemin pour éviter cette étape.
2. Exécutez, par exemple, `ngrok http 3978 --host-header=localhost:3978` ou remplacez le numéro de port au besoin.
   Cela lance ngrok à la liste sur le port que vous spécifiez. En retour, il vous donne une URL adressable extérieurement valide aussi longtemps que ngrok est en cours d’exécution.

> [!NOTE]
> Si vous arrêtez et redémarrez ngrok, l’URL change.

Pour utiliser ngrok dans votre projet en fonction des fonctionnalités que vous utilisez, vous devez remplacer toutes les références URL dans votre code, configuration et manifest.jsdans le fichier pour utiliser ce point de terminaison URL.

Pour les bots enregistrés dans le Microsoft Bot Framework, mettez à jour le point de terminaison de messagerie du bot pour utiliser ce nouveau point de terminaison ngrok. Par exemple : `https://2d1224fb.ngrok.io/api/messages`. Vous pouvez valider que ngrok fonctionne en testant la réponse bot dans la fenêtre de chat test du portail Bot Framework. Encore une fois, comme l’émulateur, ce test ne vous permet pas d’accéder Teams fonctionnalité spécifique.

> [!NOTE]
> Pour mettre à jour le point de terminaison de messagerie d’un bot, vous devez utiliser le framework Bot. Sélectionnez votre bot [dans votre liste de bots dans Bot Framework](https://dev.botframework.com/bots). Vous n’avez pas besoin de migrer votre bot vers Microsoft Azure. Vous pouvez également mettre à jour votre point de terminaison de messagerie [via App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="cloud-hosted"></a>Hébergé dans le cloud

Vous pouvez utiliser n’importe quel service adressable externement pour héberger votre code de développement et de production et leurs points de terminaison HTTPS. On ne s’attend pas à ce que vos capacités résident sur le même service. Nous exigeons que tous les domaines soient accessibles à partir de vos Microsoft Teams applications répertoriées dans [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) l’objet dans le `manifest.json` fichier.

> [!NOTE]
> Pour assurer un environnement sécurisé, soyez explicite sur le domaine exact et les sous-domaines que vous référez et ces domaines doivent être sous votre contrôle. Par exemple, `*.azurewebsites.net` n’est pas recommandé, cependant `contoso.azurewebsites.net` est recommandé.

## <a name="load-and-run-your-experience"></a>Chargez et exécutez votre expérience

Pour charger et exécuter votre expérience dans Microsoft Teams, vous devez créer un paquet et le télécharger dans Teams. Pour plus d'informations, voir :

* [Créez le paquet pour votre application Microsoft Teams.](~/concepts/build-and-test/apps-package.md)
* [Télécharger votre application dans Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"] 
> [Ajouter des données de test à votre environnement](~/concepts/build-and-test/test-data.md)

