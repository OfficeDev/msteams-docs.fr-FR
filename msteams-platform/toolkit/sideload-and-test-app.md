---
title: Chargement indépendant et test de l’application dans l’environnement Teams
author: zyxiaoyuer
description: Dans ce module, découvrez comment charger une version test et tester l’application dans un environnement différent
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 721b3a30bcc8c2fa49bb06491f4ab24bbeb844fd
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833001"
---
# <a name="sideload-and-test-app-in-teams-environment"></a>Chargement indépendant et test de l’application dans l’environnement Teams

Après avoir ajouté la connexion d’API, vous pouvez tester la connexion d’API dans l’environnement local teams Toolkit et déployer votre application dans le cloud. Dans le pipeline CI/CD, après avoir été configuré avec une autre plateforme, vous devez créer un principal de service Azure pour provisionner et déployer des ressources.

Dans cette section, vous allez découvrir

* [Tester la connexion d’API dans un environnement local](#test-api-connection-in-local-environment)
* [Déployer votre application sur Azure](#deploy-your-application-to-azure)
* [Provisionner et déployer des ressources CI/CD](#provision-and-deploy-cicd-resources)

## <a name="test-api-connection-in-local-environment"></a>Tester la connexion d’API dans un environnement local

Les étapes suivantes permettent de tester la connexion d’API dans l’environnement local du Kit de ressources Teams :

 1. **Exécuter npm install**

    Exécutez `npm install` sous `bot` le dossier ou `api` pour installer les packages ajoutés.

 2. **Ajouter des informations d’identification d’API aux paramètres de l’application locale**

    Teams Toolkit ne demande pas d’informations d’identification, mais laisse des espaces réservés dans le fichier de paramètres de l’application locale. Remplacez les espaces réservés par les informations d’identification appropriées pour accéder à l’API. Le fichier de paramètres de l’application locale est le `.env.teamsfx.local` fichier dans le `bot` dossier ou `api` .

 3. **Utiliser le client d’API pour effectuer des demandes d’API**

    Importez le client d’API à partir du code source qui a besoin d’accéder à l’API :

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **Générer des requêtes http(s) vers l’API cible (avec Axios)**

    Le client d’API généré est un client d’API Axios. Utilisez le client Axios pour effectuer des requêtes à l’API.

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) est un package nodejs populaire qui vous aide avec les requêtes http(s). Pour plus d’informations sur la façon d’effectuer des requêtes http(s), consultez [l’exemple de documentation Axios](https://axios-http.com/docs/example) pour apprendre à créer des http(s).

## <a name="deploy-your-application-to-azure"></a>Déployer votre application sur Azure

Pour déployer votre application sur Azure, vous devez ajouter l’authentification aux paramètres de l’application pour l’environnement approprié. Par exemple, votre API peut avoir des informations d’identification différentes pour `dev` et `prod`. En fonction des besoins de l’environnement, configurez Teams Toolkit.

Teams Toolkit configure votre environnement local. L’exemple de code de stratégie de démarrage contient des commentaires qui vous indiquent les paramètres d’application que vous devez configurer. Pour plus d’informations sur les paramètres d’application, consultez [Ajouter des paramètres d’application](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings).

## <a name="provision-and-deploy-cicd-resources"></a>Provisionner et déployer des ressources CI/CD

Pour provisionner et déployer des ressources ciblant Azure dans CI/CD, vous devez créer un principal de service Azure à utiliser.

Procédez comme suit pour créer des principaux de service Azure :

1. Inscrivez une application Microsoft Azure Active Directory (Azure AD) dans un seul locataire.
2. Assign a role to your Azure AD application to access your Azure subscription. The `Contributor` role is recommended.
3. Créez un secret d’application Azure AD.

> [!TIP]
> Enregistrez votre ID de locataire, l’ID d’application (AZURE_SERVICE_PRINCIPAL_NAME) et le secret (AZURE_SERVICE_PRINCIPAL_PASSWORD) pour une utilisation ultérieure.

Pour plus d’informations, consultez [Instructions relatives aux principaux de service Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Les trois méthodes suivantes permettent de créer des principaux de service :

* [Portail Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="see-also"></a>Voir aussi

[Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
