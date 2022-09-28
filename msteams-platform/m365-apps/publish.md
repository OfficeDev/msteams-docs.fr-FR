---
title: Publier des applications Teams pour Microsoft 365
description: Découvrez comment rendre vos applications Teams compatibles Avec Microsoft 365 détectables pour les utilisateurs dans Teams, Outlook et Office. En savoir plus sur la distribution multilocataire et monolocataire.
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 01806f5aa7e3a5b0cb79cb6a2562cbf104f031bb
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100937"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Publier des applications Teams pour Microsoft 365

Microsoft Teams prend en charge les applications Teams compatibles avec Microsoft 365 pour la production. Vous pouvez distribuer ces applications à l’audience qui utilise les versions *targeted Release*  (dev preview) de Outlook.com et Office.com, la build *de canal* bêta d’Outlook pour Windows Desktop et la build Office Current Channel (préversion) de l’application Office pour Android. Les options de distribution et les processus pour les applications Teams compatibles avec Microsoft 365 sont les mêmes que pour les applications Teams traditionnelles.

Une fois qu’elle est publiée, votre application est détectable en tant qu’application installable à partir des magasins d’applications Outlook et Office, en plus du Magasin Teams. Votre application utilise les autorisations définies dans Teams dans Outlook et Office. Les administrateurs Teams peuvent [gérer l’accès aux applications Teams dans Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) pour les utilisateurs de leur organisation.

:::image type="content" source="images/outlook-office-app-store.png" alt-text="La capture d’écran est un exemple montrant Outlook et Office.com installer des écrans pour les applications SurveyMonkey et MURAL Teams.":::

## <a name="single-tenant-distribution"></a>Distribution à locataire unique

Les extensions de message prenant en charge Outlook peuvent être distribuées aux locataires de test et de production de plusieurs façons :

### <a name="teams-client"></a>Client Teams

Dans le menu **Applications** , sélectionnez **Gérer vos applications** > **Publier une application** > **Envoyer une application à votre organisation**. Cela nécessite l’approbation de votre administrateur informatique.

### <a name="teams-developer-portal"></a>Portail des développeurs Teams

Utilisez le [portail des développeurs Teams](https://dev.teams.microsoft.com/) pour charger et publier une application dans votre organisation. Cela nécessite l’approbation de votre administrateur informatique. Pour plus d’informations, consultez [Gérer vos applications avec le portail des développeurs pour Microsoft Teams](../concepts/build-and-test/teams-developer-portal.md).

### <a name="microsoft-teams-admin-center"></a>Centre d’administration Microsoft Teams

En tant qu’administrateur Teams, vous pouvez charger et préinstaller le package d’application pour le locataire de votre organisation à partir du [Centre d’administration Teams](https://admin.teams.microsoft.com/). Pour plus d’informations, consultez [Charger vos applications personnalisées dans le Centre d’administration Microsoft Teams](/MicrosoftTeams/upload-custom-apps).

### <a name="microsoft-admin-center"></a>Centre d’administration Microsoft Corporation

En tant qu’administrateur général, vous pouvez charger et préinstaller le package d’application à partir de [l’administrateur Microsoft](https://admin.microsoft.com/). Pour plus d’informations, consultez [Tester et déployer Microsoft 365 Apps par des partenaires dans le portail des applications intégrées](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

## <a name="multitenant-distribution"></a>Distribution multilocataires

Le processus de soumission [de Microsoft AppSource](https://appsource.microsoft.com/) (Place de marché commerciale Microsoft) pour les applications Teams activées pour Outlook et Office est identique à celui des applications Teams traditionnelles. La seule différence est que vous devez utiliser le manifeste d’application Teams [version 1.13](../tabs/how-to/using-teams-client-sdk.md) dans votre package d’application, ce qui introduit la prise en charge des applications Teams qui s’exécutent sur Microsoft 365.

> [!TIP]
> Utilisez le portail des développeurs Teams pour [valider votre package d’application](https://dev.teams.microsoft.com/validation) afin de résoudre les erreurs ou les avertissements avant de les envoyer au magasin Teams (via [Microsoft Partner Network](https://partner.microsoft.com/)).

Pour commencer, consultez [Distribuer votre application Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md).