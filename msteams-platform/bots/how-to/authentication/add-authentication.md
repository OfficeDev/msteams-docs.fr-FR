---
title: Ajouter l’authentification à votre bot Teams’argent
author: clearab
description: Comment ajouter l’authentification OAuth à un bot dans Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 36cb6f3de6f97af1d01512175923b79f69f630ad
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565969"
---
# <a name="add-authentication-to-your-teams-bot"></a>Ajouter l’authentification à votre bot Teams’argent

Il ya des moments où vous devrez peut-être créer des bots dans Microsoft Teams qui peuvent accéder à des ressources pour le compte de l’utilisateur, comme un service de messagerie.

Cet article montre comment utiliser Azure Bot Service v4 SDK authentification, basée sur OAuth 2.0. Il est ainsi plus facile de développer un bot qui peut utiliser des jetons d’authentification basés sur les informations d’identification de l’utilisateur. La clé dans tout cela est l’utilisation de **fournisseurs d’identité**, comme nous le verrons plus loin.

OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable pour travailler avec l’authentification Teams.

Voir [OAuth 2 Simplifié](https://aka.ms/oauth2-simplified) pour une compréhension de base, [et OAuth 2.0](https://oauth.net/2/) pour la spécification complète.

Pour plus d’informations sur la façon dont le Service Azure Bot gère l’authentification, consultez [l’authentification utilisateur dans une conversation](https://aka.ms/azure-bot-authentication).

Voici les titres des sections de cet article :

- **Comment créer un bot activé par l’authentification**. Vous utiliserez [l’échantillon cs-auth pour gérer][teams-auth-bot-cs] les informations d’identification de connexion de l’utilisateur et la génération du jeton d’authentification.
- **Comment déployer le bot sur Azure et l’associer à un fournisseur d’identité**. Le fournisseur émet un jeton basé sur les informations d’identification de connexion de l’utilisateur. Le bot peut utiliser le jeton pour accéder aux ressources, telles qu’un service postal, qui nécessitent une authentification. Pour plus d’informations, [Microsoft Teams flux d’authentification pour les bots](auth-flow-bot.md).
- **Comment intégrer le bot dans Microsoft Teams**. Une fois que le bot a été intégré, vous pouvez vous connecter et échanger des messages avec lui dans un chat.

## <a name="prerequisites"></a>Configuration requise

- Connaissance des bases [bot , état][concept-basics]de gestion , [la][concept-state]bibliothèque de [dialogues][concept-dialogs], et comment implémenter [le flux de conversation séquentielle][simple-dialog].
- Connaissance du développement Azure et OAuth 2.0.
- Les versions actuelles de Visual Studio et Git.
- Compte Azure. Si nécessaire, vous pouvez créer un [compte azure gratuit](https://azure.microsoft.com/free/).
- L’échantillon suivant :

    | Échantillon | Version BotBuilder | Démontre |
    |:---|:---:|:---|
    | **Authentification** bot [en échantillon cs-auth][teams-auth-bot-cs] | v4 (en) | Support OAuthCard |
    | **Authentification** bot [en js-auth-sample][teams-auth-bot-js] | v4 (en)| Support OAuthCard  |
    | **Authentification** bot [en py-auth-sample][teams-auth-bot-py] | v4 (en) | Support OAuthCard |

## <a name="create-the-resource-group"></a>Créer le groupe de ressources

Le groupe de ressources et le plan de service ne sont pas strictement nécessaires, mais ils vous permettent de libérer facilement les ressources que vous créez. C’est une bonne pratique pour garder vos ressources organisées et gérables.

Vous utilisez un groupe de ressources pour créer des ressources individuelles pour le Cadre Bot. Pour des performances, assurez-vous que ces ressources sont situées dans la même région Azure.

1. Dans votre navigateur, connectez-vous [**au portail Azure**][azure-portal].
1. Dans le panneau de navigation gauche, sélectionnez **Groupes de ressources**.
1. En haut à gauche de la fenêtre affichée, sélectionnez **Ajouter l’onglet** pour créer un nouveau groupe de ressources. Vous serez invité à fournir les éléments suivants :
    1. **Abonnement**. Utilisez votre abonnement existant.
    1. **Groupe de ressources**. Entrez le nom du groupe de ressources. Un exemple pourrait être  *TeamsResourceGroup*. Rappelez-vous que le nom doit être unique.
    1. Dans le menu **de** drop-down de la Région, *sélectionnez West US* ou une région proche de vos applications.
    1. Sélectionnez **l’examen et créez** le bouton. Vous devriez voir une bannière qui se lit *validation passé*.
    1. Sélectionnez **le bouton** Créer. La création du groupe de ressources peut prendre quelques minutes.

> [!TIP]
> Comme avec les ressources que vous allez créer plus tard dans ce tutoriel, c’est une bonne idée d’épingler ce groupe de ressources à votre tableau de bord pour un accès facile. Si vous souhaitez le faire, sélectionnez l’icône de goupille &#128204; en haut à droite du tableau de bord.

## <a name="create-the-service-plan"></a>Créer le plan de service

1. Dans le [**portail Azure**][azure-portal], sur le panneau de navigation gauche, **sélectionnez Créer une ressource**.
1. Dans la boîte de recherche, tapez *App Service Plan*. Sélectionnez la **carte App Service Plan** à partir des résultats de recherche.
1. Sélectionnez **Créer**.
1. Il vous sera demandé de fournir les informations suivantes :
    1. **Abonnement**. Vous pouvez utiliser un abonnement existant.
    1. **Groupe de ressources**. Sélectionnez le groupe que vous avez créé précédemment.
    1. **Nom**. Entrez le nom du plan de service. Un exemple pourrait être  *TeamsServicePlan*. Rappelez-vous que le nom doit être unique, au sein du groupe.
    1. **Système d’exploitation**. Sélectionnez *Windows* ou votre système d’exploitation applicable.
    1. **Région**. Sélectionnez *West US* ou une région proche de vos applications.
    1. **Niveau de tarification**. Assurez-vous *que standard S1* est sélectionné. Il devrait s’agir de la valeur par défaut.
    1. Sélectionnez **l’examen et créez** le bouton. Vous devriez voir une bannière qui se lit *validation passé*.
    1. Sélectionnez **Créer**. La création du plan de service de l’application peut prendre quelques minutes. Le plan sera inscrit dans le groupe de ressources.

## <a name="create-the-bot-channels-registration"></a>Créer l’enregistrement des canaux bot

L’enregistrement des canaux bot enregistre votre service Web en tant que bot avec le Cadre Bot, à condition d’avoir un identifiant d’application Microsoft et un mot de passe app (secret client).

> [!IMPORTANT]
> Vous n’avez besoin d’enregistrer votre bot que s’il n’est pas hébergé dans Azure. Si vous [avez créé un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) via le portail Azure, il est déjà enregistré auprès du service. Si vous avez créé votre bot via le [Bot Framework](https://dev.botframework.com/bots/new) ou [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) votre bot n’est pas enregistré sur Azure.

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> La ressource d’enregistrement bot channels affichera la région **mondiale même** si vous avez sélectionné West US. Ceci est normal.

Pour plus d’informations, [voir Créer un bot pour Teams](../create-a-bot-for-teams.md).

## <a name="create-the-identity-provider"></a>Créer le fournisseur d’identité

Vous avez besoin d’un fournisseur d’identité qui peut être utilisé pour l’authentification.
Dans cette procédure, vous utiliserez un fournisseur d’ANNONCE Azure ; d’autres fournisseurs d’identité pris en charge par Azure AD peuvent également être utilisés.

1. Dans le [**portail Azure**][azure-portal], sur le panneau de navigation gauche, sélectionnez **Azure Active Directory**.
    > [!TIP]
    > Vous devrez créer et enregistrer cette ressource Azure AD dans un locataire dans lequel vous pouvez consentir à déléguer les autorisations demandées par une application.
    > Pour obtenir des instructions sur la création d’un locataire, [consultez Accéder au portail et créer un locataire.](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)
1. Dans le panneau gauche, sélectionnez **les enregistrements app**.
1. Dans le panneau de droite, sélectionnez le **nouvel onglet** d’enregistrement, en haut à gauche.
1. Il vous sera demandé de fournir les informations suivantes :
   1. **Nom**. Entrez le nom de l’application. Un exemple pourrait être  *BotTeamsIdentity*. Rappelez-vous que le nom doit être unique.
   1. Sélectionnez les **types de compte pris en** charge pour votre application. Sélectionnez *les comptes dans n’importe quel répertoire organisationnel (Tout répertoire Azure AD - Multitenant) et les comptes Microsoft personnels (par exemple Skype, Xbox).*
   1. Pour **l’URI Redirect**:<br/>
       &#x2713;Select **Web**. <br/>
       &#x2713; définir l’URL à `https://token.botframework.com/.auth/web/redirect` .
   1. Sélectionnez **Inscrire**.

1. Une fois qu’il est créé, Azure affiche la page **Vue d’ensemble** de l’application. Copiez et enregistrez les informations suivantes dans un fichier :

    1. La valeur **d’identification de l’application (client).** Vous utiliserez cette valeur plus tard comme identifiant *client lorsque vous* enregistrerez cette application d’identité Azure avec votre bot.
    1. La **valeur d’identification de l’annuaire (locataire).** Vous utiliserez également cette valeur plus tard en tant *qu’identifiant locataire* pour enregistrer cette application d’identité Azure avec votre bot.

1. Dans le panneau gauche, sélectionnez **certificats & secrets** pour créer un secret client pour votre application.

   1. Sous **secrets clients**, sélectionnez &#x2795; nouveau secret **client**.
   1. Ajoutez une description pour identifier ce secret à partir d’autres que vous devrez peut-être créer pour cette application, comme *l’application d’identité Bot dans Teams*.
   1. **L’ensemble expire** à votre sélection.
   1. Sélectionnez **Ajouter**.
   1. Avant de quitter cette page, **enregistrez le secret**. Vous utiliserez cette valeur plus tard comme _secret client lorsque_ vous enregistrerez votre application Azure AD avec votre bot.

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>Configurez la connexion du fournisseur d’identité et enregistrez-la avec le bot

Notez qu’il existe deux options pour les fournisseurs de services ici-Azure AD V1 et Azure AD V2.  Les différences entre les deux fournisseurs sont résumées ici, [mais](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)en général, V2 offre plus de flexibilité en ce qui concerne la modification des autorisations de bot.  Graph Les autorisations api sont répertoriées dans le champ de portée, et au fur et à mesure que de nouvelles autorisations sont ajoutées, les bots permettront aux utilisateurs de consentir aux nouvelles autorisations lors de la prochaine inscription.  Pour V1, le consentement du bot doit être supprimé par l’utilisateur pour que de nouvelles autorisations soient incitées dans le dialogue OAuth. 

#### <a name="azure-ad-v1"></a>Azure AD V1

1. Dans le portail [**Azure,**][azure-portal]sélectionnez votre groupe de ressources à partir du tableau de bord.
1. Sélectionnez votre lien d’enregistrement de canal bot.
1. Ouvrez la page de ressources et **sélectionnez Configuration** **sous Paramètres**. 
1. Sélectionnez **Ajouter OAuth Connection Paramètres**.    
L’image suivante affiche la sélection correspondante dans la page de ressources :  
![Configuration SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)
1. Remplissez le formulaire comme suit :

    1. **Nom**. Entrez un nom pour la connexion. Vous utiliserez ce nom dans votre bot dans le `appsettings.json` fichier. Par exemple *BotTeamsAuthADv1*.
    1. **Fournisseur de services**. Sélectionner **Azure Active Directory**. Une fois que vous sélectionnez ceci, les champs azuréens spécifiques à la MA s’affichent.
    1. **Id client**. Entrez l’iD d’application (client) que vous avez enregistré pour votre application fournisseur d’identité Azure dans les étapes ci-dessus.
    1. **Secret client**. Entrez le secret que vous avez enregistré pour votre application fournisseur d’identité Azure dans les étapes ci-dessus.
    1. **Type de subvention**. Entrez `authorization_code` .
    1. **URL de connexion**. Entrez `https://login.microsoftonline.com` .
    1. **Identifiant locataire**, entrez **l’IDENTIFIANT d’annuaire (locataire) que vous** avez enregistré précédemment pour votre application d’identité Azure ou commun **en** fonction du type de compte pris en charge sélectionné lors de la création de l’application fournisseur d’identité. Pour décider quelle valeur attribuer, suivez les critères suivants :

        - Si vous avez sélectionné soit les comptes de cet *annuaire organisationnel uniquement (Microsoft uniquement - locataire unique)* ou *les comptes dans n’importe quel répertoire organisationnel (répertoire Microsoft AAD - Multi locataire) entrez l’identifiant* de locataire que **vous** avez enregistré précédemment pour l’application AAD. Ce sera le locataire associé aux utilisateurs qui peuvent être authentifiés.

        - Si vous avez sélectionné *des comptes dans n’importe quel répertoire organisationnel (tout répertoire AAD - Compte Microsoft multi locataire et personnel par exemple Skype, Xbox, Outlook) entrez* le mot **commun au lieu d’un** identifiant de locataire. Dans le cas contraire, l’application AAD vérifiera par l’intermédiaire du locataire dont l’iD a été sélectionné et exclura les comptes Microsoft personnels.

    h. Pour **l’URL de** ressource, entrez `https://graph.microsoft.com/` . Ceci n’est pas utilisé dans l’échantillon de code actuel.  
    i. Laissez **les portées** vides. L’image suivante est un exemple :

    ![équipes bots app auth connection string adv1 view](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. Sélectionnez **Enregistrer**.

#### <a name="azure-ad-v2"></a>Azure AD V2

1. Dans le portail [**Azure,**][azure-portal]sélectionnez votre groupe de ressources à partir du tableau de bord.
1. Sélectionnez votre lien d’enregistrement de canal bot.
1. Ouvrez la page de ressources et **sélectionnez Configuration** **sous Paramètres**. 
1. Sélectionnez **Ajouter OAuth Connection Paramètres**.  
L’image suivante affiche la sélection correspondante dans la page de ressources :        
![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png) 

1. Remplissez le formulaire comme suit :

    1. **Nom**. Entrez un nom pour la connexion. Vous utiliserez ce nom dans votre bot dans le `appsettings.json` fichier. Par exemple *BotTeamsAuthADv2*.
    1. **Fournisseur de services**. Sélectionnez **Azure Active Directory v2**. Une fois que vous sélectionnez ceci, les champs azuréens spécifiques à la MA s’affichent.
    1. **Id client**. Entrez l’iD d’application (client) que vous avez enregistré pour votre application fournisseur d’identité Azure dans les étapes ci-dessus.
    1. **Secret client**. Entrez le secret que vous avez enregistré pour votre application fournisseur d’identité Azure dans les étapes ci-dessus.
    1. **URL de Exchange jetons**. Laisse ce vide.
    1. **Identifiant locataire**, entrez **l’IDENTIFIANT d’annuaire (locataire) que vous** avez enregistré précédemment pour votre application d’identité Azure ou commun **en** fonction du type de compte pris en charge sélectionné lors de la création de l’application fournisseur d’identité. Pour décider quelle valeur attribuer, suivez les critères suivants :

        - Si vous avez sélectionné soit les comptes de cet *annuaire organisationnel uniquement (Microsoft uniquement - locataire unique)* ou *les comptes dans n’importe quel répertoire organisationnel (répertoire Microsoft AAD - Multi locataire) entrez l’identifiant* de locataire que **vous** avez enregistré précédemment pour l’application AAD. Ce sera le locataire associé aux utilisateurs qui peuvent être authentifiés.

        - Si vous avez sélectionné *des comptes dans n’importe quel répertoire organisationnel (tout répertoire AAD - Compte Microsoft multi locataire et personnel par exemple Skype, Xbox, Outlook) entrez* le mot **commun au lieu d’un** identifiant de locataire. Dans le cas contraire, l’application AAD vérifiera par l’intermédiaire du locataire dont l’iD a été sélectionné et exclura les comptes Microsoft personnels.

    1. Pour **scopes**, entrez une liste délimitée dans l’espace des autorisations graphiques de cette application nécessite par exemple: User.Read User.ReadBasic.All Mail.Read 

1. Sélectionnez **Enregistrer**.

### <a name="test-the-connection"></a>Testez la connexion

1. Sélectionnez l’entrée de connexion pour ouvrir la connexion que vous venez de créer.
1. Sélectionnez **Connexion de** test en haut du panneau de **réglage de connexion fournisseur de** services.
1. La première fois que vous faites cela ouvrira une nouvelle fenêtre de navigateur vous demandant de sélectionner un compte. Sélectionnez celui que vous souhaitez utiliser.
1. Ensuite, il vous sera demandé de permettre au fournisseur d’identité d’utiliser vos données (informations d’identification). L’image suivante est un exemple :

    ![équipes bot auth connection string adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. Sélectionnez **Accepter**.
1. Cela devrait ensuite vous rediriger vers une connexion de test à la page **\<your-connection-name> Succeeded.** Actualisez la page si vous obtenez une erreur. L’image suivante est un exemple :

    ![équipes bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

Le nom de connexion est utilisé par le code bot pour récupérer les jetons d’authentification de l’utilisateur.

## <a name="prepare-the-bot-sample-code"></a>Préparer le code d’échantillon bot

Avec les paramètres préliminaires faits, nous allons nous concentrer sur la création du bot à utiliser dans cet article.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. Clone [cs-auth-sample][teams-auth-bot-cs].
1. Lancez-Visual Studio.
1. À partir de la barre **d’outils sélectionnez Fichier -> Open -> Project/Solution** et ouvrez le projet bot.
1. Dans C# Update **appsettings.jssur** comme suit:

    - Définissez `ConnectionName` le nom de la connexion fournisseur d’identité que vous avez ajoutée à l’enregistrement du canal bot. Le nom que nous avons utilisé dans cet exemple *est BotTeamsAuthADv1*.
    - Définissez `MicrosoftAppId` sur **l’id d’application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.
    - Définissez `MicrosoftAppPassword` le secret client **que** vous avez enregistré au moment de l’enregistrement du canal bot.

    Selon les caractères de votre secret bot, vous devrez peut-être XML échapper au mot de passe. Par exemple, tous les ampersands (&) devront être codés comme `&amp;` .

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. Dans le Solution Explorer, accédez au `TeamsAppManifest` dossier, ouvrez `manifest.json` et définissez `id` et vers `botId` **l’ID d’application bot que** vous avez enregistré au moment de l’enregistrement du canal bot.

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. Clone [nœud-auth-échantillon][teams-auth-bot-js].
1. Dans une console, accédez au projet : </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. Installer des modules</br></br>
`npm install`
1. Mettez à jour la configuration **.env** comme suit :

    - Définissez `MicrosoftAppId` sur **l’id d’application bot** que vous avez enregistré au moment de l’enregistrement du canal bot.
    - Définissez `MicrosoftAppPassword` le secret client **que** vous avez enregistré au moment de l’enregistrement du canal bot.
    - Définissez le `connectionName` nom de la connexion du fournisseur d’identité.
    Selon les caractères de votre secret bot, vous devrez peut-être XML échapper au mot de passe. Par exemple, tous les ampersands (&) devront être codés comme `&amp;` .

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. Dans le `teamsAppManifest` dossier, ouvrez `manifest.json` et définissez `id`  votre identifiant **d’application Microsoft et** `botId` **l’identifiant d’application bot que** vous avez enregistré au moment de l’enregistrement du canal bot.

# <a name="python"></a>[Python](#tab/python)

1. Clone [py-auth-sample][teams-auth-bot-py] du dépôt github.
1. Mise à **config.py**:

    - Définissez `ConnectionName` le nom du paramètre de connexion OAuth que vous avez ajouté à votre bot.
    - Définissez `MicrosoftAppId` et `MicrosoftAppPassword` vers l’iD de l’application de votre bot et le secret de l’application.

      Selon les caractères de votre secret bot, vous devrez peut-être XML échapper au mot de passe. Par exemple, tous les ampersands (&) devront être codés comme `&amp;` .

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>Déployer le bot sur Azure

Pour déployer le bot, suivez les étapes dans la façon de [déployer votre bot sur Azure](https://aka.ms/azure-bot-deployment-cli).

Alternativement, pendant Visual Studio, vous pouvez suivre ces étapes :

1. Dans Visual Studio *Solution Explorer sélectionnez* et maintenez (ou cliquez à droite) le nom du projet.
1. Dans le menu drop-down, sélectionnez **Publier**.
1. Dans la fenêtre affichée, sélectionnez le **nouveau** lien.
1. Dans la fenêtre de dialogue, **sélectionnez App Service** à gauche et **Créez nouveau** à droite.
1. Sélectionnez **le bouton** Publier.
1. Dans la fenêtre de dialogue suivante, entrez les informations requises. Voici un exemple :

    ![service auth-app](../../../assets/images/authentication/auth-bot-app-service.png)

1. Sélectionnez **Créer**.
1. Si le déploiement se termine avec succès, vous devez le voir reflété dans Visual Studio. En outre, une page est affichée dans votre navigateur par défaut en disant *que votre bot est prêt!*. L’URL sera similaire à ceci: `https://botteamsauth.azurewebsites.net/` . Enregistrez-le dans un fichier.
1. Dans votre navigateur, accédez [**au portail Azure**][azure-portal].
1. Vérifiez votre groupe de ressources, le bot doit être répertorié avec les autres ressources. L’image suivante est un exemple :

    ![équipes-bot-auth-app-service-groupe](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. Dans le groupe de ressources, sélectionnez le nom d’enregistrement du canal bot (lien).
1. Dans le panneau gauche, sélectionnez **Paramètres**.
1. Dans la boîte **de point de terminaison** messagerie, entrez l’URL obtenue ci-dessus suivie de `api/messages` . C’est un exemple: `https://botteamsauth.azurewebsites.net/api/messages` .
1. Sélectionnez le bouton **Enregistrer** en haut à gauche.

## <a name="test-the-bot-using-the-emulator"></a>Testez le bot à l’aide de l’émulateur

Si vous ne l’avez pas déjà fait, installez [le Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme). Voir aussi [Debug avec l’Émulateur](https://aka.ms/bot-framework-emulator-debug-with-emulator).

Pour que l’échantillon de bot fonctionne, vous devez configurer l’émulateur.

### <a name="configure-the-emulator-for-authentication"></a>Configurer l’émulateur pour l’authentification

Si un bot nécessite une authentification, vous devez configurer l’émulateur. Pour configurer :

1. Démarrez l’émulateur.
1. Dans l’émulateur, sélectionnez l’icône de vitesse &#9881; en bas à gauche, **ou l’émulateur Paramètres** onglet en haut à droite.
1. Cochez la case **par utilisez les jetons d’authentification de la version 1.0**.
1. Entrez le chemin local vers **l’outil ngrok.** *Voir* le Bot Framework Emulator / ngrok tunneling intégration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)). Pour plus d’informations sur les outils, [voir ngrok](https://ngrok.com/).
1. Cochez la **case par Run ngrok lorsque l’émulateur démarre.**
1. Sélectionnez **le bouton Enregistrer.**

Lorsque le bot affiche une carte de connectement et que l’utilisateur sélectionne le bouton de dédonnement, l’émulateur ouvre une page que l’utilisateur peut utiliser pour se connecter avec le fournisseur d’authentification.
Une fois que l’utilisateur le fait, le fournisseur génère un jeton utilisateur et l’envoie au bot. Après cela, le bot peut agir au nom de l’utilisateur.

### <a name="test-the-bot-locally"></a>Testez le bot localement

Une fois que vous avez configuré le mécanisme d’authentification, vous pouvez effectuer les tests de bot réels.  

1. Exécutez l’échantillon de bot localement sur votre machine, via Visual Studio par exemple.
1. Démarrez l’émulateur.
1. Sélectionnez **le bouton Open bot.**
1. Dans **l’URL Bot**, entrez l’URL locale du bot. Habituellement, `http://localhost:3978/api/messages` .
1. Dans **l’iD de l’application Microsoft,** entrez l’iD de l’application du bot à partir `appsettings.json` de .
1. Dans le mot **de passe microsoft app** entrez le mot de passe de l’application du bot à partir de la `appsettings.json` .
1. Sélectionnez **Connecter**.
1. Une fois le bot opérationnel, entrez n’importe quel texte pour afficher la carte de dédage.
1. Sélectionnez le bouton **Se connecter**.
1. Un dialogue contexturé s’affiche pour confirmer **l’URL ouverte**. Il s’agit de permettre à l’utilisateur du bot (vous) d’être authentifié.  
1. Sélectionner **Confirmer**.
1. Si on vous le demande, sélectionnez le compte de l’utilisateur applicable.
1. Selon la configuration que vous avez utilisée pour l’émulateur, vous obtenez l’une des configurations suivantes :
    1. **Utilisation du code de vérification de la dédontologie**  
      &#x2713; une fenêtre est ouverte affichant le code de validation.  
      &#x2713; copiez et entrez le code de validation dans la boîte de chat pour compléter l’inscription.
    1. **Utilisation de jetons d’authentification**.  
      &#x2713; Vous êtes connecté en fonction de vos informations d’identification.

    L’image suivante est un exemple de l’interface utilisateur bot après que vous vous êtes connecté:

    ![émulateur de connexion auth bot](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. Si vous **sélectionnez** Oui lorsque le bot *demande Souhaitez-vous afficher votre jeton?*, vous obtiendrez une réponse similaire à ce qui suit:

    ![jetons émulateur de connexion bot auth](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. Entrez **le logout** dans la boîte de chat d’entrée pour vous déduter. Cela libère le jeton utilisateur, et le bot ne sera pas en mesure d’agir en votre nom jusqu’à ce que vous vous connectez à nouveau.

> [!NOTE]
> L’authentification bot nécessite **l’utilisation du service de connecteur Bot**. Le service accède aux informations d’enregistrement des canaux bot pour votre bot.

## <a name="test-the-deployed-bot"></a>Testez le bot déployé

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. Dans votre navigateur, accédez [**au portail Azure**][azure-portal].
1. Trouvez votre groupe de ressources.
1. Sélectionnez le lien de ressources. La page de ressources s’affiche.
1. Dans la page de ressources, **sélectionnez Test in Web Chat**. Le bot démarre et affiche les salutations prédéfinis.
1. Tapez n’importe quoi dans la boîte de chat.
1. Sélectionnez **le panneau dans la** boîte.
1. Un dialogue contexturé s’affiche pour confirmer **l’URL ouverte**. Il s’agit de permettre à l’utilisateur du bot (vous) d’être authentifié.  
1. Sélectionner **Confirmer**.
1. Si on vous le demande, sélectionnez le compte de l’utilisateur applicable.
    L’image suivante est un exemple de l’interface utilisateur bot après que vous vous êtes connecté:

    ![connexion bot auth déployé](../../../assets/images/authentication/auth-bot-login-deployed.PNG).

1. Sélectionnez le **bouton Oui** pour afficher votre jeton d’authentification. L’image suivante est un exemple :

    ![connexion bot auth déployé jeton](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG).

1. Entrez logout pour vous déduter.

    ![auth bot déployé logout](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> Si vous avez des problèmes de connexion, essayez de tester la connexion à nouveau comme décrit dans les étapes précédentes. Cela pourrait recréer le jeton d’authentification.
> Avec le client Bot Framework Web Chat dans Azure, vous devrez peut-être vous connecter plusieurs fois avant que l’authentification ne soit correctement établie.

## <a name="install-and-test-the-bot-in-teams"></a>Installez et testez le bot dans Teams

1. Dans votre projet de bot, assurez-vous que `TeamsAppManifest` le dossier contient le long avec un et des `manifest.json` `outline.png` `color.png` fichiers.
1. Dans Solution Explorer, accédez au `TeamsAppManifest` dossier. Modifier `manifest.json` en attribuant les valeurs suivantes :
    1. Assurez-vous que **l’ID d’application bot** que vous avez reçu au moment de l’enregistrement du canal bot est attribué `id` à et `botId` .
    1. Attribuez cette valeur : `validDomains: [ "token.botframework.com" ]` .
1. Sélectionnez et **zip** le `manifest.json` , et les `outline.png` `color.png` fichiers.
1. Ouvrez **Microsoft Teams**.
1. Dans le panneau gauche, en bas, sélectionnez **l’icône Apps**.
1. Dans le panneau droit, en bas, sélectionnez **Télécharger une application personnalisée.**
1. Naviguez dans `TeamsAppManifest` le dossier et téléchargez le manifeste zippé.
L’assistant suivant s’affiche :

    ![auth bot équipes télécharger](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. Sélectionnez le bouton **Ajouter à une équipe**.
1. Dans la fenêtre suivante, sélectionnez l’équipe où vous souhaitez utiliser le bot.
1. Sélectionnez **le bouton Configurer un bot.**
1. Sélectionnez les trois points (&#x25cf;&#x25cf;&#x25cf;) dans le panneau gauche. Sélectionnez ensuite **l’icône App Studio.**
1. Sélectionnez **l’onglet Éditeur** Manifeste. Vous devriez voir l’icône pour le bot que vous avez téléchargé.
1. En outre, vous devriez être en mesure de voir le bot répertorié comme un contact dans la liste de chat que vous pouvez utiliser pour échanger des messages avec le bot.

### <a name="testing-the-bot-locally-in-teams"></a>Tester le bot localement dans Teams

Microsoft Teams est un produit entièrement basé sur le cloud, il nécessite tous les services qu’il accède pour être disponible à partir du cloud en utilisant les points de terminaison HTTPS. Par conséquent, pour permettre au bot (notre échantillon) de fonctionner en Teams, vous devez soit publier le code sur le nuage de votre choix, soit rendre une instance localement en cours d’exécution accessible à l’extérieur via **un outil de tunneling.** Nous recommandons  [ngrok](https://ngrok.com/download), qui crée une URL adressable extérieurement pour un port que vous ouvrez localement sur votre machine.
Pour configurer ngrok en vue de l’exécution de votre application Microsoft Teams’application locale, suivez les étapes suivantes :

1. Dans une fenêtre terminale, allez à l’annuaire où vous avez `ngrok.exe` installé. Nous suggérons de définir *le chemin variable de* l’environnement pour le pointer vers elle.
1. Exécuter, par exemple, `ngrok http 3978 --host-header=localhost:3978` . Remplacez le numéro de port au besoin.
Cela lance ngrok pour écouter sur le port que vous spécifiez. En retour, il vous donne une URL adressable extérieurement, valide aussi longtemps que ngrok est en cours d’exécution. L’image suivante est un exemple :

    ![équipes bot app auth connection string adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG).

1. Copiez l’adresse HTTPS de forwarding. Il devrait être similaire à ce qui suit: `https://dea822bf.ngrok.io/` .
1. Annexe à `/api/messages` obtenir `https://dea822bf.ngrok.io/api/messages` . Il s’agit **du point de terminaison** des messages pour le bot fonctionnant localement sur votre machine et accessible sur le Web dans un chat Microsoft Teams.
1. Une dernière étape à effectuer est de mettre à jour le point de terminaison des messages du bot déployé. Dans l’exemple, nous avons déployé le bot dans Azure. Donc **effectuons ces étapes :
    1. Dans votre navigateur naviguer vers le [**portail Azure**][azure-portal].
    1. Sélectionnez votre **inscription bot channel**.
    1. Dans le panneau gauche, sélectionnez **Paramètres**.
    1. Dans le panneau droit, dans la boîte **de point de terminaison** messagerie, entrez l’URL ngrok, dans notre exemple, `https://dea822bf.ngrok.io/api/messages` .
1. Démarrez votre bot localement, par exemple en mode Visual Studio débog.
1. Testez le bot tout en exécutant localement en utilisant le chat Web de test **du portail Bot** Framework . Comme l’émulateur, ce test ne vous permet pas d’accéder Teams fonctionnalités spécifiques.
1. Dans la fenêtre terminale `ngrok` où s’exécution, vous pouvez voir le trafic HTTP entre le bot et le client de chat web. Si vous voulez une vue plus détaillée, dans une fenêtre de navigateur, entrez-vous `http://127.0.0.1:4040` obtenu à partir de la fenêtre terminale précédente. L’image suivante est un exemple :

    ![auth bot équipes ngrok test](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png).

> [!NOTE]
> Si vous arrêtez et redémarrez ngrok, l’URL change. Pour utiliser ngrok dans votre projet, et en fonction des fonctionnalités que vous utilisez, vous devez mettre à jour toutes les références URL.
 

## <a name="additional-information"></a>Informations supplémentaires

### <a name="teamsappmanifestmanifestjson"></a>TeamsAppManifest/manifest.jssur

Ce manifeste contient les informations dont Microsoft Teams pour se connecter avec le bot :  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

Avec l’authentification, Teams se comporte légèrement différemment des autres canaux, comme expliqué ci-dessous.

### <a name="handling-invoke-activity"></a>Manipulation Invoquer l’activité

Une **activité Invocant** est envoyée au bot plutôt qu’à l’activité événementale utilisée par d’autres canaux.
Ceci est fait en sous-classant le **ActivityHandler**.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**Bots/DialogBot.cs**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**Bots/TeamsBot.cs**

*L’activité Invocation* doit être transmise au dialogue si **l’OAuthPrompt** est utilisé.

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a>TeamsActivityHandler.cs

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[JavaScript](#tab/node-js-dialog-sample)

**bots/dialogBot.js**

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

**bots/teamsBot.js**

*L’activité Invocation* doit être transmise au dialogue si **l’OAuthPrompt** est utilisé.

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**dialogues/mainDialog.js**

Dans une étape de dialogue, utilisez `beginDialog` pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.

- Si l’utilisateur est déjà connecté, cela générera un événement de réponse symbolique, sans inciter l’utilisateur.
- Dans le cas contraire, cela incitera l’utilisateur à se connecter. Le service Azure Bot envoie l’événement de réponse symbolique après que l’utilisateur tente de se connecter.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

Dans l’étape de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente. Si ce n’est pas nul, l’utilisateur s’est connecté avec succès.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**bots/logoutDialog.js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**bots/dialog_bot.py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**bots/teams_bot.py**

*L’activité Invocation* doit être transmise au dialogue si **l’OAuthPrompt** est utilisé.

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**dialogues/main_dialog.py**

Dans une étape de dialogue, utilisez `begin_dialog` pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.

- Si l’utilisateur est déjà connecté, cela générera un événement de réponse symbolique, sans inciter l’utilisateur.
- Dans le cas contraire, cela incitera l’utilisateur à se connecter. Le service Azure Bot envoie l’événement de réponse symbolique après que l’utilisateur tente de se connecter.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

Dans l’étape de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente. Si ce n’est pas nul, l’utilisateur s’est connecté avec succès.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**dialogues/logout_dialog.py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a>Voir aussi

[Ajouter l’authentification via Azure Bot Service](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
