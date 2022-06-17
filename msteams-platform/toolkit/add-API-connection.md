---
title: Connecter aux API existantes
author: MuyangAmigo
description: Dans cet article, découvrez comment le kit de ressources vous aide à démarrer un exemple d’accès aux API existantes. Il fournit la liste des différents types d’authentification.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: dc987718233801a6855fd534d561fe2f3d964aa7
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143297"
---
# <a name="add-api-connection-to-teams-app"></a>Ajouter une connexion d’API à l’application Teams

Teams Toolkit vous permet d’accéder aux API existantes pour la création d’applications Teams. Ces API sont développées par votre organisation ou par un tiers.

## <a name="advantage"></a>Avantage

Teams Toolkit vous aide à démarrer l’exemple de code pour accéder aux API si vous n’avez pas les kits SDK appropriés pour accéder à ces API.

## <a name="connect-to-the-api"></a>Connecter à l’API

Lorsque vous utilisez Teams Toolkit pour vous connecter à une API existante, Teams Toolkit exécute la fonction suivante :

* Générez un exemple de code sous `./bot` ou `./api` dossier.
* Ajoutez une référence au `@microsoft/teamsfx` package à `package.json`.
* Ajoutez des paramètres d’application pour votre API dans  `.env.teamsfx.local` lequel le débogage local est configuré.

### <a name="connect-to-api-in-visual-studio-code"></a>Connecter à l’API dans Visual Studio Code

* Vous pouvez ajouter une connexion d’API à l’aide de Teams Toolkit dans Visual Studio Code :

    1. Ouvrez Microsoft Visual Studio Code.
    2. Sélectionnez :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="Teams’icône d’API"::: Toolkit dans la barre de navigation de gauche.
    3. Sélectionnez **Ajouter des fonctionnalités** sous **DÉVELOPPEMENT** :

        :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="api add features":::

       * Vous pouvez également ouvrir la palette de commandes et entrer **Teams : Ajouter des ressources cloud**.

    4. Dans la fenêtre contextuelle, sélectionnez la **connexion API** que vous souhaitez ajouter à votre projet d’application Teams :

        :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="fonctionnalités de sélection d’api":::

    5. Sélectionnez **OK**.

    6. Entrez le point de terminaison de l’API. Il est ajouté aux paramètres d’application locale du projet et il s’agit de l’URL de base pour les demandes d’API.

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="point de terminaison d’api":::

         > [!NOTE]
         > Vérifiez que le point de terminaison est une URL http(s) valide.

    7. Sélectionnez le composant qui accède à l’API.

    8. Sélectionnez **OK**.

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="appel d’api":::

    9. Entrez un alias pour l’API. L’alias génère un nom de paramètre d’application pour l’API qui est ajouté au paramètre d’application local du projet.

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="alias d’api":::

    10. Sélectionnez l’authentification requise pour la demande d’API à partir du **type d’authentification d’API**. Il génère l’exemple de code approprié et ajoute les paramètres d’application local correspondants en fonction de votre sélection.

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-auth.png" alt-text="authentification d’api":::

         > [!NOTE]
         > En fonction du type d’authentification sélectionné, une configuration supplémentaire est nécessaire.

### <a name="api-connection-in-teamsfx-cli"></a>Connexion d’API dans l’interface CLI TeamsFx

La commande de base de cette fonctionnalité est `teamsfx add api-connection [authentication type]`. Le tableau suivant fournit la liste des différents types d’authentification et leurs exemples de commandes correspondants :

 > [!Tip]
 > Vous pouvez utiliser `teamsfx add api-connection [authentication type] -h` ce document pour obtenir de l’aide.

   |**Type d’authentification type**|**Exemple de commande**|
   |-----------------------|------------------|
   |De base|teamsfx add api-connection basic --endpoint <https://example.com> --component bot --alias example--user-name exampleuser --interactive false|
   |Clé API|teamsfx add api-connection apikey --endpoint <https://example.com> --component bot --alias example --key-location header --key-name example-key-name --interactive false|
   |Azure AD|teamsfx add api-connection aad --endpoint <https://example.com> --component bot --alias example --app-type custom --tenant-id your_tenant_id --app-id your_app_id --interactive false|
   |Certificat|teamsfx add api-connection cert --endpoint <https://example.com> --component bot --alias example --interactive false|
   |Personnalisé|teamsfx add api-connection custom --endpoint <https://example.com> --component bot --alias example --interactive false|

## <a name="understand-toolkit-updates-to-your-project"></a>Comprendre les mises à jour du kit de ressources de votre projet

 Teams Toolkit modifie `bot` ou `api` dossier en fonction de vos sélections :

1. Générer un `{your_api_alias}.js/ts` fichier. Le fichier initialise un client d’API pour votre API et exporte le client d’API.

2. Ajouter `@microsoft/teamsfx` un package à `package.json`. Le package prend en charge les méthodes d’authentification d’API courantes.

3. Ajoutez des variables d’environnement à `.env.teamsfx.local`. Ce sont les configurations pour le type d’authentification sélectionné. Le code généré lit les valeurs des variables d’environnement.

## <a name="test-api-connection-in-local-environment"></a>Tester la connexion d’API dans un environnement local

