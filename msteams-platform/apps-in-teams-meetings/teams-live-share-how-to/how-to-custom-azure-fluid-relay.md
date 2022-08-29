---
title: Comment utiliser le service Relais Azure Fluid personnalisé
author: surbhigupta
description: Dans ce module, découvrez comment utiliser un service Azure Fluid Relay personnalisé avec Live Share.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 07/21/2022
ms.openlocfilehash: baa192bf82e059b1cfe7a9fc8979874710f266b1
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425631"
---
---

# <a name="custom-azure-fluid-relay-service"></a>Service Relais Azure Fluid personnalisé

Bien que vous préfériez probablement utiliser notre service hébergé gratuit, il est utile d’utiliser votre propre service Azure Fluid Relay pour votre application Live Share.

## <a name="pre-requisites"></a>Conditions préalables

1. Créez un panneau côté réunion et une extension de réunion d’application de phase, comme illustré dans le [didacticiel](../teams-live-share-tutorial.md) sur le rouleau de dés.
2. Mettez à jour le manifeste de votre application pour inclure toutes les [autorisations nécessaires](../teams-live-share-capabilities.md#register-rsc-permissions).
3. Provisionnez un service Azure Fluid Relay comme indiqué dans ce [didacticiel](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

## <a name="connect-to-azure-fluid-relay-service"></a>Se connecter au service Azure Fluid Relay

Lors de la construction de la classe `TeamsFluidClient`, vous pouvez définir votre propre `AzureConnectionConfig`. Live Share associe des conteneurs que vous créez à des réunions, mais vous devez implémenter l’interface `ITokenProvider` pour signer des jetons pour vos conteneurs. Cet exemple explique Azure, `AzureFunctionTokenProvider`qui utilise une fonction cloud Azure pour demander un jeton d’accès à un serveur.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const clientProps = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_SERVICE_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const client = new TeamsFluidClient(clientProps);
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence, ITeamsFluidClientOptions } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const clientProps: ITeamsFluidClientOptions = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_FUNCTION_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const client = new TeamsFluidClient(clientProps);
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

---

## <a name="why-use-a-custom-azure-fluid-relay-service"></a>Pourquoi utiliser un service Azure Fluid Relay personnalisé ?

Envisagez d’utiliser une connexion de service AFR personnalisée si vous :

* Exiger le stockage des données dans des conteneurs Fluid au-delà de la durée de vie d’une réunion.
* Transmettez des données sensibles via le service qui nécessite une stratégie de sécurité personnalisée.
* Développez des fonctionnalités via Fluid Framework pour votre application en dehors de Teams.

## <a name="why-use-live-share-with-your-custom-service"></a>Pourquoi utiliser Live Share avec votre service personnalisé ?

Azure Fluid Relay est conçu pour fonctionner avec n’importe quelle application web, ce qui signifie qu’il fonctionne avec ou sans Microsoft Teams. Cela soulève une question importante : si je crée mon propre service Azure Fluid Relay, ai-je toujours besoin de Live Share ?

Live Share comporte des fonctionnalités qui sont bénéfiques pour les scénarios de réunion courants qui augmentent d’autres fonctionnalités de votre application, notamment :

* [Mappage de conteneurs](#container-mapping)
* [Objets éphémères et vérification de rôle](#ephemeral-objects-and-role-verification)
* [Synchronisation de média](#media-synchronization)

### <a name="container-mapping"></a>Mappage de conteneurs

La classe Live Share est responsable du `TeamsFluidClient` mappage d’un identificateur de réunion unique à vos conteneurs Fluid, ce qui garantit que tous les participants à la réunion rejoignent le même conteneur. Dans le cadre de ce processus, le client tente de se connecter à une `containerId` réunion mappée qui existe déjà. S’il n’en existe pas, il `AzureClient` est utilisé pour créer un conteneur à l’aide de votre `AzureConnectionConfig` conteneur, puis le relayer à d’autres participants à la `containerId` réunion.

Si votre application dispose déjà d’un mécanisme pour créer des conteneurs Fluid et les partager avec d’autres membres, par exemple en insérant l’URL `containerId` partagée à la phase de réunion, cela peut ne pas être nécessaire pour votre application.

### <a name="ephemeral-objects-and-role-verification"></a>Objets éphémères et vérification de rôle

Les structures de données éphémères de Live Share, telles que `EphemeralPresence`, `EphemeralState`sont `EphemeralEvent` adaptées à la collaboration dans les réunions et ne sont donc pas prises en charge dans les conteneurs Fluid utilisés en dehors de Microsoft Teams. Des fonctionnalités telles que la vérification de rôle aident votre application à s’aligner sur les attentes de nos utilisateurs.

> [!NOTE]
> En outre, les objets éphémères offrent des latences de messages plus rapides que les structures de données Fluid traditionnelles.

Pour plus d’informations, consultez la page [fonctionnalités de base](../teams-live-share-capabilities.md) .

### <a name="media-synchronization"></a>Synchronisation de média

Les packages à partir de `@microsoft/live-share-media` ne sont pas pris en charge dans les conteneurs Fluid utilisés en dehors de Microsoft Teams.

Pour plus d’informations, consultez la page [des fonctionnalités multimédias](../teams-live-share-media-capabilities.md) .

## <a name="see-also"></a>Voir aussi

* [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
* [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
* [Fonctionnalités de Live Share](../teams-live-share-capabilities.md)
* [Fonctionnalités média de Live Share](../teams-live-share-media-capabilities.md)
* [FAQ sur Live Share](../teams-live-share-faq.md)
* [Applications Teams dans les réunions](../teams-apps-in-meetings.md)
