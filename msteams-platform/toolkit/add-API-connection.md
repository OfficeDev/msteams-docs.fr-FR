---
title: Intégrer des API tierces existantes
author: MuyangAmigo
description: Dans cet article, découvrez comment le kit de ressources vous aide à démarrer un exemple d’accès aux API existantes. Il fournit la liste des différents types d’authentification.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: 5933227f9ba4c8b684d624a8857304c044761578
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616808"
---
# <a name="integrate-existing-third-party-apis"></a>Intégrer des API tierces existantes

Teams Toolkit vous permet d’accéder aux API existantes pour créer des applications Teams. Ces API sont développées par votre organisation ou par un tiers. Lorsque vous utilisez Teams Toolkit pour vous connecter à une API existante, Teams Toolkit exécute la fonction suivante :

* Générez un exemple de code sous `./bot` ou `./api` dossier.
* Ajoutez une référence au `@microsoft/teamsfx` package à `package.json`.
* Ajoutez des paramètres d’application pour votre API dans  `.env.teamsfx.local` lequel le débogage local est configuré.

## <a name="steps-to-connect-to-api"></a>Étapes de connexion à l’API

Vous pouvez ajouter une connexion API à l’aide de Visual Studio Code et de la commande CLI.

### <a name="add-api-connection-using-visual-studio-code"></a>Ajouter une connexion d’API à l’aide de Visual Studio Code

Les étapes suivantes vous aident à ajouter une connexion d’API à l’aide de Visual Studio Code :

1. Ouvrez Microsoft Visual Studio Code.
2. Sélectionnez :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="l’icône de l’API"::: Kit de ressources Teams dans la barre d’outils Visual Studio Code.
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

     :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/myAPI connection.png" alt-text="authentification d’api":::

     En fonction du type d’authentification sélectionné, les étapes suivantes sont nécessaires pour effectuer une configuration supplémentaire

# <a name="basic"></a>[Basique](#tab/basic)

* Entrez le nom d’utilisateur de l’authentification de base.

  L’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

# <a name="certification"></a>[Certification](#tab/certification)

   L’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

# <a name="azure-active-directory"></a>[Azure Active Directory](#tab/AAD)

  L’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

# <a name="api-key"></a>[Clé API](#tab/apikey)

* Sélectionnez la position de clé API requise dans la demande.

* Entrez un nom de clé API.

  L’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

# <a name="custom-auth-implementation"></a>[Implémentation d’authentification personnalisée](#tab/CustomAuthImplementation)

  L’exemple de code a été généré pour appeler votre API à bot\myAPI.js.

---

## <a name="add-api-connection-using-cli"></a>Ajouter une connexion d’API à l’aide de l’interface CLI

La commande de base de cette fonctionnalité est `teamsfx add api-connection [authentication type]`. Le tableau suivant fournit la liste des différents types d’authentification et leurs exemples de commandes correspondants :

 > [!TIP]
 > Vous pouvez utiliser `teamsfx add api-connection [authentication type] -h` ce document pour obtenir de l’aide.

   |**Type d’authentification type**|**Exemple de commande**|
   |-----------------------|------------------|
   |De base|teamsfx add api-connection basic--endpoint <https://example.com> --component bot--alias example--user-name exampleuser--interactive false|
   |Clé API|teamsfx add api-connection apikey--endpoint <https://example.com> --component bot--alias example--key-location header--key-name example-key-name--interactive false|
   |Azure AD|teamsfx add api-connection aad--endpoint <https://example.com> --component bot--alias example--app-type custom--tenant-id your_tenant_id--app-id your_app_id--interactive false|
   |Certificat|teamsfx add api-connection cert--endpoint <https://example.com> --component bot--alias example--interactive false|
   |Personnalisé|teamsfx add api-connection custom--endpoint <https://example.com> --component bot--alias example--interactive false|

---

## <a name="directory-structure-updates-to-your-project"></a>Mises à jour de la structure d’annuaires de votre projet

 Teams Toolkit modifie `bot` ou `api` dossier en fonction de vos sélections :

1. Générer un `{your_api_alias}.js/ts` fichier. Le fichier initialise un client d’API pour votre API et exporte le client d’API.

2. Ajouter `@microsoft/teamsfx` un package à `package.json`. Le package prend en charge les méthodes d’authentification d’API courantes.

3. Ajoutez des variables d’environnement à `.env.teamsfx.local`. Ce sont les configurations pour le type d’authentification sélectionné. Le code généré lit les valeurs des variables d’environnement.

## <a name="advantages"></a>Avantages

Teams Toolkit vous aide à démarrer l’exemple de code pour accéder aux API, si vous n’avez pas les kits de développement logiciel (SDK) appropriés pour accéder à ces API.

## <a name="see-also"></a>Voir aussi

* [Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
