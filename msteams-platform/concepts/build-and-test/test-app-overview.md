---
title: Vue d’ensemble de Tester votre application
description: Décrit le processus de test et de débogage de votre application personnalisée Teams dans Microsoft 365
ms.topic: how-to
ms.localizationpriority: high
keywords: Configurer le client Microsoft 365 Teams qui charge l’application de test
ms.openlocfilehash: 98c00ece54e1654570556bac122e6760b283b73f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111527"
---
# <a name="test-your-app"></a>Tester votre application

Après avoir intégré votre application à Microsoft Teams, vous devez tester votre application avant de la publier. L’objectif final est d'obtenir un maximum d'utilisateurs pour votre application. Veillez donc à tester l'application sur plusieurs appareils que les utilisateurs pourraient utiliser. Pour tester votre application :

* Préparer votre client Microsoft 365.
* Choisissez un espace de travail pour tester et déboguer votre application.
* Ajoutez des données de test à votre client Microsoft 365.

## <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Avant de commencer à tester votre application, préparez votre client de test Microsoft 365 et activez l’application Teams personnalisée pour vous permettre de charger votre application. Vous devez vous inscrire au programme de développement Microsoft 365 et gérer les paramètres Teams de votre organisation. Configurez votre abonnement développeur et configurez-le via [préparer votre client Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

## <a name="test-and-debug"></a>Test et débogage

Pour tester et déboguer votre application, vous devez créer au moins un espace de travail. Vous pouvez sélectionner une configuration de test, telle qu’un hôte local ou un hôte cloud pour tester et déboguer l’application. Des conseils pour déboguer votre application Teams sont fournis pour charger et exécuter votre expérience d’application. Pour plus d’informations, consultez [choisir une configuration et exécuter votre application Microsoft Teams](~/concepts/build-and-test/debug.md).

Testez votre bot en local. Pour plus d’informations, consultez [déboguer votre bot localement avec un IDE](~/bots/how-to/debug/locally-with-an-ide.md). Vous pouvez également déboguer votre bot avec un [intergiciel d’inspection](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) et des [outils adaptatifs](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).

Pour afficher les journaux de la console, afficher ou modifier des requêtes html, css et réseau pendant l’exécution, ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif pour accéder à DevTools. Pour plus d’informations, consultez [Accéder aux onglets DevTools pour Teams](~/tabs/how-to/developer-tools.md).

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Ajouter des données de test à votre client Microsoft 365

Ajoutez les données de test à un client de test Microsoft 365. Pour plus d’informations, consultez [ajouter des données de test à votre client de test Office 365](~/concepts/build-and-test/test-data.md) et remplissez toutes les conditions préalables avant de commencer à charger vos données de test.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Préparer votre client Microsoft Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="see-also"></a>Voir aussi

* [Déboguer votre onglet](~/tabs/how-to/developer-tools.md)
* [Déboguer vos bots](~/bots/how-to/debug/locally-with-an-ide.md)
* [Tester les autorisations RSC](~/graph-api/rsc/test-resource-specific-consent.md)
