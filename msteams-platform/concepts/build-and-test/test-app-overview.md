---
title: Testez la vue d’ensemble de votre application
description: Décrit le processus de test de votre application Teams personnalisée dans Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurer Microsoft 365 locataire Teams application de test de téléchargement
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565185"
---
# <a name="test-your-app"></a>Tester votre application

Après avoir intégré votre application à Microsoft Teams, vous devez tester votre application avant de la publier. Le but ultime est d’obtenir autant d’utilisateurs pour votre application, par conséquent, assurez-vous de tester l’application sur plusieurs appareils que les utilisateurs pourraient utiliser. Pour tester votre application :

* Préparez votre Microsoft 365 locataire.
* Choisissez un espace de travail pour tester et déboger votre application.
* Ajoutez des données de test à votre Microsoft 365 locataire.

## <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Avant de commencer à tester votre application, préparez votre Microsoft 365 de test et activez l’application Teams personnalisée vous permettent de télécharger votre application. Vous devez vous inscrire à un Microsoft 365 développeur et gérer les paramètres Teams de votre organisation. Configurez votre abonnement développeur et configurez-le [en préparant votre Microsoft 365 locataire](~/concepts/build-and-test/prepare-your-o365-tenant.md).

## <a name="test-and-debug"></a>Test et débogage

Pour tester et débobug votre application, vous devez créer au moins un espace de travail. Vous pouvez sélectionner une configuration de test, telle qu’un hôte local ou un hôte basé sur le cloud pour tester et débogiller l’application. Des conseils pour débobuger votre Teams est fourni pour charger et exécuter votre expérience d’application. Pour plus d’informations, [consultez le choix d’une mise en place et exécutez Microsoft Teams application](~/concepts/build-and-test/debug.md).

Testez votre bot localement. Pour plus d’informations, [voir débog votre bot localement avec un IDE](~/bots/how-to/debug/locally-with-an-ide.md). Vous pouvez également débogdier votre bot avec [middleware inspection et des](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) outils [adaptatifs](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true). 

Pour afficher les journaux de console, afficher ou modifier les requêtes html, css et réseau pendant l’exécution, ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif accéder aux DevTools. Pour plus d’informations, [consultez Access the DevTools pour Teams onglets](~/tabs/how-to/developer-tools.md). 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Ajoutez des données de test à votre Microsoft 365 locataire

Ajoutez les données de test à Microsoft 365 de test. Pour plus d’informations, [consultez ajouter des données de test à votre Office 365 de test](~/concepts/build-and-test/test-data.md)et remplir toutes les conditions préalables avant de commencer à télécharger vos données de test.

## <a name="see-also"></a>Voir aussi

- [Débogez votre onglet](~/tabs/how-to/developer-tools.md)
 
- [Débogez vos bots](~/bots/how-to/debug/locally-with-an-ide.md)

- [Testez les autorisations RSC](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Préparer votre client Microsoft Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
