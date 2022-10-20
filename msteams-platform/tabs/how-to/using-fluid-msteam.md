---
title: Utiliser Fluid avec Teams
author: timtwang
ms.author: mobajemu
description: Didacticiel sur l’intégration des fonctionnalités de collaboration en temps réel avec Fluid dans une application onglet Microsoft Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 620e2150ca6300fb8d37bc7c68b965aacb19700b
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615398"
---
# <a name="use-fluid-with-teams"></a>Utiliser Fluid avec Teams

À la fin de ce didacticiel, vous pouvez intégrer n’importe quelle application Fluid dans Teams et collaborer avec d’autres utilisateurs en temps réel.

Dans cette section, vous pouvez découvrir les concepts suivants :

1. Intégrez un client Fluid à l’application onglet Teams.
1. Exécutez et connectez votre application Teams à un service Fluid (Azure Fluid Relay).
1. Créez et obtenez des conteneurs Fluid, puis passez-les à un composant React.

Pour plus d’informations sur la création d’une application complexe, consultez [Teams Fluid Hello World](https://github.com/microsoft/FluidExamples/tree/main/teams-fluid-hello-world) exemple dans notre référentiel FluidExamples.

## <a name="prerequisites"></a>Configuration requise

Ce didacticiel nécessite une connaissance des concepts et des ressources suivants :

- [Vue d’ensemble de Fluid Framework](https://fluidframework.com/docs/)
- [Démarrage rapide de Fluid Framework](https://fluidframework.com/docs/start/quick-start/)
- Notions de base des [hooks React](https://reactjs.org/) et [React](https://reactjs.org/docs/hooks-intro.html)
- Comment créer un [onglet Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs)

> [!div class="nextstepaction"]
> [Installer les composants prérequis](tab-requirements.md)

## <a name="create-the-project"></a>Créez le projet

1. Ouvrez une invite de commandes et accédez au dossier parent dans lequel vous souhaitez créer le projet, par exemple. `/My Microsoft Teams Projects`
1. Créez une application d’onglet Teams en exécutant la commande suivante et [en créant un onglet de canal](create-channel-group-tab.md#create-a-custom-channel-or-group-tab-with-nodejs) :

    ```cmd
    yo teams
    ```

1. Après la création, accédez au projet, avec la commande `cd <your project name>`suivante .
1. Le projet utilise les bibliothèques suivantes :

    |Bibliothèque |Description |
    |---|---|
    | `fluid-framework`    |Contient le IFluidContainer et d’autres [structures de données distribuées](https://fluidframework.com/docs/build/dds/) qui synchronisent les données entre les clients.|
    | `@fluidframework/azure-client`   |Définit le schéma de départ du [conteneur Fluid](https://fluidframework.com/docs/build/containers/).|
    | `@fluidframework/test-client-utils` |Définit le `InsecureTokenProvider` nécessaire pour créer la connexion à un service Fluid.|

    Exécutez la commande suivante pour installer les bibliothèques :

    ```cmd
    npm install @fluidframework/azure-client fluid-framework @fluidframework/test-client-utils
    ```

## <a name="code-the-project"></a>Coder le projet

1. Ouvrez le fichier `/src/client/<your tab name>` dans votre éditeur de code.
1. Créez un fichier `Util.ts` et ajoutez les instructions d’importation suivantes :

    ```ts
    //`Util.ts

    import { IFluidContainer } from "fluid-framework";
    import { AzureClient, AzureClientProps } from "@fluidframework/azure-client";
    import { InsecureTokenProvider } from "@fluidframework/test-client-utils";
    ```

### <a name="defining-fluid-functions-and-parameters"></a>Définition de fonctions et de paramètres Fluid

Cette application est destinée à être utilisée dans le contexte de Microsoft Teams, avec toutes les importations, l’initialisation et les fonctions liées à Fluid ensemble. Cela offre une expérience améliorée et facilite son utilisation à l’avenir. Vous pouvez ajouter le code suivant aux instructions d’importation :

```ts
// TODO 1: Define the parameter key(s).
// TODO 2: Define container schema.
// TODO 3: Define connectionConfig (AzureClientProps).
// TODO 4: Create Azure client.
// TODO 5: Define create container function.
// TODO 6: Define get container function.
```

> [!NOTE]
> Les commentaires définissent toutes les fonctions et constantes nécessaires pour interagir avec le service et le conteneur Fluid.

1. Remplacez `TODO 1:` par le code suivant :

    ```ts
    export const containerIdQueryParamKey = "containerId";
    ```

    La constante est exportée à mesure qu’elle s’ajoute aux `contentUrl` paramètres de Microsoft Teams, et plus tard pour analyser l’ID de conteneur dans la page de contenu. Il est courant de stocker des clés de paramètre de requête importantes en tant que constantes, plutôt que de taper la chaîne brute à chaque fois.

    Pour que le client puisse créer des conteneurs, il a besoin d’un `containerSchema` objet qui définit les objets partagés utilisés dans cette application. Cet exemple utilise un SharedMap comme objet `initialObjects`partagé, mais n’importe quel objet partagé peut être utilisé.

    > [!NOTE]
    > Il `map` s’agit de l’ID de l’objet `SharedMap` et il doit être unique dans le conteneur comme tout autre DDSe.

1. Remplacez `TODO: 2` par le code suivant :

    ```ts
    const containerSchema = {
        initialObjects: { map: SharedMap }
    };
    ```

1. Remplacez `TODO: 3` par le code suivant :

    ```ts
    const connectionConfig : AzureClientProps =
    {
        connection: {
            type: "local",
            tokenProvider: new InsecureTokenProvider("foobar", { id: "user" }),
            endpoint: "http://localhost:7070"
        }
    };
    ```

    Avant que le client puisse être utilisé, il a besoin d’un `AzureClientProps` élément qui définit le type de connexion utilisé par le client. La `connectionConfig` propriété est nécessaire pour se connecter au service. Le mode local du client Azure est utilisé. Pour activer la collaboration entre tous les clients, remplacez-la par les informations d’identification du service Fluid Relay. Pour plus d’informations, voir comment [configurer le service Azure Fluid Relay](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

1. Remplacez `TODO: 4` par le code suivant :

    ```ts
    const client = new AzureClient(connectionConfig);
    ```

1. Remplacez `TODO: 5` par le code suivant :

    ```ts
    export async function createContainer() : Promise<string> {
        const { container } = await client.createContainer(containerSchema);
        const containerId = await container.attach();
        return containerId;
    };
    ```

    Lorsque vous créez le conteneur dans la page de configuration et l’ajoutez au `contentUrl` paramètre Teams, vous devez retourner l’ID de conteneur après avoir attaché le conteneur.

1. Remplacez `TODO: 6` par le code suivant :

    ```ts
    export async function getContainer(id : string) : Promise<IFluidContainer> {
        const { container } = await client.getContainer(id, containerSchema);
        return container;
    };
    ```

    Lorsque vous récupérez le conteneur Fluid, vous devez retourner le conteneur, car votre application doit interagir avec le conteneur et les DDSes qu’il contient, dans la page de contenu.

### <a name="create-fluid-container-in-the-configuration-page"></a>Créer un conteneur Fluid dans la page de configuration

1. Ouvrez le fichier `src/client/<your tab name>/<your tab name>Config.tsx` dans votre éditeur de code.

    Le flux d’application de l’onglet Teams standard passe de la configuration à la page de contenu. Pour activer la collaboration, il est essentiel de conserver le conteneur lors du chargement dans la page de contenu. La meilleure solution pour conserver le conteneur consiste à ajouter l’ID de conteneur sur les `contentUrl` URL de la page de contenu et `websiteUrl`, en tant que paramètre de requête. Le bouton Enregistrer dans la page de configuration Teams est la passerelle entre la page de configuration et la page de contenu. Il s’agit d’un emplacement où créer le conteneur et ajouter l’ID de conteneur dans les paramètres.

1. Ajoutez les instructions d’importation suivantes:

    ```ts
    import { createContainer, containerIdQueryParamKey } from "./Util";
    ```

1. Remplacez la méthode `onSaveHandler` par le code ci-dessous. Les seules lignes ajoutées ici appellent la méthode de création de conteneur définie précédemment, `Utils.ts` puis ajoutent l’ID de conteneur retourné au `contentUrl` paramètre et `websiteUrl` en tant que paramètre de requête.

    ```ts {linenos=inline,hl_lines=[134,136,137]}
    const onSaveHandler = async (saveEvent: microsoftTeams.settings.SaveEvent) => {
        const host = "https://" + window.location.host;
        const containerId = await createContainer();
        microsoftTeams.settings.setSettings({
            contentUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            websiteUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            suggestedDisplayName: "<your tab name>",
            removeUrl: host + "/<your tab name>/remove.html?theme={theme}",
            entityId: entityId.current
        });
        saveEvent.notifySuccess();
    };
    ```

    Veillez à le remplacer `<your tab name>` par le nom de l’onglet de votre projet.

    > [!WARNING]
    > Comme l’URL de la page de contenu est utilisée pour stocker l’ID de conteneur, cet enregistrement est supprimé si l’onglet Teams est supprimé.
    > En outre, chaque page de contenu ne peut prise en charge qu’un seul ID de conteneur.

### <a name="refactor-content-page-to-reflect-fluid-application"></a>Refactoriser la page de contenu pour refléter l’application Fluid

1. Ouvrez le fichier `src/client/<your tab name>/<your tab name>.tsx` dans votre éditeur de code. Une application fluid classique se compose d’une vue et d’une structure de données Fluid. Concentrez-vous sur l’obtention/chargement du conteneur Fluid et laissez toutes les interactions liées à Fluid dans un composant React.

1. Ajoutez les instructions d’importation suivantes dans la page de contenu :

    ```ts
    import { IFluidContainer } from "fluid-framework";
    import { getContainer, containerIdQueryParamKey } from "./Util";
    ```

1. Supprimez tout le code sous les instructions d’importation dans la page de contenu et remplacez-le par ce qui suit :

    ```ts
    export const <your tab name> = () => {
      // TODO 1: Initialize Microsoft Teams.
      // TODO 2: Initialize inTeams boolean.
      // TODO 3: Define container as a React state.
      // TODO 4: Define a method that gets the Fluid container
      // TODO 5: Get Fluid container on content page startup.
      // TODO 6: Pass the container to the React component as argument.
    }
    ```

    Veillez à remplacer `<your tab name>` par le nom de l’onglet que vous définissez pour votre projet.

1. Remplacez `TODO 1` par le code suivant :

    ```ts
    microsoftTeams.initialize();
    ```

    Pour afficher la page de contenu dans Teams, vous devez inclure le Kit de développement logiciel ( [SDK) client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) et inclure un appel pour l’initialiser après le chargement de votre page.

1. Remplacez `TODO 2` par le code suivant :

    ```ts
    const [{ inTeams }] = useTeams();
    ```

    Comme l’application Teams n’est qu’une injection IFrame d’une page web, vous devez initialiser la `inTeams` constante booléenne pour savoir si l’application se trouve dans Teams ou non, et si les ressources Teams, telles que la `contentUrl`, sont disponibles.

1. Remplacez `TODO 3` par le code suivant :

    ```ts
    const [fluidContainer, setFluidContainer] = useState<IFluidContainer | undefined>(undefined);
    ```

    Utilisez un état React pour le conteneur, car il permet de mettre à jour dynamiquement le conteneur et les objets de données qu’il contient.

1. Remplacez `TODO 4` par le code suivant :

    ```ts
    const getFluidContainer = async (url : URLSearchParams) => {
        const containerId = url.get(containerIdQueryParamKey);
        if (!containerId) {
            throw Error("containerId not found in the URL");
        }
        const container = await getContainer(containerId);
        setFluidContainer(container);
    };
    ```

    Analysez l’URL pour obtenir la chaîne de paramètre de requête, définie par `containerIdQueryParamKey`, et récupérer l’ID de conteneur. Avec l’ID de conteneur, vous pouvez charger le conteneur. Une fois que vous avez le conteneur, définissez l’état `fluidContainer` React, consultez l’étape précédente.

1. Remplacez `TODO 5` par le code suivant :

    ```ts
    useEffect(() => {
        if (inTeams === true) {
            microsoftTeams.settings.getSettings(async (instanceSettings) => {
                const url = new URL(instanceSettings.contentUrl);
                getFluidContainer(url.searchParams);
            });
            microsoftTeams.appInitialization.notifySuccess();
        }
    }, [inTeams]);
    ```

    Une fois que vous avez défini comment obtenir le conteneur Fluid, vous devez indiquer à React d’appeler `getFluidContainer` lors de la charge, puis stocker le résultat dans un état basé sur si l’application se trouve dans Teams.
    le [hook useState](https://reactjs.org/docs/hooks-state.html) de React fournit le stockage requis, et [useEffect](https://reactjs.org/docs/hooks-effect.html) vous permet d’appeler `getFluidContainer` le rendu, en passant la valeur retournée dans `setFluidContainer`.

    En ajoutant `inTeams` le tableau de dépendances à la fin de l’application `useEffect`, l’application garantit que cette fonction est appelée uniquement lors du chargement de la page de contenu.

1. Remplacez `TODO 6` par le code suivant :

    ```ts
    if (inTeams === false) {
      return (
          <div>This application only works in the context of Microsoft Teams</div>
      );
    }

    if (fluidContainer !== undefined) {
      return (
          <FluidComponent fluidContainer={fluidContainer} />
      );
    }

    return (
      <div>Loading FluidComponent...</div>
    );
    ```

    > [!NOTE]
    > Il est important de s’assurer que la page de contenu est chargée dans Teams et que le conteneur Fluid est défini avant de le passer dans le composant React (défini comme `FluidComponent`, voir ci-dessous).

### <a name="create-react-component-for-fluid-view-and-data"></a>Créer React composant pour la vue et les données Fluid

Vous avez intégré le flux de création de base de Teams et Fluid. Vous pouvez maintenant créer votre propre composant React qui gère les interactions entre la vue application et les données Fluid. À partir de maintenant, la logique et le flux se comportent comme d’autres applications optimisées pour Fluid. Une fois la structure de base configurée, vous pouvez créer n’importe quel [exemple Fluid](https://github.com/microsoft/FluidExamples) en tant qu’application Teams en modifiant l’interaction de l’affichage de l’application `ContainerSchema` avec les objets DDSes/data dans la page de contenu.

## <a name="start-the-fluid-server-and-run-the-application"></a>Démarrer le serveur Fluid et exécuter l’application

Si vous exécutez votre application Teams localement avec le mode local du client Azure, veillez à exécuter la commande suivante dans l’invite de commandes pour démarrer le service Fluid :

```cmd
npx @fluidframework/azure-local-service@latest
```

Pour exécuter et démarrer l’application Teams, ouvrez un autre terminal et suivez les [instructions pour exécuter le serveur d’applications](create-channel-group-tab.md#upload-your-application-to-teams).

> [!WARNING]
> Les noms d’hôte avec `ngrok`des tunnels gratuits ne sont pas conservés. Chaque exécution génère une URL différente. Lorsqu’un nouveau `ngrok` tunnel est créé, l’ancien conteneur n’est plus accessible. Pour les scénarios de production, consultez [utiliser AzureClient avec Azure Fluid Relay](#use-azureclient-with-azure-fluid-relay).

> [!NOTE]
> Installez une dépendance supplémentaire pour rendre cette démonstration compatible avec Webpack 5. Si vous recevez une erreur de compilation liée à un package « buffer », exécutez `npm install -D buffer` et réessayez. Cela sera résolu dans une prochaine version de Fluid Framework.

## <a name="next-steps"></a>Prochaines étapes

### <a name="use-azureclient-with-azure-fluid-relay"></a>Utiliser AzureClient avec Azure Fluid Relay

Comme il s’agit d’une application d’onglet Teams, la collaboration et l’interaction sont le principal objectif. Remplacez le mode `AzureClientProps` local fourni précédemment par les informations d’identification non locales de votre instance de service Azure, afin que d’autres personnes puissent participer à l’application et interagir avec vous. Découvrez [comment provisionner votre service Azure Fluid Relay](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

> [!IMPORTANT]
> Il est important de masquer les informations d’identification que vous transmettez `AzureClientProps` pour qu’elles ne soient pas validées accidentellement dans le contrôle de code source. Le projet Teams est fourni avec un `.env` fichier dans lequel vous pouvez stocker vos informations d’identification en tant que variables d’environnement et le fichier lui-même est déjà inclus dans le `.gitignore`. Pour utiliser les variables d’environnement dans Teams, consultez [Définir et obtenir la variable d’environnement](#set-and-get-environment-variable).

> [!WARNING]
> `InsecureTokenProvider` est un moyen pratique de tester l’application localement. Il vous incombe de gérer toute authentification utilisateur et d’utiliser un [jeton sécurisé](/azure/azure-fluid-relay/how-tos/connect-fluid-azure-service) pour n’importe quel environnement de production.

### <a name="set-and-get-environment-variable"></a>Définir et obtenir une variable d’environnement

Pour définir une variable d’environnement et la récupérer dans Teams, vous pouvez tirer parti du fichier intégré `.env` . Le code suivant est utilisé pour définir la variable d’environnement dans `.env`:

```
# .env

TENANT_KEY=foobar
```

Pour transmettre le contenu du `.env` fichier à notre application côté client, vous devez les `webpack.config.js` configurer pour leur `webpack` permettre d’y accéder au moment de l’exécution. Utilisez le code suivant pour ajouter la variable d’environnement à partir de `.env`:

```js
// webpack,config.js

webpack.EnvironmentPlugin({
    PUBLIC_HOSTNAME: undefined,
    TAB_APP_ID: null,
    TAB_APP_URI: null,
    REACT_APP_TENANT_KEY: JSON.stringify(process.env.TENANT_KEY) // Add environment variable here
}),
```

Vous pouvez accéder à la variable d’environnement dans `Util.ts`

```ts
// Util.ts

tokenProvider: new InsecureTokenProvider(JSON.parse(process.env.REACT_APP_TENANT_KEY!), { id: "user" }),
```

> [!TIP]
> Lorsque vous apportez des modifications au code, le projet se regénère automatiquement et le serveur d’applications se recharge. Toutefois, si vous apportez des modifications au schéma de conteneur, elles ne prendront effet que si vous fermez et redémarrez le serveur d’applications. Pour ce faire, accédez à l’invite de commandes et appuyez deux fois sur Ctrl-C. Ensuite, exécutez ou `gulp ngrok-serve` réexélez`gulp serve`.

## <a name="see-also"></a>Voir aussi

- [Documentation Azure Fluid Relay](/azure/azure-fluid-relay)

- [Documentation Fluid Framework](https://fluidframework.com/docs/)
- [Exemples de dépôt GitHub Fluid](https://github.com/microsoft/FluidExamples)
