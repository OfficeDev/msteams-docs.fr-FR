---
title: Tester la vue d'ensemble de votre application
description: Décrit le processus de test de votre application personnalisée Teams dans Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurer microsoft 365 client Teams téléchargeant l'application de test
ms.openlocfilehash: d95d65961b060ff1938d51c0f3fafc2b1e56fa7e
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058606"
---
# <a name="test-your-app"></a>Tester votre application

Après avoir intégré votre application à Microsoft Teams, vous devez la tester avant de la publier. L'objectif ultime est d'obtenir autant d'utilisateurs pour votre application, par conséquent, veillez à tester l'application sur plusieurs appareils que les utilisateurs peuvent utiliser. Pour tester votre application :

* Préparer votre client Microsoft Office 365
* Choisir un espace de travail pour tester et déboguer votre application
* Ajouter des données de test à votre client Microsoft 365

## <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Avant de commencer à tester votre application, préparez votre client de test Microsoft 365 et activez l'application Teams personnalisée pour charger votre application. Vous devez vous inscrire au programme pour les développeurs Microsoft 365 et gérer les paramètres Teams de votre organisation. Configurez votre abonnement développeur et configurez-le par le biais de la préparation de [votre client Microsoft 365.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="test-and-debug"></a>Test et débogage

Pour tester et déboguer votre application, vous devez créer au moins un espace de travail. Vous pouvez sélectionner une configuration de test, par exemple un hôte local ou un hôte basé sur le cloud pour tester et déboguer l'application. Des conseils pour déboguer votre application Teams sont fournis pour charger et exécuter votre expérience d'application. Pour plus d'informations, [voir choisir une application de mise en place et d'exécuter votre application Microsoft Teams.](~/concepts/build-and-test/debug.md)

Testez votre bot localement. Pour plus d'informations, voir [déboguer votre bot localement avec un IDE.](~/bots/how-to/debug/locally-with-an-ide.md) Vous pouvez également déboguer votre bot avec des logiciels [intermédiaires d'inspection](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) et des [outils adaptatifs.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true) 

Pour afficher les journaux de la console, afficher ou modifier des requêtes html, css et réseau pendant l'runtime, ajoutez des points d'arrêt à votre code JavaScript et effectuez un débogage interactif pour accéder aux DevTools. Pour plus d'informations, [voir Accéder aux onglets DevTools pour Teams.](~/tabs/how-to/developer-tools.md) 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Ajouter des données de test à votre client Microsoft 365

Ajoutez les données de test au client de test Microsoft 365. Pour plus d'informations, voir ajouter des données de test à votre client [test Office 365](~/concepts/build-and-test/test-data.md)et remplir toutes les conditions préalables avant de commencer à télécharger vos données de test.

## <a name="see-also"></a>Voir aussi

- [Déboguer votre onglet](~/tabs/how-to/developer-tools.md)
 
- [Déboguer vos bots](~/bots/how-to/debug/locally-with-an-ide.md)

- [Tester les autorisations RSC](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Préparer votre client Microsoft Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
