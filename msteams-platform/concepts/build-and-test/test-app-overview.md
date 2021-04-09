---
title: Tester la vue d’ensemble de votre application
description: Décrit le processus de test de votre application personnalisée Teams dans Microsoft 365
ms.topic: how-to
keywords: Configurer microsoft 365 client Teams téléchargeant l’application de test
ms.openlocfilehash: b199ca4be31b546364091b754cdb890c8c0dd7d0
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634776"
---
# <a name="test-your-app"></a>Tester votre application

Après avoir intégré votre application à Microsoft Teams, vous devez la tester avant de la publier. L’objectif ultime est d’obtenir autant d’utilisateurs pour votre application, par conséquent, veillez à tester l’application sur plusieurs appareils que les utilisateurs peuvent utiliser. Pour tester votre application :

* Préparer votre client Microsoft Office 365
* Choisir un espace de travail pour tester et déboguer votre application
* Ajouter des données de test à votre client Microsoft 365

## <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Avant de commencer à tester votre application, préparez votre client de test Microsoft 365 et activez l’application Teams personnalisée pour charger votre application. Vous devez vous inscrire au programme pour les développeurs Microsoft 365 et gérer les paramètres Teams de votre organisation. Configurez votre abonnement développeur et configurez-le par le biais de la préparation de [votre client Microsoft 365.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="test-and-debug"></a>Test et débogage

Pour tester et déboguer votre application, vous devez créer au moins un espace de travail. Vous pouvez sélectionner une configuration de test, par exemple un hôte local ou un hôte basé sur le cloud pour tester et déboguer l’application. Des conseils pour déboguer votre application Teams sont fournis pour charger et exécuter votre expérience d’application. Pour plus d’informations, [voir choisir une mise en place et exécuter votre application Microsoft Teams.](~/concepts/build-and-test/debug.md)

Testez votre bot localement. Pour plus d’informations, voir [déboguer votre bot localement avec un IDE.](~/bots/how-to/debug/locally-with-an-ide.md) Vous pouvez également déboguer votre bot avec des logiciels [intermédiaires d’inspection](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) et des [outils adaptatifs.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true) 

Pour afficher les journaux de la console, afficher ou modifier des requêtes html, css et réseau pendant l’utilisation, ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif pour accéder aux DevTools. Pour plus d’informations, [voir Accéder aux onglets DevTools pour Teams.](~/tabs/how-to/developer-tools.md) 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Ajouter des données de test à votre client Microsoft 365

Ajoutez les données de test au client de test Microsoft 365. Pour plus d’informations, voir ajouter des données de test à votre client [test Office 365](~/concepts/build-and-test/test-data.md)et remplir toutes les conditions préalables avant de commencer à télécharger vos données de test.

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Déboguer votre onglet](~/tabs/how-to/developer-tools.md)
 
> [!div class="nextstepaction"]
> [Déboguer vos bots](~/bots/how-to/debug/locally-with-an-ide.md)

> [!div class="nextstepaction"]
> [Tester les autorisations RSC](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Préparer votre client Microsoft Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
