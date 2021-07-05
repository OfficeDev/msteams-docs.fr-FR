---
title: Get started - Build your first Teams app with Blazor
author: adrianhall
description: Créez rapidement une application Microsoft Teams qui affiche un message « Hello, World ! » à l’aide Microsoft Teams Shared Computer Toolkit et .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: c14f55d014af120cab88044d31ee8600017e3c57
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254306"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a>Créer et exécuter votre première application Microsoft Teams avec Blazor

Dans ce didacticiel, vous allez apprendre à créer une application Microsoft Teams dans .NET/Blazor qui implémente une application personnelle simple pour tirer des informations du microsoft Graph. Par exemple, une *application personnelle inclut* un ensemble d’onglets pour une utilisation individuelle. Au cours du didacticiel, vous allez découvrir la structure d’une application Teams, comment exécuter une application localement et comment déployer l’application sur Azure.

L'application créée affiche des informations de base sur l'utilisateur actuel.  Lorsque l'autorisation est accordée, l'application se connecte au Microsoft Graph en tant qu'utilisateur actuel pour obtenir le profil complet.

## <a name="before-you-begin"></a>Avant de commencer

Assurez-vous que votre environnement de développement est installé en installant les conditions préalables.

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="create-your-project"></a>Créer votre projet

Utilisez le Kit de ressources Teams pou créer votre premier projet :

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

1. Ouvrez Visual Studio 2019.

1. Sélectionnez **Créer un projet.**

1. Sélectionnez **Microsoft Teams application,** puis sélectionnez **Suivant.**  Pour vous aider à trouver le modèle, utilisez le type de **projet Microsoft Teams**.

1. Entrez un nom et sélectionnez **Suivant.**

1. Entrez le nom de l’application et le nom de la société.

1. Sélectionnez **Créer**.  Le nom de l’application et le nom de la société sont affichés pour vos utilisateurs finaux. Votre application Teams est créée en quelques secondes.  Une fois le projet créé, configurer l' sign-on unique avec M365 :

   1. Sélectionnez **Project**  >  **TeamsFx**  >  **Configurer pour l' sso...**.
   1. Lorsque vous y invitez, connectez-vous à votre compte d’administrateur M365.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

1. Ouvrez un Terminal et sélectionnez le répertoire dans lequel vous souhaitez créer le projet.

1. Exécutez `dotnet new -i` cette page pour installer le modèle à partir NuGet :

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   Vous ne devez le faire que la première fois ou lors de la mise à jour du modèle. Vérifiez [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) la dernière version de ce package.

1. Créez un répertoire :

   ``` bash
   mkdir helloworld
   ```

1. Exécutez `dotnet new` cette recherche pour créer un projet :

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. Après la mise en place de la échafaudage, configurez le projet pour Teams déploiement :

   ``` bash
   teamsfx init
   ```

   Vous pouvez maintenant ouvrir la solution dans Visual Studio débogage.

---

## <a name="take-a-tour-of-the-source-code"></a>Suivre une visite guidée du code source

Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).

Une fois Teams Shared Computer Toolkit votre projet, vous avez les composants pour créer une application personnelle de base pour Teams. Les répertoires et fichiers du projet s’affichent dans la zone Explorateur de solutions Visual Studio 2019.

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Capture d’écran montrant les fichiers de projet d’application pour une application personnelle Visual Studio 2019.":::

- Les icônes d’application sont stockées sous forme de fichiers PNG dans `color.png` et `outline.png`.
- Le manifeste de l’application pour la publication via le portail de développement pour Teams est stocké dans `Properties/manifest.json` .
- Un contrôleur de serveur back-end est fourni pour `Controllers/BackendController.cs` faciliter l’authentification.

Étant donné que vous avez créé une application d’onglet lors de l’installation, l’Teams Shared Computer Toolkit crée la modèle de tout le code nécessaire pour un onglet de base en tant que [serveur Blazor](/aspnet/core/blazor).

- `Pages/Tab.razor` est le point d’entrée de l’application frontale.
- `TeamsFx.cs`et `JS/src/index.js` sert à initialiser les communications avec l’Teams hôte.

Vous pouvez ajouter des fonctionnalités de back-end en ajoutant des contrôleurs ASP.NET Core supplémentaires à votre application.

