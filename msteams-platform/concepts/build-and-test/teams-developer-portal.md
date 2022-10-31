---
title: Documentation pour les développeurs
description: Dans cet article, apprenez-en davantage sur le portail des développeurs et sur la création d’une nouvelle application et l’importation d’une application existante dans le portail des développeurs Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 3c6444f041a996b908e2c6444fecf7e3dc68ee40
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791803"
---
# <a name="developer-portal-for-teams"></a>Documentation pour les développeurs

<a href="https://dev.teams.microsoft.com" target="_blank">Portail des développeurs pour Teams</a> est l’outil principal pour configurer, distribuer et gérer vos applications Microsoft Teams. Avec le Developer Portal, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’exécution et bien plus encore.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="La capture d’écran est un exemple montrant la page d’accueil du portail des développeurs pour Teams.":::

> [!NOTE]
>
> * Actuellement, le portail des développeurs n’est pas disponible pour les locataires Government Community Cloud (GCC)-High ou Department of Defense (DOD).
> * Toutefois, vous pouvez utiliser un locataire standard pour créer une application dans le Developer Portal, télécharger l’application et charger l’application à l’aide de [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) dans un cloud national. Pour plus d’informations, consultez [Déploiements cloud nationaux](/graph/deployments).

## <a name="register-an-app"></a>Inscrire une application

Le portail des développeurs propose les méthodes suivantes pour inscrire une application Teams :

* [Créez et inscrivez une toute nouvelle application](#create-and-register-a-brand-new-app).
* [Importer un package d’application existant](#import-an-existing-app).

### <a name="create-and-register-a-brand-new-app"></a>Créer et inscrire une nouvelle application

Le portail des développeurs vous permet de créer une nouvelle application :

1. Connectez-vous [au Portail des développeurs](https://dev.teams.microsoft.com), sélectionnez **Applications** dans le volet gauche.

   :::image type="content" source="../../assets/images/tdp/home-page.png" alt-text="La capture d’écran est un exemple montrant la page d’accueil du portail des développeurs pour Teams.":::

1. Sélectionnez **Nouvelle application** et entrez le nom de l’application.

   :::image type="content" source="../../assets/images/tdp/enter-app-name-tdp.png" alt-text="La capture d’écran montre comment créer une application dans le Portail des développeurs pour Teams." lightbox="../../assets/images/tdp/create-new-app-in-tdp.png":::

1. Sélectionnez **Ajouter**.

Vous avez maintenant créé une nouvelle application et vous pouvez voir toutes les informations de base de la nouvelle application.

:::image type="content" source="../../assets/images/tdp/basic-information-app-tdp.png" alt-text="La capture d’écran est un exemple qui montre les informations de base de l’application que vous avez créée dans le portail des développeurs pour Teams.":::

### <a name="import-an-existing-app"></a>Importer une application existante

Suivez les étapes pour importer et gérer votre application existante dans le portail des développeurs.

1. Dans le portail des développeurs, sélectionnez **Applications** dans le volet gauche.
1. Sélectionnez **Importer une application**.

   :::image type="content" source="../../assets/images/tdp/import-app.png" alt-text="La capture d’écran montre comment importer votre application existante dans le Portail des développeurs pour que Teams gère vos applications.":::

1. Sélectionnez le fichier manifeste de l’application, puis sélectionnez **Ouvrir**.
1. Sélectionnez **Importer**.

> [!NOTE]
>
> * Le portail des développeurs crée un ID d’application unique et verrouille l’ID de votre application Teams inscrite. Vous ne pouvez pas modifier ou fournir un ID de votre choix, ce qui empêche d’avoir des ID d’application en double pour plusieurs applications.
> * Si vous créez une application à l’aide du Kit de ressources Microsoft Teams pour Visual Studio Code, vous pouvez gérer votre application dans le portail des développeurs. Pour plus d’informations, consultez [Créer des applications avec teams toolkit et Visual Studio Code](~/toolkit/visual-studio-code-overview.md).
> * Vous pouvez importer une application existante que vous avez créée sur App Studio dans le portail des développeurs.

## <a name="see-also"></a>Voir aussi

[Inclure une offre SaaS avec votre application Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
