---
title: Charger et tester une application dans l’environnement Teams
author: zyxiaoyuer
description: Dans ce module, découvrez comment charger et tester une application dans un environnement différent
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: ee1d3ee3a4f545a6c988c421fb18626a4a7276b7
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617216"
---
# <a name="sideload-and-test-app-in-teams-environment"></a>Charger et tester une application dans l’environnement Teams

Après avoir ajouté une connexion d’API, vous pouvez tester la connexion d’API dans l’environnement local du Kit de ressources Teams et déployer votre application dans le cloud. Dans le pipeline CI/CD, après avoir configuré avec une plateforme différente, vous devez créer un principal de service Azure pour provisionner et déployer des ressources.

Dans cette section, vous allez découvrir

* [Tester la connexion d’API dans un environnement local](#test-api-connection-in-local-environment)
* [Déployer votre application sur Azure](#deploy-your-application-to-azure)
* [Provisionner et déployer des ressources CI/CD](#provision-and-deploy-cicd-resources)

## <a name="test-api-connection-in-local-environment"></a>Tester la connexion d’API dans un environnement local

Les étapes suivantes permettent de tester la connexion d’API dans l’environnement local du Kit de ressources Teams :

 1. **Exécuter l’installation de npm**

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

Teams Toolkit configure votre environnement local. L’exemple de code bootstrapped contient des commentaires qui vous indiquent les paramètres d’application que vous devez configurer. Pour plus d’informations sur les paramètres de l’application, consultez [Ajouter des paramètres d’application](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings)

## <a name="provision-and-deploy-cicd-resources"></a>Provisionner et déployer des ressources CI/CD

Pour provisionner et déployer des ressources ciblant Azure dans CI/CD, vous devez créer un principal de service Azure à utiliser.

Procédez comme suit pour créer des principaux de service Azure :

1. Inscrivez une application Microsoft Azure Active Directory (Azure AD) dans un seul locataire.
2. Attribuez un rôle à votre application Azure AD pour accéder à votre abonnement Azure. Le rôle `Contributor` est conseillé.
3. Créez un secret d’application Azure AD.

> [!TIP]
> Enregistrez votre ID de locataire, l’ID d’application (AZURE_SERVICE_PRINCIPAL_NAME) et le secret (AZURE_SERVICE_PRINCIPAL_PASSWORD) pour une utilisation ultérieure.

Pour plus d’informations, consultez [Instructions relatives aux principaux de service Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Les trois méthodes suivantes permettent de créer des principaux de service :

* [Portail Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="see-also"></a>Voir aussi

* [Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