## <a name="run-your-app-locally"></a>Exécuter votre application localement

Le Kit de ressources Teams vous permet d’exécuter votre application localement.  Il s’agit de plusieurs parties nécessaires pour fournir l’infrastructure correcte attendue par Teams :

- Une application est inscrite auprès de Azure Active Directory.  Cette application dispose d’autorisations associées à l’emplacement à partir duquel l’application est chargée et aux ressources principales auxquelles elle accède.
- Une API web est hébergée (via IIS Express) pour faciliter les tâches d’authentification, agissant en tant que proxy entre l’application et Azure Active Directory.  
- Un manifeste d'application est généré et existe dans le portail des développeurs pour Teams.  Teams utilise le manifeste de l’application pour indiquer aux clients connectés où charger l’application.

Une fois cette demande effectuée, l’application peut être chargée dans le client Teams client.  Nous utilisons le client web Teams pour voir le code HTML, CSS et JavaScript dans un environnement de développement web standard.

Pour créer et exécuter votre application localement :


1. À Visual Studio Code, appuyez sur la **touche F5** pour exécuter votre application en mode débogage.


1. Si nécessaire, installez le certificat SSL auto-signé pour le débogage local.

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. Teams sera chargée dans un navigateur web et vous serez invité à vous connecter. Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur. Connectez-vous à votre compte M365.

1. Lorsque vous y invitez l’application sur Teams, sélectionnez **Ajouter.**

   Votre application s’affiche désormais :

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Capture d’écran de l’application terminée":::

   Vous pouvez effectuer les activités de débogage comme s’il s’était produit une autre application web telle que la définition de points d’arrêt. L’application prend en charge le rechargement à chaud.  Si vous modifiez un fichier dans le projet, la page est rechargée.

<!-- markdownlint-disable MD033 -->
<details>
<summary>Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</summary>

Lorsque vous appuyez sur **la touche F5,** le Teams Shared Computer Toolkit :

1. Inscrit votre application avec Azure Active Directory.
1. Inscrit votre application pour le « chargement de version latéral » dans Microsoft Teams.
1. Démarre le back-end de votre application en cours d’exécution localement.
1. Démarre votre application frontale hébergée localement.
1. Démarre Microsoft Teams dans un navigateur web avec une commande pour demander Teams charger l’application de côté (l’URL est enregistrée dans le manifeste de l’application).

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</summary>

Pour exécuter correctement votre application dans Teams, vous devez avoir un compte de développement Microsoft 365 qui permet le chargement côté application. Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).

</details>

## <a name="deploy-your-app-to-azure"></a>Déployer votre application sur Azure

Le déploiement se compose de deux étapes : 

1. Les ressources cloud nécessaires sont créées. C’est également ce qu’on appelle la mise en service.
1. Commencez à coder et copiez votre application dans les ressources cloud créées.

> **Aperçu**
>
> La prise en charge des applications Blazor est une nouveauté de Teams Shared Computer Toolkit.  L’approvisionnement et le déploiement sont effectués avec une combinaison de Visual Studio 2019 et du portail de développement pour Teams.

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a>Mettre en service et déployer votre application dans Azure App Service

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le nœud de projet et sélectionnez **Publier.** Vous pouvez également utiliser **l’élément**  >  **de** menu Publier la build.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Sélectionner l’opération Publier sur le projet":::

1. Dans la **fenêtre** Publier, sélectionnez **Azure** et **selct Next**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Sélectionner Azure comme cible de publication":::

1. Sélectionnez **Azure App Service (Windows)** et **sélectionnez Suivant**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Sélectionner Azure App Service comme cible de publication":::

1. Sélectionnez **+** pour créer une nouvelle instance du service d’application.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Créez une instance.":::

1. Dans la boîte de dialogue Créer un service d’application  **(Windows),** les champs d’entrée **Nom,** Nom de l’abonnement, Groupe de ressources et **Plan** d’hébergement sont remplies. Si un service d’application est déjà en cours d’exécution, les paramètres existants sont sélectionnés.  Vous pouvez choisir de créer un groupe de ressources et un plan d’hébergement.  Lorsque vous êtes prêt, sélectionnez **Créer.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Sélectionner le plan d’hébergement et l’abonnement":::