Les étapes suivantes permettent de tester la connexion d’API dans l’environnement local Teams Toolkit :

 1. **Exécuter npm installation**

    Exécutez `npm install` sous `bot` ou `api` dossier pour installer les packages ajoutés.

 2. **Ajouter des informations d’identification d’API aux paramètres de l’application locale**

    Teams Toolkit ne demande pas d’informations d’identification, mais laisse des espaces réservés dans le fichier de paramètres de l’application locale. Remplacez les espaces réservés par les informations d’identification appropriées pour accéder à l’API. Le fichier de paramètres de l’application locale est le `.env.teamsfx.local` fichier dans le ou `api` le `bot` dossier.

 3. **Utiliser le client d’API pour effectuer des demandes d’API**

    Importez le client d’API à partir du code source qui a besoin d’accéder à l’API :

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **Générer des requêtes http(s) vers l’API cible (avec Axios)**

    Le client d’API généré est un client d’API Axios. Utilisez le client Axios pour effectuer des demandes à l’API.

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) est un package nodejs populaire qui vous aide avec les requêtes http.s. Pour plus d’informations sur la façon d’effectuer des requêtes http(s), consultez [l’exemple de documentation Axios](https://axios-http.com/docs/example) pour savoir comment créer des http(s).

## <a name="deploy-your-application-to-azure"></a>Déployer votre application sur Azure

Pour déployer votre application sur Azure, vous devez ajouter l’authentification aux paramètres de l’application pour l’environnement approprié. Par exemple, votre API peut avoir des informations d’identification différentes pour `dev` et `prod`. En fonction des besoins de l’environnement, configurez Teams Toolkit.

Teams Toolkit configure votre environnement local. L’exemple de code bootstrapped contient des commentaires qui vous indiquent les paramètres d’application que vous devez configurer. Pour plus d’informations sur les paramètres d’application, consultez [Ajouter des paramètres d’application](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings).

## <a name="advanced-scenarios"></a>Scénarios d’enregistrement avancés

  La section suivante vous explique les scénarios avancés :

<br>

<details>
<summary><b>Fournisseur d’authentification personnalisé</b></summary>

Outre le fournisseur d’authentification inclus dans le `@microsoft/teamsfx` package, vous pouvez également implémenter un fournisseur d’authentification personnalisé qui implémente `AuthProvider` l’interface et l’utilise en `createApiClient(..)` fonction :

```Bash
import { AuthProvider } from '@microsoft/teamsfx'

class CustomAuthProvider implements AuthProvider {
    constructor() {
        // You can add necessary parameters for your customized logic in constructor
    }

    AddAuthenticationInfo: (config: AxiosRequestConfig) => Promise<AxiosRequestConfig> = async (
        config
    ) => {
        /*
        * The config parameter contains all the request information and can be updated to include extra authentication info.
        * Refer https://axios-http.com/docs/req_config for detailed document for the config object.
        * 
        * Add your customized logic that returns updated config
        */
    };
}
```

</details>
<details>
<summary><b>Connecter aux API pour les autorisations Azure AD</b></summary>
Azure AD authentifie certains services. La liste suivante permet d’accéder à ces services pour configurer les autorisations d’API.

* [Utiliser des listes Access Control (ACL)](#access-control-lists-acls)
* [Utiliser les autorisations d’application Azure AD](#azure-ad-application-permissions)

L’obtention d’un jeton avec les étendues de ressources appropriées pour votre API dépend de l’implémentation de l’API.

Vous pouvez suivre les étapes pour accéder à ces API tout en utilisant :

#### <a name="access-control-lists-acls"></a>listes Access Control (ACL)

   1. Démarrez le débogage local sur l’environnement cloud pour votre projet. Il crée une inscription d’application Azure AD pour votre application Teams.
  
   2. Ouvrez `.fx/states/state.{env}.json`et notez la valeur sous la `clientId` `fx-resource-aad-app-for-teams` propriété.

   3. Fournissez l’ID client au fournisseur d’API pour configurer les listes de contrôle d’accès sur le service d’API.

#### <a name="azure-ad-application-permissions"></a>Autorisations d’application Azure AD

  1. Ouvrez `templates/appPackage/aad.template.json` et ajoutez le contenu suivant à la `requiredResourceAccess` propriété :

```JSON
 {
     "resourceAppId": "The AAD App Id for the service providing the API you are connecting to",
     "resourceAccess": [
         {
             "id": "Target API's application permission Id",
             "type": "Role"
         }
     ]
 }
```

   2. Démarrez le débogage local sur l’environnement cloud pour votre projet. Il crée une inscription d’application Azure AD pour votre application Teams.

   3. Ouvrez `.fx/states/state.{env}.json` et notez la valeur de `clientId` under `fx-resource-aad-app-for-teams` , propriété. Il s’agit de l’ID client de l’application.

   4. Accordez le consentement de l’administrateur pour l’autorisation d’application requise. Pour plus d’informations, consultez [accorder le consentement de l’administrateur](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations).

        > [!NOTE]
        > Pour l’autorisation d’application, utilisez votre ID client.
        >
</details>

## <a name="see-also"></a>Voir aussi

* [Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
