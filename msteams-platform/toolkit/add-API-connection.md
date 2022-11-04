---
title: Intégrer des API tierces existantes
author: MuyangAmigo
description: Dans cet article, découvrez comment le kit de ressources vous aide à démarrer des exemples d’accès aux API existantes. Il fournit la liste des différents types d’authentification.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: 6377f7d8a38054dacca76c0f87e39e51f466d925
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833141"
---
# <a name="integrate-existing-third-party-apis"></a>Intégrer des API tierces existantes

Teams Toolkit vous permet d’accéder aux API existantes pour créer des applications Teams. Ces API sont développées par votre organisation ou par un tiers. Lorsque vous utilisez Teams Toolkit pour vous connecter à une API existante, Teams Toolkit exécute la fonction suivante :

* Générez un exemple de code sous `./bot` le dossier ou `./api` .
* Ajoutez une référence au `@microsoft/teamsfx` package à `package.json`.
* Ajoutez des paramètres d’application pour votre API dans  `.env.teamsfx.local` qui configure le débogage local.

## <a name="steps-to-connect-to-api"></a>Étapes de connexion à l’API

Vous pouvez ajouter une connexion d’API à l’aide de Visual Studio Code et de la commande CLI.

### <a name="add-api-connection-using-visual-studio-code"></a>Ajouter une connexion d’API à l’aide de Visual Studio Code

Les étapes suivantes vous aident à ajouter une connexion d’API à l’aide de Visual Studio Code :

1. Ouvrez Microsoft Visual Studio Code.
2. Sélectionnez :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="l’icône d’API"::: Teams Toolkit dans la barre d’outils Visual Studio Code.
3. Sélectionnez **Ajouter des fonctionnalités** sous **DÉVELOPPEMENT** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="api ajouter des fonctionnalités":::

    * Vous pouvez également ouvrir la palette de commandes et entrer **Teams : Ajouter des ressources cloud**.

4. Dans la fenêtre contextuelle, sélectionnez la **connexion d’API** que vous souhaitez ajouter à votre projet d’application Teams :

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="api select features":::

5. Sélectionnez **OK**.

6. Entrez point de terminaison pour l’API. Il est ajouté aux paramètres d’application locaux du projet et il s’agit de l’URL de base pour les demandes d’API.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="Point de terminaison d’api":::

     > [!NOTE]
     > Vérifiez que le point de terminaison est une URL HTTP valide.

7. Sélectionnez le composant qui accède à l’API.

8. Sélectionnez **OK**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="appel d’api":::

9. Entrez un alias pour l’API. L’alias génère un nom de paramètre d’application pour l’API qui est ajouté au paramètre d’application local du projet.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="alias d’api":::

10. Sélectionnez Authentification requise pour la demande d’API dans le **type d’authentification de l’API**. Il génère un exemple de code approprié et ajoute les paramètres d’application locaux correspondants en fonction de votre sélection.

     :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/myAPI connection.png" alt-text="Authentification api":::

     En fonction du type d’authentification sélectionné, les étapes suivantes sont requises pour effectuer une configuration supplémentaire

# <a name="basic"></a>[Basique](#tab/basic)

* Entrez le nom d’utilisateur de l’authentification de base.

  Maintenant, l’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

# <a name="certification"></a>[Certification](#tab/certification)

   Maintenant, l’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

# <a name="azure-active-directory"></a>[Azure Active Directory](#tab/AAD)

  Maintenant, l’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

# <a name="api-key"></a>[Clé API](#tab/apikey)

* Sélectionnez la position de clé API requise dans la demande.

* Entrez un nom de clé API.

  Maintenant, l’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

# <a name="custom-auth-implementation"></a>[Implémentation d’authentification personnalisée](#tab/CustomAuthImplementation)

  Maintenant, l’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

---

## <a name="add-api-connection-using-cli"></a>Ajouter une connexion d’API à l’aide de l’interface CLI

La commande de base de cette fonctionnalité est `teamsfx add api-connection [authentication type]`. Le tableau suivant fournit la liste des différents types d’authentification et leurs exemples de commandes correspondants :

 > [!TIP]
 > Vous pouvez utiliser `teamsfx add api-connection [authentication type] -h` pour obtenir un document d’aide.

   |**Type d’authentification type**|**Exemple de commande**|
   |-----------------------|------------------|
   |De base|teamsfx ajouter api-connection basic--endpoint <https://example.com> --component bot--alias example--user-name exampleuser--interactive false|
   |Clé API|teamsfx ajouter api-connection apikey--endpoint <https://example.com> --component bot--alias example--key-location header---key-name example-key-name--interactive false|
   |Azure AD|teamsfx ajouter api-connection aad--endpoint <https://example.com> --component bot--alias example--app--type custom--tenant-id your_tenant_id--app-id your_app_id--interactive false|
   |Certificat|teamsfx ajouter api-connection cert--endpoint <https://example.com> --component bot--alias example--interactive false|
   |Personnalisé|teamsfx ajouter api-connection custom--endpoint <https://example.com> --component bot---alias example--interactive false|

---

## <a name="directory-structure-updates-to-your-project"></a>Mises à jour de la structure de répertoires de votre projet

 Le Kit de ressources Teams modifie `bot` ou `api` dossier en fonction de vos sélections :

1. Générer un `{your_api_alias}.js/ts` fichier. Le fichier initialise un client API pour votre API et exporte le client d’API.

2. Ajoutez le `@microsoft/teamsfx` package à `package.json`. Le package prend en charge les méthodes d’authentification d’API courantes.

3. Ajoutez des variables d’environnement à `.env.teamsfx.local`. Il s’agit des configurations pour le type d’authentification sélectionné. Le code généré lit les valeurs des variables d’environnement.

## <a name="advantages"></a>Avantages

Teams Toolkit vous aide à démarrer l’exemple de code pour accéder aux API, si vous n’avez pas de sdk appropriés au langage pour accéder à ces API.

## <a name="see-also"></a>Voir aussi

[Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