1. Dans la **boîte de** dialogue Publier, l’instance nouvellement créée a été automatiquement sélectionnée.  Lorsque vous êtes prêt, sélectionnez **Terminer.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Sélectionnez la nouvelle instance.":::

1. Sélectionnez **l’icône** Modifier (crayon) en de côté du **mode** déploiement, puis sélectionnez **Autonome.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Sélectionnez le mode de déploiement autonome.":::

1. Sélectionnez **Publier**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Publier votre application sur le service d’application":::

   Visual Studio déploie l’application sur votre service d’application Azure et l’application web se charge dans votre navigateur.  `/tab`Ajoutez-la à la fin de l’URL pour afficher votre page.

   Le volet **Publication** des propriétés du projet affiche l’URL du site et d’autres détails. Notez l’URL du site.

## <a name="create-an-environment-for-your-app"></a>Créer un environnement pour votre application

Le Portail des développeurs pour Teams l’endroit où les onglets de votre application sont chargés à partir d’un **environnement.**  

**Pour créer un environnement :**

1. Ouvrez [le portail du développeur pour Teams](https://dev.teams.microsoft.com).  Connectez-vous avec votre compte d’administration M365.

1. Dans la barre latérale, sélectionnez **Applications.**

1. Si vous n’avez qu’une seule application, elle sera automatiquement sélectionnée.  Si ce n’est pas le cas, sélectionnez votre application dans la liste.

1. Sélectionnez **Environnements**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Sélectionner des environnements":::

1. Sélectionnez **Créer votre premier environnement.**

1. Entrez un nom pour votre environnement, puis sélectionnez **Ajouter.** Par exemple, `_Production_`.

1. Sélectionnez **Créer votre première variable d’environnement.**

1. Entrez `azure_app_url` le **nom**.  Entrez l’URL de votre site Azure sans `https://` la valeur . 

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Créer une variable d’environnement":::

   Appuyez **sur Ajouter.**

## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Le manifeste de l’application charge l’onglet à partir d’une `localhost` URL.  Dans cette section, vous allez configurer le manifeste de l’application pour charger l’onglet à partir de l’URL répertoriée dans l’environnement que vous avez créé.

1. Dans la barre latérale, sélectionnez **Informations de base.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Sélectionner des informations de base":::

1. Il existe plusieurs endroits dans le manifeste qui résentent un élément `locahost:XXXXX` dans une URL.  Remplacez toutes les occurrences `{{azure_app_url}}` par , y compris les accolades.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Ajuster les informations de base pour l’environnement":::

1. Lorsque vous avez terminé, sélectionnez **Enregistrer.**

1. Dans la barre latérale, sélectionnez **Fonctionnalités.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Sélectionner des fonctionnalités":::

1. Sélectionnez **Onglet personnel.**
1. En de côté de **l’onglet Personnel,** sélectionnez les trois points, puis sélectionnez **Modifier.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Modifier les paramètres d’onglet personnel":::

1. Remplacez l’URL par la variable d’environnement dans les champs **URL de contenu** et URL du **site** web.

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Modifier les URL d’onglet personnel":::

1. Sélectionnez **Mettre à jour**.

1. Sélectionnez **Enregistrer**.

1. Dans la barre latérale, sélectionnez **Sign-On unique**.

1. Remplacez `localhost` **l’URI de l’ID d’application** par `{{azure_app_url}}` .

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Modifier l’URI de l’ID d’application d' sign-on unique":::

1. Sélectionnez **Enregistrer**.

1. Dans la barre latérale, sélectionnez **Domaines.**

1. Sélectionnez **Ajouter un domaine**.

1. Si ce domaine n’est pas répertorié comme un domaine valide, ajoutez-le en tant que `{{azure_app_url}}` domaine valide, puis sélectionnez **Ajouter.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Ajouter un domaine":::

   Vous pouvez désormais utiliser l’option Aperçu **Teams** en haut de la page pour lancer votre application dans Teams.

## <a name="see-also"></a>Voir aussi

* [Présentation des didacticiels](code-samples.md)
* [Créer une application de bot de conversation](first-app-bot.md)
* [Créer une extension de messagerie](first-message-extension.md)
* [Exemples de code](https://github.com/OfficeDev/Microsoft-Teams-Samples)
