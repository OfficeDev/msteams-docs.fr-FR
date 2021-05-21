---
title: Tester la vue d’ensemble de votre application
description: Décrit le processus de test de votre application Teams personnalisée dans Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurer Microsoft 365 client Teams l’application de test
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565185"
---
# <a name="test-your-app"></a>Tester votre application

Après avoir intégré votre application à Microsoft Teams, vous devez la tester avant de la publier. L’objectif ultime est d’obtenir autant d’utilisateurs pour votre application, par conséquent, veillez à tester l’application sur plusieurs appareils que les utilisateurs peuvent utiliser. Pour tester votre application :

* Préparez votre Microsoft 365 client.
* Choisissez un espace de travail pour tester et déboguer votre application.
* Ajoutez des données de test à Microsoft 365 client.

## <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Avant de commencer à tester votre application, préparez votre client de test Microsoft 365 et activez l’Teams personnalisée vous permettant de télécharger votre application. Vous devez vous inscrire au programme Microsoft 365 développeur et gérer les paramètres Teams de votre organisation. Configurez votre abonnement développeur et configurez-le par le biais de [la préparation Microsoft 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="test-and-debug"></a>Test et débogage

Pour tester et déboguer votre application, vous devez créer au moins un espace de travail. Vous pouvez sélectionner une configuration de test, par exemple un hôte local ou un hôte basé sur le cloud pour tester et déboguer l’application. Des conseils pour déboguer votre Teams application sont fournis pour charger et exécuter votre expérience d’application. Pour plus d’informations, [voir choisir une application de Microsoft Teams.](~/concepts/build-and-test/debug.md)

Testez votre bot localement. Pour plus d’informations, voir [déboguer votre bot localement avec un IDE.](~/bots/how-to/debug/locally-with-an-ide.md) Vous pouvez également déboguer votre bot avec des logiciels [intermédiaires d’inspection](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) et des [outils adaptatifs.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true) 

Pour afficher les journaux de la console, afficher ou modifier des requêtes html, css et réseau pendant l’runtime, ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif pour accéder aux DevTools. Pour plus d’informations, [voir Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md). 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Ajouter des données de test à votre client Microsoft 365 client

Ajoutez les données de test Microsoft 365 client test. Pour plus d’informations, voir ajouter des données de test à [votre client de test Office 365](~/concepts/build-and-test/test-data.md)et remplir toutes les conditions préalables avant de commencer à télécharger vos données de test.

## <a name="see-also"></a>Voir aussi

- [Déboguer votre onglet](~/tabs/how-to/developer-tools.md)
 
- [Déboguer vos bots](~/bots/how-to/debug/locally-with-an-ide.md)

- [Tester les autorisations RSC](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Préparer votre client Microsoft Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
